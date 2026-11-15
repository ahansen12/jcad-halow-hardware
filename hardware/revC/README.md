# JCAD prototype schematic - Revision C

Open JCAD_Prototype.kicad_pro in KiCad 9. PDF included for review.
This is a module interconnection schematic, not a PCB design. Custom symbols describe exposed module pads; their numeric pin indices are NOT physical header numbers. Wire by pad names. Embedded symbols and local library are included.

## GPIO assignments
JCAD RX=16, TX=17. OLED SDA=8, SCL=9.
HaLow: D0 RESET_N=GPIO4; D1 WAKE=GPIO5; D2 IRQ=GPIO7; D3 CS_N=GPIO10; D4 BUSY=GPIO6; D8 SCK=GPIO12; D9 MISO=GPIO13; D10 MOSI=GPIO11.
These are proposed DevKit assignments, not firmware defaults. Update host driver configuration before operating HaLow.

## Power and assembly
USB powers the DevKit. The block labelled J3 represents its existing 3V3/GND output pads, not another power source. Converter and OLED use that 3V3 rail, subject to module compatibility and regulator capacity. Radio uses independent regulated 3.3V and 5V bench inputs with common ground; do not parallel separate 3.3V regulator outputs. Supply capacity and RF transient performance must be checked on hardware. Battery/solar, PCB footprints and RF circuitry inside purchased modules are out of scope.
OLED assumed to have onboard I2C pull-ups to its 3.3V supply; confirm. SSD1306 controller and 0x3C address remain to be tested. Converter TxIN/RxOUT match the underside photo. JCAD TX pin 3, RX pin 11, return pin 9 follow supplied project; its README identifies pin 4 as ICD serial reference. Resolve against actual cable/ICD before assembly.

## Sources and validation
- User-uploaded jcad-esp32 v1.0.0 firmware and README; module and DevKit photos.
- https://wiki.seeedstudio.com/getting_started_with_wifi_halow_module_for_xiao/
- https://github.com/Seeed-Studio/mm-iot-esp32/blob/main/framework/mm_shims/Kconfig
- XIAO ESP32-S3 mapping: D0=GPIO1, D1=2, D2=3, D3=4, D4=5, D8=7, D9=8, D10=9. These map driver defaults to carrier socket names; continuity-check board revision before powering.

KiCad 9.0.2 opened/exported the schematic and ERC reported zero violations. All module pins are passive interface pins: ERC verifies schematic connectivity, not logic voltage, regulator capacity, module internals, or physical pin assignment. No hardware validation performed.

## Revision C: GPS power confirmed by user-supplied connection diagram
U5 ATGM336H breakout VCC uses regulated 5V through J4. Common ground. UART1 RX GPIO18 receives GPS TX; UART1 TX GPIO15 drives GPS RX; optional PPS connects GPIO21. GPS input is separate from radio supply nets; a shared regulated 5V source can feed both if appropriately rated, but never parallel independent regulator outputs. USB powers DevKit separately.
The supplied diagram specifies power and signal connections, not UART/PPS electrical levels. Verify 3.3V-compatible signals before MCU connection; add level translation if needed. Diagram arrows indicate connections, not power or serial data direction. GPS TX drives MCU RX; MCU TX drives GPS RX. No firmware changes or hardware tests included.
