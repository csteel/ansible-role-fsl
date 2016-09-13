# FSL

"FSL is a comprehensive library of analysis tools for FMRI, MRI and DTI brain imaging data. It runs on Apple and PCs (both Linux, and Windows via a Virtual Machine), and is very easy to install. Most of the tools can be run both from the command line and as GUIs ("point-and-click" graphical user interfaces)." - [ FSL Home - FMRIB Software Library v5.0 ]( http://fsl.fmrib.ox.ac.uk/fsl/fslwiki/FSL )

## Notes

* First round Ansible role will run on Ubuntu 12.04.
* For per user configuration options see the **Users configuration file** section below.

* FSL runs on:
    * Linux
    * OSX
    * Windows

* Although install options currently offer a **libre** and **all** installation option, at this time only the **all** option seems to install.

* Install option descriptions:

    * **libre** - all software are DSFG-compliant, with permission to use, modify, re-distribute under any condition.
    * **all** - Up to user to determine licenses for all software.

* **fsl** could be an acemenu option.

    * Display README.Debian

### Itegration options (other Debian Packages)

* Octave
* Sun Grid Engine (SGE)
* Condor

## Resources

### Installation

* [ FSL Installation ]( http://fsl.fmrib.ox.ac.uk/fsl/fslwiki/FslInstallation )
* [ Oxford - FSL - FMRIB Software Library v5.0 - Download ]( http://fsl.fmrib.ox.ac.uk/fsl/fslwiki/FSL )
* [ Debian README.Debian - Setup Instructions ]( http://neuro.debian.net/debian/extracts/fsl/README.Debian )

### General

* [ The Debian Free Software Guidelines (DFSG) ]( https://www.debian.org/social_contract#guidelines )
* [ FSL Licence ]( http://fsl.fmrib.ox.ac.uk/fsl/fslwiki/Licence )

## Installation

### Ubuntu/Linux

* Debian/Ubuntu users should install FSL from the Neurodebian site:

    http://neuro.debian.net/pkgs/fsl-complete.html

* Ubuntu 12.04 LTS “Precise Pangolin” (precise) packages. The following two packages both install install version 5 / **5.0.7-1~nd12.04+1**.

    fsl-5.0-complete
    fsl-complete

### .profile

Adding the following to your .profile or .bashrc will ensure that 

#### edit ~/.profile

    nano ~/.profile
    
#### add something like this:

    # load user configuration
    if [ -f "/etc/fsl/5.0/fsl.sh" ] ; then
      . /etc/fsl/5.0/fsl.sh ;
    fi

to the end of your .profile file.

### Sources

Dartmouth NH, **all** option

    wget -O- http://neuro.debian.net/lists/precise.us-nh.full | sudo tee /etc/apt/sources.list.d/neurodebian.sources.list

### Add key and install

    sudo apt-key adv --recv-keys --keyserver hkp://pgp.mit.edu:80 0xA5D32F012649A5A9
	sudo apt-get update
    sudo apt-get install fsl-complete

## Users configuration

### .profile

    sudo su <user_name>
    nano ${HOME}/.profile
    
    # Source FSL
    if [ -f "/etc/fsl/5.0/fsl.sh" ] ; then
      . /etc/fsl/5.0/fsl.sh ;
    fi

### .fslconf/fsl.sh

Not required at this time.
Custom per user configurations should be installed here:

    nano ${HOME}/.fslconf/fsl.sh


