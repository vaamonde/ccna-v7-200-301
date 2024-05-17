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

## PRIMEIRA ETAPA: Acessando o Modo EXEC de Comandos de Usuário

Primeiro acesso ao modo EXEC de Comandos de usuário (> sinal de Maior - user EXEC commands mode). Use o modo EXEC para definir, visualizar e testar as operações do sistema. 

Em geral, os comandos EXEC de usuário permitem que você se conecte a dispositivos remotos, altere as configurações da linha do terminal temporariamente, utilizado para executar os testes básicos e listar as informações do Cisco IOS (Internetwork Operating System).

O modo EXEC é dividido em dois níveis de acesso: **Usuário (>) e Privilegiado (#).**

**OBSERVAÇÃO-01:** sempre que você acessar o modo EXEC pela primeira vez no Switch ou Router será mostrado o nome (hostname) padrão dos equipamentos: **Switch = Switch> e Router = Router>**

	Switch>

## SEGUNDA ETAPA: Acessando o Modo EXEC Privilegiado

01. Acessando o modo EXEC Privilegiado (# sinal de Sustenido/Hashtag - privileged EXEC mode)

**DICA-01:** utilizar sempre a tecla TAB para auto-completar os comandos no Cisco IOS;
**DICA-02:** se você estiver com dúvida do comando, utilizar o sinal de: ? (Interrogação) junto com o comando para mostrar as opções e informações reduzidas do comando.

**EXEMPLO: show? | enable? | copy? | disable? | clock? | service?**

**DICA-03** se você está estudando para a Certificação Cisco CCNAv7, é recomendado digitar os comandos completos, não abreviados, utilize comandos abreviados quando você já domina o Cisco IOS.

**EXEMPLO: enable = en | show running-config = sh runn | interface FastEthernet0/0 = int fa0/0**

Para sair do modo EXEC Privilegiado você pode digitar o comando: *disable* ou *exit*

	Switch> enable
	Switch#

	Switch# disable
	Switch>

## TERCEIRA ETAPA: Configuração da Data e Hora

01. Configuração de Data/Hora em Inglês, você pode usar o Mês abreviado ou completo na configuração

**EXEMPLO: March ou Mar | April ou Apr | November ou Nov | December ou Dec**

**EXEMPLO: Hora no formato Universal: Hora:Minutos:Segundos 00:00:00 - Data no formato: Dia Mês Completo ou Abreviado e Ano Completo: 01 March 2024**

**DICA-04:** é recomendado utilizar o Protocolo NTP (Network Time Protocol) para manter sincronizado a Data e Hora no Switch ou Router

	Switch# clock set 14:00:00 17 May 2024

## QUARTA ETAPA: Acessando o Modo de Configuração Global

01. Acessando o modo de Configuração Global de comandos do Cisco IOS
	
**DICA-05:** nesse modo que é feita a maioria das configurações do Cisco IOS tanto no Switch como no Router

	Switch# configure terminal
	Switch(config)#

## QUINTA ETAPA: Configurações Básicas (Base) do Switch

01. Configuração do nome do Switch (principal configuração principal)

**OBSERVAÇÃO-02:** essa configuração é obrigatória para o serviço de acesso remoto SSH e demais serviços de rede que utiliza nomes para o seu acesso.

**DICA-06:** utilizar nomes curtos e objetivos, não usar caracteres especiais, espaço, acentuação, nomes complexo, etc...
	
	Switch(config)# hostname sw-01
	sw-01(config)#

02. Habilitando o serviço de criptografia de senha do Tipo-7 Password do Cisco IOS.

**DICA-07:** senhas do Tipo-7 por padrão não são criptografadas no Cisco IOS (serviço está desabilitado por padrão no Cisco IOS sendo necessário habilitar para criptografar as senhas, caso você não habilite o serviços as senhas são mostradas em Texto Plano no comando: show ruuning-config).

**OBSERVAÇÃO-03:** senhas do Tipo-7 são fáceis de serem quebradas e não são mais usadas nos equipamentos da Cisco, nesse caso é recomendado utilizar senhas do Tipo-5 Secret.

**DESAFIO-01:** site para quebrar senhas do Tipo-7 https://packetlife.net/toolbox/type7/

	sw-01(config)# service password-encryption

03. Habilitando o serviço de marcação de Data/Hora detalhado nos Logs do Cisco IOS

**DICA-08:** esse recurso é utilizado nos sistemas de monitoramento, desempenho e consumo de rede, principalmente nos sistemas de auditoria de acesso ou recursos/serviços de rede e protocolos de geração de logs nos equipamentos da Cisco

	sw-01(config)# service timestamps log datetime msec

04. Desativando o serviço de resolução de nomes de domínio (serviço habilitado por padrão) no Cisco IOS

**DICA-09:** se você desabilitar esse recurso o problema de travamento de comandos digitados fora do seu modo padrão no Cisco IOS é resolvido, mais você perde a resolução de nomes no Cisco IOS, em Switch e Router esse recursos e pouco utilizado, somente quando e feito a integração com o Serviços de DNS.

**EXEMPLO: switch# time (Translating "time"...domain server (255.255.255.255))**

**DICA-10:** para desbloquear o terminal, você pressiona: Ctrl+Shift+6 ou espera a liberação do terminal que demora cerca de 60 segundos.

**DICA-11:** o comando: *no* é usado para desabilitar ou remover configurações feitas no switch ou router da Cisco

	sw-01(config)# no ip domain-lookup

05. Configuração do banner da mensagem do dia no Cisco IOS

**DICA-11:** existe vários tipos de Banners no Cisco IOS, o MOTD (Mensagem do Dia) é o mais utilizado

**EXEMPLO: banner motd (Mensagem do Dia), banner login (Mensagem de Login), banner exec (Mensagem de Modo EXEC), banner incoming (Mensagem de Entrada)**

**DICA-12:** é recomendado não utilizar acentuação, textos longos ou complexos no Banner MOTD e demais Banners pois o terminal do Cisco ISO não reconhece esses caracteres.

**DESAFIO-02:** pesquisar na Internet imagens ASCII Art Cisco para colocar no Banner MOTD

**OBSERVAÇÃO-04:** imagens ASCII Art no Banner *não pode ser muito grande*, recomendado ser **<= 1024 pixels**

**CUIDADO:** utilizar o mesmo *sinal de delimitador de Início e Fim* do Banner na imagem ASCII (# Sustenido/Hashtag) ou outro carácter que não apareça na imagem.

	sw-01(config)# banner motd #AVISO: acesso autorizado somente a funcionarios#

06. Habilitando o uso de senha do Tipo-5 Secret para acessar o modo EXEC Privilegiado do Cisco IOS

**DICA-13:** senhas do Tipo-5 por padrão utilizam criptografia forte (Algorítimo MD5) e não precisa do serviços de criptografia de senha habilitado para funcionar.

**OBSERVAÇÃO-05:** por padrão o acesso ao modo EXEC Privilegiado é liberado sem segurança

	sw-01(config)# enable secret 123@senac

07. Criação dos usuários locais utilizando senhas do Tipo-5 ou Tipo-7 e privilégios diferenciados

**DICA-14:** existe 16 níveis de privilégios no Cisco IOS (0 mais baixo até 15 mais alto);
**DICA-15:** não é recomendado criar usuários utilizando senhas do Tipo-7 (senhas fracas, fácil de quebrar);
**DICA-16:** existe a possibilidade de se autenticar no Switch utilizando os protocolos RADIUS ou TACACS;
**DICA-17:** usuários com Privilégio 15 não precisa digitar o comando enable após se logar no Switch ou Router.

**OBSERVAÇÃO-06:** criação de usuários comuns para administrar o Switch, privilégio padrão recomendado: 1

	sw-01(config)# username senac secret 123@senac
	sw-01(config)# username vaamonde password 123@senac
	sw-01(config)# username admin privilege 15 secret 123@senac

## SEXTA ETAPA: Configuração da Linha Console

01. Acessando a Linha (line) Console, porta padrão de acesso Out-of-Band (Fora da Banda) do Switch Cisco
	
**DICA-18:** conexão feita utilizando o Cabo Console RS232/DB9 ou USB e software de Acesso Remoto ao Console (PuTTY, Minicom, etc...).
**DICA-19:** nos Switch Cisco Catalyst temos apenas uma porta console RS232/DB9 ou USB (novos modelos).

	sw-01(config)# line console 0
	
a) Forçando fazer login local utilizando os usuários e senhas locais criados no Switch

**DICA-20:** por padrão a configuração da Linha Console é permitir o acesso físico sem autenticação
	
	sw-01(config-line)# login local

b) Habilitando a senha de acesso do Tipo-7 Password (senha fraca)

**DICA-21:** na porta console não temos a opção de criar senhas do Tipo-5 (forte) somente Tipo-7 (fraca)

**OBSERVAÇÃO-07:** a porta console é considerada uma porta/interface física não remota ou virtual, por esse motivo ela não tem suporte a senhas do Tipo-5 Secret, pois o acesso é feito fisicamente no Switch ou Router (se você tem a possibilidade de acessar fisicamente um equipamento, o nível de segurança da criptografia não importa mais, pois é uma invasão física e não lógica).

**OBSERVAÇÃO-08:** essa configuração só será utilizada caso não exista usuários locais criados e se a opção do comando: login local não for configurada.
	
	sw-01(config-line)# password 123@senac

c) Habilitando o sincronismo das mensagens de Logs na tela da linha de console do Cisco IOS

**DICA-22:** esse recurso ajuda bastante no dia-a-dia em administrar o Cisco IOS, por padrão todas as mensagens de Log tem sua saída padrão na tela, que muitas vezes atrapalha na digitação, esse recurso permite o sincronismos entre as mensagens e a digitação dos comandos.

**OBSERVAÇÃO-09:** por padrão todas as mensagens de status ou logs do Switch são mostradas na tela
	
	sw-01(config-line)# logging synchronous

d) Habilitando o tempo de inatividade de uso da linha de console do Cisco IOS

**DICA-22:** configuração do tempo de inatividade em minutos e segundos da linha console, utilizado principalmente quando você está conectado no console e não está interagindo nas configurações, após o tempo de inatividade a seção (logoff) será finalizada, garantindo assim a segurança do acesso aos equipamentos.

**OBSERVAÇÃO-10:** não é recomendado deixar o tempo de inatividade muito curto e nem muito longo
	
	sw-01(config-line)# exec-timeout 5 30

e) Saindo de todos os níveis e voltando para o modo EXEC Privilegiado

**DICA-23:** você pode utilizar a tecla de atalho: *Ctrl+Z* para sair de todos os níveis;
**DICA-24:** o comando: *exit* sai nível por nível, o comando: *end* sai de todos os níveis.

**OBSERVAÇÃO-11:** os dois comandos são utilizados principalmente em scripts de automação
	
	sw-01(config-line)# end

## SÉTIMA ETAPA: Salvando as Configuração Básica (Base) do Switch

01. Salvando as configurações da memória RAM (Running-Config) para a memória NVRAM (Startup-Config)

**DICA-25:** no Cisco IOS temos vários tipos de memórias: RAM (Random Access Memory), NVRAM (Non-Volatile Random Access Memory), Flash EEPROM (Electrically-Erasable Programmable Read-Only Memory), etc.
**DICA-26:** você pode utilizar o comando: *write*, indicado para criação de scripts e considerado obsoleto pela Cisco para salvar as configurações da RAM para a NVRAM.
	
	sw-01# copy running-config startup-config

## OITAVA ETAPA: Visualizando as Configurações do Switch

01. Visualizando as configurações da memória RAM (Running-Config)

**DICA-26:** no Cisco IOS temos várias opções de visualização das configurações utilizando o comando: *show*, o principal comando utilizado em todos os equipamentos da cisco para verificar as configurações que estão rodando no momento é o: *show ruunning-config* (configuração que está rodando na RAM).
	
	sw-01# show running-config

## OITAVA ETAPA: Automatizando a Configuração do Segundo Switch

01. Utilizando o Visual Studio Code (VSCode) para automatizar as configurações do Cisco IOS

**OBSERVAÇÃO-12:** recomendamos sempre utilizar um Editor de Texto Profissional para criar os scripts e automatizar as tarefas de configuração do Cisco IOS, hoje em dia é indicado utilizar o Visual Studio Code (VSCode) junto com as Extensões: *Cisco IOS Syntax e Cisco Config Highlight* para facilitar essa configuração.

**DICA-27:** o caractere ! (exclamação) é utilizado como um recurso de *Comentário*, sua utilização server para comentar o código de automação do Cisco IOS ou para desativar um comando para não ser executado, *RECOMENDO FORTEMENTE DOCUMENTAR TODOS OS COMANDOS E PROCEDIMENTOS DE CONFIGURAÇÃO PARA FACILITAR O ENTENDIMENTO.*

**DICA-28:** para facilitar a leitura do código, recomendo utilizar o recurso de Indentação de Código usando a Tecla TAB (Tabulador/Tabulação) para cada nível que você está configurando o Cisco IOS, isso facilitada a análise de erros (Debug) do código.

```python
!Automação da configuração do Switch 2
enable

!Configuração de Data/Hora em inglês, você pode usar abreviado ou completo
clock set 14:00:00 17 May 2024

	!Acessando o modo de configuração global de comandos
	configure terminal
  
	!Configuração do nome do switch
	hostname sw-02

	!Habilitando o serviço de criptografia de senhas do Tipo-7 Password 
	service password-encryption
	
	!Habilitando o serviço de marcação de Data/Hora detalhado nos Logs
	service timestamps log datetime msec
  
	!Desativando a resolução de nomes de domínio
	no ip domain-lookup
  
	!Configuração do banner da mensagem do dia
	banner motd #AVISO: acesso autorizado somente a funcionarios#
  
	!Habilitando o uso senha do Tipo-5 Secret para acessar o modo EXEC Privilegiado
	enable secret 123@senac
  
	!Criação dos usuários locais utilizando senhas do Tipo-5 ou Tipo-7 e privilégios diferenciados
	username senac secret 123@senac
	username vaamonde password 123@senac
	username admin privilege 15 secret 123@senac
	
	!Acessando a linha console, porta padrão de acesso Out-of-Band (Fora da Banda)
	line console 0
		
		!Forçando fazer login local utilizando usuário e senha locais do switch
		login local
		
		!Habilitando senha de acesso do Tipo-7 Password
		password 123@senac
		
		!Sincronizando as mensagens de logs na tela
		logging synchronous
		
		!Habilitando o tempo de inatividade de uso do console
		exec-timeout 5 30
		
		!Saindo de todos os níveis e voltando para o modo EXEC Privilegiado
		end

!Salvando as configurações da memória RAM para a memória NVRAM
write
```