---
id: 59
title: Windows computer waking up immediately after sleeping
date: 2016-01-15T21:06:29+00:00
author: arjunkrishna
layout: post
guid: http://blog.arjunkrishna.us/?p=59
permalink: /2016/01/15/windows-computer-waking-up-immediately-after-sleeping/
categories:
  - how-to
---
  * Navigate to device manager
  * Network Adapters
  * Choose a network adapterâ€™s property (right click)
  * Power Management tab
  * Un-Check â€œAllow this device to wake the computer.â€

  * Command to check who woke your computer last
  * **powercfg â€“ lastwake**

  * Details on devices which are configured to wake up your computer
  * **powercfg â€“devicequery wake_armed**
