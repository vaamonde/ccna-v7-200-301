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

## PRIMEIRA ETAPA: Reset do Switch 2960 ou 3560 (Configurações de Fábrica)

**OBSERVAÇÃO IMPORTANTE: Utilizar o PuTTY para acessar o Switch utilizando o Cabo Console.**

01. Deixar o Switch 3560 inicializar normalmente (esse processo demora cerca de 5 minutos)

02. Após a inicialização do Switch 3560, pressionar o Botão **Mode** por aproximadamente **15/20 segundos** até entrar os LED's piscarem e o Switch entrar no modo de ROMmon e ser reinicializado.

03. Após a reinicialização do Switch 3560 será apresentado o Wizard de Configuração, digite: no <Enter>

04. Limpando as configurações residuais dos outros grupos do Switch 3560.

	a) Acessar o modo privilegiado: enable <Enter>
	b) Remover o banco de dados de VLAN: delete flash:vlan.dat <Enter>
	c) Remover os backups anteriores: delete flash:startup-config <Enter>

## OBSERVAÇÃO IMPORTANTE: Caso o Switch não volte para o estado de fábrica, será necessário utilizar os procedimentos abaixo: (SÓ USAR ESSA OPÇÃO SE FOR REALMENTE NECESSÁRIO, NÃO EXECUTAR ESSES PROCEDIMENTOS NOS EQUIPAMENTOS ANTES DE INFORMAR AO DOCENTE)

	a) Pressionar o botão MODE até o switch reinicializar;
	b) Na tela de inicialização, na mensagem de hardware, pressionar o botão MODE para abortar o carregamento do IOS;
	c) Digitar o comando: flash_init;
	d) Listar o conteúdo da Flash: dir flash:
	e) Renomear o arquivo: rename flash:config.text flash:config.old
	f) Inicializar o sistema: boot
	g) Limpar o Startup-config: erase startup-config
	h) Limpar as VLAN: delete flash:vlan.dat
	i) Reinicializar o Switch: reload

## SEGUNDA ETAPA: Reset do Roteador (Router) 2911

**OBSERVAÇÃO IMPORTANTE: Utilizar o PuTTY para acessar o Switch utilizando o Cabo Console.**

01. Parar a inicialização do IOS do Router 2911 utilizando as teclas de atalho: Ctrl + Break (No PuTTY utilizar o Botão direito do Mouse na Barra de Título e selecionar as opções: Send Command: Break)

**CUIDADO!!!!!! com a Chave de Registro que você vai digitar no ROMmon (veja o tópico das Obs: 1 e 2)**

02. Nas configurações do Cisco ROMmon digite a chave em hexadecimal: confreg 0x2142 <Enter>

03. Após a mudança da chave, digite: reset <Enter> para reiniciar o Router 2911.

04. O Router 2911 vai inicializar sem ler o arquivo de configuração: startup-config da NVRAM.

05. Limpando as configurações do Router 2911 e voltando a ler o arquivo de configuração startup-config da NVRAM.

	a) Acessar o modo Exec Privilegiado: enable <Enter>
	b) Limpar a NVRAM: erase startup-config <Enter>
	c) Limpar as configurações de backup anteriores: delete flash:startup-config <Enter>
	d) Acessar o modo de configuração global: configure terminal <Enter>
	e) Mudar o registro de inicialização: config-register 0x2102 <Enter>
	f) Sair de todos os modos: end <Enter>
	g) Salvar as configurações: copy running-config startup-config <Enter>
	h) Reinicializar o router: reload <Enter>
	i) Verificar a chave de registro: enable <Enter>, show version <Enter>

**Obs1: caso você digite chaves diferentes no ROMmon o sistema pode inicializar com caracteres estranhos, isso está muitas vezes associado a velocidade da porta (Padrão 9600), será necessário fazer os testes mudando as velocidades de conexão da porta no PuTTY para: 1200,2400, 4800, 9600, 19200, 38400, 57600 e 115200.** 

**Obs2: para corrigir essa falha será necessário alterar novamente a chave de registro para:**

	a) Acessar o modo Exec Privilegiado: enable <Enter>
	b) Mudar o registro de inicialização: config-register 0x2102 <Enter>
	c) Acessar a Linha Console: line console 0 <Enter>, 
	d) Alterar a velocidade da Porta Console: speed 9600 <Enter>
	e) Salvar as configurações: copy running-config startup-config <Enter>
	f) Reinicializar o router: reload <Enter>
	g) Verificar a chave de registro: enable <Enter>, show version <Enter>