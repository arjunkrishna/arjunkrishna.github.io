---
id: 63
title: Resize a fixed Virtual Box vdi file
date: 2016-04-18T20:09:34+00:00
author: arjunkrishna
layout: post
guid: http://blog.arjunkrishna.us/?p=63
permalink: /2016/04/18/resize-a-fixed-virtual-box-vdi-file/
categories:
  - how-to
---
&nbsp;

<pre class="lang:batch decode:true ">rem resize to 200 GB
rem convert a fixed vdi to dynamic; then resize and then convert it back to fixed style
cd C:\Program Files\Oracle\VirtualBox
VBoxManage clonehd "D:\VirtualBox VMs\win10-1\win10-1_fixed1.vdi" "D:\VirtualBox VMs\win10-2\win10-2_dyn.vdi" --variant Standard
VBoxManage modifyhd "D:\VirtualBox VMs\win10-2\win10-2_dyn.vdi" --resize 204800
VBoxManage clonehd "D:\VirtualBox VMs\win10-2\win10-2_dyn.vdi" "D:\VirtualBox VMs\win10-2\win10-2_fixed.vdi" --variant Fixed</pre>

&nbsp;

After this use gparted live iso to increase the size of the partition.

  * Download the iso fromÂ <http://gparted.sourceforge.net/download.php> (eg:Â gparted-live-0.25.0-3-i686.iso)
  * Via Virtual Box&#8217;s UI, 
      * turn on EFI,
      * load this iso to your virtual machine
      * reboot the VM from the ISO
  * Within gpartedÂ live boots 
      * Right-click the partition you want to enlarge
      * select Resize/Move and select the max available size.
  * Via Virtual Box&#8217;s UI 
      * turn off efi
      * unload the iso from virtual box
      * restart the vm

&nbsp;
