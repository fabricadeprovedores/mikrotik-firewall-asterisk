# mikrotik-firewall-asterisk
Mikrotik Firewall Asterisk

Regras para redirecionar as portas (HTTPS, SIP e RTP) e proteger o servidor Asterisk de ataques externos. O uso do GeoIP restringe o acesso ao servidor para endereços geolocalizados no Brasil.

1) Cenário

WAN Link --> ether1 --> Mikrotik --> ether2 --> LAN Link --> Asterisk

2) SIP ALG

/ip firewall service-port disable sip

3) RAW

/ip firewall raw add action=drop chain=prerouting comment=HTTPS dst-port=443 in-interface=ether1 protocol=tcp src-address-list=!GeoIP2-BR
/ip firewall raw add action=drop chain=prerouting comment="SIP UDP" dst-port=5060 in-interface=ether1 protocol=udp src-address-list=!GeoIP2-BR
/ip firewall raw add action=drop chain=prerouting comment="SIP TCP" dst-port=5060 in-interface=ether1 protocol=tcp src-address-list=!GeoIP2-BR
/ip firewall raw add action=drop chain=prerouting comment="SIP TLS" dst-port=5061 in-interface=ether1 protocol=tcp src-address-list=!GeoIP2-BR
/ip firewall raw add action=drop chain=prerouting comment="Media UDP" dst-port=10000-20000 in-interface=ether1 protocol=udp src-address-list=!GeoIP2-BR

4) NAT (Portas Essenciais)

/ip firewall nat add action=dst-nat chain=dstnat comment=HTTPS dst-port=443 in-interface=ether1 protocol=tcp src-address-list=GeoIP2-BR to-addresses=[ASTERISK SERVER] to-ports=443
/ip firewall nat add action=dst-nat chain=dstnat comment="SIP UDP" dst-port=5060 in-interface=ether1 protocol=udp src-address-list=GeoIP2-BR to-addresses=[ASTERISK SERVER] to-ports=5060
/ip firewall nat add action=dst-nat chain=dstnat comment="SIP TCP" dst-port=5060 in-interface=ether1 protocol=tcp src-address-list=GeoIP2-BR to-addresses=[ASTERISK SERVER] to-ports=5060
/ip firewall nat add action=dst-nat chain=dstnat comment="SIP TLS" dst-port=5061 in-interface=ether1 protocol=tcp src-address-list=GeoIP2-BR to-addresses=[ASTERISK SERVER] to-ports=5061
/ip firewall nat add action=dst-nat chain=dstnat comment="Media UDP" dst-port=10000-20000 in-interface=ether1 protocol=udp src-address-list=GeoIP2-BR to-addresses=[ASTERISK SERVER] to-ports=10000-20000

5) GeoIP-BR - Lista de Endereços (atualiza até 16-09-2022)

Efetuar o download geoip2-br.rsc

Obsevação:
- Não nos responsabilizamos pelo uso desse script e quaisquer "problemas" causados;
- Caso você não tenha experiência com Mikrotik, ou tenha dúvidas sobre sua implementação, considere contratar uma consultoria especializada;

Contatos:
E-mail..: admin@fabricadeprovedores.com.br
WhatsApp: +5511995451003

