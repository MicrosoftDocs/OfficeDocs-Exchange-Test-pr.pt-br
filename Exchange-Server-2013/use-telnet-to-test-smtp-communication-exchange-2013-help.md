---
title: 'Usar Telnet para testar a comunicação SMTP: Exchange 2013 Help'
TOCTitle: Usar Telnet para testar a comunicação SMTP
ms:assetid: 8a5f6715-baa4-48dd-8600-02c6b3d1aa9d
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Bb123686(v=EXCHG.150)
ms:contentKeyID: 52058842
ms.date: 01/10/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Usar Telnet para testar a comunicação SMTP

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2016-12-09_

Este tópico explica como usar a Telnet para testar a comunicação SMTP entre servidores do sistema de mensagens. Por padrão, SMTP escuta na porta 25. Se você usa Telnet na porta 25, pode inserir os comandos SMTP que são usados para conectar a um servidor SMTP e enviar uma mensagem exatamente como se sua sessão Telnet fosse um servidor do sistema de mensagens SMTP. Você pode ver o sucesso ou a falha de cada etapa da conexão e do processo de envio de mensagens.

Aqui estão os cenários nos quais talvez você queira usar Telnet para testar a comunicação SMTP de ou para servidores de transporte existentes em sua organização do Microsoft Exchange:

  - Conectar ao servidor Exchange voltado à Internet da organização a partir de um host localizado fora da rede de perímetro e enviar uma mensagem de teste.

  - Conectar a um servidor de mensagens remoto a partir do servidor Exchange voltado à Internet da organização e enviar uma mensagem de teste.

O procedimento neste tópico mostra como usar o Cliente Telnet, que é um componente incluído no Microsoft Windows. Clientes Telnet de terceiros podem exigir uma sintaxe diferente daquela do componente de Telnet do Windows.

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: 30 minutos

  - Permissões do Exchange não se aplicam aos procedimentos neste tópico. Esses procedimentos são realizados no sistema operacional do Exchange Server ou em um computador cliente.

  - Os procedimentos deste tópico são melhor usados para conectar de e para servidores voltados à Internet que permitem conexões anônimas. A transmissão de mensagens entre servidores Exchange internos é criptografada e autenticada. Para usar Telnet para se conectar ao serviço de Transporte de Hub em um servidor de Caixa de Correio, é necessário criar um conector de Recebimento que esteja configurado para permitir acesso anônimo ou autenticação Básica para receber mensagens. Se o conector permitir autenticação Básica, você precisará de um utilitário para converter no formato Base64 as cadeias de caracteres de texto que são usadas para o nome de usuário e a senha. Como o nome de usuário e a senha são facilmente distinguíveis quando a autenticação Básica é usada, não recomendamos o uso da autenticação Básica sem criptografia.

  - Se você se conectar a um servidor de mensagens remoto, considere a execução dos procedimentos deste tópico em seu servidor Exchange voltado à Internet. Isso ajudará a evitar a rejeição da mensagem de teste pelos servidores de mensagens remotos que estão configurados para validar o endereço IP de origem, o nome de domínio de DNS correspondente e o endereço IP de pesquisa inversa de qualquer host da Internet que tentar enviar uma mensagem ao servidor.

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>.



## Como fazer isso?

## Etapa 1: instalar o Cliente Telnet no Windows

Por padrão, o Telnet Client não está instalado na maioria das versões de cliente ou servidor dos sistemas operacionais Microsoft Windows. Para instalá-lo, confira [Instalar cliente Telnet](https://go.microsoft.com/fwlink/p/?linkid=179054).

## Etapa 2: usar o Nslookup para localizar o FQDN ou o endereço IP no registro MX do servidor SMTP remoto

Para se conectar a um servidor SMTP de destino usando Telnet na porta 25, você deve usar o nome de domínio totalmente qualificado (FQDN) ou o endereço IP do servidor SMTP. Se o FQDN ou o endereço IP for desconhecido, a maneira mais fácil de localizar essas informações é usar a ferramenta de linha de comando Nslookup para localizar o registro MX do domínio de destino.

1.  No prompt de comando, digite **nslookup** e pressione Enter. Esse comando abre a sessão Nslookup.

2.  Digite **set type=mx** e pressione Enter.

3.  Digite **set timeout=20** e pressione Enter. Por padrão, os servidores de DNS do Windows têm um limite de tempo excedido de consulta do DNS recursivo de 15 segundos.

4.  Digite o nome do domínio do qual você deseja localizar o registro de MX. Por exemplo, para localizar o registro MX do domínio fabrikam.com, digite **fabrikam.com.** e pressione Enter.
    

    > [!NOTE]
    > O ponto à direita (<STRONG>.</STRONG>) indica um FQDN. O uso do ponto à direita impede que quaisquer sufixos de DNS padrão que estejam configurados para a sua rede sejam adicionados involuntariamente ao nome do domínio.

    
    A saída do comando se assemelhará à seguinte:
    
        fabrikam.com mx preference=10, mail exchanger = mail1.fabrikam.com
        fabrikam.com mx preference=20, mail exchanger = mail2.fabrikam.com
        mail1.fabrikam.com internet address = 192.168.1.10
        mail2 fabrikam.com internet address = 192.168.1.20
    
    Você pode usar qualquer um dos nomes de host ou endereços IP que estejam associados aos registros de MX como o servidor SMTP de destino. Um valor menor de preferência indica um servidor SMTP preferencial. Você pode usar vários registros de MX e valores diferentes de preferência para balanceamento de carga e tolerância a falhas.

5.  Quando estiver pronto para encerrar a sessão Nslookup, digite **exit** e pressione Enter.


> [!NOTE]
> O firewall ou as restrições de proxy da Internet que são impostas à rede interna da organização podem impedir o uso da ferramenta Nslookup para consultar servidores públicos de DNS na Internet.



## Etapa 3: usar Telnet na Porta 25 para testar a comunicação SMTP

Neste exemplo, os seguintes valores são usados:

  - **Servidor SMTP de destino**   mail1.fabrikam.com

  - **Domínio de origem**   contoso.com

  - **Endereço de email do remetente** chris@contoso.com

  - **Endereço de email do destinatário**   kate@fabrikam.com

  - **Assunto da mensagem**   Contoso Test

  - **Corpo da mensagem**   This is a test message


> [!NOTE]
> <UL>
> <LI>
> <P>Os comandos no Cliente Telnet não diferenciam maiúsculas de minúsculas. Os verbos do comando SMTP estão em maiúsculas por questões de clareza.</P>
> <LI>
> <P>Não é possível usar a tecla Backspace depois de conectar ao servidor SMTP de destino dentro da sessão Telnet. Se você cometer um erro ao digitar um comando SMTP, deverá pressionar Enter e digitar o comando novamente. Comandos SMTP não reconhecidos ou erros de sintaxe resultam em uma mensagem de erro semelhante à seguinte:</P><PRE><CODE>500 5.3.3 Unrecognized command</CODE></PRE></LI></UL>



1.  Em um prompt de comandos, digite **telnet** e pressione Enter. Esse comando abre a sessão Telnet.

2.  Digite **set localecho** e pressione Enter. Esse comando opcional permite visualizar os caracteres à medida que são digitados. Essa configuração pode ser necessária para alguns servidores SMTP.

3.  Digite **set logfile***\<filename\>*. Esse comando opcional permite fazer logon na sessão Telnet do arquivo de log especificado. Se você especificar apenas um nome de arquivo, o local do arquivo de log será o diretório de trabalho atual. Se você especificar um caminho e um nome de arquivo, o caminho deverá ser o local para o computador. O caminho e o nome do arquivo especificados devem ser inseridos no formato Microsoft DOS 8.3. O caminho especificado já deverá existir. Se você especificar um arquivo de log inexistente, ele será criado para você.

4.  Digite **open mail1.fabrikam.com 25** e pressione Enter.

5.  Digite **EHLO contoso.com** e pressione Enter.

6.  Digite **MAIL FROM:chris@contoso.com** e pressione Enter.

7.  Digite **RCPT TO:kate@fabrikam.com NOTIFY=success,failure** e pressione Enter. O comando opcional NOTIFY define as mensagens particulares de notificação de status de entrega que o servidor SMTP de destino deve fornecer ao remetente. Mensagens DSN são definidas no RFC 1891. Nesse caso, você está solicitando uma mensagem DSN sobre o êxito ou a falha da entrega da mensagem.

8.  Digite **DATA** e pressione Enter. Você receberá uma resposta semelhante à seguinte:
    
        354 Start mail input; end with <CLRF>.<CLRF>

9.  Digite **Subject: Test from Contoso** e pressione Enter.

10. Pressione Enter. O RFC 2822 exige uma linha em branco entre o campo de cabeçalho do `Subject:` e o corpo da mensagem.

11. Digite **This is a test message** e pressione Enter.

12. Pressione Enter, digite um ponto (**.**) e pressione Enter. Você receberá uma resposta semelhante à seguinte:
    
        250 2.6.0 <GUID> Queued mail for delivery

13. Para se desconectar do servidor SMTP de destino, digite **QUIT** e pressione Enter. Você receberá uma resposta semelhante à seguinte:
    
        221 2.0.0 Service closing transmission channel

14. Para finalizar a sessão Telnet, digite **quit** e pressione Enter.

## Etapa 4: avaliar os resultados da sessão Telnet

Esta seção fornece informações sobre as respostas que podem ser fornecidas para os seguintes comandos, que foram usados no exemplo anterior:

  - Open mail1.fabrikam.com 25

  - EHLO contoso.com

  - MAIL FROM:chris@contoso.com

  - RCPT TO:kate@fabrikam.com NOTIFY=success,failure
    

    > [!NOTE]
    > Os códigos de resposta SMTP de 3 dígitos que são definidos no RFC&nbsp;2821 são iguais para todos os servidores do sistema de mensagens SMTP. As descrições de texto podem ser ligeiramente diferentes em alguns dos servidores do sistema de mensagens SMTP.



## Open mail1.fabrikam.com 25

**Resposta bem-sucedida** `220 mail1.fabrikam.com Microsoft ESMTP MAIL Service ready at <day-date-time>`

**Falha na resposta** `Connecting to mail1.fabrikam.com...Could not open connection to the host, on port 25: Connect failed`

**Motivos possíveis para falha**

  - O serviço SMTP de destino não está disponível.

  - Há restrições no firewall de destino.

  - Há restrições no firewall de origem.

  - Um FQDN incorreto ou o endereço IP do servidor SMTP de destino foi especificado.

  - Um número de porta incorreto foi especificado.

## EHLO contoso.com

**Resposta bem-sucedida** `250 mail1.fabrikam.com Hello [<sourceIPaddress>]`

**Falha na resposta** `501 5.5.4 Invalid domain name`

**Possíveis motivos de falha**   Há caracteres inválidos no nome de domínio. Ou há restrições de conexão no servidor SMTP de destino.


> [!NOTE]
> EHLO é o verbo de Extended Simple Message Transfer Protocol (ESMTP, SMTP estendido), que é definido no RFC 2821. Servidores ESMTP podem anunciar seus recursos durante a conexão inicial. Esses recursos incluem o tamanho máximo da mensagem aceita e os métodos de autenticação suportados. HELO é o mais antigo verbo SMTP que está definido no RFC 821. A maioria dos servidores de mensagens SMTP suportam ESMTP e EHLO.



## MAIL FROM:chris@contoso.com

**Resposta bem-sucedida** `250 2.1.0 Sender OK`

**Falha na resposta** `550 5.1.7 Invalid address`

**Possíveis motivos de falha**   Há um erro de sintaxe no endereço de email do remetente.

**Falha na resposta** `530 5.7.1 Client was not authenticated`

**Possíveis motivos de falha**   O servidor de destino não aceita envios de mensagens anônimas. Você receberá esse erro se tentar usar Telnet para enviar uma mensagem diretamente para um servidor de Transporte de Hub.

## RCPT TO:kate@fabrikam.com NOTIFY=success,failure

**Resposta bem-sucedida** `250 2.1.5 Recipient OK`

**Falha na resposta** `550 5.1.1 User unknown`

**Possíveis motivos de falha**   O destinatário especificado não existe na organização.

