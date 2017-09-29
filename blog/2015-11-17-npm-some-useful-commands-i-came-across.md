---
id: 45
title: 'NPM  &#8211;  some useful commands I came across'
date: 2015-11-17T00:15:24+00:00
author: arjunkrishna
layout: post
guid: http://blog.arjunkrishna.us/?p=45
permalink: /2015/11/17/npm-some-useful-commands-i-came-across/
categories:
  - npm
---
  * npm init
  * npm install gulp &#8211;save-dev
  * npm install gulp-concat &#8211;save-dev
  * npm install gulp-uglify &#8211;save-dev
  * npm install del &#8211;save-dev
  * npm install gulp-ng-annotate &#8211;save-dev

&nbsp;

  * npm ls -g &#8211;depth=0
  * npm install -g <gulp@latest>
  * npm uninstall -g npm

&nbsp;

  * gulpfile.js
  * <pre class="lang:js decode:true ">var gulp = require("gulp");
var rimraf = require("rimraf");
var concat = require("gulp-concat");
//var cssmin = require("gulp-cssmin");
var uglify = require("gulp-uglify");
var ngAnnotate = require('gulp-ng-annotate');

/** Merge all application js files into a single app.js */
gulp.task('minifyApp', function(){
    /*Merge all js components */
    gulp.src(['app/**/*.js'])
        .pipe(concat('app.js'))
        //Perform some static analysis on the bundles angular js file
        .pipe(ngAnnotate())
        .pipe(gulp.dest('.'));

});


gulp.task('default', ["minifyApp"]);</pre>
    
    &nbsp;</li> </ul> </ul> 
    
    &nbsp;