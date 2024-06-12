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

## SEGUNDA ETAPA: Configuração do Serviço de Acesso Remoto SSH (Secure Shell) no Cisco IOS

01. Configuração do Nome de Domínio FQDN (Fully Qualified Domain Name).

**DICA-01:** o nome de Domínio FQDN (Fully Qualified Domain Name) é utilizado pelo Serviço do SSH (Secure Shell) e outros serviços de rede como o Servidor de Autenticação Remota e Monitoramento de Switch ou Router utilizando os protocolos RADIUS (Remote Authentication Dial In User Service, TACACS (Terminal Access Controller Access-Control System) ou DNS (Domain Name Service).

**ADENDO-01** um nome de domínio, muitas vezes chamado apenas de domínio, é um nome fácil de lembrar, associado sempre a um endereço IPv4 ou IPv6 físico na Internet ou na Rede Local separado sempre por um: *. (ponto)*.

	sw-01(config)# ip domain-name senac.br

02. Criação/Geração da chave de criptografia do Serviço do SSH (Secure Socket Shell) Server local.

**DICA-02:** por padrão o serviço do SSH Server está desabilitado no Switch ou Router;

**DICA-03:** por padrão todas as conexões remotas utilizando o protocolo SSH são criptografadas (segura);

**OBSERVAÇÃO-01:** é recomendado utilizar módulos de criptografia de no mínimo: *1024 bits* (opções de 360 até 2048);

**OBSERVAÇÃO-02:** no Switch ou Router *Real* utilizamos o comando: *crypto key generate rsa general-keys modulus 1024* para fazer a geração da chave e inicialização do Serviço;

**OBSERVAÇÃO-03:** existe vários algorítimos de geração das chaves públicas criptografadas no SSH, o padrão é utilizar o RSA (Rivest-Shamir-Adleman);

**OBSERVAÇÃO-04:** a porta padrão de conexão do Serviço de SSH é a: *22* utilizando o Protocolo: *TCP*;

**ADENDO-01:** versões do Cisco Packet Tracer >=7.3 possui o suporte para o comando completo de geração das chaves SSH RSA nos Switches ou Router em um único comando igual as equipamentos reais, utilizando o comando: *crypto key generate rsa general-keys modulus 1024*;

**OBSERVAÇÃO IMPORTANTE:** caso queira desativar o serviço do SSH ou remover os Módulos/Chaves Públicas RSA, digite o comando: *crypto key zeroize rsa*, caso você digite novamente o comando: *crypto key generate rsa* ele vai solicitar se você quer substituir os Módulos/Chaves Públicas RSA atuais (Do you really want to replace them? [yes/no]).

	sw-01(config)# crypto key generate rsa general-keys modulus 1024

03. Habilitando a versão 2 do Serviço de SSH Server.

**DICA-04:** a versão: *2* do serviço do SSH Server corrigiu várias falhas de segurança existe na versão: *1.99*, recomendo sempre habilitar essa versão.

**OBSERVAÇÃO-05:** após a criação da chave RSA do SSH o serviço habilita por padrão a versão 1.99.

	sw-01(config)# ip ssh version 2

04. Habilitando o tempo de inatividade para novas conexões do SSH Server.

**DICA-05:** configuração de inatividade é feita somente em segundos (1 até 120 segundos = 2 minutos).

**OBSERVAÇÃO-06:** essa configuração está relacionada ao tempo para se autenticar no serviço do SSH no Switch ou Router, diferente do tempo de inatividades de acesso remoto que é controlado pelas Lines VTY ou Console.

	sw-01(config)# ip ssh time-out 60

05. Habilitando o número máximo de tentativas de conexões simultâneas no SSH Server.

**DICA-06:** essa opção aumenta o nível de segurança contra ataques de Força Bruta (Brute-Force) utilizando dicionários de usuários e senhas e várias autenticações simultâneas com falhas (Exemplo o software Hydra).

**OBSERVAÇÃO-07:** limites de conexões simultâneas vai de: 0 até 5, por padrão várias conexão simultâneas são liberadas.

	sw-01(config)# ip ssh authentication-retries 2

06. Saindo de todos os níveis e voltando para o modo EXEC Privilegiado.

**DICA-07:** você pode usar o comando: *do write* ou o comando: *copy running-config startup-config* para salvar as configurações sem sair do Modo Exec Privilegiado.

	sw-01(config)# end

07. Salvando as configurações da memória RAM (Running-Config) para a memória NVRAM (Startup-Config).

**DICA-08:** nunca esqueça de salvar as configurações.

	sw-01# copy running-config startup-config

08. Visualizando as configurações da memória RAM (Running-Config).

**DICA-09** após a configuração do Serviço do SSH verifique se tudo está configurado de forma correta utilizando os comandos: *show*.
	
	!Visualizando as Configurações do Running-Config (RAM)
	!OBSERVAÇÃO: ÚNICA LINHA QUE NÃO APARECE NAS CONFIGURAÇÃO É A: crypto key generate rsa
	sw-01# show running-config

	!Fazendo um Filtro na Visualização do Running-Config somente da Sessão Line VTY
	sw-01# show running-config | section include line vty

	!Fazendo um Filtro na Visualização do Running-Config somente do SSH
	!OBSERVAÇÃO: ÚNICA LINHA QUE NÃO APARECE NAS CONFIGURAÇÃO É A: crypto key generate rsa
	sw-01# show running-config | section include ssh

	!Visualizando as configurações do SSH Server e Versão
	sw-01# show ip ssh

	!Visualizando das chaves públicas RSA do SSH Server
	sw-01# show crypto key mypubkey rsa

	!Visualizando as conexões ativas do SSH Server.
	!OBSERVAÇÃO: ESSA OPÇÃO SÓ VAI FUNCIONAR QUANDO VOCÊ SE CONECTAR REMOTAMENTE NO SWITCH OU ROUTER.
	sw-01# show ssh

	!Visualizando os Usuários Conectados no Switch
	!OBSERVAÇÃO: ESSA OPÇÃO VAI MOSTRAR O USUÁRIO LOGADO NO CONSOLE: con 0 OU NO VTY: vty 0
	sw-01# show users

## TERCEIRA ETAPA: Testando e Acessando Remotamente do Switch Cisco Catalyst 2960.

01. Testando as Conexão do Desktop no Switch e Acessando Remoto via SSH.

a) Abrindo o Prompt de Comando do Desktop;

**DICA-10** não confunda Terminal com Command Prompt, Terminal é utilizado para se conectar no Switch ou Router utilizando o Cabo Console, já o Command Prompt (Prompt de Comando) é utilizado para testar as configurações de rede e acessar remotamente o Switch ou Router.

	!Verificando o endereço IPv4 configurado no Desktop
	C:\> ipconfig

	!Verificando o endereço detalhado IPv4 configurado no Desktop
	C:\> ipconfig /all

	!Testando a comunicação com o Switch utilizando o pacote ICMP (Internet Control Message Protocol)
	C:\> ping 192.168.1.250   (Switch SW-01)
	C:\> ping 192.168.1.251   (Switch SW-02)

	!Testando o acesso remoto no Switch utilizando o protocolo Telnet (Teletype Network)
	C:\> telnet 192.168.1.250   (Switch SW-01)
	C:\> telnet 192.168.1.251   (Switch SW-02)

	!Acessando remotamente o Switch utilizando o protocolo SSH (Secure Shell)
	!OBSERVAÇÃO: -l (éli não é o número "1" (um) e sim "l" (éli) em minúsculo)
	C:\> ssh -l senac 192.168.1.250   (Switch SW-01)
	C:\> ssh -l senac 192.168.1.251   (Switch SW-02)

## QUARTA ETAPA: Automatizando a Configuração do Segundo Switch Cisco Catalyst 2960.

01. Utilizando o Visual Studio Code (VSCode) para automatizar as configurações do Cisco IOS.

**OBSERVAÇÃO-08:** recomendamos sempre utilizar um *Editor de Texto Profissional* para criar os scripts e automatizar as tarefas de configuração do Cisco IOS, hoje em dia é indicado utilizar o Visual Studio Code (VSCode) junto com as Extensões: *Cisco IOS Syntax e Cisco Config Highlight* para facilitar essa configuração.

**DICA-11:** o caractere: *! (exclamação)* é utilizado como um recurso de *Comentário*, sua utilização server para comentar o código de automação do Cisco IOS ou para desativar um comando para não ser executado, *RECOMENDO FORTEMENTE DOCUMENTAR TODOS OS COMANDOS E PROCEDIMENTOS DE CONFIGURAÇÃO PARA FACILITAR O ENTENDIMENTO.*

**DICA-12:** para facilitar a leitura do código, recomendo utilizar o recurso de **Indentação de Código** usando a Tecla TAB (Tabulador/Tabulação) para cada nível que você está configurando o Cisco IOS, isso facilitada a análise de erros (Debug) do código.

```python
!Acessando o modo EXEC Privilegiado
enable

	!Acessando o modo de Configuração Global de comandos
	configure terminal
	
		!Configuração do nome de domínio FQDN (Nome de Domínio Totalmente Qualificado)
		ip domain-name senac.br

		!Criação da chave de criptografia e habilitar o serviço de SSH Server local
		crypto key generate rsa general-keys modulus 1024

		!Habilitando a versão 2 do serviço de SSH Server
		ip ssh version 2

		!Habilitando o tempo de inatividade para novas conexões do SSH Server
		ip ssh time-out 60

		!Habilitando o número máximo de tentativas de conexões simultâneas no SSH Server
		ip ssh authentication-retries 2

		!Saindo de todos os níveis e voltando para o modo EXEC Privilegiado
		end

!Salvando as configurações da memória RAM para a memória NVRAM
write
```