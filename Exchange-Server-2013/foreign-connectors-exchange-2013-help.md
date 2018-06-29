---
title: 'Conectores externos: Exchange 2013 Help'
TOCTitle: Conectores externos
ms:assetid: 21c6a7a9-f4d2-4359-9ac9-930701b63a4e
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Aa996779(v=EXCHG.150)
ms:contentKeyID: 50485109
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Conectores externos

 

_**Aplica-se a:**Exchange Server 2013_

_**Tópico modificado em:**2012-09-25_

Um conector Estrangeiro entrega mensagens para um servidor ou sistema estrangeiro que não usa SMTP como seu mecanismo de transporte principal. Um exemplo disso pode ser um servidor de gateway de fax. Um conector Estrangeiro usa um diretório de Recebimento, para enviar mensagens de saída, através de uma transferência de arquivos, para o sistema estrangeiro. Os conectores estrangeiros são criados no serviço de Transporte de um servidor de Caixa de Correio do Microsoft Exchange Server 2013.

Os servidores de gateway estrangeiros podem enviar mensagens para a organização do Exchange 2013, usando os diretórios de Retirada ou Repetição que existem no serviço de Transporte de um servidor de Caixa de Correio. Arquivos de email formatados corretamente que você copia para cada diretório são enviados para entrega, para uma caixa de correio do Exchange.


> [!TIP]
> Na maioria dos casos onde você deve fornecer mensagens de saída a um sistema que não é SMTP, recomendamos conectores de Agente de Entrega, porque eles permitem o gerenciamento de filas de mensagens, as mensagens não precisam ser gravadas no sistema de arquivos, além de outros benefícios. O tópico <A href="delivery-agents-and-delivery-agent-connectors-exchange-2013-help.md">Agentes de entrega e conectores de agentes de entrega</A> fornece mais detalhes.



## Para obter mais informações

[Criar um conector estrangeiro para entregar mensagens a um gateway de fax não SMTP](create-a-foreign-connector-to-deliver-messages-to-a-non-smtp-fax-gateway-exchange-2013-help.md)

[Agentes de entrega e conectores de agentes de entrega](delivery-agents-and-delivery-agent-connectors-exchange-2013-help.md)

[New-ForeignConnector](https://technet.microsoft.com/pt-br/library/aa996310\(v=exchg.150\))

[Set-ForeignConnector](https://technet.microsoft.com/pt-br/library/bb123789\(v=exchg.150\))

