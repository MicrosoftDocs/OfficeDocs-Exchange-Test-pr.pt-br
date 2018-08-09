---
title: 'Habilitar ou desabilitar uma regra de atendimento de chamada para um usuário'
TOCTitle: Habilitar ou desabilitar uma regra de atendimento de chamada para um usuário
ms:assetid: f9e40ac3-117f-44f6-9ab1-dc9f4c72e8ac
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Dn140252(v=EXCHG.150)
ms:contentKeyID: 54651956
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Habilitar ou desabilitar uma regra de atendimento de chamada para um usuário

 

_**Aplica-se a:** Exchange Server 2013, Exchange Server 2016_

_**Tópico modificado em:** 2015-04-08_

Você pode usar o Shell para habilitar ou desabilitar um ou mais regras de atendimentos de chamadas para um usuário. Você também pode usar os cmdlets **Enable-UMCallAnsweringRule** ou **Disable-UMCallAnsweringRule** em um script do Shell de gerenciamento do Exchange para habilitar ou desabilitar um ou mais regras de atendimento de chamada para vários usuários.

Regras de atendimento de chamada são aplicadas às chamadas recebidas semelhantes à maneira como as regras de caixa de entrada são aplicadas a mensagens de email de entrada. Por padrão, quando um usuário está habilitado para Unificação de mensagens (UM), não há regras de atendimento de chamada são configuradas. Mesmo assim, as chamadas são respondidas pelo sistema de email e os chamadores for solicitados a deixar uma mensagem de voz.

Para tarefas de gerenciamento adicionais relacionadas a regras de atendimento de chamadas, consulte [Encaminhamento de chamadas de procedimentos](forwarding-calls-procedures-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: Menos de 1 minuto.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "regras de atendimento de chamadas de Unificação de mensagens" no tópico [Permissões de mensagens unificadas](unified-messaging-permissions-exchange-2013-help.md) .

  - Antes de executar esse procedimento, verifique se um plano de discagem de UM foi criado. Para obter etapas detalhadas, consulte [Criar um plano de discagem de UM](create-a-um-dial-plan-exchange-2013-help.md).

  - Antes de executar este procedimento, confirme se uma diretiva de caixa de correio UM foi criada. Para obter etapas detalhadas, consulte [Criar uma política de caixa de correio da UM](create-a-um-mailbox-policy-exchange-2013-help.md).

  - Antes de executar este procedimento, confirme que a caixa de correio do usuário foi habilitado. Para obter etapas detalhadas, consulte [Habilitar um usuário para caixa postal](enable-a-user-for-voice-mail-exchange-2013-help.md).

  - Você só pode usar o Shell para executar esse procedimento. Para saber como abrir o Shell de Gerenciamento do Exchange em sua organização Exchange local, confira [Abra o shell.](https://technet.microsoft.com/pt-br/library/dd638134\(v=exchg.150\)). Para saber como usar o Windows PowerShell para se conectar ao Exchange Online, confira o artigo [Conectar-se ao Exchange Online PowerShell](https://go.microsoft.com/fwlink/p/?linkid=396554).

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>..



## O que você deseja fazer?

## Use o Shell para habilitar uma regra de atendimento de chamada

Quando uma chamada de regra de atendimento é criada, ele é habilitado. Você pode usar o Shell para habilitar uma regra de atendimento de chamada que foi desabilitada anteriormente. Habilitar uma regra de atendimento permite que o cmdlet **Enable-UMCallAnsweringRule** recuperar a regra, incluindo as condições e ações para uma regra de atendimento de chamada especificado de atendimento de chamada de chamada.

Este exemplo habilita a chamada atendimento regra `MyUMCallAnsweringRule` na caixa de correio de Tony Smith.

    Enable-UMCallAnsweringRule -Identity MyUMCallAnsweringRule -Mailbox tonysmith

O exemplo usa a opção *WhatIf* para testar se a chamada de atendimento de regra `MyUMCallAnsweringRule` na caixa de correio de Tony Smith está pronta para ser habilitado e se houver erros no comando.

    Enable-UMCallAnsweringRule -Identity MyUMCallAnsweringRule -Mailbox tonysmith -WhatIf

Este exemplo habilita a chamada de atendimento de regra `MyUMCallAnsweringRule` na caixa de correio de Tony Smith e avisa o usuário conectado para confirmar que a regra de atendimento de chamada deve ser habilitado.

    Enable-UMCallAnsweringRule -Identity MyUMCallAnsweringRule -Mailbox tonysmith -Confirm

## Usar o Shell para desabilitar uma regra de atendimento de chamada

Desabilitar uma regra de atendimento impede que ele seja recuperado e processados quando uma chamada for recebida de chamada. Quando você cria uma regra de atendimento de chamada, você deverá desabilitá-lo enquanto você estiver configurando condições e ações. Isso impede que a regra de atendimento de chamada que estão sendo processadas quando uma chamada for recebida antes que você configurou corretamente a regra de atendimento de chamada.

Este exemplo desabilita a chamada atendimento regra `MyUMCallAnsweringRule` na caixa de correio de Tony Smith.

    Disable -UMCallAnsweringRule -Identity MyUMCallAnsweringRule -Mailbox tonysmith

Este exemplo usa a opção *WhatIf* para testar se a chamada de atendimento de regra `MyUMCallAnsweringRule` na caixa de correio de Tony Smith está pronta para ser desabilitado e se houver erros no comando.

    Disable -UMCallAnsweringRule -Identity MyUMCallAnsweringRule -Mailbox tonysmith -WhatIf

Este exemplo desabilita a chamada de atendimento de regra `MyUMCallAnsweringRule` na caixa de correio de Tony Smith e avisa o usuário conectado para confirmar se está desabilitando a regra de atendimento de chamada.

    Disable-UMCallAnsweringRule -Identity MyUMCallAnsweringRule -Mailbox tonysmith -Confirm

