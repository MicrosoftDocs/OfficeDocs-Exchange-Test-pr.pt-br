---
title: 'Habilitar ou desabilitar o envio de mensagens de voz do Outlook Voice Access: Exchange 2013 Help'
TOCTitle: Habilitar ou desabilitar o envio de mensagens de voz do Outlook Voice Access
ms:assetid: 63544ae2-6a28-40b2-82fc-3df83e93ee56
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Ee423546(v=EXCHG.150)
ms:contentKeyID: 52058434
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Habilitar ou desabilitar o envio de mensagens de voz do Outlook Voice Access

 

_**Aplica-se a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Tópico modificado em:** 2012-12-13_

Você pode habilitar os usuários do Outlook Voice Access para envio de mensagens de caixa postal para outros usuários habilitados para UM que estão associados com o mesmo plano de discagem ou impedir que eles façam isso.

Por padrão, a configuração está habilitada. Se você desabilitar esta configuração, os usuários do Outlook Voice Access que ligarem para um número do Outlook Voice Access não poderão enviar mensagens de voz para usuários dentro do mesmo plano de discagem.

Para tarefas adicionais relacionadas a planos de discagem de UM, consulte [Procedimentos de plano de discagem de UM](um-dial-plan-procedures-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: Menos de 1 minuto.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Planos de discagem de UM", no tópico [Permissões de mensagens unificadas](unified-messaging-permissions-exchange-2013-help.md).

  - Antes de executar esses procedimentos, confirme se um plano de discagem de UM foi criado. Para conhecer etapas detalhadas, consulte [Criar um plano de discagem de UM](create-a-um-dial-plan-exchange-2013-help.md).

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>..



## O que você deseja fazer?

## Use o EAC para habilitar ou impedir que os usuários do Outlook Voice Access enviem mensagen de voz para usuários no mesmo plano de discagem.

1.  No EAC, navegue até **Unificação de Mensagens** \> **Planos de discagem de UM**.

2.  Na exibição de lista, selecione o plano de discagem de UM que você deseja modificar e clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").

3.  Na página **Plano de discagem de UM**, clique em **Configurar**.

4.  Em **Transferir & pesquisa**, em **Permitir que os chamadores**, selecione **Deixem mensagens de voz sem tocar o telefone do usuário** para permitir o envio de mensagens de voz. Se você deseja impedir o envio de mensagens de voz para usuários, limpe esta configuração.

5.  Clique em **Salvar**.

## Use o Shell para habilitar ou impedir que os usuários do Outlook Voice Access enviem mensagens de voz para usuários no mesmo plano de discagem

Este exemplo habilita os usuários do Outlook Voice Access associados com o plano de discagem de UM de nome `MyUMDialPlan` para envio de mensagens de voz par usuários associados com o mesmo plano de discagem.

    Set-UMDialPlan -identity MyUMDialPlan -SendVoiceMsgEnabled $true

Este exemplo impede que os usuários do Outlook Voice Access associados com o plano de discagem de UM de nome `MyUMDialPlan` enviem mensagens de voz para usuários associados com o mesmo plano de discagem.

    Set-UMDialPlan -identity MyUMDialPlan -SendVoiceMsgEnabled $false

