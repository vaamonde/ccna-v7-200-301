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

## PRIMEIRA ETAPA: Configuração do DHCP Server no Router Cisco 2911

```python
!Acessando o modo Exec Privilegiado
enable

	!Acessar modo de configuração global
	configure terminal

		!Configurando o Pool do DHCP Server da VLAN do Primeiro Usuário
		!OBSERVAÇÃO IMPORTANTE: veja o arquivo 00-DocumentacaoDaRede.txt a partir da linha: 186 
		!(SEXTA ETAPA: Determinação das Sub-Interfaces de Gateway de cada VLAN dos Grupos)
		ip dhcp excluded-address 172.16.???.1 172.16.???.100
		ip dhcp excluded-address 172.16.???.200 172.16.???.254
		ip dhcp pool vlan-???
			network 172.16.???.0 255.255.255.0
			default-router 172.16.???.254
			dns-server 8.8.8.8 8.8.4.4
			domain-name senac.br
			exit

		!Configurando o Pool do DHCP Server da VLAN do Segundo Usuário	
		ip dhcp excluded-address 172.16.???.1 172.16.???.100
		ip dhcp excluded-address 172.16.???.200 172.16.???.254
		ip dhcp pool vlan-???
			network 172.16.???.0 255.255.255.0
			default-router 172.16.???.254
			dns-server 8.8.8.8 8.8.4.4
			domain-name senac.br
			exit

		!Configurando o Pool do DHCP Server da VLAN do Terceiro Usuário	
		ip dhcp excluded-address 172.16.???.1 172.16.???.100
		ip dhcp excluded-address 172.16.???.200 172.16.???.254
		ip dhcp pool vlan-???
			network 172.16.???.0 255.255.255.0
			default-router 172.16.???.254
			dns-server 8.8.8.8 8.8.4.4
			domain-name senac.br
			exit

		!Configurando o Pool do DHCP Server da VLAN do Quarto Usuário	
		ip dhcp excluded-address 172.16.???.1 172.16.???.100
		ip dhcp excluded-address 172.16.???.200 172.16.???.254
		ip dhcp pool vlan-???
			network 172.16.???.0 255.255.255.0
			default-router 172.16.???.254
			dns-server 8.8.8.8 8.8.4.4
			domain-name senac.br
			exit

		!Configurando o Pool do DHCP Server da VLAN Wireless
		ip dhcp excluded-address 172.16.???.1 172.16.???.100
		ip dhcp excluded-address 172.16.???.200 172.16.???.254
		ip dhcp pool vlan-???
			network 172.16.???.0 255.255.255.0
			default-router 172.16.???.254
			dns-server 8.8.8.8 8.8.4.4
			domain-name senac.br
			end

!Salvando as configurações
copy running-config startup-config

!Verificando as informações do Pool DHCP Server
show ip dhcp pool

!Visualizando os Leasing dos IP ofertados na REde
show ip dhcp binding (essas informações só estará disponível depois que configurar os clientes)
```