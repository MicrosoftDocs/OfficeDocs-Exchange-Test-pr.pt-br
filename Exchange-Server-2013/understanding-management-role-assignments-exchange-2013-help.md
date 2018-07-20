---
title: 'Noções básicas sobre as atribuições de função de gerenciamento: Exchange 2013 Help'
TOCTitle: Noções básicas sobre as atribuições de função de gerenciamento
ms:assetid: 1dc33dd6-52fb-4852-a5ce-027bc73e1d8f
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Dd335131(v=EXCHG.150)
ms:contentKeyID: 50485141
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Noções básicas sobre as atribuições de função de gerenciamento

 

_**Aplica-se a:** Exchange Online, Exchange Server 2013_

_**Tópico modificado em:** 2012-10-04_

Uma *atribuição de função de gerenciamento*, que é parte do modelo de permissões RBAC (controle de acesso baseado na função) do Microsoft Exchange Server 2013, é o vínculo entre uma função de gerenciamento e um destinatário de função. O parâmetro *destinatário de função* é um grupo de função, uma diretiva de atribuição de função, um usuário ou um USG (grupo de segurança universal). É preciso atribuir uma função a um destinatário de função para que ele tenha efeito. Para mais informações sobre o RBAC, consulte [Controle de acesso baseado em função de compreensão](understanding-role-based-access-control-exchange-2013-help.md).


> [!TIP]
> Este tópico concentra-se na funcionalidade avançada de RBAC. Se você quiser gerenciar permissões básicas do Exchange 2013, como usar o Centro de Administração do Exchange (EAC) para adicionar e remover membros de grupos de funções, criar e modificar grupos de funções ou criar e modificar políticas de atribuição de função, consulte <A href="permissions-exchange-2013-help.md">Permissões</A>.



Este tópico discute o alinhamento de funções a grupos de função e diretivas de atribuição de função e de atribuição direta de função a usuários e USGs. Não são discutidas a atribuição de grupos de função ou diretivas de atribuição de função a usuários. Para obter mais informações sobre os grupos de função e as diretivas de atribuição de função, que são a forma recomendada de atribuir permissões aos usuários, consulte os seguintes tópicos:

  - [Noções básicas sobre grupos de funções de gerenciamento](understanding-management-role-groups-exchange-2013-help.md)

  - [Noções básicas sobre diretivas de atribuição de função de gerenciamento](understanding-management-role-assignment-policies-exchange-2013-help.md)

Você pode criar os seguintes tipos de atribuições de função, que são explicados detalhadamente mais adiante neste tópico:

  - Regular and delegating role assignments

  - Exclusive role assignments

## Gerenciar atribuições de função

Ao alterar atribuições de função, é provável que suas alterações sejam entre grupos de função e diretivas de atribuição de função. Ao adicionar, remover ou modificar atribuições de função desses destinatários de função, é possível controlar quais permissões são dadas aos seus administradores e usuários, o que efetivamente ativa e desativa o gerenciamento de recursos relacionados.

Também convém atribuir funções diretamente a usuários ou USGs. Essa é uma tarefa mais avançada que permite definir em nível detalhado quais permissões seus usuários receberão. Embora ofereça mais flexibilidade, isso também aumenta a complexidade de seu modelo de permissões. Por exemplo, se o usuário mudar de emprego, pode ser preciso reatribuir manualmente as funções atribuídas a esse usuário para outro usuário. É por isso que recomendamos que você use grupos de função e diretivas de atribuição de função para dar permissões aos seus usuários. Você pode atribuir as funções a um grupo de função ou diretiva de atribuição de função, para então adicionar ou remover membros do grupo de função, ou alterar as diretivas de atribuição de função conforme a necessidade.

Você pode adicionar, remover e habilitar atribuições de função, modificar o escopo de gerenciamento em uma atribuição de função existente e mover atribuições de função para outros destinatários de função. O processo de atribuição de funções a grupos de função, diretivas de atribuição de função, usuários e USGs é praticamente o mesmo para cada destinatário de função. Os itens a seguir são as únicas exceções:

  - Diretivas de atribuição de função podem ser atribuídas apenas às funções de gerenciamento de usuário final.

  - Diretivas de atribuição de função não podem ser atribuídas às atribuições de função de delegação.

  - Não é possível especificar um escopo de gerenciamento ao criar uma atribuição de função a diretivas de atribuição de função.

Para obter mais informações sobre o gerenciamento de atribuições de função, consulte os seguintes tópicos:

  - Grupos de função:
    
      - [Gerenciar grupos de função](manage-role-groups-exchange-2013-help.md)

  - Diretivas de atribuição de função:
    
      - [Gerenciar políticas de atribuição de função](manage-role-assignment-policies-exchange-2013-help.md)
    
      - [Alterar uma atribuição de função](change-a-role-assignment-exchange-2013-help.md)

  - Usuários e USGs:
    
      - [Adicionar uma função a um usuário ou USG](add-a-role-to-a-user-or-usg-exchange-2013-help.md)
    
      - [Remover uma função de um usuário ou USG](remove-a-role-from-a-user-or-usg-exchange-2013-help.md)
    
      - [Alterar uma atribuição de função](change-a-role-assignment-exchange-2013-help.md)
    
      - [Alterar um escopo de função](change-a-role-scope-exchange-2013-help.md)
    
      - [Atribuições de função de representante](delegate-role-assignments-exchange-2013-help.md)

## Atribuições de função comuns e de delegação

As atribuições de função regulares permitem que o destinatário de função acesse as entradas de função de gerenciamento disponibilizadas pela função de gerenciamento associada. Se várias funções de gerenciamento forem atribuídas a um destinatário de função, as entradas de função de gerenciamento de cada função de gerenciamento são agregadas e aplicadas. Isso significa que se as funções de Regras de Transporte e Registro em Diário forem atribuídas a um destinatário de função, as funções são combinadas e as entradas de função de gerenciamento associadas são concedidas ao destinatário de função. Se o destinatário de função for um grupo de função ou uma diretiva de atribuição de função, as permissões fornecidas pelas funções são concedidas aos usuários atribuídos ao grupo de função ou diretiva de atribuição de função. Para obter mais informações sobre as funções de gerenciamento e entradas de função, consulte [Noções básicas sobre funções de gerenciamento](understanding-management-roles-exchange-2013-help.md).

As atribuições de função de delegação não oferecem acesso a recursos de gerenciamento. As atribuições de função de delegação dão a um destinatário de função a capacidade de atribuir a função especificada a outros destinatários de função. Se o destinatário de função for um grupo de função, qualquer membro do grupo de função pode atribuir a função a outro destinatário de função. Por padrão, apenas o grupo de função de Gerenciamento da Organização tem capacidade de atribuir funções a outros destinatários de função. Apenas o usuário que instalou o Exchange 2013 é membro do grupo de função Gerenciamento da Organização por padrão. No entanto, é possível adicionar outros usuários a esse grupo de função conforme a necessidade, ou criar outros grupos de função e atribuir atribuições de função de delegação a esses grupos.


> [!TIP]
> As atribuições de função de delegação dão aos destinatários de função a capacidade de delegar funções de gerenciamento a outros destinatários de função. Isso não permite aos usuários delegar grupos de função. Para obter mais informações sobre a delegação de grupos de função, consulte <A href="understanding-management-role-groups-exchange-2013-help.md">Noções básicas sobre grupos de funções de gerenciamento</A>.



Se quiser que um usuário seja capaz de gerenciar um recurso e atribuir a função que dá permissão ao uso do recurso a outros usuários, atribua o seguinte:

1.  Uma atribuição de função regular para cada função de gerenciamento que conceda acesso aos recursos que precisam ser gerenciados.

2.  Uma atribuição de função de delegação para cada função de gerenciamento cuja atribuição você permitir a outros destinatários de função.

As atribuições de função de delegação e regulares para um destinatário de função não precisam ser idênticas. Por exemplo, um usuário é membro de um grupo de função atribuído à função de Regras de Transporte usando uma atribuição de função regular. Isso permite que o usuário gerencie o recurso de Regras de Transporte. Entretanto, não é atribuída ao usuário uma atribuição de função de delegação para a função de Regras de Transporte, de modo que o usuário não pode atribuir essa função a outros usuários. Entretanto, o usuário é membro de um grupo de função atribuído à função de gerenciamento de Registro em Diário usando uma atribuição de função de delegação. O grupo de função do qual o usuário é membro não possui uma atribuição de função regular para a função de Registro em Diário, mas como ela possui uma atribuição de função de delegação, o usuário pode atribuir a função a outros destinatários de função.

## Escopos de gerenciamento

Ao criar uma atribuição de função de gerenciamento regular ou de representação, você terá a opção de criar a atribuição com um escopo de gerenciamento para limitar os objetos que podem ser manipulados pelo usuário. É possível criar escopos de destinatário ou escopos de configuração. Os escopos de destinatário permitem controlar quem pode manipular caixas de correio, usuários de email, grupos de distribuição e assim por diante. Os escopos de configuração permitem controlar quem pode manipular servidores e bancos de dados.

Os escopos de destinatário e configuração permitem segmentar o gerenciamento do servidor, do banco de dados ou dos objetos de destinatário em sua organização. Por exemplo, um escopo de destinatário pode ser adicionado a uma atribuição de função para que administradores em Vancouver só possam gerenciar destinatários no mesmo escritório. Um escopo de configuração de servidor pode ser adicionado a uma atribuição de função diferente, de modo que os administradores em Sydney só possam gerenciar servidores em seu site do Active Directory.

Com os escopos, é possível atribuir permissões a grupos de usuários e direcionar onde esses administradores poderão realizar a administração. Isso permite a você criar um modelo de permissões mapeado para suas fronteiras geográficas ou organizacionais.

Você pode criar uma atribuição com um escopo predefinido ou adicionar um escopo personalizado à atribuição. Os escopos predefinidos, como limitar um usuário apenas à sua caixa de correio ou aos seus grupos de distribuição, podem ser aplicados usando as opções disponíveis na própria atribuição. Outra opção é criar um escopo de configuração ou destinatário personalizado e adicionar esse escopo à atribuição de função. Um escopo personalizado oferece mais detalhamento sobre os objetos a serem incluídos no escopo.

Não é possível especificar escopos predefinidos e personalizados na mesma atribuição. Você também não pode misturar escopos exclusivos e regulares na mesma atribuição.

Cada atribuição de função pode ter apenas um escopo de destinatário e um escopo de configuração. Para aplicar mais de um escopo de destinatário ou de configuração a um destinatário de função para a mesma função de gerenciamento, múltiplas atribuições de função terão que ser criadas.

Sem um escopo predefinido ou personalizado, as atribuições de função ficam limitadas aos escopos de destinatário e configuração definidos na própria função. Estes escopos são chamados de escopos implícitos. Qualquer atribuição de função que não tenha um escopo predefinido ou personalizado herda os escopos implícitos da função à qual está associada.

Para obter mais informações sobre escopos, consulte [Noções básicas sobre escopos da função de gerenciamento](understanding-management-role-scopes-exchange-2013-help.md).

## Atribuições de função exclusivas

As atribuições de função exclusivas são criadas quando você associa um escopo exclusivo a uma atribuição de função. Os escopos exclusivos funcionam como escopos regulares e permitem que os destinatários de função gerenciem destinatários que correspondam ao escopo exclusivo. Entretanto, ao contrário dos escopos regulares, todos os outros destinatários de função são proibidos de gerenciar o destinatário, mesmo que esse destinatário corresponda aos escopos aplicados em suas atribuições de função. Isso pode ser útil quando você quiser limitar a uns poucos administradores o poder de gerenciar um destinatário. Só esses administradores específicos podem gerenciar o destinatário, e todos os outros administradores têm acesso negado.

Por exemplo, considere a situação a seguir:

  - John é um executivo da Contoso. A caixa de correio dele corresponde a um escopo exclusivo chamado Usuários VIP, associado à atribuição exclusiva Restrito a VIPs.

  - A caixa de correio de John também está incluída em um escopo regular chamado Usuários de Redmond, que está associada à atribuição regular Administração de Redmond.

  - Bill é um administrador associado à atribuição exclusiva Restrito a VIPs.

  - Chris é um administrador associado à atribuição regular Administração de Redmont.

Como a caixa de correio de John corresponde ao escopo exclusivo Usuários VIP, apenas Bill pode gerenciar sua caixa de correio. Ainda que a caixa de correio de John corresponda ao escopo regular Usuários de Redmond, Chris não está associado à atribuição exclusiva Restrito a VIPs. Portanto, o Exchange nega a Chris a capacidade de gerenciar a caixa de correio de John. Para que Chris gerencie a caixa de correio de John, Chris precisa ter uma atribuição exclusiva com um escopo exclusivo que corresponda à caixa de correio de John.

Para mais informações, consulte [Noções básicas sobre escopos exclusivos](understanding-exclusive-scopes-exchange-2013-help.md).

