---
title: 'Incluir texto com o email enviado quando uma mensagem de voz é recebida'
TOCTitle: Incluir texto com a mensagem de email enviada quando for recebida uma mensagem de voz
ms:assetid: b2eec29c-e5eb-4263-80d8-0b9813dd56dc
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Bb201718(v=EXCHG.150)
ms:contentKeyID: 51407896
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Incluir texto com a mensagem de email enviada quando for recebida uma mensagem de voz

 

_**Aplica-se a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Tópico modificado em:** 2012-12-16_

Você pode incluir texto adicional na mensagem de email enviada quando uma mensagem de voz é recebida por um usuário habilitado para caixa postal de Unificação de mensagens (UM). Por padrão, o texto que tiver incluído com uma mensagem de voz indica somente se o usuário recebeu uma mensagem de voz. No entanto, você pode criar uma mensagem personalizada, adicionando texto na caixa de ferramentas **quando um usuário recebe uma mensagem de voz** em uma diretiva de caixa de correio de UM. Por exemplo, o texto pode incluir informações sobre diretivas de segurança do sistema e descrevem a maneira correta de lidar com as mensagens de voz em sua organização. Depois de adicionar o texto, ele será incluído em cada mensagem de email é enviada quando usuários habilitados para UM associados com a diretiva de caixa de correio de Unificação de mensagens recebem uma mensagem de voz.


> [!TIP]
> O texto personalizado que acompanha uma mensagem de voz é limitado a 512 caracteres e pode incluir texto HTML simples.



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

## Usar o EAC para alterar o texto incluído com uma mensagem de voz

1.  No EAC, navegue até **Unificação de Mensagens** \> **Planos de discagem de UM**. Na exibição de lista, selecione o plano de discagem de UM que você deseja modificar e clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").

2.  Na página **Plano de Discagem de UM**, em **Políticas de Caixa de Correio de UM**, selecione a política de caixa de correio de UM que você deseja gerenciar e clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").

3.  Na página **Diretiva de caixa de correio de UM** \> **texto da mensagem**, na caixa de texto para, **quando um usuário recebe uma mensagem de voz**, insira o texto que você deseja incluir na mensagem de email enviada quando os usuários recebem uma mensagem de voz.

4.  Clique em **Salvar**.

## Use o Shell para alterar o texto incluído com uma mensagem de voz

Este exemplo inclui o texto adicional, "Não encaminhar mensagens de voz para usuários fora da organização", com as mensagens de voz enviada aos usuários que estão associados a diretiva de caixa de correio de UM chamado `MyUMMailboxPolicy`.

    Set-UMMailboxPolicy -identity MyUMMailboxPolicy -VoiceMailText "Do not forward voice messages to users outside this organization."

