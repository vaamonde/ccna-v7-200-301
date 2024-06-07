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

## PRIMEIRA ETAPA: Configuração das SubInterfaces das VLAN's no Router Cisco 2911 

```python
!Acessando o modo Exec Privilegiado
enable

	!Acessar modo de configuração global
	configure terminal
	
		!Acessando a Interface Física GigabitEthernet 0/0
		interface gigabitEthernet 0/0
			
			!Inicializando a Interface Física gigabitEthernet 0/0
			no shutdown
			
			!Saindo da Interface Física gigabitEthernet 0/0
			exit

		!OBSERVAÇÃO IMPORTANTE: veja o arquivo 00-DocumentacaoDaRede.txt a partir da linha: 77 
		!(TERCEIRA ETAPA: Determinação das Redes (Sub-Redes) e VLAN (Virtual-LAN) de Cada Grupo)
		interface gigabitEthernet 0/0.???
			description Subinterface da VLAN de SVI do Switch Layer 3 3560 do Grupo-0???
			encapsulation dot1Q ???
			ip address 172.16.???.254 255.255.255.0
			exit

		!Configurando a Subinterface da VLAN do Primeiro Usuário
		interface gigabitEthernet 0/0.???
			description Subinterface da VLAN do ???Primeiro_Nome_do_Primeiro_Aluno???
			encapsulation dot1Q ???
			ip address 172.16.???.254 255.255.255.0
			exit

		!Configurando a Subinterface da VLAN do Segundo Usuário
		interface gigabitEthernet 0/0.???
			description Subinterface da VLAN do ???Primeiro_Nome_do_Segundo_Aluno???
			encapsulation dot1Q ???
			ip address 172.16.???.254 255.255.255.0
			exit

		!Configurando a Subinterface da VLAN do Terceiro Usuário
		interface gigabitEthernet 0/0.???
			description Subinterface da VLAN do ???Primeiro_Nome_do_Terceiro_Aluno???
			encapsulation dot1Q ???
			ip address 172.16.???.254 255.255.255.0
			exit

		!Configurando a Subinterface da VLAN do Quarto Usuário
		interface gigabitEthernet 0/0.???
			description Subinterface da VLAN do ???Primeiro_Nome_do_Quarto_Aluno???
			encapsulation dot1Q ???
			ip address 172.16.???.254 255.255.255.0
			exit

		!Configurando a Subinterface da VLAN Wireless
		interface gigabitEthernet 0/0.???
			description Subinterface da VLAN Wireless
			encapsulation dot1Q ???
			ip address 172.16.???.254 255.255.255.0
			end
		
!Salvando as configurações
copy running-config startup-config
	
!Visualizando as configurações
show running-config

!Visualizando as configurações de endereçamento IPv4
show ip interface brief

!Visualizando as informações de Roteamento
show ip route

!Visualizando as informações de Interfaces Conectadas para Roteamento
show ip route connected
```