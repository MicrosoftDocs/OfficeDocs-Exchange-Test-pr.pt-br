---
title: 'Definir seus próprios modelos de DLP e tipos de informaçõess'
TOCTitle: Definir seus próprios modelos de DLP e tipos de informações
ms:assetid: f4622dba-3347-4758-b4a2-f01b043c908c
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/JJ674310(v=EXCHG.150)
ms:contentKeyID: 50487003
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Definir seus próprios modelos de DLP e tipos de informações

 

_**Aplica-se a:** Exchange Online, Exchange Server 2013_

_**Tópico modificado em:** 2015-01-14_

Você pode desenvolver modelos de política de prevenção contra perda de dados (DLP) como arquivos XML independentes do Microsoft Exchange Server 2013 e importá-los usando o Centro de Administração do Exchange ou o Shell de gerenciamento do Exchange. Esta seção descreve o processo e os detalhes de criação e ajuste de arquivos XML de DLP para uso em uma solução de DLP. Você não precisa desenvolver seus próprios arquivos XML de DLP porque o Centro de Administração do Exchange oferece uma forma de começar rapidamente com modelos de política de DLP e regras de transporte existentes para verificar mensagens.

Procurando tarefas de gerenciamento relacionadas aos modelos de política DLP? Consulte [Procedimentos DLP](dlp-procedures-exchange-2013-help.md) (Exchange Server 2013 ) ou [Procedimentos DLP](https://technet.microsoft.com/pt-br/library/jj938003\(v=exchg.150\)) (Exchange Online ).


> [!NOTE]  
> Exchange 2013: DLP é um recurso premium que exige uma licença dos Serviços da Enterprise CAL do Exchange. Para saber mais sobre CALs e sobre licenciamento de servidor, confira o artigo <A href="https://go.microsoft.com/fwlink/p/?linkid=237292">Licenciamento do Exchange Server</A>.<BR>Exchange Online: DLP é um recurso premium que exige uma assinatura do Plano 2 do Exchange Online. Para saber mais, confira <A href="https://go.microsoft.com/fwlink/p/?linkid=286154">Licenciamento do Exchange Online</A>.




> [!IMPORTANT]
> Ela está além do escopo desta documentação para recomendar um modelo comercial ou informações sobre o empacotamento de arquivos ou diretrizes de implantação para as regras de informações sensíveis ou para discutir como essas regras seriam distribuídas. Além do mais, esta documentação não discute mecanismos de proteção, como criptografia, para regras desenvolvidas personalizadas, e também não discute como esse mecanismo seria empregado.



## Estender os tipos de informações para atender às suas necessidades

As seguintes seções descrevem os conceitos e a definição de esquema XML que você deve entender para começar a criar seus próprios arquivos XML para modelos de política de DLP e pacotes de regras de informações confidenciais que podem ser importados no Exchange 2013 e usados como políticas de DLP.

A DLP no Microsoft Exchange o ajuda a aplicar a política específica de organização a informações confidenciais. Um fator importante no poder de uma solução de DLP é a capacidade de identificar corretamente as informações confidenciais ou sensíveis que podem ser exclusivas da organização, de necessidades regulamentares, de região ou de outros aspectos comerciais. Embora a Microsoft tenha fornecido modelos de política e tipos de informações sensíveis no produto para que você possa começar, suas necessidades de negócios exclusivas podem exigir uma solução personalizada de prevenção contra perda de dados. Por esse motivo, a Microsoft oferece uma forma de você criar e importar seus próprios modelos de política de DLP ou suas próprias definições de informações confidenciais com pacotes de regras de classificação. Uma solução de DLP precisa depende da configuração do conjunto correto de regras do mecanismo de detecção de informações confidenciais ofereçam um grau alto de proteção enquanto minimizam os falsos positivos e negativos.

## Desenvolver seus próprios modelos de política de DLP

Você pode escrever seu próprio arquivo XML de modelo de política de DLP e importá-lo. Essa abordagem para estender a solução de DLP fornecida no Exchange permitirá que você crie políticas de DLP mais próximas de seus requisitos de DLP.

O gerenciamento de modelos personalizados e suas políticas relacionadas é parecido com o gerenciamento de políticas de DLP criadas com base em modelos fornecidos pela Microsoft. Em um típico ciclo de vida de política DLP, faça o seguinte:

1.  Crie seu próprio modelo de política de DLP, um arquivo XML personalizado. Para saber mais, consulte [Desenvolver arquivos de modelo de política de DLP](xml-rule-schema-and-rule-structure-guide-for-dlp-policy-files.md).

2.  Importe o modelo personalizado. Para saber mais, consulte [Importar um modelo de política DLP personalizado de um arquivo](import-a-custom-dlp-policy-template-from-a-file-exchange-2013-help.md).

3.  Crie uma política de DLP com base em seu modelo personalizado. Para saber mais, consulte [Criar uma política de DLP a partir de um modelo](https://docs.microsoft.com/pt-br/exchange/security-and-compliance/data-loss-prevention/create-dlp-policy-from-template).

4.  Atualize o modelo personalizado, repetindo as etapas 1 e 2.

5.  Remova o modelo personalizado. Para saber mais, consulte [Remove-DlpPolicyTemplate](https://technet.microsoft.com/pt-br/library/jj215739\(v=exchg.150\)).

Para mais informações sobre a definição de esquema XML e os conceitos relacionados ao desenvolvimento de seus próprios modelos, consulte [Desenvolver arquivos de modelo de política de DLP](xml-rule-schema-and-rule-structure-guide-for-dlp-policy-files.md).

## Desenvolver seus próprios tipos de informações confidenciais e a lógica correspondente nos pacotes de regra de classificação

Você pode escrever suas próprias definições de informações confidenciais em um pacote de regra de classificação, que é um arquivo XML, e importe-o como parte de sua solução DLP. O mecanismo de detecção de informações confidenciais fornece os recursos de análise de conteúdo completos para identificar informações confidenciais como números de cartão de crédito, números de seguridade social e propriedade intelectual da empresa. O mecanismo é controlado por um conjunto configurável de instruções, ou regras, para verificar e analisar o conteúdo. As regras são combinadas em um pacote de regra de classificação, um documento XML que adota uma definição de esquema XML de pacote de regras padronizado. Veja como você pode desenvolver seu próprio.

1.  Crie seus próprios tipos de informações confidenciais, um arquivo XML personalizado. Para saber mais, consulte [Desenvolver pacotes de regras de informações confidenciais](technical-description-of-xml-schema-for-dlp-rule-packages.md).

2.  Importe seu tipo de informação confidencial. Para saber mais, consulte [New-ClassificationRuleCollection](https://technet.microsoft.com/pt-br/library/jj218619\(v=exchg.150\)).

3.  Crie um modelo personalizado com base em seus tipos de informações. Para saber mais, consulte [Desenvolver pacotes de regras de informações confidenciais](technical-description-of-xml-schema-for-dlp-rule-packages.md)

4.  Atualize o modelo personalizado, repetindo as etapas 1 e 2.

5.  Remova o modelo personalizado. Para saber mais, consulte [Remove-ClassificationRuleCollection](https://technet.microsoft.com/pt-br/library/jj218670\(v=exchg.150\))

Para mais informações sobre os pacotes de regras, consulte [Desenvolver pacotes de regras de informações confidenciais](technical-description-of-xml-schema-for-dlp-rule-packages.md) e [Métodos e técnicas para pacotes de regras correspondentes](technical-description-of-xsd-rule-matching-for-dlp-rule-packages.md).

## Noções básicas sobre tipos de regra em pacotes de regras

As regras em um pacote de regras configuram o processo de detecção de características de conteúdo bem-definidas; por exemplo, regras para localizar o número de uma carteira de motorista. Estão disponíveis dois tipos de regras principais: Entidade e Afinidade.

As regras de *Entidade* são direcionadas a identificadores bem-definidos (e às vezes regulamentados), como números de seguridade social dos EUA. Uma Entidade é representada por uma coleção de padrões contáveis. Um padrão define uma coleção de correspondências com um identificador de correspondência principal explícito. Uma Entidade de exemplo é a carteira de motorista.

As regras de *Afinidade* são direcionadas a um certo tipo de documento, como demonstrativo financeiro corporativo. Uma Afinidade é representada como uma coleção de evidências independentes. Evidência é uma agregação de correspondências necessárias dentro de uma certa proximidade. Um exemplo de Afinidade é o Sarbanes-Oxley Act dos EUA.

## Para obter mais informações

[Prevenção de perda de dados](https://docs.microsoft.com/pt-br/exchange/security-and-compliance/data-loss-prevention/data-loss-prevention)

[Importar um modelo de política DLP personalizado de um arquivo](import-a-custom-dlp-policy-template-from-a-file-exchange-2013-help.md)

[New-ClassificationRuleCollection](https://technet.microsoft.com/pt-br/library/jj218619\(v=exchg.150\))

[Regras de fluxo de emails ou de transporte](mail-flow-rules-transport-rules-in-exchange-2013-exchange-2013-help.md) Exchange Server 2013

[Regras de fluxo de emails (regras de transporte) no Exchange Online](https://technet.microsoft.com/pt-br/library/jj919238\(v=exchg.150\)) Exchange Online

[O que os tipos de informações confidenciais no Exchange procurar](what-the-sensitive-information-types-in-exchange-look-for-exchange-online-help.md)

