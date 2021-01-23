<h1 align="center">
  <img src="public/simcard.png" width="115">
  <br>
    3g/4g modem on ARMBIAN
</h1>
<p>Integrating the Qualcomm-Sim7600SA (or another one) modem (3g / 4g) into a ARMBIAN devices (running in a nanopi neo core in my case)</p>
☝️ this works with "sakis3g"
<br>
https://github.com/Trixarian/sakis3g-source.git
<br>
<br>

## Installing prerequisites :
Make sure your device image has the following packages ->
<br>
- usb-modeswitch
<br>
```
sudo apt-get install usb-modeswitch
```
- ppp
<br>
```
sudo apt-get install ppp
```
- wvdial
<br>
```
sudo apt-get install wvdial
```
- libusb-1.0-0-dev
<br>
```
sudo apt-get install libusb-1.0-0-dev
```
- sakis3g
<br>
```
git clone https://github.com/Trixarian/sakis3g-source.gi
```
<br>

## Sakis3g configuration
<br>

```
#include <libusb-1.0/libusb.h>
```


```
sudo cp /usr/include/libusb-1.0/libusb.h /usr/include
```

<br>
Change to directory when the repo has downloaded:
<br>
<br>

```
cd sakis3g-source
```
```
./compile
```
```
./compile embedded
```
```
./compile stripped
```
Copy the compiled file to your bin folder:
<br>

```
sudo cp build/sakis3gz /usr/bin/sakis3g
```

<br>

## Locating the device id :
we can type "lsusb" to find it

```
root@nanopineo:~# lsusb
Bus 008 Device 001: ID 1d6b:0001 Linux Foundation 1.1 root hub
Bus 005 Device 002: ID 152d:0578 JMicron Technology Corp. / JMicron USA Technology Corp. 
Bus 005 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub
Bus 007 Device 001: ID 1d6b:0001 Linux Foundation 1.1 root hub
Bus 004 Device 002: ID 1e0e:9003 Qualcomm / Option 
Bus 004 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub
Bus 006 Device 001: ID 1d6b:0001 Linux Foundation 1.1 root hub
Bus 003 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub
Bus 002 Device 001: ID 1d6b:0001 Linux Foundation 1.1 root hub
Bus 001 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub

```
The 1e0e:9003 is what we will need (1e0e:9003 is for my modem specifically probaly yours will be diferent)
<br>

## Configuration commnad syntax :

```
sudo sakis3g connect USBMODEM="<DEVICE ID>" USBINTERFACE="<2 for Qualcom>" CUSTOM_APN="<sim card provider apn" APN_USER="<apn_user>" APN_PASS="<apn_password"
```
it was like this for me :

```
sudo sakis3g connect USBMODEM="1e0e:9003" USBINTERFACE="2" CUSTOM_APN="claro.com.br" APN_USER="claro" APN_PASS="claro"
```

 If you follow these steps, an ppp interface will be created

```
ppp0: flags=4305<UP,POINTOPOINT,RUNNING,NOARP,MULTICAST>  mtu 1500
        inet 10.99.232.103  netmask 255.255.255.255  destination 10.64.64.64
        ppp  txqueuelen 3  (Point-to-Point Protocol)
        RX packets 311  bytes 23318 (23.3 KB)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 316  bytes 23661 (23.6 KB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0
```
Hope this help u ;)
<br>
 by Popovicz. ͡•_ゝ ͡•




