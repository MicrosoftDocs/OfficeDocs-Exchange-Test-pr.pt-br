---
title: 'Habilitar o envio de fax para um grupo de usuários: Exchange 2013 Help'
TOCTitle: Habilitar o envio de fax para um grupo de usuários
ms:assetid: b8d9f54d-ff06-4942-83e1-fc6c4ad02178
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Ee423556(v=EXCHG.150)
ms:contentKeyID: 52058489
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Habilitar o envio de fax para um grupo de usuários

 

_**Aplica-se a:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Tópico modificado em:**2016-12-09_

Você pode habilitar faxes de entrada para os usuários vinculados com uma política de caixa de correio de Unificação de mensagens (UM). Por padrão, quando você habilita usuários para Unificação de mensagens, os usuários não podem receber mensagens de fax até que você especifique o URI para o servidor de parceiro de fax, implantar um servidor de parceiro de fax para sua organização e habilite o envio de fax em uma diretiva de caixa de correio de Unificação de MENSAGENS. Se a opção para permitir que os faxes de entrada estiver desabilitada em UM plano de discagem, os usuários vinculados com a diretiva de caixa de correio de Unificação de MENSAGENS ainda não será capazes de receber faxes. Da mesma forma, se a opção de permitir faxes de entrada estiver desabilitada em um usuário individual, que o usuário não conseguirá receber fax.

Para obter mais informações sobre os parceiros de fax, consulte [Microsoft identifique para parceiros de Fax](https://go.microsoft.com/fwlink/?linkid=190238).

Para conhecer tarefas de gerenciamento adicionais relacionadas a mensagens de fax, consulte [Procedimentos de envio de fax](faxing-procedures-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: Menos de 1 minuto.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Diretivas de caixa de correio da UM" no tópico [Permissões de mensagens unificadas](unified-messaging-permissions-exchange-2013-help.md).

  - Antes de executar esses procedimentos, confirme se um plano de discagem da UM foi criado. Para obter etapas detalhadas, consulte [Criar um plano de discagem de UM](create-a-um-dial-plan-exchange-2013-help.md).

  - Antes de executar esses procedimentos, verifique se uma política de caixa de correio de UM foi criada. Para obter etapas detalhadas, consulte [Criar uma política de caixa de correio da UM](create-a-um-mailbox-policy-exchange-2013-help.md).

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>..



## O que você deseja fazer?

## Usar o EAC para habilitar o envio de fax de entrada

1.  No EAC, navegue até **Unificação de Mensagens** \> **Planos de discagem de UM**. Na exibição de lista, selecione o plano de discagem de UM que você deseja alterar e clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").

2.  Na página **Plano de discagem de UM**, em **Políticas de Caixa de Correio de UM**, selecione a política de caixa de correio de UM que você deseja alterar e clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").

3.  Na página **política de caixa de correio de Unificação de MENSAGENS** \> **Geral**, marque a caixa de seleção ao lado de **Permitir que os faxes de entrada**.

4.  Clique em **Salvar** para salvar as suas alterações.

## Use o Shell para habilitar o envio de fax de entrada

Este exemplo permite que os usuários que estão vinculados com a Unificação de MENSAGENS da caixa de correio diretiva `MyUMMailboxPolicy` para usar o envio de fax de entrada.

    Set-UMMailboxPolicy -identity MyUMMailboxPolicy -AllowFax $true

