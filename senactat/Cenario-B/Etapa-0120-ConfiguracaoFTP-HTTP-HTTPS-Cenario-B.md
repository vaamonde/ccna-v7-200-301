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

## PRIMEIRA ETAPA: Conhecendo o Serviço do FTP, HTTP e HTTPS Server no Cisco Packet Tracer

**FTPv4 (File Transfer Protocol)** é um protocolo padrão/genérico independente do hardware projetado para transferir arquivos pela rede. A transferência de dados em redes de computadores envolve normalmente transferência de arquivos e acesso a sistemas de arquivos remotos.

O protocolo padrão utilizado pelo FTP Server é o: *TCP (Transmission Control Protocol)* na porta padrão: *21*.

O protocolo FTP também utiliza as portas TCP: *20 (ftp-data)* e: *TCP 990 (SFTP) Security FTP* com suporte a SSL/TLS (Secure Sockets Layer / Transport Layer Security).

**HTTP (Hypertext Transfer Protocol)** é um protocolo de comunicação utilizado nos sistemas de informação de hipermídia, distribuídos e colaborativos. Ele é a base para a comunicação de dados da Internet (World Wide Web). Por padrão o protocolo HTTP transfere dados em texto plano, sem criptografia.

O protocolo padrão utilizado pelo HTTP Server é o: *TCP (Transmission Control Protocol)* na porta padrão: *80*.

**HTTPS (Hyper Text Transfer Protocol Secure)** é uma implementação do protocolo HTTP sobre uma camada adicional de segurança que utiliza os protocolos SSL/TLS (Secure Sockets Layer / Transport Layer Security). Essa camada adicional permite que os dados sejam transmitidos por meio de uma conexão criptografada e que se verifique a autenticidade do servidor e do cliente por meio de certificados digitais e unidade certificadoras.

O protocolo padrão utilizado pelo HTTPS Server é o: *TCP (Transmission Control Protocol)* na porta padrão: *443*.

a) Configurações do Serviço de FTP Server no Cisco Packet Tracer:

**OBSERVAÇÃO-01:** por padrão o Serviço de FTP Server no Cisco Packet Tracer está: *ligado*;

**OBSERVAÇÃO-02:** diferente do TFTP o FTP trabalha com autenticação ou acesso anônimo (sem autenticação - famoso usuário: anonymous) e permissões de: *Escrita (Write), Leitura (Read), Remoção (Delete), Renomear (Rename) e Listar (List)* o conteúdo dos arquivos e diretórios.

	!Habilitando o Serviço do FTP Server no Servidor 02
	Server-02
		Services
			FTP

	Service       On
	User Setup    Username: senac      Password: 123@senac
	              Write=Yes, Read=Yes, Delete=Yes, Rename=Yes, List=Yes
	              Username: vaamonde   Password: 123@senac
	              Write=No, Read=Yes, Delete=No, Rename=No, List=Yes

b) Configurações do Serviço de HTTP/HTTPS Server no Cisco Packet Tracer:

**OBSERVAÇÃO-03:** por padrão o Serviço de HTTP/HTTPS Server no Cisco Packet Tracer está: *ligado*;

**OBSERVAÇÃO-04:** recomendo acessar o site: https://www.w3schools.com/ para mais informações sobre a Linguagem de Marcação de Texto HTML.

**DICA-01:** para acessar páginas utilizando o Protocolo HTTPS é necessário a configuração de uma Unidade Certificadora e um Certificado Assinado pela CA (Certificate Authority) para habilitar o recuso do HTTPS.

**OBSERVAÇÃO-05:** o Cisco Packet Tracer é limitado para as configurações de Unidade Certificadora CA e geração dos certificados assinados, esse procedimento e feito em servidores reais como o Windows Server ou GNU/Linux.

	!Habilitando o Serviço do HTTP e HTTPS Server no Servidor 02
	Server-02
		Services
			HTTP

	Service HTTP    On
	Service HTTPS   On

!TERCEIRA ETAPA: Configuração de uma página HTML com nossas informações para testar o serviço HTTP e HTTPS
```html
<!DOCTYPE html>
<html>
	<head>
		<title>Bora para Prática</title>
	</head>
	<body>
		<center>
		<h1>Robson Vaamonde</h1>
		<p>Configuração do Servidor HTTP e HTTPS no Cisco Packet Tracer</p>
		<p><b>Projeto Bora para Prática!!!</b></p>
		<p><b><i><u>Curso de Técnico em Informática</u></i></b></p>
		</center>
	</body>
</html>
```

!Comandos básicos para testar o acesso ao FTP e HTTP/HTTPS

!PRIMEIRA ETAPA: testando localmente no servidor os serviços de rede
nslookup ftp.vaamonde.pti
ping ftp.vaamonde.pti

ftp ftp.vaamonde.pti
	Username: vaamonde
	Password: vaamonde

http://localhost
http://127.0.0.1

!SEGUNDA ETAPA: testando remotamente no cliente Microsoft Windows
http://www.vaamonde.pti
https://www.vaamonde.pti
Text Editor: vaamonde.txt
dir

!Enviando arquivos para o servidor FTP
ftp ftp.vaamonde.pti
	Username: vaamonde
	Password: vaamonde	
	dir
	put vaamonde.txt
	quit

!Recebendo arquivos do servidor FTP
ftp ftp.vaamonde.pti
	Username: robson
	Password: robson	
	get vaamonde.txt
	quit
dir