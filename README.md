
ansible-role-fsl
================

An Ansible role for installing and configuring fsl.

## Description

"FSL is a comprehensive library of analysis tools for FMRI, MRI and DTI brain imaging data. It runs on Apple and PCs (both Linux, and Windows via a Virtual Machine), and is very easy to install. Most of the tools can be run both from the command line and as GUIs ("point-and-click" graphical user interfaces)." - [ FSL Home - FMRIB Software Library v5.0 ]( http://fsl.fmrib.ox.ac.uk/fsl/fslwiki/FSL )


Resources
---------

### Installation

-   [](files/recipe.md)
-   [ FSL Installation ]( http://fsl.fmrib.ox.ac.uk/fsl/fslwiki/FslInstallation )
-   [ Oxford - FSL - FMRIB Software Library v5.0 - Download ]( http://fsl.fmrib.ox.ac.uk/fsl/fslwiki/FSL )
-   [ Debian README.Debian - Setup Instructions ]( http://neuro.debian.net/debian/extracts/fsl/README.Debian )

### General

- [ The Debian Free Software Guidelines (DFSG) ]( https://www.debian.org/social_contract#guidelines )
- [ FSL Licence ]( http://fsl.fmrib.ox.ac.uk/fsl/fslwiki/Licence )



Requirements
------------

Any pre-requisites that may not be covered by Ansible itself or the role should be mentioned here. For instance, if the role uses the EC2 module, it may be a good idea to mention in this section that the boto package is required.

### ssh agent

```shell
eval `ssh-agent -s`
/usr/bin/ssh-add
```

### remove stale ssh keys

```shell
ssh-keygen -f "/home/ansible/.ssh/known_hosts" -R workstation-001
ssh-keygen -f "/home/ansible/.ssh/known_hosts" -R 144.222.111.11
```

### ensure for connectivity

Can we connect using ssh keypairs? 

```shell
ssh workstation-001
```

### Itegration options (other Debian Packages)

(Not implemented with this role at this time)

- Octave
- Sun Grid Engine (SGE)
- Condor



Role Variables
--------------

### roles/fsl/defaults/main.yml

```yaml
---
# defaults file for ansible-role-fsl

# fsl installation state

fsl_state         : present     # absent, present
fsl_src_state     : absent      # absent, present 

fsl_users_group   : aceresearchers
fsl_users_gid     : 80005

# fsl users id range

fsl_uid_min       : 60000	# minimum (LDAP) User Id Number
fsl_uid_max       : 65000     # maximum (LDAP) User Id Number

# key info

#fsl_keyserver_url: hkp://pgp.mit.edu:80
#fsl_key_id       : 0xA5D32F012649A5A9

# dartmouth nh

#deb http://neuro.debian.net/debian data main contrib non-free
##deb-src http://neuro.debian.net/debian data main contrib non-free

#deb http://neuro.debian.net/debian xenial main contrib non-free
##deb-src http://neuro.debian.net/debian xenial main contrib non-free

### ???

#deb http://neurodebian.ovgu.de/debian data main contrib non-free
##deb-src http://neurodebian.ovgu.de/debian data main contrib non-free

#deb http://neurodebian.ovgu.de/debian {{ ansible_distribution_release }} main contrib non-free
##deb-src http://neurodebian.ovgu.de/debian {{ ansible_distribution_release }} main contrib non-free
```


Dependencies
------------

None at this time.


Example Playbook
----------------


### fsl.yml

```shell
cd projectroot
cp roles/fsl/files/fsl.yml fsl.yml
```

```yaml
---
# file: {{ ansible_project }}/fsl.yml

- hosts: fsl
  become: true
  gather_facts: true
  pre_tasks:

    - set_fact: fact_controller_user="{{ lookup('env','USER') }}"
    - debug: var=fact_controller_user

    - set_fact: fact_controller_home="{{ lookup('env','HOME') }}"
    - debug: var=fact_controller_home

  roles:

    - fsl
```



    - hosts: fsl
      roles:
         - { role: fsl, fsl_src_state: 'present' }

## ansible-playbook

```shell
ansible-playbook -i inventory/dev systems.yml --limit "ace-ws-63" 
```

## Testing

```shell
vagrant up
```

Connect to vagrant host using X forwarding for testing...

```shell
vagrant ssh -- -X
```

```shell
sudo cat /etc/skel/.profile
. /etc/fsl/5.0/fsl.sh
echo $PATH
```

```shell
/usr/lib/fsl/5.0:/home/ansible/bin:/home/ansible/.local/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games:/usr/local/games:/snap/bin
which fsl
```

```shell
/usr/lib/fsl/5.0/fsl
```

### Environment

Test that the environment and command line tools are set up correctly: 

```
echo $FSLDIR
```

Output example:

```shell
/usr/share/fsl/5.0
```

### Path

Check your path: 

```shell
flirt -version
```

Output example:

```shell
FLIRT version 6.0
```

## License

MIT

## Author Information

Christopher Steel
Systems Administrator
McGill Centre for Integrative Neuroscience
Montreal Neurological Institute
McGill University
3801 University Street
Montréal, QC, Canada H3A 2B4
Tel. No. +1 514 398-2494
E-mail: christopherDOTsteel@mcgill.ca
[MCIN](http://mcin-cnim.ca/), [theneuro.ca](http://theneuro.ca)