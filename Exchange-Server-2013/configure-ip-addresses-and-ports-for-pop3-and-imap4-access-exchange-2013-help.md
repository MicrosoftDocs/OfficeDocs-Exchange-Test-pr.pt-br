---
title: 'Configurar endereços IP e portas para acesso POP3 e IMAP4: Exchange 2013 Help'
TOCTitle: Configurar endereços IP e portas para acesso de POP3 e IMAP4
ms:assetid: 8292747b-6626-4d7f-ba73-1e17f5d99fa4
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Bb123530(v=EXCHG.150)
ms:contentKeyID: 50556235
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configurar endereços IP e portas para acesso de POP3 e IMAP4

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2012-11-28_

Você pode usar o EAC e o Shell para configurar o Microsoft Exchange POP3 e IMAP4 serviços usar endereços IP e portas diferentes das configurações padrão.


> [!TIP]
> Digite os endereços IP e intervalos de endereços IP no formato de protocolo IP versão 4 (IPv4), o formato de Internet Protocol versão 6 (IPv6) ou ambos os formatos. Uma instalação padrão do Windows Server 2008 habilita o suporte para IPv4 e IPv6.



Para mais informações relacionadas a POP3 e IMAP4, consulte [POP3 e IMAP4 no Exchange Server 2013](pop3-and-imap4-in-exchange-server-2013-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para concluir cada procedimento: 5 minutos.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "configurações de POP3" e "configurações de IMAP4" no tópico [Permissões de dispositivos móveis e clientes](clients-and-mobile-devices-permissions-exchange-2013-help.md).

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>..



## O que você deseja fazer?

## Configurar portas e endereços IP para POP3

## Use o EAC para configurar as portas e endereços IP de POP3

1.  No EAC, navegue até **Servidores** **\>Servidores**.

2.  Na lista de servidores, selecione o servidor de Acesso para Cliente e clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").

3.  Na página de propriedades do servidor, clique em **POP3**.

4.  Em **TLS ou conexões sem criptografia**, clique em **Adicionar**![Ícone Adicionar](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Ícone Adicionar").

5.  Na página **endereço IP adicionar**, em **endereço IP**, escolha uma das seguintes opções:
    
      - **Todos os endereços IPv4 disponíveis**    Use todos os endereços IP IPv4 disponíveis para um servidor.
    
      - **Todos os endereços IPv6 disponíveis**    Use todos os endereços IP IPv6 disponíveis para um servidor.
    
      - **Especificar um endereço IP**    Use um endereço IP específico.

6.  Em **porta**, insira um número de porta ou aceite a porta padrão.

7.  Clique em **Salvar** para salvar suas alterações.

Depois de definir as configurações de porta e endereço IP para POP3, você deve reiniciar o serviço POP3 para que as configurações entrem em vigor. Para obter informações sobre como reiniciar o serviço POP3, consulte [Iniciar e interromper os serviços POP3](start-and-stop-the-pop3-services-exchange-2013-help.md).

## Use o Shell para configurar as portas e endereços IP para POP3

Este exemplo define o endereço IP e porta de comunicação com Exchange usando POP3 com o Secure Sockets Layer (SSL).

    Set-PopSettings -SSLBindings: IPaddress:Port

Este exemplo define o endereço IP e porta de comunicação com Exchange usando POP3 sem criptografia ou a criptografia de segurança de camada de transporte (TLS).

    Set-PopSettings -UnencryptedOrTLSBindings IPaddress:Port

Depois de definir as configurações de porta e endereço IP para POP3, você deve reiniciar o serviço POP3 para que as configurações entrem em vigor. Para obter informações sobre como reiniciar o serviço POP3, consulte [Iniciar e interromper os serviços POP3](start-and-stop-the-pop3-services-exchange-2013-help.md).

Para obter mais informações sobre sintaxe e parâmetros, consulte [Set-PopSettings](https://technet.microsoft.com/pt-br/library/aa997154\(v=exchg.150\)).

## Como saber se funcionou?

Faça o seguinte para verificar que você alterou as configurações de porta e endereço de IP de POP3 em um servidor.

1.  Execute o seguinte comando no Shell.
    
        Get-PopSettings | format-list

2.  Verifique se que as configurações de *UnencryptedOrTLSBindings* e *SSLBindings* estão corretas.

## Configurar portas e endereços IP para o IMAP4

## Usar o EAC para configurar as portas e endereços IP para o IMAP4

1.  No EAC, navegue até **Servidores** **\>Servidores**.

2.  Na lista de servidores, selecione o servidor de Acesso para Cliente e clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").

3.  Na página de propriedades do servidor, clique em **IMAP4**.

4.  Se você deseja definir o TLS ou configurações de conexão não criptografada, em **TLS ou conexões sem criptografia**, clique em **Adicionar**![Ícone Adicionar](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Ícone Adicionar"). Se você deseja alterar as configurações de conexão de Secure Sockets Layer (SSL), em **conexões de Secure Sockets Layer (SSL)**, clique em **Adicionar**![Ícone Adicionar](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Ícone Adicionar").

5.  Na página **endereço IP adicionar**, em **endereço IP**, escolha uma das seguintes opções:
    
      - **Todos os endereços IPv4 disponíveis**    Use todos os endereços IP IPv4 disponíveis para um servidor.
    
      - **Todos os endereços IPv6 disponíveis**    Use todos os endereços IP IPv6 disponíveis para um servidor.
    
      - **Especificar um endereço IP**    Use um endereço IP específico.

6.  Em **porta**, insira um número de porta ou aceite a porta padrão.

7.  Clique em **Salvar** para salvar suas alterações.

Depois de definir as configurações de porta e endereço IP para o IMAP4, você deve reiniciar os serviços IMAP4 para que as configurações entrem em vigor. Para obter informações sobre como reiniciar os serviços IMAP4, consulte [Iniciar e interromper os serviços de IMAP4](start-and-stop-the-imap4-services-exchange-2013-help.md).

## Use o Shell para configurar as portas e endereços IP para o IMAP4

Este exemplo define o endereço IP e porta de comunicação com Exchange usando IMAP4.

    Set-ImapSettings -SSLBindings: IPaddress:Port

Este exemplo define o endereço IP e porta de comunicação com Exchange usando IMAP4 sem criptografia ou a criptografia TLS.

    Set-ImapSettings -UnencryptedOrTLSBindings IPaddress:Port 

Depois de definir as configurações de porta e endereço IP para o IMAP4, você deve reiniciar o serviço IMAP4 para que as configurações entrem em vigor. Para obter informações sobre como reiniciar o serviço IMAP4, consulte [Iniciar e interromper os serviços de IMAP4](start-and-stop-the-imap4-services-exchange-2013-help.md).

Para obter mais informações sobre sintaxe e parâmetros, consulte [Set-ImapSettings](https://technet.microsoft.com/pt-br/library/aa998252\(v=exchg.150\)).

## Como saber se funcionou?

Faça o seguinte para verificar que você alterou as configurações de porta e endereço de IP de IMAP4 em um servidor.

1.  Execute o seguinte comando no Shell.
    
        Get-ImapSettings | format-list

2.  Verifique se que as configurações de *UnencryptedOrTLSBindings* e *SSLBindings* estão corretas.

## Para obter mais informações

Depois de configurar portas e endereços IP para POP3 e IMAP4, você também pode querer:

[Habilitar IMAP4 no Exchange 2013](enable-imap4-in-exchange-2013-exchange-2013-help.md)

[Habilitar POP3 no Exchange 2013](enable-pop3-in-exchange-2013-exchange-2013-help.md)

