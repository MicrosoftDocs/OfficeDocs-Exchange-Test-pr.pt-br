---
title: 'Adicionar uma entrada de função a uma função de nível superior sem escopo: Exchange 2013 Help'
TOCTitle: Adicionar uma entrada de função a uma função de nível superior sem escopo
ms:assetid: 52fd3f20-c348-49d5-9bdb-f2cbf780cf2d
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Dd979789(v=EXCHG.150)
ms:contentKeyID: 50485594
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Adicionar uma entrada de função a uma função de nível superior sem escopo

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2012-10-03_

Você poderá adicionar scripts e cmdlets não-Exchange a funções de gerenciamento de nível superior sem escopo se quiser disponibilizar novos scripts ou cmdlets não-Exchange a funções sem escopo existentes. Esses scripts e cmdlets não-Exchange são adicionados como entradas de função de gerenciamento a funções de gerenciamento de nível superior sem escopo. Eles podem ser usados por essas entradas de função de nível superior sem escopo ou qualquer função sem escopo derivada de funções de nível superior. Para obter mais informações sobre entradas de função sem escopo, consulte [Noções básicas sobre funções de gerenciamento](understanding-management-roles-exchange-2013-help.md).


> [!TIP]
> Se você quiser alterar uma entrada de função em uma função de gerenciamento que contenha cmdlets do Exchange, consulte <A href="change-a-role-entry-exchange-2013-help.md">Alterar uma entrada de função</A>.



Procurando outras tarefas de gerenciamento relacionadas a funções? Consulte [Permissões avançadas](advanced-permissions-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para concluir cada procedimento: 5 minutos

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "funções de gerenciamento" no tópico [Permissões de gerenciamento de função](role-management-permissions-exchange-2013-help.md).

  - Você deve usar o Shell para executar estes procedimentos.

  - A capacidade de adicionar uma entrada de função a uma função de nível superior sem escopo não está incluída em nenhum grupo de funções de gerenciamento por padrão. É preciso primeiro atribuir a função de Gerenciamento de Função sem Escopo a um usuário ou a um grupo de funções ou USG de que o usuário seja membro, antes de o usuário poder adicionar uma entrada de função de nível superior sem escopo. Para mais informações sobre como adicionar uma função a um usuário, USG ou grupo de funções, consulte os seguintes tópicos:
    
      - [Gerenciar grupos de função](manage-role-groups-exchange-2013-help.md)
    
      - [Adicionar uma função a um usuário ou USG](add-a-role-to-a-user-or-usg-exchange-2013-help.md)

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>.



## O que você deseja fazer?

## Adicionar uma entrada de função de script a uma função de nível superior sem escopo

Se quiser adicionar um script a uma função sem escopo existente, use este procedimento. Se quiser adicionar um cmdlet não-Exchange a uma função sem escopo existente, consulte "Adicionar uma entrada de função de cmdlet não-Exchange a uma função de nível superior sem escopo" mais adiante neste tópico.

Para adicionar um script do PowerShell do Windows a uma função de nível superior sem escopo, é preciso adicionar uma entrada de função de gerenciamento à função. A entrada de função contém o nome do script e os parâmetros do script que você deseja tornar disponíveis à função.

O script deve residir no diretório Scripts no caminho de instalação do Microsoft Exchange Server 2013 em todos os servidores que executam um Exchange 2013 onde os usuários possam se conectar para executar o script. Se um usuário tiver acesso para executar um script, mas o script não estiver localizado no servidor do Exchange 2013 ao qual o usuário está conectado, ocorre um erro. Por padrão, o caminho para o diretório Scripts é C:\\Arquivos de Programas\\Microsoft\\Exchange Server\\V15\\Scripts.

Depois de copiar o script para os servidores apropriados do Exchange 2013 e decidir quais parâmetros do script devem ser usados, crie a entrada de função usando a sintaxe a seguir.

    Add-ManagementRoleEntry <unscoped top-level role name>\<script filename> -Parameters <parameter 1, parameter 2, parameter...> -Type Script -UnscopedTopLevel

Este exemplo adiciona o script BulkProvisionUsers.ps1 à função Scripts de TI com os parâmetros *Name* e *Location*.

    Add-ManagementRoleEntry "IT Scripts\BulkProvisionUsers.ps1" -Parameters Name, Location -Type Script -UnscopedTopLevel


> [!TIP]
> O cmdlet <STRONG>Add-ManagementRoleEntry</STRONG> realiza uma validação básica para garantir que você tenha adicionado apenas os parâmetros existentes no script. Entretanto, nenhuma outra validação é realizada depois que a entrada de função for adicionada. Se parâmetros forem adicionados ou removidos posteriormente, você terá que atualizar manualmente as entradas de função que contenham o script.



## Adicionar uma entrada de função de cmdlet não-Exchange a uma função de nível superior sem escopo

Se quiser adicionar um cmdlet não-Exchange a uma função sem escopo existente, use este procedimento. Se você quiser adicionar um script a uma função sem escopo existente, consulte a seção "Adicionar uma entrada de função de script a uma função de nível superior sem escopo" já mencionada neste tópico.

Para adicionar um cmdlet que não seja do Exchange a uma função de nível superior sem escopo, é preciso adicionar uma entrada de função de gerenciamento à função. A entrada de função contém o snap-in do cmdlet, o nome do cmdlet e os parâmetros do cmdlet que você deseja tornar disponível à função.

Se você adicionar cmdlets que não sejam do Exchange à nova função, os cmdlets deverão ser instalados em todos os servidores do Exchange 2013 nos quais os usuários possam se conectar para executar os cmdlets. Para aprender a instalar e registrar corretamente os snap-ins do Windows PowerShell que contêm os cmdlets que você deseja usar, consulte a documentação do Produto.

Após instalar o snap-in do Windows PowerShell que contém os cmdlets nos servidores do Exchange 2013 apropriados e decidir quais parâmetros do cmdlet devem ser usados, crie a entrada de função usando a sintaxe a seguir.

    Add-ManagementRoleEntry <unscoped top-level role name>\<cmdlet name> -PSSnapinName <snap-in name> -Parameters <parameter 1, parameter 2, parameter...> -Type Cmdlet -UnscopedTopLevel

Este exemplo adiciona o cmdlet **Set-WidgetConfiguration** no snap-in Contoso.Admin.Cmdlets à função Widget Cmdlets com os parâmetros *Database* e *Size*.

    Add-ManagementRoleEntry "Widget Cmdlets\Set-WidgetConfiguration" -PSSnapinName Contoso.Admin.Cmdlets -Parameters Database, Size -Type Cmdlet -UnscopedTopLevel


> [!TIP]
> O cmdlet <STRONG>Add-ManagementRoleEntry</STRONG> realiza uma validação básica para garantir que você tenha adicionado apenas os parâmetros existentes no cmdlet. Entretanto, nenhuma outra validação é realizada depois que a entrada de função for adicionada. Se o cmdlet for alterado posteriormente, e se parâmetros forem adicionados ou removidos, você terá que atualizar manualmente as entradas de função que contenham o cmdlet.



## Outras tarefas

Após adicionar uma entrada de função ou uma função de nível superior sem escopo, você poderá também:

[Adicionar uma entrada de função a uma função](add-a-role-entry-to-a-role-exchange-2013-help.md)

[Gerenciar grupos de função](manage-role-groups-exchange-2013-help.md)

[Gerenciar membros do grupo de função](manage-role-group-members-exchange-2013-help.md)

[Adicionar uma função a um usuário ou USG](add-a-role-to-a-user-or-usg-exchange-2013-help.md)

[Remover uma função de um usuário ou USG](remove-a-role-from-a-user-or-usg-exchange-2013-help.md)

