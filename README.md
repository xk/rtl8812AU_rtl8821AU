# rtl8821 rtl8812
*2 de Diciembre 2016 jorge@jorgechamorro.com*

For armbian / Orange Pi PC / D-Link DWA-171
## Prepare
```sh
sudo apt-get install build.essential git
git clone https://github.com/xk/rtl8812AU_rtl8821AU.git
cd rtl8812AU_rtl8821AU
```
## Compile and install
```sh
make -j4
sudo make install
```
## Load and test
```
sudo modprobe -a 8821au
lsmod
Module                  Size  Used by
8821au               1987288  0 
[...]
```
## Plug it in (D-Link DWA-171)
```
lsusb
Bus 003 Device 003: ID 2001:3314 D-Link Corp.
[...]

dmesg
[   45.791972] ehci_irq: highspeed device connect
[   46.060149] usb 3-1: new high-speed USB device number 2 using sunxi-ehci
[   46.433427] RTL871X: module init start
[   46.433447] RTL871X: rtl8821au v4.3.19.5_17672.20160506_BTCOEX20150921-58
[   46.433458] RTL871X: build time: Dec  2 2016 19:35:59
[   46.433467] RTL871X: rtl8821au BT-Coex version = BTCOEX20150921-58
[   46.433638] RTL871X: 
[   46.433642] usb_endpoint_descriptor(0):
[   46.433650] RTL871X: bLength=7
[   46.433657] RTL871X: bDescriptorType=5
[   46.433664] RTL871X: bEndpointAddress=84
[   46.433671] RTL871X: wMaxPacketSize=512
[   46.433678] RTL871X: bInterval=0
[   46.433686] RTL871X: RT_usb_endpoint_is_bulk_in = 4
[...]

iwconfig
wlan0     unassociated  Nickname:"<WIFI@REALTEK>"
          Mode:Managed  Frequency=5.18 GHz  Access Point: Not-Associated   
          Sensitivity:0/0  
          Retry:off   RTS thr:off   Fragment thr:off
          Power Management:off
          Link Quality:0  Signal level:0  Noise level:0
          Rx invalid nwid:0  Rx invalid crypt:0  Rx invalid frag:0
          Tx excessive retries:0  Invalid misc:0   Missed beacon:0

nano /etc/network/interfaces
(you know how to do that, right?)

sudo ifup wlan0
iwconfig
wlan1     IEEE 802.11AC  ESSID:"YOUR SSID"  Nickname:"<WIFI@REALTEK>"
          Mode:Managed  Frequency:5.18 GHz  Access Point: 88:1F:A1:34:CD:5B   
          Bit Rate:434 Mb/s   Sensitivity:0/0  
          Retry:off   RTS thr:off   Fragment thr:off
          Power Management:off
          Link Quality=100/100  Signal level=48/100  Noise level=0/100
          Rx invalid nwid:0  Rx invalid crypt:0  Rx invalid frag:0
          Tx excessive retries:0  Invalid misc:0   Missed beacon:0
```


BTW:
```
uname -a
Linux orangepipc 3.4.112-sun8i #10 SMP PREEMPT Sun Oct 23 16:06:55 CEST 2016 armv7l GNU/Linux
```
Good luck!
