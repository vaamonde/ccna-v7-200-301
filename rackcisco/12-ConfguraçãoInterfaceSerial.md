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

## PRIMEIRA ETAPA: Configuração da Interface Serial no Router Cisco 2911

```python
!Acessando o modo Exec Privilegiado
enable

	!Acessar modo de configuração global
	configure terminal
		
	!Configuração da interface Serial0/0/0
	interface serial 0/0/0
	
		!Descrição da Interface Serial
		!OBSERVAÇÃO IMPORTANTE: veja o arquivo 00-DocumentacaoDaRede.txt a partir da linha: 232
		!(SÉTIMA ETAPA: Determinação da Interface Serial de WAN dos Grupos e seu Endereçamento IPv4)
		description Interface Serial do Grupo-??? para Grupo-???
		
		!Configuração do endereçamento IPv4
		!Verificar a tabela de endereçamento IP dos Grupos
		!Sempre vai ser o Endereço IPv4 IMPAR na Interface Serial 0/0/0
		ip address 192.168.1.??? 255.255.255.252
		
		!Configurando o Clock Rate, Velocidade do Link
		clock rate 64000
		
		!Configurando a Largura de Banda
		bandwidth 64
		
		!Habilitando a interface
		no shutdown
		
		!Saindo das configurações da interface
		exit
		
	!Configuração da interface Serial0/0/1
	interface serial 0/0/1
	
		!Descrição da Interface
		!OBSERVAÇÃO IMPORTANTE: veja o arquivo 00-DocumentacaoDaRede.txt a partir da linha: 232
		!(SÉTIMA ETAPA: Determinação da Interface Serial de WAN dos Grupos e seu Endereçamento IPv4)
		description Interface Serial do Grupo-??? para Grupo-???
		
		!Configuração do endereçamento IP
		!Verificar a tabela de endereçamento IP dos Grupos
		!Sempre vai ser o Endereço IPv4 PAR na Interface Serial 0/0/1
		ip address 192.168.1.??? 255.255.255.252
		
		!Configurando a Largura de Banda
		bandwidth 64
		
		!Habilitando a interface
		no shutdown
		
		!Saindo das configurações da interface
		end

!Salvando as configurações
copy running-config startup-config

!Visualizando as configurações
show running-config

!Visualizando as configurações de endereçamento IPv4
show ip interface brief

!Visualizando as informações de Roteamento
show ip route

ROUTER VIZINHO-DCE <---> DTE-0/0/1_SEU ROUTER_DCE-0/0/0 <---> DTE-ROUTER VIZINHO

!Pingar a SUA Interface Serial 0/0/0 (SEMPRE SERÁ O IPv4 PAR)
ping 192.168.1.??? (serial 0/0/0)

!Pingar a SUA Interface Serial 0/0/1 (SEMPRE SERÁ O IPv4 IMPAR)
ping 192.168.1.??? (serial 0/0/1)

!Pingar a Interface Serial 0/0/0 do SEU VIZINHO (SEMPRE SERÁ O IPv4 IMPAR)
ping 192.168.1.??? (serial 0/0/0)

!Pingar a Interface Serial 0/0/1 do SEU VIZINHO (SEMPRE SERÁ O IPv4 PAR)
ping 192.168.1.??? (serial 0/0/0)
```