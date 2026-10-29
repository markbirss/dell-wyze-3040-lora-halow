# dell-wyze-3040-lora-halow
OpenWRT Dell Wyze 3040 Thin Client based Meshtatic and Halow using USB Meshstick and USB Halow Adapter

Coneect both your CH341 USB MESHSTICK and USB Halow adapter alongside a USB flash drive ( if your openwrt image is on USB )

then

Press F12 to select the USB sroage device OpenWRT image was flash onto - or internal storage if you have actually written the image to it

<img width="1534" height="873" alt="image" src="https://github.com/user-attachments/assets/8ae2e869-f8e9-4044-a92f-56eeeabaa56c" />

Once you see OpenWRT grub screen press e to edit the boot command line
 We need to remove the serial console re-direction

```
  menuentry "OpenWrt" {
          linux /boot/vmlinuz root=PARTUUID=ca165c20-f717-ec14-f184-b15f1bb0e102 rootwait console=tty1 noinitrd
```

Connect LAN cable to the ethernet port on the Thin Client
* set your lan ip address to 10.42.0.2/24 ( any ip except 10.42.0.1/24 )
* point your web browser to 10.42.0.1
* and run trrogh the morse micro web interface wizzard to setup halow
* enable ttyd - Services - Terminal
* and go through the setps to install meshtasticd on openwrt - https://github.com/meshtastic/openwrt-repo
* install meshtasticd

Confirm meshtasticd is running
```
/etc/init.d/meshtasticd status
```

```
logread | grep meshtasticd
```

* point your phone or meshtastic desktop application to connect to 10.42.0.1 and set a LoRa Region
* use whichever client anadoid or desktop

  <img width="1010" height="1166" alt="image" src="https://github.com/user-attachments/assets/e8a5324c-a164-4049-ac34-f09fbd8339c7" />


OpenWRT based on Morse Micro SDK

Lora USB Stick used MESHSTICK
LINK

https://www.elecrow.com/meshstick-usb-to-spi-sx1262-tcxo-lora-usb-stick-usb-plug-and-play-meshtastic-lora-mesh-node.html

Halow USB Stick used WFD8108 but you could also use the official RD9 or a diy version
LINK

https://www.alibaba.com/product-detail/WFDG8108-WiFi-HaLow-Dongle-Plug-And_1601962754478.html

<img width="1182" height="1071" alt="image" src="https://github.com/user-attachments/assets/7cd1a63f-20d0-4c25-9cee-e2cf7ba3490d" />

<img width="1716" height="1377" alt="image" src="https://github.com/user-attachments/assets/35fa6cdd-3d16-41cd-839e-18cece18d2a1" />

<img width="1716" height="1377" alt="image" src="https://github.com/user-attachments/assets/50275ed9-80d4-4da6-99a9-1d0ee9d2af17" />

---

## ⚠️ Disclaimer

> [!WARNING]
> Use of the resources provided in this repository is entirely at your own risk. I take no responsibility for any hardware damage, malfunctions, or data loss.

---

## ☕ Support My Work

If this open-hardware project brings value to you, please consider supporting my design pipeline!

[![Buy Me A Coffee](https://img.shields.io/badge/buy_me_a_coffee-FFDD00?style=for-the-badge&logo=buy-me-a-coffee&logoColor=black)](https://buymeacoffee.com/mark.birss)
