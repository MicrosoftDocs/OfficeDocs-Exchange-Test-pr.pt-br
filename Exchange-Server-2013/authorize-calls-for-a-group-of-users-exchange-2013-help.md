---
title: 'Autorizar chamadas para um grupo de usuários: Exchange 2013 Help'
TOCTitle: Autorizar chamadas para um grupo de usuários
ms:assetid: 7fc36757-868c-4bde-b793-6ae630da155c
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Bb232099(v=EXCHG.150)
ms:contentKeyID: 51407889
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Autorizar chamadas para um grupo de usuários

 

_**Aplica-se a:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Tópico modificado em:**2013-02-21_

Você pode habilitar autorizações de discagem em uma diretiva de caixa de correio de Unificação de mensagens (UM). Você pode usar autorizações de discagem em uma diretiva de caixa de correio para proibir que os usuários autenticados do Outlook Voice Access vinculadas à diretiva de caixa de correio de Unificação de mensagens de fazer chamadas telefônicas de país/região ou internacionais ou *discagem externa*. Discagem externa acontece quando Unified Messaging faz uma chamada de saída para um usuário depois que eles tenham chamado para um número de telefone do Outlook Voice Access que está configurado em um plano de discagem de UM. Quando você configura uma configuração em uma diretiva de caixa de correio de Unificação de mensagens, que a configuração se aplica a todos os usuários habilitados para UM vinculada com a diretiva de caixa de correio de Unificação de mensagens.

Para conhecer tarefas de gerenciamento adicionais relacionadas à discagem externa, consulte [Permitindo que usuários façam chamadas de procedimentos](allowing-users-to-make-calls-procedures-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: Menos de 1 minuto.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Diretivas de caixa de correio da UM" no tópico [Permissões de mensagens unificadas](unified-messaging-permissions-exchange-2013-help.md).

  - Antes de executar esses procedimentos, verifique se uma política de caixa de correio de UM foi criada. Para obter etapas detalhadas, consulte [Criar uma política de caixa de correio da UM](create-a-um-mailbox-policy-exchange-2013-help.md).

  - Antes de executar esses procedimentos, confirme que as regras de discagem do país/região e internacionais foram criadas em um plano de discagem de UM. Para obter etapas detalhadas, consulte [Criar regras de discagem para usuários](create-dialing-rules-for-users-exchange-2013-help.md).

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>..



## O que você deseja fazer?

## Usar o EAC para habilitar autorizações de discagem em uma diretiva de caixa de correio de Unificação de mensagens para grupos de regras de discagem do país/região

1.  No EAC, navegue até **Unificação de Mensagens** \> **Planos de discagem de UM**. Na exibição de lista, selecione o plano de discagem de UM que você deseja modificar e clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").

2.  Na página de **Plano de discagem de UM**, em **Diretivas de caixa de correio de UM**, selecione a política de caixa de correio de Unificação de mensagens para o qual você deseja criar uma autorização de discagem e, em seguida, clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").

3.  Na página **Diretiva de caixa de correio de UM** \> **autorização de discagem**, clique em **Adicionar**![Ícone Adicionar](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Ícone Adicionar") sob **autorizados grupos de regras de discagem do país/região**.

4.  Na página **Selecionar grupos de regras de discagem para permitir**, selecione o grupo de regras de discagem, clique em **OK** e, em seguida, clique em **Salvar**.

## Usar o EAC para habilitar autorizações de discagem em uma diretiva de caixa de correio de Unificação de mensagens para grupos de regras de discagem internacional

1.  No EAC, navegue até **Unificação de Mensagens** \> **Planos de discagem de UM**. Na exibição de lista, selecione o plano de discagem de UM que você deseja modificar e clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").

2.  Na página de **Plano de discagem de UM**, em **Diretivas de caixa de correio de UM**, selecione a política de caixa de correio de Unificação de mensagens para o qual você deseja criar uma autorização de discagem e, em seguida, clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").

3.  Na página **Diretiva de caixa de correio de UM** \> **autorização de discagem**, clique em **Adicionar**![Ícone Adicionar](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Ícone Adicionar") em **grupos de regras de discagem internacional de autorizados**.

4.  Na página **Selecionar grupos de regras de discagem para permitir**, selecione o grupo de regras de discagem, clique em **OK** e, em seguida, clique em **Salvar**.

## Use o Shell para habilitar autorizações de discagem do país/região e internacionais em uma diretiva de caixa de correio UM

Este exemplo habilita as autorizações de discagem InCountry/RegionGroup1, InCountry/RegionGroup2, InternationalGroup1 e InternationalGroup2 em uma diretiva de caixa de correio de UM chamado `MyUMMailboxPolicy`.

    Set-UMMailboxPolicy -Identity MyUMMailboxPolicy -AllowedInCountryOrRegionGroups InCountry/RegionGroup1,InCountry/RegionGroup2 -AllowedInternationalGroups InternationalGroup1,InternationalGroup2

