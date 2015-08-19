# Install pfsense on a GPT disk

This script could be useful for people trying to install pfSense using GPT, specially needed 
on disks bigger than 2 Tb. On the pfSense installer for version 2.2 (at least in 2.2.4) 
only MBR is available.

By: Abilio Marques <https://github.com/abiliojr/>

Note: this script needs you to install pfsense in a specific way to properly work. It assumes your installation is made on a fresh formatted disk.

Please install pfSense as usual, but creating 3 partitions of the freebsd type:
  - 1 Mb (2048 sectors, used for alignment purposes)
  - System partition (the size you want, up to close to 2 Tb), mark as active
  - Extra partition, the remaining of the disk (*). In drives smaller than 2 Tb, you must guarantee it have at least 2 times the system RAM, as this script will need free space for the swap.

The installer will force you to resize the partitions. Go with smaller in the first and bigger in the system partition. Complete the installation by installing the bootloader and removing the swap (it will be recreated later by this script).
 
Proceed to reboot again from the thumb drive, this time wait or press C to boot to the liveCD. Enable ssh access, configure at least the LAN interface and get into the Shell. Copy this script from another computer by using scp. Check the variables named "drive" and "systemSlice". If you followed this guide, "systemSlice" would match. If your system has a single hard disk, "drive" would probably match.

Any extra space beyond the swap will be assigned to a data partition (including the space beyond the 2 Tb MBR limit. You must format it later in order to use it. Check the variables "dataPartitionFormat" and "dataPartitionName" for further customizations. They default to zfs and gptdata respectively.

Run the script. Then reboot the system from hard disk and continue configuring the pfSense as usual.

This code is published under the Simplified BSD License.

---

Copyright (c) 2015, Abilio Marques
All rights reserved.

Redistribution and use in source and binary forms, with or without
modification, are permitted provided that the following conditions are met:

1. Redistributions of source code must retain the above copyright notice, this
   list of conditions and the following disclaimer.
2. Redistributions in binary form must reproduce the above copyright notice,
   this list of conditions and the following disclaimer in the documentation
   and/or other materials provided with the distribution.

THIS SOFTWARE IS PROVIDED BY THE COPYRIGHT HOLDERS AND CONTRIBUTORS "AS IS" AND
ANY EXPRESS OR IMPLIED WARRANTIES, INCLUDING, BUT NOT LIMITED TO, THE IMPLIED
WARRANTIES OF MERCHANTABILITY AND FITNESS FOR A PARTICULAR PURPOSE ARE
DISCLAIMED. IN NO EVENT SHALL THE COPYRIGHT OWNER OR CONTRIBUTORS BE LIABLE FOR
ANY DIRECT, INDIRECT, INCIDENTAL, SPECIAL, EXEMPLARY, OR CONSEQUENTIAL DAMAGES
(INCLUDING, BUT NOT LIMITED TO, PROCUREMENT OF SUBSTITUTE GOODS OR SERVICES;
LOSS OF USE, DATA, OR PROFITS; OR BUSINESS INTERRUPTION) HOWEVER CAUSED AND
ON ANY THEORY OF LIABILITY, WHETHER IN CONTRACT, STRICT LIABILITY, OR TORT
(INCLUDING NEGLIGENCE OR OTHERWISE) ARISING IN ANY WAY OUT OF THE USE OF THIS
SOFTWARE, EVEN IF ADVISED OF THE POSSIBILITY OF SUCH DAMAGE.

The views and conclusions contained in the software and documentation are those
of the authors and should not be interpreted as representing official policies,
either expressed or implied, of the FreeBSD Project.
