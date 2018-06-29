---
title: 'Gerenciar membros do grupo de função: Exchange 2013 Help'
TOCTitle: Gerenciar membros do grupo de função
ms:assetid: c064729d-7cda-47fc-b105-acf4b300d430
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/JJ657492(v=EXCHG.150)
ms:contentKeyID: 50486543
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Gerenciar membros do grupo de função

 

_**Aplica-se a:**Exchange Online, Exchange Server 2013_

_**Tópico modificado em:**2012-10-08_

Este tópico mostra como adicionar, remover e exibir os membros de um grupo de função de gerenciamento Microsoft Exchange Server 2013. Para obter mais informações sobre grupos de função no Exchange 2013, consulte [Noções básicas sobre grupos de funções de gerenciamento](understanding-management-role-groups-exchange-2013-help.md).

Para tarefas de gerenciamento adicionais relacionadas a grupos de funções, consulte [Permissões](permissions-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para concluir cada procedimento: 5 minutos

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Grupos de função" no tópico [Permissões de gerenciamento de função](role-management-permissions-exchange-2013-help.md) .

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>.



## O que você deseja fazer?

## Adicionar membros a um grupo de funções

Para conceder as permissões que são concedidas por um grupo de funções de um usuário, você precisa adicionar o usuário, ou um grupo de segurança universal (USG) ou outro grupo de função que o usuário é um membro de, como membro do grupo de funções.

## Usar o EAC para adicionar membros a um grupo de funções

1.  No Exchange Centro de administração (EAC), navegue até **permissões** \> **Funções de administrador**.

2.  Selecione o grupo de função que você deseja adicionar membros e clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").

3.  Na seção **membros**, clique em **Adicionar**![Ícone Adicionar](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Ícone Adicionar").

4.  Selecione os usuários, USGs ou outros grupos de função que você deseja adicionar ao grupo de funções, clique em **Adicionar** e, em seguida, clique em **Okey**.

5.  Clique em **Salvar** para salvar as alterações feitas no grupo de funções.

## Use o Shell para adicionar membros a um grupo de funções

Para adicionar um membro do grupo de função, consulte a seção de [Examples](https://technet.microsoft.com/pt-br/dd638207\(exchg.150\)#examples) em [Add-RoleGroupMember](https://technet.microsoft.com/pt-br/library/dd638207\(v=exchg.150\)).

Para adicionar vários membros do grupo de função ou substituir a associação ao grupo de função inteiramente, consulte a seção de [Examples](https://technet.microsoft.com/pt-br/dd638116\(exchg.150\)#examples) em [Update-RoleGroupMember](https://technet.microsoft.com/pt-br/library/dd638116\(v=exchg.150\)).

## Como saber se funcionou?

Para verificar se adicionou com êxito um ou mais membros a um grupo de função, faça o seguinte:

1.  No EAC, navegue até **permissões** \> **Funções de administrador**.

2.  Selecione o grupo de função que você adicionou membros.

3.  No painel de detalhes do grupo de função, verifique se os membros que você adicionou estão listados.

## Remover membros de um grupo de funções

Para remover as permissões concedidas por um grupo de funções de um usuário, você precisa remover o usuário ou o grupo de segurança universal (USG) do usuário é um membro de, de associação do grupo de função.

## Usar o EAC para remover membros de um grupo de funções

1.  No EAC, navegue até **permissões** \> **Funções de administrador**.

2.  Selecione o grupo de função que você deseja remover membros de e clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").

3.  Na seção **membros**, selecione os membros que você deseja remover, clique em **Remover**![ícone Remover](images/JJ657492.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "ícone Remover")e, em seguida, clique em **Salvar**.

## Use o Shell para remover membros de um grupo de funções

Para remover um membro do grupo de função, consulte a seção de [Examples](https://technet.microsoft.com/pt-br/dd638208\(exchg.150\)#examples) em [Remove-RoleGroupMember](https://technet.microsoft.com/pt-br/library/dd638208\(v=exchg.150\)).

Para remover vários membros do grupo de função ou substituir a associação ao grupo de função inteiramente, consulte a seção de [Examples](https://technet.microsoft.com/pt-br/dd638116\(exchg.150\)#examples) em [Update-RoleGroupMember](https://technet.microsoft.com/pt-br/library/dd638116\(v=exchg.150\)).

## Como saber se funcionou?

Para verificar se você removeu com êxito um ou mais membros a um grupo de função, faça o seguinte:

1.  No EAC, navegue até **permissões** \> **Funções de administrador**.

2.  Selecione o grupo de função de que removeu membros.

3.  No painel de detalhes do grupo de função, verifique se que os membros que você removeu não são mais listados.

## Exibir os membros de um grupo de função

Os membros de um grupo de função são concedidos as permissões fornecidas pelas funções de gerenciamento atribuídas ao grupo de funções. Você pode exibir os membros de um grupo de funções para ver que quais usuários, grupos de segurança universal (USG) ou outros grupos de função são concedidos com permissões pelo grupo de função que você especificar.

## Use o EAC para exibir os membros de um grupo de função

1.  No EAC, navegue até **permissões** \> **Funções de administrador**.

2.  Selecione o grupo de funções do qual você deseja ver os membros.

3.  No painel de detalhes do grupo de função, exiba os membros no painel de detalhes do grupo de função.

## Use o Shell para exibir os membros de um grupo de função

Para exibir os membros de um grupo de função, consulte a seção "Exemplos" em [Get-RoleGroupMember](https://technet.microsoft.com/pt-br/library/dd638093\(v=exchg.150\)).

