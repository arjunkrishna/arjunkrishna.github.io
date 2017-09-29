---
id: 50
title: Upload Folder via CURL/FTPS from a windows machine
date: 2015-12-25T23:03:07+00:00
author: arjunkrishna
layout: post
guid: http://blog.arjunkrishna.us/?p=50
permalink: /2015/12/25/upload-folder-via-curlftps-from-a-windows-machine/
categories:
  - how-to
---
simple dos script to upload folder using curl/ftps

<pre class="lang:batch decode:true ">@echo off 
set localdir=C:\test\
set ftpdir=test
set ftphost=&lt;ftp host&gt;
set ftpuser=&lt;ftp user&gt;
set ftppass=&lt;ftp password&gt;


setlocal enableDelayedExpansion

cd %localdir%
rem main directory
for /F %%x in ('dir /B/D %localdir%') do (
  set FILENAME=%localdir%\%%x
 c:\curl\curl.exe -T !FILENAME! ftps://%ftphost%/%ftpdir%/ --user %ftpuser%:%ftppass% -k --ftp-ssl
 )

rem sub-directories
for /F %%a in ('dir /ad /on /s /b "%localdir%"') do (	
	for /F %%x in ('dir /B/D %%a') do (
	  set FILENAME=%%a\%%x
	  set FOLDERNAME=%%a	 
	  rem here 8 is the length of localdir string. "c:\test\"
	  set FOLDERNAME2=!FOLDERNAME%:~8,-2!
	  c:\curl\curl.exe -T "!FILENAME!" --ftp-create-dirs ftps://%ftphost%/%ftpdir%/!FOLDERNAME2!/ --user %ftpuser%:%ftppass% -k --ftp-ssl 
	)
)

endlocal
</pre>

aboveÂ is an extension to an existing [solution](http://superuser.com/questions/590567/upload-folder-with-curl-and-ftp-using-batch-file-on-windows)Â as I needed only one level sub directories. For my final solution, I went with powershell. The solution I used to invoke curl from powershell was slow. If you can zip and upload your complete folder, then stick to that approach. This is only needed if due to some reason, you cannot unzip on the server side.

<pre class="lang:ps decode:true  ">#rem http://windowsitpro.com/powershell/running-executables-powershell
function Start-Executable {
  param(
    [String] $FilePath,
    [String[]] $ArgumentList
  )
  $OFS = " "
  $process = New-Object System.Diagnostics.Process
  $process.StartInfo.FileName = $FilePath
  $process.StartInfo.Arguments = $ArgumentList
  $process.StartInfo.UseShellExecute = $false
  $process.StartInfo.RedirectStandardOutput = $true
  if ( $process.Start() ) {
    $output = $process.StandardOutput.ReadToEnd() `
      -replace "\r\n$",""
    if ( $output ) {
      if ( $output.Contains("`r`n") ) {
        $output -split "`r`n"
      }
      elseif ( $output.Contains("`n") ) {
        $output -split "`n"
      }
      else {
        $output
      }
    }
    $process.WaitForExit()
    & "$Env:SystemRoot\system32\cmd.exe" `
      /c exit $process.ExitCode
  }
}


function _UploadViaFTPSCurl($path, $ftpurl, $ftpfolder, $credentials)
{
   foreach ($item in Get-ChildItem $path)
   {
        if (Test-Path $item.FullName -PathType Container)
        {
            $ftpurlparam = $ftpurl+""+$ftpfolder+"/"
            _UploadViaFTPSCurl $item.FullName $ftpurlparam $item.Name $credentials
        }
        else
        {
            $url =  $ftpurl +""+ $ftpfolder
            $itemFullName = $item.FullName	       
            $params = @("-T ""$itemFullName"" --ftp-create-dirs $url/ --user $credentials -k --ftp-ssl")
            Write-Host $params
            Start-Executable "curl.exe" $params
        }

    }
} 

$path="C:\Test"
$ftpurl = "ftps://&lt;ftp server name&gt;/"
$ftpfolder = "test"
$credentials = "&lt;ftp username&gt;:&lt;ftp password&gt;"
_UploadViaFTPSCurl $path $ftpurl $ftpfolder $credentials</pre>

&nbsp;