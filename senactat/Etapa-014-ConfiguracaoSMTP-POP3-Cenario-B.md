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

!SMTP (Simple Mail Transfer Protocol) é o protocolo padrão de envio de mensagens de correio eletrônico (e-mail)
!através da Internet entre dois dispositivos computacionais (computadores, smartphone, etc), definido na RFC 821.

!O protocolo padrão utilizado pelo SMTP Server é o TCP (Transmission Control Protocol) na porta padrão: 25
!OBSERVAÇÃO: desde 01/01/2013 o CGI.br solicitou o bloqueio do envio de e-mails utilizando a porta padrão: 25 
!OBSERVAÇÃO: atualmente a porta utilizada pelo SMTP é a: TCP 587, essa mudança tem o foco na diminuição de SPAM
!DICA: a porta 587 utiliza TLS (segurança) já a porta 465 utiliza SSL (segurança) mais foi considera depreciada (desuso)
!ERRATA: no vídeo eu falo: 01/01/2003 o correto é: 01/01/2013

!POP3 (Post Office Protocol) é um protocolo utilizado no acesso remoto a um servidor de correio eletrônico (e-mail), 
!definido no RFC 1939, que permite que todas as mensagens contidas em uma caixa de correio eletrônico possam
!ser transferidas sequencialmente para um software cliente de e-mail em outro dispositivo.

!O protocolo padrão utilizado pelo POP3 é o TCP (Transmission Control Protocol) na porta padrão: 110
!DICA: a porta: TCP 995 utiliza TLS/SSL (segurança) ela também é conhecida como POP3S

!IMAP (Internet Message Access Protocol) é um protocolo de gerenciamento de correio eletrônico (e-mail). O mais 
!interessante é que as mensagens ficam armazenadas no servidor de hospedagem de e-mail. Trabalhando com
!sincronismo entre a caixa postal é o cliente de e-mail.

!O protocolo padrão utilizado pelo IMAP é o TCP (Transmission Control Protocol) na porta padrão: 143
!DICA: a porta: TCP 993 utiliza TLS/SSL (segurança) ela também é conhecida como IMAPS

!MAPI (Messaging API) é um protocolo proprietário desenvolvido pela Microsoft. Ele é usado como interface de
!comunicação entre as aplicações e o servidor Microsoft Exchange.

!O protocolo MAPI utiliza um conjunto de protocolos TCP (Transmission Control Protocol) nas portas:
!80 (HTTP), 443 (HTTPS), 143 (IMAP), 993 (IMAPS), 110 (POP3), 995 (POP3S) é 587 (SMTP) 

!PRIMEIRA ETAPA: Configurações do Serviço de SMTP e POP3 Server no Cisco Packet Tracer:
!OBSERVAÇÃO: por padrão o Serviço de SMTP e POP3 no Cisco Packet Tracer está ligado
!DICA: em servidores de e-mail geralmente no Servidor de DNS é feito a criação do Registro MX (Mail Exchanger Record)
!DICA: nesse servidor também é criado os arquivos do Tipo TXT com informações de Black List (Sender Policy Framework)
!OBSERVAÇÃO: esses recursos de e-mail avançado são limitados no Cisco Packet Tracer. 

SMTP Service        On
POP3 Service        On
Domain Name         vaamonde.pti     SET
User Setup          User: robsonvaamonde    Password: 123456    (+)     Email: robsonvaamonde@vaamonde.pti
                    User: leandroramos      Password: 123456    (+)     Email: leandroramos@vaamonde.pti
                    User: josedeassis       Password: 123456    (+)     Email: josedeassis@vaamonde.pti
                    User: jeffersoncosta    Password: 123456    (+)     Email: jeffersoncosta@vaamonde.pti
                    User: rogeriosampaio    Password: 123456    (+)     Email: rogeriosampaio@vaamonde.pti
                    User: sirlenesanches    Password: 123456    (+)     Email: sirlenesanches@vaamonde.pti
                    User: denisnovais       Password: 123456    (+)     Email: denisnovais@vaamonde.pti
                    User: vaamonde          Password: 123456    (+)     Email: vaamonde@vaamonde.pti

!SEGUNDA ETAPA: Configurações do Clientes de SMTP e POP3 no Cisco Packet Tracer
!DICA: o principal cliente de e-mail utilizado hoje em dia no mercado corporativo é o: Microsoft Outlook
!OBSERVAÇÃO: existe outros clientes de e-mail como: Thunderbid, Evolution, SeaMonkey, eM Client, etc
!OBSERVAÇÃO: não confundir Cliente de Email com Webmail, nesse caso o acesso e feito via Navegador

!Testando as resoluções de nome do SMTP e POP3
nslookup smtp.vaamonde.pti
nsllokup pop3.vaamonde.pti

!Configurando o cliente de email
Configure Mail
Your Name               Admin SOA
Email Address           vaamonde@vaamonde.pti

Server Information
Incoming Mail Server    pop3.vaamonde.pti
Outgoing Mail Server    smtp.vaamonde.pti

Logon Information
User Name               vaamonde
Password                123456
(SAVE)