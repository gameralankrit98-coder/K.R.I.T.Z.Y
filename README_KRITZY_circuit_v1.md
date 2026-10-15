# KRITZY Circuit Design v1

This package is the first concrete circuit-level design for the chosen configuration:
- 1S protected LiPo (3.0–4.2 V)
- ESP32-S3-WROOM-1 family
- Four SG90-class servos
- Plug-in OLED, MPU6050, microSD, INMP441, MAX98357A-compatible amp and touch modules
- 2-layer carrier PCB

## Files
- `KRITZY_circuit_schematic_v1.svg`: circuit-level wiring schematic with power and signal connections.
- `KRITZY_PCB_placement_v1.svg`: board placement and routing-intent drawing.
- `KRITZY_netlist_v1.csv`: pin/net connection schedule.
- `KRITZY_BOM_v5.csv`: provisional bill of materials.
- `KRITZY_GPIO_map_v5.csv`: provisional GPIO map.
- `KRITZY_power_budget_v5.csv`: current calculations.
- `KRITZY_v5_engineering_definition.pdf`: engineering report.

## Architecture choice
For v1, use external, properly rated converter modules for the 5V servo rail and 3.3V logic rail. Use an external 1S charger and disconnect the robot while charging. This intentionally avoids inventing an unverified charger/load-sharing circuit or pretending an unspecified boost IC is adequate.

## Power estimate
Assuming 0.65A stall current per servo, 30% margin, 3.0V minimum battery and 85% converter efficiency:
- Servo rail target: 3.38A at 5V.
- Servo boost input estimate: 6.63A from battery.
- Logic rail target: 1A at 3.3V; battery input estimate: 1.29A.
- Combined estimate: 7.92A before transients and audio peaks.
These are assumptions for design sizing, not exact SG90 specifications or measured current.

## Important limitations
This is a circuit design definition, not yet a native KiCad schematic or a routed PCB. SVG line art is not electrical-rule-checkable. Exact module variants, footprints, cell/protection ratings, converter performance, board dimensions and connector pin orders must be frozen. No ERC/DRC, simulation or bench validation has been performed. Do not fabricate until these checks are completed.
