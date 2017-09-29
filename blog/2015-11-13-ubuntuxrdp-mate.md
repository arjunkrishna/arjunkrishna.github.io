---
id: 29
title: 'Ubuntu&ndash;xrdp (mate)'
date: 2015-11-13T23:13:39+00:00
author: arjunkrishna
layout: post
guid: http://blog.arjunkrishna.us/?p=29
permalink: /2015/11/13/ubuntuxrdp-mate/
categories:
  - how-to
  - ubuntu
---
For a different user installed MATE desktop UI 

  * **sudo apt-get install xrdp**
  * **sudo apt-add-repository ppa:ubuntu-mate-dev/ppa**
  * **sudo apt-add-repository ppa:ubuntu-mate-dev/trusty-mate**
  * **sudo apt-get update** 
  * **sudo apt-get upgrade**
  * **sudo apt-get install ubuntu-mate-core ubuntu-mate-desktop**
  * **echo mate-session >~/.xsession**
  * **sudo service xrdp restart**
