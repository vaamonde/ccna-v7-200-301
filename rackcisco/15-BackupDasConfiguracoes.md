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

## PRIMEIRA ETAPA: Backup das Configurações do Switch Cisco Catalyst 3560 e do Router Cisco 2911

01. Backup das configurações do Router Cisco 2911

```python
!Acessando o modo exec privilegiado
enable

	!Salvando as configurações da RAM para a NVRAM
	copy running-config startup-config
	
	!Salvando uma cópia das configurações da NVRAM para FLASH
	copy startup-config flash:
	
	!Visualizando o conteúdo da Flash
	dir flash:
	
	!Salvando as configurações para NOTEPAD++ ou VSCode
	!OBSERVAÇÃO IMPORTANTE: será mostrado em sala de aula os procedimentos
	show running-config
```

01. Backup das configurações do Switch Cisco Catalyst 3560

```python
!Acessando o modo exec privilegiado
enable

	!Salvando as configurações da RAM para a NVRAM
	copy running-config startup-config
	
	!Salvando uma cópia das configurações da NVRAM para FLASH
	copy startup-config flash:
	
	!Visualizando o conteúdo da Flash
	dir flash:
	
	!Salvando as configurações para NOTEPAD++ ou VSCode
	!OBSERVAÇÃO IMPORTANTE: será mostrado em sala de aula os procedimentos
	show running-config
```