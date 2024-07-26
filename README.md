# Config Date Time in Windows Server

## 1 - Enable and Start Windows Time Service
Open Services Manager:

Open Console.
Type `services.msc` and press Enter to open the Services Manager.
Locate Windows Time Service:

In the Services window, scroll down to find Windows Time.
Enable the Service:

Right-click on `Windows Time` and select Properties.
In the Properties window, set the Startup type to `Automatic`.
Click Apply and then OK.

Start the Service:
In the Services window, right-click on Windows Time again and select Start.

## 2 - Setting NTP Server and Config

```
w32tm /config /manualpeerlist:"time.windows.com" /syncfromflags:manual /reliable:YES /update
```

**2.1 Reduduce system hour and setting time zone by Windows UI**

**2.2 Force Synchronization**

```
w32tm /resync
```

## 3 - More commands

```sh
// Verify the configuration:
// To check the status of the NTP configuration, run:
w32tm /query /status

// To check the list of configured NTP servers, run:
w32tm /query /peers

// To Stop
w32tm stop

// Top Satrt
w32tm start
```

## 4 - Checking with python

```python
import ntplib
from time import ctime

ntp_client = ntplib.NTPClient()
response = ntp_client.request('time.windows.com')
print(ctime(response.tx_time))
```

Source: https://chatgpt.com/share/40139b1f-8354-40a0-82f3-8a88624df219

