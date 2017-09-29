---
id: 100
title: 'Invoke Docker Installed on Windows 10 Creator&#8217;s Update via &#8220;Bash On Ubuntu on Windows&#8221;'
date: 2017-08-12T22:29:59+00:00
author: arjunkrishna
layout: post
guid: http://blog.arjunkrishna.us/?p=100
permalink: /2017/08/12/invoke-docker-installed-on-windows-10-creators-update-via-bash-on-ubuntu-on-windows/
categories:
  - Uncategorized
---
once in a blue moon when I need to run a bash script, I use git bash.. but wanted to try the new &#8220;bash on ubuntu on windows&#8221;. So trying to add my experiments in trying to make it work are below

<pre class="lang:c# decode:true ">"%ProgramFiles(x86)%\Git\bin\bash.exe" xyz.sh</pre>

&nbsp;

I looked at the following <a href="https://blog.jayway.com/2017/04/19/running-docker-on-bash-on-windows/" target="_blank" rel="noopener">link</a>

pre-requisite: you have already installed <a href="https://docs.docker.com/docker-for-windows/install/" target="_blank" rel="noopener">Docker for Windows</a>

&nbsp;

I did this to run my bash scripts that are part of the deployment folder of the repo containing docker images.

Before I cloned the repo which contained the shell scripts, I ran the following command for git to maintain the line feed

<pre class="lang:c# decode:true ">git config --global core.autocrlf false</pre>

also I cloned the repo under the following folder for simplicity

<pre class="lang:c# decode:true ">c:\Users\&lt;UserName&gt;\git</pre>

&nbsp;

On &#8220;creator&#8217;s update&#8221; Windows 10 install;

enable bash and configure it to call docker running on windows

<pre class="lang:default decode:true ">Windows+ I (opens windows settings)
Select "Developer Mode" radio button
Windows + R  (opens Run command)
type appwiz.cpl (to open programs and features)
select Turn Windows features on or off
check "Windows Subsystem for Linux (Beta)"
Open Bash On Ubuntu On Windows
the terminal window will open; set username and password for super user access
type "nano  .bashrc" (without double quotes)
add the following lines to the file
#call docker installed on windows from bash
PATH="$HOME/bin;$HOME/.local/bin:$PATH"
PATH="$PATH:/mnt/c/Program*Files/Docker/Docker/resources/bin"
alias docker=docker.exe
save and close the file.
sudo apt-get update
sudo apt-get upgrade
Open new instance of bash (Bash On Ubuntu On Windows)
type "docker --version"</pre>

&nbsp;

instead of alias you can also use the following, if alias gets deprecated.

Shell functions and aliases are limited to the shell and do not work in executed shell scripts. I&#8217;ll try creating a bin folder and then add the the docker functions shell scripts there and will try it out.

<pre class="lang:c# decode:true ">docker() {
/mnt/c/Program*Files/Docker/Docker/resources/bin/docker.exe "$@"
}
export -f docker

docker-compose() {
/mnt/c/Program*Files/Docker/Docker/resources/bin/docker-compose.exe "$@"
}
export -f docker-compose

docker-credential-wincred() {
/mnt/c/Program*Files/Docker/Docker/resources/bin/docker-credential-wincred.exe "$@"
}
export -f docker-credential-wincred

docker-machine() {
/mnt/c/Program*Files/Docker/Docker/resources/bin/docker-machine.exe "$@"
}
export -f docker-machine

notary {
/mnt/c/Program*Files/Docker/Docker/resources/bin/notary.exe "$@"
}
export -f notary</pre>

&nbsp;