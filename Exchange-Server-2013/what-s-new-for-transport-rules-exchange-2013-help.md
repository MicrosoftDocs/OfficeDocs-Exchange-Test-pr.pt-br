---
title: 'Novidades sobre regras de transporte: Exchange 2013 Help'
TOCTitle: Novidades sobre regras de transporte
ms:assetid: 0c2fc0b5-3cd2-4d79-aa2b-0c7622ae15a8
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/JJ150483(v=EXCHG.150)
ms:contentKeyID: 50484994
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Novidades sobre regras de transporte

 

_**Aplica-se a:** Exchange Online, Exchange Server 2013_

_**Tópico modificado em:** 2014-10-03_

No Microsoft Exchange Server 2013, várias melhorias foram feitas para as regras de transporte. Este tópico oferece uma visão geral resumida de alguns das principais mudanças e melhorias. Para saber mais sobre regras de transporte, consulte [Regras de fluxo de emails ou de transporte](mail-flow-rules-transport-rules-in-exchange-2013-exchange-2013-help.md).

## Suporte para políticas de prevenção de perda de dados

Os recursos de prevenção de perda de dados (DLP) do Exchange 2013 podem ajudar as organizações a reduzir a divulgação não intencional de dados confidenciais. As regras de transporte foram atualizadas para suportar a criação de regras que acompanham e impõem políticas de DLP. Para saber mais sobre o suporte a DLP nas regras de transporte, consulte estes tópicos:

[Integrando regras de informações confidenciais com regras de transporte](integrating-sensitive-information-rules-with-transport-rules-exchange-2013-help.md)

[Prevenção de perda de dados](technical-overview-of-dlp-data-loss-prevention-in-exchange.md)

## Novas ações e predicados

A funcionalidade e as regras de transporte foram expandidas, com a adição de novos predicados e ações. Cada predicado listado abaixo pode ser usado como uma condição ou uma exceção, quando você estiver criando regras de transporte.

Para informações detalhadas sobre como usar esses novos predicados e ações, consulte [Condições de regra de transporte (predicados)](mail-flow-rule-conditions-and-exceptions-predicates-in-exchange-2013-exchange-2013-help.md) e [Ações de regra de transporte](mail-flow-rule-actions-in-exchange-2013-exchange-2013-help.md).

## Novos predicados

  -  
    **AttachmentExtensionMatchesWords**   Usado para detectar mensagens que contêm anexos com extensões específicas.

  -  
    **AttachmentHasExecutableContent**   Usado para detectar mensagens que contêm anexos com conteúdo executável.

  -  
    **HasSenderOverride** Usado para detectar mensagens cujo remetente tenha escolhido substituir uma restrição de política de DLP.

  -  
    **MessageContainsDataClassifications**   Usado para detectar informações confidenciais no corpo da mensagem e em qualquer dos anexos. Para obter uma lista das classificações de dados disponíveis, consulte [O que os tipos de informações confidenciais no Exchange procurar](what-the-sensitive-information-types-in-exchange-look-for-exchange-online-help.md).

  -  
    **MessageSizeOver**   Usado para detectar mensagens cujo tamanho geral seja maior ou igual ao limite especificado.

  -  
    **SenderIPRanges**   Usado para detectar mensagens enviadas de um conjunto específico de intervalos de endereços IP.

## Novas ações

  -  
    **GenerateIncidentReport**   Gera um relatório de incidentes que é enviado para um endereço SMTP específico. A ação também tem um parâmetro chamado *IncidentReportOriginalMail* que aceita um de dois valores: IncludeOriginalMail ou DoNotIncludeOriginalMail.

  -  
    **NotifySender**   Controla como o remetente de uma mensagem que não está de acordo com uma política DLP é notificado. Você pode optar por simplesmente informar o remetente e rotear a mensagem normalmente ou rejeitar a mensagem e notificar o remetente.

  -  
    **StopRuleProcessing**   Interrompe o processamento de todas as regras subsequentes na mensagem.

  -  
    **ReportSeverityLevel**   Define o nível de severidade especificado no relatório de incidentes. Os valores da ação são: Informacional, Baixo, Médio, Alto e Desativado.

  -  
    **RouteMessageOutboundRequireTLS**   Requer uma criptografia de Segurança de Camada de Transporte (TLS) ao se rotear essa mensagem fora da sua organização. Se não houver suporte para a criptografia TLS, a mensagem será rejeitada e não entregue.

## Outras mudanças em regras de Transporte

  - **Suporte para sintaxe de expressão regular estendida**   As regras de transporte no Exchange 2013 são baseadas na funcionalidade da expressão regular (regex) do Microsoft.NET Framework e agora suportam sintaxe de expressão regular estendida.

  - **Invocação do agente de regras de transporte**   A principal mudança na arquitetura do Exchange 2013 para regras de Transporte é que o Agente de Regras de Transporte é invocado no onResolvedMessage. Nas versões anteriores do Exchange, o Agente de Regras era invocado no onRoutedMessage. Essa mudança nos permitiu adicionar novas ações, como requerer TLS, o que pode mudar como uma mensagem é roteada. Para saber mais sobre a arquitetura de regras de transporte do Exchange 2013, consulte [Regras de fluxo de emails ou de transporte](mail-flow-rules-transport-rules-in-exchange-2013-exchange-2013-help.md).

  - **Informações de regra de Transporte detalhadas nos logs de monitoramento de mensagem**   Informações detalhadas sobre as regras de Transporte agora estão inclusas nos logs de monitoramento de mensagens. As informações incluem quais regras foram acionadas para uma mensagem específicas e as ações executadas como um resultado do processamento dessas regras.

  - **Nova funcionalidade de monitoramento de regras**   O Exchange 2013 monitora as regras de Transporte que são configuradas e mede o custo de executar essas regras tanto quando você estiver criando a regra quanto durante o funcionamento regular. O Exchange pode detectar e gerar alertas para regras que estão causando atrasos na entrega do email.

