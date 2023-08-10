!Autor: Robson Vaamonde
!Procedimentos em TI: http://procedimentosemti.com.br
!Bora para Prática: http://boraparapratica.com.br
!Robson Vaamonde: http://vaamonde.com.br
!Facebook Procedimentos em TI: https://www.facebook.com/ProcedimentosEmTi
!Facebook Bora para Prática: https://www.facebook.com/BoraParaPratica
!Instagram Procedimentos em TI: https://www.instagram.com/procedimentoem
!YouTUBE Bora Para Prática: https://www.youtube.com/boraparapratica
!Data de criação: 30/04/2020
!Data de atualização: 10/08/2023
!Versão: 0.04
!Testado e homologado no Cisco Packet Tracer 7.3.x, 8.0.x, 8.1.x, 8.2.x e GNS3 2.2.x

!FTPv4 (File Transfer Protocol) é um protocolo padrão/genérico independente do hardware projetado para
!transferir arquivos pela rede. A transferência de dados em redes de computadores envolve normalmente
!transferência de arquivos e acesso a sistemas de arquivos remotos.

!O protocolo padrão utilizado pelo FTP Server é o TCP (Transmission Control Protocol) na porta padrão: 21
!o protocolo FTP também utiliza as portas TCP 20 (ftp-data) e TCP 990 (SFTP) Security FTP com suporte a SSL.

!HTTP (Hypertext Transfer Protocol) é um protocolo de comunicação utilizado nos sistemas de informação de
!hipermídia, distribuídos e colaborativos. Ele é a base para a comunicação de dados da Internet (World Wide Web).
!Por padrão o protocolo HTTP transfere dados em texto plano, sem criptografia.

!O protocolo padrão utilizado pelo HTTP Server é o TCP (Transmission Control Protocol) na porta padrão: 80

!HTTPS (Hyper Text Transfer Protocol Secure) é uma implementação do protocolo HTTP sobre uma camada adicional
!de segurança que utiliza os protocolos TLS/SSL. Essa camada adicional permite que os dados sejam transmitidos
!por meio de uma conexão criptografada e que se verifique a autenticidade do servidor e do cliente por meio
!de certificados digitais e unidade certificadoras.

!O protocolo padrão utilizado pelo HTTPS Server é o TCP (Transmission Control Protocol) na porta padrão: 443

!PRIMEIRA ETAPA: Configurações do Serviço de FTP Server no Cisco Packet Tracer:
!OBSERVAÇÃO: por padrão o Serviço de FTP Server no Cisco Packet Tracer está ligado
!OBSERVAÇÃO: diferente do TFTP o FTP trabalha com autenticação ou acesso anônimo (sem autenticação) e permissões
!de: Escrita, Leitura, Remoção, Renomear e Listar o conteúdo dos arquivos e diretórios.
Service       On
User Setup    Username: vaamonde	Password: vaamonde
              Write=Yes, Read=Yes, Delete=Yes, Rename=Yes, List=Yes
              Username: robson	Password: robson
              Write=No, Read=Yes, Delete=No, Rename=No, List=Yes

!SEGUNDA ETAPA: Configurações do Serviço de HTTP/HTTPS Server no Cisco Packet Tracer:
!OBSERVAÇÃO: por padrão o Serviço de HTTP/HTTPS Server no Cisco Packet Tracer está ligado
!OBSERVAÇÃO: recomendo acessar o site: https://www.w3schools.com/ para mais informações sobre o HTML
!DICA: para acessar páginas utilizando o Protocolo HTTPS, é necessário a configuração de um Certificado usando uma CA
!OBSERVAÇÃO: No Cisco Packet Tracer é limitado para as configurações da Unidade Certificadora CA e geração dos certificados
Service HTTP    On
Service HTTPS   On

!TERCEIRA ETAPA: Configuração de uma página HTML com nossas informações para testar o serviço HTTP e HTTPS
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
		<p><b><i><u>Curso de CCNAv7 Exame 200-301</u></i></b></p>
		</center>
	</body>
</html>

!Comandos básicos para testar o acesso ao FTP e HTTP/HTTPS

!PRIMEIRA ETAPA: testando localmente no servidor os serviços de rede
nslookup ftp.vaamonde.pti
ping ftp.vaamonde.pti

!ERRATA: no vídeo eu falo o nome do usuário vaamonde, mais utilizo o usuário robson, qualquer um dos dois usuários vai 
!funcionar no teste de acesso ao serviço do FTP

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