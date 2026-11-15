# JCAD HaLow hardware prototype

Module interconnection schematic for a JCAD telemetry interface using an ESP32-S3 N16R8 development board, an existing RS-232-to-3.3V TTL converter, a 128x64 I2C OLED, a Seeed XIAO HaLow transceiver carrier, and an ATGM336H GPS breakout.

## Download and open

Use **Code → Download ZIP**, extract the archive, then open `hardware/revC/JCAD_Prototype.kicad_pro` with KiCad 9. The PDF is in the same directory. A standalone project archive is included in `releases/JCAD_Prototype_RevC.zip`.

## Scope and validation

Revision C describes purchased module wiring, not a PCB layout. Battery/solar circuitry and firmware integration are deferred. The ALFA TUBE-AHM is the planned HaLow access point with Ethernet to the existing PC monitor.

KiCad 9.0.2 exported the PDF and reported zero electrical rules violations. Passive module interface symbols do not validate internal module circuits, supply capacity, or external voltage compatibility. No physical hardware validation was performed.

Before assembly, resolve the JCAD signal-ground/cable reference and verify GPS UART/PPS voltage compatibility. GPS VCC is 5V according to the supplied breakout wiring diagram. See `hardware/revC/README.md` and schematic notes for details.

Firmware baseline: https://github.com/ahansen12/jcad-esp32/releases/tag/v1.0.0
