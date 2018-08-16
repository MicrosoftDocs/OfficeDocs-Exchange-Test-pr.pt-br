---
title: 'Permitir ou impedir transferência de chamadas do Outlook Voice Access'
TOCTitle: Permitir ou impedir transferência de chamadas do Outlook Voice Access
ms:assetid: b80c57f1-394c-4608-8ad3-52a3e6d697db
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Ee423554(v=EXCHG.150)
ms:contentKeyID: 52058488
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Permitir ou impedir transferência de chamadas do Outlook Voice Access

 

_**Aplica-se a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Tópico modificado em:** 2013-02-22_

Você pode permitir que os usuários do Outlook Voice Access transferir chamadas para um usuário que está associada a um plano de discagem de Unificação de mensagens (UM) ou impedir isso. Por padrão, ambos os essa opção e a opção **deixar mensagens de voz, sem precisar ligar o telefone de um usuário** estão habilitados, para que os usuários do Outlook Voice Access podem transferir chamadas para os usuários a UM mesmo plano de discagem e deixar mensagens de voz para eles. Essa configuração se aplica apenas aos usuários do Outlook Voice Access que tenham inserido seu PIN e são autenticados.

Para tarefas adicionais relacionadas a planos de discagem de UM, consulte [Procedimentos de plano de discagem de UM](um-dial-plan-procedures-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: Menos de 1 minuto.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Planos de discagem de UM" no tópico [Permissões de mensagens unificadas](unified-messaging-permissions-exchange-2013-help.md).

  - Antes de executar esses procedimentos, confirme se um plano de discagem da UM foi criado. Para obter etapas detalhadas, consulte [Criar um plano de discagem de UM](create-a-um-dial-plan-exchange-2013-help.md).

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>..



## O que você deseja fazer?

## Usar o EAC para habilitar ou impedir que os usuários do Outlook Voice Access transferindo chamadas

1.  No EAC, navegue até **Unificação de Mensagens** \> **Planos de discagem de UM**. Na exibição de lista, selecione o plano de discagem de UM que você deseja modificar e clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").

2.  Na página **Plano de discagem de UM**, clique em **Configurar**.

3.  Na **transferência & pesquisa**, em **Permitir que chamadores**, marque a caixa de seleção ao lado de **transferência aos usuários** para permitir que os chamadores transferir chamadas para outros usuários no plano de discagem. Se você deseja impedir que os usuários do Outlook Voice Access transferindo chamadas aos usuários, desmarque essa caixa de seleção.

4.  Clique em **Salvar**.

## Usar o Shell para habilitar ou impedir que os usuários do Outlook Voice Access transferindo chamadas

Este exemplo permite que os usuários do Outlook Voice Access transferir chamadas para usuários no mesmo plano de discagem em um plano de discagem de UM chamado `MyUMDialPlan`.

    Set-UMDialPlan -identity MyUMDialPlan -AllowDialPlanSubscribers $true

Este exemplo impede que os usuários do Outlook Voice Access transferindo chamadas para usuários no mesmo plano de discagem em um plano de discagem de UM chamado `MyUMDialPlan`.

    Set-UMDialPlan -identity MyUMDialPlan -AllowDialPlanSubscribers $false

