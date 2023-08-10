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

!OBSERVAÇÃO IMPORTANTE: NA NOVA CERTIFICAÇÃO DA CISCO CCNAv7 EXAME 200-301 NÃO É MAIS COBRADO 
!CONHECIMENTOS EM LICENCIAMENTO DO CISCO IOS OU UPGRADES DE CISCO IOS NO SWITCH OU ROUTERS

!Acessando o modo EXEC Privilegiado
enable
	
	!Atualizando o Cisco IOS (Firmware) do Switch Layer 2 2960
	!DICA: as imagens do Cisco IOS estão no formato BIN (binário) e compactadas (m=RAM | z=zip)
	!OBSERVAÇÃO: só executar esse procedimento depois de fazer os Backups do IOS é das Configurações
	!OBSERVAÇÃO: não é aconselhável alterar o nome da imagem, ela segue um padrão de nomenclatura
	!CUIDADO: como o Cisco IOS é uma sub-derivação do Unix/BSD, ele é Case Sensitive (Maiúscula/Minúscula)
	!CUIDADO: por padrão, caso não tenha espaço suficiente na Flash para a nova imagem, o Cisco IOS irá remover 
	!a imagem anterior para liberar espaço para a nova imagem (por causa disso fazer o Backup antes de atualizar)
	copy tftp: flash:
		192.168.1.1
		c2960-lanbasek9-mz.150-2.SE4.bin
	show flash:
	
	!Acessando o modo de Configuração Global de comandos
	configure terminal
	
		!Atualizando o nome da imagem de inicialização do Cisco IOS
		!OBSERVAÇÃO: o nome da imagem tem que ser igual ao copiado para o Flash Card 
		boot system c2960-lanbasek9-mz.150-2.SE4.bin
		
		!Saindo de todos os níveis e voltando para o modo EXEC Privilegiado
		end

!Visualizando as informações da inicialização do Switch Layer 2 2960
show boot
	
!Salvando as configurações da memória RAM para a memória NVRAM
write
	
!Reinicializando o Switch Layer 2 2960
!DICA: no Switch ou Router não existe o comando para desligar somente o comando de reiniciar
!OBSERVAÇÃO: Switch e desligado diretamente no Cabo de Força e o Router utilizando o Botão Power
reload
