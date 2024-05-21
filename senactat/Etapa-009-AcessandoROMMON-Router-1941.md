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

## PRIMEIRA ETAPA: Parando a Inicialização do Cisco IOS do Router 1941

01. Parando a inicialização do Cisco IOS do Router 1941 para acessar o ROMMon.

**DICA-01:** no Cisco Packet Tracer utilizamos a combinação de teclas: Ctrl + C para abortar a inicialização do Cisco IOS;

**OBSERVAÇÃO-01:** em equipamento reais, podemos utilizar as combinações de teclas: Ctrl + C, Ctrl + Break ou Ctrl + Backspace para abortar a inicialização do Cisco IOS dependendo do sistema de acesso Remoto que você está utilizando;

**OBSERVAÇÃO-02:** no aplicativo PuTTY você deve usar o Botão direito do Mouse na Barra de Título e escolher as opções: Send Command: depois: Break (somente quando começar a descompactação do Cisco IOS para a memória RAM #####).

A) Desligar o Router 1941 no Botão Power e aguardar 10 segundos;<br>
B) Ligar o Bota Power do Router 1941 (no Cisco Packet Tracer esse processo e muito rápido);<br>
C) Na tela de IOS Image Load Test, quando começar a descompactação da imagem em: Self decompressing the image, pressionar: Ctrl + C para acessar o ROMMon.

	IOS Image Load Test
	___________________
	Digitally Signed Release Software
	program load complete, entry point: 0x81000000, size: 0x2bb1c58
	Self decompressing the image :
	#########
	monitor: command "boot" aborted due to user interrupt
	rommon 1 > 

## SEGUNDA ETAPA: Alterando a Modo de Inicialização do Cisco IOS do Router 1941

01. Visualizando as opções de comandos do Modo ROMMON (ROM (read-only memory) monitor)

**DICA-02:** diferente do Cisco IOS o Modo ROMMon é bem limitado em configurações, o recurso de Auto-Complemento não funciona nesse modo, sendo necessário digitar os comandos manualmente, existe a opção: *? (Interrogação)* para ver a lista de comandos disponíveis no ROMMon.

	rommon 1 >?

02. Alterando o modo de inicialização do Cisco IOS do Router 1941.

**DICA-03:** o comando: *confreg* altera a forma como a inicialização do Cisco IOS ler os arquivos de configuração no momento da inicialização;

**DICA-04:** no modo ROMMON a opção do TAB não funciona, precisando digitar o comando completo, as opções abreviadas também não funcionar nesse modo.

**OBSERVAÇÃO-03:** essa opção força o Router a não ler as configurações do: *startup-config* no momento da inicialização do Cisco IOS.

**OBSERVAÇÃO-04:** chave de registro em hexadecimal: *0x2142* (não ler as configurações do startup-config);

**OBSERVAÇÃO-05:** chave de registro em hexadecimal: *0x2102* (ler as configurações do startup-config - padrão);

**CUIDADO-01:** existe várias chaves de registro no Cisco IOS, se você errar a chave pode acontecer do Cisco IOS inicializar de forma incorreta ou com caracteres irreconhecível na Linha Console ou na Linha Virtual, CUIDADO!!!!! nessa configuração.

	!Alterando a chave de registro para 0x2142
	rommon 2 > confreg 0x2142

	!Reinicializando o Router 1941 no Modo ROMMON
	rommon 3 > reset

	!Aguardar a inicialização do Cisco IOS
	Press RETURN to get started!

	AVISO: acesso autorizado somente a funcionarios
	User Access Verification
	Username:

## TERCEIRA ETAPA: Limpando as Configurações Residuais do Router 1941

01. Acessando o modo EXEC Privilegiado e o modo de Configuração Global de Comandos.

**DICA-05** para voltar as configurações do modo de inicialização do Cisco IOS e necessário fazer a limpeza das configurações do: startup-config e depois alterar a chave de registro e salvar as configurações novas.

	AVISO: acesso autorizado somente a funcionarios
	User Access Verification
	Username: senac
	Password: 123@senac

	!Alterando do Modo EXEC de Usuário para o Modo EXEC Privilegiado
	rt-01> enable
	Password: 123@senac
	rt-01#

	!Visualizando as configurações de inicialização do Router 1941
	rt-01# show version
	
	!Visualizando as configurações do startup-config
	rt-01# show startup-config
	
	!Limpando as configurações do startup-config
	rt-01# erase startup-config
	rt-01# show startup-config
	
	!Acessando o modo de Configuração Global de comandos
	rt-01# configure terminal
	
		!Alterando o modo de inicialização do Cisco IOS do Router 1941
		rt-01(config)# config-register 0x2102
		
		!Saindo de todos os níveis e voltando para o modo EXEC Privilegiado
		rt-01(config)# end
	
	!Salvando as configurações da memória RAM para a memória NVRAM
	rt-01# write
		
	!Reinicializando o Router 1941
	rt-01# reload
		System configuration has been modified. Save? [yes/no]:yes
		Proceed with reload? [confirm]

02. Visualizando as Mudanças da Chave de Registro do Cisco IOS e Restaurando o Backup da Flash

**DICA-06** após o reset do Router 1941 todas as configurações iniciais são perdidas, mesmo restaurando o Backup alguns ajustes são necessários para o Router voltar a funcionar.

	AVISO: acesso autorizado somente a funcionarios
	User Access Verification
	Username: senac
	Password: 123@senac

	!Alterando do Modo EXEC de Usuário para o Modo EXEC Privilegiado
	rt-01> enable
	Password: 123@senac
	rt-01#

	!Visualizando as configurações de inicialização do Router 1941
	rt-01# show version
	
	!Visualizando os arquivos no Flash Card
	rt-01# show flash:
	
	!Copiando o arquivo do Flash Card startup-config para NVRAM
	rt-01# copy flash: startup-config 
		Source filename []? startup-config
		Destination filename [startup-config]? 

	!Visualizando as configurações do startup-config
	rt-01# show startup-config

03. Aplicando as configurações da NVRAM (startup-config) para a RAM (running-config)

**OBSERVAÇÃO-06:** após a cópia da configuração da NVRAM para RAM, as Interfaces não serão inicializadas automaticamente sendo necessário iniciar cada Interface no seu modo de configuração utilizando o comando: *no shutdown*, no arquivo: *running-config* ou *startup-config* por padrão não tem o comando: *no shutdown* nas configurações das Interfaces;

**OBSERVAÇÃO-07:** o serviço do SSH Server depois que o Router ou Switch é resetado ele também não volta a funcionar, no arquivo: **running-config* ou *startup-config* por padrão não tem o comando: *crypto key*, para resolver essa falha, recomendo digitar os comandos: *crypto key zeroize rsa* (zerar todas as chaves primeiro) e depois o comando: *crypto key generate rsa general-keys modulus 1024* (gerar as chaves novamente).

	!Salvando as Configurações do NVRAM para a RAM
	rt-01# copy startup-config running-config
		Destination filename [running-config]? 

	!Acessando o Modo de Configuração Global
	rt-01# configure terminal
	rt-01(config)#

	!Limpando as Chaves RSA do SSH
	rt-01(config)# crypto key zeroize rsa
		Do you really want to remove these keys? [yes/no]: yes
	
	!Gerando novamente as Chaves RSA do SSH
	rt-01(config)# crypto key generate rsa general-keys modulus 1024

	!Inicializando a Interface GigabitEthernet 0/0
	rt-01(config)# interface gigabitEthernet 0/0
	rt-01(config-if)# no shutdown

	!Saindo de todos os níveis do Cisco IOS
	rt-01(config-if)# end

	!Salvando as configurações da memória RAM para a memória NVRAM
	rt-01# write
	
	!Reinicializando o Router 1941
	rt-01# reload
		System configuration has been modified. Save? [yes/no]:yes
		Proceed with reload? [confirm]