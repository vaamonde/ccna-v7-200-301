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
Data de atualização: 18/05/2024<br>
Versão: 0.02<br>
Testado e homologado no Cisco Packet Tracer 8.2.x e Rack Cisco SW-3560 e RT-2911

## INFORMAÇÕES IMPORTANTES SOBRE ESSA DOCUMENTAÇÃO:

A) **ACRÉSCIMO:** informações ou comandos que não estava no script original e nem comentado no vídeo, algo importante para o cenário ou dicas de alunos;<br>
B) **DESAFIO:** desafio proposto para o aluno, com o objetivo de estimular o raciocínio lógico para a resolução de problemas de rede ou mudanças nas configurações;<br>
C) **DICA:** informações importantes da tecnologia ou da prova de certificação, dica para configurar ou lembrar os recursos para sua configuração no exame;<br>
D) **ERRATA:** correções dos scripts, correções de falas, correções de configurações, etc...;<br>
E) **EXEMPLO:** exemplos de comandos ou configurações das opções de DICAS ou OBSERVAÇÃO;<br>
F) **IMPORTANTE:** informações importantes da tecnologia ou da configuração, com foco em adicionar informações detalhadas da tecnologia ou da certificação;<br>
G) **OBSERVAÇÃO:** informações relevantes da tecnologia ou da configuração, com foco em adicionar informações extras da tecnologia ou da certificação.

## PRIMEIRA ETAPA: Acessando o Modo de Configuração Global do Router Cisco 1941.

01. Acessando o modo EXEC Privilegiado e o modo de Configuração Global de Comandos.

		AVISO: acesso autorizado somente a funcionarios
		User Access Verification
		Username: senac
		Password: 123@senac

		!Alterando para o Modo EXEC Privilegiado
		rt-01> enable
		Password: 123@senac

		!Acessando o Modo de Configuração Global
		rt-01# configure terminal
		rt-01(config)#

## SEGUNDA ETAPA: Configuração da Interface LAN do Router no Cisco IOS.

01. Acessando a Interface GigabitEthernet 0/0 da LAN.

**DICA-01:** é recomendado utilizar a Interface GigabitEthernet 0/0 ou outra Interface para as Configurações da Rede Local LAN (Local Area Network).

	rt-01(config)# interface gigabitEthernet 0/0

a) Configuração da Descrição da Interface GigabitEthernet 0/0 da LAN.

**DICA-02:** sempre utilizar o comando: *description* nas Interfaces para efeito de documentação.

**OBSERVAÇÃO-01:** documentação de Interface facilita o processo de identificação e função dela na topologia de rede, configuração obrigatória em Switch ou Router.

	rt-01(config-if)# description Interface de Gateway da Rede LAN

b) Configuração do Endereçamento IPv4 da Interface GigabitEthernet 0/0 da LAN.

**OBSERVAÇÃO-02:** configuração do endereço IPv4 deve ser: *IPv4 + Máscara de Rede Completa (ClassFull)*, não utilizar CIDR (Classes Inter-Domain Routing) nas configurações.

**OBSERVAÇÃO-03:** essa Interface será o endereço de Gateway da Topologia da Rede LAN.

	rt-01(config-if)# ip address 192.168.1.254 255.255.255.0

c) Inicializando a Interface GigabitEthernet 0/0 da LAN.

**DICA-03:** por padrão todas as Interfaces dos Roteadores estão no status: *desligada (Shutdown)*.

**OBSERVAÇÃO-04:** por padrão todas as Interfaces dos Roteadores estão com o status: *Administratively Down (Desligada Administrativamente)*.

	rt-01(config-if)# no shutdown

d) Saindo de todos os níveis e voltando para o modo EXEC Privilegiado.

**DICA-04:** somente no modo EXEC Privilegiado você tem o comando: *copy* para salvar as configurações.

	rt-01(config-if)# end

e) Salvando as configurações da memória RAM (Running-Config) para a memória NVRAM (Startup-Config)

**DICA-05:** nunca esqueça de salvar as configurações.

	rt-01# copy running-config startup-config

02. Visualizando as configurações da memória RAM (Running-Config).

**DICA-06** após a configuração da Interface GigabitEthernet 0/0 da LAN, verifique se tudo está configurado de forma correta utilizando os comandos: *show*.
	
	!Visualizando as Configurações do Running-Config (RAM)
	rt-01# show running-config

	!Fazendo um Filtro na Visualização do Running-Config somente da Interface GigabitEthernet 0/0
	rt-01# show running-config | section include interface gigabitEthernet 0/0

	!Visualizando informações detalhadas da Interface GigabitEthernet 0/0
	rt-01# show interface gigabitEthernet 0/0

	!Visualizando as configurações das Interfaces do Router
	rt-01# show ip interface brief

	!Visualizando informações de roteamento
	rt-01# show ip route

## TERCEIRA ETAPA: Testando e Acessando Remotamente do Router Cisco 1941.

01. Testando as Conexão do Desktop no Router e Acessando Remoto via SSH.

a) Abrindo o Prompt de Comando do Desktop;

**DICA-07** não confunda Terminal com Command Prompt, Terminal é utilizado para se conectar no Switch ou Router utilizando o Cabo Console, já o Command Prompt (Prompt de Comando) é utilizado para testar as configurações de rede e acessar remotamente o Switch ou Router.

	!Verificando o endereço IPv4 configurado no Desktop
	C:\> ipconfig

	!Verificando o endereço detalhado IPv4 configurado no Desktop
	C:\> ipconfig /all

	!Testando a comunicação com o Router utilizando o pacote ICMP (Internet Control Message Protocol)
	C:\> ping 192.168.1.254   (Router RT-01)

	!Testando o acesso remoto no Router utilizando o protocolo Telnet (Teletype Network)
	C:\> telnet 192.168.1.254   (Router RT-01)

	!Acessando remotamente o Router utilizando o protocolo SSH (Secure Shell)
	!OBSERVAÇÃO: -l (éli não é o número "1" (um) e sim "l" (éli) em minúsculo)
	C:\> ssh -l senac 192.168.1.254   (Router RT-01)