---
title: 'Configurar o limite em saudações pessoais para usuários do Outlook Voice Access: Exchange 2013 Help'
TOCTitle: Configurar o limite em saudações pessoais para usuários do Outlook Voice Access
ms:assetid: d400f250-0f55-45f5-9918-5f1d7819fbdf
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Bb201731(v=EXCHG.150)
ms:contentKeyID: 50556297
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configurar o limite em saudações pessoais para usuários do Outlook Voice Access

 

_**Aplica-se a:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Tópico modificado em:**2012-11-05_

A configuração de **limite de saudações pessoais (minutos)** permite que você insira o número máximo de minutos que os usuários associados a diretiva de caixa de correio de Unificação de mensagens (UM) podem usar para gravar sua saudação da caixa postal. Essa configuração se aplica a suas mensagens de voz padrão e a sua saudação da caixa postal de ausência temporária. Por padrão, a duração máxima da saudação é definida como 5 minutos. No entanto, você pode configurar a duração máxima da saudação para qualquer configuração entre 1 e 10 minutos.

Para conhecer tarefas de gerenciamento adicionais relacionadas a políticas de caixa de correio de UM, consulte [Procedimentos de diretiva de caixa de correio de Unificação de mensagens](um-mailbox-policy-procedures-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: Menos de 1 minuto.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Diretivas de caixa de correio da UM" no tópico [Permissões de mensagens unificadas](unified-messaging-permissions-exchange-2013-help.md).

  - Antes de executar esses procedimentos, confirme se um plano de discagem da UM foi criado. Para obter etapas detalhadas, consulte [Criar um plano de discagem de UM](create-a-um-dial-plan-exchange-2013-help.md).

  - Antes de executar esses procedimentos, verifique se uma política de caixa de correio de UM foi criada. Para obter etapas detalhadas, consulte [Criar uma política de caixa de correio da UM](create-a-um-mailbox-policy-exchange-2013-help.md).

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>..



## O que você deseja fazer?

## Usar o EAC para alterar a duração máxima da saudação

1.  No EAC, navegue até **Unificação de mensagens** \> **planos de discagem de UM**. Na exibição de lista, selecione o plano de discagem de Unificação de mensagens que você deseja modificar e, na barra de ferramentas, clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").

2.  Na página de **Plano de discagem de UM**, em **Diretivas de caixa de correio de UM**, selecione a política de caixa de correio de Unificação de mensagens que você deseja gerenciar e clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição")na barra de ferramentas.

3.  Na página **política de caixa de correio de Unificação de mensagens** \> **Geral**, em **limite de saudações pessoais (minutos)**, insira o período de tempo, em minutos, permitido para saudações pessoais para usuários de email de voz.

4.  Clique em **Salvar**.

## Use o Shell para alterar a duração máxima da saudação

Este exemplo configura a duração máxima da saudação na de diretiva de caixa de correio `MyUMMailboxPolicy` Unificação de mensagens para 3 minutos.

    Set-UMMailboxPolicy -identity MyUMMailboxPolicy MaxGreetingDuration 3

