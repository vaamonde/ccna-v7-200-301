!Autor: Robson Vaamonde
!Procedimentos em TI: http://procedimentosemti.com.br
!Bora para Prática: http://boraparapratica.com.br
!Robson Vaamonde: http://vaamonde.com.br
!Facebook Procedimentos em TI: https://www.facebook.com/ProcedimentosEmTi
!Facebook Bora para Prática: https://www.facebook.com/BoraParaPratica
!Instagram Procedimentos em TI: https://www.instagram.com/procedimentoem
!YouTUBE Bora Para Prática: https://www.youtube.com/boraparapratica
!Data de criação: 21/04/2020
!Data de atualização: 09/08/2023
!Versão: 0.04
!Testado e homologado no Cisco Packet Tracer 7.3.x, 8.0.x, 8.1.x, 8.2.x e GNS3 2.2.x

!Acessando o modo EXEC Privilegiado
enable

!Configuração de Data/Hora em Inglês, você pode usar o Mês abreviado ou completo na configuração
clock set 19:54:00 05 May 2021

	!Acessando o modo de Configuração Global de comandos
	configure terminal
  
		!Configuração do nome do router
		hostname rt-1941-1

		!Habilitando o serviço de criptografia de senhas do Tipo-7 Password 
		service password-encryption

		!Habilitando o serviço de marcação de Data/Hora detalhado nos Logs
		!DICA: habilitar o recurso de marcação de Data/Hora detalhado no Debug (Depurar)
		!OBSERVAÇÃO: esse recurso é utilizado para análise detalhada de logs de protocolos de roteamento
		service timestamps log datetime msec
		service timestamps debug datetime msec

		!Desativando a resolução de nomes de domínio
		no ip domain-lookup

		!Configuração do Banner da mensagem do dia
		banner motd #AVISO: acesso autorizado somente a funcionarios#
		
		!Habilitando o comprimento mínimo da criação das senhas do Tipo-5 ou Tipo-7
		!DICA: esse recurso aumenta o nível de segurança na criação de senhas no roteador
		!OBSERVAÇÃO: esse recurso não está disponível em Switch Layer 2 2960 ou Switch Layer 3 3560 
		security passwords min-length 8

		!Habilitando o uso senha do Tipo-5 Secret para acessar o modo EXEC Privilegiado
		enable secret vaamonde@pti

		!Criação dos usuários locais utilizando senhas do Tipo-5 ou Tipo-7 e privilégios diferenciados
		username robson secret vaamonde@pti
		username vaamonde password vaamonde@pti
		username admin privilege 15 secret vaamonde@pti
		
		!Configuração do nome de domínio FQDN (Fully Qualified Domain Name)
		ip domain-name vaamonde.pti

		!Criação da chave de criptografia e habilitando o serviço do SSH Server local
		!ADENDO IMPORTANTE: você pode substituir a linha pelo comando completo que hoje e suportado no
		!Cisco PAcket Tracer: crypto key generate rsa general-keys modulus 1024
		crypto key generate rsa general-keys modulus 1024

		!Habilitando a versão 2 do serviço de SSH Server
		ip ssh version 2

		!Habilitando o tempo de inatividade para novas conexões do SSH Server
		ip ssh time-out 60

		!Habilitando o número máximo de tentativas de conexões simultâneas no SSH Server
		ip ssh authentication-retries 2
		
		!Bloqueando tentativas de conexões simultâneas com falha de autenticação no Router
		!DICA: esse recurso é recomendado para aumentar o nível de segurança junto com o serviço do SSH
		!OBSERVAÇÃO: períodos de tempo de bloqueio configurados em segundos (block-for 1 até 65535)
		!OBSERVAÇÃO: tentativas de falhas de conexões em quantidade (attempts 1 até 65535)
		!OBSERVAÇÃO: dentro do período de tempo configurado em segundos (within 1 até 65535)
		!OBSERVAÇÃO: esse recurso não está disponível em Switch Layer 2 2960 mais está disponível no Switch Layer 3 3560
		login block-for 120 attempts 2 within 60

		!Acessando a linha console, porta padrão de acesso Out-of-Band (Fora da Banda)
		line console 0

			!Forçando fazer login local utilizando usuário e senha locais do switch
			login local

			!Habilitando senha de acesso do Tipo-7 Password
			password vaamonde@pti

			!Sincronizando as mensagens de logs na tela
			logging synchronous

			!Habilitando o tempo de inatividade de uso do console
			exec-timeout 5 30
			
			!Saindo da configuração da linha console
			exit

		!Acessando a linha auxiliar, acesso remoto feito utilizando o Fax-Modem
		!DICA: a porta auxiliar permite configurações do suporte a discagem (Fax-Modem)
		!OBSERVAÇÃO: no simulador Cisco Packet Tracer as configurações são limitadas na porta auxiliar
		!OBSERVAÇÃO: essa configuração não é cobrada no CCNAv7, hoje em dia não é mais utilizada
		line aux 0

			!Forçando fazer login local utilizando usuário e senha locais do switch
			login local

			!Habilitando senha de acesso do Tipo-7 Password
			password vaamonde@pti

			!Sincronizando as mensagens de logs na tela
			logging synchronous

			!Habilitando o tempo de inatividade de uso do console
			exec-timeout 5 30
			
			!Habilitando a velocidade de envio e recebimento de dados
			!DICA: geralmente quando utilizamos modem, a velocidade precisa ser configurada
			!DICA: essa velocidade de transmissão vária de equipamento para equipamento
			!OBSERVAÇÃO: configuração feita em bits por segundos (0 até 4294967295)
			speed 115200
			
			!Habilitando o controle de fluxo de dados
			!DICA: o controle de fluxo de dados mantém a estabilidade da transmissão
			!OBSERVAÇÃO: a configuração de fluxo de dados pode ser controlada por hardware ou software
			flowcontrol hardware
			
			!Recursos que não estão disponíveis no Cisco Packet Tracer
			!DICA: a porta auxiliar e bem parecidas com as portas Virtuais VTY
			!modem inout <-- configuração da entrada/saída do modem
			!transport input all <-- protocolo de entrada
			!transport output all <-- protocolo de saída
			
			!Saindo da configuração da linha console
			exit

		!Acessando as linhas virtuais de acesso remoto do Router
		line vty 0 4

			!Forçando fazer login local utilizando usuário e senha locais do Router
			login local

			!Habilitando senha de acesso do Tipo-7 Password
			password vaamonde@pti

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
	
!Visualizando as configurações da memória RAM
show running-config

!Visualizando as configuração das linhas Virtuais ou Físicas
show line