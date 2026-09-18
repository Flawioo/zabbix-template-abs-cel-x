# Itens monitorados

O template utiliza tags para facilitar filtros no **Latest data**.

## Principais componentes

- `component=raw` — coleta bruta / item mestre
- `component=api` — saúde da API
- `component=system` — uptime e inventário
- `component=cellular` — modem, WAN e rádio
- `component=ethernet` — links físicos Ethernet
- `component=vpn` — OpenVPN e IPsec
- `component=tcp` — conexão TCP de telemetria
- `component=serial` — interfaces seriais
- `component=watchdog` — watchdog/keepalive

Os itens de rádio também utilizam:

```
subsystem=radio
```

Métricas específicas de UMTS podem utilizar:

```
technology=umts
```

## Itens mestres

### ABS CEL X - Status JSON

Chave:

```
abs.cel.status.raw
```

Intervalo padrão: 1 minuto.

Executa uma única consulta de status e alimenta a maior parte dos itens dependentes.

### ABS CEL X - Radio SMONI JSON

Chave:

```
abs.radio.smoni.raw
```

Intervalo padrão: 5 minutos.

Envia `AT^SMONI` pela interface HTTP do equipamento e alimenta os itens dependentes de rádio.

## Exemplos de chaves coletadas

```
abs.api.result_code
abs.uptime
abs.serial
abs.firmware.version
abs.hostname
abs.cel.signal
abs.cel.wan.state
abs.cel.wan.ip
abs.eth0.link
abs.eth1.link
abs.waneth.state
abs.openvpn.state
abs.openvpn.ip
abs.tcp.connected
abs.tcp.connection_count
abs.tcp.attempt_count
abs.tcp.rx_total
abs.tcp.tx_total
abs.serial_public.connected
abs.serial_abs.connected
abs.radio.rscp
abs.radio.ecno
abs.radio.cellid
abs.radio.uarfcn
```

Para a lista completa, consulte o template importado no Zabbix ou o arquivo YAML.
