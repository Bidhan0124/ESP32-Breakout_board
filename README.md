### ***ESP32 DevKit-V1 Breakout Board***



A custom breakout board for the ESP32 DevKit-V1, designed to make prototyping faster and cleaner. Instead of a jungle of  jumper wires directly onto the DevKit every project and prototype, this board gives you organized, labeled headers for every peripheral you'll  use.

This is my first PCB design project.



**What It Breaks Out:**

1. SPI x2 — Shared bus (SCK, MOSI, MISO) with independent CS lines (CS1 on D5, CS2 on D15)
2. I2C x2 — Two physical headers on the same bus (SDA on D21, SCL on D22) for connecting   multiple I2C devices simultaneously
3. UART — TX2/RX2 with VCC and GND
4. Power — Selectable between onboard 3.3V or external voltage via jumper

##### 

**Specs:**

* 3.3V operation
* Through-hole components throughout
* 2-layer board (signal on F.Cu, ground plane as well as signal on B.Cu)
* 2.54mm pitch pin headers
* Screw terminal for power input



**3D Render**

**!\[3D Render](images/3d\_render.png)**



**Schematic**

**!\[Schematic](images/schematic.svg)**











**Design Decisions:**

1. Power select jumper — Instead of hardwiring 3.3V, I added a 3-pin jumper so the board can be powered from the onboard 3.3V rail or an external voltage source. More flexible for different prototyping scenarios where different voltages may be needed.
2. I2C pull-ups on the bus — Added 4.7kΩ pull-up resistors on SDA and SCL once on the board rather than per device. I2C is an open-drain bus so the pull-ups are a bus property, not a per-device one. Two headers on the same bus means you can connect multiple devices simultaneously as long as they are initialized with unique addresses.
3. D15 pull-down — D15 is used as CS2 for SPI2. It's also a strapping pin on the ESP32 with an internal pull-up active during boot. I have added a 10kΩ pull-down from D15 to GND to ensure the SPI peripheral ignores the pin cleanly during the boot sequence,so no errors occur.

&#x20;  Shared SPI bus — SPI1 and SPI2 share the same SCK, MOSI, and MISO lines but have independent CS pins. 





**Known Limitations:**

1. D34 and D35 are input-only GPIOs on the ESP32 — they are exposed on the headers but cannot be used as outputs. 
2. No onboard decoupling capacitors — add 0.1µF caps on your board near noisy peripherals if you run into stability issues.





**Tools Used:**

KiCad 9.0

FreeRouting plugin for autorouting





**Board Status:**

&#x20;\[x] Schematic complete

&#x20;\[x] PCB layout complete

&#x20;\[x] DRC clean

&#x20;\[x] Gerbers generated

&#x20;\[] Fabricated

&#x20;\[]Tested





**Files:**

/gerbers — Fabrication files ready

ESP32\_breakout\_board.kicad\_sch — Schematic

ESP32\_breakout\_board.kicad\_pcb — PCB layout

