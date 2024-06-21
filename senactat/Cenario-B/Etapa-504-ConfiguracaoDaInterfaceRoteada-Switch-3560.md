!Autor: Robson Vaamonde
!Procedimentos em TI: http://procedimentosemti.com.br
!Bora para Prática: http://boraparapratica.com.br
!Robson Vaamonde: http://vaamonde.com.br
!Facebook Procedimentos em TI: https://www.facebook.com/ProcedimentosEmTi
!Facebook Bora para Prática: https://www.facebook.com/BoraParaPratica
!Instagram Procedimentos em TI: https://www.instagram.com/procedimentoem
!YouTUBE Bora Para Prática: https://www.youtube.com/boraparapratica
!Data de criação: 10/05/2020
!Data de atualização: 10/05/2020
!Versão: 0.01
!Testado e homologado no Cisco Packet Tracer 7.3 e GNS3 2.2.7

!Acessando o modo EXEC Privilegiado
enable

	!Acessando o modo de Configuração Global de Comandos
	configure terminal
		
		!Habilitando o recurso de Roteamento Local do Switch Layer 3 3560
		!DICA: habilitar o recurso de roteamento no Switch Layer 3 permite utilizar protocolos de roteamento no Switch
		!OBSERVAÇÃO: habilitar o recurso de roteamento do Switch Layer 3 somente se for necessário
		!OBSERVAÇÃO: por padrão o recurso de roteamento do Switch Layer 3 está desligado/desabilitado
		!OBSERVAÇÃO: os recursos de roteamento permite utilizar protocolos dinâmicos como o RIP, RIPv2, EIGRP e OSPF no Switch
		!IMPORTANTE: o Switch Layer 3 não foi projetado para trabalhar com Roteamento de WAN, indicado somente para a LAN
		ip routing
		
		!Alterando o Endereço IPv4 da Interface Virtual SVI do Switch Layer 3
		!DICA: com a ativação do recurso de roteamento, as Interfaces Virtual se tornam Gateway da Rede Local
		!OBSERVAÇÃO: as SVI são utilizadas para o roteamento entre VLAN's, agilizando o processo em camada de Hardware
		!OBSERVAÇÃO: utilizar Switch Layer 3 para fazer o Roteamento da VLAN é mais rápido do que utilizar o Router-on-Stick
		interface vlan 1
			ip address 192.168.3.254 255.255.255.0
			exit
		
		!Configurando a Interface (Porta de Rede) Roteada do Switch Layer 3
		interface FastEthernet 0/24
		
			!Desabilitando o recurso de Switch da Porta conectada com o Router 1941
			!DICA: desabilitar o recurso de Switch da porta permite transforma a mesma em um Interface de Rede, permitindo
			!adicionar um endereço IPv4 ou IPv6 é utilizar como uma Interface Roteada ou como uma Porta de Gateway
			no switchport
			
			!Configurando a Descrição da Interface de No Switchport
			description Interface de conexão com o Router 1941-2
			
			!Configurando o endereço de IPv4 de conexão com a Rede do Router 1941-2
			ip address 192.168.2.1 255.255.255.0
			exit
			
		!Configurando o Gateway do Switch Layer 3 3560
		!DICA: a configuração do Gateway no Switch Layer 3 com suporte a roteamento será utilizada somente para o acesso
		!remoto ou gerenciamento do Switch, utilizando protocolos como SNMP, Syslog, etc
		!OBSERVAÇÃO: para a porta roteada acessar outras redes é necessário a configuração do roteamento estático, dinâmico
		!ou rota padrão
		ip default-gateway 192.168.2.254
		end

!Salvando as configurações da memória RAM para a memória NVRAM
write

!Visualizando as configurações da memória RAM
show running-config | section interface

!Verificando as informações das Interfaces e Roteamento
show ip interface brief
show ip route