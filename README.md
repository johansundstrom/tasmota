# Tasmota
Hur jag installerade Tasmota

## Sonoff Basic (validerad) samt Sonoff Basic R2 (validerad)

1. Anslut USB-TTL enligt 3V3 (närmast SW), RX, TX, GND
2. Håll ned SW och anslut 3V3
3. Efter spänningsanslutning, släpp SW
4. <a href="https://github.com/tasmota/tasmotizer">Tasmotize</a>
5. Anslut till 230VAC
6. Vid blink, tethera till 2.4GHz WiFi
7. Surfa till 192.168.4.1
8. Ange SSID och PWD

## Sonoff Basic DIY (R3) ESP8285 chip (validerad)

1. Uppdatera Sonoff till minst v.3.1 mha eWelink
2. Koppla bort 230VAC
3. Sätt på OTA-jumpern (over the air)
4. Ladda ned <a href="https://github.com/arendst/Tasmota/releases">Tasmota.bin</a>
5. Installera <a href="https://github.com/itead/Sonoff_Devices_DIY_Tools/tree/master/tool>tool_01DIY85(3.3.0).exe</a> (för PC)
6. Skapa en mobil hotspot med SSID ```sonoffDiy``` och pw ```20170618sn```
7. Koppla in 230VAC
8. Anslut Tasmota och PC till ```sonoffDiy```
9. Starta ```tool_01DIY85(3.3.0).exe```
10. Kontrollera att Sonoff nås genom att klicka ```on``` och ```off```
11. Klicka ```Firmware flash``` och välj  ```Tasmota.bin```. Klicka OK

(min sonoff hade bara plats för 508kB i minnet. Jag valde file ```tasmota-lite.bin```)

12. Ta bort OTA jumpern
13. Starta om


## ESP32 Devkit V1 (validerad)

1. Ladda ned <a href="https://github.com/arendst/Tasmota/tree/firmware/firmware/tasmota32">tasmota32.bin</a>
2. Ladda ned samtliga <a href="https://github.com/arendst/Tasmota/tree/firmware/firmware/tasmota32/ESP32_needed_files">bin-filer</a>
3. Installera "Flash Download Tools (ESP8266 & ESP32 & ESP32-S2)" från ```espressif.com > support > tools```
4. Starta "Developer Mode" > "ESP32 DownloadTool"
5. Inställningar:

  * bootloader_dout_40m.bin - 0x1000
  * partitions.bin - 0x8000
  * boot_app0.bin - 0xe000
  * tasmota32.bin - 0x10000 

  * SPI Speed - 80MHz
  * SPI Mode - DIO
  * Flash Size - 32Mbit

6. WiFi Provisioning 192.168.4.1
7. Sänd i Tasmota konsolen ```SetOption19 1```

## Tasmota32-sensors.bin

* För t.ex. BME280 - I2C
* Ladda ned <a href="https://github.com/arendst/Tasmota/blob/firmware/firmware/tasmota32/tasmota32-sensors.bin">tasmota32-sensors.bin</a>
* Uppdatera med ´´´Firmware Upgrade´´´
* Anslut t.ex. GPIO21 - SDA, GPIO22 - SCL
* Konfigurera modulen
* Efter uppstart genomförs en I2C scan och hittar sensorn

## Tasmota32-display.bin

* För t.ex. SSD1306 OLED
* Ladda ned <a href="https://github.com/arendst/Tasmota/blob/firmware/firmware/tasmota32/tasmota32-display.bin">Tasmota32-display.bin</a>
* Uppdatera med ´´´Firmware Upgrade´´´
* Anslut t.ex. GPIO21 - SDA, GPIO22 - SCL
* Konfigurera modulen
* Efter uppstart genomförs en I2C scan och hittar displayen

### Användbara displaykommandon

* *Display* - visar nuvarande inställningar
* *DisplayRotate 2* - rotera
* *DisplayText text* - visar "text"
* *DisplayMode [0-5]* - 0 - text, 1 - Tid/datum, 2 - 

## Tasmota mallar
* https://templates.blakadder.com/

## Tasmota kommandon
* https://tasmota.github.io/docs/#/Commands

## Firmware
* https://github.com/arendst/Tasmota/releases

## Flasher 
* https://www.banggood.com/RobotDyn-USB-Serial-Adapter-CH340G-5V3_3V-USB-to-TTL-UART-For-Arduino-ProMini-DIY-p-1128916.html?rmmds=search&cur_warehouse=CN

## Flasha firmware
* https://tasmota.github.io/docs/#/installation/Prerequisites?id=needed-software
