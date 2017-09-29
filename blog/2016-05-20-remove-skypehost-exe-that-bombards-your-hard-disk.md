---
id: 83
title: remove skypehost.exe that bombards your hard disk
date: 2016-05-20T19:57:59+00:00
author: arjunkrishna
layout: post
guid: http://blog.arjunkrishna.us/?p=83
permalink: /2016/05/20/remove-skypehost-exe-that-bombards-your-hard-disk/
categories:
  - how-to
  - powershell
---
I came home today from work to see 100% disk usage on my ssd. After looking at the task manager saw skypehost.exe bombarding my ssd.

I just simply uninstalled it.

<pre class="lang:ps decode:true ">Get-AppxPackage | Select Name, PackageFullName
 Get-AppxPackage *Messaging* | Remove-AppxPackage
 Get-AppxPackage *skypeapp* | Remove-AppxPackage</pre>

&nbsp;
