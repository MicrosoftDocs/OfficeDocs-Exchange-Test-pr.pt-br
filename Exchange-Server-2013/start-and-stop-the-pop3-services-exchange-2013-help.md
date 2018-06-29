---
title: 'Iniciar e interromper os serviços POP3: Exchange 2013 Help'
TOCTitle: Iniciar e interromper os serviços POP3
ms:assetid: 3d543921-d8c9-4d4b-99a1-82446b585ceb
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Aa997475(v=EXCHG.150)
ms:contentKeyID: 50485363
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Iniciar e interromper os serviços POP3

 

_**Aplica-se a:**Exchange Server 2013_

_**Tópico modificado em:**2013-03-13_

Por padrão, os dois serviços POP3, o serviço POP3 do Microsoft Exchange e o serviço de backend do POP3 do Microsoft Exchange, não são iniciados em computadores com o MicrosoftExchange Server 2013. Você deve iniciar esses dois serviços, para permitir que seus clientes de email se conectem ao Exchange usando POP3. Com esses serviços em execução, o Exchange 2013 aceita comunicações com clientes POP3 desprotegidas na porta 110 e pela porta 995 usando SSL (Secure Sockets Layer).

O serviço POP3 do Microsoft Exchange funciona em computadores com o Exchange 2013 que estejam executando a função de servidor Acesso para Cliente. O serviço de backend do POP3 do Microsoft Exchange funciona no computador com o Exchange 2013 que esteja executando a função de servidor Caixa de Correio. Em ambientes em que as funções de Acesso para Cliente e Caixa de Correio estejam sendo executadas no mesmo computador, você gerencia ambos os serviços no mesmo computador.

Para mais informações relacionadas a POP3 e IMAP4, consulte [POP3 e IMAP4 no Exchange Server 2013](pop3-and-imap4-in-exchange-server-2013-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: 2 minutos.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Permissões de POP3 e IMAP4" no tópico [Permissões de dispositivos móveis e clientes](clients-and-mobile-devices-permissions-exchange-2013-help.md).

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>..



## O que você deseja fazer?

## Usar os serviços do Console de Gerenciamento Microsoft para iniciar e parar o serviço POP3

Para iniciar os serviços POP3:

1.  No computador com a função de servidor Acesso para Cliente, clique em **Iniciar**, aponte para **Programas**, **Ferramentas Administrativas** e clique em **Serviços**. Clique com o botão direito em **POP3 do Microsoft Exchange** e clique em **Iniciar**.

2.  No computador com a função de servidor Caixa de Correio, clique em **Iniciar**, aponte para **Programas**, **Ferramentas Administrativas** e clique em **Serviços**. No painel de resultados, clique com o botão direito em **Backend do POP3 do Microsoft Exchange** e clique em **Iniciar**.

Para interromper os serviços POP3:

1.  No computador com a função de servidor Acesso para Cliente, clique em **Iniciar**, aponte para **Programas**, **Ferramentas Administrativas** e clique em **Serviços**. Clique com o botão direito em **POP3 do Microsoft Exchange** e clique em **Parar**.

2.  No computador com a função de servidor Caixa de Correio, clique em **Iniciar**, aponte para **Programas**, **Ferramentas Administrativas** e clique em **Serviços**. Clique com o botão direito em **Backend do POP3 do Microsoft Exchange** e clique em **Parar**.

## Usar o Shell para iniciar ou parar os serviços POP3

Para iniciar os serviços POP3:

1.  No computador com a função de servidor Acesso para Cliente, execute, usando o Shell, o seguinte comando, para iniciar o serviço do POP3 do Microsoft Exchange.
    
        Start-service MSExchangePOP3

2.  No computador com a função de servidor Caixa de Correio, execute, usando o Shell, o seguinte comando, para iniciar o serviço do Backend do POP3 do Microsoft Exchange.
    
        Start-service MSExchangePOP3BE

Para interromper os serviços POP3:

1.  No computador com a função de servidor Acesso para Cliente, execute, usando o Shell, o seguinte comando, para interromper o serviço do POP3 do Microsoft Exchange.
    
        Stop-service MSExchangePOP3

2.  No computador com a função de servidor Caixa de Correio, execute, usando o Shell, o seguinte comando, para interromper o serviço do Backend do POP3 do Microsoft Exchange.
    
        Stop-service MSExchangePOP3BE

## Usar o net start para iniciar ou parar os serviços POP3

Para iniciar os serviços POP3:

1.  No computador com a função de servidor Acesso para Cliente, execute, no prompt de comando, o seguinte comando, para iniciar o serviço do POP3 do Microsoft Exchange.
    
        Net Start msExchangePOP3

2.  No computador com a função de servidor Acesso para Cliente, execute, no prompt de comando, o seguinte comando, para iniciar o serviço do Backend do POP3 do Microsoft Exchange.
    
        Net Start msExchangePOP3BE

Para interromper os serviços POP3:

1.  No computador com a função de servidor Acesso para Cliente, execute, no prompt de comando, o seguinte comando, para interromper o serviço do POP3 do Microsoft Exchange.
    
        Net Stop MSExchangePOP3

2.  No computador com a função de servidor Acesso para Cliente, execute, no prompt de comando, o seguinte comando, para interromper o serviço do Backend do POP3 do Microsoft Exchange.
    
        Net Stop MSExchangePOP3BE

## Como saber se funcionou?

1.  No servidor de Acesso para Cliente do Exchange, abra o Gerenciador de Tarefas do Windows. Na guia **Serviços**, o status de **MSExchangePOP3** irá aparecer como **Em execução**, se o serviço do POP3 do Microsoft Exchange estiver em execução.

2.  No servidor de caixa de correio do Exchange, abra o Gerenciador de Tarefas do Windows. Na guia **Serviços**, o status de **MSExchangePOP3BE** irá aparecer como **Em execução**, se o serviço do Backend do POP3 do Microsoft Exchange estiver em execução.

