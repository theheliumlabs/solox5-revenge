# SOLO-X5 PCB reverse engineering - Findings

1- System is powered by a 3.7V LiPo
2- micro-B USB is used to charge the system.
3- LTC4056 (LTH7) serves as BMS (2.7k prog resistor) with Vpreset of 4.2V. With no battery present, it is down to 3.66V, Shutdown
4- AUX_DET checks for low on T pin to notify insertion.
5- MIC is connected to dedicated port on MCU but FW doesnt seem to use it.
6- System FW forces BT first, even when AUX plugged in.
7- The hole on the corner is probably for FM antenna
8- The Audio AMP is dual mode (Class F/D) but here forced on F
9- Switch inputs are chained to save 1 GPIO

