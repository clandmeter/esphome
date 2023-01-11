# ESPHome config for MelcoBEMS MINI (Mitsubishi heat pumps)

MelcoBEMS MINI (A1M) is a MODBUS Building Energy Management Systems for Mitsubishi heat pumps.
The included yaml file in this project can be written to an esphome compatible device and act as a MODBUS controller.
The ESP should be equiped with a compatible RS-485 device and connected to the MelcoBEMS MINI (A1M).

## Generic MODBUS information

### MODBUS Primary tables

| Primary tables    | Object type | Type of access | Comments                                                      |
| ----------------- | ----------- | -------------- | ------------------------------------------------------------- |
| Discretes Input   | Single bit  | Read-Only      | This type of data can be provided by an I/O system.           |
| Coils             | Single bit  | Read-Write     | This type of data can be alterable by an application program. |
| Input Registers   | 16-bit word | Read-Only      | This type of data can be provided by an I/O system            |
| Holding Registers | 16-bit word | Read-Write     | This type of data can be alterable by an application program. |


### MODBUS Function codes

| Function Code | Address     | Table            | R/W      | Size        | Value   |
| ------------- | ----------- | ---------------- | -------- | ----------- | ------- |
| 1             | 00001-10000 | Coils            | Readonly | Single bit  | 0/1     |
| 5             | 00001-10000 | Coils            | Single   | Single bit  | 0/1     |
| 15            | 00001-10000 | Coils            | Multiple | Single bit  | 0/1     |
| 2             | 10001-20000 | Discretes Input  | Readonly | Single bit  | 0/1     |
| 3             | 40001-50000 | Holding Register | Readonly | 16-bit word | 0-65535 |
| 6             | 40001-50000 | Holding Register | Single   | 16-bit word | 0-65535 |
| 16            | 40001-50000 | Holding Register | Multiple | 16-bit word | 0-65535 |
| 4             | 30001-40000 | Input Register   | Readonly | 16-bit word | 0-65535 |
