---
title: Scan réseau
permalink: /Scan_reseau/
---

# Scan réseau

Petit script pour faire du scan réseau sans nmap:

``` python
#!/usr/bin/env python
# From https://www.pythonforbeginners.com/code-snippets-source-code/port-scanner-in-python
import socket
import subprocess
import sys
from datetime import datetime

# Clear the screen
subprocess.call('clear', shell=True)

print "-" * 60
print "-" * 60

t1 = datetime.now()

try: 
	for i in range(1,255):
		remoteServerIP = "XXX.XXX.XXX.{}".format(i) # CHANGE ME
		for port in [22,80]: # Ports to check
			sock = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
			result = sock.connect_ex((remoteServerIP, port))
			if result == 0:
				print "Address {} - Port {}: 	 Open".format(remoteServerIP, port)
			else:
				print "Address {} - Port {}: 	 Closed".format(remoteServerIP, port)
			sock.close()

except KeyboardInterrupt:
    print "You pressed Ctrl+C"
    sys.exit()

except socket.gaierror:
    print 'Hostname could not be resolved. Exiting'
    sys.exit()

except socket.error:
    print "Couldn't connect to server"
    sys.exit()

# Checking the time again
t2 = datetime.now()

# Calculates the difference of time, to see how long it took to run the script
total =  t2 - t1

# Printing the information to screen
print 'Scanning Completed in: ', total
```
