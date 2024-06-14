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

## PRIMEIRA ETAPA: Configuração Base Switch Cisco Catalyst Layer 2 2960 (LADO ESQUERDO - ACESSO)
```python
!Acessando o modo Exec Privilegiado
enable

!Configuração de Data/Hora em inglês, você pode usar abreviado ou completo
clock set 14:00:00 14 June 2024

	!Acessando o modo de configuração global de comandos
	configure terminal

		!Configuração do nome do switch
		hostname sw-03

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
			exit

		!Acessando as linhas virtuais de acesso remoto do Switch
		line vty 0 4

			!Forçando fazer login local utilizando usuário e senha locais do switch
			login local

			!Habilitando senha de acesso do Tipo-7 Password
			password 123@senac

			!Sincronizando as mensagens de logs na tela
			logging synchronous

			!Habilitando o tempo de inatividade de uso da linha virtual
			exec-timeout 5 30

			!Configuração do tipo de protocolo de transporte de entrada
			transport input ssh

			!Saindo de todos os níveis e voltando para o modo EXEC Privilegiado
			end

!Salvando as configurações da memória RAM para a memória NVRAM
write
```

## SEGUNDA ETAPA: Configuração Base Switch Cisco Catalyst Layer 2 2960 (LADO DIREITO - ACESSO)
```python
!Acessando o modo Exec Privilegiado
enable

!Configuração de Data/Hora em inglês, você pode usar abreviado ou completo
clock set 14:00:00 14 June 2024

	!Acessando o modo de configuração global de comandos
	configure terminal

		!Configuração do nome do switch
		hostname sw-04

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
			exit

		!Acessando as linhas virtuais de acesso remoto do Switch
		line vty 0 4

			!Forçando fazer login local utilizando usuário e senha locais do switch
			login local

			!Habilitando senha de acesso do Tipo-7 Password
			password 123@senac

			!Sincronizando as mensagens de logs na tela
			logging synchronous

			!Habilitando o tempo de inatividade de uso da linha virtual
			exec-timeout 5 30

			!Configuração do tipo de protocolo de transporte de entrada
			transport input ssh

			!Saindo de todos os níveis e voltando para o modo EXEC Privilegiado
			end

!Salvando as configurações da memória RAM para a memória NVRAM
write
```

## TERCEIRA ETAPA: Configuração Base Switch Cisco Multilayer 3650 (CENTRO - DISTRIBUIÇÃO)
```python
!Acessando o modo Exec Privilegiado
enable

!Configuração de Data/Hora em inglês, você pode usar abreviado ou completo
clock set 14:00:00 14 June 2024

	!Acessando o modo de configuração global de comandos
	configure terminal

		!Configuração do nome do switch
		hostname sw-05

		!Habilitando o serviço de criptografia de senhas do Tipo-7 Password 
		service password-encryption
		
		!Habilitando o serviço de marcação de Data/Hora detalhado nos Logs
		service timestamps log datetime msec

		!Habilitando o serviço de marcação de Data/Hora detalhado nos Logs do Debug
		service timestamps debug datetime msec

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

		!Bloqueando tentativas de conexões simultâneas com falha de autenticação no Switch
		login block-for 120 attempts 2 within 60

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
			exit

		!Acessando as linhas virtuais de acesso remoto do Switch
		line vty 0 4

			!Forçando fazer login local utilizando usuário e senha locais do switch
			login local

			!Habilitando senha de acesso do Tipo-7 Password
			password 123@senac

			!Sincronizando as mensagens de logs na tela
			logging synchronous

			!Habilitando o tempo de inatividade de uso da linha virtual
			exec-timeout 5 30

			!Configuração do tipo de protocolo de transporte de entrada
			transport input ssh

			!Saindo de todos os níveis e voltando para o modo EXEC Privilegiado
			end

!Salvando as configurações da memória RAM para a memória NVRAM
write
```

## QUARTA ETAPA: Configuração Base do Router Cisco 1941 (CENTRO - NÚCLEO)
```python
!Acessando o modo EXEC Privilegiado
enable

!Configuração de Data/Hora Router
clock set 14:00:00 14 June 2024

	!Acessando o modo de Configuração Global de comandos
	configure terminal

		!Configuração do nome do router
		hostname rt-02

		!Habilitando o serviço de criptografia de senhas do Tipo-7 Password 
		service password-encryption

		!Habilitando o serviço de marcação de Data/Hora detalhado nos Logs
		service timestamps log datetime msec
		service timestamps debug datetime msec

		!Desativando a resolução de nomes de domínio
		no ip domain-lookup

		!Configuração do Banner da mensagem do dia
		banner motd #AVISO: acesso autorizado somente a funcionarios#
		
		!Habilitando o comprimento mínimo da criação das senhas do Tipo-5 ou Tipo-7
		security passwords min-length 8

		!Habilitando o uso senha do Tipo-5 Secret para acessar o modo EXEC Privilegiado
		enable secret 123@senac

		!Criação dos usuários locais utilizando senhas do Tipo-5 ou Tipo-7 e privilégios diferenciados
		username senac secret 123@senac
		username vaamonde password 123@senac
		username admin privilege 15 secret 123@senac
		
		!Configuração do nome de domínio FQDN (Fully Qualified Domain Name)
		ip domain-name senac.br

		!Criação da chave de criptografia e habilitando o serviço do SSH Server local
		crypto key generate rsa general-keys modulus 1024

		!Habilitando a versão 2 do serviço de SSH Server
		ip ssh version 2

		!Habilitando o tempo de inatividade para novas conexões do SSH Server
		ip ssh time-out 60

		!Habilitando o número máximo de tentativas de conexões simultâneas no SSH Server
		ip ssh authentication-retries 2
		
		!Bloqueando tentativas de conexões simultâneas com falha de autenticação no Router
		login block-for 120 attempts 2 within 60

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
			
			!Saindo da configuração da linha console
			exit

		!Acessando as linhas virtuais de acesso remoto do Router
		line vty 0 4

			!Forçando fazer login local utilizando usuário e senha locais do Router
			login local

			!Habilitando senha de acesso do Tipo-7 Password
			password 123@senac

			!Sincronizando as mensagens de logs na tela
			logging synchronous

			!Habilitando o tempo de inatividade de uso da linha virtual
			exec-timeout 5 30

			!Configuração do tipo de protocolo de transporte de entrada
			transport input ssh

			!Saindo de todos os níveis e voltando para o modo EXEC Privilegiado
			end

!Salvando as configurações da memória RAM para a memória NVRAM
write
```

## QUINTA ETAPA: Verificando as Configurações dos Switches e Roteadores.

	!Visualizando as Configurações do Running-Config (RAM)
	!OBSERVAÇÃO: ÚNICA LINHA QUE NÃO APARECE NAS CONFIGURAÇÃO É A: crypto key generate rsa
	show running-config

	!Fazendo um Filtro na Visualização do Running-Config somente da Sessão Line Console 0
	show running-config | section include con 0

	!Fazendo um Filtro na Visualização do Running-Config somente da Sessão Line VTY
	show running-config | section include line vty

	!Fazendo um Filtro na Visualização do Running-Config somente do SSH
	!OBSERVAÇÃO: ÚNICA LINHA QUE NÃO APARECE NAS CONFIGURAÇÃO É A: crypto key generate rsa
	show running-config | section include ssh

	!Visualizando as configurações do SSH Server e Versão
	show ip ssh

	!Visualizando das chaves públicas RSA do SSH Server
	show crypto key mypubkey rsa

	!Visualizando as conexões ativas do SSH Server.
	!OBSERVAÇÃO: ESSA OPÇÃO SÓ VAI FUNCIONAR QUANDO VOCÊ SE CONECTAR REMOTAMENTE NO SWITCH OU ROUTER.
	show ssh

	!Visualizando os Usuários Conectados no Switch
	!OBSERVAÇÃO: ESSA OPÇÃO VAI MOSTRAR O USUÁRIO LOGADO NO CONSOLE: con 0 OU NO VTY: vty 0
	show users