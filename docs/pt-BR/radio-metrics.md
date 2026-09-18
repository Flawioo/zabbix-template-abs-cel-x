# Métricas de rádio celular

Força de sinal e qualidade de sinal são medidas diferentes. O template mantém RSSI, RSCP e EC/N0 como métricas separadas.

## RSSI

No equipamento testado, o campo nativo `SINAL` corresponde à conversão padrão de `AT+CSQ`.

Exemplo:

```
+CSQ: 11,99
RSSI = -113 + (11 × 2) = -91 dBm
```

| RSSI | Interpretação |
|---|---|
| >= -70 dBm | Excelente |
| >= -85 dBm | Bom |
| >= -100 dBm | Razoável |
| >= -110 dBm | Ruim |
| < -110 dBm | Muito ruim |

## RSCP em UMTS

RSCP representa a potência recebida da célula em redes UMTS/WCDMA e é uma medida mais específica da célula 3G do que o RSSI geral.

| RSCP | Interpretação |
|---|---|
| >= -60 dBm | Excelente |
| >= -75 dBm | Bom |
| >= -85 dBm | Razoável |
| >= -95 dBm | Ruim |
| < -95 dBm | Muito ruim |

## EC/N0 em UMTS

EC/N0 é um indicador de qualidade/interferência do sinal UMTS.

| EC/N0 | Interpretação |
|---|---|
| >= -6 dB | Excelente |
| >= -10 dB | Bom |
| >= -15 dB | Razoável |
| >= -20 dB | Ruim |
| < -20 dB | Muito ruim |

## Cinterion EHS6 e AT^SMONI

Um equipamento testado retornou:

```
^SMONI: 3G,4379,230,-9.0,-92,724,10,9CB7,077AC46,9,11,NOCONN
```

O template interpreta o formato 3G testado no EHS6 em campos como:

- tecnologia de acesso
- UARFCN
- PSC
- EC/N0
- RSCP
- MCC
- MNC
- LAC
- Cell ID
- SQual
- SRxLev
- estado de conexão de rádio

Não assuma que o mesmo layout será retornado por todos os módulos celulares ou tecnologias de rádio.

## Referências

- Página oficial do ABS CEL X: https://abstelemetria.com/abs-cel-x-4g/
- Teltonika Mobile Signal Strength Recommendations: https://wiki.teltonika-networks.com/view/Mobile_Signal_Strength_Recommendations
- Teltonika RSCP: https://wiki.teltonika-networks.com/view/RSCP
- Teltonika EC/IO: https://wiki.teltonika-networks.com/view/EC/IO
- ThingPark cellular backhaul signal documentation: https://docs.thingpark.com/thingpark-enterprise/latest/docs/user-guide/base-stations/monitor-base-stations-performance/monitor-cellular-and-wifi-backhaul-interface-statistics
