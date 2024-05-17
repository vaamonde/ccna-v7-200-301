!Autor: Robson Vaamonde
!Procedimentos em TI: http://procedimentosemti.com.br
!Bora para Prática: http://boraparapratica.com.br
!Robson Vaamonde: http://vaamonde.com.br
!Facebook Procedimentos em TI: https://www.facebook.com/ProcedimentosEmTi
!Facebook Bora para Prática: https://www.facebook.com/BoraParaPratica
!Instagram Procedimentos em TI: https://www.instagram.com/procedimentoem
!YouTUBE Bora Para Prática: https://www.youtube.com/boraparapratica
!Data de criação: 30/04/2020
!Data de atualização: 10/08/2023
!Versão: 0.04
!Testado e homologado no Cisco Packet Tracer 7.3.x, 8.0.x, 8.1.x, 8.2.x e GNS3 2.2.x

!DHCPv4 (Dynamic Host Configuration Protocol) é um protocolo de serviço TCP/IP (Transmission Control Protocol/
!Internet Protocol) que oferece configuração dinâmica de dispositivos finais, com concessão de endereços IP de 
!host, máscara de sub-rede, gateway padrão, servidores DNS, sufixos de pesquisa do DNS, servidores WINS, 
!servidores NTP é muito mais.

!O protocolo padrão utilizado pelo DHCP Server é o UDP (User Datagram Protocol) na porta padrão: 67

!Escopo DHCP: Trata-se do intervalo completo dos possíveis endereços IP de uma rede. Os escopos definem a sub-rede
!física da rede que vai oferecer os serviços do DHCP.

!Configurações do Serviço de DHCP Server no Cisco Packet Tracer:
!OBSERVAÇÃO: por padrão o Serviço de DHCP Server no Cisco Packet Tracer está desligado
!OBSERVAÇÃO: o nome do escopo padrão do DHCP Server no Cisco Packet Tracer tem que ser: serverPool
!DICA: o escopo inicial está sempre relacionado a Placa de Rede e sua Configuração do Endereçamento IPv4
!DICA: geralmente em Servidores Microsoft ou GNU/Linux, após a instalação do Serviço do DHCP ele está desligado
!CUIDADO: é recomendado ter apenas 1 (um) Servidor DHCP na rede, em redes mais complexas existe a possibilidade de mais servidores
!OBSERVAÇÃO: o Switch Layer 3 ou Router possui os recursos de DHCP Server que será explorado em breve.

!Interface:                 FastEthernet0
!Service:                   On
!Pool Name:                 serverPool
!Default Gateway:           192.168.3.254
!DNS Server:                192.168.3.1	(DNS Preferencial ou Alternativo - no Cisco Packet Tracer e limitado)
!Start IP Address:          192.168.3.100 (Início da Faixa de Oferta de Endereços IPv4)
!Subnet Mask:               255.255.255.0
!Maximum Number of Users:   50 (Fim da Faixa de Oferta de Endereços IPv4 - 100 até 150)
!TFTP Server:               192.168.3.1
!WLC Address:               NÃO UTILIZADO NESSE VÍDEO (Endereço IP do WLC - Wireless LAN Controller)

!Comandos básicos de configuração dinâmica em dispositivos finais Microsoft Windows
ipconfig
ipconfig /all
ipconfig /release
ipconfig /renew