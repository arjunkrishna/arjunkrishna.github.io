---
id: 71
title: Useful Powershell scripts
date: 2016-04-19T22:03:08+00:00
author: arjunkrishna
layout: post
guid: http://blog.arjunkrishna.us/?p=71
permalink: /2016/04/19/useful-powershell-scripts/
categories:
  - how-to
  - powershell
---
### Steps to create your profile file (perform these steps as admin within powershellÂ command prompt) {#ecxUsefulPowershellcommands-Stepstocreateyourprofilefile}

<pre class="lang:ps decode:true ">$profile
test-path $profile
#if false then create a new file for your user account
new-item -path $profile -itemtype file -force
notepad $profile
Set-ExecutionPolicy unrestricted</pre>

### Create powershell functions and store them in your profile file {#ecxUsefulPowershellcommands-Createapowershellfunctionandstoretheminyourprofilefile}

<pre class="lang:ps decode:true ">function _pskill ($processName="") {Get-Process | Where { $_.Name -Eq $processName } | Kill} 
function _pskillMultipleProcesses ($processName="") {Get-Process $processName | Kill} 
function _pskillInstance ($processName="", $windowTitleText) {Get-Process $processName | Where-Object { $_.MainWindowTitle â€“like â€˜*'+$windowTitleText+'*â€™ } | Kill} 
function pro { notepad $profile }
function _touch ($fileName="") {(Get-Item $fileName).lastwritetime=$(Get-Date)} 
function _touch1 ($fileName="", $date) {(Get-Item $fileName).lastwritetime=$(Get-Date $date)} 
function _copyToDesktop ($filename) {Copy-Item $filename ([Environment]::GetFolderPath("Desktop"))}
function _listSpecialFolders { [enum]::getvalues([system.environment+specialfolder]) | foreach {"$_ maps to " + [system.Environment]::GetFolderPath($_)}}
function _open ($pathOrFile=".") {ii $pathOrFile}
function _removeLeadingZeroes($stringValue) { $stringValue -replace '\b0+\B'}
function _tail($filename) {gc $filename -wait}
function _whoamI {[System.Security.Principal.WindowsIdentity]::GetCurrent()}
 
function _FolderSize($Path=$home) {
$code = { ('{0:0.0} MB' -f ($this/1MB)) }
Get-ChildItem -Path $Path |
Where-Object { $_.Length -eq $null } |
ForEach-Object {
Write-Progress -Activity 'Calculating Total Size for:' -Status $_.FullName
$sum = Get-ChildItem $_.FullName -Recurse -ErrorAction SilentlyContinue |
Measure-Object -Property Length -Sum -ErrorAction SilentlyContinue
$bytes = $sum.Sum
if ($bytes -eq $null) { $bytes = 0 }
$result = 1 | Select-Object -Property Path, TotalSize
$result.Path = $_.FullName
$result.TotalSize = $bytes | 
Add-Member -MemberType ScriptMethod -Name toString -Value $code -Force -PassThru
$result
}
}
function _outExcelReport
{
param ($Path = "$env:temp\$(Get-Random).csv")
$Input | Export-Csv -Path $Path -Encoding UTF8 -NoTypeInformation -UseCulture
ii -Path $Path
}
function _ProductKey { 
$map="BCDFGHJKMPQRTVWXY2346789"
$value = (get-itemproperty "HKLM:\SOFTWARE\Microsoft\Windows NT\CurrentVersion").digitalproductid[0x34..0x42] 
$ProductKey = ""
for ($i = 24; $i -ge 0; $i--) { 
$r = 0 
for ($j = 14; $j -ge 0; $j--) { 
$r = ($r * 256) -bxor $value[$j] 
$value[$j] = [math]::Floor([double]($r/24)) 
$r = $r % 24 
} 
$ProductKey = $map[$r] + $ProductKey
if (($i % 5) -eq 0 -and $i -ne 0) { 
$ProductKey = "-" + $ProductKey
} 
} 
$ProductKey
} 
function applist { Get-WmiObject -Class Win32_Product | Select-Object -Property Name }
function EasyView { process { $_; Start-Sleep -seconds .5}}</pre>

&nbsp;
