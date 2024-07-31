Autor: Robson Vaamonde<br>
Procedimentos em TI: http://procedimentosemti.com.br<br>
Bora para Prática: http://boraparapratica.com.br<br>
Robson Vaamonde: http://vaamonde.com.br<br>
Facebook Procedimentos em TI: https://www.facebook.com/ProcedimentosEmTi<br>
Facebook Bora para Prática: https://www.facebook.com/BoraParaPratica<br>
Instagram Procedimentos em TI: https://www.instagram.com/procedimentoem<br>
YouTUBE Bora Para Prática: https://www.youtube.com/boraparapratica<br>
LinkedIn Robson Vaamonde: https://www.linkedin.com/in/robson-vaamonde-0b029028/<br>
Github Procedimentos em TI: https://github.com/vaamonde<br>
Data de criação: 16/05/2024<br>
Data de atualização: 16/05/2024<br>
Versão: 0.01<br>
Testado e homologado no Cisco Packet Tracer 8.2.x e Rack Cisco SW-3560 e RT-2911

## PRIMEIRA ETAPA: Configuração da Interface de Internet no Router Cisco 2911

```python
!Acessando o modo Exec Privilegiado
enable

	!Acessar modo de configuração global
	configure terminal
		
	!Configuração da interface GigabitEthernet 0/1 para acesso a Internet
	interface gigabitEthernet 0/1
	
		!Descrição da Interface
		description Interface de acesso a Internet do Grupo-???
		
		!Configuração do endereçamento IP Dinâmico via DHCP Client
		ip address dhcp
		
		!Inicializando a Interface
		no shutdown
		
		!Saindo das configurações da interface
		end

!Salvando as configurações
copy running-config startup-config
	
!Visualizando as configurações
show running-config

!Visualizando as configurações de endereçamento IPv4
show ip interface brief

!Visualizando as informações de Roteamento
show ip route

!Pingar os servidores do SENAC Tatuapé no Router
ping 10.26.40.191
ping 10.26.40.190

!Pingar o Endereço IPv4 do Google no Router
ping 8.8.8.8

!Desktops Linux Mint ou Windows 10 deverá pingar via DNS
ping 8.8.8.8
ping google.com
```