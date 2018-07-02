---
title: 'Agentes de transporte de modo de exibição no pipeline de transporte: Exchange 2013 Help'
TOCTitle: Agentes de transporte de modo de exibição no pipeline de transporte
ms:assetid: bd715d8e-7b21-48de-8f68-d425d8506e4c
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Bb124395(v=EXCHG.150)
ms:contentKeyID: 51407906
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Agentes de transporte de modo de exibição no pipeline de transporte

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2015-04-08_

Você pode usar o Shell de gerenciamento do Exchange para exibir uma lista de agentes de transporte no pipeline de transporte nos servidores de caixa de correio do Microsoft Exchange Server 2013 e acesso para cliente. Especificamente, o cmdlet **Get-TransportPipeline** mostra informações sobre os seguintes tipos de agentes de transporte no pipeline de transporte:

  - Operadores com base nas classes de **SmtpReceiveAgent**, **RoutingAgent**, **DeliveryAgent**e **StorageAgent** no serviço de transporte em servidores de caixa de correio.

  - Operadores com base no **SmtpReceiveAgentClass** no serviço de entrega de transporte de caixa de correio em servidores de caixa de correio.

  - Operadores com base no **SmtpReceiveAgentClass** no serviço Front End Transport em servidores de acesso para cliente.

Você pode exibir uma lista de todos os agentes de transporte habilitado que foram encontrados mensagens no pipeline de transporte e os eventos de SMTP em que estão registrados. Para obter mais informações sobre agentes de transporte, consulte [Agentes de transporte](transport-agents-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: cinco minutos

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Agentes de transporte" no tópico [Permissões de fluxo de email](mail-flow-permissions-exchange-2013-help.md) .

  - Você só pode usar o Shell para executar esse procedimento.

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>.



## Usar o Shell para exibir uma lista de agentes de transporte no pipeline de transporte

Para usar o Shell para exibir uma lista de agentes de transporte no pipeline de transporte em um servidor Exchange, execute o seguinte comando:

    Get-TransportPipeline | Format-List

Para exportar os resultados para um arquivo de texto chamado C:\\My Documents\\Transport Agents.txt, execute o seguinte comando:

    Get-TransportPipeline | Format-List > "C:\My Documents\Transport Agents.txt"

## Como saber se funcionou?

Apenas os agentes de transporte que foram encontrados mensagens no pipeline de transporte entre o tempo que o serviço de transporte foi iniciado e a hora de quando o cmdlet **Get-TransportPipeline** foi executado são exibidos pelo cmdlet. Um agente de transporte que ainda não encontrou uma mensagem no pipeline de transporte não aparecerá nos resultados da exibido pelo cmdlet **Get-TransportPipeline** , mesmo se esse agente de transporte está habilitado.

