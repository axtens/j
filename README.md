# j
A pushd/popd tool with symbols and extras written in [8th](https://8th-dev.com/).

j.8th is a command-line navigation tool wrapping the functionality of PUSHD and POPD, adding shortcuts and optional commands to run once the change of directory has been achieved.

j.8th is executed within the context of j.cmd. Shortcuts are stored in "j.json"  which is stored in "%USERPROFILE%\.j\". Both the folder and the file are created if they do not exist. Shortcuts are words which resolve to paths in the directory. j.8th provides tools for adding and listing shortcuts.

j.cmd at its simplest is
	@echo off
	8th c:\bin\j.8th "%~f0" %*

(j.cmd assumes that 8th.exe is on the PATH. If it's not there, add it to PATH or edit j.cmd to be explicit as to where 8th.exe may be found.)

The result of any given run of j.8th adds one or two lines to j.cmd.

The following are examples of command lines:

	C:\> j -add root "%CD%"

creates an entry in the j.json file, mapping "root" to "C:\" (using the %CD% substitution.)
	
	C:\> j root Users Bruce Downloads

changes the directory to C:\Users\Bruce\Downloads (using PUSHD)
	
	C:\Users\Bruce\Downloads> j 

Changes back to the previous directory (using POPD)
	
	C:\> j -l 

Lists the contents of j.json as symbol -> path
		
	C:\> j -a home "%USERPROFILE%" 

Creates an entry in j.json, mapping "home" to "C:\Users\Bruce"
	
	C:\> j home Downloads -i dir /w

Changes to C:\Users\Bruce\Downloads and then issues the "dir /w" command. "-i" means 'inline' in the sense that "dir/w" is appended to j.cmd 
	 
	C:\Users\Bruce\Downloads> j home Destkop # Machines -s mstsc Azure.rdp

Changes to C:\Users\Bruce\Desktop\#\Machines and then issues "mstsc Azure.rdp" using "START".
	
	C:\Users\Bruce\Desktop\#\Machines> j -h

Displays the help string:
```
Syntax: 
j 
[ [ -add | -a ] sym val | 
[ -delete | -d ] sym | 
-list | 
[ -help | -h ] | 
[ -jsondir path ] | 
[ -cmddir path ] ] | 
sym [subdir ...] [ -s shell_cmd | 
		-i inline_cmd ] | 
		<empty>
```
I started working with computers in 1977. Back then when there was only a command line (and sometimes not even that.) Despite the nice glossy front ends available nowadays I still live mostly on a command line: bash/fish in Linux/Mac or CMD (and occasionally PowerShell and wsl) in Windows. I had written a purely batch version but wanted some more functionality. 8th provided the tools for that functionality.

