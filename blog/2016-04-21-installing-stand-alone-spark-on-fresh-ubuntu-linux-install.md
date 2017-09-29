---
id: 78
title: Installing Stand-alone Spark on fresh ubuntu linux install
date: 2016-04-21T23:02:50+00:00
author: arjunkrishna
layout: post
guid: http://blog.arjunkrishna.us/?p=78
permalink: /2016/04/21/installing-stand-alone-spark-on-fresh-ubuntu-linux-install/
categories:
  - how-to
  - ubuntu
---
I looked at the following links :Â <a href="https://www.dezyre.com/apache-spark-tutorial/apache-spark-installation-tutorial" target="_blank">install spark</a>, <a href="http://dmitrypukhov.pro/install-apache-spark-on-ubuntu/" target="_blank">install spark with hadoop</a>Â &Â <a href="http://www.liberiangeek.net/2014/03/daily-ubuntu-tips-manually-install-oracle-java-jdk-8-in-ubuntu/" target="_blank">install jdk</a>

&nbsp;

<pre class="lang:sh decode:true ">mkdir apps
chmod 777 â€“R ./apps

#installing jdk

wget --no-cookies --no-check-certificate --header "Cookie: gpw_e24=http%3A%2F%2Fwww.oracle.com%2F; oraclelicense=accept-securebackup-cookie" "http://download.oracle.com/otn-pub/java/jdk/8u51-b16/jdk-8u51-linux-x64.tar.gz"

tar xzf jdk-8u51-linux-x64.tar.gz

#create folder for jdk under /usr/lib
sudo mkdir -p /usr/lib/jvm/jdk1.8.0/
sudo mv jdk1.8.0_51/* /usr/lib/jvm/jdk1.8.0/
#begin configuring Java, enable javac, javaws
sudo update-alternatives --install "/usr/bin/java" "java" "/usr/lib/jvm/jdk1.8.0/bin/java" 1
sudo update-alternatives --install "/usr/bin/javac" "javac" "/usr/lib/jvm/jdk1.8.0/bin/javac" 1
sudo update-alternatives --install "/usr/bin/javaws" "javaws" "/usr/lib/jvm/jdk1.8.0/bin/javaws" 1
#check java installation
java â€“version


#download spark
wget http://shinyfeather.com/spark/spark-1.6.1/spark-1.6.1-bin-hadoop2.6.tgz
mkdir /opt/spark
tar -xvf spark-1.6.1-bin-hadoop2.6.tgz -C /opt/spark
ln -s /opt/spark/spark-1.6.1-bin-hadoop2.6 spark
cd ~
nano .bashrc
SPARK_HOME=/root/apps/spark
export PATH=$SPARK_HOME/bin:$PATH
#after saving, then source the updated file.
source  ~/.bashrc

spark-shell
sc.version</pre>

&nbsp;