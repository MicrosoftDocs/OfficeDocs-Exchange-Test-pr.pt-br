---
title: 'Configurar a duração máxima da chamada: Exchange 2013 Help'
TOCTitle: Configurar a duração máxima da chamada
ms:assetid: 01aa40d2-f918-472b-bace-158222143484
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Ee423535(v=EXCHG.150)
ms:contentKeyID: 50484869
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configurar a duração máxima da chamada

 

_**Aplica-se a:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Tópico modificado em:**2012-11-09_

Você pode especificar o número máximo de minutos que uma chamada de entrada pode permanecer conectada ao sistema sem ser transferida para um número de ramal válido antes de a chamada ser encerrada. Para a maioria das organizações, esse valor deve ser definido como o padrão: 30 minutos. Essa configuração se aplica a todas as chamadas, incluindo chamadas de entrada do Outlook Voice Access, chamadas de voz internas para sua organização, chamadas de voz para os atendedores de voz de Unificação de Mensagens (UM) e chamadas de voz e fax originadas fora da sua organização.

Esse valor pode ser definido como um número entre 10 e 120. Definir esse valor muito baixo pode fazer com que as chamadas de voz sejam desconectadas antes de serem concluídas. Por exemplo, se sua organização recebe muitas mensagens de fax grandes, talvez você queira aumentar esse valor a partir do padrão, de modo que todas as páginas das mensagens de fax sejam recebidas.

Para tarefas adicionais relacionadas a planos de discagem de UM, consulte [Procedimentos de plano de discagem de UM](um-dial-plan-procedures-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: Menos de 1 minuto.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Planos de discagem da UM" no tópico [Permissões de mensagens unificadas](unified-messaging-permissions-exchange-2013-help.md).

  - Antes de executar esses procedimentos, confirme se um plano de discagem de UM foi criado. Para obter etapas detalhadas, consulte [Criar um plano de discagem de UM](create-a-um-dial-plan-exchange-2013-help.md).

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>..



## O que você deseja fazer?

## Usar o EAC para configurar a duração máxima da chamada

1.  No EAC, navegue até **Unificação de Mensagens** \> **Planos de discagem de UM**.

2.  No modo de exibição de lista, selecione o plano de discagem de UM que você deseja modificar e clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").

3.  Na página **Plano de discagem de UM**, clique em **Configurar**.

4.  Em **Configurações**, em **Duração máxima da chamada (minutos)**, insira o número de minutos.

5.  Clique em **Salvar**.

## Usar o Shell para configurar a duração máxima de chamada

Este exemplo define a duração máxima de chamada como 10 minutos em um plano de discagem de UM chamado `MyUMDialPlan`.

    Set-UMDialPlan -identity MyUMDialPlan -MaxCallDuration 10

