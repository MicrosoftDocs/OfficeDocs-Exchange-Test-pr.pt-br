---
title: 'Ignorar um log de auditoria de caixa de correio: Exchange 2013 Help'
TOCTitle: Bypass de um usuário da conta de auditoria de caixa de correio log
ms:assetid: 98a87071-fe31-4b67-beb8-a73799e54df2
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Ff461934(v=EXCHG.150)
ms:contentKeyID: 50486241
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Bypass de um usuário da conta de auditoria de caixa de correio log

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2013-05-21_

Quando você habilita uma caixa de correio do log de auditoria de caixa de correio, os eventos de acesso de caixa de correio especificada (por exemplo, como acessar uma pasta ou uma mensagem ou excluir permanentemente uma mensagem) serão registrados. No entanto, o acesso por alguns autorizado contas, como contas usadas por ferramentas de terceiros ou as contas usadas para monitoramento dentro da lei, pode criar um grande número de auditoria de caixa de correio entradas de log e não podem ser de interesse para sua organização.

Você pode configurar uma conta de usuário ou de computador para ignorar o log de auditoria de caixa de correio, portanto ações tomadas por essa conta de usuário ou de qualquer caixa de correio não são registradas. Ignorando as contas de computador que precisam de acesso freqüente para caixas de correio ou de usuário confiável, você pode reduzir o ruído nos logs de auditoria de caixa de correio.


> [!CAUTION]
> Se você usar o log de auditoria de caixa de correio para auditar ações e acesso de caixa de correio, você deve monitorar as associações de bypass de auditoria de caixa de correio em intervalos regulares. Se a associação de desvio de uma auditoria de caixa de correio é adicionada para uma conta, a conta pode acessar qualquer caixa de correio na organização à qual ela recebeu permissões, sem qualquer entradas de log de auditoria de caixa de correio que está sendo geradas para esse tipo de acesso ou quaisquer ações tomadas (por exemplo, exclusões de mensagem).



Para tarefas de gerenciamento adicionais relacionadas ao log de auditoria de caixa de correio, consulte [Procedimentos de registro em log de auditoria de caixa de correio](mailbox-audit-logging-procedures-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: 1 minuto.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Log de auditoria de caixas de correio" no tópico [Permissões de política e conformidade de mensagens](messaging-policy-and-compliance-permissions-exchange-2013-help.md).

  - Quando uma conta está configurada para o desvio de log de auditoria de caixa de correio, acesso a qualquer caixa de correio por essa conta não estar conectado. Você não pode configurar uma conta para ignorar o registro de acesso a uma caixa de correio específica.

  - Você não pode usar o Centro de administração do Exchange (EAC) para habilitar ou desabilitar o desvio de mídia para uma conta do log de auditoria de caixa de correio. Você deve usar o Shell.

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>.



## Usar o Shell para habilitar ou desabilitar o desvio do log de auditoria de caixa de correio para uma conta

Para obter um exemplo de como habilitar o desvio de mídia para uma conta do log de auditoria de caixa de correio, consulte o [Examples](https://technet.microsoft.com/pt-br/ff696758\(exchg.150\)#examples) na [Set-MailboxAuditBypassAssociation](https://technet.microsoft.com/pt-br/library/ff696758\(v=exchg.150\)).

Para obter um exemplo de como desabilitar o desvio de mídia para uma conta do log de auditoria de caixa de correio, consulte o [Examples](https://technet.microsoft.com/pt-br/ff696758\(exchg.150\)#examples) na [Set-MailboxAuditBypassAssociation](https://technet.microsoft.com/pt-br/library/ff696758\(v=exchg.150\)).

## Como saber se funcionou?

Depois de você ter desviada do log de auditoria de caixa de correio de uma conta de usuário, você pode verificar as definições de desvio, executando o cmdlet [Get-MailboxAuditBypassAssociation](https://technet.microsoft.com/pt-br/library/ff696741\(v=exchg.150\)) .

Para obter exemplos de como verificar a auditoria de caixa de correio bypass associações, consulte [Examples](https://technet.microsoft.com/pt-br/ff696741\(exchg.150\)#examples) na [Get-MailboxAuditBypassAssociation](https://technet.microsoft.com/pt-br/library/ff696741\(v=exchg.150\)).

