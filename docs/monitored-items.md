# Monitored items

The template uses tags to make **Latest data** easier to filter.

## Main components

- `component=raw`
- `component=api`
- `component=system`
- `component=cellular`
- `component=ethernet`
- `component=vpn`
- `component=tcp`
- `component=serial`
- `component=watchdog`

Radio items also use:

```
subsystem=radio
```

UMTS-specific metrics can use:

```
technology=umts
```

## Master items

### ABS CEL X - Status JSON

Key:

```
abs.cel.status.raw
```

Default interval: 1 minute.

### ABS CEL X - Radio SMONI JSON

Key:

```
abs.radio.smoni.raw
```

Default interval: 5 minutes.

## Example keys

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
