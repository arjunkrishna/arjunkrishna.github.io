---
id: 32
title: 'Ubuntu &ndash; setting up Docker'
date: 2015-11-14T01:15:05+00:00
author: arjunkrishna
layout: post
guid: http://blog.arjunkrishna.us/?p=32
permalink: /2015/11/14/ubuntusetting-up-docker/
categories:
  - docker
  - how-to
  - ubuntu
---
  * **sudo apt-get update** 
      * **sudo apt-get -y upgrade** 
          * **sudo apt-get install linux-image-extra-&#8216;uname -r&#8217;** 
              * **sudo apt-key adv &#8211;keyserver hkp://pgp.mit.edu:80 &#8211;recv-keys 58118E89F3A912897C070ADBF76221572C52609D** 
                  * **echo &#8220;deb https://apt.dockerproject.org/repo ubuntu-trusty main&#8221; | sudo tee /etc/apt/sources.list.d/docker.list** 
                      * **sudo apt-get update** 
                          * **sudo apt-get install docker-engine** 
                              * **sudo nano /etc/default/ufw** 
                                  * change from DEFAULT\_FORWARD\_POLICY=&#8221;DROP&#8221; to DEFAULT\_FORWARD\_POLICY=&#8221;ACCEPT&#8221; 
                                      * Save and Close file. </ul> 
                                      * **sudo ufw reload** </ul>