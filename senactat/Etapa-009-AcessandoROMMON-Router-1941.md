!Autor: Robson Vaamonde
!Procedimentos em TI: http://procedimentosemti.com.br
!Bora para Prática: http://boraparapratica.com.br
!Robson Vaamonde: http://vaamonde.com.br
!Facebook Procedimentos em TI: https://www.facebook.com/ProcedimentosEmTi
!Facebook Bora para Prática: https://www.facebook.com/BoraParaPratica
!Instagram Procedimentos em TI: https://www.instagram.com/procedimentoem
!YouTUBE Bora Para Prática: https://www.youtube.com/boraparapratica
!Data de criação: 26/04/2020
!Data de atualização: 09/08/2023
!Versão: 0.04
!Testado e homologado no Cisco Packet Tracer 7.3.x, 8.0.x, 8.1.x, 8.2.x e GNS3 2.2.x

!ADENDO: No vídeo não foi comentando sobre a inicialização do serviço do SSH Server depois que o Router ou Switch
!é resetado. Para resolver essa falha, recomendo digitar os comandos: crypto key zeroize rsa (zerar as chaves) e
!depois o comando: crypto key generate rsa (gerar as chaves novamente), você pode digitar o comando completo
!crypto key generate rsa general-keys modulus 1024 que hoje e suporte na versão mais nova do Cisco IOS do Packet Tracer

!ADENDO: No vídeo não foi comentando sobre a inicialização das Interfaces, por padrão nos arquivos running-config ou
!startup-config o comando: no shutdown não está presente, quando você retorna um backup das configurações do Router
!as Interfaces vão está no Status Shutdown, você pode adicionar nos arquivos de configurações o comando para inicializar
!as Interfaces: no shutdown

!PRIMEIRA ETAPA: parar a inicialização do Cisco IOS do Router 1941
!DICA: no Cisco Packet Tracer utilizamos a combinação de teclas: Ctrl+C
!OBSERVAÇÃO: em equipamento reais, podemos utilizar as combinações de teclas: Ctrl+C, Ctrl+Break ou Ctrl+Backspace
!OBSERVAÇÃO: no aplicativo PuTTY você deve usar o Botão direito do Mouse na Barra de Título e utilizar a opção:
!Send Command: Break

!Visualizando as opções de comandos do Modo ROMMON (ROM (read-only memory) monitor)
rommon 1 >?

!Alterando o modo de inicialização do Cisco IOS do Router 1941
!DICA: o comando confreg altera a forma como a inicialização do Cisco IOS ler os arquivos de configuração
!DICA: no modo ROMMON a opção do TAB não funciona, precisando digitar o comando completo
!OBSERVAÇÃO: essa opção força o Router a não ler as configurações do startup-config na inicialização
!OBSERVAÇÃO: chave de registro em hexadecimal: 0x2142 (não ler as configurações do startup-config)
!OBSERVAÇÃO: chave de registro em hexadecimal: 0x2102 (ler as configurações do startup-config - padrão)
!CUIDADO: existe várias chaves de registro do Cisco IOS, se você errar a chave pode acontecer do Cisco IOS 
!inicializar de forma incorreta ou com caracteres irreconhecível na Linha Console ou na Linha Virtual.
rommon 2 >confreg 0x2142

!Reinicializando o Router 1941 do Modo ROMMON
rommon 3 >reset

!Acessando o modo EXEC Privilegiado
enable

	!Visualizando as configurações de inicialização do Router 1941
	show version
	
	!Visualizando as configurações do startup-config
	show startup-config
	
	!Limpando as configurações do startup-config
	erase startup-config
	show startup-config
	
	!Acessando o modo de Configuração Global de comandos
	configure terminal
	
		!Alterando o modo de inicialização do Cisco IOS do Router 1941
		config-register 0x2102
		
		!Saindo de todos os níveis e voltando para o modo EXEC Privilegiado
		end
	
!Salvando as configurações da memória RAM para a memória NVRAM
write
	
!Reinicializando o Router 1941
reload

!Acessando o modo EXEC Privilegiado
enable

	!Visualizando as configurações de inicialização do Router 1941
	show version
	
	!Visualizando os arquivos no Flash Card
	show flash:
	
	!Copiando o arquivos do Flash Card startup-config para NVRAM
	copy flash: startup-config 
		startup-config 
	
	!Visualizando as configurações do startup-config
	show startup-config
	
	!Aplicando as configurações da NVRAM (startup-config) para a RAM (running-config)
	!OBSERVAÇÃO: no vídeo após a cópia da configuração da NVRAM para RAM, por padrão as Interfaces não estão 
	!inicializadas sendo necessário inicializar manualmente cada Interface, no arquivo running-config por 
	!padrão não tem o comando: no shutdown
	!ERRATA: no vídeo não foi falado ou comentado sobre isso, não esqueça de inicializar as Interfaces após o Backup
	copy startup-config running-config
	
	!Salvando as configurações da memória RAM para a memória NVRAM
	write
	
	!Reinicializando o Router 1941
	reload
	
!SEGUNDA ETAPA: parar a inicialização do Cisco IOS do Switch Layer 2 2960 ou Layer 3 3560
!OBSERVAÇÃO: no Cisco Packet Tracer esse procedimento é limitado, não sendo possível demonstrar, somente em equipamentos reais.

_01# Deixar o Switch 2960 ou 3560 inicializar normalmente;
_02# Após a inicialização, pressionar o Botão MODE por aproximadamente 15/20 segundos;
_03# Os LED's do Switch vai piscar e entrar no modo de ROMMON, o Switch será reinicializado automaticamente;
_04# Após a reinicialização o Switch será resetado para o modo de fábrica (fabric mode).

!Caso o Switch 2960 ou 3560 não volte para o modo de Fábrica (Reset), utilizar os procedimentos abaixo:
!CUIDADO: só utilizar esse procedimento se for realmente necessário ou se os equipamentos não voltar

1. Pressionar o botão MODE até o Switch ser reinicializado;
2. Na tela de inicialização, na mensagem de hardware, pressionar o botão MODE para cancelar o carregamento do IOS;
3. No modo ROMMON, digitar o comando: flash_init
4. Listar o conteúdo da Flash: dir flash:
5. Renomear o arquivo config: rename flash:config.text flash:config.old
6. Reinicializar o Switch: boot
7. Limpar o arquivo statup-config: erase startup-config
8. Limpar as configurações de VLAN: delete flash:vlan.dat
9. Reinicializar o Switch: reload

!ADENDO: NÃO ESTÁ NO VÍDEO: Atualização do Cisco IOS via TFTPDNLD ROMMON
!OBSERVAÇÃO: esse recurso é utilizado em caso de corrompimento do Cisco ISO da Flash

rommon 1 > IP_ADDRESS=192.168.10.20 
rommon 2 > IP_SUBNET_MASK=255.255.255.0 
rommon 3 > DEFAULT_GATEWAY=192.168.10.1
rommon 4 > TFTP_SERVER=192.168.10.10
rommon 5 > TFTP_FILE=c2960-lanbasek9-mz.150-2.SE4.bin
rommon 6 > TFTP_CHECKSUM=0
rommon 7 > set
rommon 8 > tftpdnld
rommon 9 > confreg 0x2102
rommon 10 > reset