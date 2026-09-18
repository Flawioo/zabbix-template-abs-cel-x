# Instalação

## Requisitos

- Zabbix 7.0
- Alcance de rede do Zabbix Server ou Proxy até a interface HTTP de gerenciamento do ABS CEL X
- Acesso ao endpoint:
  `http://IP_DO_EQUIPAMENTO/cgi-bin/conversor_server_config.pyc`

## Importação

1. Baixe `template_abs_cel_x.yaml`.
2. No Zabbix, acesse **Data collection → Templates**.
3. Clique em **Import**.
4. Importe o arquivo YAML.
5. Vincule **Template ABS CEL X by Flawioo** ao host desejado.

## Endereço do host

Os itens mestres HTTP utilizam:

```
http://{HOST.CONN}/cgi-bin/conversor_server_config.pyc
```

Configure o host para que `{HOST.CONN}` resolva para um endereço acessível pelo Zabbix Server ou Proxy.

## Serviços obrigatórios por instalação

As macros abaixo permitem que o mesmo template seja usado em cenários diferentes:

```
{$ABS.OPENVPN.REQUIRED}=1
{$ABS.TCP.REQUIRED}=1
{$ABS.ETH0.REQUIRED}=0
{$ABS.ETH1.REQUIRED}=0
```

Altere uma macro de Ethernet para `1` somente quando aquele link físico for obrigatório no local.

## Diagnóstico de rádio

O parser de `AT^SMONI` foi validado atualmente com:

```
Cinterion EHS6
3G / UMTS
```

Outros módulos celulares ou variantes 4G podem retornar outro formato.

Quando uma métrica específica de UMTS não está disponível, o template descarta a amostra em vez de deixar o item como não suportado.

## Segurança

A interface HTTP de gerenciamento pode expor informações operacionais e dados do modem. Mantenha o acesso restrito a uma rede de gerenciamento confiável, VPN ou caminho equivalente.
