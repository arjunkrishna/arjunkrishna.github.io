---
id: 86
title: Unable to remove node-modules folder from Windows machine.
date: 2016-09-24T20:20:32+00:00
author: arjunkrishna
layout: post
guid: http://blog.arjunkrishna.us/?p=86
permalink: /2016/09/24/unable-to-remove-node-modules-folder-from-windows-machine/
categories:
  - npm
---
original post:Â <http://t.co/0pV4OSTG1L>

Install rimrafÂ (<https://www.npmjs.com/package/rimraf>Â is a deep deletion module)

<pre class="lang:batch decode:true">npm install rimraf -g
</pre>

within the project folder run the following command to remove the folder

<pre class="lang:batch decode:true ">rimraf node_modules</pre>

&nbsp;
