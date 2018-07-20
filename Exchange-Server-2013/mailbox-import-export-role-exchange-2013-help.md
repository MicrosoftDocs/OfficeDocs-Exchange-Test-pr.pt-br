---
title: 'Função Importar Exportar Caixa de Correio: Exchange 2013 Help'
TOCTitle: Função Importar Exportar Caixa de Correio
ms:assetid: d7cdce7a-6c46-4750-b237-d1c1773e8d28
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Ee633482(v=EXCHG.150)
ms:contentKeyID: 50486750
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Função Importar Exportar Caixa de Correio

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2015-03-09_

A função de gerenciamento `Mailbox Import Export` permite que administradores importem e exportem conteúdo de caixa de correio e removam seu conteúdo indesejado.

A função de gerenciamento é uma das várias funções internas no modelo de permissões do Controle de Acesso Baseado na Função (RBAC) no Microsoft Exchange Server 2013. As funções de gerenciamento, que são atribuídas a um ou mais grupos de função de gerenciamento, políticas de atribuição de função de gerenciamento, usuários ou grupos de segurança universal (USG), agem como um agrupamento lógico de cmdlets ou scripts que são combinados para permitir acesso para ver ou modificar a configuração de componentes do Exchange 2013, como bancos de dados de caixas de correio, regras de transporte e destinatários. Se um cmdlet ou um script e seus parâmetros, chamados em conjunto de entrada de função de gerenciamento, estiverem incluídos em uma função, o cmdlet ou o script e seus parâmetros podem ser executados por aqueles a quem a função foi atribuída. Para mais informações sobre as funções de gerenciamento e entradas de função de gerenciamento, confira [Noções básicas sobre funções de gerenciamento](understanding-management-roles-exchange-2013-help.md).

Para mais informações sobre funções de gerenciamento, grupos de funções e outros componentes do RBAC, confira [Controle de acesso baseado em função de compreensão](understanding-role-based-access-control-exchange-2013-help.md).

## Atribuições da função de gerenciamento

Para essa função conceder permissões, ela deve ser atribuída a um destinatário de função, que pode ser um grupo de funções, usuário ou grupo de segurança universal (USG). Esta atribuição é feita usando atribuições de função de gerenciamento. Atribuições de função vinculam destinatários de função e funções juntos. Se mais de uma função for atribuída a um destinatário de função, a ele será concedida a combinação de todas as permissões concedidas por todas as funções atribuídas.

Além de vincular destinatários de função a funções, as atribuições de função podem também aplicar escopos de gerenciamento internos ou personalizados. Os escopos de gerenciamento controlam quais destinatários, servidores e objetos de banco de dados podem ser modificados pelos destinatários de função. Se a função for atribuída a um destinatário de função, mas um escopo de gerenciamento permitir que o destinatário de função gerencie somente alguns objetos, com base em um escopo definido, o destinatário de função poderá usar somente as permissões concedidas por essa função nos objetos específicos. As permissões fornecidas pela função não podem ser aplicadas aos objetos fora do escopo definido na atribuição de funções. Para mais informações sobre atribuições de função e escopos, confira os seguintes tópicos:

  - [Noções básicas sobre as atribuições de função de gerenciamento](understanding-management-role-assignments-exchange-2013-help.md)

  - [Noções básicas sobre escopos da função de gerenciamento](understanding-management-role-scopes-exchange-2013-help.md)

Esta função é atribuída a um ou mais grupos de função, por padrão. Para saber mais, confira a seção "Atribuições de Função Apenas para Delegação" mais adiante neste tópico.

Se você quiser exibir uma lista de grupos de funções, usuários ou USGs atribuídos a essa função, use o comando abaixo.

    Get-ManagementRoleAssignment -Role "<role name>"

## Atribuições de função comuns e de delegação

Essa função pode ser atribuída aos destinatários de função com o uso de atribuições de função regulares ou de delegação. As atribuições regulares de função concedem as permissões fornecidas pela função ao destinatário da função. As atribuições de função de delegação concedem a um destinatário de função a capacidade de atribuir a função a outros destinatários de função. Para saber mais sobre atribuições de função regulares e de delegação, consulte [Noções básicas sobre as atribuições de função de gerenciamento](understanding-management-role-assignments-exchange-2013-help.md).

## Adicionar ou remover atribuições de função

Você pode alterar a quais destinatários será atribuída essa função. Alterando a qual destinatário a função é atribuída, você altera quem recebe suas permissões. Você pode atribuir essa função a outros grupos de função internos ou pode criar grupos de função e atribuir essa função a eles. Você também pode atribuir esta função a usuários ou USGs. Entretanto, recomendamos que você limite a atribuição de funções a usuários e USGs, pois essas atribuições podem aumentar muito a complexidade do seu modelo de permissões.

Para atribuir essa função aos destinatários, a função deve ser atribuída a um grupo de função do qual você seja membro, ou diretamente a você ou a um USG do qual você seja membro, usando uma atribuição de função de delegação. Para mais informações sobre delegar as atribuições de função, confira a seção "Atribuições de Funções Regulares e de Delegação".

Você também pode remover essa função de grupos de função internos, grupos de função que você criar, usuários e USGs. Entretanto, deve sempre haver pelo menos uma atribuição de função de delegação entre essa função e um grupo de função ou USG. Não é possível excluir a última atribuição de função de delegação. Essa limitação ajuda a impedir que você mesmo bloqueie a sua entrada no sistema.


> [!IMPORTANT]
> Deve haver pelo menos uma atribuição de função de delegação entre essa função e um grupo de função ou USG. Você não pode remover a última atribuição de função de delegação associada a essa função, se a última atribuição tiver sido a um usuário.



Para mais informações sobre como adicionar ou remover atribuições entre essa função e grupos, usuários e USGs da função, confira estes tópicos:

  - [Gerenciar grupos de função](manage-role-groups-exchange-2013-help.md)

  - [Adicionar uma função a um usuário ou USG](add-a-role-to-a-user-or-usg-exchange-2013-help.md)

  - [Remover uma função de um usuário ou USG](remove-a-role-from-a-user-or-usg-exchange-2013-help.md)

## Alterar os escopos de gerenciamento para atribuições de função

Você também pode alterar os escopos de gerenciamento em atribuições de função existentes entre essa função e os destinatários da função. Alterando os escopos nas atribuições de função, você controla que objetos podem ser gerenciados usando-se as permissões fornecidas por essa função. Você tem várias opções ao alterar o escopo de uma atribuição de função. Você pode selecionar uma destas opções:

  - Adicione um novo escopo personalizado usando o cmdlet **Set-ManagementRoleAssignment**. Para saber mais, confira os seguintes tópicos:
    
      - [Criar um escopo regular ou exclusivo](create-a-regular-or-exclusive-scope-exchange-2013-help.md)
    
      - [Alterar uma atribuição de função](change-a-role-assignment-exchange-2013-help.md)

  - Adicionar ou alterar um escopo de unidade organizacional usando o cmdlet **Set-ManagementRoleAssignment**. Para saber mais, confira [Alterar uma atribuição de função](change-a-role-assignment-exchange-2013-help.md).

  - Adicionar ou alterar um escopo predefinido usando o cmdlet **Set-ManagementRoleAssignment**. Para saber mais, confira [Alterar uma atribuição de função](change-a-role-assignment-exchange-2013-help.md).

  - Alterar o destinatário, servidor, ou escopo de banco de dados em um escopo personalizado associado a uma atribuição de função usando o cmdlet **Set-ManagementScope**. Para saber mais, confira [Alterar um escopo de função](change-a-role-scope-exchange-2013-help.md).

## Habilitar ou desabilitar atribuições de função

Ao habilitar ou desabilitar uma atribuição de função, você controla se a atribuição de função deve entrar em vigor. Se a atribuição de função estiver desabilitada, as permissões concedidas pela função associada não serão aplicadas ao destinatário da função. Isso é conveniente se você quiser remover permissões temporariamente sem delegar uma atribuição de função. Para saber mais, confira [Alterar uma atribuição de função](change-a-role-assignment-exchange-2013-help.md).

## Atribuições de função de gerenciamento padrão

Essa função tem atribuições de função para um ou mais destinatários de função. A tabela a seguir indica se a atribuição de função é regular ou de delegação e também indica os escopos de gerenciamento aplicados a cada atribuição. A lista a seguir descreve cada coluna:

  - **Atribuição regular**   As atribuições regulares de função habilitam o destinatário da função a acessar as permissões fornecidas pelas entradas da função de gerenciamento na função.

  - **Atribuição de delegação**   As atribuições de delegação de função habilitam o destinatário da função a atribuir a função a grupos, usuários ou USGs de função.

  - **Escopo de leitura do destinatário**   O escopo de leitura do destinatário determina quais objetos de destinatário o destinatário terá permissão para ler do Active Directory.

  - **Escopo de gravação do destinatário**   O escopo de gravação do destinatário determina quais objetos de destinatário o destinatário terá permissão para modificar no Active Directory.

  - **Escopo de leitura da configuração**   O escopo de leitura da configuração determina quais configurações e objetos de servidor o destinatário terá permissão para ler do Active Directory.

  - **Escopo de gravação da configuração**   O escopo de gravação da configuração determina quais objetos de servidor e organizacionais o destinatário terá permissão para modificar no Active Directory.

### Atribuições de função de gerenciamento padrão desta função

<table style="width:100%;">
<colgroup>
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
</colgroup>
<thead>
<tr class="header">
<th>Grupo de função</th>
<th>Atribuição comum</th>
<th>Atribuição de delegação</th>
<th>Escopo de leitura do destinatário</th>
<th>Escopo de gravação do destinatário</th>
<th>Escopo de leitura da configuração</th>
<th>Escopo de gravação do destinatário</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="organization-management-exchange-2013-help.md">Gerenciamento da Organização</a></p></td>
<td><p></p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
</tbody>
</table>


## Personalização da função de gerenciamento

Essa função foi configurada para oferecer, a um destinatário de função, todos os cmdlets e parâmetros necessários para gerenciar os recursos e componentes listados no início deste tópico. Outras funções também foram fornecidas para habilitar o gerenciamento de outros recursos. Ao adicionar e remover funções de grupos de funções, você pode criar um modelo de permissões personalizadas sem a necessidade de personalizar funções de gerenciamento individuais. Para uma lista completa de funções, confira [Funções de gerenciamento internas](built-in-management-roles-exchange-2013-help.md). Para mais informações sobre como personalizar grupos de funções, confira [Gerenciar grupos de função](manage-role-groups-exchange-2013-help.md).

Se você precisar criar uma versão personalizada desta função, você deverá criar uma função como uma filha daquela função e personalizar essa nova função.


> [!WARNING]
> As informações a seguir permitem que você execute o gerenciamento avançado de permissões. Personalizar funções de gerenciamento pode aumentar significativamente a complexidade do seu modelo de permissões. Você pode fazer com que determinados recursos parem de funcionar, se você substituir uma função de gerenciamento interna por uma função personalizada configurada incorretamente.



Estas são as etapas mais comuns para se criar uma função personalizada e atribuí-la a um destinatário de função:

1.  Criar uma cópia dessa função. Para saber mais, confira [Criar uma função](create-a-role-exchange-2013-help.md).

2.  Alterar ou remover as entradas de função na nova função, usando os cmdlets **Set-ManagementRoleEntry** e **Remove-ManagementRoleEntry**. Você não pode adicionar entradas de função à nova função porque ela só pode conter as entradas internas da função-mãe. Para saber mais, confira os seguintes tópicos:
    
      - [Alterar uma entrada de função](change-a-role-entry-exchange-2013-help.md)
    
      - [Remover uma entrada de função de uma função](remove-a-role-entry-from-a-role-exchange-2013-help.md)

3.  Se você quiser substituir a função interna por essa nova função personalizada, remova quaisquer atribuições de função associadas à função interna. Para saber mais, confira os seguintes tópicos:
    
      - Seção "Adicionar ou remover uma função de um grupo de função" em [Gerenciar grupos de função](manage-role-groups-exchange-2013-help.md)
    
      - [Remover uma função de um usuário ou USG](remove-a-role-from-a-user-or-usg-exchange-2013-help.md)

4.  Adicionar a nova função personalizada aos destinatários de função necessários. Para saber mais, confira os seguintes tópicos:
    
      - Seção "Adicionar ou remover uma função de um grupo de função" em [Gerenciar grupos de função](manage-role-groups-exchange-2013-help.md)
    
      - [Adicionar uma função a um usuário ou USG](add-a-role-to-a-user-or-usg-exchange-2013-help.md)
        

        > [!IMPORTANT]
        > Se você quiser que outros usuários, além daquele que criou a função, possa atribuir a nova função personalizada, certifique-se de adicionar uma atribuição de função de delegação para um destinatário de função, pelo menos. Para saber mais, confira <A href="delegate-role-assignments-exchange-2013-help.md">Atribuições de função de representante</A>.


