---
title: 'Alterar um escopo de função: Exchange 2013 Help'
TOCTitle: Alterar um escopo de função
ms:assetid: 9180e1e0-c352-4ccd-8da6-885a2e309867
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Dd298145(v=EXCHG.150)
ms:contentKeyID: 50486183
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Alterar um escopo de função

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2012-10-03_

Escopos da função de gerenciamento determinam quais objetos são disponibilizados para um usuário para que os objetos podem ser alterados usando os cmdlets e parâmetros atribuídos a eles. Alterando um escopo, você pode alterar a quais objetos são disponibilizados aos usuários para criar, alterar ou remover.

Você pode alterar um escopo de gerenciamento personalizado. Você pode alterar os escopos exclusivos ou regulares. Se você alterar um escopo exclusivo, o novo escopo entrará em vigor imediatamente. Se você quiser alterar uma atribuição de função de gerenciamento com um escopo de gerenciamento de unidade predefinido ou organizacional (UO), consulte [Alterar uma atribuição de função](change-a-role-assignment-exchange-2013-help.md).

Para mais informações sobre os escopos e as atribuições de função de gerenciamento no Microsoft Exchange Server 2013, consulte estes tópicos:

  - [Noções básicas sobre escopos da função de gerenciamento](understanding-management-role-scopes-exchange-2013-help.md)

  - [Noções básicas sobre as atribuições de função de gerenciamento](understanding-management-role-assignments-exchange-2013-help.md)

Procurando outras tarefas de gerenciamento relacionadas a escopos de função? Consulte [Permissões avançadas](advanced-permissions-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para concluir cada procedimento: 5 minutos

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Escopos de gerenciamento" no tópico [Permissões de gerenciamento de função](role-management-permissions-exchange-2013-help.md).

  - Você deve usar o Shell para executar estes procedimentos.

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>.



## O que você deseja fazer?

## Altere o nome de um escopo

Para alterar o nome de um escopo, use a seguinte sintaxe.

    Set-ManagementScope <current scope name> -Name <new scope name>

Este exemplo altera o escopo de servidores de Seattle para servidores do Exchange de Seattle.

    Set-ManagementScope "Seattle Servers" -Name "Seattle Exchange Servers"

Para detalhadas sobre sintaxe e informações de parâmetro, consulte [Set-ManagementScope](https://technet.microsoft.com/pt-br/library/dd297996\(v=exchg.150\)).

## Alterar um filtro de destinatário em um escopo

Para alterar o filtro de destinatário em um escopo, use a seguinte sintaxe.

    Set-ManagementScope <scope name> -RecipientRestrictionFilter { <new recipient filter> }

Este exemplo altera o filtro de destinatário para corresponder todos os objetos de destinatário cuja propriedade **Company** é definida como contoso.

    Set-ManagementScope "Company Scope" -RecipientRestrictionFilter { Company -eq 'contoso' }

Para detalhadas sobre sintaxe e informações de parâmetro, consulte [Set-ManagementScope](https://technet.microsoft.com/pt-br/library/dd297996\(v=exchg.150\)).

Para obter mais informações sobre filtros de destinatários e para ver uma lista de propriedades de destinatário filtráveis, consulte [Noções básicas sobre filtros do escopo de função de gerenciamento](understanding-management-role-scope-filters-exchange-2013-help.md).

## Alterar a raiz da unidade organizacional em um escopo

Para alterar a raiz da unidade Organizacional em um escopo, use a seguinte sintaxe.

    Set-ManagementScope <scope name> -RecipientRoot <OU>

Este exemplo altera a raiz da unidade Organizacional para a UO de usuários de vendas da América do Norte/vendas sob o domínio contoso.com.

    Set-ManagementScope "Sales Users" -RecipientRoot "contoso.com/North America/Sales"

Para detalhadas sobre sintaxe e informações de parâmetro, consulte [Set-ManagementScope](https://technet.microsoft.com/pt-br/library/dd297996\(v=exchg.150\)).

## Alterar um filtro de servidor em um escopo

Para alterar o filtro do servidor em um escopo, use a seguinte sintaxe.

    Set-ManagementScope <scope name> -ServerRestrictionFilter { <new server filter> }

Este exemplo altera o filtro do servidor para fazer a correspondência de todos os objetos de servidor em que a propriedade **ServerSite** é definida como ' CN = Redmond, CN = Sites, CN = Configuration, DC = contoso, DC = com ".

    Set-ManagementScope "Company Scope" -ServerRestrictionFilter { ServerSite -eq 'CN=Redmond,CN=Sites,CN=Configuration,DC=contoso,DC=com' }

Para detalhadas sobre sintaxe e informações de parâmetro, consulte [Set-ManagementScope](https://technet.microsoft.com/pt-br/library/dd297996\(v=exchg.150\)).

Para obter mais informações sobre filtros de servidor e para ver uma lista de propriedades do servidor filtráveis, consulte [Noções básicas sobre filtros do escopo de função de gerenciamento](understanding-management-role-scope-filters-exchange-2013-help.md).

## Alterar a lista de servidores em um escopo

Você não pode alterar a lista de servidores em um escopo. Se você precisar alterar a lista de servidores, você precisa fazer o seguinte:

1.  Se necessário, recupere a lista atual de servidor do escopo a ser substituído usando o procedimento "Exibir um escopo específico" no tópico [Exibir escopos de função](view-role-scopes-exchange-2013-help.md) .

2.  Criar um escopo com a nova lista de servidor usando o "etapa 1: criar um escopo personalizado" procedimento no tópico [Criar um escopo regular ou exclusivo](create-a-regular-or-exclusive-scope-exchange-2013-help.md) .

3.  Altere todas as atribuições de função de gerenciamento que usam o escopo antigo para usar o novo escopo usando o procedimento "Usar o Shell para alterar o filtro do servidor ou baseada em lista de escopo em uma atribuição de função" no tópico [Alterar uma atribuição de função](change-a-role-assignment-exchange-2013-help.md) .

4.  Remova o escopo antigo usando o procedimento no tópico [Remover um escopo de função](remove-a-role-scope-exchange-2013-help.md) .

## Alterar um filtro de banco de dados em um escopo

Para alterar o filtro de banco de dados em um escopo, use a seguinte sintaxe.

    Set-ManagementScope <scope name> -DatabaseRestrictionFilter { <new database filter> }

Este exemplo altera o filtro de banco de dados para coincidir com todos os objetos de banco de dados cuja propriedade **Name** contiver a cadeia de caracteres "Executivo".

    Set-ManagementScope "Database Executive Scope" -DatabaseRestrictionFilter { Name -Like "*Executive*" }

Para detalhadas sobre sintaxe e informações de parâmetro, consulte [Set-ManagementScope](https://technet.microsoft.com/pt-br/library/dd297996\(v=exchg.150\)).

Para obter mais informações sobre filtros de banco de dados e para ver uma lista de propriedades de banco de dados filtráveis, consulte [Noções básicas sobre filtros do escopo de função de gerenciamento](understanding-management-role-scope-filters-exchange-2013-help.md).

## Alterar a lista de banco de dados em um escopo

Você não pode alterar a lista de bancos de dados em um escopo. Se você precisar alterar a lista de banco de dados, você precisará fazer o seguinte:

1.  Se necessário, recupere a lista de banco de dados atual do escopo a ser substituído usando o procedimento "Exibir um escopo específico" no tópico [Exibir escopos de função](view-role-scopes-exchange-2013-help.md) .

2.  Criar um escopo com a nova lista de banco de dados usando o "etapa 1: criar um escopo personalizado" procedimento no tópico [Criar um escopo regular ou exclusivo](create-a-regular-or-exclusive-scope-exchange-2013-help.md) .

3.  Altere todas as atribuições de função de gerenciamento que usam o escopo antigo para usar o novo escopo usando o procedimento "Usar o Shell para alterar o filtro de banco de dados ou baseada em lista de escopo em uma atribuição de função" no tópico [Alterar uma atribuição de função](change-a-role-assignment-exchange-2013-help.md) .

4.  Remova o escopo antigo usando o procedimento no tópico [Remover um escopo de função](remove-a-role-scope-exchange-2013-help.md) .

