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

## PRIMEIRA ETAPA: Instalação e Configuração do GNU/Linux Mint e Windows 10

**OBSERVAÇÃO IMPORTANTE: Utilizar as máquinas virtuais do Linux Mint e Windows 10 no VirtualBOX, nesse cenário as máquinas virtuais estarão conectadas na Rede do Switch Cisco Catalyst 3560 e vai obter os endereços IPv4 fornecidos pelo Router Cisco 2911**

01. Alterar a Porta de Rede da Máquina VirtualBOX

		LinuxMint
			Propriedades
				Rede
					Adaptador 1
						Conectado a: Placa em mode Bridge (Alterar)
						Nome: Realtek PCI GbE Family Controller (Alterar)
			<OK>

		Windows10
			Propriedades
				Rede
					Adaptador 1
						Conectado a: Placa em mode Bridge (Alterar)
						Nome: Realtek PCI GbE Family Controller (Alterar)
			<OK>

02. Conectar o Cabo de Rede na Placa de Rede Off-Board do Desktop

		a) Conectar o cabo de rede na placa de rede off-board;
		b) Conectar o cabo de rede no ponto de rede do Rack Cisco do seu usuário;
		c) Verificar se os LED's da Placa de Rede e Switch estão ligados;
		d) Desativar e Ativar novamente a Placa de Rede no Linux Mint.

03. Ligar as Máquinas Virtuais e verificar se obteve os endereços IPv4
	
		Linux Mint
		Terminal: Ctrl + Alt + T 
			ifconfig (verificar a linha: inet 172.16.???.??? da sua Sub-Rede)
			route -n (verificar a linha: 0.0.0.0 172.16.???.254 da sua Sub-Rede)
			resolvectl (verificar a linha: DNS Servers 8.8.8.8)

		Windows 10
		Powershell
			ipconfig /all (verificar a linha: da sua Sub-Rede)
			ipconfig /all (verificar a linha: da sua Sub-Rede)
			ipconfig /all (verificar a linha: da sua Sub-Rede)

04. Testar o ping no Router e Switch

		Linux Mint ou Windows 10 
			ping 172.16.???.253
			ping 172.16.???.254

05. Acessar remotamente o Switch Cisco Catalyst 3560 e Router Cisco 2911 utilizando o SSH

		Linux Mint
		Terminal: Ctrl + Alt + T 
			#Linha do SSH para acessar o Switch
			#OBSERVAÇÃO IMPORTANTE: existe somente a Primeira Sub-Rede para acessar o Switch
			ssh -oKexAlgorithms=+diffie-hellman-group1-sha1 -oHostKeyAlgorithms=+ssh-rsa -c aes256-cbc seu_usuario@172.16.???.253
			
			#Linha do SSH para acessar o Router
			#OBSERVAÇÃO IMPORTANTE: alterar a Sub-Rede para cada usuário a Rede
			ssh -oKexAlgorithms=+diffie-hellman-group1-sha1 -oHostKeyAlgorithms=+ssh-rsa -c aes256-cbc seu_usuario@172.16.???.254
		
		Windows 10
		Powershell
			#Linha do SSH para acessar o Switch
			#OBSERVAÇÃO IMPORTANTE: existe somente a Primeira Sub-Rede para acessar o Switch
			ssh -oKexAlgorithms=+diffie-hellman-group1-sha1 -oHostKeyAlgorithms=+ssh-rsa -c aes256-cbc seu_usuario@172.16.???.253
			
			#Linha do SSH para acessar o Router
			#OBSERVAÇÃO IMPORTANTE: alterar a Sub-Rede para cada usuário a Rede
			ssh -oKexAlgorithms=+diffie-hellman-group1-sha1 -oHostKeyAlgorithms=+ssh-rsa -c aes256-cbc seu_usuario@172.16.???.254
