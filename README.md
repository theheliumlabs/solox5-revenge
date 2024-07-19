# solox5-revenge
Reverse Engineering the SOLO-X5 Bluetooth speaker

## Reverse engineering - Findings

### Power Delivery, Battery Management
System is powered by a 3.7V LiPo, that charges through a micro-B USB (3-pin) connector.

The power is directly fed into LTC4056 (LTH7) that serves as BMS. The charging current determined by PROG resistor (2.7k) is around 130mA. The battery charge reference voltage is 4.2V and it is observed that the system enters undervoltage shutdown at 3.85V. Which indicates quite a lot of battery capacity is un-claimed. The red charing LED indicator is controlled by the open drain charging status pin.

### Audio feed points.

    - BLUETOOTH
    - FM
    - SD Card
    - USB Flash Drive
    - AUX IN


4- AUX_DET checks for low on T pin to notify insertion.

5- MIC is connected to dedicated port on MCU but FW doesnt seem to use it.

6- System FW forces BT first, even when AUX plugged in.

7- The hole on the corner is probably for FM antenna

8- The Audio AMP is dual mode (Class F/D) but here forced on F

9- Switch inputs are chained to save 1 GPIO for 4 switches

10- A very slow TF Card interface utilizing only 1 data pin.

11- microSD is powered by VDDIO generated internally by MCU (current limited by 4.7k resistor.)

12- The SD detect pin is pulling the SD Card clock. (Best Guess: When no card is present, det is pulled low internally by the connector and hence the clock line has a strong pull down. When card is present, the clock line gets its needed pull-up to VDD)

13- Bluetooth RF connects to a Printed Antenna (2.4GHz) while the FMIP connects to a dipole antenna passing through a pi filter.

14- MIX2018A audio amp is a dual mode (F/D) amplifier serving as class F in this application.

15- The Audio Amp enable/control line is controlled by MCU GPIO

16- MCU serves a BLUE status LED (open drain Output).

17- AUX input jack Left/Right channels are combined.

