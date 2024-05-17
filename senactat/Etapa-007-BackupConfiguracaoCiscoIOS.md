!Autor: Robson Vaamonde
!Procedimentos em TI: http://procedimentosemti.com.br
!Bora para Prática: http://boraparapratica.com.br
!Robson Vaamonde: http://vaamonde.com.br
!Facebook Procedimentos em TI: https://www.facebook.com/ProcedimentosEmTi
!Facebook Bora para Prática: https://www.facebook.com/BoraParaPratica
!Instagram Procedimentos em TI: https://www.instagram.com/procedimentoem
!YouTUBE Bora Para Prática: https://www.youtube.com/boraparapratica
!Data de criação: 24/04/2020
!Data de atualização: 09/08/2023
!Versão: 0.04
!Testado e homologado no Cisco Packet Tracer 7.3.x, 8.0.x, 8.1.x, 8.2.x e GNS3 2.2.x

!PRIMEIRA ETAPA: Backup das Configurações e Cisco IOS do Switch Layer 2 2960
!Acessando o modo EXEC Privilegiado
enable
	
	!Visualizando a versão do Cisco IOS e informações do Hardware do Switch Layer 2 2960
	!DICA: esse comando é utilizado para verificar a versão de hardware e do IOS do Switch ou Router
	!DICA: atualmente a versão utilizada nos hardware da Cisco é a 15.x (ou superior, dependendo do modelo)
	!OBSERVAÇÃO: as informações de memórias em equipamentos da Cisco estão em Kbytes ou em Bytes
	!OBSERVAÇÃO: esse comando fornece informações referente a Configuração do Registro de Inicialização
	show version
		63488K bytes of flash-simulated non-volatile configuration memory.
		63488KB/1000=64MB

	!Visualizando as informações da inicialização do Switch Layer 2 2960
	!DICA: esse comando é utilizado para verificar o arquivo de configuração de inicialização
	!OBSERVAÇÃO: as informações são importante para o processo de quebra de senha do Switch
	show boot
	
	!Visualizando as informações do Flash Card (Memória de Massa) do Switch Layer 2 2960
	!DICA: a memória de massa em Switch geralmente são Chips soldados ou módulos internos
	!OBSERVAÇÃO: diferente do Router, a memória Flash em Switch não pode ser acessada sem desmontar o equipamento
	show flash:
	dir flash:
		64016384 Bytes Total = 64 MB
		59599664 Bytes Free  = 60 MB
	
	!Salvando as configurações da memória RAM para a memória NVRAM
	copy running-config startup-config
	
	!Salvando as configurações da memória NVRAM para a memória FLASH
	copy startup-config flash: 
	dir flash:
	
	!Salvando as configurações da memória NVRAM para o Servidor TFTP 
	!DICA: o serviço de TFTP (Trivial File Transfer Protocol) utiliza o Protocolo UDP na Porta Padrão 69
	!OBSERVAÇÃO: o protocolo UDP (User Datagram Protocol) não é confiável, porque ele não exige confirmação
	!OBSERVAÇÃO: o protocolo TFTP foi escolhido pela Cisco para ser o sistema padrão de Atualização e Backup
	dir nvram:
	ping 192.168.1.1
	copy startup-config tftp:
		192.168.1.1
	
	!Salvando a imagem do Cisco IOS do Switch Layer 2 2960 para o Servidor TFTP
	!DICA: as imagens do Cisco IOS estão no formato BIN (binário) e compactadas (m=RAM | z=zip)
	!OBSERVAÇÃO: não é aconselhável alterar o nome da imagem, ela segue um padrão de nomenclatura
	!EXEMPLO: c2960-lanbase-mz.122-25.FX.bin (Primeira parte: c2960 plataforma/família do equipamento, Segunda 
	!parte: lanbase indicação do package/funcionalidade do IOS, Terceira parte: compactação da Imagem m=RAM | z=zip
	!Quarta parte: 122-25.FX.bin versão do IOS)
	!CUIDADO: como o Cisco IOS é uma sub-derivação do Unix/BSD, ele também é Case Sensitive (Maiúscula/Minúscula)
	copy flash: tftp:
		c2960-lanbase-mz.122-25.FX.bin
		192.168.1.1
	
	!Salvando as configurações do Running Config ou Startup Config no Bloco de Notas
	!DICA: esse é o método mais simples de backup das configurações do Switch ou Router 
	!OBSERVAÇÃO: utilizar sempre um editor de texto profissional para não modificar a estrutura do arquivo
	!DICA: copiar as informações a partir da primeira: ! (exclamação) do running-config ou startup-config
	!até a última opção: end
	show running-config
	
	!Saindo do modo EXEC Privilegiado
	disable
	
=====================================================================================================

!SEGUNDA ETAPA: Backup das Configurações e Cisco IOS do Router 1941
!Acessando o modo EXEC Privilegiado
enable
	
	!Visualizando a versão do Cisco IOS e informações do Hardware do Router
	!DICA: em roteadores esse comando fornece informações de licenciamento do hardware
	!OBSERVAÇÃO: igual no Switch, esse comando fornece informações de inicialização do IOS do Router
	!OBSERVAÇÃO: em roteadores não temos o comando: show boot
	show version
		249856K bytes of ATA System CompactFlash 0 (Read/Write)
		249856KB/1000=250MB
	
	!Visualizando informações do Flash Card (Memória de Massa) do Router 1941
	!DICA: em roteadores temos vários módulos de memória Flash Card
	!OBSERVAÇÃO: o acesso a memória Flash em roteadores é feito utilizando módulos externos
	show flash:
	dir flash0:
		255744000 Bytes Total = 256MB
		33847587 Bytes Used = 34MB
		221896413 Bytes Available = 222MB
	
	!Salvando as configurações da memória RAM para memória NVRAM
	copy running-config startup-config
	
	!Salvando as configurações da memória NVRAM para a memória FLASH
	copy startup-config flash: 
	
	!Salvando as configurações da memória NVRAM para o Servidor TFTP
	dir nvram:
	ping 192.168.1.1
	copy startup-config tftp:
		192.168.1.1
	
	!Salvando a imagem do Cisco IOS do Router 1941 para o Servidor TFTP
	copy flash: tftp:
		c1900-universalk9-mz.SPA.151-4.M4.bin
		192.168.1.1
		
	!Salvando as configurações do Running Config ou Startup Config no Bloco de Notas
	show running-config
	
	!Saindo do modo EXEC Privilegiado
	disable
