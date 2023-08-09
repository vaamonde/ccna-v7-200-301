!Autor: Robson Vaamonde
!Procedimentos em TI: http://procedimentosemti.com.br
!Bora para Prática: http://boraparapratica.com.br
!Robson Vaamonde: http://vaamonde.com.br
!Facebook Procedimentos em TI: https://www.facebook.com/ProcedimentosEmTi
!Facebook Bora para Prática: https://www.facebook.com/BoraParaPratica
!Instagram Procedimentos em TI: https://www.instagram.com/procedimentoem
!YouTUBE Bora Para Prática: https://www.youtube.com/boraparapratica
!Data de criação: 18/04/2020
!Data de atualização: 09/08/2023
!Versão: 0.04
!Testado e homologado no Cisco Packet Tracer 7.3.x, 8.0.x, 8.1.x, 8.2.x e GNS3 2.2.x

!Acessando o modo EXEC Privilegiado
enable

	!Acessando o modo de Configuração Global de comandos
	configure terminal
	
		!Configuração do nome de Domínio FQDN (Fully Qualified Domain Name)
		!DICA: o nome de Domínio é utilizado pelo Serviço do SSH e outros serviços de rede, como o serviço de 
		!autenticação remota ou monitoramento de Switch ou Router utilizando os protocolos RADIUS ou TACACS
		ip domain-name vaamonde.pti

		!Criação/Geração da chave de criptografia do serviço do SSH (Secure Socket Shell) Server local
		!DICA: por padrão o serviço do SSH Server está desabilitado no Switch ou Router
		!DICA: por padrão todas as conexões remotas utilizando o protocolo SSH são criptografadas
		!OBSERVAÇÃO: é recomendado utilizar módulos de criptografia de 1024 bits (opções de 360 até 2048)
		!OBSERVAÇÃO: no Switch ou Router Real utilizamos o comando: crypto key generate rsa general-keys modulus 1024
		!OBSERVAÇÃO: existe vários modos de geração das chaves públicas criptografadas, o padrão é utilizar o RSA
		!OBSERVAÇÃO: a porta padrão de conexão do serviço de SSH é a: 22 utilizando o Protocolo TCP
		!ADENDO: versões do Cisco Packet Tracer >=7.3 possui o suporte para o comando completo de geração das chaves SSH
		!RSA nos Switches ou Router, utilizando o comando: crypto key generate rsa general-keys modulus 1024
		!OBSERVAÇÃO IMPORTANTE: caso queira desativar o serviço do SSH ou remover os Módulos RSA, digite o comando:
		!crypto key zeroize rsa, caso você digite novamente o comando: crypto key generate rsa ele vai solicitar se
		!você quer substituir os Módulos atuais (Do you really want to replace them? [yes/no])
		crypto key generate rsa general-keys modulus 1024

		!Habilitando a versão 2 do serviço de SSH Server
		!DICA: a versão 2 do serviço do SSH Server corrigi várias falhas de segurança existe na versão 1.99
		!OBSERVAÇÃO: após a criação da chave RSA do SSH o serviço habilita a versão 1.99 por padrão
		ip ssh version 2

		!Habilitando o tempo de inatividade para novas conexões do SSH Server
		!DICA: configuração de inatividade é feita somente em segundos (1 até 120 - 2 minutos)
		!OBSERVAÇÃO: essa configuração está relacionada ao tempo para se autenticar no serviço do SSH no Switch ou Router
		ip ssh time-out 60

		!Habilitando o número máximo de tentativas de conexões simultâneas no SSH Server
		!DICA: essa opção aumenta o nível de segurança contra ataques de Força Bruta (Brute-Force)
		!OBSERVAÇÃO: limites de conexões simultâneas vai de: 0 até 5
		ip ssh authentication-retries 2

		!Acessando as linhas virtuais de acesso remoto do Switch
		line vty 0 4
		
			!Configuração do protocolo de transporte de entrada para aceitar somente o protocolo SSH
			transport input ssh

			!Saindo de todos os níveis e voltando para o modo EXEC Privilegiado
			end

!Salvando as configurações da memória RAM para a memória NVRAM
copy running-config startup-config
	
!Visualizando as configurações da memória RAM
show running-config

!Visualizando as configurações do SSH Server
show ip ssh

!Visualizando das chaves públicas RSA
show crypto key mypubkey rsa

!Visualizando as conexões ativas do SSH Server
show ssh

!Verificando o endereço IPv4 no Desktop
ipconfig

!Testando a comunicação com o Switch utilizando pacotes ICMP
ping 192.168.1.250
ping 192.168.1.251

!Acessando remotamente o Switch utilizando o protocolo Telnet
telnet 192.168.1.250
telnet 192.168.1.251

!Acessando remotamente o Switch utilizando o protocolo SSH
!OBSERVAÇÃO: -l (não é o número "1" e sim "l" minúsculo)
ssh -l admin 192.168.1.250
ssh -l admin 192.168.1.251

!Visualizando as conexões remotas estabelecidas no Switch
show users

==============================================================================================

!Automação da configuração do Switch 2

!Acessando o modo EXEC Privilegiado
enable

	!Acessando o modo de Configuração Global de comandos
	configure terminal
	
		!Configuração do nome de domínio FQDN (Nome de Domínio Totalmente Qualificado)
		ip domain-name vaamonde.pti

		!Criação da chave de criptografia e habilitar o serviço de SSH Server local
		crypto key generate rsa

		!Habilitando a versão 2 do serviço de SSH Server
		ip ssh version 2

		!Habilitando o tempo de inatividade para novas conexões do SSH Server
		ip ssh time-out 60

		!Habilitando o número máximo de tentativas de conexões simultâneas no SSH Server
		ip ssh authentication-retries 2

		!Acessando as linhas virtuais de acesso remoto do Switch
		line vty 0 4
		
			!Configuração do protocolo de transporte somente SSH
			transport input ssh

			!Saindo de todos os níveis e voltando para o modo EXEC Privilegiado
			end

!Salvando as configurações da memória RAM para a memória NVRAM
write
	
!Visualizando as configurações da memória RAM
show running-config

!Visualizando as configurações do SSH Server
show ip ssh

!Visualizando das chaves públicas RSA
show crypto key mypubkey rsa

!Visualizando as conexões ativas do SSH Server
show ssh

!Visualizando as conexões remotas estabelecidas no Switch
show users
