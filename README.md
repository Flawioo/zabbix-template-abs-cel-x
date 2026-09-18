# Zabbix Template for ABS CEL X

Community Zabbix template for monitoring **ABS CEL X / ABS LX** industrial cellular routers through the device's native HTTP/JSON interface.

**Maintained by Flawioo**  
Professional contact for **Zabbix monitoring, connectivity, VPN and industrial/IoT connectivity services**: **flawioo@gmail.com**

> This is an independent community project. It is not an official template from ABS Telemetria and is not affiliated with or endorsed by the manufacturer.

## Compatibility

- **Zabbix:** 7.0
- **Device family:** ABS CEL X / ABS LX
- **Status API:** `/cgi-bin/conversor_server_config.pyc`
- **Radio diagnostics tested with:** Cinterion EHS6, 3G/UMTS
- Product reference: https://abstelemetria.com/abs-cel-x-4g/

The core HTTP status collection is based on the ABS Configurador Web interface. The extended `AT^SMONI` parser was validated on a Cinterion EHS6. Other cellular modules or 4G variants may return a different radio format.

## What it monitors

- Device/API health, uptime and inventory
- Cellular modem availability, WAN state, APN and IP
- RSSI signal level
- UMTS radio metrics: RSCP, EC/N0, UARFCN, PSC, MCC/MNC, LAC and Cell ID
- Ethernet physical link state and Ethernet WAN state
- OpenVPN and IPsec
- TCP telemetry connection, retry counters and RX/TX
- Serial interface state and statistics
- Watchdog/keepalive parameters

## Signal quality maps

The template includes separate value maps for RSSI, UMTS RSCP and UMTS EC/N0 so Latest data is easier to interpret while preserving the raw numeric values.

## Installation

1. Download `template_abs_cel_x.yaml`.
2. In Zabbix 7.0 go to **Data collection → Templates → Import**.
3. Import the YAML.
4. Link **Template ABS CEL X by Flawioo** to the host.
5. Configure the host address so `{HOST.CONN}` resolves to the ABS management IP.
6. Adjust host macros when required.

See [docs/installation.md](docs/installation.md).

## Main macros

| Macro | Default | Purpose |
|---|---:|---|
| `{$ABS.OPENVPN.REQUIRED}` | 1 | Require OpenVPN up |
| `{$ABS.TCP.REQUIRED}` | 1 | Require TCP telemetry connection |
| `{$ABS.ETH0.REQUIRED}` | 0 | Require Ethernet 0 physical link |
| `{$ABS.ETH1.REQUIRED}` | 0 | Require Ethernet 1 physical link |
| `{$ABS.SIGNAL.MIN}` | -100 | RSSI warning threshold |
| `{$ABS.SIGNAL.HIGH}` | -110 | RSSI high-severity threshold |
| `{$ABS.RSCP.WARN}` | -85 | UMTS RSCP warning threshold |
| `{$ABS.RSCP.HIGH}` | -95 | UMTS RSCP high-severity threshold |
| `{$ABS.ECNO.WARN}` | -10 | UMTS EC/N0 warning threshold |
| `{$ABS.ECNO.HIGH}` | -15 | UMTS EC/N0 high-severity threshold |

## Native HTTP calls

Status:

```bash
curl -H 'Content-Type: application/json' \
  -X POST \
  -d '{"cmd":"get_conversor_status","parms":{}}' \
  http://ROUTER_IP/cgi-bin/conversor_server_config.pyc
```

Cinterion EHS6 radio diagnostics:

```bash
curl -H 'Content-Type: application/json' \
  -X POST \
  -d '{"cmd":"cel_modem","parms":{"command":"at_command","data":"AT^SMONI"}}' \
  http://ROUTER_IP/cgi-bin/conversor_server_config.pyc
```

Keep the management interface restricted to trusted networks/VPNs.

## Documentation

- [Installation](docs/installation.md)
- [Monitored items](docs/monitored-items.md)
- [Radio metrics](docs/radio-metrics.md)
- [Changelog](CHANGELOG.md)

## Contributing

Issues and pull requests are welcome, especially test results from other ABS CEL X hardware revisions or cellular modules. Sanitize IMSI, IMEI, ICCID, passwords, customer IPs and other sensitive information before publishing captures.

## Professional contact

For Zabbix monitoring, VPN, cellular connectivity, industrial routers or IoT connectivity:

**Flawioo**  
**flawioo@gmail.com**

## License

Released under the [MIT License](LICENSE).
