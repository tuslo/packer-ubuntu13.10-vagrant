# Packer Ubuntu 13.10 box template

## Introduction

Shell provisioner scripts:
- apt.sh (headers, dev libs, vim, dkms, nfs, git, curl, ruby, augeas)
- build_time.sh
- cleanup.sh
- puppet.sh
- sudo.sh
- vagrant.sh
- vbox.sh

## Installation

The following instructions are specific to OSX.

### Requirements

- OSX 10.9
- Packer

### Install Packer

Download and install Packer (0.3.11+): http://www.packer.io/downloads.html

### Create Vagrant box

```sh
$ git clone https://github.com/mikekamornikov/packer-ubuntu13.10-vagrant
$ cd packer-ubuntu13.10-vagrant
$ packer build template.json
# finally "packer_virtualbox_virtualbox.box" will be created
```

## Notes

I used `veewee` template (https://github.com/jedi4ever/veewee/tree/master/templates) and `veewee-to-packer` gem (http://www.packer.io/docs/templates/veewee-to-packer.html) to create this config:

```sh
$ gem install veewee-to-packer
$ veewee-to-packer templates/ubuntu-13.10-server-amd64/definition.rb
```

Don't forget to add `vagrant` `post-installer` to your `template.json`:

```json
"post-processors": ["vagrant"]
```

Finally, i changed shell provisioner scripts to:
- Install `ruby` instead of compiling it
- Remove `chef installation and configuration
- Install `git`, `curl`, `augeas`

