# Tasmota
Hur jag installerade Tasmota

## Sonoff Basic (validerad) samt Sonoff Basic R2 (validerad)

1. Koppla bort 230VAC
2. Anslut USB-TTL (FTDI) enligt 3V3 (närmast SW), RX, TX, GND
3. Håll ned SW och anslut 3V3
4. Efter spänningsanslutning, släpp SW
5. <a href="https://github.com/tasmota/tasmotizer">Tasmotize</a>
6. Anslut till 230VAC
7. Vid blink, tethera till 2.4GHz WiFi
8. Surfa till 192.168.4.1
9. Ange SSID och PWD

## Sonoff Basic DIY (R3) ESP8285 chip (validerad)

1. Uppdatera Sonoff till minst v.3.1 mha eWelink
2. Koppla bort 230VAC
3. Sätt på OTA-jumpern (over the air)
4. Ladda ned <a href="https://github.com/arendst/Tasmota/releases">Tasmota.bin</a>
5. Installera <a href="https://github.com/itead/Sonoff_Devices_DIY_Tools/tree/master/tool">tool_01DIY85(3.3.0).exe</a> (för PC)
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
3. Installera <a href="https://www.espressif.com/sites/default/files/tools/flash_download_tool_v3.8.5.zip">Flash Download Tools (ESP8266 & ESP32 & ESP32-S2)</a> från ```espressif.com > support > tools```
4. Starta "Developer Mode" > "ESP32 DownloadTool"
5. Inställningar:

| Fil | Adress |
|---|---|
| bootloader_dout_40m.bin | 0x1000 |
| partitions.bin | 0x8000 |
| boot_app0.bin | 0xe000 |
| tasmota32.bin | 0x10000 | 

| Inställning | Värde |
|---|---|
| SPI Speed | 80MHz |
| SPI Mode | DIO |
| Flash Size | 32Mbit |

6. WiFi Provisioning 192.168.4.1
7. Aktivera MQTT som Home Assistant Discovery mode genom ```SetOption19 1``` Tasmota konsolen 

## ESP8266 Devkit V3

1. https://tasmota.github.io/install/

## Tasmota32-sensors.bin

* För t.ex. BME280 - I2C
* Ladda ned <a href="https://github.com/arendst/Tasmota/blob/firmware/firmware/tasmota32/tasmota32-sensors.bin">tasmota32-sensors.bin</a>
* Uppdatera med ```Firmware Upgrade```
* Anslut t.ex. GPIO21 - SDA, GPIO22 - SCL
* Konfigurera modulen
* Efter uppstart genomförs en I2C scan och hittar sensorn

## Rules

```Rule<x> ON <trigger1> DO <command> ENDON ON <trigger2> DO <command> ENDON```

* autoexec.bat
* Namnger flera DS18B20 vid uppstart

```
Rule1 ON System#Boot DO 
  Backlog 
    DS18Alias 783C01F096F2BB28,1;
    DS18Alias 113C01F096174528,2;
    DS18Alias 8B0316C310F3FF28,3
ENDON
```

## Tasmota32-display.bin

* För t.ex. SSD1306 OLED
* Ladda ned <a href="https://github.com/arendst/Tasmota/blob/firmware/firmware/tasmota32/tasmota32-display.bin">Tasmota32-display.bin</a>
* Uppdatera med ```Firmware Upgrade```
* Anslut t.ex. GPIO21 - SDA, GPIO22 - SCL
* Konfigurera modulen
* Efter uppstart genomförs en I2C scan och hittar displayen

### DisplayMode

* Sex förprogrammerade displaymode's (0-5)
* För att visa text med DisplayText, sätt DisplayMode 0

| Parameter	| LCD Display	| OLED Display (SSD1306) |	TFT Display	| 7-segment Display (TM163x and MAX7219) |
|---|---|---|---|---|
| 0	| DisplayText	| DisplayText	| DisplayText	| All TM163x Displayfunctions |
| 1	| Time/Date	| Time/Date	| Time/Date	| Time |
| 2	| Local sensors	| Local sensors	| Local sensors	| Date |
| 3	| MQTT and Time/Date	| Local sensors and Time/Date	| Local sensors and Time/Date	| Time/Date |
| 4	| Local sensors	| MQTT and local sensors	| MQTT and local sensors	| NA |
| 5	| MQTT and Time/Date	| MQTT, local sensors and Time/Date	| MQTT, local sensors and Time/Date	| NA |



#### Användbara displaykommandon

* ```Display``` - visar nuvarande inställningar
* ```DisplayRotate [0, 1, 2, 3]``` - rotera 90 grader
* ```DisplayText text``` - visar "text"
* ```DisplayText [z]``` - rensar skärm
* ```DisplayText [sp1]``` - skalfaktor
 
#### positionering

* ```DisplayText [s1l1c1]text``` - scale 1, line 1, column 1, text
* ```DisplayText [s1x10y10]text``` - scale 1, x 10, y 10, text
* ```DisplayText [zs3x12y16t]``` - visar klockan tt:mm centrerat
* ```DisplayText [zx0y0r128:64s3x12y16t]``` - tid och rektangel
* ```DisplayMode [0-5]``` 
   * 0 - text
   * 1 - Tid/datum, 2 -
 
#### DisplaySize

```DisplaySize 1..4``` Set display scale-up size (SSD1306 and ILI9341 only) 
   
## Tasmota Display/MQTT

* ESP32 - boot btn is gpio0
* Tasmota SwitchMode 3 - toggle, SwitchMode 4 - Inverted SwitchMode
* Power2 - toggle = if power state is ON switch to OFF and vice versa

```
rule1 
on AM2301#Temperature do DisplayText [s2p21x0y0]T  %value%*C endon 
on AM2301#Humidity do DisplayText [s2p21x0y24]Rh %value%% endon 
on AM2301#Dewpoint do DisplayText [s2p21x0y47]Dew %value%*C endon

rule2
on AM2301#Temperature do publish h83/mobile/tph/temp %value% endon 
on AM2301#Humidity do publish h83/mobile/tph/humid %value% endon 
on AM2301#DewPoint do publish h83/mobile/tph/dew %value% endon 

rule3 
on Button1 do Power1 endon 
on Power1#State=1 do ruletimer1 5 endon 
on rules#timer=1 do power1 0 Endon
```

* Rules#Timer=&lt;x&gt;	- when countdown RuleTimer<x> expires (x = 1..8).
 
Annan enhet kan visa MQTT events
 
```
Rule1
  ON mqtt#connected DO Subscribe h83Temp, tele/h83/SENSOR, AM2301.Temperature ENDON   
  ON Event#h83Temp DO DisplayText [z]%value% ENDON

```
 
## connect via UART
 
```Backlog SSID1 myssid; Password1 mypassword; SSID2 myssid2; ...```

## Visa lokala sensorer på display

* Sätt ```Displaymode``` 4 eller 5 för SSD1306

```rule1 on DS18B20-1#temperature do displaytext %value% C endon```

eller...

```
rule1
  on DS18B20-1#temperature do displaytext [y1]%value% *C endon
  on DS18B20-2#temperature do displaytext [y10]%value% *C endon
```

## Event

* ```Rules``` agerar på triggers som t.ex ```ON Power1#state=1 DO...```
* Kommandot ```Event eventmame``` skapar egna triggers
* Skapa Event med ```=```

```on DS18B20-1#temperature do event tempalarm=%value% endon```

* Utvärdera eventtrigger

```on event#tempalarm=28 do power1 0 enddo```

eller...

```
Rule2 
on DS18B20-1#temperature do event b1=%value% endon
on event#b1>27 do power1 1 endon
on event#b1<=27 do power1 0 endon
```

eller kanske...

```
on DS18B20-1#temperature do event b1=%value% endon 
on event#b1>27 do displaytext [z]ALARM endon 
on event#b1<=27 do displaytext [z]%value% endon
```


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
