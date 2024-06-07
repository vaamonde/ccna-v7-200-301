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

## PRIMEIRA ETAPA: Configuração SVI (Switch Virtual Interface) no Switch Cisco Catalyst 3560 

```python
!Acessando o modo Exec Privilegiado
enable

	!Acessar modo de configuração global
	configure terminal
	
	!Configuração do gateway padrão IPv4 do SVI
	!Utilizado para acessar remotamente o equipamento
	!OBSERVAÇÃO IMPORTANTE: veja o arquivo 00-DocumentacaoDaRede.txt a partir da linha: 129 
	!(QUARTA ETAPA: Determinação dos Endereços de SVI (Switch Virtual Interface) e Gateway de cada Grupo)
	ip default-gateway 172.16.???.254
  
	!Configuração da interface virtual VLAN SVI
	!OBSERVAÇÃO IMPORTANTE: veja o arquivo 00-DocumentacaoDaRede.txt a partir da linha: 77
	!(TERCEIRA ETAPA: Determinação das Redes (Sub-Redes) e VLAN (Virtual-LAN) de Cada Grupo)
	interface vlan ???
		
		!Configuração da descrição
		description Interface SVI de Gerenciamento do Grupo-0???
		
		!Configuração do endereçamento IPv4 do SVI
		!OBSERVAÇÃO IMPORTANTE: veja o arquivo 00-DocumentacaoDaRede.txt a partir da linha: 129
		!(QUARTA ETAPA: Determinação dos Endereços de SVI (Switch Virtual Interface) e Gateway de cada Grupo)
		ip address 172.16.???.253 255.255.255.0
		
		!Inicializando a interface
		no shutdown
		
		!Saindo de todos os níveis
		end

!Salvando as configurações
copy running-config startup-config
	
!Visualizando as configurações
show running-config

!Visualizando as configurações de endereçamento IPv4
show ip interface brief

!Visualizando as informações de VLAN
show vlan brief

!Visualizando informações detalhadas da VLAN
show vlan id ???
```