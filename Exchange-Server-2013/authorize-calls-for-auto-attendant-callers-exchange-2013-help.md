---
title: 'Autorizar chamadas para chamadores de atendedor automático: Exchange 2013 Help'
TOCTitle: Autorizar chamadas para os chamadores de atendedor automático
ms:assetid: c6c94fad-64df-44aa-a198-980f017ef716
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Bb691238(v=EXCHG.150)
ms:contentKeyID: 51407913
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Autorizar chamadas para os chamadores de atendedor automático

 

_**Aplica-se a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Tópico modificado em:** 2013-02-21_

Você pode habilitar autorizações de discagem em um atendedor automático de Unificação de mensagens (UM). Autorizações de discagem em um atendedor automático são usadas para proibir que os usuários que ligam para o atendedor automático de fazer chamadas telefônicas de país/região ou internacionais ou *discagem externa*. Discagem externa acontece quando Unified Messaging faz uma chamada de saída para um usuário depois que eles foram chamado em um número de telefone que está configurado em um automáticos attendant.

Para conhecer tarefas de gerenciamento adicionais relacionadas à discagem externa, consulte [Permitindo que usuários façam chamadas de procedimentos](allowing-users-to-make-calls-procedures-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: Menos de 1 minuto.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Atendedores automáticos da UM" no tópico [Permissões de mensagens unificadas](unified-messaging-permissions-exchange-2013-help.md).

  - Antes de executar esses procedimentos, confirme se um plano de discagem da UM foi criado. Para obter etapas detalhadas, consulte [Criar um plano de discagem de UM](create-a-um-dial-plan-exchange-2013-help.md).

  - Antes de executar esses procedimentos, verifique se um plano de discagem de UM foi criado. Para conhecer etapas detalhadas, consulte [Criar um Atendedor Automático da UM](create-a-um-auto-attendant-exchange-2013-help.md).

  - Antes de executar esses procedimentos, confirme que as regras de discagem do país/região e internacionais foram criadas em um plano de discagem de UM. Para obter etapas detalhadas, consulte [Criar regras de discagem para usuários](create-dialing-rules-for-users-exchange-2013-help.md).

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>..



## O que você deseja fazer?

## Usar o EAC para habilitar autorizações de discagem em um atendedor automático para grupos de regras do país/região

1.  No EAC, navegue até **Unificação de Mensagens** \> **Planos de discagem de UM**. Na exibição de lista, selecione o plano de discagem de UM que você deseja modificar e clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").

2.  Na página **Plano de discagem de UM**, em **Atendedores automáticos de UM**, selecione o atendedor automático de UM para o qual você deseja criar uma autorização de discagem e, em seguida, clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").

3.  Na página de **Atendedor automático de UM** \> **autorização de discagem**, clique em **Adicionar**![Ícone Adicionar](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Ícone Adicionar") sob **autorizados grupos de regras de discagem do país/região**.

4.  Na página **Selecionar grupos de regras de discagem para permitir**, selecione o grupo de regras de discagem, clique em **OK** e, em seguida, clique em **Salvar**.

## Usar o EAC para habilitar autorizações de discagem em um atendedor automático para grupos de regras internacionais

1.  No EAC, navegue até **Unificação de Mensagens** \> **Planos de discagem de UM**. Na exibição de lista, selecione o plano de discagem de UM que você deseja modificar e clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").

2.  Na página **Plano de discagem de UM**, em **Atendedores automáticos de UM**, selecione o atendedor automático de UM para o qual você deseja criar uma autorização de discagem e, em seguida, clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").

3.  Na página de **Atendedor automático de UM** \> **autorização de discagem**, clique em **Adicionar**![Ícone Adicionar](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Ícone Adicionar") em **grupos de regras de discagem internacional de autorizados**.

4.  Na página **Selecionar grupos de regras de discagem para permitir**, selecione o grupo de regras de discagem, clique em **OK** e, em seguida, clique em **Salvar**.

## Use o Shell para habilitar autorizações de discagem do país/região e internacionais em um atendedor automático

Este exemplo habilita o InCountry/RegionGroup1, InCountry/RegionGroup2. InternationalGroup1 e autorizações de discagem InternationalGroup2 em um atendedor automático de UM chamado `MyUMAutoAttendant`.

    Set-UMAutoAttendant -Identity MyUMAutoAttendant -AllowedInCountryOrRegionGroups InCountry/RegionGroup1,InCountry/RegionGroup2 -AllowedInternationalGroups InternationalGroup1,InternationalGroup2

