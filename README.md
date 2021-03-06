# man page for deb-client
## NAME 
**deb-client** manages the local debian trusted key database and remote installation repository databases. It allows the user to indicate from what repository they wish to install additional packages and with what key the authenticity of the downloads from the repository are to be verified.

## SYNOPSIS
**deb-client** [objectPath] [ objectId1 ... objectIdN ] -action [ actionArg1 .. actionArgM]

## DESCRIPTION 
### key
Use this object path to manage an individual key in the debian trusted repository key database.

### keys
Use this object path to manage the entire collection of debian trusted repository keys.

### repo
Use this object path to manage an individual remote installation repository. You can declare it in your system or remove its declaration.

### repos
Use this object path to manage the entire collection of remote installation repositories for your debian-based or debian-derived system.

### repo.url.release
Use this object path to declare a repository's url and release.

## OPTIONS

### --help
shows the general help paragraph.

### [objectpath] --help
shows general help for the object path.

### --version
shows the program's version.

### --license
shows the program's license.

### key [obj] -remove
This command removes a trusted key from the debian trusted key database. Example:  
**deb-client** key info@garagesoft.com -remove  
The key is represented by either an email address (if it is unique in the trusted key database) or else by a key ID. Example:  
**deb-client** key FBB75451 -remove  
You must run this command either as root or with sudo privileges.
### key [obj] -add
This command adds a key from a url to the debian trusted keys database. Example:  
**deb-client** key http://packages.garagesoft.com/garagesoft.pubkey -add  
As the public repository keys are generally distributed by download, you need to enter a download url. Any url protocol (http, ftp, ...) supported by the 'wget' program is acceptable. You must run this command either as root or with sudo privileges.

### keys -show
This command lists the keys in the debian trusted key database. Example:  
**deb-client** keys -show  
ftpmaster@ubuntu.com                     437D05B5   Ubuntu Archive Automatic Signing Key  
cdimage@ubuntu.com                       FBB75451   Ubuntu CD Image Automatic Signing Key  
ftpmaster@ubuntu.com                     3E5C1192   Ubuntu Extras Archive Automatic Signing Key  
linux@dropbox.com                        5044912E   Dropbox Automatic Signing Key  
The first column is the email address that identifies the key. The second column is the keyID, and the third column is the signatory's name.
### repo [obj] -remove
This command removes an additional, remote debian repository. Example:  
**deb-client** repo noobslab-swar-themes-precise.list -remove  
The argument to supply is a repository declaration file, typically ending in the '.list' extension. You must run this command either as root or with sudo privileges.

### repos -show
This command shows the list of additional repositories in a debian system. Each repository/release is declared in its own file. Example:  
**deb-client** repos -show  
file                                     url                                                     release  
indiestor-precise.list                   http://packages.indiestor.com/apt/ubuntu                precise          
noobslab-swar-themes-precise.list.save   http://ppa.launchpad.net/noobslab/swar-themes/ubuntu    precise          
precise-partner.list                     http://archive.canonical.com/ubuntu                     precise          
The first column is the file in which the repository/release has been declared. The second column is the url from which the debian package management system will download packages. The third column is the release from which the debian package system will download packages.
### repo.url.release.arg.arg [obj] -add
This command adds a remote debian repository to the debian package management system. Synopsis:  
sudo repo [reponame] [url] [release] -add  
Example:  
sudo repo indiestor http://packages.indiestor.com/apt/ubuntu precise -add  
The _reponame_ parameter is only used to give a name to the additional repository declaration file. You can freely choose this name, as long as it is a valid filename. The reponame will help you to recognize the repository, if you ever want to remove it.

## EXIT-STATUS 
### 0
A zero exit code means that everything went ok.
### 1
A one exit code is usually an error generated by **deb-client** itself.
### other
Another exit code is always an error generated by one of the underlying programs invoked by **deb-client**.

## FILES 
### /etc/apt
This folder contains the overall database of trusted keys and remote installation repositories for a debian-style system.

### /etc/apt/sources.list
This is the main table in which the system's default remote repositories have been declared during installation. **deb-client** does not manage this file, as **deb-client** only manages additional remote package installation repositories.

### /etc/apt/sources.list.d
This directory contains a file per additional remote package installation repositories. **deb-client** declares each additional remote package installation repository in this folder.

### /etc/apt/trusted.gpg
This file is the trusted key database. For each remote package installation repository declared, it must contains an entry with a trusted key. Multiple repositories can have the same key, if they are being managed by the same entity. All package downloads are verified by the package management system for authenticity using these keys.

## AUTHOR
Erik Poupaert <erik@sankuru.biz>

## REPORTING-BUGS
Report bugs to: erik@sankuru.biz

# COPYRIGHT
Licensed under: GPL
