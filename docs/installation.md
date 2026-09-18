# Installation

## Requirements

- Zabbix 7.0
- Network reachability from the Zabbix server or proxy to the ABS CEL X management HTTP interface
- Access to:
  `http://DEVICE_IP/cgi-bin/conversor_server_config.pyc`

## Import

1. Download `template_abs_cel_x.yaml`.
2. In Zabbix, go to **Data collection → Templates**.
3. Click **Import**.
4. Import the YAML file.
5. Link **Template ABS CEL X by Flawioo** to the target host.

## Host address

The HTTP master items use:

```
http://{HOST.CONN}/cgi-bin/conversor_server_config.pyc
```

Configure the host so `{HOST.CONN}` resolves to an address reachable by the Zabbix server or proxy.

## Optional service requirements

```
{$ABS.OPENVPN.REQUIRED}=1
{$ABS.TCP.REQUIRED}=1
{$ABS.ETH0.REQUIRED}=0
{$ABS.ETH1.REQUIRED}=0
```

Set the Ethernet requirement macro to `1` only when that physical link is mandatory at the site.

## Radio diagnostics

The `AT^SMONI` parser is currently validated with:

```
Cinterion EHS6
3G / UMTS
```

Other cellular modules or 4G variants can return a different layout.

## Security

The management HTTP interface can expose operational and modem information. Keep it restricted to a trusted management network, VPN or equivalent controlled path.
