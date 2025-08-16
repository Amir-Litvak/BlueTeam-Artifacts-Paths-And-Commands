# Paths And Commands For Forensics (And some other useful information)
## Browsers
### History File Location:
```
#Windows:
  Chrome:
    C:\Users\<username>\AppData\Local\Google\Chrome\User Data\Default
    C:\Users\<username>\AppData\Local\Google\Chrome\User Data\Default\Cache
  FireFox:
    C:\Users\<username>\AppData\Roaming\Mozilla\Firefox\Profiles\
    C:\Users\<username>\AppData\Roaming\Mozilla\Firefox\Profiles\<profile>\places.sqlite
  Edge:
    C:\Users\<username>\AppData\Local\Microsoft\Edge\User Data\Default\
  Opera:
    C:\Users\<username>\AppData\Roaming\Opera Software\Opera Stable\

#MacOS:
  Chrome:
    /Users/<username>/Library/Application Support/Google/Chrome/Default
    /Users/<username>/Library/Caches/Google/Chrome/Default/Cache
  Safari:
    /Users/{user}/Library/Safari/History.db

#Linux:
  Chrome:
    /home/<username>/.config/google-chrome/Default
    /home/<username>/.cache/google-chrome/Default/Cache
  Firefox: 
    /home/<username>/.mozilla/firefox/<profile_folder>/places.sqlite
```

### Windows Cookies stored location:
```
AppData\Roaming\Microsoft\Windows\Cookies
(Tracks user activity, including opened documents)

Chrome:
  AppData\Local\Google\Chrome\User Data\Default\Cookies
Firefox:
  AppData\Roaming\Mozilla\Firefox\Profiles\<profile>\cookies.sqlite
Edge:
  AppData\Local\Microsoft\Edge\User Data\Default\Cookies

```

### Locate the lastupdated Windows Chrome history file (Command):
```
gci 'C:\Users\*\AppData\Local\Google\Chrome\User Data\*\History' | select FullName, LastWriteTime | sort LastWriteTime
```
### Locate the lastupdated Mac\Linux Chrome history file (Command):
```
find /Users/*/Library/"Application Support"/Google/Chrome/* -name "History" -type f -exec stat -f "%Sm %N" -t "%Y-%m-%d %H:%M:%S" {} + | sort
```


## Web Service Logs Location
### Windows Web Service Logs Location:
```
# Apache HTTP Server:
C:\Program Files\Apache Group\Apache2\logs\
C:\Apache24\logs\

# Nginx:
<nginx_install_dir>\logs\

# Microsoft IIS:
%SystemDrive%\inetpub\logs\LogFiles\

# Tomcat:
C:\tomcat\logs\
```

### Linux Web Service Logs Location:
```
# Apache HTTP Server
/var/log/apache2/
/var/log/httpd/
/var/log/apache2/access.log
/var/log/apache2/error.log

# Nginx
/var/log/nginx/access.log
/var/log/nginx/error.log

#Tomcat
/opt/tomcat/logs/
```


## System
### System Logs Location
```
#Windows:
C:\Windows\System32\winevt\Logs

#Mac\Linux:
/var/log/
```

### Windows Execution Logs
```
AppData\Local\Microsoft\Windows\WebCache\
```

### Recent: Tracking Opened Files and Folders
```
C:\Users\<username>\AppData\Roaming\Microsoft\Windows\Recent\
```

### Prefetch: Tracking Executed Programs
```
C:\Windows\Prefetch\
```


### Prefetch: Tracking Executed Programs
```
C:\Windows\Prefetch\
```

### Registry Analysis
```
#System-wide registry hives - HKEY_LOCAL_MACHINE (HKLM):
  C:\Windows\System32\Config\SAM
                            \SYSTEM
                            \SOFTWARE
                            \DEFAULT


#User-specific registry settings - HKEY_CURRENT_USER (HKCU):
  C:\Users<username>\NTUSER.DAT

#Commonly used by attackers to mainain persistance:
  HKCU\Software\Microsoft\Windows\CurrentVersion\Run
  HKCU\Software\Microsoft\Windows\CurrentVersion\RunOnce

#USB Device History:
  HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Enum\USBSTOR

```

### Firewall Log File Location
```
C:\Windows\System32\LogFiles\Firewall\pfirewall.log
```

### Event Log IDs
```
#Windows Event Logs provide a chronological record of system and security events. They are essential for tracking:
  User logins and authentication attempts (Security Log - Event ID 4624 & 4625).
  Failed login attempts and account lockouts (Event ID 4740).
  Process creation and software execution (Event ID 4688).
  User Account Created (Event ID 4720).
  USB Device Plugged In (Event ID 2003).
  System startup, shutdown, and crashes (System Log).
  Service and driver activity (Application and System Logs)
```

## Windows Commands:
```
Process List:
  wmic.exe process get /format:csv
Services:
  wmic.exe service get /format:csv
ActiveNetConnections:
  netstat.exe -abno
List Shared Resources:
  net view \\<computer_name>
List all shared folders:
  Get-SmbShare
List Stored Wi-Fi Profiles:
  netsh wlan show profiles
Collect System Information:
  systeminfo > "%OutputDir%\SystemInfo.txt"
View Current Firewall Logging Settings:
  netsh advfirewall show allprofiles
Export Wi-Fi Profiles for Forensic Analysis:
  netsh wlan export profile folder=C:\WiFi-Backup key=clear
Extract User Accounts:
  net user > "%OutputDir%\Users.txt"
Netword Configuration Details:
  ipconfig /all > "%OutputDir%\NetworkConfig.txt"
Extract Active DNS Cache:
  ipconfig /displaydns > "%OutputDir%\DNSCache.txt"
ScheduledTasks:
  schtasks.exe /query /v /fo CSV
Extract Running Services:
  sc query > "%OutputDir%\Services.txt"
List Running Processes:
  tasklist /FI "USERNAME eq NT AUTHORITY\SYSTEM" > "%OutputDir%\RunningProcesses.txt"
Wmic Installed Programs:
  wmic.exe product get Caption,Description,IdentifyingNumber,InstallDate,InstallDate2,InstallLocation,InstallSource,InstallState,Language,LocalPackage,Name,PackageCache,PackageCode,PackageName,ProductID,Vendor,Version /format:csv
Node Installed Programs:
  reg.exe QUERY "HKLM\Software\Wow6432Node\Microsoft\Windows\CurrentVersion\Uninstall" /s
Installed Programs:
  reg.exe QUERY "HKLM\Software\Microsoft\Windows\CurrentVersion\Uninstall" /s
LocalGroups:
  cmd.exe /C "for /f "delims=*" %x in ('net localgroup ^|find "*"') do net localgroup "%x""
Extract Windows Event Logs:
  wevtutil epl System "%OutputDir%\SystemLog.evtx"
  wevtutil epl Security "%OutputDir%\SecurityLog.evtx"
  wevtutil epl Application "%OutputDir%\ApplicationLog.evtx"
Extract Registry Hives:
  REG EXPORT HKLM\Software "%OutputDir%\HKLM_Software.reg" /y
  REG EXPORT HKLM\SYSTEM "%OutputDir%\HKLM_System.reg" /y
  REG EXPORT HKLM\SAM "%OutputDir%\HKLM_SAM.reg" /y

```

