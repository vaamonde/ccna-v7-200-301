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

## Protocolos de Roteamento utilizados no Cisco (APROFUNDAMENTO DE ESTUDO)

**==== TCP e IP ====**

	a) TCP (Transmission Control Protocol - Protocolo de Controle de Transmissão - Confiabilidade)
	b) UDP (User Datagram Protocol - Protocolo de Datagrama do Usuário - Sem Confiabilidade)
	c) IPv4 (Internet Protocol - Protocolo de Internet versão 4 - Decimal)
	d) IPv6 (Internet Protocol - Protocolo de Internet versão 6 - Hexadecimal)

**==== Protocolos IGP, EGP e BGP ====**

	a) IGP (Interior Gateway Protocol - Protocolo de Gateway Interior)
	b) EGP (Exterior Gateway Protocol - Protocolo de Gateway Externo)
	c) BGP (Border Gateway Protocol - Protocolo de Gateway de Borda)

**==== Distância Administrativa (Escolha do Melhor Caminho e Confiabilidade do Link) ====**

	a) AD   0 --> Interface Diretamente Conectada
	b) AD   1 --> Rota Estática, Rota Flutuante ou Gateway Padrão
	c) AD  90 --> EIGRP (Enhanced Interior Gateway Routing Protocol - Protocolo de Roteamento de Gateway Interno Aprimorado)
	d) AD 110 --> OSPF (Open Shortest Path First - Caminho Mais Curto Primeiro)
	e) AD 120 --> RIP (Routing Information Protocol - Protocolo de Informações de Roteamento)

**==== Métrica (Custo do Link) ====**

	a) Rota Estática --> Custo 0
	b) EIGRP         --> Largura de Banda, Atraso, Confiabilidade, Utilização, MTU (Maximum Transmission Unit) e Contagem de Saltos
	c) OSPF          --> Largura de Banda Acumulativa, Menor Custo e Menor Distância
	d) RIP           --> Contagem de Saltos no Máximo de 15 (routes)

## PRIMEIRA ETAPA: Configuração do Protocolo OSPF Router Cisco 2911

```python
!Acessando o modo Exec Privilegiado
enable

	!Acessar modo de configuração global
	configure terminal

		!Configuração da Interface de Loopback 0 (sempre será a Loopback 0, não mudar o número)
		interface loopback 0

			!Descrição da Interface
			description Interface de Loopback para ID do OSPF

			!Endereço IPv4 para o ID do OSPF
			!Verificar o endereçamento IPv4 de Loopback do seu grupo
			!Endereço IPv4 utilizado para o gerenciamento e métrica do OSPF
			!OBSERVAÇÃO IMPORTANTE: veja o arquivo 00-DocumentacaoDaRede.txt a partir da linha: 270 
			!(NOVA ETAPA: Determinação das Configurações do Protocolo de Roteamento Dinâmico OSPF)
			ip address ???.???.???.??? 255.255.255.255

			!Inicializando a interface
			no shutdown

			!Saindo das configurações da Interface
			exit

		!Configurando o Roteamento de OSPF (??? = número de processo local)
		!Verificar a tabela de Endereçamento para ver o seu número de Processo Local
		!Pode existir vários processo locais do OSPF, cada um com uma finalidade diferente
		!OBSERVAÇÃO IMPORTANTE: veja o arquivo 00-DocumentacaoDaRede.txt a partir da linha: 270 
		!(NOVA ETAPA: Determinação das Configurações do Protocolo de Roteamento Dinâmico OSPF)
		router ospf ???

			!Identificação do Roteador
			!Verificar o endereço IPv4 de Loopback do seu grupo
			!OSPF utiliza o endereço de Loopback para gerenciar o processo local
			router-id ???.???.???.???
				
			!Desativando os anúncios do Protocolo OSPF na Interface da LAN
			!Essa interface não vai anunciar suas rotas pela interface, mais pode receber anúncios
			passive-interface gigabitEthernet 0/0

			!Desativando os anúncios do Protocolo OSPF na Interface de Internet
			!Essa interface não vai anunciar suas rotas pela interface, mais pode receber anúncios
			passive-interface gigabitEthernet 0/1

			!Configuração da referência de largura de banda (Métrica)
			!Utilizado para o cálculo de custo dos links, padrão 10^8 = 100000000 bps
			!Link da tabela padrão de métrica do custo dos links do OSPF: 
			!http://nomundodasredes.blogspot.com.br/2012/03/metrica-do-ospf.html
			!https://ciscoredes.com.br/wp-content/uploads/2012/06/Cost_Interface.png
			auto-cost reference-bandwidth 10000

			!Registrar todas as alterações de adjacência e o estado dos links
			!Esses registros vão ficar armazenados no log do sistema
			log-adjacency-changes detail

			!Declarando as redes fisicamente conectadas
			!Utilizando o recurso de Wildcard Mask (máscara coringa - máscara invertida)
			!Configuração da Área 0 (Single Area - Backbone, obrigatória existir)
			!Calculando a máscara coringa: 255.255.255.255 - sua_mascara
			!Exemplo: 255.255.255.255 - 255.255.255.252 = 0.0.0.3
			!OBSERVAÇÃO IMPORTANTE: veja o arquivo 00-DocumentacaoDaRede.txt a partir da linha: 270 
			!(NOVA ETAPA: Determinação das Configurações do Protocolo de Roteamento Dinâmico OSPF)
			network 172.16.???.0 0.0.0.255 area 0
			network 172.16.???.0 0.0.0.255 area 0
			network 172.16.???.0 0.0.0.255 area 0
			network 172.16.???.0 0.0.0.255 area 0
			network 172.16.???.0 0.0.0.255 area 0
			network 172.16.???.0 0.0.0.255 area 0
			network 192.168.1.??? 0.0.0.3 area 0
			network 192.168.1.??? 0.0.0.3 area 0

			!Saindo de todas as configurações
			end

!Salvando todas as configurações
copy running-config startup-config

!Comandos de Verificação do OSPF e da última etapa

!Visualizando as configurações
show running-config

!Visualizando parâmetros e estatísticas do processo do protocolo de roteamento IP
show ip protocols

!Visualizando as configurações de endereçamento IPv4
show ip interface brief

!Visualizando as informações de Roteamento
show ip route

!Visualizando as informações de Roteamento do Open Shortest Path First (OSPF)
show ip route ospf 

!Visualizando as informações do Processo do OSPF
show ip route ospf ??? (ID)

!Visualizando as informações das listas das vizinhanças do OSPF
show ip ospf neighbor

!Visualizando as informações sumarizadas do banco de dados do OSPF
show ip ospf database

!Visualizando as informações dos statos dos links do OSPF
show ip ospf database router

!Visualizando as informações do processo do OSPF
show ip ospf ??? (ID)

!Visualizando as informações de interfaces do OSPF
show ip ospf interface
```

## A PARTIR DESSE MOMENTO TODOS OS GRUPOS DEVERÃO SE PINGAR, PINGAR O ENDEREÇO IPv4 DE CADA SWITCH DOS GRUPOS E TAMBÉM OS DESKTOPS.

```python
!Pingando todos os Grupos o Endereço IPv4 do Switch
ping 172.16.10.253
ping 172.16.20.253
ping 172.16.30.253
ping 172.16.40.253
ping 172.16.50.253
ping 172.16.60.253
```