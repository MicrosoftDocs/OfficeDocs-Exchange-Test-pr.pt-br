---
title: 'Configurar cotas de itens recuperáveis e retenção de Item excluído: Exchange 2013 Help'
TOCTitle: Configurar cotas de itens recuperáveis e retenção de Item excluído
ms:assetid: de7d667a-1c93-4364-a4f9-2aa5e3678b12
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Ee364752(v=EXCHG.150)
ms:contentKeyID: 50556304
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configurar cotas de itens recuperáveis e retenção de Item excluído

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2016-12-09_

Quando um usuário exclui os itens da pasta Itens excluídos padrão usando o Delete, Shift + Delete ou ações **Esvaziar pasta Itens excluídos**, os itens são movidos para a pasta **Items\\Deletions recuperável**. A duração que itens excluídos permaneçam nesta pasta baseia-se as configurações de retenção de item excluído definidas para o banco de dados de caixa de correio ou a caixa de correio. Por padrão, um banco de dados de caixa de correio está configurado para reter itens excluídos 14 dias, e os aviso de cota e a cota de itens recuperáveis de itens recuperáveis são definidos como 20 gigabytes (GB) e 30 GB respectivamente.


> [!TIP]
> Antes do tempo de retenção para ter decorrido de itens excluídos, Microsoft Outlook e Microsoft OfficeOutlook Web App os usuários podem recuperar itens excluídos, usando o recurso de recuperar itens excluídos. Para saber mais sobre esses recursos, consulte o tópico "Recuperar itens excluídos" for <A href="https://go.microsoft.com/fwlink/p/?linkid=198206">Outlook</A> ou <A href="https://go.microsoft.com/fwlink/p/?linkid=198207">Outlook Web App</A>.



Você pode usar o Shell para configurar cotas de itens recuperáveis para uma caixa de correio ou de um banco de dados de caixa de correio e as configurações de retenção de item excluído. Mantenha a retenção de item excluído configurações serão ignoradas quando uma caixa de correio for colocada em retenção In-loco ou retenção de litígio.

Para obter mais informações sobre a retenção de itens excluídos, a pasta Itens Recuperáveis, Bloqueio In-loco e retenção de litígio, consulte [Pasta Itens Recuperáveis](recoverable-items-folder-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: 5 minutos.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Gerenciamento de registros de mensagens" no tópico [Permissões de política e conformidade de mensagens](messaging-policy-and-compliance-permissions-exchange-2013-help.md).

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>.



## O que você deseja fazer?

## Configurar a retenção de item excluído de uma caixa de correio

**Usar o EAC para configurar a retenção de item excluído de uma caixa de correio**

1.  Navegue até **Destinatários** \> **Caixas de Correio**.

2.  Na exibição de lista, selecione uma caixa de correio e clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").

3.  Na página de propriedades de caixa de correio, clique em **uso de caixa de correio**, clique em **mais opções** e selecione uma das seguintes opções
    
      - **Use as configurações de retenção padrão do banco de dados de caixa de correio**    Use esta configuração para a configuração de retenção de item excluído está configurada para o banco de dados de caixa de correio.
    
      - **Personalizar as configurações para esta caixa de correio**    Use esta configuração para definir as configurações de retenção de item excluído da caixa de correio.
        
        **Manter os itens excluídos por (dias)**    Esta caixa exibe a quantidade de tempo que os itens excluídos são mantidos antes de serem excluídos permanentemente e não podem ser recuperados pelo usuário. Quando a caixa de correio é criada, esse valor baseia-se as configurações de retenção de item excluído definidas para o banco de dados de caixa de correio. Por padrão, um banco de dados de caixa de correio está configurado para reter itens excluídos 14 dias. O intervalo de valores para essa propriedade é de 0 a 24,855 dias.
    
      - **Não excluir itens permanentemente até que seja feito backup do banco de dados**   Marque essa caixa de seleção para impedir que caixas de correio e emails sejam excluídos permanentemente até que seja feito backup do banco de dados de caixa de correio em que a caixa de correio está.

**Use o Shell para configurar a retenção de item excluído de uma caixa de correio**

Este exemplo configura a caixa de correio de April Stewart para reter itens excluídos por 30 dias.

    Set-Mailbox -Identity - "April Stewart" -RetainDeletedItemsFor 30

Para obter informações detalhadas sobre sintaxes e parâmetros, confira [Set-Mailbox](https://technet.microsoft.com/pt-br/library/bb123981\(v=exchg.150\)).

## Use o Shell para configurar cotas de itens recuperáveis para uma caixa de correio


> [!TIP]
> Você não pode usar o EAC para configurar cotas de itens recuperáveis para uma caixa de correio.



Este exemplo configura um aviso de cota de 12 GB e uma cota de itens recuperáveis de 15 GB para caixa de correio de April Stewart de itens recuperáveis.

    Set-Mailbox -Identity "April Stewart" -RecoverableItemsWarningQuota 12GB -RecoverableItemsQuota 15GB -UseDatabaseQuotaDefaults $false


> [!TIP]
> Para configurar uma caixa de correio para usar cotas de itens recuperáveis diferentes que o banco de dados de caixa de correio em que reside, você deve definir o parâmetro <EM>UseDatabaseQuotaDefaults</EM> para <CODE>$false</CODE>.



Para obter informações detalhadas sobre sintaxes e parâmetros, confira [Set-Mailbox](https://technet.microsoft.com/pt-br/library/bb123981\(v=exchg.150\)).

## Use o Shell para configurar a retenção de item excluído de um banco de dados de caixa de correio


> [!TIP]
> Você não pode usar o EAC para configurar a retenção de item excluído de um banco de dados de caixa de correio.



Este exemplo configura um período de retenção de item excluído de 10 dias para o banco de dados de caixa de correio MDB2.

    Set-MailboxDatabase -Identity MDB2 -DeletedItemRetention 10

Para obter informações detalhadas de sintaxes e de parâmetros, consulte [Set-MailboxDatabase](https://technet.microsoft.com/pt-br/library/bb123971\(v=exchg.150\)).

## Use o Shell para configurar cotas de itens recuperáveis para um banco de dados de caixa de correio


> [!TIP]
> Você não pode usar o EAC para configurar cotas de itens recuperáveis para um banco de dados de caixa de correio



Este exemplo configura um aviso de cota de 15 GB e uma cota de itens recuperáveis de 20 GB no banco de dados de caixa de correio MDB2 de itens recuperáveis.

    Set-MailboxDatabase -Identity MDB2 -RecoverableItemsWarningQuota 15GB -RecoverableItemsQuota 20GB

Para obter informações detalhadas de sintaxes e de parâmetros, consulte [Set-MailboxDatabase](https://technet.microsoft.com/pt-br/library/bb123971\(v=exchg.150\)).

