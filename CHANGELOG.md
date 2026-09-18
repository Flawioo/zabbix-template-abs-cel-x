# Changelog

## 1.0.0 - 2026-09-18

Initial public release.

### Added
- Zabbix 7.0 template for ABS CEL X / ABS LX.
- Native HTTP/JSON status collection.
- Cellular WAN, APN and modem monitoring.
- RSSI signal monitoring with value mapping.
- Ethernet physical link monitoring.
- OpenVPN and IPsec monitoring.
- TCP client status, retry counters and RX/TX statistics.
- Serial interface status and statistics.
- Watchdog/keepalive monitoring.
- Device inventory information.
- Cinterion EHS6 UMTS radio diagnostics through `AT^SMONI`.
- UMTS RSCP and EC/N0 monitoring with dedicated value maps.
- Configurable trigger thresholds using host macros.
- Item tags organized by component, subsystem and scope.
- Safe handling of unavailable radio metrics without marking items unsupported.
