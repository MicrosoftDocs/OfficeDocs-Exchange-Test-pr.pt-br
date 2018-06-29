---
title: 'Pesquisar o log de auditoria de caixa de correio para uma caixa de correio: Exchange 2013 Help'
TOCTitle: Pesquisar o log de auditoria de caixa de correio para uma caixa de correio
ms:assetid: 5b518a08-3b51-4ba3-bfbd-0e35cc5ff374
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Ff461930(v=EXCHG.150)
ms:contentKeyID: 50485660
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Pesquisar o log de auditoria de caixa de correio para uma caixa de correio

 

_**Aplica-se a:**Exchange Server 2013_

_**Tópico modificado em:**2012-10-03_

Você pode pesquisar em sincronia as entradas de log de auditoria de caixa de correio para uma caixa de correio e visualizar os resultados da pesquisa no Shell.

Se você deseja pesquisar logs de auditoria de caixa de correio de várias caixas de correio e enviar os resultados por email para um endereço específico, você deve criar uma pesquisa de log de auditoria de caixa de correio. Para detalhes, consulte [Criar uma pesquisa de log de auditoria de caixas de correio](create-a-mailbox-audit-log-search-exchange-2013-help.md).

Para tarefas de gerenciamento adicionais relacionadas ao log de auditoria de caixa de correio, consulte [Procedimentos de registro em log de auditoria de caixa de correio](mailbox-audit-logging-procedures-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: 1 minuto.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Log de auditoria de caixas de correio" no tópico [Permissões de política e conformidade de mensagens](messaging-policy-and-compliance-permissions-exchange-2013-help.md).

  - Por padrão, o registro em log de auditoria de caixa de correio está desabilitado para todas as caixas de correio. Para cada caixa de correio que deseja auditorar, você deve habilitar o registro em log de auditoria e especificar as ações do proprietário, delegado ou administrador da caixa de correio que será auditada. Para detalhes, consulte [Habilitar ou desabilitar uma caixa de correio do log de auditoria de caixa de correio](enable-or-disable-mailbox-audit-logging-for-a-mailbox-exchange-2013-help.md).

  - Você não pode usar o EAC para pesquisar o log de auditoria de caixa de correio para uma caixa de correio. Entretanto, você pode usar o EAC para executar ou pesquisar e exportar um relatório de acesso de caixa de correio que não seja de proprietário.

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>.



## Usar o Shell para pesquisar o log de auditoria de caixa de correio para uma caixa de correio

Para exemplos de como usar o Shell para pesquisar o log de auditoria de caixa de correio para uma caixa de correio, consulte [Examples](https://technet.microsoft.com/pt-br/ff522360\(exchg.150\)#examples), em [Search-MailboxAuditLog](https://technet.microsoft.com/pt-br/library/ff522360\(v=exchg.150\)).

