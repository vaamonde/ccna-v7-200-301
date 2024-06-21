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
Data de atualização: 13/06/2024<br>
Versão: 0.04<br>
Testado e homologado no Cisco Packet Tracer 8.2.x e Rack Cisco SW-3560 e RT-2911

## INFORMAÇÕES IMPORTANTES SOBRE ESSA DOCUMENTAÇÃO:

A) **ACRÉSCIMO:** informações ou comandos que não estava no script original e nem comentado no vídeo, algo importante para o cenário ou dicas de alunos;<br>
B) **DESAFIO:** desafio proposto para o aluno, com o objetivo de estimular o raciocínio lógico para a resolução de problemas de rede ou mudanças nas configurações;<br>
C) **DICA:** informações importantes da tecnologia ou da prova de certificação, dica para configurar ou lembrar os recursos para sua configuração no exame;<br>
D) **ERRATA:** correções dos scripts, correções de falas, correções de configurações, etc...;<br>
E) **EXEMPLO:** exemplos de comandos ou configurações das opções de DICAS ou OBSERVAÇÃO;<br>
F) **IMPORTANTE:** informações importantes da tecnologia ou da configuração, com foco em adicionar informações detalhadas da tecnologia ou da certificação;<br>
G) **OBSERVAÇÃO:** informações relevantes da tecnologia ou da configuração, com foco em adicionar informações extras da tecnologia ou da certificação.

## PRIMEIRA ETAPA: Conhecendo as VLANs (Virtual LANs – Redes Locais Virtuais) no Cisco Packet Tracer.

As VLANs (Virtual LANs – Redes Locais Virtuais) é uma rede logicamente independente, várias VLANs podem coexistir em um mesmo Switch, de forma a dividir uma rede local em mais de uma rede, criando domínios de Broadcast separados.

As VLANs permitem a segmentação das redes físicas, sendo que a comunicação entre máquinas de VLANs diferentes terá de passar obrigatoriamente por um **Roteador** ou outro equipamento capaz de realizar o **Roteamento**, esse equipamento será o responsável por encaminhar o tráfego entre as VLANs distintas (iguais).

As VLANs oferecem vantagens das quais se destacam: *segurança, escalabilidade, flexibilidade, redução de custos, etc.*

Um Switch com a capacidade de criar VLANs suporta dois tipos de configurações de porta: 

1. **Access Port** (porta de acesso para conexões de dispositivos finais);<br>
2. **Trunk Port** (porta de tronco para interligação de Switch, Router ou Server).

## SEGUNDA ETAPA: Conhecendo os Ranges das VLANs no Cisco Packet Tracer.

Os range de VLANs nos Switches Cisco são divididos em: 

A) **0 e 4095** Reservadas (Reserved - apenas para uso do sistema operacional IOS, você não pode ver ou usar essas VLANs);<br>
B) **1 Padrão/Nativa** (Default/Native - você pode usar essa VLAN, está associada por padrão em todas as Portas do Switch, você não pode deletar essa VLAN);<br> 
C) **2 até 1001 Nativas** (Normal - usadas para as VLANs Ethernet, você pode criar, usar e excluir essas VLANs, são armazenadas no arquivo **vlan.dat**);<br> 
D) **1002 até 1005 Nativa** (Normal - padrões da Cisco para Redes FDDI (Fiber Distributed Data Interface) e Token Ring, você não pode excluir essas VLANs);<br>
E) **1006 até 4094 Estendidas** (Extended elas são usadas principalmente em redes de provedores de serviços para permitir o provisionamento do número do assinante).

## TERCEIRA ETAPA: Tipos de VLANs no Cisco Packet Tracer.

Exite também dois tipos de associações de VLANs: 

A) **VLANs Estáticas** (Static - configurada manualmente na porta de rede do Switch ou do Router);<br>
B) **VLANs Dinâmicas** (Dynamic - são criadas e alteradas dinamicamente via Software como por exemplo o VMPS (VLAN Management Policy Server)).

## QUARTA ETAPA: Conhecendo os Tipos de Portas das VLANs no Cisco Packet Tracer.

Uma Porta de **Acesso (access)**, permite associar uma porta do Switch a uma VLAN, as portas do tipo acesso são usadas para conectar dispositivos finais (Desktop, Notebook, Impressoras, Access Point, etc), por padrão, todas as portas dos Switches estão associadas na *VLAN Padrão/Nativa 1*, que transporta os dados sem marcação (Untagged VLAN).

## QUINTA ETAPA: Configurando as VLANs no Switch Multilayer 3650 (CENTRO - DISTRIBUIÇÃO)
```python
!Acessando o modo Exec Privilegiado
enable

	!Acessando o modo de Configuração Global de Comandos
	configure terminal

		!Criando as VLANs Standard (Padrão) no Switch Multilayer 3650
		!DICA: por padrão é recomendado trabalhar nos Switches Catalyst ou Multilayer a faixa de VLANs 
		!Standard (padrão de 2 até 1001)
		vlan 10

			!Configurando o nome da VLAN Standard
			!DICA: a configuração do nome da VLAN facilita na administração e auditoria com o comando: 
			!show vlan brief
			!OBSERVAÇÃO: para criar uma nova VLAN não é necessário sair do modo de configuração de VLAN 
			!com o comando exit, pode digitar no mesmo prompt.
			name switch
		
		vlan 20
			name server 
		vlan 30
			name wireless 
		vlan 40
			name estoque
		vlan 50
			name financeiro
		vlan 60
			name gerencia
			exit

		!Configurando a Interface de Gerenciamento SVI do Switch Multilayer 3650
		!OBSERVAÇÃO: as SVIs dos Switches Layer 2 e 3 serão configuradas utilizando a VLAN 10
		interface vlan 10
			description Interface de SVI de Gerenciamento Switch Multilayer 3650
			ip address 192.168.10.254 255.255.255.0
			no shutdown
			exit

		!Configurando a Interface de Acesso a VLAN 20 dos Servidores
		!DICA: a opção range do comando interface possibilita fazer a mesma configuração em várias interfaces
		!OBSERVAÇÃO: existe a possibilidade de utilizar a opção de range para portas não consecutivas, 
		!utilizando o separador , (vírgula) e adicionando o nome das portas na configuração.
		!EXEMPLO: interface range fastEthernet 0/1 - 5 , fastEthernet 0/10, fastEthernet 0/15
		interface range GigabitEthernet 1/0/10 - 12
			
			!Descrição das Interfaces dos Servidores
			description Interface de Acesso da VLAN 20 dos Servidores

			!Configurando a Interface (Porta de Rede) para o Modo de Acesso (Access)
			!DICA: uma Interface de Acesso pertence e trafega dados de uma única VLAN
			!OBSERVAÇÃO: por padrão todos os Switches tem a VLAN 1 que não pode ser removida e está associada 
			!a todas as Interfaces, é recomendado sempre configurar as Interfaces dos dispositivos finais para 
			!o Modo Acesso (Access).
			!OBSERVAÇÃO: tipos de configuração: access (porta de acesso), trunk (porta de tronco) e dynamic 
			!(porta dinâmica) 
			switchport mode access

			!Desabilitando o recurso de auto-negociação da Interface (Porta de Rede)
			!DICA: por padrão todas as Interfaces dos Switches está com o recurso do DTP (Dynamic Trunk 
			!Protocol) habilitado
			!OBSERVAÇÃO: é recomendado desabilitar o recurso de DTP nas Interfaces que são do tipo Acesso 
			!(Access) para que servidores ou clientes configure as opção de Trunk nessas portas.
			switchport nonegotiate

			!Configurando o acesso a VLAN 20 das Interfaces dos Servidores
			!DICA: por padrão só podemos configurar uma VLAN na porta de rede do Switch
			!OBSERVAÇÃO: a partir do momento que configuramos a VLAN na porta do Switch, todos os quadros 
			!(frames) recebem a Tag (etiqueta) dot1q (IEEE 802.1Q) no seu frame (quadro) Ethernet quando 
			!transmite pacotes pela porta de rede do switch
			switchport access vlan 20
			exit

		!Configurando a Interface de Acesso a VLAN 30 do Access Point 802.11-AC
		interface GigabitEthernet 1/0/23
			description Interface de Acesso da VLAN 30 do Access Point AC
			switchport mode access
			switchport nonegotiate
			switchport access vlan 30
			exit

		!Acessando todas as Interfaces (Porta de Rede) que não estão sendo utilizadas
		interface range GigabitEthernet 1/0/5 - 9, GigabitEthernet 1/0/13 - 22,  GigabitEthernet 1/1/1 - 4
			
			!Desligando as Interfaces
			shutdown
			
			!Saindo de todos os níveis e voltando para o modo EXEC Privilegiado
			end

!Salvando as configurações da memória RAM para a memória NVRAM
write
```

## SEXTA ETAPA: Configurando as VLANs no Switch Cisco Layer 2 2960 (LADO ESQUERDO - ACESSO)
```python
!Acessando o modo Exec Privilegiado
enable

	!Acessando o modo de Configuração Global de Comandos
	configure terminal

		!Criando as VLANs Standard (Padrão) no Switch 2960
		vlan 10
			name switch
		vlan 20
			name server
		vlan 30
			name wireless
		vlan 40
			name estoque
		vlan 50
			name financeiro
		vlan 60
			name gerencia
			exit

		!Configurando a Interfaces de SVI do Switch 2960
		interface vlan 10
			description Interface de SVI de Gerenciamento Switch Layer 2 2960
			ip address 192.168.10.250 255.255.255.0
			no shutdown
			exit

		!Configurando a Interface da VLAN 40 Estoque
		interface fastEthernet 0/1
			description Interface de Acesso da VLAN 40 Estoque
			switchport mode access
			switchport nonegotiate
			switchport access vlan 40
			exit

		!Configurando a Interface da VLAN 50 Financeiro
		interface fastEthernet 0/2
			description Interface de Acesso da VLAN 50 Financeiro
			switchport mode access
			switchport nonegotiate
			switchport access vlan 50
			exit

		!Configurando a Interface da VLAN 60 Gerencia
		interface fastEthernet 0/3
			description Interface de Acesso da VLAN 60 Gerencia
			switchport mode access
			switchport nonegotiate
			switchport access vlan 60
			exit

		!Desligando as Interfaces que não estão sendo utilizadas
		interface range fastEthernet 0/4 - 22
			shutdown
			exit

		!Configurando o Gateway Padrão do Gerenciamento do Switch Layer 2 2960
		ip default-gateway 192.168.10.254
		end
write
```

## SÉTIMA ETAPA: Configurando as VLANs no Switch Cisco Layer 2 2960 (LADO DIREITO - ACESSO)
```python
!Acessando o modo Exec Privilegiado
enable

	!Acessando o modo de Configuração Global de Comandos
	configure terminal

		!Criando as VLANs Standard (Padrão) no Switch 2960
		vlan 10
			name switch
		vlan 20
			name server
		vlan 30
			name wireless
		vlan 40
			name estoque
		vlan 50
			name financeiro
		vlan 60
			name gerencia
			exit

		!Configurando a Interfaces de SVI do Switch 2960
		interface vlan 10
			description Interface de SVI de Gerenciamento Switch Layer 2 2960
			ip address 192.168.10.251 255.255.255.0
			no shutdown
			exit

		!Configurando a Interface da VLAN 40 Estoque
		interface fastEthernet 0/1
			description Interface de Acesso da VLAN 40 Estoque
			switchport mode access
			switchport nonegotiate
			switchport access vlan 40
			exit

		!Configurando a Interface da VLAN 50 Financeiro
		interface fastEthernet 0/1
			description Interface de Acesso da VLAN 50 Financeiro
			switchport mode access
			switchport nonegotiate
			switchport access vlan 50
			exit

		!Configurando a Interface da VLAN 60 Gerencia
		interface fastEthernet 0/1
			description Interface de Acesso da VLAN 60 Gerencia
			switchport mode access
			switchport nonegotiate
			switchport access vlan 60
			exit

		!Desligando as Interfaces que não estão sendo utilizadas
		interface range fastEthernet 0/4 - 22
			shutdown
			exit

		!Configurando o Gateway Padrão do Gerenciamento do Switch Layer 2 2960
		ip default-gateway 192.168.10.254
		end
write
```

## OITAVA ETAPA: Verificando as Configurações dos Switches e Roteadores.

	!Visualizando as Configurações do Running-Config (RAM)
	show running-config

	!Visualizando as configurações da memória RAM
	show running-config | section interface

	!Verificando as informações das VLAN (Tabela, Id e Name)
	show vlan brief
	show vlan id 10
	show vlan name svi