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

## PRIMEIRA ETAPA: Conhecendo as Portas Trunk (Tronco) no Cisco Packet Tracer.

Uma **Porta de Tronco (trunk)**, normalmente é usada para interligação de Switches ou ligação de Roteadores e Servidores, ela permite a passagem de tráfego de várias VLANs, configurando uma porta como Trunk, todo o tráfego de todas as VLANs criadas no Switch podem passar por ela, no entanto o administrador pode limitar o número de VLANs que podem passar pelo Trunk.

## SEGUNDA ETAPA: Configurando as Portas Trunk no Switch Multilayer 3650 (CENTRO - DISTRIBUIÇÃO)
```python
!Acessando o modo Exec Privilegiado
enable

	!Acessando o modo de Configuração Global de Comandos
	configure terminal

		!Configurando as Interface de Trunk com os Switches Layer 2 2960
		interface range GigabitEthernet 1/0/1 - 4
			
			!Descrição das Interfaces de Trunk
			description Interface de Trunk com os Switches Layer 2 2960
			
			!Configurando o modo de Trunk (Tronco) da Interfaces
			switchport mode trunk

			!Desabilitando a Auto-negociação da Interface de Trunk
			switchport nonegotiate

			!Saindo de todos os níveis e voltando para o modo EXEC Privilegiado
			end

!Salvando as configurações da memória RAM para a memória NVRAM
write
```

## TERCEIRA ETAPA: Configurando as Portas Trunk no Switch Cisco Layer 2 2960 (LADO ESQUERDO - ACESSO)
```python
!Acessando o modo Exec Privilegiado
enable

	!Acessando o modo de Configuração Global de Comandos
	configure terminal

	!Configuração das Interfaces de Trunk do Switch Layer 2
	interface range GigabitEthernet 0/1 - 2
		description Interface de Trunk com os Switches Layer 2 e 3 
		switchport mode trunk
		switchport nonegotiate
		exit

	!Configuração das Interfaces de Trunk do Switch Layer 2
	interface range FastEthernet 0/23 - 24
		description Interface de Trunk com os Switches Layer 2 e 3 
		switchport mode trunk
		switchport nonegotiate

		!Saindo de todos os níveis e voltando para o modo EXEC Privilegiado
		end

!Salvando as configurações da memória RAM para a memória NVRAM
write
```

## QUARTA ETAPA: Configurando as Portas Trunk no Switch Cisco Layer 2 2960 (LADO DIREITO - ACESSO)
```python
!Acessando o modo Exec Privilegiado
enable

	!Acessando o modo de Configuração Global de Comandos
	configure terminal

	!Configuração das Interfaces de Trunk do Switch Layer 2
	interface range GigabitEthernet 0/1 - 2
		description Interface de Trunk com os Switches Layer 2 e 3 
		switchport mode trunk
		switchport nonegotiate
		exit

	!Configuração das Interfaces de Trunk do Switch Layer 2
	interface range FastEthernet 0/23 - 24
		description Interface de Trunk com os Switches Layer 2 e 3 
		switchport mode trunk
		switchport nonegotiate

		!Saindo de todos os níveis e voltando para o modo EXEC Privilegiado
		end

!Salvando as configurações da memória RAM para a memória NVRAM
write
```

## QUINTA ETAPA: Verificando as Configurações dos Switches.

	!Visualizando as Configurações do Running-Config (RAM)
	show running-config

	!Visualizando as configurações da memória RAM
	show running-config | section interface

	!Verificando as informações das Interfaces de Trunk
	show interface status
	show interface trunk
	show interfaces gigabitEthernet 0/1 status
	show interfaces gigabitEthernet 0/1 switchport