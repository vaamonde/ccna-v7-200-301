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

## PRIMEIRA ETAPA: Acessando o Modo de Configuração Global do Switch Cisco Catalyst 2960.

01. Acessando o modo EXEC Privilegiado e o modo de Configuração Global de Comandos.

		AVISO: acesso autorizado somente a funcionarios
		User Access Verification
		Username: senac
		Password: 123@senac

		sw-01> enable
		Password: 123@senac

		sw-01# configure terminal
		sw-01(config)#

## SEGUNDA ETAPA: Configuração do Gateway padrão IPv4 no Cisco IOS.

01. Configuração do Gateway Padrão IPv4 no Switch para Acesso Remoto.

**DICA-01:** configuração do Gateway IPv4 em Switch Cisco Catalyst Layer 2 serve somente para acesso remoto com finalidade de monitoramento/gerenciamento do Switch;

**DICA-02:** em Switch Cisco Catalyst Layer 3 o recurso de Gateway é utilizado tanto para acesso remoto ou para roteamento de Redes/Sub-Redes utilizando principalmente VLAN (Virtual-LAN) ou Protocolos de Roteamento.

**OBSERVAÇÃO-01:** esse recurso é necessário para administração remota ou monitoramento do Switch Cisco Catalyst Layer 2 ou Layer 3.

**OBSERVAÇÃO-02:** existe a possibilidade da configuração do Gateway utilizar o endereço IPv6 em Switch Cisco Catalyst Layer 2 ou Layer 3, para essa configuração é recomendo atualizar o Cisco IOS para a versão no mínimo 15.x (versão padrão no Cisco Packet Tracer 12.x).

	sw-01(config)# ip default-gateway 192.168.1.254

## TERCEIRA ETAPA: Configuração da Interface SVI no Cisco IOS.

01. Configuração da Interface Virtual do Switch SVI (Switch Virtual Interface) no Switch.

**DICA-03:** interfaces virtuais são criadas utilizando o recurso de VLAN (Virtual-LAN) disponível nos Switch Cisco Catalyst Layer 2 ou Layer 3.

**DICA-04:** é recomendado utilizar outra VLAN para o SVI, não é recomendado utilizar a VLAN padrão 1 para essa finalidade, a VLAN 1 (VLAN Default) existe em todos os Switch e é por causa disso que Switches de Fabricantes Diferente se comunicam entre si, todos utilizam sempre a VLAN 1 como padrão para a comunicação.

**OBSERVAÇÃO-03:** em Switch Cisco Catalyst Layer 2 utilizamos o SVI somente para administração remota ou monitoramento do equipamento, ela não será utilizada para Gateway da Rede Local ou para integração com Protocolos de Roteamento.

**OBSERVAÇÃO-04:** o SVI é necessário para o acesso remoto nas Linhas Virtuais (VTY) utilizando os protocolos Telnet, SSH ou outro protocolo configurado, após a configuração da SVI o Switch irá possuir um Endereço Lógico de Rede (IPv4 ou IPv6) permitindo o seu acesso remoto.

	sw-01(config)# interface vlan 1
		
a) Configuração da Descrição da Interface Virtual VLAN-1.

**DICA-05:** sempre utilizar o comando: *description* nas Interfaces para efeito de documentação.

**OBSERVAÇÃO-05:** documentação de Interface facilita o processo de identificação e função dela na topologia de rede, configuração obrigatória em Switch ou Router.

	sw-01(config-if)# description Interface de Gerenciamento do Switch SW-01

b) Configuração do Endereçamento IPv4 da Interface Virtual VLAN-1.

**DICA-06:** o endereço IPv4 deve ser da mesma faixa de Rede ou Sub-Rede do Gateway Padrão utilizado no Switch na Segunda Etapa.

**DICA-07:** é recomendado que os endereços de Rede ou Sub-Redes dos Switches sejam diferentes das Redes dos Desktops, Notebook, Wi-Fi (Wireless/Sem-Fio), CFTV (Circuito Fechado de TV), etc... para garantir a segurança de acesso dos equipamentos somente para a equipe/profissionais de TI que esteja nessa mesma Rede/Sub-Rede.

**OBSERVAÇÃO-06:** configuração do endereço IPv4 deve ser: *IPv4 + Máscara de Rede Completa (ClassFull)*, não utilizar CIDR (Classes Inter-Domain Routing) nas configurações.

	sw-01(config-if)# ip address 192.168.1.250 255.255.255.0

c) Inicializando a Interface Virtual da VLAN-1.

**DICA-08:** por padrão todas as Interfaces estão no status: *desligada (Shutdown)* no Switch ou Router.

**DICA-09:** por padrão todas as Portas de Rede estão no status: *ligada (No-Shutdown)* no Switch.

**OBSERVAÇÃO-07:** o comando: *no* também é utilizado para ligar as Interfaces tirando do status: *shutdown (Desligada)* e mudando o seu status para: *no shutdown (Ligada)*.

	sw-01(config-if)# no shutdown

d) Saindo de todos os níveis e voltando para o modo EXEC Privilegiado.

**DICA-10:** somente no modo EXEC Privilegiado você tem o comando: *copy* para salvar as configurações.

**DICA-11:** existe também o comando: *do*, esse comando permite executar qualquer comando fora do seu nível padrão.

**EXEMPLO: sw-01(config-line)# do copy running-config startup-config | sw-01(config-line)# do show running-config | sw-01(config-line)# do write**

	sw-01(config-if)# end

e) Salvando as configurações da memória RAM (Running-Config) para a memória NVRAM (Startup-Config)

**DICA-12:** nunca esqueça de salvar as configurações.

	sw-01# copy running-config startup-config

09. Visualizando as configurações da memória RAM (Running-Config).

**DICA-12** após a configuração da SVI verifique se tudo está configurado de forma correta utilizando os comandos: *show*.
	
	!Visualizando as Configurações do Running-Config (RAM)
	sw-01# show running-config

	!Fazendo um Filtro na Visualização do Running-Config somente da Interface Vlan1
	sw-01# show running-config | section include interface Vlan1

	!Visualizando as configurações das interfaces e portas de rede do Switch
	sw-01# show ip interface brief

	!Visualizando as configurações das VLAN's padrão do Switch
	sw-01# show vlan brief

f) Testando a conectividade entre o Switch e os Desktops da Rede

**DICA-13** depois da configuração da SVI no Switch Cisco Catalyst Layer 2 você consegue agora pingar os Desktops da Rede utilizado o Protocolo ICMP (Internet Control Message Protocol) como comando: *ping* para testar a interconectividade de rede.

**OBSERVAÇÃO-05** o carácter: *! (exclamação)* utilizado no comando: ping significa que os pacotes ICMP enviado para o destino foi recebido com sucesso, parão é enviar: *5 Pacotes (Sending 5)* já o carácter: *. (ponto)* significa que os pacotes ICMP foram perdidos ou o destino não recebeu os pacotes.

	!Pingando a SVI do Switch Layer 2
	sw-01# ping 192.168.1.250
		Type escape sequence to abort.
		Sending 5, 100-byte ICMP Echos to 192.168.1.250, timeout is 2 seconds:
		!!!!!
		Success rate is 100 percent (5/5), round-trip min/avg/max = 8/10/15 ms

	!Pingando o Servidor
	sw-01# ping 192.168.1.1

## TERCEIRA ETAPA: Automatizando a Configuração do Segundo Switch Cisco Catalyst 2960.

01. Utilizando o Visual Studio Code (VSCode) para automatizar as configurações do Cisco IOS.

**OBSERVAÇÃO-06:** recomendamos sempre utilizar um *Editor de Texto Profissional* para criar os scripts e automatizar as tarefas de configuração do Cisco IOS, hoje em dia é indicado utilizar o Visual Studio Code (VSCode) junto com as Extensões: *Cisco IOS Syntax e Cisco Config Highlight* para facilitar essa configuração.

**DICA-14:** o caractere: *! (exclamação)* é utilizado como um recurso de *Comentário*, sua utilização server para comentar o código de automação do Cisco IOS ou para desativar um comando para não ser executado, *RECOMENDO FORTEMENTE DOCUMENTAR TODOS OS COMANDOS E PROCEDIMENTOS DE CONFIGURAÇÃO PARA FACILITAR O ENTENDIMENTO.*

**DICA-15:** para facilitar a leitura do código, recomendo utilizar o recurso de **Indentação de Código** usando a Tecla TAB (Tabulador/Tabulação) para cada nível que você está configurando o Cisco IOS, isso facilitada a análise de erros (Debug) do código.

```python
!Acessando o modo EXEC Privilegiado
enable

	!Acessando o modo de Configuração Global de comandos
	configure terminal
	
	!Configuração do Gateway padrão IPv4 no Switch
	ip default-gateway 192.168.1.254
  
	!Configuração da Interface Virtual do Switch SVI
	interface vlan 1
		
		!Configuração da Descrição da Interface Virtual
		description Interface de Gerenciamento do Switch SW-02
		
		!Configuração do Endereçamento IPv4 da Interface Virtual
		ip address 192.168.1.251 255.255.255.0
		
		!Inicializando a Interface Virtual do Switch
		no shutdown
		
		!Saindo de todos os níveis e voltando para o modo EXEC Privilegiado
		end

!Salvando as configurações da memória RAM para a memória NVRAM
write
```