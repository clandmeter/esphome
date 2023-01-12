# ESPHome config for MelcoBEMS MINI (Mitsubishi heat pumps)

MelcoBEMS MINI (A1M) is a MODBUS Building Energy Management Systems for Mitsubishi heat pumps.
The included yaml file in this project can be written to an esphome compatible device and act as a MODBUS controller.
The ESP should be equiped with a compatible RS-485 device and connected to the MelcoBEMS MINI (A1M).

## General MODBUS information

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


## Added MODBUS registers in ESPHome config

### MelcoBEMS MINI (A1M) Input Register

| Register name                                       | Address | Hex | Modicom | Type        |
|-----------------------------------------------------|---------|-----|---------|-------------|
| MelcoBEMS MINI (A1M) Firmware Version               | 3       | 3   | 30004   | sensor      |
| Fault Code (decimal)                                | 8       | 8   | 30009   | text_sensor |
| System Type Detected                                | 9       | 9   | 30010   | text_sensor |
| Defrost                                             | 26      | 1A  | 30027   | text_sensor |
| Residual Heat Removal                               | 27      | 1B  | 30028   | text_sensor |
| Refrigerant Error Info                              | 28      | 1C  | 30029   | text_sensor |
| 7-Segment Display Error Code Digit 1                | 29      | 1D  | 30030   | text_sensor |
| 7-Segment Display Error Code Digit 2                | 30      | 1E  | 30031   | text_sensor |
| Heat Pump Frequency – Master                        | 32      | 20  | 30033   | sensor      |
| Heat Source Status                                  | 39      | 27  | 30040   | text_sensor |
| Temperature Setpoint – Zone 1 (signed)              | 40      | 28  | 30041   | sensor      |
| Temperature Setpoint – Zone 2 (signed)              | 42      | 2A  | 30043   | sensor      |
| Flow Temperature Setpoint – Zone 1 (signed)         | 44      | 2C  | 30045   | sensor      |
| Flow Temperature Setpoint – Zone 2 (signed)         | 46      | 2E  | 30047   | sensor      |
| Legionella Temperature Setpoint (signed)            | 48      | 30  | 30049   | sensor      |
| DHW Temperature Drop (signed)                       | 50      | 32  | 30051   | sensor      |
| Room Temperature – Zone 1 (signed)                  | 52      | 34  | 30053   | sensor      |
| Room Temperature – Zone 2 (signed)                  | 54      | 36  | 30055   | sensor      |
| Refrigerant Liquid Temperature (signed)             | 56      | 38  | 30057   | sensor      |
| Outdoor Ambient Temperature 58 (signed)             | 58      | 3A  | 30059   | sensor      |
| Flow Temperature (signed)                           | 60      | 3C  | 30061   | sensor      |
| Return Temperature (signed)                         | 62      | 3E  | 30063   | sensor      |
| Tank Water Temperature 64 (signed)                  | 64      | 40  | 30065   | sensor      |
| Flow Temperature – Zone 1 (signed)                  | 66      | 42  | 30067   | sensor      |
| Return Temperature – Zone 1 (signed)                | 68      | 44  | 30069   | sensor      |
| Flow Temperature – Zone 2 (signed)                  | 70      | 46  | 30071   | sensor      |
| Return Temperature – Zone 2 (signed)                | 72      | 48  | 30073   | sensor      |
| Boiler Flow Temperature (signed)                    | 74      | 4A  | 30075   | sensor      |
| Boiler Return Temperature (signed)                  | 76      | 4C  | 30077   | sensor      |
| Heat Pump Run Time (hours)                          | 79      | 4F  | 30080   | sensor      |
| Heat Pump Run Time (hours x100)                     | 80      | 50  | 30081   | sensor      |
| Model Profile 1                                     | 151     | 97  | 30152   | text_sensor |
| Last Measured Heating Energy Consumption – kWh part | 156     | 9C  | 30157   | sensor      |
| Last Measured Heating Energy Consumption – Wh part  | 157     | 9D  | 30158   | sensor      |
| Last Measured Cooling Energy Consumption – kWh part | 158     | 9E  | 30159   | sensor      |
| Last Measured Cooling Energy Consumption – Wh part  | 159     | 9F  | 30160   | sensor      |
| Last Measured DHW Energy Consumption – kWh part     | 160     | A0  | 30161   | sensor      |
| Last Measured DHW Energy Consumption – Wh part      | 161     | A1  | 30162   | sensor      |
| Last Measured Total Energy Consumption – kWh        | 162     | A2  | 30163   | sensor      |
| Last Measured Heating Energy Produced – kWh part    | 166     | A6  | 30167   | sensor      |
| Last Measured Heating Energy Produced – Wh part     | 167     | A7  | 30168   | sensor      |
| Last Measured Cooling Energy Produced – kWh part    | 168     | A8  | 30169   | sensor      |
| Last Measured Cooling Energy Produced – Wh part     | 169     | A9  | 30170   | sensor      |
| Last Measured DHW Energy Produced – kWh part        | 170     | AA  | 30171   | sensor      |
| Last Measured DHW Energy Produced – Wh part         | 171     | AB  | 30172   | sensor      |
| Last Measured Total Energy Produced – kWh           | 172     | AC  | 30173   | sensor      |
| Flow Rate                                           | 173     | AD  | 30174   | sensor      |
| Version of main software                            | 199     | C7  | 30200   | sensor      |
| Sub-version of software                             | 200     | C8  | 30201   | sensor      |
| Consumed Electric Power                             | 227     | E3  | 30228   | sensor      |
| Produced Power                                      | 228     | E4  | 30229   | sensor      |

### MelcoBEMS MINI (A1M) Holding Registers

| Register name                                       | Address | Hex | Modicom | Type        |
|-----------------------------------------------------|---------|-----|---------|-------------|
| Operating Mode                                      | 26      | 1A  | 40027   | text_sensor |
| Operating Mode (DHW)                                | 27      | 1B  | 40028   | switch      |
| A/C Mode – Zone 1                                   | 28      | 1C  | 40029   | select      |
| A/C Mode – Zone 2                                   | 29      | 1D  | 40030   | select      |
| Set Tank Water Temperature (signed)                 | 30      | 1E  | 40031   | number      |
| H/C Thermostat Target Temperature – Zone 1 (signed) | 32      | 20  | 40033   | number      |
| H/C Thermostat Target Temperature – Zone 2 (signed) | 34      | 22  | 40035   | number      |
| Force DHW                                           | 37      | 25  | 40038   | switch      |
| Holiday                                             | 38      | 26  | 40039   | switch      |
| Cooling On Prohibit – Zone 1                        | 41      | 29  | 40042   | switch      |
| Cooling On Prohibit – Zone 2                        | 43      | 2B  | 40044   | switch      |
| Thermostat Target Temperature – Zone 1 (signed)     | 54      | 36  | 40055   | number      |
| Thermostat Target Temperature – Zone 2 (signed)     | 56      | 38  | 40057   | number      |
| HC Control Type                                     | 58      | 3A  | 40059   | select      |

### MelcoBEMS MINI (A1M) Coils

| Register name | Address | Hex | Modicom | Type   |
|---------------|---------|-----|---------|--------|
| System On/Off | 1       | 1   | 00002   | switch |
