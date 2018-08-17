---
title: 'Prevenção de perda de dados: Exchange Online Help'
TOCTitle: Prevenção de perda de dados
ms:assetid: 7c8ed3c1-ca91-4d9b-b16b-0a2b8ac89730
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/JJ150527(v=EXCHG.150)
ms:contentKeyID: 50484739
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Prevenção de perda de dados

 

_**Aplica-se a:** Exchange Online, Exchange Server 2013_

_**Tópico modificado em:** 2016-12-09_

Saiba mais sobre políticas DLP no Exchange Server 2013 e o Exchange Online, incluindo o que elas contêm e como testá-las. Você também saberá mais sobre um novo recurso no Exchange DLP.

A prevenção de perda de dados (DLP) é um problema importante para sistemas de mensagens corporativas, por causa do uso intenso de emails para comunicações críticas de negócios que incluem dados confidenciais. Para impor os requisitos de conformidade para tais dados e gerenciar seu uso em emails, sem atrapalhar a produtividade dos funcionários, os recursos de DLP permitem gerenciar dados confidenciais com mais facilidade do que nunca. Para obter uma visão geral conceitual do DLP, assista ao seguinte vídeo.

> [!VIDEO https://www.microsoft.com/pt-br/videoplayer/embed/31f2b48e-93ed-4be3-b46d-e7230c0fed8f]

As políticas DLP são pacotes simples que contêm conjuntos de condições que são compostas de regras, ações e exceções de transporte que você cria no Centro de Administração do Exchange (EAC) e ativa para filtrar mensagens de email e anexos. Você pode criar uma política de DLP, mas optar por não ativá-la. Isso permite que você teste suas políticas sem afetar o fluxo de emails. As políticas DLP podem usar todo o poder de regras de transporte existentes. Na verdade, vários novos tipos de regras de transporte foram criados no Exchange Server 2013 e no Exchange Online, a fim de realizar um novo recurso DLP. Um novo recurso importante das regras de transporte é um novo enfoque para classificar informações confidenciais que podem ser incorporadas ao processamento de fluxo de emails. Esse novo recurso DLP executa uma análise profunda de conteúdo, através de comparações de palavras-chave, comparações de dicionários e avaliação de expressões regulares e outros exames de conteúdo para detectar conteúdo que viole as políticas DLP organizacionais. A versão mais recente do Exchange Online e do Exchange 2013 SP1 adicionam a [Impressão Digital de Documento](overview-of-document-fingerprinting-in-exchange.md), que ajuda a detectar informações confidenciais em formulários padrão. Para saber mais sobre regras de transporte, consulte [Regras de fluxo de emails ou de transporte](mail-flow-rules-transport-rules-in-exchange-2013-exchange-2013-help.md) (Exchange 2013) ([Regras de fluxo de emails (regras de transporte) no Exchange Online](https://technet.microsoft.com/pt-br/library/jj919238\(v=exchg.150\))) (Exchange Online) e [Integrando regras de informações confidenciais com regras de transporte](integrating-sensitive-information-rules-with-transport-rules-exchange-2013-help.md). Você também pode gerenciar suas políticas de DLP usando os cmdlets do Shell de Gerenciamento do Exchange. Para saber mais sobre cmdlets de políticas e conformidade, consulte [Cmdlets de política e conformidade](https://technet.microsoft.com/pt-br/library/dd298082\(v=exchg.150\)).

Além das próprias políticas de DLP personalizáveis, você também pode informar aos remetentes de email que eles podem estar prestes a violar uma de suas políticas — mesmo antes de enviarem uma mensagem ofensiva. Você pode fazer isso configurando a Política de Dicas. As Dicas de Política são similares às Dicas de Email e podem ser configuradas para apresentar uma nota breve no cliente do Microsoft Outlook 2013 que oferece informações sobre possíveis violações de política para a pessoa que está criando uma mensagem. Na versão mais recente do Exchange Online e no Exchange 2013 SP1, as Dicas de Política também são exibidas no Outlook Web App e no OWA para dispositivos. Para mais informações, consulte [Dicas de política](technical-overview-of-policy-tips-in-exchange-online-and-exchange-2013.md).


> [!NOTE]
> Exchange Online: DLP é um recurso premium que exige uma assinatura do Plano 2 do Exchange Online. Para saber mais, confira <A href="https://go.microsoft.com/fwlink/p/?linkid=286154">Licenciamento do Exchange Online</A>.<BR>Exchange 2013: DLP é um recurso premium que exige uma licença dos Serviços da Enterprise CAL do Exchange. Para saber mais sobre CALs e sobre licenciamento de servidor, confira o artigo <A href="https://go.microsoft.com/fwlink/p/?linkid=237292">Licenciamento do Exchange Server</A>.<BR><STRONG>Exchange Enterprise CAL com Serviços:</STRONG> Existe uma diferença de comportamento que deve ser observada se você for um cliente do Exchange Enterprise CAL com Serviços com implantação híbrida, em que algumas caixas de correio são locais e outras estão no Exchange Online. As políticas de DLP são aplicadas no Exchange Online. Portanto, as mensagens enviadas do usuário local para outro usuário local não possui as políticas de DLP aplicadas, porque a mensagem não deixa a infraestrutura local.



Procurando tarefas de gerenciamento relacionadas a Prevenção contra Perda de Dados? Consulte [Procedimentos DLP](dlp-procedures-exchange-2013-help.md) (Exchange 2013) ou [Procedimentos DLP](https://technet.microsoft.com/pt-br/library/jj938003\(v=exchg.150\)) (Exchange Online).

**Sumário**

Estabelecer políticas para proteger dados confidenciais

Tipos de informações confidenciais em políticas de DLP

Detectar informações confidenciais, juntamente com a classificação tradicional de mensagens

Detectar dados confidenciais de formulário com a Impressão Digital de Documento

As Dicas de Política notificam os usuários sobre as expectativas em relação a conteúdo confidencial

Informações sobre mensagens processadas por DLP

Pré-requisitos de instalação

Para obter mais informações

## Estabelecer políticas para proteger dados confidenciais

Os recursos de prevenção de perda de dados podem ajudar você a identificar e monitorar muitas categorias de informações confidenciais que você definiu dentro das condições de suas políticas, como números de identificação particular ou números de cartão de crédito. Você tem a opção de definir suas próprias políticas e regras de transporte personalizadas ou de usar os modelos de política de DLP predefinidos fornecidos pela Microsoft para começar rapidamente. Para mais informações sobre os modelos de políticas incluídos, consulte [Modelos de política DLP fornecidos no Exchange](dlp-policy-templates-supplied-in-exchange-exchange-2013-help.md). Um *modelo de política* inclui várias condições, regras e ações dentre as quais você escolher para criar e salvar uma política de DLP real que irá ajudá-lo a inspecionar mensagens. Os modelos de política são modelos a partir dos quais você pode selecionar ou construir suas próprias regras específicas para criar uma política que atenda às suas necessidades, no tocante à prevenção de perda de dados.

Três métodos diferentes existem para você começar a usar DLP:

1.  **Aplicar um modelo pronto fornecido pela Microsoft.**   O jeito mais rápido de começar a usar políticas de DLP é criar e implementar uma nova política, usando um modelo. Isso faz que você não precise se esforçar para construir um novo conjunto de regras partindo do zero. Você precisará saber que tipos de dados você precisa verificar ou que regulamentação de conformidade você está tentando endereçar. Você também precisará saber as expectativas das suas organizações para processar tais dados. Mais informações em [Modelos de política DLP fornecidos no Exchange](dlp-policy-templates-supplied-in-exchange-exchange-2013-help.md) e [Criar uma política de DLP a partir de um modelo](how-to-new-dlp-data-loss-prevention-policy-template.md).

2.  **Importar um arquivo de política previamente criado de fora da sua organização**   Você pode importar políticas que já foram criadas fora do seu ambiente de mensagens por fornecedores de software independentes. Desse jeito, você pode adequar as soluções DLP para ficarem de acordo com seus requisitos de negócios. Mais informações em [Modelos de política de parceiros da Microsoft](policy-templates-from-microsoft-partners-exchange-2013-help.md), [Definir seus próprios modelos de DLP e tipos de informações](define-your-own-dlp-templates-and-information-types-exchange-2013-help.md) e [Importar um modelo de política DLP personalizado de um arquivo](import-a-custom-dlp-policy-template-from-a-file-exchange-2013-help.md).

3.  **Criar uma política personalizada sem nenhuma condição pré-existente.**   A sua empresa pode ter seus próprios requisitos para monitorar certos tipos de dados conhecidos dentro de um sistema de mensagens. Você pode criar uma política personalizada totalmente por si só, para começar a verificar e agir em relação aos seus dados de mensagens exclusivos. Você precisará conhecer os requisitos e as restrições do ambiente em que a política de DLP será imposta para criar essa política personalizada. Mais informações em [Criar uma política DLP personalizada](create-a-custom-dlp-policy-exchange-2013-help.md).

Depois de você ter adicionado uma política, você poderá revisá-la e alterar as regras dela, deixar a política inativa ou removê-la completamente. Os procedimentos para essas ações são fornecidos no tópico [Gerenciar políticas de DLP](manage-dlp-policies-exchange-2013-help.md).

## Tipos de informações confidenciais em políticas de DLP

Ao criar ou alterar políticas DLP, você pode incluir regras que incluam verificações de informações confidenciais. Os tipos de informações confidenciais listados no tópico [O que os tipos de informações confidenciais no Exchange procurar](what-the-sensitive-information-types-in-exchange-look-for-exchange-online-help.md) estão disponíveis para serem usados nas suas políticas. As condições que você estabelecer dentro de uma política, como quantas vezes algo tem que ser encontrado antes de uma ação ser executada ou exatamente o que a ação é, podem ser personalizadas dentro de suas novas políticas personalizadas para atender aos requisitos de política específicos. Para saber mais sobre como criar políticas DLP, consulte [Criar uma política DLP personalizada](create-a-custom-dlp-policy-exchange-2013-help.md). Para saber mais sobre todo o conjunto de regras de transporte, consulte [Regras de fluxo de emails ou de transporte](mail-flow-rules-transport-rules-in-exchange-2013-exchange-2013-help.md) (Exchange 2013) ou [Regras de fluxo de emails (regras de transporte) no Exchange Online](https://technet.microsoft.com/pt-br/library/jj919238\(v=exchg.150\)) (Exchange Online).

Para permitir que você use facilmente as regras relacionadas a informações confidenciais, a Microsoft forneceu modelos de política que já incluem alguns dos tipos de informações confidenciais. Entretanto, você não pode adicionar condições para todos os tipos de informações confidenciais listados aqui a modelos de política, porque os modelos são projetados para ajudar você a se concentrar nos tipos mais comuns de dados relacionados a dados de conformidade dentro da sua organização. Para mais informações sobre os modelos preparados previamente, consulte [Modelos de política DLP fornecidos no Exchange](dlp-policy-templates-supplied-in-exchange-exchange-2013-help.md). Você pode criar várias políticas DLP para sua organização e habilitar todas, de modo que muitos tipos diferentes de informações sejam examinados. Você também pode criar uma política de DLP não baseada em um modelo existente. Para começar a criar tal política, consulte [Criar uma política DLP personalizada](create-a-custom-dlp-policy-exchange-2013-help.md). Para mais informações sobre os tipos de informações confidenciais, consulte [O que os tipos de informações confidenciais no Exchange procurar](what-the-sensitive-information-types-in-exchange-look-for-exchange-online-help.md).

## Detectar dados confidenciais de formulário com a Impressão Digital de Documento

Com o Exchange 2013 SP1 e a versão mais recente do Exchange Online, você pode usar a [Impressão Digital de Documento](overview-of-document-fingerprinting-in-exchange.md) para criar com facilidade um tipo de informação confidencial baseado em um formulário padrão. Para saber como proteger os dados de formulário, consulte [Proteger os dados de formulário com a impressão digital de documento](protect-form-data-with-document-fingerprinting-exchange-2013-help.md).

## As Dicas de Política notificam os usuários sobre as expectativas em relação a conteúdo confidencial

Você pode usar as mensagens de notificações de Dica de Política para informar os remetentes sobre possíveis problemas de conformidade quando eles escreverem um email. Quando você configurar uma Dica de Política em uma política DLP, a mensagem de notificação aparecerá somente se algo no email do remetente atender às condições descritas na sua política. As Dicas de Política são similares às Dicas de Email que foram apresentadas no Microsoft Exchange 2010. Para saber mais, consulte [Dicas de política](technical-overview-of-policy-tips-in-exchange-online-and-exchange-2013.md).

## Detectar informações confidenciais, juntamente com a classificação tradicional de mensagens

O Exchange 2013 e o Exchange Online apresentam um novo método para ajudar você a gerenciar dados de mensagens e de anexos, quando comparados à classificação tradicional de mensagens. Um fator chave na robustez de uma solução DLP é a habilidade de identificar corretamente conteúdo confidencial ou restrito que pode ser exclusivo da sua organização, necessidades regulamentares, geografia ou outras necessidades de negócios. O Exchange 2013 pode conseguir isso, usando uma nova arquitetura para análise profunda de conteúdo em conjunto com critérios de detecção que você estabelecer através das regras nas suas políticas de DLP. Ajudar a evitar perda de dados no Exchange 2013 passa por configurar o conjunto correto de regras para informações confidenciais, para que elas ofereçam um grau alto de proteção enquanto minimizam as interrupções inadequadas do fluxo de emails com falsos positivos e negativos. Esses tipos de regras, chamados de detecção de informações confidenciais nas informações de DLP, funcionam dentro da estrutura oferecida pelas regras de transporte para habilitar capacidades DLP.

Para saber mais sobre estes recursos, consulte [Integrando regras de informações confidenciais com regras de transporte](integrating-sensitive-information-rules-with-transport-rules-exchange-2013-help.md) Os campos de classificação tradicional de mensagens ainda podem ser aplicados a mensagens no Exchange, e estas podem ser combinadas com a nova detecção de informações confidenciais, seja junto com uma única política DLP ou em execução simultaneamente, de modo que elas sejam avaliadas independentemente dentro do Exchange. Para saber mais sobre classificações de mensagens herdadas do Exchange 2010, consulte [Noções Básicas sobre Classificações de Mensagem](https://go.microsoft.com/fwlink/?linkid=266612) na Biblioteca da TechNet.

## Informações sobre mensagens processadas por DLP

Para que o Exchange 2013 obtenha informações sobre mensagens e detecções de política DLP no seu ambiente, consulte [Exibir relatórios de detecção de política DLP](view-dlp-policy-detection-reports-exchange-2013-help.md) e [Criar relatórios de incidentes para detecções de política DLP](create-incident-reports-for-dlp-policy-detections-exchange-2013-help.md). Os dados relacionados a detecções DLP são altamente integrados à ferramenta de monitoramento de mensagens de relatórios de entrega do Exchange 2013.

Para o Exchange Online, consulte [Exibir relatórios de detecção de política DLP](https://technet.microsoft.com/pt-br/library/dn904484\(v=exchg.150\)) e [Criar relatórios de incidentes para detecção de política DLP](https://technet.microsoft.com/pt-br/library/dn904486\(v=exchg.150\)).

## Pré-requisitos de instalação

Para usar os recursos de DLP, você deve ter o Exchange 2013 ou o Exchange Online configurado em pelo menos uma caixa de correio de remetente. A Prevenção de Perda de Dados é um recurso premium que requer uma Licença de Acesso para Cliente Empresarial (CAL). Para mais informações sobre como começar a usar o Exchange 2013, consulte [Planejamento e implantação](planning-and-deployment-for-exchange-2013-installation-instructions.md). Para mais informações sobre como começar a usar o Exchange Online, consulte [Exchange Online](https://technet.microsoft.com/pt-br/library/jj200580\(v=exchg.150\)).

## Para obter mais informações

Exchange 2013

  - [Conformidade e política de sistema de mensagens](messaging-policy-and-compliance-exchange-2013-help.md)

  - [Procedimentos DLP](dlp-procedures-exchange-2013-help.md)

  - [Exibir relatórios de detecção de política DLP](view-dlp-policy-detection-reports-exchange-2013-help.md)

  - [Impressão Digital de Documento](overview-of-document-fingerprinting-in-exchange.md)

  - [Cmdlets de política e conformidade](https://technet.microsoft.com/pt-br/library/dd298082\(v=exchg.150\))

Exchange Online

  - [Segurança e conformidade para Exchange Online](https://technet.microsoft.com/pt-br/library/jj200706\(v=exchg.150\))

  - [Procedimentos DLP](https://technet.microsoft.com/pt-br/library/jj938003\(v=exchg.150\))

  - [Exibir relatórios de detecção de política DLP](https://technet.microsoft.com/pt-br/library/dn904484\(v=exchg.150\))

  - [Impressão Digital de Documento](overview-of-document-fingerprinting-in-exchange.md)

