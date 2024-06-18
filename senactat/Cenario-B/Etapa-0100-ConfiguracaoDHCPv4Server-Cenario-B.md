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
Data de atualização: 18/05/2024<br>
Versão: 0.02<br>
Testado e homologado no Cisco Packet Tracer 8.2.x e Rack Cisco SW-3560 e RT-2911

## INFORMAÇÕES IMPORTANTES SOBRE ESSA DOCUMENTAÇÃO:

A) **ACRÉSCIMO:** informações ou comandos que não estava no script original e nem comentado no vídeo, algo importante para o cenário ou dicas de alunos;<br>
B) **DESAFIO:** desafio proposto para o aluno, com o objetivo de estimular o raciocínio lógico para a resolução de problemas de rede ou mudanças nas configurações;<br>
C) **DICA:** informações importantes da tecnologia ou da prova de certificação, dica para configurar ou lembrar os recursos para sua configuração no exame;<br>
D) **ERRATA:** correções dos scripts, correções de falas, correções de configurações, etc...;<br>
E) **EXEMPLO:** exemplos de comandos ou configurações das opções de DICAS ou OBSERVAÇÃO;<br>
F) **IMPORTANTE:** informações importantes da tecnologia ou da configuração, com foco em adicionar informações detalhadas da tecnologia ou da certificação;<br>
G) **OBSERVAÇÃO:** informações relevantes da tecnologia ou da configuração, com foco em adicionar informações extras da tecnologia ou da certificação.

## PRIMEIRA ETAPA: Conhecendo o Serviço do DHCP Server no Cisco Packet Tracer.

**DHCPv4 (Dynamic Host Configuration Protocol)** é um protocolo de serviço *TCP/IP (Transmission Control Protocol/Internet Protocol)* que oferece configuração dinâmica de dispositivos finais, com concessão de endereços IP de Host (Computador), máscara de sub-rede, gateway padrão, servidores DNS (Domain Name Service), sufixos de pesquisa do DNS, servidores WINS (Windows Internet Name Service), servidores NTP (Network Time Protocol) é muito mais.

O protocolo padrão utilizado pelo DHCP Server é o: *UDP (User Datagram Protocol)* na porta padrão: *67*.

**Escopo DHCP:** Trata-se do intervalo completo dos possíveis endereços IP de uma rede. Os escopos definem a sub-rede física da rede que vai oferecer os serviços do DHCP.

a) Configurações do Serviço de DHCP Server no Cisco Packet Tracer:

**OBSERVAÇÃO-01:** por padrão o Serviço de DHCP Server no Cisco Packet Tracer está: *desligado*

**OBSERVAÇÃO-02:** o nome do escopo padrão do DHCP Server no Cisco Packet Tracer tem que ser: *serverPool*

**DICA-01:** o escopo inicial está sempre relacionado a Placa de Rede e sua Configuração do Endereçamento IPv4, com base nesse endereço que é ofertado o escopo de rede.

**DICA-02:** geralmente em Servidores Microsoft ou GNU/Linux, após a instalação do Serviço do DHCP Server ele está desligado por padrão para não entrar em conflito com outros servidores na rede.

**CUIDADO-01:** é recomendado ter apenas: *1 (um) Servidor DHCP* na rede, em redes mais complexas existe a possibilidade de mais servidores para prover redundância.

**OBSERVAÇÃO-03:** o Switch Cisco Catalyst Layer 3 3560 ou Router possui os recursos para a configuração do DHCP Server, para redes pequenas e de médio porte é recomendado o seu uso, para redes grandes ou complexas o seu uso é limitado em alguns recursos, principalmente de monitoramento, relatórios e integrações de serviços.

	!Habilitando o Serviço do DHCP Server no Servidor 02
	Server-02
		Services
			DNS

	!Configurando o Escopo padrão da Rede 192.68.3.0/24
	Interface:                 FastEthernet0
	Service:                   On
	Pool Name:                 serverPool
	Default Gateway:           192.168.3.254
	DNS Server:                192.168.3.1    (DNS Preferencial ou Alternativo - no Cisco Packet Tracer e limitado)
	Start IP Address:          192.168.3.100  (Início da Faixa de Oferta de Endereços IPv4)
	Subnet Mask:               255.255.255.0
	Maximum Number of Users:   50             (Fim da Faixa de Oferta de Endereços IPv4 - 100 até 150)
	TFTP Server:               192.168.3.1
	WLC Address:               NÃO UTILIZADO NESSE VÍDEO (Endereço IP do WLC - Wireless LAN Controller)
	<Save>

b) Abrindo o Prompt de Comando do Desktop;

**DICA-03** não confunda Terminal com Command Prompt, Terminal é utilizado para se conectar no Switch ou Router utilizando o Cabo Console, já o Command Prompt (Prompt de Comando) é utilizado para testar as configurações de rede e acessar remotamente o Switch ou Router.

	!Verificando o endereço IPv4 configurado no Desktop
	C:\> ipconfig

	!Verificando o endereço detalhado IPv4 configurado no Desktop
	C:\> ipconfig /all

	!Liberando o Aluguel do Leasing do DHCP Client
	C:\> ipconfig /release

	!Renovando o Aluguel do Leasing do DHCP Cliente
	C:\> ipconfig /renew

	!Verificando o endereço detalhado IPv4 configurado no Desktop
	C:\> ipconfig /all

	!Testando a comunicação com o Server 01 utilizando o pacote ICMP (Internet Control Message Protocol)
	C:\> ping 192.168.3.1
