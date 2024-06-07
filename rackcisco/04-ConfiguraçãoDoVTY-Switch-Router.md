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

## PRIMEIRA ETAPA: Configuração das Linhas Virtuais do Switch Cisco Catalyst 3560 

```python
!Acessando o modo Exec Privilegiado
enable

	!Acessar modo de configuração global
	configure terminal

	!Acessando as linhas virtuais
	line vty 0 4
		
		!Habilitando senha do tipo Password Tipo-7
		password 123@senac
		
		!Forçando fazer login com usuário e senha local
		login local 
		
		!Sincronizando os logs na tela
		logging synchronous
		
		!Habilitando o tempo de inatividade do terminal
		exec-timeout 5 30
		
		!Configuração do tipo de protocolo de transporte de entrada
		transport input ssh
		
		!Saindo de todos os níveis
		end

!Salvando as configurações
copy running-config startup-config
	
!Visualizando as configurações
show running-config
```

## SEGUNDA ETAPA: Configuração das Linhas Virtuais do Router Cisco 2911

```python
!Acessando o modo Exec Privilegiado
enable

	!Acessar modo de configuração global
	configure terminal
  
	!Acessando as linhas virtuais
	line vty 0 4
		
		!Habilitando senha do tipo Password Tipo-7
		password 123@senac
		
		!Forçando fazer login com usuário e senha local
		login local 
		
		!Sincronizando os logs na tela
		logging synchronous
		
		!Habilitando o tempo de inatividade do terminal
		exec-timeout 5 30
		
		!Configuração do tipo de protocolo de transporte de entrada
		transport input ssh
		
		!Saindo de todos os níveis
		end

!Salvando as configurações
copy running-config startup-config
	
!Visualizando as configurações
show running-config
```