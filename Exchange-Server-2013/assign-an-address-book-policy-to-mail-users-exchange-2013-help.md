---
title: 'Atribuir uma política de catálogo de endereços para usuários de email: Exchange 2013 Help'
TOCTitle: Atribuir uma política de catálogo de endereços para usuários de email
ms:assetid: bdfe6575-24c0-47d0-9cfb-ece910db248b
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Hh529942(v=EXCHG.150)
ms:contentKeyID: 50486522
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Atribuir uma política de catálogo de endereços para usuários de email

 

_**Aplica-se a:** Exchange Online, Exchange Server 2013_

_**Tópico modificado em:** 2012-10-11_

Depois de criar uma política de catálogo de endereços (ABP), você deve atribuí-lo aos usuários de caixa de correio. Os usuários não estão atribuídos a uma ABP padrão quando sua conta de usuário é criada. Se você não atribuir uma ABP a um usuário, a lista de endereços global (GAL) para toda sua organização será acessível para o usuário por meio do Outlook e Outlook Web App. Para saber mais, consulte [Políticas de catálogo de endereços](address-book-policies-exchange-2013-help.md).

Para tarefas de gerenciamento adicionais relacionadas a ABPs, consulte [Procedimentos de política de catálogo de endereços](address-book-policy-procedures-exchange-2013-help.md).

Interessado em cenários que utilizam este procedimento? Consulte [Cenário: Implantando políticas de catálogo de endereços](scenario-deploying-address-book-policies-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: Menos de 5 minutos.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Políticas de catálogos de endereços" no tópico [Endereço de email e permissões do catálogo de endereços](email-address-and-address-book-permissions-exchange-2013-help.md).

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>.



## O que você deseja fazer?

## Usar o EAC para atribuir uma ABP a um usuário de caixa de correio

1.  Navegue até **Destinatários** \> **Caixas de Correio**.

2.  Na exibição de lista, selecione o usuário que você deseja atribuir a política e clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").

3.  Clique em **recursos de caixa de correio**.

4.  Na lista de **política de catálogo de endereços**, selecione a ABP que você deseja aplicar a este usuário.

5.  Clique em **Salvar**.

## Usar o EAC para atribuir uma ABP a vários usuários de caixa de correio

1.  Navegue até **Destinatários** \> **Caixas de Correio**.

2.  Na exibição de lista, use a tecla Ctrl para selecionar vários usuários.

3.  No painel de detalhes, clique em **Mais opções**.

4.  Em **Política de catálogo de endereços**, clique em **Atualizar**.

5.  Na lista **Selecione política de catálogo de endereços**, selecione a ABP que você deseja aplicar a esses usuários.

6.  Clique em **Salvar**.

## Use o Shell para atribuir uma ABP aos usuários de caixa de correio

Este exemplo atribui a All Fabrikam ABP para o existente da caixa de correio usuário joe@fabrikam.com.

    Set-Mailbox -Identity joe@fabrikam.com -AddressBookPolicy "All Fabrikam"

Este exemplo atribui a ABP\_EngineeringDepartment ABP a todos os usuários de caixa de correio cujo valor `CustomAttribute11` contém "Departamento de engenharia".

    Get-Mailbox -Filter {(CustomAttribute11 -like "Engineering Department")} | Set-Mailbox -AddressBookPolicy ABP_EngineeringDepartment

Para a sintaxe detalhada e informações sobre o parâmetro, consulte [Set-Mailbox](https://technet.microsoft.com/pt-br/library/bb123981\(v=exchg.150\)) e [Get-Mailbox](https://technet.microsoft.com/pt-br/library/bb123685\(v=exchg.150\)).

