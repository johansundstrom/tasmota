# Tasmota
Hur jag installerade Tasmota

## Sonoff Basic (validerad)

1. Anslut USB-TTL enligt 3V3 (närmast SW), RX, TX, GND
2. Håll ned SW och anslut 3V3
3. Efter spänningsanslutning, släpp SW
4. Tasmotize!
5. Anslut till 230VAC
6. Vid blink, tethera till 2.4GHz WiFi
7. Surfa till 192.168.4.1
8. Ange SSID och PWD

## Sonoff Basic R2 (validerad)

### Tasmota mallar
* https://templates.blakadder.com/

### Tasmota kommandon
* https://tasmota.github.io/docs/#/Commands

### Firmware
* https://github.com/arendst/Tasmota/releases

### Flasher 
* https://www.banggood.com/RobotDyn-USB-Serial-Adapter-CH340G-5V3_3V-USB-to-TTL-UART-For-Arduino-ProMini-DIY-p-1128916.html?rmmds=search&cur_warehouse=CN

### Flasha firmware
* https://tasmota.github.io/docs/#/installation/Prerequisites?id=needed-software

## Sonoff Basic DIY (R3) ESP8285 chip (validerad)

1. Uppdatera Sonoff till minst v. 3.1 mha eWelink
2. Koppla bort 230VAC
3. Sätt på OTA-jumpern (over the air)
4. Ladda ned ```Tasmota-SE.bin``` (https://github.com/arendst/Tasmota/releases)
5. Ladda ned ```tool_01DIY85(3.3.0).exe``` (https://github.com/itead/Sonoff_Devices_DIY_Tools/tree/master/tool) (för PC)
6. Skapa en mobil hotspot med SSID ```sonoffDiy``` och pw ```20170618sn```
7. Koppla in 230VAC
8. Anslut Tasmota och PC till ```sonoffDiy```
9. Starta ```tool_01DIY85(3.3.0).exe```
10. Kontrollera att Sonoff nås genom att klicka ```on``` och ```off```
11. Klicka ```Firmware flash``` och välj Tasmota.bin. Klicka OK

(min sonoff hade bara plats för 508kB i minnet. Jag valde file ```tasmota-lite.bin```)

12. Ta bort OTA jumpern
13. Starta om


## ESP32 Devkit V1 (validerad)

1. Ladda ned ```tasmota32.bin``` från https://github.com/arendst/Tasmota/tree/firmware/firmware/tasmota32
2. Samtliga bin-filer från https://github.com/arendst/Tasmota/tree/firmware/firmware/tasmota32/ESP32_needed_files
3. Installera "Flash Download Tools (ESP8266 & ESP32 & ESP32-S2)" från ```espressif.com > support > tools```
4. Start in "Developer Mode" > ESP32 DownloadTool
5. Inställningar

* bootloader_dout_40m.bin - 0x1000
* partitions.bin - 0x8000
* boot_app0.bin - 0xe000
* tasmota32.bin - 0x10000 

* SPI Speed - 80MHz
* SPI Mode - DIO
* Flash Size - 32Mbit

6. <a href="https://github.com/johansundstrom/tasmota/blob/master/README.md#wifi-provisioning">WiFi Provisioning</a>

## WiFi Provisioning

1. Surfa 192.168.4.1

## Aktivera Discovery mode MQTT

* Sänd i Tasmota consolen ```SetOption19 1```
