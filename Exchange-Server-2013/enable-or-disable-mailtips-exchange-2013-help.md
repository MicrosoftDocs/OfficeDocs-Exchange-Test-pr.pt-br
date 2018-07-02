---
title: 'Ativar ou desativar dicas de email: Exchange 2013 Help'
TOCTitle: Ativar ou desativar dicas de email
ms:assetid: 11ad3848-f303-4ad5-a21d-9b0883db4bda
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/JJ649321(v=EXCHG.150)
ms:contentKeyID: 50485048
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Ativar ou desativar dicas de email

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2015-04-08_

É possível usar o Shell de Gerenciamento do Exchange para definir várias configurações sobre a forma como o MailTips será usado em sua organização.

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: 5 minutos

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Dicas de Email" no tópico [Permissões de fluxo de email](mail-flow-permissions-exchange-2013-help.md).

  - Você só pode usar o Shell para executar esse procedimento.

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>.



## Usar o Shell para habilitar ou desabilitar MailTips

Use o cmdlet **Set-OrganizationConfig** para habilitar ou desabilitar o MailTips em sua organização. As Dicas de Email são habilitadas por padrão, quando você instala uma nova organização do Exchange. Este exemplo mostra como habilitar MailTips em sua organização.

    Set-OrganizationConfig -MailTipsAllTipsEnabled $true

Para informações detalhadas de sintaxes e de parâmetros, consulte [Set-OrganizationConfig](https://technet.microsoft.com/pt-br/library/aa997443\(v=exchg.150\)).

