---
title: 'Configurar o grupo de usuários que podem ser contatados: Exchange 2013 Help'
TOCTitle: Configurar o grupo de usuários que podem ser contatados
ms:assetid: 45d9d6d5-c9d6-4b73-8aa2-a23599a4381c
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Ee423545(v=EXCHG.150)
ms:contentKeyID: 52058414
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configurar o grupo de usuários que podem ser contatados

 

_**Aplica-se a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Tópico modificado em:** 2012-12-09_

Você pode especificar o grupo de usuários que os chamadores podem contatar ao chamarem um atendedor automático da UM (Unificação de Mensagens). Por padrão, os chamadores podem entrar em contato com usuários no mesmo plano de discagem associado ao atendedor automático da UM. Entretanto, é possível alterar o grupo de usuários para permitir que chamadores transfiram chamadas ou enviem mensagens de voz para usuários localizados no catálogo de endereços da organização ou para um conjunto de usuários específico.

Para conhecer tarefas de gerenciamento adicionais relacionadas a atendedores automáticos de UM, consulte [Gerenciar um atendedor automático](manage-a-um-auto-attendant-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: Menos de 1 minuto.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Atendedores automáticos de UM", no tópico [Permissões de mensagens unificadas](unified-messaging-permissions-exchange-2013-help.md).

  - Antes de executar esses procedimentos, confirme se um plano de discagem de UM foi criado. Para conhecer etapas detalhadas, consulte [Criar um plano de discagem de UM](create-a-um-dial-plan-exchange-2013-help.md).

  - Antes de executar esses procedimentos, verifique se um plano de discagem de UM foi criado. Para conhecer etapas detalhadas, consulte [Criar um Atendedor Automático da UM](create-a-um-auto-attendant-exchange-2013-help.md).

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>..



## O que você deseja fazer?

## Usar o EAC para configurar o grupo de usuários que os chamadores podem contatar

1.  No EAC, navegue até **Unificação de Mensagens** \> **Planos de discagem de UM**. Na exibição de lista, selecione o plano de discagem de UM que você deseja modificar e clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").

2.  Na página **Plano de Discagem da UM**, em **Atendedores Automáticos da UM**, selecione o atendedor automático da UM que deseja alterar e clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").

3.  Na página **Atendedor Automático da UM** \> **Catálogo de endereços e acesso de operador**, em **Opções para pesquisa do catálogo de endereços**, escolha uma destas opções:
    
      - **Neste plano de discagem apenas**   Selecione essa opção para permitir que os chamadores que ligarem para o atendedor automático da UM localizem e contatem usuários que estejam no mesmo plano de discagem associado ao atendedor automático da UM.
    
      - **Em toda a organização**   Selecione essa opção para permitir que os chamadores que ligarem para o atendedor automático da UM localizem e contatem qualquer pessoa incluída no catálogo de endereços da organização. Isso inclui todos os usuários habilitados para caixa de correio.

4.  Clique em **Salvar**.

## Usar o Shell para configurar o grupo de usuários que os chamadores podem contatar

Este exemplo configura o escopo de usuários que os chamadores podem contatar como todos os usuários do catálogo de endereços da organização em um atendedor automático da UM chamado `MyUMAutoAttendant`.

    Set-UMAutoAttendant -Identity MyUMAutoAttendant -ContactScope GlobalAddressList

