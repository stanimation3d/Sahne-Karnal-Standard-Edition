# What Hardware Support Are Components Responsible For in the Karnal Operating System Architecture?
1. Sahne Karnal Standard Edition (Kernel): CPU and Memory
2. File System (e.g. SADAK): NVMe SSD, SATA SSD, SATA HDD, RAID, SD, MicroSD, UFS, eMMC vb. drives that provide persistent storage
3. Window System: GPU, NPU, Mouse, Touch Screen, Monitor, Keyboard, HDMI, Dısplayport, Thunderbolt, VGA, DVI, PCle, PCl, AGP, MIPI
4. Sound System: DSP, Speaker, Microphone, Audio Jacks, HDMI, Dısplayport, Thunderbolt, VGA, DVI,
5. Network system: Wİ-Fİ, Bluetooth, Ethernet, USB, Zigbee, Z-Wave, NFC (Near Field Communication), LoRa/LoRaWAN, Cellular (3G, 4G/LTE, 5G),

* Other components are not required to do this; they simply communicate with the drivers they provide.
* The reason for this list is that it is not pure MicroKernel but extended MicroKernel, and also the components that hold other responsibilities except the kernel are also internal servers, and this hardware support comes from it.
