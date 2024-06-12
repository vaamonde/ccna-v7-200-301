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
		sw-01#

## SEGUNDA ETAPA: Backup das Configurações do Cisco IOS do Primeiro Switch Cisco Catalyst Layer 2 2960

02. Visualizando a versão do Cisco IOS e informações do Hardware do Switch Layer 2 2960.

**DICA-01:** o comando: *show version* é utilizado para verificar a versão de hardware e do Cisco IOS do Switch ou Router.

**DICA-02:** atualmente a versão utilizada nos hardware da Cisco é a 15.x (ou superior, dependendo do modelo)

**OBSERVAÇÃO-01:** as informações de Memória RAM em equipamentos da Cisco estão em: *Kbytes* ou em: *Bytes*, sendo necessário fazer a conversão para: *MBytes* para facilitar a leitura.

**OBSERVAÇÃO-02:** esse comando também mostrar as informações referente a *Configuração do Registro de Inicialização* do equipamento para efeito de manutenção ou Reset.

	sw-01# show version
		cisco WS-C2960-24TT-L (PowerPC405) processor (revision B0) with 65536K bytes of memory.
			65536KB / 1000 = 65MB (65MB de Memória RAM)
		64K bytes of flash-simulated non-volatile configuration memory.
		Configuration register is 0xF

03. Visualizando as informações da inicialização do Switch Layer 2 2960.

**DICA-03:** o comando: *show boot* é utilizado para verificar os arquivos de configuração de inicialização e qual binário do Cisco IOS está habilitado no Switch.

**OBSERVAÇÃO-03:** essas informações são importante para o processo de quebra de senha do Switch se necessário.

	sw-01# show boot
		BOOT path-list      : 2960-lanbasek9-mz.150-2.SE4.bin    (Binário do Cisco IOS)
		Config file         : flash:/config.text                 (Arquivo de Inicialização do Cisco IOS)
		Private Config file : flash:/private-config.text         (Arquivo de Segurança da Inicialização)

04. Visualizando as informações do Flash Card (Memória de Massa) do Switch Layer 2 2960.

**DICA-04:** a memória de massa (Flash Card) em Switch geralmente são Chips soldados ou módulos internos.

**OBSERVAÇÃO-04:** diferente do Router, a memória Flash em Switch não pode ser acessada sem desmontar o equipamento.

	sw-01# show flash:
		64016384 bytes total (59344187 bytes free)
	
	sw-01# dir flash:
		64016384 bytes total (59344187 bytes free)
		64016384 Bytes Total / 1000 = 64 MB
		59344187 Bytes Free  / 1000 = 60 MB

05. Salvando as configurações da memória RAM para a memória NVRAM.

**DICA-05:** nunca esqueça de salvar as configurações.
	
	sw-01# copy running-config startup-config
		Destination filename [startup-config]?

06. Salvando as configurações da memória NVRAM para a memória FLASH.
	
**DICA-06:** deixar sempre um backup das configuração na Memória FLASH.
	
	sw-01# copy startup-config flash: 
		Destination filename [startup-config]?
	
	sw-01# dir flash:
		5  -rw-        1799          <no date>  startup-config

07. Salvando as configurações da memória NVRAM para o Servidor TFTP.

**DICA-07:** o serviço de TFTP (Trivial File Transfer Protocol) utiliza o Protocolo: *UDP* na Porta Padrão: *69* e por padrão está ativo no Servidor no Cisco Packet Tracer, precisando apenas habilitar o endereço IPv4 ou IPv6.

**OBSERVAÇÃO-05:** o protocolo UDP (User Datagram Protocol) não é confiável, porque ele não exige confirmação de recebimento.

**OBSERVAÇÃO-06:** o protocolo TFTP foi escolhido pela Cisco para ser o sistema padrão de Atualização e Backup dos Switch e Router.

	!Pingando o Servidor de TFTP
	sw-01# ping 192.168.1.1
	
	!Verificando o Arquivo Startup-Config da NVRAM
	sw-01# dir nvram:
		238  -rw-        1690          <no date>  startup-config
	
	!Copiando o arquivo de configuração da NVRAM para o Servidor TFTP
	sw-01# copy startup-config tftp:
		Address or name of remote host []? 192.168.1.1
		Destination filename [sw-01-confg]? vaamonde-sw-01-config

	!Verificando o Backup no Servidor TFTP
	Server-01
		Services
			TFTP

08. Salvando a imagem do Cisco IOS do Switch Layer 2 2960 para o Servidor TFTP.

**DICA-08:** as imagens do Cisco IOS estão no formato: *BIN (binário)* e compactadas (m=RAM | z=zip)

**OBSERVAÇÃO-07:** não é aconselhável alterar o nome da imagem, ela segue um padrão de nomenclatura que é recomendado pela Cisco.

**EXEMPLO: 2960-lanbasek9-mz.150-2.SE4.bin (Primeira parte: 2960 plataforma/família do equipamento, Segunda parte: lanbasek9 indicação do package/funcionalidade do IOS, Terceira parte: compactação da Imagem m=RAM | z=zip, Quarta parte: 150-2.SE4 versão do IOS).**

**CUIDADO:** como o Cisco IOS é uma sub-derivação do *Unix/BSD* (Berkeley Software Distribution), ele também é Case Sensitive (faz diferença de Maiúscula/Minúscula).

	!Verificando o Binário do Cisco IOS do Switch
	sw-01# dir flash:
		1  -rw-     4414921          <no date>  2960-lanbasek9-mz.150-2.SE4.bin

	sw-01# copy flash: tftp:
		Source filename []? c2960-lanbasek9-mz.150-2.SE4.bin
		Address or name of remote host []? 192.168.1.1
		Destination filename [2960-lanbasek9-mz.150-2.SE4.bin]?

	!Verificando o Backup no Servidor TFTP
	Server-01
		Services
			TFTP

09. Salvando as configurações do Running Config (RAM) ou Startup Config (NVRAM) no VSCode.

**DICA-09:** esse é o método mais simples de backup das configurações do Switch ou Router

**OBSERVAÇÃO-08:** recomendo sempre utilizar um *Editor de Texto Profissional* para não modificar a estrutura do arquivo de configuração no momento de copiar e colar, não utilizar, por exemplo: MS Word, Wordpad, etc..., esses editores de Texto modificam as codificações dos arquivos prejudicando no processo de automação dos scripts.

**DICA-10:** copiar as informações do Running Config (RAM) ou Startup Config (NVRAM) a partir da primeira: *! (exclamação)* até a última linha com o comando: *end*

	!Visualizando as Configuração da RAM
	sw-01# show running-config

	!Utilize *BARRA DE ESPAÇO* para descer até a última linha do arquivo de configuração (MORE)
	!Selecione a partir da primeira ! (exclamação) do Running-Config
	!Não Selecione a linha: Current configuration : 1799 bytes
	
	!
	version 15.0
	...
	end

	!Copiar o conteúdo com o botão direito do mouse e selecionar: Copy
	!Salvar o Conteúdo no VSCode: Ctrl + V (ou botão direito colar).

	!Saindo do modo EXEC Privilegiado
	sw-01# disable
	
## TERCEIRA ETAPA: Backup das Configurações do Cisco IOS do Primeiro Router Cisco 1941.

01. Visualizando a versão do Cisco IOS e informações do Hardware do Router.

**DICA-11:** em roteadores esse comando fornece informações de licenciamento do hardware.

**OBSERVAÇÃO-09:** igual no Switch, esse comando fornece informações de inicialização do IOS do Router, utilizado principalmente para manutenção ou Quebra de Senha do equipamento.

**OBSERVAÇÃO-10:** em roteadores não temos o comando: *show boot*, essa opção só existe no Switch Cisco Catalyst Layer 2 ou 3.

	rt-01# show version
		249856K bytes of ATA System CompactFlash 0 (Read/Write)
		249856KB / 1000 = 250MB (250MB de Memória RAM Disponível)

02. Visualizando informações do Flash Card (Memória de Massa) do Router 1941.

**DICA-12:** em roteadores temos vários módulos de memória Flash Card, utilizado principalmente como Redundância caso algum Flash Card tenha problema.

**OBSERVAÇÃO-11:** o acesso a memória Flash em roteadores é feita utilizando módulos externos, geralmente não são soldados nos modelos antigos, modelos atuais está vindo chipado (soldado).

	rt-01# show flash:
		[33849219 bytes used, 221894781 available, 255744000 total]
		249856K bytes of processor board System flash (Read/Write)

	rt-01# dir flash0:
		255744000 bytes total (221894781 bytes free)
		255744000 Bytes Total = 256MB
		33847587 Bytes Used = 34MB
		221896413 Bytes Available = 222MB

03. Fazendo o Backup das Configurações e do Cisco IOS para o TFTP.

**DICA-13:** procedimento é igual do Switch Cisco Catalyst Layer 2 2960.

	!Salvando as configurações da memória RAM para memória NVRAM
	rt-01# copy running-config startup-config
		Destination filename [startup-config]? 

	!Salvando as configurações da memória NVRAM para a memória FLASH
	rt-01# copy startup-config flash: 
		Destination filename [startup-config]? 

	!Salvando as configurações da memória NVRAM para o Servidor TFTP
	
	!Pingando o Servidor de TFTP
	rt-01# ping 192.168.1.1
	
	!Verificando o Arquivo Startup-Config da NVRAM
	rt-01# dir nvram:
		238  -rw-        1690          <no date>  startup-config
	
	!Copiando o arquivo de configuração da NVRAM para o Servidor TFTP
	rt-01# copy startup-config tftp:
		Address or name of remote host []? 192.168.1.1
		Destination filename [rt-01-confg]? vaamonde-rt-01-config

	!Salvando a imagem do Cisco IOS do Router 1941 para o Servidor TFTP
	rt-01# copy flash: tftp:
		Source filename []? c1900-universalk9-mz.SPA.151-4.M4.bin
		Address or name of remote host []? 192.168.1.1
		Destination filename [c1900-universalk9-mz.SPA.151-4.M4.bin]? 

	!Saindo do modo EXEC Privilegiado
	disable

	!Verificando os Backups no Servidor TFTP
	Server-01
		Services
			TFTP