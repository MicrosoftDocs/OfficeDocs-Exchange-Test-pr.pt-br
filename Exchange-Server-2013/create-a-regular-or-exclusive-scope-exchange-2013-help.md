---
title: 'Criar um escopo regular ou exclusivo: Exchange 2013 Help'
TOCTitle: Criar um escopo regular ou exclusivo
ms:assetid: b97a5be3-15cc-4954-ba30-a824a95e21be
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Dd351083(v=EXCHG.150)
ms:contentKeyID: 50486479
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Criar um escopo regular ou exclusivo

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2015-04-07_

Escopos da função de gerenciamento determinam quais objetos são disponibilizados para um usuário para que os objetos podem ser alterados usando os cmdlets e parâmetros atribuídos a eles. Adicionando um escopo de gerenciamento, você pode configurar as atribuições de função de gerenciamento para que os usuários podem administrar servidores específicos, bancos de dados, os destinatários e outros objetos em sua organização enquanto impedidos alterando a outros objetos.


> [!IMPORTANT]  
> Quando você cria um escopo regular ou exclusivo, você pode substituir o escopo de gravação que é definido na função de gerenciamento que está sendo atribuído. Você não pode substituir o escopo de leitura que está configurado na função de gerenciamento.



Você pode criar um escopo de gerenciamento personalizado e, em seguida, adicionar ou alterar uma atribuição de função de gerenciamento. Se você deseja criar uma atribuição de função de gerenciamento com um escopo de gerenciamento de unidade pré-criados ou organizacional (UO), consulte [Adicionar uma função a um usuário ou USG](add-a-role-to-a-user-or-usg-exchange-2013-help.md).

Para mais informações sobre os escopos e as atribuições de função de gerenciamento no Microsoft Exchange Server 2013, consulte estes tópicos:

  - [Noções básicas sobre escopos da função de gerenciamento](understanding-management-role-scopes-exchange-2013-help.md)

  - [Noções básicas sobre as atribuições de função de gerenciamento](understanding-management-role-assignments-exchange-2013-help.md)

Procurando outras tarefas de gerenciamento relacionadas a escopos? Consulte [Permissões avançadas](advanced-permissions-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para concluir cada procedimento: 5 minutos

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Escopos de gerenciamento" no tópico [Permissões de gerenciamento de função](role-management-permissions-exchange-2013-help.md).

  - Você deve usar o Shell para executar estes procedimentos.

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]  
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>.



## Como fazer isso?

## Etapa 1: Criar um escopo personalizado

Para criar um escopo personalizado, escolha um dos seguintes tipos de escopos.

## Escopo de filtro de destinatário

Escopos baseado em filtro de destinatários são criados usando-se o parâmetro *RecipientRestrictionFilter* no cmdlet **New-ManagementScope** . Quando você cria um filtro de destinatário, além de propriedades de destinatário para filtrar, você pode especificar a UO na qual a consulta de filtro é executada. Quando você especifica uma UO de base, você ainda mais restringir o escopo de gravação da função.

Para obter mais informações sobre filtros de escopo de gerenciamento, consulte [Noções básicas sobre filtros do escopo de função de gerenciamento](understanding-management-role-scope-filters-exchange-2013-help.md).

Use a seguinte sintaxe para criar um escopo de filtro de restrição de domínio com uma UO de base.

    New-ManagementScope -Name <scope name> -RecipientRestrictionFilter <filter query> [-RecipientRoot <OU>]

Este exemplo cria um escopo que inclui todas as caixas de correio dentro do contoso.com/Sales UO.

    New-ManagementScope -Name "Mailboxes in Sales OU" -RecipientRestrictionFilter { RecipientType -eq 'UserMailbox' } -RecipientRoot "contoso.com/Sales OU"


> [!NOTE]  
> Você pode omitir o parâmetro <EM>RecipientRoot</EM> se quiser que o filtro a ser aplicado a todo implícito leitura o escopo da função de gerenciamento e não apenas dentro de uma OU específica.



Para informações detalhadas de sintaxes e de parâmetros, consulte [New-ManagementScope](https://technet.microsoft.com/pt-br/library/dd335137\(v=exchg.150\)).

## Escopo de configuração de filtro do servidor

Escopos de configuração baseado em filtro de servidor são criados usando-se o parâmetro *ServerRestrictionFilter* no cmdlet **New-ManagementScope** . Um filtro do servidor permite criar um escopo que se aplica somente aos servidores que correspondem ao filtro que você especificar.

Para obter mais informações sobre filtros do escopo de gerenciamento e para obter uma lista de propriedades do servidor filtráveis, consulte [Noções básicas sobre filtros do escopo de função de gerenciamento](understanding-management-role-scope-filters-exchange-2013-help.md).

Use a sintaxe a seguir para criar um escopo de filtro do servidor.

```powershell
New-ManagementScope -Name <scope name> -ServerRestrictionFilter <filter query>
```

Este exemplo cria um escopo que inclui todos os servidores dentro do ' CN = Redmond, CN = Sites, CN = Configuration, DC = contoso, DC = com' site do AD (Active Directory ).

    New-ManagementScope -Name "Servers in Seattle AD site" -ServerRestrictionFilter { ServerSite -eq 'CN=Redmond,CN=Sites,CN=Configuration,DC=contoso,DC=com' }

Para informações detalhadas de sintaxes e de parâmetros, consulte [New-ManagementScope](https://technet.microsoft.com/pt-br/library/dd335137\(v=exchg.150\)).

## Escopo de configuração de lista de servidor

Escopos de configuração baseada na lista de servidor são criados usando-se o parâmetro *ServerList* no cmdlet **New-ManagementScope** . Um escopo de lista do servidor permite criar um escopo que se aplica somente para os servidores que você especificar em uma lista.

Use a seguinte sintaxe para criar um escopo de lista do servidor.

```powershell
New-ManagementScope -Name <scope name> -ServerList <server 1>, <server 2...>
```

Este exemplo cria um escopo que se aplica somente a MBX1, MBX3 e MBX5.

```powershell
New-ManagementScope -Name "Mailbox servers" -ServerList MBX1,MBX3,MBX5
```

Para informações detalhadas de sintaxes e de parâmetros, consulte [New-ManagementScope](https://technet.microsoft.com/pt-br/library/dd335137\(v=exchg.150\)).

## Escopo de configuração de filtro de banco de dados

Escopos de configuração baseado em filtro de banco de dados são criados usando-se o parâmetro *DatabaseRestrictionFilter* no cmdlet **New-ManagementScope** . Um filtro de banco de dados permite criar um escopo que é aplicada apenas os bancos de dados que correspondem ao filtro que você especificar.


> [!IMPORTANT]
> Atribuições de função associadas com os escopos de banco de dados são aplicadas somente a usuários que se conectam a servidores que executam o Microsoft Exchange Server 2010 Service Pack 1 (SP1) ou posterior ou Exchange 2013. Se um usuário atribuído a uma atribuição de função associada a um escopo de banco de dados se conecta a um servidor de pré-Exchange 2010 SP1, a atribuição de função não será aplicada ao usuário e o usuário não receber permissões qualquer fornecidos pela atribuição de função.



Para obter mais informações sobre filtros do escopo de gerenciamento e para obter uma lista das propriedades do banco de dados filtráveis, consulte [Noções básicas sobre filtros do escopo de função de gerenciamento](understanding-management-role-scope-filters-exchange-2013-help.md).

Use a sintaxe a seguir para criar um filtro de restrição de banco de dados.

```powershell
New-ManagementScope -Name <scope name> -DatabaseRestrictionFilter <filter query>
```

Este exemplo cria um escopo que inclui todos os bancos de dados que contêm a cadeia de caracteres "Executivo" na propriedade **Name** do banco de dados.

    New-ManagementScope -Name "Executive Databases" -DatabaseRestrictionFilter { Name -Like '*Executive*' }

Para informações detalhadas de sintaxes e de parâmetros, consulte [New-ManagementScope](https://technet.microsoft.com/pt-br/library/dd335137\(v=exchg.150\)).

## Escopo de configuração de lista do banco de dados

Escopos de configuração baseada na lista de banco de dados são criados usando-se o parâmetro *DatabaseList* no cmdlet **New-ManagementScope** . Um escopo de lista do banco de dados permite criar um escopo que é aplicada apenas os bancos de dados que você especificar em uma lista.


> [!IMPORTANT]
> Atribuições de função associadas com os escopos de banco de dados são aplicadas somente a usuários que se conectam a servidores que executam o Microsoft Exchange Server 2010 Service Pack 1 (SP1) ou posterior ou Exchange 2013. Se um usuário atribuído a uma atribuição de função associada a um escopo de banco de dados se conecta a um servidor de pré-Exchange 2010 SP1, a atribuição de função não será aplicada ao usuário e o usuário não receber permissões qualquer fornecidos pela atribuição de função.



Use a seguinte sintaxe para criar um escopo de lista do banco de dados.

```powershell
New-ManagementScope -Name <scope name> -DatabaseList <database 1>, <database 2...>
```

Esse exemplo cria um escopo que se aplica somente aos bancos de dados Banco de Dados 1, Banco de Dados 2 e Banco de Dados 3.

```powershell
New-ManagementScope -Name "Primary databases" -DatabaseList "Database 1", "Database 2", "Database 3"
```

Para informações detalhadas de sintaxes e de parâmetros, consulte [New-ManagementScope](https://technet.microsoft.com/pt-br/library/dd335137\(v=exchg.150\)).

## Escopo exclusivo

Qualquer escopo que você criou com o cmdlet **New-ManagementScope** pode ser designado como um escopo exclusivo. Para criar um escopo exclusivo, use os mesmos comandos em uma das seções anteriores para criar um escopo baseado em filtro de destinatário, baseado em filtro de escopo do servidor, com base em lista de escopo do servidor, escopo baseado em filtro de banco de dados ou escopo com base em lista de banco de dados e, em seguida, adicione a opção *Exclusive* ao comando.


> [!WARNING]
> Quando você criar escopos de gerenciamento exclusivos, apenas os função os destinatários atribuídos escopos exclusivos que contêm os objetos a serem modificadas podem acessar esses objetos. Apenas aos administradores uma função com o escopo exclusiva atribuídos podem acessar esses objetos protegidos, ou exclusivos.



Este exemplo cria um destinatário baseado em filtro escopo exclusivo que corresponde a qualquer usuário do departamento de executivos.

    New-ManagementScope "Executive Users Exclusive Scope" -RecipientRestrictionFilter { Department -Eq "Executives" } -Exclusive

Por padrão, quando um escopo exclusivo é criado, é necessário que reconhece que você criou um escopo exclusivo e que você esteja ciente do impacto que um escopo exclusivo tem sobre atribuições de função existente que não são exclusivas. Se você quiser suprime o aviso, você pode usar a opção *Force* . Este exemplo cria o mesmo escopo, como no exemplo anterior, mas sem aviso.

    New-ManagementScope "Executive Users Exclusive Scope" -RecipientRestrictionFilter { Department -Eq "Executives" } -Exclusive -Force

Para informações detalhadas de sintaxes e de parâmetros, consulte [New-ManagementScope](https://technet.microsoft.com/pt-br/library/dd335137\(v=exchg.150\)).

## Etapa 2: Adicionar ou alterar uma atribuição de função de gerenciamento

Depois de criar o escopo, você deve adicioná-lo para uma atribuição de função de gerenciamento de novo ou existente.

Se você cria um escopo de gerenciamento e quiser adicioná-la a uma nova atribuição de função de gerenciamento que você vai criar, consulte os seguintes tópicos:

  - [Gerenciar grupos de função](manage-role-groups-exchange-2013-help.md)

  - [Adicionar uma função a um usuário ou USG](add-a-role-to-a-user-or-usg-exchange-2013-help.md)

Se você cria um escopo de função de gerenciamento e quiser adicioná-la a uma atribuição de função de gerenciamento existente, consulte os seguintes tópicos:

  - [Gerenciar políticas de atribuição de função](manage-role-assignment-policies-exchange-2013-help.md)

  - [Alterar uma atribuição de função](change-a-role-assignment-exchange-2013-help.md)

