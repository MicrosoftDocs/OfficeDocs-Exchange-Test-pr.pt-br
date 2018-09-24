---
title: 'Iniciar e interromper os serviços de IMAP4: Exchange 2013 Help'
TOCTitle: Iniciar e interromper os serviços de IMAP4
ms:assetid: a52db4bd-69a6-47b2-acf3-d9d8571c7a87
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Bb124022(v=EXCHG.150)
ms:contentKeyID: 50486319
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Iniciar e interromper os serviços de IMAP4

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2012-10-05_

Por padrão, os dois serviços IMAP4, o serviço IMAP4 do Microsoft Exchange e o serviço de back-end do Microsoft Exchange IMAP4, não são iniciados em computadores que executam o MicrosoftExchange Server 2013. Você deve iniciar esses dois serviços para permitir que os clientes de email para se conectar ao Exchange usando o IMAP4. Quando estiver executando esses serviços, Exchange 2013 aceita comunicações com clientes IMAP4 desprotegidas na porta 143 e pela porta 993 usando Secure Sockets Layer (SSL).

O serviço Microsoft Exchange IMAP4 executa Exchange 2013 para computadores que executam a função de servidor acesso para cliente. O serviço de back-end do Microsoft Exchange IMAP4 é executado no computador Exchange 2013 que está executando a função de servidor de caixa de correio. Em ambientes onde as funções de servidor acesso para cliente e caixa de correio estão sendo executado no mesmo computador, você gerenciar ambos os serviços no mesmo computador.

Para mais informações relacionadas a POP3 e IMAP4, consulte [POP3 e IMAP4 no Exchange Server 2013](pop3-and-imap4-in-exchange-server-2013-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: 2 minutos.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Permissões de POP3 e IMAP4" no tópico [Permissões de dispositivos móveis e clientes](clients-and-mobile-devices-permissions-exchange-2013-help.md).

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>..



## O que você deseja fazer?

## Use o snap-in do Microsoft Management Console serviços para iniciar ou parar os serviços de IMAP4

Para iniciar os serviços de IMAP4:

1.  No computador que executa a função de servidor acesso para cliente, clique em **Iniciar**, aponte para **programas**, aponte para **Ferramentas administrativas** e, em seguida, clique em **Serviços**. Clique com o botão **IMAP4 do Microsoft Exchange** e, em seguida, clique em **Iniciar**.

2.  No computador que executa a função de servidor de caixa de correio, clique em **Iniciar**, aponte para **programas**, aponte para **Ferramentas administrativas** e, em seguida, clique em **Serviços**. Clique com o botão **Back-end do Microsoft Exchange IMAP4** e, em seguida, clique em **Iniciar**.

Para interromper os serviços IMAP4:

1.  No computador que executa a função de servidor acesso para cliente, clique em **Iniciar**, aponte para **programas**, aponte para **Ferramentas administrativas** e, em seguida, clique em **Serviços**. Clique com o botão **IMAP4 do Microsoft Exchange** e clique em **Parar**.

2.  No computador que executa a função de servidor de caixa de correio, clique em **Iniciar**, aponte para **programas**, aponte para **Ferramentas administrativas** e, em seguida, clique em **Serviços**. Clique com o botão **Back-end do Microsoft Exchange IMAP4** e clique em **Parar**.

## Usar o Shell para iniciar ou parar os serviços de IMAP4

Para iniciar os serviços de IMAP4:

1.  No computador que executa a função de servidor acesso para cliente, no Shell, execute o seguinte comando para iniciar o serviço IMAP4 do Microsoft Exchange.
    
    ```powershell
Start-service msExchangeIMAP4
```

2.  No computador que executa a função de servidor de caixa de correio, no Shell, execute o seguinte comando para iniciar o serviço de back-end do Microsoft Exchange IMAP4.
    
    ```powershell
Start-service msExchangeIMAP4BE
```

Para interromper os serviços IMAP4:

1.  No computador que executa a função de servidor acesso para cliente, no Shell, execute o seguinte comando para parar o serviço IMAP4 do Microsoft Exchange.
    
    ```powershell
Stop-service msExchangeIMAP4
```

2.  No computador que executa a função de servidor de caixa de correio, no Shell, execute o seguinte comando para parar o serviço de back-end do Microsoft Exchange IMAP4.
    
    ```powershell
Stop-service msExchangeIMAP4BE
```

## Use net start para iniciar ou interromper os serviços de IMAP4

Para iniciar os serviços de IMAP4:

1.  No computador que executa a função de servidor acesso para cliente, no prompt de comando, execute o seguinte comando para iniciar o serviço IMAP4 do Microsoft Exchange.
    
    ```powershell
net start msExchangeIMAP4
```

2.  No computador que executa a função de servidor de caixa de correio, no prompt de comando, execute o seguinte comando para iniciar o serviço de back-end do Microsoft Exchange IMAP4.
    
    ```powershell
net start msExchangeIMAP4BE
```

Para interromper os serviços IMAP4:

1.  No computador que executa a função de servidor acesso para cliente, no prompt de comando, execute o seguinte comando para parar o serviço IMAP4 do Microsoft Exchange.
    
    ```powershell
Net Stop MSExchangeIMAP4
```

2.  No computador que executa a função de servidor de caixa de correio, no prompt de comando, execute o seguinte comando para parar o serviço de back-end do Microsoft Exchange IMAP4.
    
    ```powershell
Net Stop MSExchangeIMAP4BE
```

## Como saber se funcionou?

1.  No servidor de acesso para cliente do Exchange, abra o Gerenciador de tarefas do Windows. Na guia **Serviços**, o status de **MSExchangeIMAP4** mostrará como **Running** se o serviço Microsoft Exchange IMAP4 estiver em execução.

2.  No servidor de caixa de correio Exchange, abra o Gerenciador de tarefas do Windows. Na guia **Serviços**, o status de **MSExchangeIMAP4BE** mostrará como **Running** se o serviço de back-end do Microsoft Exchange IMAP4 estiver em execução.

