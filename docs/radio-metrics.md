# Cellular radio metrics

Signal strength and signal quality are different measurements. This template keeps RSSI, RSCP and EC/N0 as separate metrics.

## RSSI

On the tested device, the native `SINAL` field matches the standard `AT+CSQ` conversion.

Example:

```
+CSQ: 11,99
RSSI = -113 + (11 × 2) = -91 dBm
```

| RSSI | Interpretation |
|---|---|
| >= -70 dBm | Excelente |
| >= -85 dBm | Bom |
| >= -100 dBm | Razoável |
| >= -110 dBm | Ruim |
| < -110 dBm | Muito ruim |

## UMTS RSCP

| RSCP | Interpretation |
|---|---|
| >= -60 dBm | Excelente |
| >= -75 dBm | Bom |
| >= -85 dBm | Razoável |
| >= -95 dBm | Ruim |
| < -95 dBm | Muito ruim |

## UMTS EC/N0

| EC/N0 | Interpretation |
|---|---|
| >= -6 dB | Excelente |
| >= -10 dB | Bom |
| >= -15 dB | Razoável |
| >= -20 dB | Ruim |
| < -20 dB | Muito ruim |

## Cinterion EHS6 and AT^SMONI

A tested device returned:

```
^SMONI: 3G,4379,230,-9.0,-92,724,10,9CB7,077AC46,9,11,NOCONN
```

The template parses the tested EHS6 3G layout into technology, UARFCN, PSC, EC/N0, RSCP, MCC, MNC, LAC, Cell ID, SQual, SRxLev and radio state.

Do not assume the same field layout for every modem or radio technology.

## References

- ABS CEL X product page: https://abstelemetria.com/abs-cel-x-4g/
- Teltonika Mobile Signal Strength Recommendations: https://wiki.teltonika-networks.com/view/Mobile_Signal_Strength_Recommendations
- Teltonika RSCP: https://wiki.teltonika-networks.com/view/RSCP
- Teltonika EC/IO: https://wiki.teltonika-networks.com/view/EC/IO
- ThingPark cellular backhaul signal documentation: https://docs.thingpark.com/thingpark-enterprise/latest/docs/user-guide/base-stations/monitor-base-stations-performance/monitor-cellular-and-wifi-backhaul-interface-statistics
