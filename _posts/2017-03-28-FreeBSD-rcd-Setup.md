---
title: How to Make a Basic rc.d Script in FreeBSD
layout: post
author: Eric Miller
category: Tutorial
tags: FreeBSD
---

Recently, I wanted to make an rc.d script for my FreeBSD server, in order to include TeamCity in the 
`service` interface, which in FreeBSD is linked to the rc.d system, as opposed to Linux's systemd system.
I was unable to find an easy tutorial, until I stumbled upon a Minecraft forum where I found information on
a suitable script. The rc.d system is actually rather nice to work with, and in my opinion, confers more
power to the user than does systemd. This is largely thanks to the `/etc/rc.conf` file. That said, writing
an rc.d script is relatively easy once you understand how to do it.

The first step is to set up the script that tells `service` how to understand what to do. 
For the purpose of this tutorial, I'll call the service `myservice`. The first thing
to do is put a script in the `/usr/local/etc/rc.d/` folder. Name this file the name of your service, in
this case `myservice`. This means the absolute path of this file is `/usr/local/etc/rc.d/myservice`.
Finally, make this file executable using `chmod +x /usr/local/etc/rc.d/myservice`.

Now, edit the file. The first step is the hashbang, which should be put on the first line. This lets the 
program know how to start the script independently. Your file should look like this:

    #!/bin/sh
    
Next, we need to tell it how to use the rc subrouting. This is basically just boilerplate; add 
`. /etc/rc.subr` to the file. Your file will now look like this:

    #!/bin/sh
    
    . /etc/rc.subr
    
Now, it's time to put in some metadata so that rc.d understands some basic information about this service.
Again, this is, to some extent, boilerplate to work with the rc.d system.

    name="myservice" # How the service will be invoked from service
    rcvar="${name}_enable" # The variable in rc.conf that will allow this service to run
    load_rc_config $name # Loads the config file, if relevant.
    
Okay, this script is set up to work with the rc.d system. Now, we need to tell it what to do. The first
thing is to set up any environment variables your service may need. You may or may not need to do this,
depending on the nature of your service. Let's say `myservice` needs Java to run, so we need to add the
`JRE_HOME` environment variable.

    export JRE_HOME="/usr/local"
    
Excellent! Now it's time to tell service what to do when it uses particular commands. In this example, I'll
say we're using 3 commands: start, stop, and status. To do this, we set up a variable for each command,
where the value is the `sh` code to run. For complicated setups, you're best off setting this up to be an
independent file, or initializing these values as functions rather than variables. For the sake of
simplicity in the example, I'm going to use quick `sh` one-liners. For reference, the variable names we use
are `start_cmd`, `stop_cmd`, and `status_cmd`. Also note, in this example I'm assuming that `myservice`
starts as a daemon, and stores its PID in a file called `myservice.pid`.

    pidfile="/home/ericmiller/myservice/myservice.pid"
    start_cmd="/home/ericmiller/myservice/start ; echo MyService is now running on PID $(cat $pidfile)"
    stop_cmd="/home/ericmiller/myservice/stop ; echo MyService is not running. ; rm $(cat $pidfile)"
    status_cmd="if [ -e $pidfile ]; then echo MyService is running on PID $(cat $pidfile). ; return 1; fi; echo MyService is not running. ; return 0"
    
Okay, we're almost done. Now we just need to tell rc.d to run the appropriate command based on the user's
input. This is done with the following line:

    run_rc_command "$1"
    
Okay! That's all you need for the script. Here's what our `/usr/local/etc/rc.d/myservice` script looks like:

    #!/bin/sh
    
    . /etc/rc.subr
    
    name="myservice" # How the service will be invoked from service
    rcvar="${name}_enable" # The variable in rc.conf that will allow this service to run
    load_rc_config $name # Loads the config file, if relevant.
    
    export JRE_HOME="/usr/local"
    
    pidfile="/home/ericmiller/myservice/myservice.pid"
    start_cmd="/home/ericmiller/myservice/start ; echo MyService is now running on PID $(cat $pidfile)"
    stop_cmd="/home/ericmiller/myservice/stop ; echo MyService is not running. ; rm $(cat $pidfile)"
    status_cmd="if [ -e $pidfile ]; then echo MyService is running on PID $(cat $pidfile). ; return 1; fi; echo MyService is not running. ; return 0"
    
    run_rc_command "$1"
    
Now, there's one last step. If you try to run the service with `service start myservice`, it'll give you
a message telling you that you need to enable it in `/etc/rc.conf`. You can do this with one simple command:

    echo myservice_enable="YES" >> /etc/rc.conf
    
Congrats! Your rc.d script is set up and ready to go.
    