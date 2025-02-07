# ath-dbg

Adapter and level shifter PCB for debugging the Xtensa CPU in WiFi modules for
the Nintendo DSi.

## Usage

Mount a module on J1. If desired, also use J4 to connect the UART and ERST
signals to the corresponding testpoints on the module. This latter thing will
require some soldering.

Either use the external connectors (J2/J3, J5, J6) or solder a Raspberry Pico
directly to the pin holes present for it.

Some software will still be required to actually do JTAG debugging of the Xtensa
Cpu from a computer. Figuring out how exactly this could be made possible is
the reaosn I built this to begin with.

### Raspberry Pico pinouts

* `GP00`: UART RP to Ath/DWM (R2A)
* `GP01`: UART Ath/DWM to RP (A2R)
* `GP02`: JTAG.ERST (debug CPU reset extension)
* `GP03`: JTAG.TRST
* `GP04`: ~{WIFI_RST}
* `GP05`: SPI.~{WP}
* `GP06`: nSEL_ATH (0=Ath/DWM/TWL, 1=NTR wifi)
* `GP07`: 32 kHz clock to DWM
* `GP08`: SPI.CIPO
* `GP09`: SPI.~{CS}
* `GP10`: SPI.SCK
* `GP11`: SPI.COPI
* `GP12`: JTAG.TDO
* `GP13`: JTAG.TCK
* `GP14`: JTAG.TDI
* `GP15`: JTAG.TMS
* `GP16`: SDIO.CLK
* `GP17`: SDIO.D0
* `GP18`: SDIO.D1
* `GP19`: SDIO.D2
* `GP20`: SDIO.D3
* `GP21`: SDIO.CMD
* `GP22`: ATH_TX_H
* `GP26`: nTWLRST (DSi system reset)
* `GP27`: nDETECT (0=DWM inserted)

## Bill of Materials

| Reference | Value  | Footprint           | Notes |
|:--------- |:------ |:------------------- |:----- |
| C1, C3    | 1 uF   | 0603                | 1V8 LDO cap |
| C3-C8     | 100 nF | 0603                | decoupling caps |
| J1        | Molex SlimStack 52991-0508 | | WiFi module connector. must be this exact part number. |
| J2, J5    | 1x8-pin header | 2.54mm pitch | |
| J3        | 10-pin Cortex Debug connector | 1.27mm | dual SMD/THT footprint |
| J4        | 1x5-pin header | 2.54mm pitch | |
| J6        | 1x4-pin header | 2.54mm pitch | |
| R1-R6     | 22 Ohm         | 0603         | |
| R7-R18    | 48 kOhm        | 0603         | |
| U1        | Raspberry Pico | Raspberry Pico | |
| U2        | 3.3V-&gt;1.8V LDO | SOT-23-5  | TI TLV70018DDC, Diodes AP7343D-18W5-7 |
| U3-U5     | 3.3V&lt;-&gt;1.8V level shifter | TSSOP-14 | TI TXU0304, Nexperia NSU0304 |

## Dependencies

RP2040 and Raspberry Pico symbols and footprints from [here
](https://github.com/ncarandini/KiCad-RP-Pico).

## License

[CERN-OHL-S v2](./LICENSE)

