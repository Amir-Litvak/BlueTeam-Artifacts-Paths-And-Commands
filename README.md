# Paths And Commands For Forensics
## Browsers
### History File Location:
```
Windows
C:\Users\<username>\AppData\Local\Google\Chrome\User Data\Default
C:\Users\<username>\AppData\Local\Google\Chrome\User Data\Default\Cache
macOS
/Users/<username>/Library/Application Support/Google/Chrome/Default
/Users/<username>/Library/Caches/Google/Chrome/Default/Cache
Linux
/home/<username>/.config/google-chrome/Default
/home/<username>/.cache/google-chrome/Default/Cache
```

### Locate the lastupdated Windows Chrome history file:
```
gci 'C:\Users\*\AppData\Local\Google\Chrome\User Data\*\History' | select FullName, LastWriteTime | sort LastWriteTime
```
### Locate the lastupdated Mac\Linux Chrome history file:
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

## System Logs Location
```
#Windows:
C:\Windows\System32\winevt\Logs

#Mac\Linux:
/var/log/
```

