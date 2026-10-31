# dell-wyze-3040-lora-halow

<img width="450" height="350" alt="image" src="https://github.com/user-attachments/assets/49f2cdd0-d936-4b8a-ad2d-0a8c9c643a75" />

OpenWRT Dell Wyze 3040 Thin Client based Meshtastic and Halow using USB Meshstick and USB Halow Adapter firmware

Coneect both your CH341 USB MESHSTICK and USB Halow adapter alongside a USB flash drive ( if your openwrt image is on USB )

then

Press F12 to select the USB sroage device OpenWRT image was flash onto - or internal storage if you have actually written the image to it

NOTE: you will also need to disable Secure Boot in the BIOS - F2

<img width="1534" height="873" alt="image" src="https://github.com/user-attachments/assets/8ae2e869-f8e9-4044-a92f-56eeeabaa56c" />

Once you see OpenWRT grub screen press e to edit the boot command line
 We need to remove the serial console re-direction, then press F10 to continue to boot with the modified command line

OpenWRT will not bootup with the serial console redirection on the Dell Wyze 3040

```
  menuentry "OpenWrt" {
          linux /boot/vmlinuz root=PARTUUID=ca165c20-f717-ec14-f184-b15f1bb0e102 rootwait console=tty1 noinitrd
```

<img width="1385" height="1044" alt="image" src="https://github.com/user-attachments/assets/0ccc0376-67e8-4765-bdf1-9a6b69153d06" />


<img width="1385" height="1044" alt="image" src="https://github.com/user-attachments/assets/5f94e0f8-cd84-43e2-ad13-045281dac38b" />

We also need to make the grub command line permanent once OpenWRT is up
```
nano /boot/grub/grub.cfg
```

Connect LAN cable to the ethernet port on the Thin Client
* set your lan ip address to 10.42.0.2/24 ( any ip except 10.42.0.1/24 )
* point your web browser to 10.42.0.1
* and run trrogh the morse micro web interface wizzard to setup halow - Selecting your Region would it be US, EU, AU etc (in my case in need EU)
  Refer to the Morse Micro Officail PDF guide for more information regarding the Web interface
  - https://www.morsemicro.com/resources/user_guides/MM6108_MM8108-Eval-Kit-User-Guide-2.8.pdf
  as this firmware experience will have the same look and feel just be running on diffirent hardware

* enable ttyd - Services - Terminal (Web based Terminal Access as Dropbear SSH is disabled by default )
 OR
perform the installation steps on the Dell Wyze 3040 itself 
  
* and go through the setps to install meshtasticd on openwrt

Notes from 
https://github.com/meshtastic/openwrt-repo

```
opkg update
opkg install wget-ssl
wget -O /tmp/meshtastic-ipk.pub https://openwrt.meshtastic.org/meshtastic-ipk.pub
opkg-key add /tmp/meshtastic-ipk.pub && rm /tmp/meshtastic-ipk.pub
sed -i '/meshtastic/d' /etc/opkg/customfeeds.conf
ARCH=$( . /etc/openwrt_release; echo "$DISTRIB_ARCH" )
WRT_VER=$( . /etc/openwrt_release; echo "${DISTRIB_RELEASE%%-*}" | cut -d. -f1-2 )
echo "src/gz meshtastic https://openwrt.meshtastic.org/openwrt-${WRT_VER}/${ARCH}" >> /etc/opkg/customfeeds.conf
opkg update
opkg install meshtasticd
```

Confirm meshtasticd is running
```
/etc/init.d/meshtasticd status
```

```
logread | grep meshtasticd
```

* point your android phone or meshtastic desktop application to connect to 10.42.0.1 and set a LoRa Region
* use whichever client anadoid or desktop

  <img width="1010" height="1166" alt="image" src="https://github.com/user-attachments/assets/e8a5324c-a164-4049-ac34-f09fbd8339c7" />


OpenWRT based on Morse Micro SDK Morse-3.1-dev - https://github.com/MorseMicro/openwrt


Lora USB Stick used my MESHSTICK

LINK

https://www.elecrow.com/meshstick-usb-to-spi-sx1262-tcxo-lora-usb-stick-usb-plug-and-play-meshtastic-lora-mesh-node.html

Halow USB Stick used WFD8108 but you could also use the official RD9 or a diy version

LINK

https://www.alibaba.com/product-detail/WFDG8108-WiFi-HaLow-Dongle-Plug-And_1601962754478.html

<img width="1182" height="1071" alt="image" src="https://github.com/user-attachments/assets/7cd1a63f-20d0-4c25-9cee-e2cf7ba3490d" />

<img width="1716" height="1377" alt="image" src="https://github.com/user-attachments/assets/35fa6cdd-3d16-41cd-839e-18cece18d2a1" />

<img width="1716" height="1377" alt="image" src="https://github.com/user-attachments/assets/50275ed9-80d4-4da6-99a9-1d0ee9d2af17" />

---

## Further Reading

https://www.parkytowers.me.uk/thin/wyse/3040/

## ⚠️ Disclaimer

> [!WARNING]
> Use of the resources provided in this repository is entirely at your own risk. I take no responsibility for any hardware damage, malfunctions, or data loss.

---

## ☕ Support My Work

If this open-hardware project brings value to you, please consider supporting my design pipeline!

[![Buy Me A Coffee](https://img.shields.io/badge/buy_me_a_coffee-FFDD00?style=for-the-badge&logo=buy-me-a-coffee&logoColor=black)](https://buymeacoffee.com/mark.birss)
