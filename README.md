# aubio-Vagrant-Script
Project to cross-compile aubio for Windows automatically.

This script provides an easy and reproducable way to cross-compile any version of aubio for Windows (x86 and x64).
You don't have to install a linux and mingw yourself!

This script creates a virtual machine running ubuntu linux in your local VirtualBox.
It updates linux, installs all needed packages including the gcc-mingw-w64 cross-compiler.
After that is runs the build_mingw script, which is included in the aubio sources.
Finally, it copies the created zip packages and the sha256 checksum files back to your Windows file system.


## Requirements

1. Install Vagrant from: https://www.vagrantup.com/

2. Install Oracle VirtualBox from: https://www.virtualbox.org/. __NOTE:__ Don't use the latest version of VirtualBox. Please read: https://www.vagrantup.com/docs/virtualbox/

3. Download the aubio sources you want to cross-compile (aubio version 0.4.4 or higher).
   Version 0.4.4 was the first released version with the build_mingw script.
   - latest version: https://github.com/aubio/aubio
   - older releases: https://aubio.org/pub/


## Installation & Usage

0. Install required software (see Requirements)

1. Unpack this project to a local folder

2. Unpack the downloaded aubio sources to the `to_build` folder
   -> The files of the aubio root folder should be in `to_build`

3. Start your Command Prompt (`cmd`) and go to the folder with the Vagrantfile

4. Run command: `vagrant up`

5. Go and get another cup of coffee :)
   -> or 2 or 3 ... it takes a while to install and update the virtual machine at first start

If Vagrant has completed the build process, you will find the ZIP files for the cross-compiled
win32 and win64 aubio lib in the `out` folder.

   
## Troubleshooting

### Problem 1
Running any `vagrant` command in the cmd of my Windows 10 doesn't do nor output anything.
It just returns.

Solution:
On my system the problem was resolved by defining the environment variable `VAGRANT_LOG` and
set it to `warn`.

### Problem 2
Vagrant has problems with VirtualBox (i.e. cannot install tools and packages to the VM).

Solution:
Don't use the latest version of VirtualBox.
You need a version of VirtualBox, which is comaptible to the VirtualBox Provider of Vagrant.
Please read: https://www.vagrantup.com/docs/virtualbox/

## License

This script is released under the MIT License.

ATTENTION:
Only this script (Vagrantfile) is licensed under the MIT License!
Other software may NOT (like Oracle VirtualBox, aubio or parts of optional libs to enhance aubio functionality)!
