---
title: 'Permitir ou impedir que um usuário crie regras de atendimento de chamada: Exchange 2013 Help'
TOCTitle: Permitir ou impedir que um usuário crie regras de atendimento de chamada
ms:assetid: 81863440-8b21-4523-bdab-6a2311889a0d
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Dd298097(v=EXCHG.150)
ms:contentKeyID: 50556234
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Permitir ou impedir que um usuário crie regras de atendimento de chamada

 

_**Aplica-se a:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Tópico modificado em:**2013-02-22_

Você pode especificar se deseja que usuários individuais possam criar e gerenciar sua próprias chamada regras de atendimento, definindo suas propriedades de caixa de correio. Por padrão, eles podem criar regras de atendimento de chamadas.

Você pode habilitar ou desabilitar regras de atendimento de chamada para vários usuários que estão habilitados para Unificação de mensagens (UM), configurando regras de atendimento de chamada em um plano de discagem ou política de caixa de correio de Unificação de mensagens.


> [!TIP]
> Você não pode usar o EAC para configurar esse recurso. Você deve usar o Shell para habilitar ou desabilitar regras de atendimento de chamadas para um usuário de email de voz.



Para tarefas de gerenciamento adicionais relacionadas a permitindo que os usuários encaminhar chamadas, consulte [Encaminhamento de chamadas de procedimentos](forwarding-calls-procedures-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: Menos de 1 minuto.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Caixas de correio da UM" no tópico [Permissões de mensagens unificadas](unified-messaging-permissions-exchange-2013-help.md).

  - Antes de executar esse procedimento, verifique se um plano de discagem de UM foi criado. Para obter etapas detalhadas, consulte [Criar um plano de discagem de UM](create-a-um-dial-plan-exchange-2013-help.md).

  - Antes de executar este procedimento, confirme se uma diretiva de caixa de correio UM foi criada. Para obter etapas detalhadas, consulte [Criar uma política de caixa de correio da UM](create-a-um-mailbox-policy-exchange-2013-help.md).

  - Antes de executar este procedimento, confirme que a caixa de correio do usuário foi habilitado. Para obter etapas detalhadas, consulte [Habilitar um usuário para caixa postal](enable-a-user-for-voice-mail-exchange-2013-help.md).

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>..



## Usar o Shell para habilitar ou desabilitar regras para um usuário habilitado para Unificação de mensagens de atendimento de chamada

Este exemplo habilita a regras de atendimento de chamada para o usuário tony@contoso.com.

    Set-UMMailbox -Identity tony@contoso.com -CallAnsweringRulesEnabled $true

Este exemplo desativa regras de atendimento de chamada para o usuário tony@contoso.com.

    Set-UMMailbox -Identity tony@contoso.com -CallAnsweringRulesEnabled $false

