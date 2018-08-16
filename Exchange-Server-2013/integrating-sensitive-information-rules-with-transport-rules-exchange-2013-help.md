---
title: 'Integrar regras de informações confidenciais com regras de transporte'
TOCTitle: Integrando regras de informações confidenciais com regras de transporte
ms:assetid: feb014a7-89dd-4f2d-a06d-52806ce435d4
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/JJ150583(v=EXCHG.150)
ms:contentKeyID: 50484824
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Integrando regras de informações confidenciais com regras de transporte

 

_**Aplica-se a:** Exchange Online, Exchange Server 2013_

_**Tópico modificado em:** 2015-01-14_

No Microsoft Exchange, você pode criar políticas de DLP que contêm regras para classificações de mensagem tradicional não apenas e regras de transporte existentes, mas também combiná-los com regras de informações confidenciais encontradas nas mensagens. A estrutura de regras de transporte existentes oferece recursos avançados para definir políticas de mensagens, que abrangem toda a gama de suave aos controles de disco rígidos. Exemplos incluem:

  - Limitando a interação entre destinatários e remetentes, incluindo interações entre grupos departamentais dentro de uma organização.

  - Aplicando diretivas separadas para comunicações dentro e fora da organização.

  - Evitar que conteúdo inadequado entre ou saia de uma organização.

  - Filtragem de informações confidenciais.

  - Acompanhar ou arquivar mensagens que são enviadas ou recebidas de determinadas pessoas.

  - Redirecionar mensagens de entrada e saídas para inspeção antes da entrega.

  - Aplicar avisos de isenção às mensagens transmitidas pela organização.

Regras de transporte permitem que você aplique políticas de mensagens para mensagens de email desse fluxo através do pipeline de transporte no serviço de transporte nos servidores de caixa de correio e nos servidores de transporte de borda. Essas regras permitem que os administradores de sistema para impor políticas de mensagens, para ajudar a manter as mensagens mais seguro, ajudam a proteger os sistemas de mensagens e ajudar a evitar perda de informações acidental. Para obter mais informações sobre regras de transporte, consulte [Regras de fluxo de emails ou de transporte](mail-flow-rules-transport-rules-in-exchange-2013-exchange-2013-help.md) ( Exchange Server 2013 ) ou [Regras de fluxo de emails (regras de transporte) no Exchange Online](https://technet.microsoft.com/pt-br/library/jj919238\(v=exchg.150\)) (Exchange Online ).

## Regras de informações confidenciais dentro da estrutura de regra de transporte

Regras de informações confidenciais são integradas com a estrutura de regras de transporte por introdução de uma condição que você pode personalizar: **se a mensagem contiver … Informações confidenciais**. Esta condição pode ser configurada com um ou mais tipos de informações confidenciais que estão contidos dentro de mensagens. Quando várias políticas de DLP ou regras dentro de uma diretiva são configuradas com essa condição, a política ou a regra será satisfeita quando qualquer uma das condições corresponder. regras de política de Exchange examinar o assunto, corpo e quaisquer anexos de uma mensagem. Se a regra corresponder a qualquer um desses componentes de mensagem, as ações de regra serão aplicadas.

A condição de informações confidenciais pode ser combinada com qualquer uma das regras de transporte já existente para definir políticas de mensagens. Se combinada, a condição funciona em conjunto com outras regras e fornece a semântica AND. Por exemplo, duas condições diferentes são acrescentadas em conjunto com uma instrução de e para que ambos precisam corresponder para a ação a ser aplicado. Entre as ações de regra de transporte pode ser configurado como resultado de regras que contenham a correspondência de tipos de informações confidenciais. Muitos tipos de arquivo diferentes podem ser verificados pelo agente de regras de transporte, que verifica as mensagens para impor regras de transporte. Para saber mais sobre os tipos de arquivo com suporte, consulte [Usar regras de transporte para inspecionar anexos de mensagens](use-transport-rules-to-inspect-message-attachments-exchange-2013-help.md) (Exchange Server 2013 ) ou [Usar regras de fluxo de email para inspecionar anexos de mensagens no Office 365](https://technet.microsoft.com/pt-br/library/jj919236\(v=exchg.150\)) (Exchange Online ).

As regras também podem ser usadas na parte de exceção de uma definição de regra. Seu uso na definição de exceção é independente do seu uso como uma condição de regra. Isso oferece flexibilidade para definir as regras que têm a condição especificando vários tipos de informação a ser aplicado como parte da condição e também diferentes tipos de informações da condição. Isso só permitia políticas como correspondência com regras de classificação tradicional de mensagem específicos, mas não correspondência outros tipos de informações confidenciais antes de executar ações que você define dentro de uma política.

## Para obter mais informações

[Prevenção de perda de dados](technical-overview-of-dlp-data-loss-prevention-in-exchange.md)

[O que os tipos de informações confidenciais no Exchange procurar](what-the-sensitive-information-types-in-exchange-look-for-exchange-online-help.md)

[Regras de fluxo de emails ou de transporte](mail-flow-rules-transport-rules-in-exchange-2013-exchange-2013-help.md) Exchange Server 2013

[Regras de fluxo de emails (regras de transporte) no Exchange Online](https://technet.microsoft.com/pt-br/library/jj919238\(v=exchg.150\)) Exchange Online

[Criar uma política DLP personalizada](create-a-custom-dlp-policy-exchange-2013-help.md)

