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

## PRIMEIRA ETAPA: Configuração das VLAN's e Trunk no Switch Cisco Catalyst 3560 

```python
!Acessando o modo Exec Privilegiado
enable

	!Acessar modo de configuração global
	configure terminal

		!Criando as VLANs Standard (Padrão) no Switch Layer 3 3560
		!OBSERVAÇÃO IMPORTANTE: veja o arquivo 00-DocumentacaoDaRede.txt a partir da linha: 77
		!(TERCEIRA ETAPA: Determinação das Redes (Sub-Redes) e VLAN (Virtual-LAN) de Cada Grupo)

		!Criação da VLAN padrão de SVI do Grupo
		vlan ???
			!Nome da VLAN padrão
			name svig0???
		vlan ???
			name ???Primeiro_Nome_do_Primeiro_Aluno??? 
		vlan ???
			name ???Primeiro_Nome_do_Segundo_Aluno???
		vlan ???
			name ???Primeiro_Nome_do_Terceiro_Aluno???
		vlan ???
			name ???Primeiro_Nome_do_Quarto_Aluno???
		vlan ???
			name wifi
			exit

		!OBSERVAÇÃO IMPORTANTE: a Interface fastEthernet 0/1 não será usada.
		
		!Configurando a Interface de Acesso a VLAN do Primeiro Usuário
		interface fastEthernet 0/2
			
			!Configurando a Interface de Acesso a VLAN
			description Interface de Acesso da VLAN ??? do ???Nome_E_Sobrenome_Primeiro_Usuário???
			
			!Configurando o Modo de Acesso da Interface
			switchport mode access
			
			!Configurando o Acesso a VLAN
			switchport access vlan ???
			
			!Saindo da configuração da Interface
			exit
		
		!Configurando a Interface de Acesso a VLAN do Segundo Usuário
		interface fastEthernet 0/3
			description Interface de Acesso da VLAN ??? do ???Nome_E_Sobrenome_Segundo_Usuário???
			switchport mode access
			switchport access vlan ???
			exit

		!Configurando a Interface de Acesso a VLAN do Terceiro Usuário
		interface fastEthernet 0/4
			description Interface de Acesso da VLAN ??? do ???Nome_E_Sobrenome_Terceiro_Usuário???
			switchport mode access
			switchport access vlan ???
			exit

		!Configurando a Interface de Acesso a VLAN do Quarto Usuário
		interface fastEthernet 0/5
			description Interface de Acesso da VLAN ??? do ???Nome_E_Sobrenome_Quarto_Usuário???
			switchport mode access
			switchport access vlan ???
			exit

		!Configurando a Interface de Acesso a VLAN da Rede Sem-Fio (Wi-Fi/Wireless)
		interface fastEthernet 0/6
			description Interface de Acesso da VLAN ???Wireless do Grupo-0???
			switchport mode access
			switchport access vlan ???
			exit
		
		!Desativando as Interfaces que não serão utilizadas no Switch Layer 3 3560
		interface range fastEthernet 0/7 - 23
			shutdown
			exit

		!Configurando a Interface de Trunk com o Router 2911
		interface fastEthernet 0/24
			description Interface de Trunk com o Router 2911 do Grupo-0???
			switchport trunk encapsulation dot1q
			switchport mode trunk
		end

!Salvando as configurações
copy running-config startup-config
	
!Visualizando as configurações
show running-config

!Visualizando as configurações de endereçamento IPv4
show ip interface brief

!Visualizando as informações de VLAN
show vlan brief

!Visualizando informações de uma VLAN utilizando o ID
show vlan id ???

!Visualizando informações de uma VLAN utilizando o Nome
show vlan name ???

!Visualizando as informações de Status das Interfaces
show interface status

!Visualizando informações de Interfaces Trunk
show interface trunk

!Visualizando informações detalhadas das Interfaces de Trunk
show interfaces fastEthernet 0/24 status
show interfaces fastEthernet 0/24 switchport

!Comandos para testar a conexão com o Router

!Pingando o endereço de SVI do Switch
ping 172.16.???.253

!Pingando o endereço de Gateway do Router
ping 172.16.???.254

!Acessando via SSH o Router do Switch
!OBSERVAÇÃO: -l (éli não é o número "1" (um) e sim "l" (éli) em minúsculo)
ssh -l ???seu_usuário??? 172.16.???.254
```