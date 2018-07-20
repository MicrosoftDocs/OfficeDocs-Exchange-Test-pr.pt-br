---
title: 'Remover uma regra de atendimento de chamada para um usuário: Exchange 2013 Help'
TOCTitle: Remover uma regra de atendimento de chamada para um usuário
ms:assetid: 1da3c5bc-7227-4b37-96f6-67ceefc084d5
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/JJ898497(v=EXCHG.150)
ms:contentKeyID: 51407844
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Remover uma regra de atendimento de chamada para um usuário

 

_**Aplica-se a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Tópico modificado em:** 2015-04-08_

Você pode usar o Shell para remover a chamada de um ou mais regras de atendimento de um usuário. Você também pode usar o cmdlet **Remove-UMCallAnsweringRule** em um script do Shell de gerenciamento do Exchange para remover a chamada de um ou mais regras de atendimento para vários usuários.

Regras de atendimento de chamada são aplicadas às chamadas recebidas semelhantes à maneira como as regras de caixa de entrada são aplicadas a mensagens de email de entrada. Por padrão, quando um usuário está habilitado para Unificação de mensagens (UM), não há regras de atendimento de chamada são configuradas. Mesmo assim, as chamadas são respondidas pelo sistema de email e os chamadores for solicitados a deixar uma mensagem de voz.


> [!TIP]
> Usuários que foram habilitados para Unificação de mensagens podem entrar no Outlook Web App para criar, gerenciar e remover regras de atendimento de chamada.



Para tarefas de gerenciamento adicionais relacionadas às regras de atendimento de chamadas, consulte [Encaminhamento de chamadas de procedimentos](forwarding-calls-procedures-exchange-2013-help.md).

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



## Use o Shell para remover uma regra de atendimento de chamada

Este exemplo remove a regra atendimento chamada `MyUMCallAnsweringRule` da caixa de correio do usuário. Caixa de correio do usuário é a caixa de correio do usuário executando o cmdlet.

    Remove-UMCallAnsweringRule -Identity MyUMCallAnsweringRule

Este exemplo remove a regra atendimento chamada `MyUMCallAnsweringRule` da caixa de correio de Tony Smith.

    Remove-UMCallAnsweringRule -Identity MyUMCallAnsweringRule -Mailbox tonysmith

