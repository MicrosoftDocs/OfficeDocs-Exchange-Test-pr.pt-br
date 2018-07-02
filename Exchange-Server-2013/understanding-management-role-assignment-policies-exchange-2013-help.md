---
title: 'Noções básicas sobre diretivas de atribuição de função de gerenciamento: Exchange 2013 Help'
TOCTitle: Noções básicas sobre diretivas de atribuição de função de gerenciamento
ms:assetid: 25913e43-326a-4371-90b5-021a35f100fe
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Dd638100(v=EXCHG.150)
ms:contentKeyID: 50485200
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Noções básicas sobre diretivas de atribuição de função de gerenciamento

 

_**Aplica-se a:** Exchange Online, Exchange Server 2013_

_**Tópico modificado em:** 2015-03-09_

Uma *diretiva de atribuição de função de gerenciamento* é uma coleção de uma ou mais funções de gerenciamento de usuários finais que permitem a esses usuários gerenciar suas próprias configurações de grupo de distribuição e caixa de correio do Microsoft Exchange Server 2013. As diretivas de atribuição de função, que são parte do modelo de permissões RBAC (controle de acesso baseado na função) no Exchange 2013, permitem controlar quais configurações de grupo de distribuição e caixa de correio específicas seus usuários finais poderão modificar. Grupos de usuários diferentes podem ter diretivas de atribuição de função especializadas para eles.


> [!TIP]
> Este tópico concentra-se na funcionalidade avançada de RBAC. Se você quiser gerenciar permissões básicas do Exchange 2013, como usar o Centro de Administração do Exchange (EAC) para adicionar e remover membros de grupos de funções, criar e modificar grupos de funções ou criar e modificar políticas de atribuição de função, consulte <A href="permissions-exchange-2013-help.md">Permissões</A>.



Para mais informações sobre o RBAC, consulte [Controle de acesso baseado em função de compreensão](understanding-role-based-access-control-exchange-2013-help.md).

**Sumário**

Role assignment policy layers

Default and explicit role assignment policies

Using role assignment policies

Role assignment policy management

## Camadas de diretiva de atribuição de função

A lista a seguir descreve as camadas que compõem o modelo de diretiva de atribuição de função:

  - **Caixa de correio**   Uma única diretiva de atribuição de função é atribuída às caixas de correio. Quando uma caixa de correio é atribuída a uma diretiva de atribuição de função, as atribuições entre as funções de gerenciamento e a diretiva de atribuição de função são aplicadas à caixa de correio. Isso concede à caixa de correio todas as permissões oferecidas pelas funções de gerenciamento.

  - **Diretiva de atribuição de função de gerenciamento**   A *diretiva de atribuição de função de gerenciamento* é um objeto especial no Exchange 2013. Os usuários são associados a uma diretiva de atribuição de função quando suas caixas de correio são criadas, ou se você alterar a diretiva de atribuição de função em uma caixa de correio. Também é a ela que você atribui funções de gerenciamento de usuário final. A combinação de todas as funções em uma diretiva de atribuição de função define tudo o que o usuário pode gerenciar em sua caixa de correio ou em seus grupos de distribuição.

  - **Atribuição de função de gerenciamento**   Uma *atribuição de função de gerenciamento* é o vínculo entre uma função de gerenciamento e uma diretiva de atribuição de função. Atribuir uma função de gerenciamento a uma diretiva de atribuição de função concede a capacidade de usar cmdlets e parâmetros definidos na função de gerenciamento. Ao criar uma atribuição de função entre uma diretiva de atribuição de função e uma função de gerenciamento, não é possível especificar um escopo. O escopo aplicado pela atribuição baseia-se na função de gerenciamento e é `Self` ou `MyGAL`. Para mais informações, consulte [Noções básicas sobre as atribuições de função de gerenciamento](understanding-management-role-assignments-exchange-2013-help.md).

  - **Função de gerenciamento**   Uma *função de gerenciamento* é um contêiner para um agrupamento de entradas de função de gerenciamento. As funções são usadas para definir as tarefas específicas que um usuário pode realizar em sua caixa de correio ou em seus grupos de distribuição. Uma *entrada de função de gerenciamento* é um cmdlet, script ou permissão especial que permite que cada tarefa especificada em uma função de gerenciamento seja realizada. Só é possível usar funções de gerenciamento com diretivas de atribuição de função. Para mais informações, consulte [Noções básicas sobre funções de gerenciamento](understanding-management-roles-exchange-2013-help.md).

  - **Entrada de função de gerenciamento**   As entradas de função de gerenciamento são as entradas individuais em uma função de gerenciamento que determinam quais cmdlets e parâmetros estão disponíveis à função de gerenciamento e ao grupo de função. Cada entrada de função consiste em um único cmdlet e nos parâmetros que podem ser acessados pela função de gerenciamento.

A imagem a seguir mostra cada camada de diretiva de atribuição de função na lista anterior e como cada camada se relaciona à outra.

**Modelo de diretiva de atribuição de função de gerenciamento**

![Relacionamentos do Modelo de Atribuição de Função](images/Dd638100.7f7c11ca-0d61-464d-98a3-a9991ec811b5(EXCHG.150).jpg "Relacionamentos do Modelo de Atribuição de Função")

Para mais informações sobre funções de gerenciamento, atribuições de função e escopos, consulte [Controle de acesso baseado em função de compreensão](understanding-role-based-access-control-exchange-2013-help.md).

## Diretivas de atribuição de função explícitas e padrão

As seções a seguir descrevem os dois tipos de diretivas de atribuição de função no Exchange 2013.

## Diretiva de atribuição de função padrão

Uma diretiva de atribuição de função padrão é aquela que é atribuída a uma caixa de correio quando a caixa de correio é criada ou movida para um servidor que executa o Exchange 2013, e uma diretiva de atribuição de função não foi fornecida usando o parâmetro *RoleAssignmentPolicy* nos cmdlets **New-Mailbox** ou **Enable-Mailbox**.

O Exchange 2013 inclui uma diretiva de atribuição de função padrão que oferece aos usuários finais as permissões de uso mais comum. As permissões padrão podem ser alteradas na diretiva de atribuição de função padrão adicionando funções de gerenciamento a ela ou removendo-as.

Se você quiser substituir a diretiva de atribuição de função padrão integrada pela sua própria diretiva de atribuição de função padrão, use o cmdlet **Set-RoleAssignmentPolicy** para selecionar um novo padrão. Ao fazer isso, as caixas de correio novas são atribuídas à diretiva de atribuição de função especificada por padrão, caso uma diretiva de atribuição de função não seja especificada explicitamente.

Quando você altera a diretiva de atribuição de função padrão, as caixas de correio atribuídas à diretiva de atribuição de função padrão não são atribuídas automaticamente à nova diretiva de atribuição de função padrão. Se quiser atualizar caixas de correio criadas anteriormente para que usem a diretiva de atribuição de função que você definiu como padrão, use o cmdlet **Set-Mailbox** para isso.

## Diretiva de Atribuição de Função Explícita

Uma diretiva de atribuição de função explícita é uma diretiva que você atribui a uma caixa de correio manualmente usando o parâmetro *RoleAssignmentPolicy* nos cmdlets **New-Mailbox**, **Set-Mailbox** ou **Enable-Mailbox**. Ao atribuir uma diretiva de atribuição de função explícita, a nova diretiva tem efeito imediato e substitui a diretiva de atribuição de função explícita atribuída anteriormente.

## Usando diretivas de atribuição de função

As diretivas de atribuição de função permitem adaptar as permissões com base nas necessidades empresariais seus usuários precisam ser capazes de configurar. Se a diretiva de atribuição de função padrão atender às suas necessidades, não será preciso fazer mais personalizações. No entanto, se você tiver muitos grupos de usuários diferentes com necessidades especializadas, é possível criar diretivas de atribuição de função para cada um deles.

A diretiva de atribuição de função padrão que você usa deve conter as permissões que se aplicam ao maior grupo de seus usuários. Em seguida, crie diretivas de atribuição de função para cada grupo especializado de usuários e adapte essas diretivas de atribuição de função para conceder mais ou menos permissões restritivas a eles. Ao organizar suas diretivas de atribuição de função dessa forma, você reduz a complexidade atribuindo explicitamente apenas diretivas de atribuição de função aos seus usuários especializados, enquanto a maior parte de seus usuários recebe as permissões mais comuns fornecidas pela diretiva de atribuição de função padrão.

Uma caixa de correio pode ter apenas uma diretiva de atribuição de função. A todos os usuários, incluindo os administradores e usuários especialistas, é atribuída uma diretiva de atribuição de função. Se quiser que um usuário tenha um conjunto diferente de permissões, atribua à caixa de correio do usuário outra diretiva de atribuição de função com as permissões exigidas.

## Gerenciamento de diretiva de atribuição de função

Para adicionar uma nova diretiva de atribuição de função, crie uma primeiro e decida se ela deve ser a diretiva de atribuição de função padrão. Depois de criar uma diretiva de atribuição de função, atribua funções de gerenciamento à diretiva de atribuição de função e atribua a diretiva de atribuição de função às caixas de correio. Mais tarde, você poderá adicionar ou remover funções de gerenciamento ou escolher uma diretiva de atribuição de função diferente como padrão.

A tabela a seguir lista a camada de diretiva de atribuição de função e os tópicos sobre os procedimentos que podem ser usados no gerenciamento de cada camada.

### Tópicos de gerenciamento de diretiva de atribuição de função

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Camada de modelo de diretiva de atribuição de função</th>
<th>Tópicos de gerenciamento</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Caixa de Correio</p></td>
<td><p><a href="manage-user-mailboxes-exchange-2013-help.md">Gerenciar caixas de correio do usuário</a></p>
<p><a href="change-the-assignment-policy-on-a-mailbox-exchange-2013-help.md">Alterar a política de atribuição de uma caixa de correio</a></p></td>
</tr>
<tr class="even">
<td><p>Diretiva de atribuição de função</p></td>
<td><p><a href="manage-role-assignment-policies-exchange-2013-help.md">Gerenciar políticas de atribuição de função</a></p>
<p></p></td>
</tr>
<tr class="odd">
<td><p>Funções de gerenciamento e atribuições</p></td>
<td><p><a href="manage-role-assignment-policies-exchange-2013-help.md">Gerenciar políticas de atribuição de função</a></p>
<p></p></td>
</tr>
<tr class="even">
<td><p>Entradas de função de gerenciamento</p></td>
<td><p><a href="add-a-role-entry-to-a-role-exchange-2013-help.md">Adicionar uma entrada de função a uma função</a></p>
<p><a href="change-a-role-entry-exchange-2013-help.md">Alterar uma entrada de função</a></p>
<p><a href="remove-a-role-entry-from-a-role-exchange-2013-help.md">Remover uma entrada de função de uma função</a></p>

> [!TIP]
> Alterar as entradas de função de gerenciamento nas funções de gerenciamento em uma diretiva de atribuição de função é uma tarefa avançada e na maioria dos caso não é exigida. Você pode, em vez disso, ser capaz de usar uma função de gerenciamento pré-existente adequada às suas necessidades. Para mais informações, consulte <A href="built-in-role-groups-exchange-2013-help.md">Grupos de funções internos</A>.


</td>
</tr>
</tbody>
</table>

