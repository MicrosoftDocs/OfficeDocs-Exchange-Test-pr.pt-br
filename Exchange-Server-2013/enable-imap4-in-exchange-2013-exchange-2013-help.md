---
title: 'Habilitar IMAP4 no Exchange 2013: Exchange 2013 Help'
TOCTitle: Habilitar IMAP4
ms:assetid: c1ae10dd-14da-4400-b38d-2aeafde8abe6
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Bb124489(v=EXCHG.150)
ms:contentKeyID: 50486555
ms.date: 01/10/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Habilitar IMAP4 no Exchange 2013

 

_**Aplica-se a:**Exchange Server 2013_

_**Tópico modificado em:**2016-06-02_

Saiba como habilitar a conectividade do cliente de IMAP4 no Exchange 2016 usando o Console de Gerenciamento Microsoft (MMC) ou o Shell de Gerenciamento do Exchange (EMS).

Ao instalar o Exchange Server 2016, a conectividade do cliente de IMAP4 não é habilitada. Para habilitar a conectividade do cliente IMAP4, é necessário iniciar dois serviços IMAP, o serviço IMAP4 do Microsoft Exchange e o serviço de back-end do IMAP4 do Microsoft Exchange. Após habilitar o IMAP4, o Exchange 2016 aceita comunicações com clientes IMAP4 desprotegidas na porta 143 e pela porta 993 usando SSL (Secure Sockets Layer).

Gerencie serviços IMAP4 e IMAP4 Backend no mesmo computador do Exchange 2016 que executa a função de servidor de Caixa de Correio. No Exchange 2016, os serviços de Acesso para Cliente fazem parte da função de servidor de Caixa de Correio, para que você não precise mais gerenciar os serviços separadamente.

Para saber mais sobre como configurar POP3 e IMAP4, confira [POP3 e IMAP4 no Exchange Server 2013](pop3-and-imap4-in-exchange-server-2013-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: 2 minutos.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Seção "Permissões de POP3 e IMAP4" no tópico [Permissões de dispositivos móveis e clientes](clients-and-mobile-devices-permissions-exchange-2013-help.md).

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>.



## O que você deseja fazer?

## Usar o Console de Gerenciamento Microsoft (MMC) para habilitar IMAP4

No computador que executa a função de servidor de Caixa de Correio:

1.  No snap-in **Serviços**, na árvore do console, clique em **Serviços (Local)**.

2.  No painel de resultados, clique com o botão direito do mouse em **Microsoft Exchange IMAP4** e, em seguida, clique em **Propriedades**.

3.  No painel de resultados, clique com o botão direito do mouse em **Back-end do IMAP4 do Microsoft Exchange** e, em seguida, clique em **Propriedades**.

4.  Na guia **Geral**, em **Tipo de inicialização**, selecione **Automática** e clique em **Aplicar**.

5.  Em **Status do Serviço**, clique em **Iniciar** e em **OK**.

## Usar o Shell de Gerenciamento do Exchangepara habilitar IMAP4

No computador que executa a função de servidor de Caixa de Correio:

1.  Defina o serviço IMAP4 do Microsoft Exchange para iniciar automaticamente.
    
        Set-service msExchangeIMAP4 -startuptype automatic

2.  Inicie o serviço IMAP4 do Microsoft Exchange.
    
        Start-service msExchangeIMAP4

3.  Defina o serviço de Back-end do IMAP4 do Microsoft Exchange para iniciar automaticamente.
    
        Set-service msExchangeIMAP4BE -startuptype automatic

4.  Inicie o serviço de Back-end do IMAP4 do Microsoft Exchange.
    
        Start-service msExchangeIMAP4BE

## Como saber se funcionou?

No servidor de Caixa de Correio do Exchange 2016, abra o Gerenciador de Tarefas do Windows. Na guia **Serviços**, o status de **MSExchangeIMAP4** e **MSExchangeIMAP4BE**será exibido como **Em execução** se IMAP4 for habilitado.

