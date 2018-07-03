---
title: 'Modelos de política de DLP: Exchange 2013 Help'
TOCTitle: Modelos de política de DLP
ms:assetid: c7b1a8e4-30d9-4409-85c5-f85ae023737d
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/JJ657730(v=EXCHG.150)
ms:contentKeyID: 50486606
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Modelos de política de DLP

 

_**Aplica-se a:**Exchange Online, Exchange Server 2013_

_**Tópico modificado em:**2015-01-14_

Você pode usar os modelos de política de prevenção (DLP) de perda de dados para começar a sua solução DLP no Microsoft Exchange 2013. Um modelo de política DLP é um modelo para uma diretiva. Você pode selecionar um modelo para começar o processo de criação de sua própria política de DLP personalizada. Dentro de sua política DLP, você pode personalizar as regras para garantir que ele atenda às suas necessidades de negócios para prevenção de perda de dados. Vários modelos de política são fornecidos pela Microsoft, mas não são a única maneira de implementar uma solução de prevenção de perda de dados em Exchange.

Procurando tarefas de gerenciamento relacionadas a modelos de política de DLP? Consulte [Procedimentos DLP](dlp-procedures-exchange-2013-help.md).

**Conteúdo**

Extend the templates and information types to meet your needs

Create your own new DLP policy template

Include DLP functionality with existing transport rules

Use DLP policies created by Microsoft

For more information

## Estender os modelos e tipos de informações para atender às suas necessidades

Você pode incorporar definições sensíveis ao conteúdo e modelos de política de Parceiros da Microsoft ou de arquivos que você mesmo desenvolveu como um complemento aos modelos de política de DLP, tipos de informação e as regras já fornecidos no Exchange 2013. Apresentamos aqui várias maneiras pelas quais você pode adicionar seu próprio conteúdo DLP exclusivo e ampliar a funcionalidade de DLP. Os modelos já fornecidos pela Microsoft são um método conveniente para começar com uma solução de DLP. Para estender os recursos de DLP com os seus próprios arquivos exclusivos de modelo de política de DLP, você deve entender os requisitos de esquema XML para modelos de política que são criados independentemente do Exchange. Para saber mais sobre os cmdlets do Shell de Gerenciamento do Exchange associados a modelos de política de DLP, consulte os cmdlets relacionados a `Get-DlpPolicyTemplate` em [Cmdlets de política e conformidade](https://technet.microsoft.com/pt-br/library/dd298082\(v=exchg.150\)). Além disso, você pode definir seus próprios tipos de conteúdo sensível depois de entender o formato e o procedimento para incorporá-los. Para saber mais sobre os cmdlets do Shell de Gerenciamento do Exchange associados a modelos de política de DLP, consulte os cmdlets relacionados a `Get-ClassificationRuleCollection` em [Cmdlets de política e conformidade](https://technet.microsoft.com/pt-br/library/dd298082\(v=exchg.150\)).


> [!WARNING]
> Você deve ativar as políticas de DLP no modo de teste antes de aplicá-las ao seu ambiente de produção. Durante esses testes, recomendamos que você configure exemplos de caixas de correio de usuários e envie mensagens de teste que invoquem as políticas de teste para confirmar os resultados.



## Crie o seu próprio novo modelo de política de DLP ou os seus próprios tipos de informações confidenciais em um pacote de regras de classificação

Você pode criar um arquivo de modelo de política de DLP independente do Exchange que atenda à definição de esquema XML específica fornecida pela Microsoft e, em seguida, importar esse arquivo no seu sistema para poder criar políticas de DLP a partir dele. Criando seus próprios arquivos de modelo, você pode definir seu próprio modelo para as políticas de DLP que a Microsoft ainda não tenha fornecido. Isso é diferente de criar uma política de DLP usando o Centro de Administração do Exchange, o que normalmente acontece depois que os modelos de política ficam disponíveis. Se você criar um modelo de política independente do Exchange, você terá que importá-lo antes que possa usá-lo para verificar mensagens. Você também pode criar suas próprias definições de informações sensíveis além das definidas pela Microsoft em Exchange. Há uma definição de esquema XML separada para arquivos de modelo de política de DLP e pacotes de regras de classificação. Para começar, consulte as informações a seguir:

  -  [Definir seus próprios modelos de DLP e tipos de informações](define-your-own-dlp-templates-and-information-types-exchange-2013-help.md)

  -  [Importar um modelo de política DLP personalizado de um arquivo](import-a-custom-dlp-policy-template-from-a-file-exchange-2013-help.md)

## Incluem a funcionalidade de DLP com regras de transporte existentes

Você pode incorporar recursos de detecção de DLP com regras de transporte tradicionais sem criar uma política de DLP nova. Se você criou um conjunto complexo de regras em uma versão anterior do Exchange, e quer duplicá-los ou adicionar detecção de informações sensíveis em Exchange 2013, então você pode usar o editor de regras de transporte no Exchange Administration Center o Shell de Gerenciamento do Exchange para incorporar esses dois recursos. Para começar, consulte as informações a seguir:

  -  [Regras de fluxo de emails ou de transporte](mail-flow-rules-transport-rules-in-exchange-2013-exchange-2013-help.md) (Exchange Server 2013)

  -  [Regras de fluxo de emails (regras de transporte) no Exchange Online](https://technet.microsoft.com/pt-br/library/jj919238\(v=exchg.150\)) (Exchange Online)

  -  [Gerenciar regras de fluxo de emails](manage-mail-flow-rules-exchange-2013-help.md)
    
    [Cmdlets de política e conformidade](https://technet.microsoft.com/pt-br/library/dd298082\(v=exchg.150\))

## Usar diretivas DLP, criadas pela Microsoft

Diversas políticas DLP são fornecidas pela Microsoft. Esta é a maneira mais fácil de começar uma solução de DLP que é flexível e simples de implementar. Você sempre pode usar as políticas previstas como ponto de partida e personalizar-las ainda mais para atender às suas necessidades. Para começar, consulte as informações a seguir:

  - [Modelos de política DLP fornecidos no Exchange](dlp-policy-templates-supplied-in-exchange-exchange-2013-help.md)

  - [Criar uma política de DLP a partir de um modelo](how-to-new-dlp-data-loss-prevention-policy-template.md)

## Para obter mais informações

[Prevenção de perda de dados](technical-overview-of-dlp-data-loss-prevention-in-exchange.md)

