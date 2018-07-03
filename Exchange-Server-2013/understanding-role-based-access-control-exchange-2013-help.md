---
title: 'Controle de acesso baseado em função de compreensão: Exchange 2013 Help'
TOCTitle: Controle de acesso baseado em função de compreensão
ms:assetid: fd268867-2ae5-441b-8103-7a7583eb2bbe
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Dd298183(v=EXCHG.150)
ms:contentKeyID: 50487086
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Controle de acesso baseado em função de compreensão

 

_**Aplica-se a:** Exchange Online, Exchange Server 2013_

_**Tópico modificado em:** 2018-01-31_

*Role Based Access Control* (RBAC) é usado no Microsoft Exchange Server 2013 o modelo de permissões. Com o RBAC, você não precisa modificar e gerenciar listas de controle de acesso (ACLs), que foi feito no Exchange Server 2007. ACLs criado vários desafios no Exchange 2007, como modificar ACLs sem causando consequências indesejadas, mantendo modificações de ACL por meio de upgrades e solução de problemas ocorridos devido ao uso de ACLs de forma diferente do padrão.

RBAC permite que você controle, em ambos os amplo número e os usuários finais, o que os administradores e os níveis de granulares podem fazer. RBAC também permite que você alinhar mais de perto as funções que você atribuir usuários e administradores às funções reais que eles manter dentro da sua organização. Em Exchange 2007, o modelo de permissões do servidor é aplicada apenas para os administradores que gerenciados a infraestrutura de Exchange 2007. Em Exchange 2013, RBAC agora controla as tarefas administrativas que podem ser executadas e a extensão ao qual os usuários podem agora administrar seus próprios grupos de distribuição e de caixa de correio.

RBAC tem duas formas básicas de atribuir permissões a usuários em sua organização, dependendo se o usuário é um administrador ou especialista em ou um usuário final: grupos de função de gerenciamento e políticas de atribuição de função de gerenciamento. Cada método associa os usuários com as permissões que precisam para realizar seus trabalhos. Um terceiro, mais avançado método, diretamente a atribuição de função do usuário, também pode ser usado. As seções a seguir neste tópico explicam RBAC e fornecem exemplos de seu uso.


> [!TIP]
> Este tópico concentra-se na funcionalidade avançada de RBAC. Se você quiser gerenciar permissões básicas do Exchange 2013, como usar o Centro de Administração do Exchange (EAC) para adicionar e remover membros de grupos de funções, criar e modificar grupos de funções ou criar e modificar políticas de atribuição de função, consulte <A href="permissions-exchange-2013-help.md">Permissões</A>.



**Sumário**

Grupos de funções de gerenciamento

Políticas de atribuição de função de gerenciamento

Atribuição de função direta do usuário

Resumo e exemplos

Para obter mais informações

## Grupos de funções de gerenciamento

*Grupos de funções de gerenciamento* associar as funções de gerenciamento para um grupo de administradores ou usuários especializados. Os administradores gerenciam uma configuração de organização ou destinatário amplo Exchange. Usuários especializados gerenciam os recursos específicos do Exchange, como conformidade. Ou, eles podem ter limitado capacidades de gerenciamento, como membros da equipe de assistência técnica de Ajuda, mas não são fornecidos amplos direitos administrativos. Grupos de função geralmente associar as funções de gerenciamento administrativo que permitem que administradores e usuários especialistas gerenciar a configuração de sua organização e os destinatários. Por exemplo, se os administradores podem gerenciar destinatários ou usar os recursos de descoberta de caixa de correio é controlado usando os grupos de função.

Adicionando ou removendo aos usuários ou grupos de função é como você com mais frequência atribuir permissões a administradores ou especialista em usuários. Para obter mais informações, consulte [Noções básicas sobre grupos de funções de gerenciamento](understanding-management-role-groups-exchange-2013-help.md).

Grupos de função consistem dos seguintes componentes que definem o que os administradores e usuários especialistas podem fazer:

  - **Grupo de funções de gerenciamento**   O *grupo de funções de gerenciamento* é um grupo de segurança universal especiais (USG) que contenha caixas de correio, usuários, USGs e outros grupos de função que são membros do grupo de função. Isso é onde você adicionar e remove membros, e também é o que as funções de gerenciamento são atribuídas a. A combinação de todas as funções em um grupo de função define tudo o que os usuários adicionados a um grupo de função podem gerenciar na organização Exchange.

  - **Função de gerenciamento**   Uma *função de gerenciamento* é um contêiner para um agrupamento de entradas de função de gerenciamento. Funções são usadas para definir as tarefas específicas que podem ser executadas pelos membros de um grupo de função que possui a função atribuída. Uma *entrada de função de gerenciamento* é um cmdlet, script ou permissão especial que permite que cada tarefa específica em uma função a ser executada. Para obter mais informações, consulte [Noções básicas sobre funções de gerenciamento](understanding-management-roles-exchange-2013-help.md).

  - **Atribuição de função de gerenciamento**   Uma *atribuição de função de gerenciamento* vincula uma função e um grupo de funções. Atribuindo uma função a um grupo de função concede a membros do grupo de função a capacidade de usar os cmdlets e parâmetros definidos na função. Atribuições de função podem usar os escopos de gerenciamento para controlar onde a atribuição pode ser usada. Para obter mais informações, consulte [Noções básicas sobre as atribuições de função de gerenciamento](understanding-management-role-assignments-exchange-2013-help.md).

  - **Escopo de função de gerenciamento**   Um *escopo de função de gerenciamento* é o escopo de influência ou impacto sobre uma atribuição de função. Quando uma função é atribuída com um escopo para um grupo de funções, o escopo de gerenciamento destina-se especificamente quais objetos que a atribuição é permitida para gerenciar. A atribuição e seu escopo, então são concedidas aos membros do grupo de funções e restringem o que esses membros podem gerenciar. Um escopo pode consistir em uma lista de servidores ou bancos de dados, unidades organizacionais (OUs) ou filtros nos objetos de servidor, o banco de dados ou o destinatário. Para obter mais informações, consulte [Noções básicas sobre escopos da função de gerenciamento](understanding-management-role-scopes-exchange-2013-help.md).

Quando você adiciona um usuário a um grupo de função, o usuário recebe todas as funções atribuídas ao grupo de funções. Se os escopos são aplicados a qualquer uma das atribuições da função entre o grupo de função e as funções, os escopos controlam quais configuração do servidor ou destinatários, o usuário pode gerenciar.

Se você quiser alterar a quais funções são atribuídas a grupos de função, você precisará alterar as atribuições da função que são vinculados os grupos de função às funções. A menos que as atribuições incorporadas ao Exchange 2013 não atenderem às suas necessidades, você não precisará alterar essas atribuições. Para obter mais informações, consulte [Noções básicas sobre as atribuições de função de gerenciamento](understanding-management-role-assignments-exchange-2013-help.md).

Para mais informações sobre grupos de funções, consulte [Noções básicas sobre grupos de funções de gerenciamento](understanding-management-role-groups-exchange-2013-help.md).

## Políticas de atribuição de função de gerenciamento

Políticas de atribuição de função de gerenciamento associar funções de gerenciamento do usuário final para os usuários. Políticas de atribuição de função consistem em funções que controlam o que um usuário pode fazer com sua caixa de correio ou grupos de distribuição. Essas funções não permitem o gerenciamento de recursos que não estão diretamente associada ao usuário. Quando você cria uma política de atribuição de função, é possível definir tudo o que um usuário pode fazer com sua caixa de correio. Por exemplo, uma política de atribuição de função poderá permitir que um usuário definir o nome para exibição, configure a caixa postal e configurar as regras de caixa de entrada. Outra política de atribuição de função pode permitir que um usuário alterar o endereço, use a mensagem de texto e configurar grupos de distribuição. Cada usuário com uma caixa de correio Exchange 2013, incluindo administradores, a recebe uma política de atribuição de função por padrão. Você pode decidir qual política de atribuição de função deve ser atribuída por padrão, escolha o que a diretiva de atribuição de função de padrão deve incluir, substituir o padrão para determinadas caixas de correio ou não atribuir políticas de atribuição de função por padrão em todas as.

Atribuindo um usuário a uma diretiva de atribuição é como gerenciar com mais frequência permissões para os usuários gerenciem suas próprias opções de grupo de distribuição e de caixa de correio. Para obter mais informações, consulte [Noções básicas sobre diretivas de atribuição de função de gerenciamento](understanding-management-role-assignment-policies-exchange-2013-help.md).

Políticas de atribuição de função consistem dos seguintes componentes que definem o que os usuários podem fazer com suas próprias caixas de correio. Observe que alguns dos mesmos componentes também se aplicam a grupos de funções. Quando usado com políticas de atribuição de função, esses componentes estão limitados para permitir que os usuários gerenciem apenas sua própria caixa de correio:

  - **Diretiva de atribuição de função de gerenciamento**   A *diretiva de atribuição de função de gerenciamento* é um objeto especial no Exchange 2013. Os usuários são associados a política de atribuição de função quando suas caixas de correio são criadas ou se você alterar a política de atribuição de função em uma caixa de correio. Isso também é o que você atribuir funções de gerenciamento do usuário final para. A combinação de todas as funções em uma política de atribuição de função define tudo o que o usuário pode gerenciar na sua caixa de correio ou grupos de distribuição.

  - **Função de gerenciamento**   Uma *função de gerenciamento* é um contêiner para um agrupamento de entradas de função de gerenciamento. Funções são usadas para definir as tarefas específicas que um usuário pode fazer com sua caixa de correio ou grupos de distribuição. Uma *entrada de função de gerenciamento* é um cmdlet, o script ou a permissão especial que permite que cada tarefa específica em uma função de gerenciamento a ser executada. Você só pode usar as funções de usuário final com políticas de atribuição de função. Para obter mais informações, consulte [Noções básicas sobre funções de gerenciamento](understanding-management-roles-exchange-2013-help.md).

  - **Atribuição de função de gerenciamento**   Uma *atribuição de função de gerenciamento* é o vínculo entre uma função e uma política de atribuição de função. Atribuindo uma função a uma política de atribuição de função concede a capacidade de usar os cmdlets e parâmetros definidos na função. Quando você cria uma atribuição de função entre uma política de atribuição de função e uma função, é possível especificar qualquer escopo. O escopo aplicada pela atribuição é `Self` ou `MyGAL`. Todas as atribuições de função limitam-se a caixa de correio do usuário ou grupos de distribuição. Para obter mais informações, consulte [Noções básicas sobre as atribuições de função de gerenciamento](understanding-management-role-assignments-exchange-2013-help.md).

Se você quiser alterar a quais funções são atribuídas a diretivas de atribuição de função, você precisará alterar as atribuições da função que são vinculados as políticas de atribuição de função às funções. A menos que as atribuições incorporadas ao Exchange 2013 não atenderem às suas necessidades, você não precisará alterar essas atribuições. Para obter mais informações, consulte [Noções básicas sobre as atribuições de função de gerenciamento](understanding-management-role-assignments-exchange-2013-help.md).

Para obter mais informações, consulte [Noções básicas sobre diretivas de atribuição de função de gerenciamento](understanding-management-role-assignment-policies-exchange-2013-help.md).

## Atribuição de função direta do usuário

*Atribuição de função diretas* é um método avançado para atribuição de funções de gerenciamento diretamente a um usuário ou USG sem usar um grupo de funções ou a diretiva de atribuição de função. Atribuições da função diretas podem ser útil quando você precisa fornecer um conjunto granular de permissões para um usuário específico e nenhum outro. No entanto, usar as atribuições da função diretas pode aumentar significativamente a complexidade do seu modelo de permissões. Se um usuário altera trabalhos ou deixa a empresa, você precisará remover as atribuições manualmente e adicioná-los para o novo funcionário. Recomendamos que você use grupos de função para atribuir permissões a administradores e usuários especialistas e diretivas de atribuição de função para atribuir permissões aos usuários.

Para obter mais informações sobre a atribuição de direta do usuário, consulte [Noções básicas sobre as atribuições de função de gerenciamento](understanding-management-role-assignments-exchange-2013-help.md).

## Resumo e exemplos

A figura a seguir mostra os componentes de RBAC e como eles se encaixam:

  - Grupos de função:
    
      - Um ou mais administradores podem ser membros de um grupo de funções. Eles também podem ser membros de mais de um grupo de função.
    
      - O grupo de função é atribuído a um ou mais atribuições de função. Esses link o grupo de função com um ou mais funções administrativas que definem as tarefas que pode ser executadas.
    
      - As atribuições da função podem conter os escopos de gerenciamento que definem onde os usuários do grupo de função podem executar ações. Os escopos determinam onde os usuários do grupo de função podem modificar a configuração.

  - Diretivas de atribuição de função:
    
      - Um ou mais usuários podem ser associados uma política de atribuição de função.
    
      - A política de atribuição de função é atribuída a um ou mais atribuições de função. Essas opções estão vinculadas a política de atribuição de função com um ou mais funções de usuário final. As funções de usuário final definem o que o usuário pode definir na sua caixa de correio.
    
      - As atribuições de função entre as políticas de atribuição de função e funções têm escopos internos que restringem o escopo das atribuições para os grupos de distribuição ou de caixa de correio do usuário.

  - Atribuição de função diretas (avançada):
    
      - Uma atribuição de função pode ser criada diretamente entre um usuário ou USG e um ou mais funções. A função define quais tarefas que o usuário ou USG pode executar.
    
      - As atribuições da função podem conter os escopos de gerenciamento que definem onde o usuário ou USG pode executar ações. Os escopos determinam onde o usuário ou USG pode modificar configuração.

**Visão geral RBAC**

![relacionamentos de componentes de RBAC](images/Dd298183.1dee60cc-1d58-4d36-b34e-639f091e7a56(EXCHG.150).jpg "relacionamentos de componentes de RBAC")

Conforme mostrado na figura anterior, muitos componentes de RBAC estão relacionados entre si. É como cada componente é juntar que define as permissões aplicadas a cada usuário ou administrador. Os exemplos a seguir fornecem algumas contexto adicional sobre como os grupos de função e políticas de atribuição de função são usadas em uma organização.

## O administrador de Jane

Jane é um administrador para a empresa de médio porte, Contoso. Ela é responsável pelo gerenciamento de destinatários da empresa no office seus Vancouver. Quando o modelo de permissões para a Contoso foi criado, Jane foi feita membro do Gerenciamento de Destinatários- grupo de função personalizado Vancouver. O Gerenciamento de Destinatários- Vancouver, grupo de função personalizada é mais parecido com tarefas do seu trabalho, que incluem a criação e a remoção de destinatários, como caixas de correio e contatos, gerenciar a associação de grupo de distribuição e propriedades de caixa de correio e tarefas semelhantes.

Além do Gerenciamento de Destinatários- grupo de função personalizada Vancouver, Jane também precisa de uma política de atribuição de função para gerenciar definições de configuração da própria caixa de correio. Os administradores de organização tem decidido que todos os usuários, exceto para o gerenciamento sênior, recebem as mesmas permissões quando eles gerenciam suas próprias caixas de correio. Eles podem configurar suas mensagens de voz, configurar políticas de retenção e alterar suas informações de endereço. A política de atribuição de função padrão fornecida com o Exchange 2013 agora reflete a esses requisitos.


> [!TIP]
> Você deve ter percebido que porque Jane é um membro do Gerenciamento de Destinatários- grupo de função personalizada Vancouver, que deve dar seus permissões para gerenciar a própria caixa de correio. Isso é verdadeiro; No entanto, o grupo de função não fornece seu todas as permissões necessárias para gerenciar todos os recursos da sua caixa de correio. As permissões necessárias para gerenciar a caixa postal e configurações de política de retenção não estão incluídas no seu grupo de função. Aqueles são fornecidos somente pela diretiva de atribuição de função padrão atribuída a ela.



Para permitir isso, considere o grupo de função, que fornece permissões administrativas de Jane por destinatários na Vancouver:

1.  Um grupo de função personalizado chamado Gerenciamento de Destinatários- Vancouver foi criado. Quando ela foi criada, ocorreu o seguinte:
    
    1.  O grupo de funções foi atribuído a todas as funções de gerenciamento mesmo que também são atribuídas ao grupo de funções internas Gerenciamento de Destinatários. Assim, os usuários adicionados ao Gerenciamento de Destinatários- Vancouver as mesmas permissões que os usuários adicionados ao grupo de funções Gerenciamento de Destinatários de grupo de função personalizada. No entanto, as seguintes etapas limitam onde eles podem usar essas permissões.
    
    2.  O escopo de gerenciamento personalizado Vancouver destinatários tiver sido criado, que corresponde a somente os destinatários que estão localizados em Vancouver. Isso foi feito criando um escopo que filtra na cidade de um usuário ou outras informações exclusivas.
    
    3.  O grupo de função foi criado com o escopo de gerenciamento personalizado de destinatários de Vancouver. Isso significa, enquanto os administradores adicionados ao Gerenciamento de Destinatários- grupo de função personalizado Vancouver ter permissões de gerenciamento de destinatários completa, eles só podem usar essas permissões em relação a destinatários com base em Vancouver.
    
    Para obter mais informações sobre como criar um grupo de função personalizada, consulte [Gerenciar grupos de função](manage-role-groups-exchange-2013-help.md).

2.  Jane é adicionada como um membro do Gerenciamento de Destinatários- grupo de função personalizado Vancouver.
    
    Para obter mais informações sobre como adicionar membros a um grupo de funções, consulte [Gerenciar membros do grupo de função](manage-role-group-members-exchange-2013-help.md).

Para conceder a capacidade de gerenciar próprias configurações de caixa de correio de Jane, uma política de atribuição de função deve ser configurado com as permissões necessárias. A política de atribuição de função padrão é usada para fornecer aos usuários as permissões que eles precisem configurar suas próprias caixas de correio. Todas as funções de usuário final são removidas da diretiva de atribuição de função padrão, exceto para: `MyBaseOptions`, `MyContactInformation`, `MyVoicemail`e `MyRetentionPolicies`. `MyBaseOptions` está incluído porque essa função de gerenciamento fornece a funcionalidade básica do usuário em Outlook Web App, como regras de caixa de entrada, configuração de calendário e outras tarefas.

Nada mais precisa ser feito porque Jane já foi atribuída a política de atribuição de função padrão. Isso significa que as alterações feitas que diretiva de atribuição de função são aplicadas imediatamente à sua caixa de correio e quaisquer outras caixas de correio também atribuídas à diretiva de atribuição de função padrão.

Para obter mais informações sobre como personalizar a política de atribuição de função padrão, consulte [Gerenciar políticas de atribuição de função](manage-role-assignment-policies-exchange-2013-help.md).

## Joe o especialista

Joe funciona para Contoso, da mesma empresa, Jane funciona para. Ele é responsável por realizar descoberta legal, definindo as políticas de retenção e configurando regras de transporte e diário para a organização inteira. Como com Jane, quando o modelo de permissões para a Contoso foi criado, Joe foi adicionado aos grupos de função que coincidem com suas responsabilidades de trabalho. O grupo de funções Gerenciamento de Registros fornece Joe com as permissões para configurar políticas de retenção, registro no diário e transporte de regras. O grupo de funções Gerenciamento de Descobertas ele fornece a capacidade de realizar pesquisas de caixa de correio.

Assim como acontece com Jane, Joe também precisa de permissões para gerenciar sua própria caixa de correio. Ele recebe as mesmas permissões que Jane: ele pode configurar suas políticas de retenção e correio de voz e alterar suas informações de endereço.

Para conceder as permissões para executar suas tarefas de trabalho de Joe, Joe é adicionado aos grupos de função Gerenciamento de Registros e Gerenciamento de Descobertas. Os grupos de função não precisam ser alterado de qualquer maneira, porque eles já oferecem-lo com as permissões que necessárias e os escopos de gerenciamento aplicados aos mesmos abrangem toda a organização.

Para obter mais informações sobre como adicionar um usuário a um grupo de funções, consulte [Gerenciar membros do grupo de função](manage-role-group-members-exchange-2013-help.md).

Caixa de correio do Aníbal também é atribuída a mesma política de atribuição de função de padrão que é aplicada à caixa de correio de Jane. Isso dá a ele todas as permissões que necessárias para gerenciar os recursos da sua caixa de correio que ele tem permissão para gerenciar.

## O vice-presidente de Isabel

Isabel é o vice-presidente de Marketing da Contoso. Isabel, como parte da equipe de liderança sênior da Contoso, recebe mais permissões do que o usuário médio. Isso inclui as permissões que ela é fornecida para gerenciar sua caixa de correio, com uma exceção: Isabel não é permitida para gerenciar próprias políticas de retenção por motivos de conformidade legal. Isabel pode configurar sua caixa postal, alterar suas informações de contato, alterar as informações do seu perfil, criar e gerenciar seus próprio grupos de distribuição e adicionar ou remover por conta própria de grupos de distribuição existentes pertencentes a outras pessoas.

Portanto, Isabel recebe permissões diferentes na própria caixa de correio. A maioria dos usuários da Contoso são atribuídos a diretiva de atribuição de função padrão. No entanto, liderança sênior é atribuída a política de atribuição de função de liderança sênior. O exemplo a seguir é realizado para criar a política de atribuição de função personalizada:

1.  Uma política de atribuição de função personalizada denominada liderança sênior é criada. A política de atribuição de função é atribuída a `MyBaseOptions`, `MyContactInformation`, `MyVoicemail`, `MyProfileInformation`, `MyDistributionGroupMembership`e funções` MyDistributionGroups` . `MyBaseOptions` está incluído porque essa função fornece a funcionalidade básica do usuário em Outlook Web App, como regras de caixa de entrada, configuração de calendário e outras tarefas.

2.  Isabel, em seguida, é atribuída a política de atribuição de função de liderança sênior manualmente.

Caixa de correio de Isabel agora tem as permissões fornecidas pela política de atribuição de função de liderança sênior. Quaisquer alterações feitas a esta política de atribuição de função são aplicadas automaticamente para sua caixa de correio e quaisquer outras caixas de correio também é atribuídas para a mesma política de atribuição de função.

## Para saber mais

[Gerenciar políticas de atribuição de função](manage-role-assignment-policies-exchange-2013-help.md)

[Alterar a política de atribuição de uma caixa de correio](change-the-assignment-policy-on-a-mailbox-exchange-2013-help.md)

