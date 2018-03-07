---
layout: post
title: "Duplicity: The Best Free Backup Software"
author: Eric Miller
category: Tutorial
tags: backup duplicity python freebsd
---

Lately, I've been looking into backups a lot. At one point, I even looked into setting up a
[Time Machine Server](/Tutorial/2017-12-12-Time-Machine-with-FreeBSD.md) on my FreeBSD machine.
That said, it's all been a headache that sometimes works and sometimes doesn't. Now, however, I've
discovered [Duplicity](https://launchpad.net/duplicity), a GPL software package, powered by python,
that is feature-heavy, simple, reliable, and *fast*.

## Features of Duplicity

* Relatively easy to automate
* Encrypts your backups by default
* Compresses your backups by default
* Takes incremental backups
* Can self-heal if a backup goes wrong
* Allows incremental restoration from backups
* Supports a lot of different protocols
* Supports AWS S3 very well by default.

A list of duplicity's supported protocols:

* acd_cli
* Amazon S3
* Backblaze B2
* Copy.com
* DropBox
* ftp
* GIO
* Google Docs
* Google Drive
* HSI
* Hubic
* IMAP
* local filesystem
* Mega.co
* Microsoft Azure
* Microsoft Onedrive
* par2
* Rackspace Cloudfiles
* rsync
* Skylabel
* ssh/scp
* SwiftStack
* Tahoe-LAFS
* WebDAV

## Security Considerations

Backups are a potentially huge security liability, because they can contain a lot of sensitive
information. Lots of times we want to back up information *because* it is sensitive. So we need to
consider the ramifications of our backup system. In particular, there are three systems we need to
consider when using duplicity.

1. The source machine
2. Data in transit
3. The backup server

Part of the key to ensuring good security is having sensible assumptions about the state and
security of your system. These assumptions depend on the nature of the machines in use, the nature
of the network, and whether you're using full disk encryption on the source and target machines.
Here are some assumptions I'm working with, if they're not true for you, then adjust your security
measures appropriately.

1. I am using duplicity's built-in PGP encryption. This protects the data on the target machine and in-transit.
2. Access to the source and target machines is restricted.

These two assumptions allow a generous amount of leeway in how we handle things. That said, they're
really a bare minimum for confidentiality, and do not necessarily guarantee integrity. Using a
secure transit protocol, like SFTP or S3, solves many of these problems. If you're using FTP over
the internet for example, you're wide-open to a man-in-the-middle attack. For that reason, I
recommend using a protocol that is already encrypted and password-protected.

## Basic Duplicity Usage

I have a script template that I use for my duplicity backups. I currently use a cloud solution for
file synchronization and offsite backups, and duplicity for larger local backups of size up to
about 200GB. My ISP has a data limit, so backing up to S3 would be impractical. Another thing to
consider if you're considering using S3 is cost – S3 costs $0.023 per gigabyte per month, which
gets expensive. If you want offsite backups, here's a quick price comparison.

| Service      | Storage | Price/GB/month | Price/month |
| ------------ | ------- | -------------- | ----------- |
| AWS S3       | 15GB    | $0.023         | $0.34       |
| AWS S3       | 50GB    | $0.023         | $1.30       |
| AWS S3       | 100GB   | $0.023         | $2.30       |
| AWS S3       | 200GB   | $0.023         | $4.60       |
| AWS S3       | 500GB   | $0.023         | $11.50      |
| AWS S3       | 1TB     | $0.023         | $23.00      |
| AWS S3       | 10TB    | $0.023         | $230.00     |
| Google Drive | 15G     | Free           | $0          |
| Google Drive | 100GB   | $0.0199        | $1.99       |
| Google Drive | 1TB     | $0.0100        | $9.99       |
| Google Drive | 10TB    | $0.0100        | $99.99      |
| DropBox      | 1TB     | $0.00825       | $8.25       |
| OneDrive     | 50GB    | $0.398         | $1.99       |
| OneDrive     | 1TB     | $0.00699       | $6.99       |

```bash
#!/bin/sh
# Duplicity needs an environment variable or arg to decrypt. This is the best way of doing that.
export PASSPHRASE="top_secret_password_for_encryption"
cd $HOME
backup_excludes="--exclude ./relative/path/1 --exclude ./relative/path/2"
backup_targets=$HOME
backup_server='192.168.x.y'
backup_server_proto='sftp'
backup_server_port='22'
# Generate a path based on our user and hostname. Ideally, this means there's a unique backup
# namespace for every user on every machine you need to worry about. Adjust this to meet your needs.
backup_server_path="/home/$(whoami)/backups/$(whoami).$(hostname | cut -d '.' -f 1)"
backup_dest="${backup_server_proto}://${backup_server}:${backup_server_port}/${backup_server_path}"
backup_parameters="$backup_excludes . ${backup_dest}"

ulimit -n 1024 # necessary on mac, on some linux distros

# Build the commands we're going to run in advance.
# The first command checks if there's a backup done within the last two weeks.
#   If so, does an incremental backup. If not, do a full backup.
# The second command removes any backups older than 2 weeks to save space.
#   If a full backup doesn't exist that's newer than the last two weeks, it doesn't delete the full
#   backup, just the incremental backups that have occurred since then.
full_if_old="incr --full-if-older-than 14D ${backup_parameters}"
remove_if_old="remove-older-than 14D ${backup_dest}"
incr="incr ${backup_parameters}"

# Print out the commands we're running to make debugging easier
echo duplicity ${full_if_old}
duplicity ${full_if_old}
echo duplicity ${remove_if_old}
duplicity ${remove_if_old}

unset PASSPHRASE
```

This script is designed to be *relatively* portable for different protocols and machines.
You may need some adjustments (for example, for the service authentication, or for some protocols'
sensitivities to file paths or hosts). Notably, this won't work for the `s3://` protocol because it
doesn't have access to AWS credentials, and it won't work for the `file://` protocol because it
forces you to use a hostname and port. These are relatively easy adjustments though.

### Fetching Duplicity Info

Using the same variables as above:

`duplicity collection-status ${backup_dest}` lists the backups that are available.

`duplicity restore ${backup_dest} ./local-folder` will restore the entire backup to the given
folder. Be aware that if the local folder is not empty, duplicity will throw an error.

`duplicity restore -t 1D --file-to-restore specific_file.txt ${backup_dest} restored-specific-file.txt`
will restore a single `specific_file.txt` to the state it was in one day ago, and put the result in
`restored-specific-file.txt` in the current directory.

`duplicity list ${backup_dest}` will list all of the files that were backed up.

Many of the options, like `-t` (restore time), can be used for various commands.

## In Closing

Duplicity is a very viable, effective, free, and portable backup solution. It does have its
downsides (single-threaded file access, currently somewhat inefficient) but for most people those
issues won't matter. I use it personally because of its backups and efficiency.
