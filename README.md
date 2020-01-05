# Tasmota
Hur jag installerade Tasmota

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
