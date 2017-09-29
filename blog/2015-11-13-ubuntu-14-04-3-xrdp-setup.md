---
id: 25
title: 'Ubuntu &#8211; xrdp setup'
date: 2015-11-13T21:21:18+00:00
author: arjunkrishna
layout: post
guid: http://blog.arjunkrishna.us/?p=25
permalink: /2015/11/13/ubuntu-14-04-3-xrdp-setup/
categories:
  - how-to
  - ubuntu
---
I was trying to setup xrdp on ubuntu 14.04.3 so that I can RDP into it from my windows machine. This is what worked for me.

&nbsp;

  * Open the terminal 
      * **sudo apt-get install xrdp** 
          * **sudo apt-get update** 
              * **sudo apt-get install xfce4** 
                  * **echo xfce4-session >~/.xsession** 
                      * **sudo service xrdp restart** 
                          * **hostname –I** 
                              * **note down the ip address**</ul> 
                          * **On a windows machine** 
                              * **Windows + R** 
                                  * **mstsc** 
                                      * **type in the IP address of the remote linux machine** 
                                          * **type in the username and password** 
                                              * **done.**</ul> </ul>