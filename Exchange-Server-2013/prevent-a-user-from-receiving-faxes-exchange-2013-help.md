---
title: 'Impedir que um usuário receba faxes: Exchange 2013 Help'
TOCTitle: Impedir que um usuário receba faxes
ms:assetid: b5d022b9-043a-4324-87fb-074d5e2c2ca3
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Bb201722(v=EXCHG.150)
ms:contentKeyID: 52058487
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Impedir que um usuário receba faxes

 

_**Aplica-se a:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Tópico modificado em:**2016-12-09_

Impedir que um usuário de Unificação de mensagens (UM) receba faxes. Descubra como alterar as configurações de fax para os usuários de Unificação de MENSAGENS novas e existentes.

Por padrão, quando você habilita um usuário para Unificação de mensagens, eles poderão receber faxes se você habilitar o envio de fax e configurar URI de um parceiro de fax na diretiva de caixa de correio de Unificação de MENSAGENS que está vinculada ao usuário. Envio de fax pode ser habilitado ou desabilitado na Unificação de MENSAGENS discagem planos, políticas de caixa de correio de Unificação de MENSAGENS ou caixa de correio do usuário habilitado para UM.

Por padrão, a caixa de correio do usuário e o plano de discagem que está vinculado ao usuário permite que os faxes de entrada. No entanto, para um usuário receber faxes você deve primeiro habilitar envio de fax de entrada na diretiva de caixa de correio de Unificação de MENSAGENS que está associada ao usuário habilitado para Unificação de MENSAGENS e insira o URI do parceiro de fax.


> [!TIP]
> Você pode usar o EAC para configurar as configurações de fax em uma diretiva de caixa de correio de Unificação de mensagens. No entanto, você deve usar o Shell para definir as configurações de fax em planos de discagem ou para usuários individuais.



Para obter mais informações sobre os parceiros de fax, consulte [Microsoft identifique para parceiros de Fax](https://go.microsoft.com/fwlink/?linkid=190238).

Para conhecer tarefas de gerenciamento adicionais relacionadas a mensagens de fax, consulte [Procedimentos de envio de fax](faxing-procedures-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: 2 minutos.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Diretivas de caixa de correio da UM" no tópico [Permissões de mensagens unificadas](unified-messaging-permissions-exchange-2013-help.md).

  - Antes de executar esses procedimentos, confirme se um plano de discagem da UM foi criado. Para obter etapas detalhadas, consulte [Criar um plano de discagem de UM](create-a-um-dial-plan-exchange-2013-help.md).

  - Antes de executar esses procedimentos, verifique se uma política de caixa de correio de UM foi criada. Para obter etapas detalhadas, consulte [Criar uma política de caixa de correio da UM](create-a-um-mailbox-policy-exchange-2013-help.md).

  - Antes de executar esses procedimentos, confirme que o usuário está habilitado para Unificação de mensagens. Para obter etapas detalhadas, consulte [Habilitar um usuário para caixa postal](enable-a-user-for-voice-mail-exchange-2013-help.md).

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>..



## Usar o Shell para impedir que um usuário habilitado receba faxes

Este exemplo impede que um usuário habilitado para UM, chamado Tony do recebimento de mensagens de fax em sua caixa de correio.

    Set-UMMailbox -Identity tony@contoso.com -FaxEnabled $false

