---
title: 'Criar uma regra de atendimento de chamada: Exchange 2013 Help'
TOCTitle: Criar uma regra de atendimento de chamada
ms:assetid: 0976f8f2-3449-44f1-b0d1-20c91622e827
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/JJ898495(v=EXCHG.150)
ms:contentKeyID: 51407832
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Criar uma regra de atendimento de chamada

 

_**Aplica-se a:** Exchange Server 2013, Exchange Server 2016_

_**Tópico modificado em:** 2015-04-08_

Você pode usar o Shell para criar a chamada de um ou mais regras de atendimento de um usuário. Você também pode usar o cmdlet **New-UMCallAnsweringRule** em um script do Shell de gerenciamento do Exchange para criar regras de atendimento de chamada para vários usuários.

Regras de atendimento de chamada são aplicadas às chamadas recebidas semelhantes à maneira como as regras de caixa de entrada são aplicadas a mensagens de email de entrada. Por padrão, quando um usuário está habilitado para Unificação de mensagens (UM), não há regras de atendimento de chamada são configuradas. Mesmo assim, as chamadas são respondidas pelo sistema de email e os chamadores for solicitados a deixar uma mensagem de voz.


> [!TIP]
> Usuários que foram habilitados para Unificação de mensagens podem entrar no Outlook Web App para criar, gerenciar e remover regras de atendimento de chamada.



Para tarefas de gerenciamento adicionais relacionadas às regras de atendimento de chamadas, consulte [Encaminhamento de chamadas de procedimentos](https://docs.microsoft.com/pt-br/exchange/voice-mail-unified-messaging/set-up-client-voice-mail-features/forwarding-calls-procedures).

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



## Use o Shell para criar uma regra de atendimento de chamada

Este exemplo cria a regra atendimento chamada `MyCallAnsweringRule` na caixa de correio de Tony Smith com a prioridade 2.

    New-UMCallAnsweringRule -Name MyCallAnsweringRule -Priority 2 -Mailbox tonysmith

Este exemplo cria a regra atendimento chamada `MyCallAnsweringRule` na caixa de correio de Tony Smith e executa as seguintes ações:

  - Define a regra de atendimento de chamada para dois ID de chamadas.

  - Define a prioridade da regra de atendimento de chamada para 2.

  - Define a regra de atendimento de chamada para permitir que chamadores interrompam a saudação.

<!-- end list -->

    New-UMCallAnsweringRule -Name MyCallAnsweringRule -CallerIds "1,4255550100,,","1,4255550123,," -Priority 2 -CallersCanInterruptGreeting $true -Mailbox tonysmith

Este exemplo cria a regra atendimento chamada `MyCallAnsweringRule` na caixa de correio de Tony Smith e executa as seguintes ações:

  -  Define a prioridade da regra de atendimento de chamada para 2.

  -  Cria mapeamentos de teclas para a regra de atendimento de chamada.

  -  Se o chamador chegar no correio de voz do usuário e o status do usuário estiver configurado para Ocupado, o chamador pode:
    
      - Pressionar a tecla 1 e ser transferido para uma recepcionista no ramal 45678.
    
      - Pressionar a tecla 2 para que localizar-Me recurso seja usado para assuntos urgentes, toquem para o ramal 23456 primeiro e, em seguida, toque para a extensão 45671.

<!-- end list -->

    New-UMCallAnsweringRule -Name MyCallAnsweringRule -Priority 2 -Mailbox tonysmith -ScheduleStatus 0x4 - -KeyMappings "1,1,Receptionist,,,,,45678,","5,2,Urgent Issues,23456,23,45671,50,,"

