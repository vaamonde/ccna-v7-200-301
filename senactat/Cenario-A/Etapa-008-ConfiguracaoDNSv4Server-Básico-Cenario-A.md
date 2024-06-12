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

## PRIMEIRA ETAPA: Conhecendo o Serviço do DNS Server no Cisco Packet Tracer.

**DNSv4 (Domain Name System)** é um sistema hierárquico e distribuído de gestão de nomes para computadores, serviços ou qualquer máquina conectada à Internet ou a uma rede privada. Utilizado principalmente para fazer as resoluções de nomes para endereços IPv4 ou IPv6.

O protocolo padrão utilizado pelo DNS Server é o: *UDP (User Datagram Protocol)* na porta padrão: *53*, utilizada principalmente pelo cliente para fazer as consultas de Nomes para IP ou IP para Nomes.

**OBSERVAÇÃO-01:** O DNS Server também utiliza o: *TCP (Transmission Control Protocol)* na porta padrão: *53*,utilizado para receber a transferência de Zonas entre o Servidores: *Master (Mestre - Preferencial)* e: *Slaver (Escravo - Alternativo)*.

**OBSERVAÇÃO-02:** O DNS Server também utiliza o: *TCP (Transmission Control Protocol)* na porta padrão: *953*, utilizado pelo serviço do RNDC (Remote Name Daemon Control).

**DICA-01:** Zona de Pesquisa Direta: resolução de Nome para endereço IPv4 ou IPv6.

**DICA-02:** Zona de Pesquisa Inversa/Reversa: resolução de endereço IPv4 ou IPv6 para Nome.

**Registros DNS:** Os registros DNS são mapeamentos de arquivos ou sistemas que dizem a um servidor DNS para qual endereço IP um determinado domínio está associado. Também informa aos servidores DNS como lidar com as solicitações que estão sendo enviadas para cada nome de domínio.

**Sintaxe DNS:** Diferentes sequências de letras são usadas para ditar as ações do servidor DNS. Essas letras são chamadas de sintaxe DNS (Exemplo: A, AAAA, CNAME, MX, PTR, NS, SOA, SRV, TXT, etc).

**Registro Tipo A....:** Significa Endereço e é o tipo mais básico de sintaxe DNS. Indica o endereço IP real para um domínio ou computador;<br>
**Registro Tipo AAAA.:** Igual ao Tipo A mais utilizado nas configurações do IPv6;<br>
**Registro Tipo CNAME:** Significa o Nome Canônico (Canonical Name Record) e seu papel é fazer que um domínio use um alias (Pseudônimo - Apelido) de outro domínio;<br>
**Registro Tipo SOA..:** Significa Início de Autoridade. Obviamente é um dos registros de DNS mais importantes;<br>
**Registro Tipo NS...:** Significa Name Server ele indica qual nome de servidor é autoritativo para o domínio.

01. Configurações do Serviço de DNS Server no Cisco Packet Tracer.

**OBSERVAÇÃO-03:** por padrão o Serviço de DNS Server no Cisco Packet Tracer está: *desligado*.

**OBSERVAÇÃO-04:** no Cisco Packet Tracer as configuração de Sintaxe DNS são limitadas somente ao tipos: *A, AAA, CNAME, SOA e NS* estão disponíveis para configuração.

**OBSERVAÇÃO-05:** no Cisco Packet Tracer temos apenas a configuração da Zona de Pesquisa Direta, não está disponível a opção para configurar a Zona de Pesquisa Reversa.

	!Habilitando o Serviço do DNS Server no Servidor 01
	Server-01
		Services
			DNS

	DNS Service:       On
	Resource Records:  Name = server-01       Type = A Record     Address = 192.168.1.1
	Resource Records:  Name = sw-01           Type = A Record     Address = 192.168.1.250
	Resource Records:  Name = sw-02           Type = A Record     Address = 192.168.1.251
	Resource Records:  Name = rt-01           Type = A Record     Address = 192.168.1.254
	Resource Records:  Name = desktop-01      Type = A Record     Address = 192.168.1.10
	Resource Records:  Name = desktop-02      Type = A Record     Address = 192.168.1.11
	Resource Records:  Name = desktop-03      Type = A Record     Address = 192.168.1.12
	Resource Records:  Name = desktop-04      Type = A Record     Address = 192.168.1.13
	Resource Records:  Name = notebook-01     Type = A Record     Address = 192.168.1.21
	Resource Records:  Name = notebook-02     Type = A Record     Address = 192.168.1.23
	Resource Records:  Name = celular-01      Type = A Record     Address = 192.168.1.20
	Resource Records:  Name = celular-02      Type = A Record     Address = 192.168.1.22

a) Abrindo o Prompt de Comando do Desktop.

**DICA-03** não confunda Terminal com Command Prompt, Terminal é utilizado para se conectar no Switch ou Router utilizando o Cabo Console, já o Command Prompt (Prompt de Comando) é utilizado para testar as configurações de rede e acessar remotamente o Switch ou Router.

	!Verificando o endereço IPv4 configurado no Desktop
	C:\> ipconfig

	!Verificando o endereço detalhado IPv4 configurado no Desktop
	C:\> ipconfig /all

	!Testando a Resolução de Nomes DNS no Desktop
	C:\> nslookup server-01
	C:\> nslookup sw-01

	!Testando a comunicação com o Server 01 utilizando o pacote ICMP (Internet Control Message Protocol)
	C:\> ping server-01

	!Testando a comunicação com o Switch 01 utilizando o pacote ICMP (Internet Control Message Protocol)
	C:\> ping sw-01

	!Acessando remotamente o Switch utilizando o protocolo SSH (Secure Shell)
	!OBSERVAÇÃO: -l (éli não é o número "1" (um) e sim "l" (éli) em minúsculo)
	C:\> ssh -l senac sw-01   (Switch SW-01)