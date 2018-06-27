---
title: 'Agentes de entrega e conectores de agentes de entrega: Exchange 2013 Help'
TOCTitle: Agentes de entrega e conectores de agentes de entrega
ms:assetid: 38c942ee-b59d-47ec-87eb-bebad441ada5
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Dd638118(v=EXCHG.150)
ms:contentKeyID: 50485384
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Agentes de entrega e conectores de agentes de entrega

 

_**Aplica-se a:**Exchange Server 2013_

_**Tópico modificado em:**2016-12-09_

Um agente de entrega pode entregar mensagens do ambiente SMTP do servidor Exchange para um sistema que não use o protocolo SMTP. Cada agente de entrega é associado a um conector de Agente de Entrega, que coloca em fila as mensagens roteadas para cada agente de entrega, para processamento e entrega para o dispositivo ou sistema não SMTP.


> [!TIP]
> A arquitetura do conector Externo permanece no Microsoft Exchange 2013, mas, ainda assim, recomendamos usar os Agentes de Entrega para rotear mensagens para sistemas não-SMTP, sempre que possível. As razões principais para isso são: você pode usar o gerenciamento de fila para mensagens; não há necessidade de gerenciar a transferência de arquivos para um diretório de Entrega; e você pode verificar a entrega de mensagens.



**Conteúdo**

Function and benefits of Delivery Agents

Adding Delivery Agents to your organization

Delivery Agent connectors

Default text messaging Delivery Agent connector

## Função e benefícios dos Agentes de Entrega

Um agente de entrega é um componente instalado no serviço de Transporte de um servidor de Caixa de Correio que pode executar estas tarefas:

  - Estabelecer uma conexão para o sistema externo para a entrega de mensagens.

  - Recupere as mensagens das filas de entrega nos servidores de Caixa de Correio.

  - Entregar mensagens a um sistema externo.

  - Fornecer confirmação para cada entrega de mensagem bem-sucedida.

A arquitetura do conector Externo permanece no Microsoft Exchange Server 2013, mas, ainda assim, recomendamos usar os Agentes de Entrega para rotear mensagens para sistemas não-SMTP, sempre que possível. Agentes de Entrega oferecem os seguintes benefícios:

  - Eles permitem o gerenciamento da filas de mensagens roteadas para sistemas externos.

  - Como as mensagens não precisam mais ser gravadas e lidas no sistema de arquivos, o desempenho da entrega de mensagens é melhorado.

  - Eles fornecem acesso às propriedades de mensagem com eventos sofisticados para desenvolvedores de agentes.

  - O tempo de desenvolvimento para um Agente de Entrega é menor do que implementar um conector Externo, pois o Agente de Entrega pode usar os recursos de representação da mensagem e gerenciamento do Exchange.

  - Você pode verificar se as mensagens são entregues para o sistema externo, em vez de simplesmente gravá-las no diretório de Entrega.

  - O uso dos conectores do Agente de Entrega permite a análise do contrato de nível de serviço (SLA), porque agora é possível monitorar a latência da entrega da mensagem para o sistema externo.

## Adicionar Agentes de Entrega à sua organização

Para usar um Agente de Entrega na sua organização, siga estas instruções:

1.  Adquira o Agente de Entrega. Normalmente, os Agentes de Entrega são gravados por terceiros. O Exchange 2013 vem com apenas um conector de Agente de Entrega, por padrão: o conector de Agente de Entrega Mensagens de Texto.

2.  Instale o Agente de Entrega no serviço de Transporte dos servidores de Caixa de Correio que irão agir como servidores de origem dos conectores de Agente de Entrega.

3.  Criar um conector de Agente de Entrega para o protocolo específico.

Quando você terminar de aplicar essas instruções, as mensagens para sistemas externos serão roteadas através dos conectores de Agentes Externos e processadas pelo Agente de Entrega.

[Namespace deliveryhttp](https://go.microsoft.com/fwlink/?linkid=262690) fornece mais informações sobre o desenvolvimento de um agente de entrega.

## Conectores de Agente de Entrega

Um conector de Agente de Entrega no Exchange 2013 é similar ao conector de Agente de Entrega apresentado no Exchange 2010. Eles roteiam mensagens endereçadas para sistemas externos que não usem o protocolo SMTP. Quando uma mensagem é roteada para um conector de Agente de Entrega, o Agente de Entrega associado executa a conversão do conteúdo e a entrega da mensagem. Normalmente, os agentes de entrega são criados por um terceiro e configurados para funcionar com um conector de Agente de Entrega na sua organização.

Um conector de Agente de entrega não pode ser criado no Centro de Administração do Exchange. Em vez disso, crie um conector de Agente de Entrega, no Shell de Gerenciamento do Exchange, com o cmdlet [New-DeliveryAgentConnector](https://technet.microsoft.com/pt-br/library/dd351063\(v=exchg.150\)) e edite as propriedades do conector do Agente de Entrega com [Set-DeliveryAgentConnector](https://technet.microsoft.com/pt-br/library/dd351159\(v=exchg.150\)). Você pode especificar um ou mais servidores de Caixa de Correio de host para o conector, usando o parâmetro opcional *SourceTransportServers*.

## Conector do Agente de Entrega de Mensagens de Texto padrão

Você pode usar o conector Agente de Entrega de Mensagens de Texto para rotear mensagens para dispositivos móveis. No seu servidor do Exchange, execute `Get-DeliveryAgentConnector | fl` para exibir o conector e todos os seus parâmetros. Observe que o *DeliveryProtocol* é definido para `MOBILE`.

