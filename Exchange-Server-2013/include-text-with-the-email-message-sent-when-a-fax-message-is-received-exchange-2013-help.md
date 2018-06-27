---
title: 'Incluir texto com a mensagem de email enviada quando for recebida uma mensagem de fax: Exchange 2013 Help'
TOCTitle: Incluir texto com a mensagem de email enviada quando for recebida uma mensagem de fax
ms:assetid: 48244e58-b7d6-4f0e-bbae-d22bf0fc11ff
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Bb201684(v=EXCHG.150)
ms:contentKeyID: 51407868
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Incluir texto com a mensagem de email enviada quando for recebida uma mensagem de fax

 

_**Aplica-se a:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Tópico modificado em:**2016-12-09_

Você pode incluir texto adicional na mensagem de email enviada quando uma mensagem de fax é recebida por um usuário habilitado para a caixa postal da UM (Unificação de Mensagens) e para fax, e quando a política de caixa de correio da UM tiver sido configurada corretamente para usar um provedor parceiro de fax. Por padrão, o texto incluído quando um usuário habilitado para UM recebe uma mensagem de fax indica somente que o usuário recebeu uma mensagem de fax. No entanto, você pode criar uma mensagem personalizada adicionando texto na caixa de texto **Quando um usuário receber uma mensagem de fax** em uma política de caixa de correio da UM. Por exemplo, o texto pode incluir informações sobre políticas de segurança do sistema e descrever a forma correta para manipular mensagens de fax em sua organização. Depois de adicionar o texto, ele será incluído em cada mensagem de email enviada quando usuários habilitados para UM que estejam associados a uma política de caixa de correio da UM receberem uma mensagem de fax.


> [!TIP]
> O texto personalizado que acompanha uma mensagem de fax é limitado a 512 caracteres e pode incluir texto HTML simples.



Para obter mais informações sobre os parceiros de fax, consulte [Microsoft identifique para parceiros de Fax](https://go.microsoft.com/fwlink/?linkid=190238).

Para conhecer tarefas de gerenciamento adicionais relacionadas a mensagens de fax, consulte [Procedimentos de envio de fax](faxing-procedures-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: Menos de 1 minuto.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Políticas de caixa de correio de UM", no tópico [Permissões de mensagens unificadas](unified-messaging-permissions-exchange-2013-help.md).

  - Antes de executar esses procedimentos, confirme se um plano de discagem de UM foi criado. Para conhecer etapas detalhadas, consulte [Criar um plano de discagem de UM](create-a-um-dial-plan-exchange-2013-help.md).

  - Antes de executar esses procedimentos, verifique se uma política de caixa de correio de UM foi criada. Para conhecer etapas detalhadas, consulte [Criar uma política de caixa de correio da UM](create-a-um-mailbox-policy-exchange-2013-help.md).

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>..



## O que você deseja fazer?

## Usar o EAC para alterar o texto incluído em uma mensagem de fax

1.  No EAC, navegue até **Unificação de Mensagens** \> **Planos de discagem de UM**. Na exibição de lista, selecione o plano de discagem de UM que você deseja modificar e clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").

2.  Na página **Plano de Discagem de UM**, em **Políticas de Caixa de Correio de UM**, selecione a política de caixa de correio de UM que você deseja gerenciar e clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").

3.  Na página **Política de Caixa de Correio de UM** \> **Texto da mensagem**, na caixa de texto para **Quando um usuário recebe uma mensagem de fax**, insira o texto que deseja incluir na mensagem de email enviada quando usuários recebem uma mensagem de fax na caixa de correio.

4.  Clique em **Salvar**.

## Usar o Shell para alterar o texto incluído em uma mensagem de fax

Este exemplo habilita usuários habilitados para a UM que estejam associados a uma diretiva de caixa de correio da UM a receber instruções adicionais sobre como abrir mensagens de fax recebidas em suas caixas de correio.

    Set-UMMailboxPolicy -identity MyUMMailboxPolicy -FaxMessageText "To open this fax message, double-click the file attachment."

