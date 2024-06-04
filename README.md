# Effekta-AX-Series-Axpert-MKS-esphome
Čítanie a posielanie príkazov pomocou esphome do Meniča, ktorý nemá výstup cez RS232 rozhranie ale iba USB

Zdroje: https://github.com/syssi/esphome-pipsolar/issues/127

Typ meniča: Effekta AX series P1 3000 24 (prebalený Axpert MKS)
Komunikačná doska, ktorá má iba USB HID rozhranie:
![f3ef07da91605fa8a8b03e6beefd629b5c719fc6](https://github.com/tiimsvk/Effekta-AX-Series-Axpert-MKS-esphome/assets/52893640/5802d067-58f9-4b80-a4a9-df7841d17872)

Pre bezpečnú komunikáciu medzi MEničom a ESP32 je potrebné umiestniť digitalny (alebo optický) izolátor napríklad typ π122U31 (na ali: https://vi.aliexpress.com/item/1005005643287661.html)

Pripojenie ku konektoru JST na meniči:
Pin     | Digitalny izol. | ESP32
------------------------------
1 TX    | AI -> AO        | TX
2 RX    | BO -> BI        | RX
3 5V    | V2 -> V1        | 3V3
4 GND   | G2 -> G1        | GND
5 HFPW+ |
6 Relay |
![20240509_100444](https://github.com/tiimsvk/Effekta-AX-Series-Axpert-MKS-esphome/assets/52893640/58d1dd17-24be-4778-885c-c5e8146efe5d)


Yaml v prilohách a v esphome následne uvidíme jednotlivé snezory:

![Clipboard02](https://github.com/tiimsvk/Effekta-AX-Series-Axpert-MKS-esphome/assets/52893640/2c1ff83c-be19-49c9-927d-beba2932220b)

Je potrebné ale vložiť upravený komponent, ktorý pridáva a opravuje niektoré chyby [pipsolar.zip](https://github.com/user-attachments/files/15545178/pipsolar.zip).
- pridanie možnosti entity_category
- QFLAG su teraz ako prepínače
- opravené príkazy MUCHGC a MNCHGC
- pridané entity ako je power a total energy v yaml

Ďalši postup je pirdnie ďalši exterierových možností vrámci esphome:
- pridanie BL0939 dvojkanalove meranie spotreby za dvoma vystupnymi ističami pomocou modulu bez esp32 Sonoff Dual R3 (cez optický izolátor)
- pridanie merania AC vstupu pomocou CT clamp
- Pridanie na vstup aj vystup relé 4x
- Pridaný stykač pre vzdialené odpínanie Solárnych panelov
- Kontrola pripojenia poistiek pomocou magnetického senzoru
- Teplota baterie pomocou dallas
- Pridaný segmentovy displej alebo kryštalovy displej pre ďalšie položky na zobrazenie
- Buzzer ako alarm

Výsledok:
![20240604_093214](https://github.com/tiimsvk/Effekta-AX-Series-Axpert-MKS-esphome/assets/52893640/e139e28b-fbd2-4e1e-85a1-370ffba8630b)

