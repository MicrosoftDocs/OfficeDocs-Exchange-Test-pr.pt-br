---
title: 'Habilitar ou desabilitar o envio de mensagens de voz para usuários'
TOCTitle: Habilitar ou desabilitar o envio de mensagens de voz aos usuários
ms:assetid: faa300d8-2534-40db-8ef9-428be8bb7934
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Dd351277(v=EXCHG.150)
ms:contentKeyID: 52058556
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Habilitar ou desabilitar o envio de mensagens de voz aos usuários

 

_**Aplica-se a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Tópico modificado em:** 2012-12-13_

Você pode permitir que os chamadores enviar mensagens de voz aos usuários de um atendedor automático de Unificação de mensagens (UM) ou impedir isso. Por padrão, essa opção está habilitada e permite que os chamadores enviar mensagens de voz aos usuários em UM plano de discagem associado do atendedor automático. Se você desabilitar essa opção, o atendedor automático não convida os chamadores para enviar uma mensagem de voz durante um prompt do sistema.

Para conhecer tarefas de gerenciamento adicionais relacionadas a atendedores automáticos de UM, consulte [Procedimentos atendedor automático a Unificação de mensagens](um-auto-attendant-procedures-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: Menos de 1 minuto.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Atendedores automáticos da UM" no tópico [Permissões de mensagens unificadas](unified-messaging-permissions-exchange-2013-help.md).

  - Antes de executar esses procedimentos, confirme se um plano de discagem da UM foi criado. Para obter etapas detalhadas, consulte [Criar um plano de discagem de UM](create-a-um-dial-plan-exchange-2013-help.md).

  - Antes de executar esses procedimentos, verifique se um plano de discagem de UM foi criado. Para conhecer etapas detalhadas, consulte [Criar um Atendedor Automático da UM](create-a-um-auto-attendant-exchange-2013-help.md).

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>..



## O que você deseja fazer?

## Usar o EAC para permitir que os chamadores enviar mensagens de voz ou impedir isso

1.  No EAC, navegue até **Unificação de Mensagens** \> **Planos de discagem de UM**. Na exibição de lista, selecione o plano de discagem de UM que você deseja modificar e clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").

2.  Na página **Plano de discagem de UM**, em **Atendedores automáticos de UM**, selecione o atendedor automático de UM que deseja gerenciar e clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").

3.  Na página de **Atendedor automático de UM** \> **acesso de operador e catálogo de endereços**, em **Opções para entrar em contato com os usuários**, marque a caixa de seleção ao lado de **Permitir que chamadores deixar mensagens de voz para os usuários** para permitir que os chamadores deixar mensagens de voz. Para impedir que os chamadores deixando mensagens de voz, desmarque a caixa de seleção.

4.  Clique em **Salvar**.


> [!TIP]
> Se você desabilitar essa opção e também desabilitar a opção de <STRONG>Permitir que os chamadores para usuários de discagem</STRONG>, as <STRONG>Opções para pesquisar o catálogo de endereços</STRONG> também são desabilitados.



## Use o Shell para habilitar os chamadores enviar mensagens de voz ou impedir isso

Este exemplo impede que os chamadores que ligam para um atendedor automático de UM chamado `MyUMAutoAttendant` enviem mensagens de voz.

    Set-UMAutoAttendant -Identity MyUMAutoAttendant -SendVoiceMsgEnabled $false

Este exemplo permite que os chamadores que ligam para um atendedor automático de UM chamado `MyUMAutoAttendant` para enviar mensagens de voz.

    Set-UMAutoAttendant -Identity MyUMAutoAttendant -SendVoiceMsgEnabled $true

