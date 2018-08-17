---
title: 'Adicionar um número de ramal de atendedor automático: Exchange 2013 Help'
TOCTitle: Adicionar um número de ramal de atendedor automático
ms:assetid: f2bd62ba-1e01-4cb7-862c-c750752e20e0
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Bb232200(v=EXCHG.150)
ms:contentKeyID: 50486984
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Adicionar um número de ramal de atendedor automático

 

_**Aplica-se a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Tópico modificado em:** 2012-11-05_

Você pode configurar um número de ramal ou vários números de ramal em um atendedor automático de Unificação de mensagens (UM). Quando você adiciona um número de ramal para um atendedor automático de UM, esse número pode ser usado por chamadores a ligar para o atendedor automático. Além disso, você talvez precise adicionar números de ramal porque não há mais de um número de ramal que os chamadores podem usar para acessar um atendedor automático. Por padrão, nenhuma números de ramal são configurados quando você cria um atendedor automático.

Você pode criar um novo atendedor automático sem configurar um número de ramal para o atendedor automático. Você também pode associar mais de um número de telefone ou ramal um atendedor automático único. Você pode adicionar os números de ramal quando você cria UM atendedor automático ou adicioná-los após configurar o atendedor automático. O número de dígitos no número do ramal que tenha configurado no atendedor automático de UM deve corresponder ao número de dígitos para um número de ramal configurado em UM plano de discagem associado ao atendedor automático de UM.


> [!NOTE]
> Você também pode adicionar um endereço de protocolo de iniciação de sessão (SIP) em vez de adicionar um número de ramal. Um endereço SIP é usado por alguns IP PBXs Private Branch eXchanges () e Office Communications Server 2007 R2 ou Microsoft Lync Server.



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

## Usar o EAC para adicionar um extensão ou números de telefone para um atendedor automático

1.  No EAC, navegue até **Unificação de mensagens** \> **planos de discagem de UM**. Na exibição de lista, selecione o plano de discagem de Unificação de mensagens que você deseja editar e clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").

2.  Na página de **Plano de discagem de UM**, em **Atendedores automáticos de UM**, selecione do atendedor automático para que você deseja adicionar números de telefone ou ramal.

3.  Na barra de ferramentas, clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").

4.  Na página de **Atendedor automático de UM** \> **Geral**, em **números de acesso**, na caixa de texto, digite o número de telefone ou de extensão que você deseja usar e clique em **Adicionar**![Ícone Adicionar](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Ícone Adicionar").

5.  Clique em **Salvar** para adicionar o número.

## Usar o Shell para configurar um número de ramal em um atendedor automático

Este exemplo configura um atendedor automático de UM chamado `MyUMAutoAttendant` com vários números de ramal.

    Set-UMAutoAttendant -Identity MyUMAutoAttendant -PilotIdentifierList "12345, 72000, 75000"

