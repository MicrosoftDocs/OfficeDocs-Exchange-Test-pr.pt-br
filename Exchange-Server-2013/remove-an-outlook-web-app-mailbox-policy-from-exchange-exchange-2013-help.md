---
title: 'Remover uma política de caixa de correio do Outlook Web App do Exchange: Exchange 2013 Help'
TOCTitle: Remover uma política de caixa de correio do Outlook Web App do Exchange
ms:assetid: edab7bac-b62c-4b82-8f21-dcac77cf0e8f
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Dd351239(v=EXCHG.150)
ms:contentKeyID: 50486944
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Remover uma política de caixa de correio do Outlook Web App do Exchange

 

_**Aplica-se a:**Exchange Online, Exchange Server 2013_

_**Tópico modificado em:**2013-03-15_

Você pode remover uma política de caixa de correio MicrosoftOutlook Web App de uma organização Exchange usando o EAC ou o Shell.

Para tarefas de gerenciamento adicionais relacionadas às políticas de caixa de correio Outlook Web App, consulte [Diretivas de caixa de correio do Outlook Web App](outlook-web-app-mailbox-policies-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para finalizar cada procedimento: 3 minutos.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Políticas de caixa de correio do Outlook Web App", no tópico [Permissões de dispositivos móveis e clientes](clients-and-mobile-devices-permissions-exchange-2013-help.md).

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>..



## O que você deseja fazer?

## Usar o EAC para remover uma política de caixa de correio do Outlook Web App

1.  No EAC, clique em **Permissões** \> **Políticas do Outlook Web App**.

2.  No painel de resultados, clique para selecionar a política de caixa de correio que você deseja remover.

3.  Clique no botão **Excluir**.

4.  Na janela de confirmação, clique em **Sim** para remover a diretiva de caixa de correio ou clique em **não** para cancelar.

## Use o Shell para remover uma política de caixa de correio do Outlook Web App

Este exemplo remove uma diretiva de caixa de correio de Outlook Web App chamada `Policy1`.

    Remove-OwaMailboxPolicy -Name Policy1 

Para obter mais informações sobre sintaxe e parâmetros, consulte [Remove-OwaMailboxPolicy](https://technet.microsoft.com/pt-br/library/dd298103\(v=exchg.150\)).

## Como saber se funcionou?

Para verificar se você removeu com êxito uma política de caixa de correio Outlook Web App:

  - No EAC, clique em **permissões** \> **políticas de Outlook Web App**. A política que você removeu não é mais deve aparecer na lista.

