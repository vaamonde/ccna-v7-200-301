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

## PRIMEIRA ETAPA: Configuração dos Routers e Access Point D-Link, TP-Link ou Linksys

01. Procedimento de Reset dos Routers e Access Point D-Link, TP-Link ou Linksys

	Modelo D-Link DIR-809<br>
	Segurar o Botão WPS/Reset por 15 segundos<br>
	Após soltar, todos os LED´s deve piscar e os LED´s de rede ficar ligados e depois apagar.<br>
	Manual: https://www.dlink.com.br/wp-content/uploads/2018/10/DIR-809_A2_Manual_v1.00DI.pdf

	Modelo D-Link DIR-819<br>
	Segurar o Botão WPS/Reset por 15 segundos<br>
	Após soltar, todos os LED´s deve piscar e os LED´s de rede ficar ligados e depois apagar.<br>
	Manual: https://www.dlink.com.br/wp-content/uploads/2018/10/DIR-819_A1_PPPoE.pdf

	Modelo D-Link DIR-846<br>
	Segurar o Botão WPS/Reset por 15 segundos<br>
	Após soltar, todos os LED´s deve piscar e os LED´s de rede ficar ligados e depois apagar.<br>
	Manual: https://www.dlink.com.br/wp-content/uploads/2020/02/DIR-846_MANUAL_10072020_v1.03_EN.pdf

	Modelo D-Link DIR-853<br>
	Segurar o Botão WPS/Reset por 15 segundos<br>
	Após soltar, todos os LED´s deve piscar e os LED´s de rede ficar ligados e depois apagar.<br>
	Manual: https://www.dlink.com.br/wp-content/uploads/2019/03/DIR-853_A2_WiFi.pdf

	Modelo TP-Link AX3000<br>
	Segurar o Botão WPS/Reset por 15 segundos<br>
	Após soltar, todos os LED´s deve piscar e os LED´s de rede ficar ligados e depois apagar.<br>
	Manual: https://static.tp-link.com/upload/manual/2022/202206/20220621/1910013193_Archer%20AX3000%20Pro(US)1.0_UG_V1.pdf

	Modelo Linksys AC-1900<br>
	Segurar o Reset por 15 segundos<br>
	Após soltar, todos os LED´s deve piscar e os LED´s de rede ficar ligados e depois apagar.<br>
	Manual: https://downloads.linksys.com/downloads/userguide/1224699372213/MAN_EA6900_8220_01617A00_Userguide_EN.pdf

	Modelo Linksys EA4500<br>
	Segurar o Reset por 15 segundos<br>
	Após soltar, todos os LED´s deve piscar e os LED´s de rede ficar ligados e depois apagar.<br>
	Manual: https://downloads.linksys.com/downloads/userguide/EA-Series_UG_Full_3425-00125D_EN_FR-CA_Web.pdf

**OBSERVAÇÃO: DESATIVAR O SERVIÇO DE DHCP SERVER DO ROUTER ACCESS POINT D-LINK, TP-LINK OU LINKSYS, CONECTAR O CABO DE REDE NA PORTA 6 DO SEU SWITCH DIRETAMENTE NA PORTA DO SWITCH DO ROUTER ACCESS POINT D-LINK, TP-LINK OU LINKSYS, O ENDEREÇO IPv4 SERÁ FORNECIDO PELO ROUTER CISCO 2911.**

02. Endereço IPv4 de cada Access Point para o Gerenciamento dos Grupos

		Grupo-01	IPv4: 172.16.15.250 - Máscara: 255.255.255.0
		Grupo-02	IPv4: 172.16.25.250 - Máscara: 255.255.255.0
		Grupo-03	IPv4: 172.16.35.250 - Máscara: 255.255.255.0
		Grupo-04	IPv4: 172.16.45.250 - Máscara: 255.255.255.0
		Grupo-05	IPv4: 172.16.55.250 - Máscara: 255.255.255.0
		Grupo-06	IPv4: 172.16.65.250 - Máscara: 255.255.255.0

03. Configuração da Rede Sem-Fio (cuidado com roteador Dual Band 2.4 e 5.0Ghz)

		Grupo-01    SSID: G-01 (G-01-2.4 E G-01-5.0) - Senha: 123@senac
		Grupo-02    SSID: G-02 (G-02-2.4 E G-02-5.0) - Senha: 123@senac
		Grupo-03    SSID: G-03 (G-03-2.4 E G-03-5.0) - Senha: 123@senac
		Grupo-04    SSID: G-04 (G-04-2.4 E G-04-5.0) - Senha: 123@senac
		Grupo-05    SSID: G-05 (G-05-2.4 E G-05-5.0) - Senha: 123@senac
		Grupo-06    SSID: G-06 (G-06-2.4 E G-06-5.0) - Senha: 123@senac

04. Baixar os Softwares de Análise de Rede Sem-Fio no seu Smartphone

	a) WiFiMan: https://play.google.com/store/apps/details?id=com.ubnt.usurvey&hl=pt_BR&gl=US<br>
	b) SIMET Mobile: https://play.google.com/store/apps/details?id=br.ceptro.simet.client.android&hl=pt_BR&gl=US
