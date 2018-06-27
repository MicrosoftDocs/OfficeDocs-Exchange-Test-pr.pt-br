---
title: 'Gerenciamento de carga de trabalho do Exchange: Exchange 2013 Help'
TOCTitle: Gerenciamento de carga de trabalho do Exchange
ms:assetid: 276740c4-bdb7-49f1-9470-ae6f2bfd65aa
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/JJ150503(v=EXCHG.150)
ms:contentKeyID: 50485181
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Gerenciamento de carga de trabalho do Exchange

 

_**Aplica-se a:**Exchange Online, Exchange Server 2013_

_**Tópico modificado em:**2014-11-16_

Uma carga de trabalho do Exchange é um recurso, protocolo ou serviço que foi explicitamente definido para as finalidades de gerenciamento de recursos do sistema do Exchange. Cada carga de trabalho do Exchange consome recursos do sistema, como CPU, operações de banco de dados de caixa de correio ou solicitações do Active Directory para executar solicitações de usuário ou trabalho em segundo plano. Os exemplos de cargas de trabalho do Exchange incluem Outlook Web App, Exchange ActiveSync, migração de caixa de correio e assistentes de caixa de correio.

Você pode gerenciar cargas de trabalho do Exchange por meio do controle como os recursos são consumidos por usuários individuais (às vezes chamados de usuário limitação no Exchange 2010). Controlar como os recursos de sistema do Exchange são consumidos por usuários individuais que era possível nos Exchange Server 2010 e esse recurso foi expandido para Exchange Server 2013.


> [!TIP]
> Gerenciando cargas de trabalho por meio do monitoramento de integridade de recursos do sistema nos servidores do Exchange em sua organização deve ser feito apenas sob a orientação do suporte e atendimento ao cliente Microsoft.



## Gerenciando cargas de trabalho por meio do controle de como os recursos são consumidos por usuários individuais

A funcionalidade de limitação foi aprimorada no Exchange 2013. A funcionalidade aprimorada ajuda a garantir que o consumo de recursos excessivo por usuários individuais não afete negativamente o desempenho do servidor ou a experiência do usuário.

Por padrão, o usuário limitação no Exchange 2013 permite aos usuários aumentar o consumo de recursos por curtos períodos sem enfrentar qualquer redução na largura de banda. Além disso, o bloqueio de usuários que usam uma grande quantidade de recursos do completo será esporádica, ou nunca ocorrer. Em vez de bloqueio de um usuário para executar operações completamente, limitação ocorre e processos estão atrasados por curtos períodos de tempo (imagine-las como "microdelays"), que ocorrem antes que causem um impacto significativo em um servidor.

**Destaques do recurso**

Aqui são apresentados alguns destaques da forma como o Exchange controla como os recursos são consumidos por usuários individuais no Exchange 2013:

  - **Permissões de intermitência**   As permissões de intermitência permitem que os usuários passem curtos períodos de consumo maior de recursos sem enfrentar nenhuma limitação.

  - **Taxa de recarga**   A taxa de recarga gerencia o consumo de recursos de seus usuários com a utilização de um sistema de orçamento de recursos. Você pode definir a taxa em que os orçamentos de recursos de seus usuários são recarregados. Por exemplo, um valor de 600.000 (em milissegundos) implica na recarga dos orçamentos desses usuários em uma taxa de dez minutos de uso por hora.

  - **Formação de tráfego**  Quando a utilização de recursos de um usuário atinge o limite configurado em um intervalo de tempo, esse usuário é adiado por períodos muito curtos bem antes de causar um impacto significativo em um servidor. Os usuários geralmente não percebem esses "microadiamentos." Esse processo permite que o Exchange 2013 forme o tráfego eficientemente sem impedir que os usuários sejam produtivos. A formação de tráfego causa menos impacto para seus usuários do que o bloqueio antecipado e reduz bastante a chance de ocorrer um bloqueio.

  - **Uso máximo**   Em raras circunstâncias, um usuário pode consumir uma quantidade muito alta de recursos em um curto intervalo de tempo. Como precaução, o usuário que atingir um limite de uso máximo pode ser impedido temporariamente de utilizar os recursos. Os usuários temporariamente impedidos de usar os recursos são liberados assim que seus orçamentos de uso forem recarregados.

Para obter uma lista de cmdlets que você pode usar para controlar como os recursos são consumidos por usuários individuais, consulte "Cmdlets para controlar como os recursos são usados por usuários individuais" mais adiante neste tópico.

**Considerações sobre a implantação e a funcionalidade de limitação no Exchange 2013**

Se você realizar uma instalação limpa do Exchange 2013 ou instalar o Exchange 2013 em um ambiente de coexistência que inclua computadores com Exchange 2010, todos os usuários com caixas de correio em computadores com Exchange 2013 serão limitados pela nova funcionalidade de limitação do Exchange 2013. Entretanto, as caixas de correio do Exchange 2010 permanecerão limitadas pela funcionalidade de limitação do Exchange 2010 quando acessarem suas caixas de correio por meio dos servidores de Acesso para Cliente do Exchange 2010.

Quando o Exchange 2013 está instalado em um ambiente de coexistência, o processo de instalação do Exchange 2013 pode tentar encaminhar algumas das configurações de limitação que você definiu na sua configuração do Exchange 2010. Contudo, a funcionalidade de limitação do Exchange 2013 é tão diferente que o impacto de quaisquer configurações de limitação existentes geralmente não afetará o modo como a limitação funciona no Exchange 2013.

**Gerenciando políticas de limitação usando escopos**

Similar ao Exchange 2010, há uma política de limitação padrão única no Exchange 2013. No Exchange 2013, a política de limitação padrão recebe o nome **GlobalThrottlingPolicy**. Essa política tem o escopo **Global**. Os outros escopos de limitação de usuário disponíveis são **Organization** e **Regular**. Devido à introdução da atribuição de escopo para as políticas de limitação de usuário do Exchange 2013, você gerencia as políticas de limitação de modo diferente em relação ao Exchange 2010. A **GlobalThrottlingPolicy** define as configurações de limitação padrão de linha de base para todos os usuários novos e existentes de sua organização, a menos que você tenha personalizado as políticas de limitação para a sua organização. Em vários cenários típicos de implantação do Exchange, a **GlobalThrottlingPolicy** será adequada para gerenciar seus usuários.

É altamente recomendável não personalizar as configurações de limitação por meio da modificação de **GlobalThrottlingPolicy**. Em vez disso, você deve criar políticas de limitação adicionais. A criação de políticas de limitação adicionais o ajudará a gerenciar melhor suas cargas de trabalho. Ela também impedirá que quaisquer modificações nas configurações da política de limitação sejam substituídas por atualizações futuras do Exchange 2013.

Para personalizar as configurações de limitação aplicáveis a todos os usuários de sua organização, crie uma nova política de limitação com a atribuição de escopo **Organization**. Nas novas políticas do escopo Organização, você deverá apenas definir as configurações de limitação diferentes das encontradas em **GlobalThrottlingPolicy**. Para personalizar as configurações de limitação aplicáveis somente a usuários específicos de sua organização, crie uma nova política de limitação com a atribuição de escopo **Regular**. Nas novas políticas do escopo Regular, você deverá apenas definir as configurações de limitação diferentes das encontradas em **GlobalThrottlingPolicy** e em todas as outras políticas de organização. Isso o ajudará a herdar o restante das configurações de política de **GlobalThrottlingPolicy** e permitirá que você se beneficie com todas as atualizações efetuadas nas políticas de limitação adicionadas em atualizações futuras do Exchange.

## Gerenciando configurações de limitação de carga de trabalho

Gerencie as configurações de limitação de carga de trabalho do Exchange usando o Shell de Gerenciamento do Exchange.

**Cmdlets para controlar como os recursos são usados por usuários individuais**

Gerencie as configurações de limitação com os seguintes cmdlets, que foram introduzidos no Exchange 2010:

Gerenciar políticas de limitação

  - [Get-ThrottlingPolicy](https://technet.microsoft.com/pt-br/library/dd351264\(v=exchg.150\))

  - [New-ThrottlingPolicy](https://technet.microsoft.com/pt-br/library/dd351045\(v=exchg.150\))

  - [Remove-ThrottlingPolicy](https://technet.microsoft.com/pt-br/library/dd351178\(v=exchg.150\))

  - [Set-ThrottlingPolicy](https://technet.microsoft.com/pt-br/library/dd298094\(v=exchg.150\))

Atribuir políticas de limitação

  - [Get ThrottlingPolicyAssociation](https://technet.microsoft.com/pt-br/library/ff459241\(v=exchg.150\))

  - [Set-ThrottlingPolicyAssociation](https://technet.microsoft.com/pt-br/library/ff459231\(v=exchg.150\))


> [!TIP]
> Os cmdlets de gerenciamento de carga de trabalho de sistema <STRONG>*-ResourcePolicy</STRONG>, <STRONG>*-WorkloadManagementPolicy</STRONG> e <STRONG>*-WorkloadPolicy</STRONG> foram preteridos. Configurações de gerenciamento de carga de trabalho do sistema devem ser personalizadas apenas sob a orientação do suporte e atendimento ao cliente Microsoft.


