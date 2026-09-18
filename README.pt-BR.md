# Template Zabbix para ABS CEL X

Template comunitário para monitoramento de roteadores celulares industriais **ABS CEL X / ABS LX** por meio da interface HTTP/JSON nativa do equipamento.

**Mantido por Flawioo**  
Contato profissional para **serviços de monitoramento Zabbix, conectividade, VPN e conectividade industrial/IoT**: **flawioo@gmail.com**

> Este é um projeto comunitário independente. Não é um template oficial da ABS Telemetria e não possui vínculo ou endosso do fabricante.

## Idiomas

- 🇧🇷 **Português:** este arquivo
- 🇺🇸 [English](README.md)

## Compatibilidade

- **Zabbix:** 7.0
- **Família de equipamentos:** ABS CEL X / ABS LX
- **API de status:** `/cgi-bin/conversor_server_config.pyc`
- **Diagnóstico de rádio testado com:** Cinterion EHS6, 3G/UMTS
- Página oficial do produto: https://abstelemetria.com/abs-cel-x-4g/

A coleta principal usa a interface HTTP/JSON utilizada pelo Configurador Web da ABS. O parser estendido de `AT^SMONI` foi validado em um modem Cinterion EHS6. Outros módulos celulares ou variantes 4G podem retornar um formato diferente.

## O que o template monitora

- Saúde do equipamento/API, uptime e inventário
- Disponibilidade do modem celular, estado da WAN, APN e IP
- Nível de sinal RSSI
- Métricas de rádio UMTS: RSCP, EC/N0, UARFCN, PSC, MCC/MNC, LAC e Cell ID
- Estado físico dos links Ethernet e estado da WAN Ethernet
- OpenVPN e IPsec
- Conexão TCP de telemetria, tentativas, reconexões e RX/TX
- Estado e estatísticas das interfaces seriais
- Parâmetros de watchdog/keepalive

## Mapas de qualidade de sinal

O template possui mapas de valores separados para RSSI, RSCP e EC/N0, facilitando a interpretação em **Latest data** sem perder os valores numéricos originais.

## Instalação

1. Baixe `template_abs_cel_x.yaml`.
2. No Zabbix 7.0, acesse **Data collection → Templates → Import**.
3. Importe o arquivo YAML.
4. Vincule **Template ABS CEL X by Flawioo** ao host.
5. Configure o endereço do host para que `{HOST.CONN}` resolva para o IP de gerenciamento do ABS.
6. Ajuste as macros do host quando necessário.

Veja [docs/pt-BR/installation.md](docs/pt-BR/installation.md).

## Principais macros

| Macro | Padrão | Função |
|---|---:|---|
| `{$ABS.OPENVPN.REQUIRED}` | 1 | Exige OpenVPN ativo |
| `{$ABS.TCP.REQUIRED}` | 1 | Exige a conexão TCP de telemetria |
| `{$ABS.ETH0.REQUIRED}` | 0 | Exige link físico na Ethernet 0 |
| `{$ABS.ETH1.REQUIRED}` | 0 | Exige link físico na Ethernet 1 |
| `{$ABS.SIGNAL.MIN}` | -100 | Limite de aviso para RSSI |
| `{$ABS.SIGNAL.HIGH}` | -110 | Limite de alta severidade para RSSI |
| `{$ABS.RSCP.WARN}` | -85 | Limite de aviso para RSCP UMTS |
| `{$ABS.RSCP.HIGH}` | -95 | Limite de alta severidade para RSCP UMTS |
| `{$ABS.ECNO.WARN}` | -10 | Limite de aviso para EC/N0 UMTS |
| `{$ABS.ECNO.HIGH}` | -15 | Limite de alta severidade para EC/N0 UMTS |

## Chamadas HTTP nativas

Status:

```bash
curl -H 'Content-Type: application/json' \
  -X POST \
  -d '{"cmd":"get_conversor_status","parms":{}}' \
  http://IP_DO_ROTEADOR/cgi-bin/conversor_server_config.pyc
```

Diagnóstico de rádio em Cinterion EHS6:

```bash
curl -H 'Content-Type: application/json' \
  -X POST \
  -d '{"cmd":"cel_modem","parms":{"command":"at_command","data":"AT^SMONI"}}' \
  http://IP_DO_ROTEADOR/cgi-bin/conversor_server_config.pyc
```

Mantenha a interface de gerenciamento restrita a redes confiáveis, VPN ou outro caminho controlado.

## Documentação

### Português
- [Instalação](docs/pt-BR/installation.md)
- [Itens monitorados](docs/pt-BR/monitored-items.md)
- [Métricas de rádio](docs/pt-BR/radio-metrics.md)

### English
- [Installation](docs/installation.md)
- [Monitored items](docs/monitored-items.md)
- [Radio metrics](docs/radio-metrics.md)

- [Changelog](CHANGELOG.md)

## Contribuindo

Issues e pull requests são bem-vindos, especialmente testes em outras revisões de hardware do ABS CEL X ou outros módulos celulares. Antes de publicar capturas ou respostas da API, remova IMSI, IMEI, ICCID, senhas, IPs de clientes e outras informações sensíveis.

## Contato profissional

Para projetos envolvendo Zabbix, VPN, conectividade celular, roteadores industriais ou IoT:

**Flawioo**  
**flawioo@gmail.com**

## Licença

Distribuído sob a [Licença MIT](LICENSE).
