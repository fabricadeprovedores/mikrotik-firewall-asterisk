# mikrotik-firewall-asterisk
Mikrotik Firewall Asterisk

1) Cenário
WAN Link --> ether1 --> Mikrotik --> ether2 --> LAN Link --> Asterisk

2) Endereços
ether1    = 200.200.200.2/24
ether2    = 192.168.0.1/24
Asterisk  = 192.168.0.10/24

3) GeoIP
--> Importar o geoip-br.rsc

4) Firewall
--> Criar regras na tabela NAT
