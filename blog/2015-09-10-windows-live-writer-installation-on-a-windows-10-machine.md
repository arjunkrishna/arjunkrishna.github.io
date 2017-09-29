---
id: 22
title: 'Windows Live Writer &ndash; Installation on a Windows 10 machine.'
date: 2015-09-10T22:53:55+00:00
author: arjunkrishna
layout: post
guid: http://blog.arjunkrishna.us/?p=22
permalink: /2015/09/10/windows-live-writer-installation-on-a-windows-10-machine/
categories:
  - how-to
---
<p align="justify">
  I found this helpful hint <a href="http://iunknownme.com/blog/2015/04/16/installing-windows-live-writer-2012-on-windows-10-technical-preview/" target="_blank">here</a> and thought of making this my first post.
</p>

  * Download installation file from <http://wl.dlservice.microsoft.com/download/C/1/B/C1BA42D6-6A50-4A4A-90E5-FA9347E9360C/en/wlsetup-all.exe>
  * Open command prompt 
      * Navigate to the local folder where the file was downloaded
      * run the following command 
          * **wlsetup-all.exe /AppSelect:Writer /q /log:C:\InstallationLog\WLW.Log /noMU /noHomepage /noSearch**