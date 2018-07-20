﻿---
title: 'Função MyName: Exchange 2013 Help'
TOCTitle: Função MyName
ms:assetid: 6c8320d3-7a71-4975-b8b3-c1b1b52dd7df
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Ff461931(v=EXCHG.150)
ms:contentKeyID: 50485889
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Função MyName

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2012-10-17_

A função de gerenciamento `MyName` permite que usuários individuais exibam e modifiquem seu nome completo e seu campo de anotações. Esta é uma função personalizada criada a partir da função pai [Função MyProfileInformation](myprofileinformation-role-exchange-2013-help.md)

A função de gerenciamento é uma das várias funções internas no modelo de permissões do Controle de Acesso Baseado na Função (RBAC) no Microsoft Exchange Server 2013. As funções de gerenciamento, que são atribuídas a um ou mais grupos de funções de gerenciamento, políticas de atribuição de funções de gerenciamento, usuários ou grupos de segurança universal (USG), agem como um agrupamento lógico de cmdlets ou scripts que são combinados para permitir acesso para ver ou modificar a configuração de componentes do Exchange 2013, como bancos de dados de caixas de correio, regras de transporte e destinatários. Se um cmdlet ou um script e seus parâmetros, chamados em conjunto de entrada de função de gerenciamento, estiverem incluídos em uma função, o cmdlet ou o script e seus parâmetros podem ser executados por aqueles a quem a função foi atribuída.

Essa função é um tipo específico de função chamada uma função personalizada. Uma função personalizada é uma que é criada, ou derivada de uma função pai. Ela contém um conjunto de entradas de função de gerenciamento que existe na função pai. Esta função é fornecida para possibilitar o controle, com grande nível de granularidade, das informações que os usuários finais podem modificar em suas próprias caixas de correio. Ao contrário das outras funções internas, funções personalizadas, incluindo esta, podem ser excluídas. Se esta função não for utilizada, pode ser excluída.

Para mais informações sobre as funções de gerenciamento personalizadas internas e entradas de função de gerenciamento, confira [Noções básicas sobre funções de gerenciamento](understanding-management-roles-exchange-2013-help.md).

Para mais informações sobre funções de gerenciamento, grupos de funções e outros componentes do RBAC, confira [Controle de acesso baseado em função de compreensão](understanding-role-based-access-control-exchange-2013-help.md).

## Atribuições da função de gerenciamento

Para que esta função conceda permissões, deve ser atribuída a um destinatário de função, como uma diretiva de atribuição de função. Esta atribuição é feita usando atribuições de função de gerenciamento. Atribuições de função vinculam destinatários de função e funções juntos. Se mais de uma função for atribuída a um destinatário de função, a ele será concedida a combinação de todas as permissões concedidas por todas as funções atribuídas.


> [!TIP]
> Também é possível atribuir esta função de gerenciamento a um grupo de função, USG, ou diretamente a um usuário. No entanto, as funções destacadas para o usuário são mais eficazes quando usadas com diretivas de atribuição de função.



Esta função destacada para o usuário tem escopos implícitos que não podem ser modificados. Portanto, você deve adicionar escopos personalizados a atribuições de função que atribuem esta função às diretivas de atribuição de função, grupos de função, USGs, ou usuários.

Para mais informações sobre atribuições de função e escopos, confira os seguintes tópicos:

  - [Noções básicas sobre as atribuições de função de gerenciamento](understanding-management-role-assignments-exchange-2013-help.md)

  - [Noções básicas sobre escopos da função de gerenciamento](understanding-management-role-scopes-exchange-2013-help.md)

Esta função pode ser atribuída a uma ou mais diretivas de atribuição de função, por padrão. Para saber mais, confira a seção "Atribuições de Função de Gerenciamento Padrão".

Se você quiser exibir uma lista de grupos de funções, usuários ou USGs atribuídos a essa função, use o comando abaixo.

    Get-ManagementRoleAssignment -Role "<role name>"

## Atribuições de função comuns e de delegação

Essa função pode ser atribuída aos destinatários de função com o uso de atribuições de função regulares ou de delegação. As atribuições regulares de função concedem as permissões fornecidas pela função ao destinatário da função. As atribuições de função de delegação concedem a um destinatário de função a capacidade de atribuir a função a outros destinatários de função. Para saber mais sobre atribuições de função regulares e de delegação, consulte [Noções básicas sobre as atribuições de função de gerenciamento](understanding-management-role-assignments-exchange-2013-help.md).

## Adicionar ou remover atribuições de função

Você pode alterar a quais destinatários será atribuída essa função. Alterando a qual destinatário a função é atribuída, você altera quem recebe suas permissões. Você pode atribuir essa função a outras diretivas de atribuição de função internos ou pode criar diretivas de função e atribuir essa função a elas.

Para atribuir esta função aos administradores, suas funções principais devem ser atribuídas a um grupo de funções da qual você é um membro, diretamente para você ou para USG que você é um membro, usando a atribuição de função de delegação. Para mais informações sobre delegar as atribuições de função, confira a seção "Atribuições de Funções Regulares e de Delegação".

Você também pode remover esta função da diretiva de atribuição padrão, diretivas de atribuição da função e grupos de função que você cria, usuários e USGs.

Para mais informações sobre como adicionar ou remover atribuições entre essa função e grupos, usuários e USGs da função, confira estes tópicos:

  - Seção "Adicionar ou remover uma função de um grupo de função" em [Gerenciar grupos de função](manage-role-groups-exchange-2013-help.md)

  - [Adicionar uma função a um usuário ou USG](add-a-role-to-a-user-or-usg-exchange-2013-help.md)

  - [Remover uma função de um usuário ou USG](remove-a-role-from-a-user-or-usg-exchange-2013-help.md)

## Habilitar ou desabilitar atribuições de função

Ao habilitar ou desabilitar uma atribuição de função, você controla se a atribuição de função deve entrar em vigor. Se a atribuição de função estiver desabilitada, as permissões concedidas pela função associada não serão aplicadas ao destinatário da função. Isso é conveniente se você quiser remover permissões temporariamente sem delegar uma atribuição de função. Para saber mais, confira [Alterar uma atribuição de função](change-a-role-assignment-exchange-2013-help.md).

## Atribuições de função de gerenciamento padrão

Esta função não tem quaisquer atribuições de função padrão. Ela é oferecida no caso de se desejar controlar, em um nível mais granular, quais informações de usuário final seus usuários podem modificar. Para saber mais sobre a atribuição desta função a uma política de atribuição de função, consulte a seção "Adicionando ou removendo atribuições de função".

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


