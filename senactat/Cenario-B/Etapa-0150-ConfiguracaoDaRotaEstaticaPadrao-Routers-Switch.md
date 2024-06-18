!Autor: Robson Vaamonde
!Procedimentos em TI: http://procedimentosemti.com.br
!Bora para Prática: http://boraparapratica.com.br
!Robson Vaamonde: http://vaamonde.com.br
!Facebook Procedimentos em TI: https://www.facebook.com/ProcedimentosEmTi
!Facebook Bora para Prática: https://www.facebook.com/BoraParaPratica
!Instagram Procedimentos em TI: https://www.instagram.com/procedimentoem
!YouTUBE Bora Para Prática: https://www.youtube.com/boraparapratica
!Data de criação: 10/05/2020
!Data de atualização: 10/05/2020
!Versão: 0.01
!Testado e homologado no Cisco Packet Tracer 7.3 e GNS3 2.2.7

!PRIMEIRA ETAPA: Configuração do Router 1941-2
!Acessando o modo EXEC Privilegiado
enable

	!Acessando o modo de Configuração Global de Comandos
	configure terminal
	
		!Configurando a Interface de Interligação com o Router 1941-1
		interface GigabitEthernet 0/1
		
			!Configurando a descrição da Interface
			description Interface de WAN com o Router 1941-1
			
			!Configuração do endereço IPv4 do Router 1941-2
			!DICA: configuração das Interface de WAN, os endereços IPv4/IPv6 devem pertencer a mesma rede
			!OBSERVAÇÃO: configuração de Link Ponto-a-Ponto (Point-to-Point) é recomendado utilizar endereços IPv4 /30
			!OBSERVAÇÃO: o CIDR /30 permite apenas 4 endereços IPv4 válidos: ID Rede, Primeiro e Último endereço IPv4 e Broadcast
			!EXEMPLO: 2^2-2=2 (2 = Base | ^2 = Exponenciação de 2 bits emprestados | -2 = Subtração do ID de Rede e Broadcast)
			!OBSERVAÇÃO: por padrão todas as Interfaces de Roteador está com o Status Shutdown (Desligadas)
			ip address 10.0.0.2 255.255.255.252
			no shutdown
			exit
			
		!Configurando a Interface de Interligação com Switch Layer 3 3560
		interface GigabitEthernet 0/0
		
			!Configurando a descrição da Interface
			description Interface de LAN com o Switch Layer 3 3560
			
			!Configuração da Velocidade do Link e Modo de Transmissão da Interface
			!OBSERVAÇÃO: essas configurações foram feitas na Interface (Porta de Rede) do Switch Layer 3
			!OBSERVAÇÃO: a velocidade da Interface do Switch Layer 3 é de 100Mbps, por isso a mudança de velocidade
			speed 100
			duplex full
			
			!Configuração do endereço IPv4 do Router 1941
			!OBSERVAÇÃO: esse endereço será o Gateway para o Switch Layer 3 3560
			ip address 192.168.2.254 255.255.255.0
			no shutdown
			exit
			
		!Configurando a Rota Estática para atingir a Rede 192.168.1.0/24
		!DICA: rota estática é indicada para links Ponto-a-Ponto e para redes simples, com poucos roteadores (saltos/caminhos)
		!DICA: rota estática recebe a letra: S (static) no início da rota declarada manualmente na Tabela de Roteamento
		!OBSERVAÇÃO: na tabela de roteamento temos as opções: L - local (Endereço Local) e C - connected (Rede Diretamente Conectada)
		!OBSERVAÇÃO: rota estática é configurada manualmente em cada equipamento da rede, sua atualização não é dinâmica (automática)
		!OBSERVAÇÃO: rota estática tem a Distância Administrativa (AD - Confiabilidade) de: 1 (um)
		!OBSERVAÇÃO: rota estática tem Métrica (Custo) de: 0 (zero)
		!OBSERVAÇÃO: rota estática pode encaminhar redes por: Endereço IPv4/IPv6 de Próximo Salto ou Interface de Saída
		!EXEMPLO: ip route Rede_de_Destino Máscara_de_Rede_de_Destino Interface_de_Saída ou IP_do_Próximo_Salto Distância_Administrativa
		ip route 192.168.1.0 255.255.255.0 10.0.0.1
		ip route 192.168.3.0 255.255.255.0 192.168.2.1
		end
	
!Salvando as configurações da memória RAM para a memória NVRAM
write

!SEGUNDA ETAPA: Configuração do Switch Layer 3 3560
!Acessando o modo EXEC Privilegiado
enable
	configure terminal
	
		!Configurando a Rota Padrão para o Gateway do Router 1941-2
		!DICA: a rota padrão (Default Route), também conhecida como “Gateway de Último Recurso”, é utilizada quando não há rotas conhecidas
		!OBSERVAÇÃO: todos os pacotes para destinos desconhecidos da Tabela do Roteador são enviados para o endereço de rota padrão
		!OBSERVAÇÃO: o endereço de rota padrão no IPv4 (Na notação CIDR) é o: 0.0.0.0/0, também conhecido como “Rota dos Quatro Zeros”.
		!OBSERVAÇÃO: a rota padrão é utilizada para indicar uma rede além dos seus roteadores, como Links com ISP, WAN, VPN, Internet etc 
		!OBSERVAÇÃO: a rota padrão estática recebe a letra S com Asterisco: S* que significa que é um Gateway of last resort
		ip route 0.0.0.0 0.0.0.0 192.168.2.254
		end
write

!TERCEIRA ETAPA: Configuração do Router 1941-1
!Acessando o modo EXEC Privilegiado
enable
	configure terminal
		!Configurando a Interface de Interligação com o Router 1941-2
		interface GigabitEthernet 0/1
			description Interface de WAN com o Router 1941-2
			ip address 10.0.0.1 255.255.255.252
			no shutdown
			exit
			
		!Configurando a Rota Estática para atingir as Redes 192.168.2.0/30 e 192.168.3.0/30
		!OBSERVAÇÃO: nesse cenário vou utilizar a Interface de Saída para as Redes
		ip route 192.168.2.0 255.255.255.0 GigabitEthernet 0/1
		ip route 192.168.3.0 255.255.255.0 GigabitEthernet 0/1
		end
write

!Visualizando as configurações da memória RAM
show running-config | section interface
show running-config | section ip route

!Verificando as informações das Interfaces e Tabela de Roteamento Local
show ip interface brief
show ip route

!Testando a conexão nos Desktops da Rede com o Protocolo ICMP
ping 192.168.1.1
ping 192.168.3.1
tracert 192.168.1.1
tracert 192.168.3.1