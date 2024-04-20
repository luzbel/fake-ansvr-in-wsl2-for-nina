# fake-ansvr-in-wsl2-for-nina
[![es](https://img.shields.io/badge/lang-es-yellow.svg)](https://github.com/luzbel/fake-ansvr-in-wsl2-for-nina/blob/master/README.md)

Scripts and procedures to use an updated version of astrometry.net from N.I.N.A. installed in WSL2 instead of ansvr

So you want to use a local version of astrometry.net from N.I.N.A. but…  
Don’t want to install Cygwin when WSL2 is a more modern and integrated option with Windows?  
Don’t trust the ansvr executable since it doesn’t publish the sources?  
Do you think the latest version of ansvr is not updated and does not have the latest versions of astrometry.net?  
Do you need a customized version of astrometry.net with some changes in the sources?
Does using astrotortilla also seem inconvenient for the same reasons?  
Don’t trust the executable distributed by https://www.hnsky.org/linux_subsyst and don’t feel like compiling the sources?  

Let’s use the Linux version of astrometry.net in WSL2 and trick N.I.N.A. into thinking it’s calling ansvr!

- Install WSL2 on Windows
-  Make sure to execute the following steps in the distribution marked as default in WSL2
	1. Install astrometry.net with your preferred distribution’s package system or by compiling from sources
	2. Rename /usr/bin/wcsinfo to /usr/bin/wcsinfo.elf
	3. Rename /usr/bin/wcsinfo to /usr/bin/wcsinfo.elf
	4. Download the solve-field and wcsinfo scripts from this repository and copy them to /usr/bin
	5. Make sure the scripts have 755 permissions (rwxr-xr-x) to be used by any user
- In Windows
	1. Create a directory so that N.I.N.A. thinks you have a Cygwin installed, for example in %USERPROFILE%\fakecygwin
	2. Create a bin subdirectory, for example in %USERPROFILE%\fakecygwin\bin
	3. Copy c:\Windows\System32\bash.exe to the bin directory created in the previous step
- In N.I.N.A.
	1. In the “Plate Solving” section of Options->Plate Solving choose “Local plate solver” as Plate Solver
	2. In the “Plate solver setting\Local plate solver” section of Options->Plate Solving
		- In the “Cygwin folder” section, select the fake Cygwin directory created (the base without the /bin)
	3. Use N.I.N.A. normally

You can open a WSL2 terminal and see the traces in /tmp/solve.txt or /tmp/wcs.txt 
Normally your Linux distribution in WSL2 purges this directory on each restart, so there is no file trace rotation mechanism. 
Don’t forget to copy these files if you want to keep traces of a session. 
If at any point the resolution becomes eternal because you have downloaded many catalogs and you are sure it will not resolve (for example, if by mistake you have taken a shot without removing the cap or the stars have moved) it is best to end the process from a WSL2 terminal with “pkill solve-field”. This avoids the N.I.N.A. process from becoming unresponsive. Remember that if you have configured “Local plate solver” both as “Plate solver” and as “Blind solver” you will have to execute a second pkill to finish the second resolution attempt.

Based on the proposed solution to use astrometry.net in WSL2 at https://www.hnsky.org/linux_subsyst"
