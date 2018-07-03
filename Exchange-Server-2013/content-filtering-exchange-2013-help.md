---
title: 'Filtragem de conteúdo: Exchange 2013 Help'
TOCTitle: Filtragem de conteúdo
ms:assetid: d660ffbf-de05-46c2-940b-5200eca94e0a
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Bb124739(v=EXCHG.150)
ms:contentKeyID: 50486754
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Filtragem de conteúdo

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2016-12-09_


> [!TIP]
> Em 1 de novembro de 2016, o Microsoft interrompeu a produção de atualizações de definição de spam para os Filtros SmartScreen, no Exchange e no Outlook. As definições de spam existentes para SmartScreen permanecerão inalteradas, mas a respectiva eficácia provavelmente diminuirá ao longo do tempo. Para saber mais, confira o artigo <A href="https://go.microsoft.com/fwlink/p/?linkid=835894">Substituição do suporte para SmartScreen no Outlook e no Exchange</A>.



O agente de filtro de conteúdo avalia mensagens de email de entrada e avalia a probabilidade de que uma mensagem de entrada é legítima ou spam. Ao contrário de muitas outras tecnologias de filtragem, o agente Filtro de conteúdo usa as características de um exemplo de estatística significativa de mensagens de email. A inclusão de mensagens legítimas neste exemplo reduz a chance de erros. Porque o agente Filtro de conteúdo reconhece as características de spam e mensagens legítimas, sua precisão é aumentada. Atualizações para o agente de filtro de conteúdo estão disponíveis periodicamente por meio [Microsoft Update](https://go.microsoft.com/fwlink/p/?linkid=54836).

**Sumário**

Usando o agente de filtro de conteúdo

Configurando o agente de filtro de conteúdo

## Usando o agente de filtro de conteúdo

O agente de filtro de conteúdo é um dos vários agentes antispam no Exchange. Quando você configura os agentes anti-spam em um servidor Exchange, os agentes de atuam em mensagens de forma cumulativa para reduzir a quantidade de spam que entra na organização. Para obter mais informações sobre como planejar e implantar os agentes antispam, consulte [Proteção contra spam](anti-spam-protection-exchange-2013-help.md).

O agente de filtro de conteúdo atribui uma classificação de nível de confiança de spam (SCL) a cada mensagem. A classificação SCL é um número entre 0 e 9. Uma classificação de SCL maior indica que uma mensagem é mais provável de ser spam.

Você pode configurar o agente de filtro de conteúdo para executar as seguintes ações em mensagens de acordo com sua classificação de SCL:

  - Excluir mensagem

  - Rejeitar mensagem

  - Mensagem em quarentena

Por exemplo, você pode determinar o que devem ser excluídas mensagens que têm uma classificação de SCL de 7 ou superior, mensagens que têm uma classificação de SCL de 6 devem ser rejeitadas e mensagens que têm uma classificação de SCL 5 devem ser colocado em quarentena.

Você pode ajustar o comportamento de limite SCL, atribuindo diferentes classificações de SCL para cada uma das seguintes ações. Para obter mais informações sobre como ajustar o limite de SCL para atender às necessidades da sua organização e sobre os limites de SCL por destinatário, consulte [Limite do Nível de Confiança de Spam](spam-confidence-level-threshold-exchange-2013-help.md).


> [!TIP]
> Mensagens com mais de 11 MB não são verificados pelo filtro de mensagens inteligente. Em vez disso, eles passam pelo filtro de conteúdo sem serem verificadas.



## Permitir frases e frases de bloqueio

Você pode personalizar como o agente de filtro de conteúdo atribui valores SCL, definindo as palavras personalizadas. Palavras personalizadas são palavras individuais ou frases que o agente de filtro de conteúdo usa para aplicar apropriado de processamento de filtro. Configure o aprovado palavras ou frases com frases permitir e não aprovadas palavras ou frases com frases de bloco. Quando o agente de filtro de conteúdo detecta uma frase de permitir pré-configurado em uma mensagem de entrada, o agente Filtro de conteúdo atribui automaticamente um valor SCL 0 à mensagem. Como alternativa, quando o agente de filtro de conteúdo detecta uma frase de bloco configurada em uma mensagem de entrada, o agente Filtro de conteúdo atribui uma classificação de SCL 9.

Você pode inserir palavras ou frases em qualquer combinação de letras maiusculas e minúsculas personalizadas. No entanto, quando o agente do filtro de conteúdo avalia o conteúdo da mensagem, diferencia maiusculas de minúsculas. O número máximo de palavras ou frases que podem ser criados personalizadas é 800.

## Validação de carimbo postal de Email do Outlook

O agente de filtro de conteúdo também inclui a validação da carimbo postal de Email do Microsoft Office Outlook, uma prova computacional que o Outlook se aplica às mensagens enviadas para ajudar a distinguir emails legítimos de lixo eletrônico destinatários sistemas de mensagens. Esse recurso ajuda a reduzir a chance de falsos positivos. No contexto de filtragem de spam, um *falso positivo* existe quando um filtro de spam identifica incorretamente uma mensagem de um remetente legítimo como spam. Quando a validação da carimbo postal de Email do Outlook estiver habilitada, o agente Filtro de conteúdo analisa a mensagem de entrada para um cabeçalho de carimbo postal computacional. A presença de um cabeçalho de carimbo postal computacional de válido, resolvido na mensagem indica que o computador cliente que gerou a mensagem resolvidos o carimbo postal computacional.

Computadores não exigem um tempo de processamento significativo para resolver os carimbos de computacionais individuais. No entanto, os carimbos para muitas mensagens de processamento pode ser proibitivo para um remetente mal-intencionado. Qualquer pessoa que envia milhões de mensagens de spam é improvável de investir o poder de processamento que é necessária para resolver os carimbos computacionais para todos os de spam de saída. Se o email de um remetente contém um carimbo computacional válido, resolvido, é improvável que o remetente é um remetente mal-intencionado. Nesse caso, o agente Filtro de conteúdo reduziria a classificação SCL. Se o recurso de validação da carimbo postal está habilitado e uma mensagem de entrada um não contiver um cabeçalho de carimbo postal computacional ou o cabeçalho da carimbo postal computacional não for válida, o agente Filtro de conteúdo não alteraria a classificação SCL.

## Ignorando o destinatário, o remetente e o domínio do remetente

Em algumas organizações, todos os emails para determinadas aliases devem ser aceito. Este cenário pode introduzir problemas se sua organização estiver em um setor que gerencia volumes significativos de spam.

Por exemplo, uma empresa chamada Woodgrove Bank tem um alias nomeado customerloans@woodgrovebank.com que fornece suporte baseado em email para os clientes externos empréstimo. Os administradores do Exchange configuram o agente de filtro de conteúdo para definir bloco frases que filtram palavras ou frases que costumam ser usados em spam que é enviada pelo órgãos inescrupulosos empréstimo. Para impedir que mensagens potencialmente legítimas sendo rejeitadas, os administradores definir exceções para inserindo uma lista de endereços de destinatário de email SMTP na configuração do agente de filtro de conteúdo de filtragem de conteúdo.

Você também pode especificar remetentes e domínios de remetente que você não quiser que o agente de filtro de conteúdo para bloquear.

## Agregação de lista segura

Em Exchange 2013, o agente Filtro de conteúdo usa as listas de remetentes confiáveis do Outlook, lista de remetentes bloqueados, lista de destinatários seguros e confiáveis contatos do Outlook para otimizar a filtragem de spam. *Agregação de lista segura* é um conjunto de funcionalidades anti-spam que são compartilhadas entre o Outlook e Exchange. Como seu nome sugere, essa funcionalidade coleta dados das listas confiáveis antispam que configuram os usuários do Outlook e disponibiliza esses dados para os agentes antispam no Exchange server. Mensagens de email que os usuários do Outlook recebem dos contatos que esses usuários adicionados à sua lista de destinatários confiáveis do Outlook, lista de remetentes confiáveis ou lista de contatos confiáveis são identificadas pelo agente de filtro de conteúdo como seguros. O agente Filtro de remetente também executa o remetente por destinatário usando a lista de remetentes bloqueados que os usuários configurar a filtragem. Para obter mais informações, consulte [Agregação de Lista Segura](safelist-aggregation-exchange-2013-help.md).

## Configurando o agente de filtro de conteúdo

Você pode configurar o agente de filtro de conteúdo usando o Shell de gerenciamento do Exchange.


> [!IMPORTANT]
> Alterações na configuração feitas para o agente de filtro de conteúdo no Shell de gerenciamento do Exchange são feitas somente no computador local. Se você tiver o agente de filtro de conteúdo executando em vários servidores do Exchange em sua organização, você deve fazer alterações de configuração de filtro de conteúdo em cada computador.



O agente de filtro de conteúdo depende de atualizações para determinar se uma mensagem pode ser entregue com confiança que não é spam. Essas atualizações contêm dados sobre sites de phishing, heurísticas de spam Microsoft SmartScreen e outras atualizações do filtro inteligente de mensagens. Atualizações do filtro de conteúdo geralmente contenham cerca de 6 MB de dados que é útil por longos períodos de tempo que outros dados de atualização anti-spam.

Atualizações de filtro de conteúdo estão disponíveis no [Microsoft Update](https://go.microsoft.com/fwlink/p/?linkid=54836). Os dados de atualização de filtro de conteúdo são atualizado e disponível para download a cada duas semanas.

Para obter mais informações sobre como configurar a filtragem de conteúdo, consulte [Gerenciar filtragem de conteúdo](manage-content-filtering-exchange-2013-help.md).

