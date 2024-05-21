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

## PRIMEIRA ETAPA: Acessando o Modo de Configuração Global do Switch.

01. Acessando o modo EXEC Privilegiado e o modo de Configuração Global de Comandos.

		AVISO: acesso autorizado somente a funcionarios
		User Access Verification
		Username: senac
		Password: 123@senac

		!Alterando do Modo EXEC de Usuário para o Modo EXEC Privilegiado
		sw-01> enable
		Password: 123@senac
		sw-01#

## SEGUNDA ETAPA: Atualizando o Cisco IOS no Switch Catalyst Layer 2 2960.

**OBSERVAÇÃO IMPORTANTE:** NA NOVA CERTIFICAÇÃO DA CISCO CCNAv7 EXAME 200-301 NÃO É MAIS COBRADO CONHECIMENTOS EM LICENCIAMENTO DO CISCO IOS OU UPGRADES DE CISCO IOS NO SWITCH OU ROUTERS.

01. Atualizando o Cisco IOS (Firmware) do Switch Layer 2 2960.

**DICA-01:** as imagens do Cisco IOS estão no formato BIN (binário) e compactadas (m=RAM | z=zip).

**OBSERVAÇÃO-01:** só executar esse procedimento depois de fazer os Backups do IOS é das Configurações no Servidor TFTP para diminuir o risco de perda ou falha de inicialização.

**OBSERVAÇÃO-02:** não é aconselhável alterar o nome da imagem, ela segue um padrão de nomenclatura que a Cisco já utiliza a bastante tempo e o Switch ou Router sempre procura esse padrão para iniciar o Binário do IOS.

**CUIDADO-01:** como o Cisco IOS é uma sub-derivação do Unix/BSD, ele é Case Sensitive (faz diferença de Maiúscula/Minúscula).

**CUIDADO-02:** por padrão, caso não tenha espaço suficiente na Flash para a nova imagem, o Cisco IOS irá remover a imagem anterior para liberar espaço para a nova imagem (por causa desse comportamento padrão do Cisco IOS e indicado sempre fazer o Backup antes de atualizar).

	!Verificando o Nome da Imagem do IOS no TFTP
	Server-01
		Services
			TFTP

	!Atualizando a Imagem do Cisco IOS no Switch 2960
	sw-01# copy tftp: flash:
		192.168.1.1
		c2960-lanbasek9-mz.150-2.SE4.bin
	
	!Visualizando a nova Imagem do Cisco IOS na Flash do Switch 2960
	sw-01# show flash:

02. Atualizando as Configurações de Boot do Cisco IOS do Switch 2960 para a nova Imagem.

**OBSERVAÇÃO-03:** o nome da imagem tem que ser igual ao copiado para o Flash Card.

	!Acessando o Modo de Configuração Global
	sw-01# configure terminal
	sw-01(config)#

	!Alterando a Imagem de Boot do Cisco IOS do Switch 2960
	sw-01(config)# boot system c2960-lanbasek9-mz.150-2.SE4.bin

	!Saindo de todos os níveis e voltando para o modo EXEC Privilegiado
	sw-01(config)# end

	!Salvando as configurações da memória RAM para a memória NVRAM
	sw-01# copy running-config startup-config

	!Visualizando as informações da inicialização do Switch Layer 2 2960
	sw-01# show boot
	
03. Reinicializando o Switch Layer 2 2960 para testar a nova versão do Cisco IOS.

**DICA-02:** no Switch ou Router não existe o comando para desligar somente o comando de reiniciar, no Switch o processo de desligar e Remover o Cabo de Força e no Router e pressionar o Botão Power.

	!Reiniciando o Switch Cisco Catalyst Layer 2 2960
	sw-01# reload
		System configuration has been modified. Save? [yes/no]: yes
		Proceed with reload? [confirm]

	AVISO: acesso autorizado somente a funcionarios
	User Access Verification
	Username: senac
	Password: 123@senac

	!Alterando do Modo EXEC de Usuário para o Modo EXEC Privilegiado
	sw-01> enable
	Password: 123@senac
	sw-01#

	!Visualizando a Versão do Cisco IOS
	sw-01# show boot
		BOOT path-list      : c2960-lanbasek9-mz.150-2.SE4.bin
		Config file         : flash:/config.text
		Private Config file : flash:/private-config.te