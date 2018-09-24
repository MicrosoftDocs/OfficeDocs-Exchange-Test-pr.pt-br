---
title: 'Criar uma função sem escopo: Exchange 2013 Help'
TOCTitle: Criar uma função sem escopo
ms:assetid: 5a042ccf-4d5f-4609-a91b-21c20d1e6459
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Dd876886(v=EXCHG.150)
ms:contentKeyID: 50485669
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Criar uma função sem escopo

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2014-06-09_

Uma função de gerenciamento sem escopo pode ser usada oferecer a administradores e usuários especializados acesso a scripts do Windows PowerShell e cmdlets não-Exchange. Você pode também criar uma função de nível superior sem escopo e adicionar scripts ou cmdlets não-Exchange a essa função ou criar uma função com base em uma função de nível superior sem escopo existente. Após uma função sem escopo ter sido criada e personalizada, ela poderá ser atribuída a grupos de funções de gerenciamento, usuários e grupos de segurança universal (USGs). Funções sem escopo não podem ser atribuídas a diretivas de atribuição de função de gerenciamento. Para obter mais informações sobre funções sem escopo, consulte [Noções básicas sobre funções de gerenciamento](understanding-management-roles-exchange-2013-help.md).


> [!CAUTION]
> As funções sem escopo podem ser poderosas porque, como seu próprio nome diz, nenhum escopo de gerenciamento é aplicado a elas. Isso significa que os scripts e os cmdlets não-Exchange que elas contêm podem ser executados para qualquer objeto em sua organização do Exchange. Considere isso ao adicionar scripts ou cmdlets não-Exchange a uma função sem escopo e ao atribuir a função sem escopo.




> [!NOTE]
> Se você quiser criar uma função que contenha cmdlets do Exchange, será preciso criar uma função baseada em uma função de gerenciamento existente. Para obter mais informações sobre como criar funções com cmdlets do Exchange, consulte <A href="create-a-role-exchange-2013-help.md">Criar uma função</A>.



Procurando outras tarefas de gerenciamento relacionadas a funções? Consulte [Permissões avançadas](advanced-permissions-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para concluir cada procedimento: 5 minutos

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "funções de gerenciamento" no tópico [Permissões de gerenciamento de função](role-management-permissions-exchange-2013-help.md).

  - Você deve usar o Shell para executar estes procedimentos.

  - A capacidade de criar funções sem escopo não está incluída em nenhum grupo de funções de gerenciamento por padrão. É preciso primeiro atribuir a função de Gerenciamento de Função sem Escopo a um usuário ou a um grupo de funções ou USG de que o usuário seja membro, antes de o usuário poder criar um grupo de funções. Para mais informações sobre como adicionar uma função a um usuário, USG ou grupo de função, consulte os seguintes tópicos:
    
      - [Gerenciar grupos de função](manage-role-groups-exchange-2013-help.md)
    
      - [Adicionar uma função a um usuário ou USG](add-a-role-to-a-user-or-usg-exchange-2013-help.md)

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>.



## O que você deseja fazer?

## Criar uma função de gerenciamento de nível superior sem escopo

Se quiser disponibilizar scripts ou cmdlets não-Exchange a administradores ou especialistas de sua organização, será preciso criar uma função de nível superior sem escopo. Scripts e cmdlets não-Exchange só podem ser adicionados a uma função sem escopo criada como função de nível superior, porque a função sem escopo inicial não é herdada de outras funções. A nova função de nível superior sem escopo pode ser pai de outras funções sem escopo que podem também usar os scripts adicionados e cmdlets não-Exchange.

Aqui estão as etapas para criar uma função de nível superior sem escopo:

## Etapa 1: Criar a função de nível superior sem escopo

Funções de nível superior sem escopo não têm uma função pai. É preciso especificar a opção *UnscopedTopLevel* para criar uma função sem um pai. Use a sintaxe a seguir para criar a nova função.

```powershell
New-ManagementRole <name of new role> -UnscopedTopLevel
```

Este exemplo cria a função de nível superior sem escopo de scripts de TI.

```powershell
New-ManagementRole "IT Scripts" -UnscopedTopLevel
```

Após ser criada, a função ficará vazia até você adicionar scripts ou cmdlets não-Exchange a ela.

Para informações detalhadas de sintaxes e de parâmetros, consulte [New-ManagementRole](https://technet.microsoft.com/pt-br/library/dd298073\(v=exchg.150\)).

## Etapa 2a: Adicionar entradas de função de gerenciamento de script

Se quiser adicionar um script à nova função sem escopo, use esta etapa. Se quiser adicionar um cmdlet não-Exchange à nova função sem escopo, use Step 2b.

Para adicionar um script do PowerShell do Windows a uma função de nível superior sem escopo, é preciso adicionar uma entrada de função de gerenciamento à função. A entrada de função contém o nome do script e os parâmetros do script que você deseja tornar disponíveis à função.

O script deve residir no diretório `RemoteScripts` no caminho de instalação do Microsoft Exchange Server 2013 em todos os servidores que executam o Exchange 2013, onde os usuários podem se conectar para executar o script. Se um usuário tiver acesso para executar um script, mas o script não estiver localizado no servidor do Exchange 2013 ao qual o usuário está conectado, ocorre um erro. Por padrão, o caminho para o diretório `RemoteScripts` é C:\\Arquivos de Programas\\Microsoft\\Exchange Server\\V15\\RemoteScripts.

Depois de copiar o script para os servidores apropriados do Exchange 2013 e decidir quais parâmetros do script devem ser usados, crie a entrada de função usando a sintaxe a seguir.

    Add-ManagementRoleEntry <unscoped top-level role name>\<script filename> -Parameters <parameter 1, parameter 2, parameter...> -Type Script -UnscopedTopLevel

Este exemplo adiciona o script BulkProvisionUsers.ps1 à função Scripts de TI com os parâmetros *Name* e *Location*.

    Add-ManagementRoleEntry "IT Scripts\BulkProvisionUsers.ps1" -Parameters Name, Location -Type Script -UnscopedTopLevel


> [!NOTE]
> O cmdlet <STRONG>Add-ManagementRoleEntry</STRONG> realiza uma validação básica para garantir que você tenha adicionado apenas os parâmetros existentes no script. Entretanto, nenhuma outra validação é realizada depois que a entrada de função for adicionada. Se parâmetros forem adicionados ou removidos posteriormente, você terá que atualizar manualmente as entradas de função que contenham o script.



## Etapa 2b: Adicionar entradas de função do cmdlet não-Exchange

Se quiser adicionar um cmdlet não-Exchange à nova função sem escopo, use esta etapa. Se quiser adicionar um script à nova função sem escopo, use Step 2a.

Para adicionar um cmdlet que não seja do Exchange a uma função de nível superior sem escopo, é preciso adicionar uma entrada de função de gerenciamento à função. A entrada de função contém o snap-in do cmdlet, o nome do cmdlet e os parâmetros do cmdlet que você deseja tornar disponível à função.

Se você adicionar cmdlets que não sejam do Exchange à nova função, os cmdlets deverão ser instalados em todos os servidores do Exchange 2013 nos quais os usuários possam se conectar para executar os cmdlets. Para aprender a instalar e registrar corretamente os snap-ins do Windows PowerShell que contêm os cmdlets que você deseja usar, consulte a documentação do Produto.

Após instalar o snap-in do Windows PowerShell que contém os cmdlets nos servidores do Exchange 2013 apropriados e decidir quais parâmetros do cmdlet devem ser usados, crie a entrada de função usando a sintaxe a seguir.

    Add-ManagementRoleEntry <unscoped top-level role name>\<cmdlet name> -PSSnapinName <snap-in name> -Parameters <parameter 1, parameter 2, parameter...> -Type Cmdlet -UnscopedTopLevel

Este exemplo adiciona o cmdlet **Set-WidgetConfiguration** no snap-in Contoso.Admin.Cmdlets à função Widget Cmdlets com os parâmetros *Database* e *Size*.

    Add-ManagementRoleEntry "Widget Cmdlets\Set-WidgetConfiguration" -PSSnapinName Contoso.Admin.Cmdlets -Parameters Database, Size -Type Cmdlet -UnscopedTopLevel


> [!NOTE]
> O cmdlet <STRONG>Add-ManagementRoleEntry</STRONG> realiza uma validação básica para garantir que você tenha adicionado apenas os parâmetros existentes no cmdlet. Entretanto, nenhuma outra validação é realizada depois que a entrada de função for adicionada. Se o cmdlet for alterado posteriormente, e se parâmetros forem adicionados ou removidos, você terá que atualizar manualmente as entradas de função que contenham o cmdlet.



## Etapa 3: Atribuir a função de gerenciamento

A etapa final ao criar e configurar uma função é atribuí-la a um destinatário de função.


> [!IMPORTANT]
> Os escopos de gerenciamento não podem ser configurados em atribuições de função que atribuam uma função sem escopo. Ao escolher criar uma atribuição de função para um grupo de função, usuário ou USG, é preciso escolher a opção para criar uma atribuição de função sem um escopo de gerenciamento.



É possível atribuir a nova função a um grupo de função, usuário ou USG. Para obter mais informações, consulte os tópicos a seguir:

  - [Gerenciar grupos de função](manage-role-groups-exchange-2013-help.md)

  - [Adicionar uma função a um usuário ou USG](add-a-role-to-a-user-or-usg-exchange-2013-help.md)

## Criar uma função sem escopo com base em outra função sem escopo

Se tiver uma função de nível superior sem escopo existente ou outras funções sem escopo que queira ter como base para novas funções sem escopo, você poderá criar funções sem escopo filhas. Essas funções podem conter um subconjunto dos scripts e cmdlets existentes nas funções sem escopo pai. Isso será útil, por exemplo, se você quiser fornecer apenas um subconjunto dos scripts ou cmdlets disponíveis em uma função sem escopo pai a um administrador menos experiente.

Aqui estão as etapas para criar uma função sem escopo filha:

## Etapa 1: Criar a função filha sem escopo

Funções novas filhas sem escopo podem ter como base funções sem escopo existentes. Quando você cria uma função, uma função existente e suas entradas de função de gerenciamento são copiadas para a nova função. A função existente se torna pai da nova função filha. Se você criar uma função sem escopo que tenha como base outra função sem escopo, será preciso escolher uma função que tenha todos os cmdlets e parâmetros que precisa usar e remover os que não quer usar. As funções sem escopo filhas não podem ter entradas de função de gerenciamento que não existem na função pai.


> [!NOTE]
> Se for preciso criar uma função sem escopo que tenha scripts ou cmdlets não-Exchange que não existam em nenhuma outra função sem escopo, crie uma função de nível superior sem escopo. Para obter mais informações, consulte Create an unscoped top-level management role, anteriormente neste tópico.



Use a sintaxe a seguir para criar a nova função.

    New-ManagementRole -Parent <existing unscoped role to copy> -Name <name of new unscoped role>

Este exemplo copia a função de Scripts Globais de TI e suas entradas de função de gerenciamento para a função de Scripts de TI de Diagnóstico.

```powershell
New-ManagementRole -Parent "IT Global Scripts" -Name "Diagnostic IT Scripts"
```

Para informações detalhadas de sintaxes e de parâmetros, consulte [New-ManagementRole](https://technet.microsoft.com/pt-br/library/dd298073\(v=exchg.150\)).

## Etapa 2: Alterar as entradas de função de gerenciamento da função

Depois de criar sua função, você terá que alterar as entradas da função. Você pode remover toda a entrada da função, que remove o acesso ao script associado ou cmdlet não-Exchange completamente. Ou pode remover os parâmetros de uma entrada de função para remover o acesso aos parâmetros específicos no script associado ou cmdlet não-Exchange.

Não é possível adicionar entradas ou parâmetros em entradas de função, a menos que existam na função pai. Como você acabou de criar uma função a partir de uma função pai na Etapa 1, não poderá adicionar nenhuma entrada de função ou parâmetro extra nas entradas de função, pois eles não existem na função pai.

Ao alterar uma entrada de função em uma função, você pode realizar um destes procedimentos:

  - Remover uma única entrada de função inteira.

  - Remover várias entradas de função inteiras.

  - Remover parâmetros de uma entrada de função.

Para remover entradas de função de sua nova função, consulte [Remover uma entrada de função de uma função](remove-a-role-entry-from-a-role-exchange-2013-help.md).

## Etapa 3: Atribuir a função de gerenciamento

A etapa final ao criar e configurar uma função é atribuí-la a um destinatário de função.


> [!IMPORTANT]
> Os escopos de gerenciamento não podem ser configurados em atribuições de função que atribuam uma função sem escopo. Ao escolher criar uma atribuição de função para um grupo de função, usuário ou USG, é preciso escolher a opção para criar uma atribuição de função sem um escopo de gerenciamento.



É possível atribuir a nova função a um grupo de função, usuário ou USG. Para mais informações, consulte os seguintes tópicos:

  - [Gerenciar grupos de função](manage-role-groups-exchange-2013-help.md)

  - [Adicionar uma função a um usuário ou USG](add-a-role-to-a-user-or-usg-exchange-2013-help.md)

