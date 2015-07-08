# Work-Stuff
installation script from work
(upload as .bat from home)

code:
ECHO off

	SET regfilename=regbackup%date:~0,3%%date:~-7,2%%date:~-4,4%

	CLS


ECHO ________________________________________________________
ECHO.
ECHO ### Copying files for OEM information...
ECHO.

	COPY /Y "%userprofile%\Desktop\Windows 7 - Copy to Desktop\system32\*.*" c:\windows\system32\

ECHO ### Backing up the Registry...

	IF NOT EXIST "c:\Registry" MKDIR "c:\Registry"

	IF EXIST "c:\Registry\%regfilename%.reg" GOTO merge
		regedit /e "c:\Registry\%regfilename%.reg"

:merge

ECHO ### Merging OEM registry settings...

  :: Create temporary REG file
  > %TEMP%.\oem.reg ECHO Windows Registry Editor Version 5.00
  >>%TEMP%.\oem.reg ECHO.
  >>%TEMP%.\oem.reg ECHO [HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\OEMInformation]
  >>%TEMP%.\oem.reg ECHO "Logo"="C:\\Windows\\System32\\oemlogo.bmp"
  >>%TEMP%.\oem.reg ECHO "Manufacturer"="Exact Computers and Home Entertainment"
  >>%TEMP%.\oem.reg ECHO "SupportHours"="Mon-Fri 9am-5pm"
  >>%TEMP%.\oem.reg ECHO "SupportPhone"="(02) 6056 5746"
  >>%TEMP%.\oem.reg ECHO "SupportURL"="http://www.exactcomputers.com.au"
  >>%TEMP%.\oem.reg ECHO.

	
	:: Merge (import) the REG file to add OEM details
  REGEDIT /S %TEMP%.\oem.reg
  
  :: Delete the temporary REG file
  DEL %TEMP%.\oem.reg


ECHO ________________________________________________________
ECHO.
ECHO ### Finished

start %userprofile%\Desktop\"Windows 7 - Copy to Desktop"\Adobe\"ADOBE READER 11"\setup.exe

start %userprofile%\Desktop\"Windows 7 - Copy to Desktop"\"Remote help WindowsAgentSetup"

start %userprofile%\Desktop\"Windows 7 - Copy to Desktop"\"BIT Pro"\bit.exe

start %userprofile%\Desktop\"Windows 7 - Copy to Desktop"\"BIT Pro"\"BurnInTest Professional V5 License Key".txt

echo change BIT settings then continue
pause

start %userprofile%\Desktop\"Windows 7 - Copy to Desktop"\"BIT Pro"\bit.exe

exit
	
