---
title: 'Desabilitar o envio de fax para um grupo de usuários: Exchange 2013 Help'
TOCTitle: Desabilitar o envio de fax para um grupo de usuários
ms:assetid: 1c57c3ba-2b0e-43dd-9b28-43bada1592c5
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/JJ650864(v=EXCHG.150)
ms:contentKeyID: 52058381
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Desabilitar o envio de fax para um grupo de usuários

 

_**Aplica-se a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Tópico modificado em:** 2016-12-09_

Você pode desabilitar os faxes de entrada para usuários associados a uma política de caixa de correio de UM (Unificação de Mensagens). Por padrão, quando você habilita usuários para Unificação de Mensagens, os usuários não podem receber mensagens de fax até que você especifique o URI do servidor parceiro de fax, implante um servidor de parceiro de fax para sua organização e habilite o envio de fax em uma política de caixa de correio de UM. Se a opção que permite o recebimento de mensagens de fax estiver desabilitada no plano de discagem de UM, os usuários vinculados à política de caixa de correio de UM não poderão receber mensagens de fax. Da mesma forma, se a opção que permite o recebimento de mensagens de fax estiver desabilitada para um usuário específico, esse usuário não poderá receber mensagens de fax.

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

## Usar o EAC para desabilitar fax de entrada

1.  No EAC, navegue até **Unificação de Mensagens** \> **Planos de discagem de UM**. Na exibição de lista, selecione o plano de discagem de UM que você deseja alterar e clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").

2.  Na página **Plano de discagem de UM**, em **Políticas de Caixa de Correio de UM**, selecione a política de caixa de correio de UM que você deseja alterar e clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").

3.  Na página **Política de caixa de correio de UM** \> **Geral**, desmarque a caixa de seleção ao lado de **Permitir faxes de entrada**.

4.  Clique em **Salvar** para salvar suas alterações.

## Usar o Shell para desabilitar fax de entrada

Este exemplo evita que usuários vinculados à política de caixa de correio de UM `MyUMMailboxPolicy` usem fax de entrada.

    Set-UMMailboxPolicy -identity MyUMMailboxPolicy -AllowFax $false

