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

!DNSv4 (Domain Name System) é um sistema hierárquico e distribuído de gestão de nomes para computadores, 
!serviços ou qualquer máquina conectada à Internet ou a uma rede privada. Utilizado principalmente para 
!fazer as resoluções de nomes para endereços IPv4 ou IPv6.

!O protocolo padrão utilizado pelo DNS Server é o UDP (User Datagram Protocol) na porta padrão: 53
!utilizada principalmente pelo cliente para fazer as consultas de Nomes para IP ou IP para Nomes.

!OBSERVAÇÃO: O DNS Server também utiliza o TCP (Transmission Control Protocol) na porta padrão: 53
!utilizado para receber a transferência de Zonas entre o Servidor Master (Mestre) é o Slaver (Escravo) 
!OBSERVAÇÃO: O DNS Server também utiliza o TCP (Transmission Control Protocol) na porta padrão: 953 
!utilizado pelo serviço do RNDC (Remote Name Daemon Control).

!Zona de Pesquisa Direta: resolução de Nome para endereço IPv4 ou IPv6.
!Zona de Pesquisa Inversa/Reversa: resolução de endereço IPv4 ou IPv6 para Nome.

!Registros DNS: Os registros DNS são mapeamentos de arquivos ou sistemas que dizem a um servidor DNS 
!para qual endereço IP um determinado domínio está associado. Também informa aos servidores DNS como 
!lidar com as solicitações que estão sendo enviadas para cada nome de domínio.

!Sintaxe DNS: Diferentes sequências de letras são usadas para ditar as ações do servidor DNS. Essas 
!letras são chamadas de sintaxe DNS (Exemplo: A, AAAA, CNAME, MX, PTR, NS, SOA, SRV, TXT, etc).

!Registro Tipo A: Significa Endereço e é o tipo mais básico de sintaxe DNS. Indica o endereço IP real para um domínio.
!Registro Tipo CNAME: Significa o Nome Canônico e seu papel é fazer que um domínio use um alias de outro domínio.
!Registro Tipo SOA: Significa Início de Autoridade. Obviamente é um dos registros de DNS mais importantes.
!Registro Tipo NS: Significa Name Server ele indica qual nome de servidor é autoritativo para o domínio.

!Configurações do Serviço de DNS Server no Cisco Packet Tracer:
!OBSERVAÇÃO: por padrão o Serviço de DNS Server no Cisco Packet Tracer está desligado
!OBSERVAÇÃO: no Cisco Packet Tracer as configuração de Sintaxe são limitadas somente ao tipos: A, CNAME, SOA e NS.
!OBSERVAÇÃO: no Cisco Packet Tracer temos apenas a configuração da Zona de Pesquisa Direta

!ERRATA: correção do nome do NS para: ns1.vaamonde.pti e correção do Server Name para: server-02
!ERRATA: correção do nome do SOA do Server Name para: ns1.vaamonde.pti
!ERRATA: no vídeo os registros dos Switch e Router foram criados com o Tipo: CNAME, correto é: A Record

DNS Service:       On
Resource Records:  Name = server-02            Type = A Record     Address = 192.168.3.1
Resource Records:  Name = ns1.vaamonde.pti     Type = NS           Server Name = server-02
Resource Records:  Name = vaamonde.pti         Type = SOA          Primary Server Name = ns1.vaamonde.pti
                                                                   Mail Box = vaamonde@vaamonde.pti
                                                                   Minimum TTL = 3600 (1h ou 60 minutos)
                                                                   Refresh Time = 3600 (1h ou 60 minutos)
                                                                   Retry Time = 600 (10 minutos)
                                                                   Expiry Time = 86400 (24h ou 1440 minutos)
Resource Records:  Name = vaamonde.pti         Type = CNAME        Host Name = server-02
Resource Records:  Name = www.vaamonde.pti     Type = CNAME        Host Name = server-02
Resource Records:  Name = pop3.vaamonde.pti    Type = CNAME        Host Name = server-02
Resource Records:  Name = smtp.vaamonde.pti    Type = CNAME        Host Name = server-02
Resource Records:  Name = ftp.vaamonde.pti     Type = CNAME        Host Name = server-02
Resource Records:  Name = tftp.vaamonde.pti    Type = CNAME        Host Name = server-02
Resource Records:  Name = ntp.vaamonde.pti     Type = CNAME        Host Name = server-02
Resource Records:  Name = log.vaamonde.pti     Type = CNAME        Host Name = server-02
Resource Records:  Name = sw-l2-2960-3         Type = A Record     Address = 192.168.3.250
Resource Records:  Name = sw-l2-2960-4         Type = A Record     Address = 192.168.3.251
Resource Records:  Name = sw-l3-3560-1         Type = A Record     Address = 192.168.3.252
Resource Records:  Name = rt-1941-2            Type = A Record     Address = 192.168.2.254

!Comandos básicos de consulta de resoluções de nomes DNS no Microsoft Windows
ipconfig
ipconfig /all
nslookup server-02
nslookup vaamonde.pti
ping vaamonde.pti