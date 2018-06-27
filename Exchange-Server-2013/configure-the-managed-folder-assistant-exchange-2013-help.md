---
title: 'Configurar o Assistente de pasta gerenciada: Exchange 2013 Help'
TOCTitle: Configurar o Assistente de pasta gerenciada
ms:assetid: 9fcfb9b6-bd24-4218-a163-bc599cd5476a
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Bb123958(v=EXCHG.150)
ms:contentKeyID: 50486264
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configurar o Assistente de pasta gerenciada

 

_**Aplica-se a:**Exchange Server 2013_

_**Tópico modificado em:**2014-10-01_

O *Assistente de pasta gerenciada* é um MicrosoftExchange caixa de correio Assistant que se aplica as configurações de retenção de mensagem configuradas em diretivas de retenção.

Para outras tarefas de gerenciamento relacionadas ao gerenciamento de registros de mensagens (MRM), consulte [Procedimentos de gerenciamento de registros de mensagens](messaging-records-management-procedures-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo de conclusão: 1 minuto.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Gerenciamento de registros de mensagens" no tópico [Permissões de política e conformidade de mensagens](messaging-policy-and-compliance-permissions-exchange-2013-help.md).

  - Você não pode usar o Centro de administração do Exchange (EAC) para configurar o Assistente de pasta gerenciada. Você deve usar o Shell

  - Em Exchange 2013, o Assistente de pasta gerenciada é um Assistente de limitação. Os assistentes de limitação são sempre em execução e não precisam ser agendado. Os recursos do sistema que consomem são limitados. Você pode configurar o Assistente de pasta gerenciada para processar todas as caixas de correio em um servidor de caixa de correio em um determinado período (conhecido como um *ciclo de trabalho)*. Por padrão, o ciclo de trabalho é definido para um dia.

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>.



## O que você deseja fazer?

## Use o Shell para configurar o Assistente de pasta gerenciada

Este exemplo configura o Assistente de pasta gerenciada para processar todas as caixas de correio dentro de um dia.

    Set-MailboxServer MyMailboxServer -ManagedFolderWorkCycle 1

Para informações detalhadas de sintaxes e de parâmetros, consulte [Set-MailboxServer](https://technet.microsoft.com/pt-br/library/aa998651\(v=exchg.150\)).

## Como saber se funcionou?

Para verificar se você configurou com êxito Assistente de pasta gerenciada, use o cmdlet [Get-MailboxServer](https://technet.microsoft.com/pt-br/library/bb123539\(v=exchg.150\)) para verificar se o parâmetro *ManagedFolderWorkCycle* .

Este comando recupera todos os servidores de caixa de correio na organização e emite o propriedades workcycle do Assistente de pasta gerenciada em cada servidor no formato de tabela. A opção de *Auto* é usada para ajustar automaticamente a largura da coluna.

    Get-MailboxServer | Format-Table Name,ManagedFolderWorkCycle* -Auto

## Use o Shell para iniciar o Assistente de pasta gerenciada

Este exemplo aciona o Assistente de pasta gerenciada para processar imediatamente a caixa de correio de Morris Cornejo.

    Start-ManagedFolderAssistant -Identity morris.cornejo@contoso.com

Para detalhadas sobre sintaxe e informações de parâmetro, consulte [Start-ManagedFolderAssistant](https://technet.microsoft.com/pt-br/library/aa998864\(v=exchg.150\)).

