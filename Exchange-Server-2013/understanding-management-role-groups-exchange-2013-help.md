---
title: 'Noções básicas sobre grupos de funções de gerenciamento: Exchange 2013 Help'
TOCTitle: Noções básicas sobre grupos de funções de gerenciamento
ms:assetid: 2a92e06c-523e-4fd4-a937-152562b7741d
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Dd638105(v=EXCHG.150)
ms:contentKeyID: 50485222
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Noções básicas sobre grupos de funções de gerenciamento

 

_**Aplica-se a:** Exchange Online, Exchange Server 2013_

_**Tópico modificado em:** 2015-03-09_

Um *grupo de funções de gerenciamento* é um grupo de segurança universal (USG) usado no modelo de permissões do Controle de Acesso Baseado em Função (RBAC) no Microsoft Exchange Server 2013. Um grupo de gerenciamento de funções simplifica a atribuição de funções de gerenciamento para um grupo de usuários. Todos os membros de um grupo de função recebem o mesmo conjunto de funções. Aos grupos de função são atribuídas funções de administrador e especialista que definem as principais tarefas administrativas do Exchange 2013, como gerenciamento da organização, gerenciamento de destinatário e outras tarefas. Os grupos de função permitem atribuir mais facilmente um conjunto mais amplo de permissões a um grupo de administradores ou usuários especialistas.


> [!TIP]  
> Este tópico concentra-se na funcionalidade avançada de RBAC. Se você quiser gerenciar permissões básicas do Exchange 2013, como usar o Centro de Administração do Exchange (EAC) para adicionar e remover membros de grupos de funções, criar e modificar grupos de funções ou criar e modificar políticas de atribuição de função, consulte <A href="permissions-exchange-2013-help.md">Permissões</A>.



**Sumário**

Role group layers

Role group management

Built-in role groups

Linked role groups

Role group delegation

Role group membership

Role group creation workflow


> [!TIP]  
> Se quiser atribuir permissões a usuários para que gerenciem suas próprias caixas de correio ou grupos de distribuição, consulte <A href="understanding-management-role-assignment-policies-exchange-2013-help.md">Noções básicas sobre diretivas de atribuição de função de gerenciamento</A>.



## Camadas de grupo de funções

As camadas que constituem o modelo de grupo de função são:

  - **Membro do grupo de funções**   Um *membro do grupo de funções* é uma caixa de correio, grupo de segurança universal (USG) ou outro grupo de funções que pode ser adicionado como um membro de um grupo de funções. Quando uma caixa de correio, USG ou outro grupo de funções é adicionado como membro de um grupo de funções, as atribuições que foram feitas entre funções de gerenciamento e um grupo de funções são aplicadas ao novo membro. Isso concede, ao novo membro, todas as permissões oferecidas pelas funções de gerenciamento.

  - **Grupo de funções de gerenciamento**   O *grupo de funções de gerenciamento* é um USG especial que contém caixas de correio, USGs e outros grupos de funções que são membros do grupo de funções. É nele que os adiciona e remove membros, e as funções de gerenciamento também são atribuídas a ele. A combinação de todas as funções em um grupo de funções define tudo o que os membros adicionados a um grupo de funções podem gerenciar na organização do Exchange.

  - **Atribuição de função de gerenciamento** Uma *atribuição de função de gerenciamento* vincula uma função de gerenciamento e um grupo de função. Atribuir uma função de gerenciamento a um grupo de função concede aos membros do grupo de função a capacidade de usar cmdlets e parâmetros definidos na função de gerenciamento. As atribuições de função podem usar escopos de gerenciamento para controlar onde a atribuição pode ser usada. Para obter mais informações, consulte [Noções básicas sobre as atribuições de função de gerenciamento](understanding-management-role-assignments-exchange-2013-help.md).

  - **Escopo de função de gerenciamento** Um *escopo de função de gerenciamento* é o escopo de influência ou impacto em uma atribuição de função. Quando uma função é atribuída com um escopo a um grupo de função, o escopo de gerenciamento é direcionado especificamente aos objetos que essa atribuição tem permissão para gerenciar. A atribuição e seu escopo são dadas aos membros do grupo de função, que restringe o que esses membros podem gerenciar. Um escopo pode ser constituído de listas de servidores ou bancos de dados, unidades organizacionais ou filtros em objetos de banco de dados, servidor ou destinatário. Para obter mais informações, consulte [Noções básicas sobre escopos da função de gerenciamento](understanding-management-role-scopes-exchange-2013-help.md).

  - **Função de gerenciamento**   Uma *função de gerenciamento* é um contêiner para um agrupamento de entradas de função de gerenciamento. As funções são usadas para definir as tarefas específicas que podem ser realizadas pelos membros de um grupo de função com a função atribuída. Para obter mais informações, consulte [Noções básicas sobre funções de gerenciamento](understanding-management-roles-exchange-2013-help.md).

  - **Entradas de função de gerenciamento** As *entradas de função de gerenciamento* são entradas individuais em uma função de gerenciamento que oferecem acesso a cmdlets, scripts e outras permissões especiais que dão acesso à realização de uma tarefa específica. Na maioria das vezes, as entradas de função consistem em um único cmdlet ou script e nos parâmetros que podem ser acessados pela função de gerenciamento, e, assim, pelo grupo de funções ao qual a função é atribuída.

A imagem a seguir mostra cada camada de grupo de função na lista anterior e como cada camada se relaciona à outra.

**Camadas de grupos de função de gerenciamento**

![Camadas de grupos de função de gerenciamento](images/Dd638105.a98c237c-7bdb-434b-8c98-22509e46cccf(EXCHG.150).gif "Camadas de grupos de função de gerenciamento")

Para mais informações sobre o RBAC, consulte [Controle de acesso baseado em função de compreensão](understanding-role-based-access-control-exchange-2013-help.md).

Voltar ao início

## Gerenciamento de grupo de funções

Quando você cria um grupo de função, cria o USG que detém os membros do grupo de função e cria as atribuições entre o grupo de função e as funções de gerenciamento que você especificar. Uma opção é especificar um escopo de gerenciamento para aplicar as atribuições de função, e você pode adicionar quaisquer caixas de correio que você quiser tornar membros do novo grupo de função.

Após criar um grupo de função, cada camada se torna um objeto independente. O grupo de função continua sendo o ponto central no qual todas as camadas se unem, mas cada camada é gerenciada individualmente. Por exemplo, para modificar o escopo de gerenciamento que você aplicou ao grupo de função quando ele foi criado, é preciso alterar o escopo em cada atribuição de função individual após a criação do grupo de função. O gerenciamento do modelo de grupo de função é realizado usando os cmdlets que gerenciam as camadas individuais do modelo de grupo de função.

A tabela a seguir lista a camada de grupo de função e os tópicos procedurais que podem ser usados no gerenciamento de cada camada.

### Tópicos de gerenciamento de grupo de função

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Camada de modelo de grupo de função</th>
<th>Tópico de gerenciamento</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Membro do grupo de funções</p></td>
<td><p><a href="manage-role-group-members-exchange-2013-help.md">Gerenciar membros do grupo de função</a></p>
<p></p></td>
</tr>
<tr class="even">
<td><p>Grupo de função</p></td>
<td><p><a href="manage-role-groups-exchange-2013-help.md">Gerenciar grupos de função</a></p>
<p></p></td>
</tr>
<tr class="odd">
<td><p>Funções de gerenciamento e atribuições</p></td>
<td><p><a href="manage-role-groups-exchange-2013-help.md">Gerenciar grupos de função</a></p></td>
</tr>
<tr class="even">
<td><p>Entradas de função de gerenciamento</p></td>
<td><p><a href="add-a-role-entry-to-a-role-exchange-2013-help.md">Adicionar uma entrada de função a uma função</a></p>
<p><a href="change-a-role-entry-exchange-2013-help.md">Alterar uma entrada de função</a></p>
<p><a href="remove-a-role-entry-from-a-role-exchange-2013-help.md">Remover uma entrada de função de uma função</a></p>

> [!TIP]  
> Alterar as entradas de função de gerenciamento nas funções de gerenciamento em um grupo de função é uma tarefa avançada e na maioria dos casos não é exigida. Você pode, em vez disso, ser capaz de usar uma função de gerenciamento pré-existente adequada às suas necessidades. Para obter mais informações, consulte <A href="built-in-role-groups-exchange-2013-help.md">Grupos de funções internos</A>.


</td>
</tr>
</tbody>
</table>


Voltar ao início

## Grupos de função internos

Grupos de funções internas são funções fornecidas com o Exchange 2013. Eles oferecem um conjunto de grupos de função que você pode usar para proporcionar níveis variáveis de permissões administrativas a grupos de usuários. Você pode adicionar ou remover usuários de qualquer grupo de função interno. Você também pode adicionar ou remover atribuições de função da maioria dos grupos de função. As únicas exceções são as seguintes:

  - Não é possível remover nenhuma atribuição de função de delegação a partir do grupo de função Gerenciamento da Organização.

  - Não é possível remover a função de Gerenciamento de Função a partir do grupo de função Gerenciamento da Organização.

A tabela a seguir lista todos os grupos de função internos incluídos com o Exchange 2013. Para obter mais informações sobre grupos de função internos, consulte [Grupos de funções internos](built-in-role-groups-exchange-2013-help.md).

### Grupos de funções internos

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Grupo de funções</th>
<th>Descrição</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="organization-management-exchange-2013-help.md">Gerenciamento da Organização</a></p></td>
<td><p>Os administradores que sejam membros do grupo de função Gerenciamento da Organização têm acesso administrativo à organização inteira do Microsoft Exchange 2013 e podem realizar quase qualquer tarefa em relação a qualquer objeto do Exchange 2013, com algumas exceções. Por padrão, os membros desse grupo de função não podem realizar pesquisas em caixas de correio nem gerenciar funções de gerenciamento de nível superior sem escopo.</p></td>
</tr>
<tr class="even">
<td><p><a href="view-only-organization-management-exchange-2013-help.md">Gerenciamento da organização somente exibição</a></p></td>
<td><p>Administradores que sejam membros do grupo de função Gerenciamento de Organizações Somente Exibição podem exibir as propriedades de qualquer objeto da organização do Exchange.</p></td>
</tr>
<tr class="odd">
<td><p><a href="recipient-management-exchange-2013-help.md">Gerenciamento de Destinatários</a></p></td>
<td><p>Administradores que sejam membros do grupo de função Gerenciamento de Destinatários têm acesso administrativo para criar ou modificar destinatários do Exchange 2013 dentro da organização do Exchange 2013.</p></td>
</tr>
<tr class="even">
<td><p><a href="um-management-exchange-2013-help.md">Gerenciamento de UM</a></p></td>
<td><p>Os administradores que são membros do grupo de função Gerenciamento de UM podem gerenciar recursos na organização do Exchange como a configuração do servidor de UM (Unificação de Mensagens), propriedades de UM em caixas de correio, prompts de UM e configuração do atendedor automático de UM.</p></td>
</tr>
<tr class="odd">
<td><p><a href="discovery-management-exchange-2013-help.md">Gerenciamento de Descobertas</a></p></td>
<td><p>Administradores ou usuários que forem membros do grupo de função Gerenciamento de Descobertas podem realizar pesquisas de caixas de correio na organização do Exchange em busca de dados que atendam a critérios específicos e também podem configurar retenções de litígios em caixas de correios.</p></td>
</tr>
<tr class="even">
<td><p><a href="records-management-exchange-2013-help.md">Gerenciamento de Registros</a></p></td>
<td><p>Usuários que sejam membros do grupo de função Gerenciamento de Registros podem configurar recursos de conformidade, como marcas de diretivas de retenção, classificações de mensagens, regras de transporte e mais.</p></td>
</tr>
<tr class="odd">
<td><p><a href="server-management-exchange-2013-help.md">Gerenciamento de Servidor</a></p></td>
<td><p>Os administradores que forem membros desse grupo de funções podem definir configurações específicas de servidor para recursos de transporte, acesso para cliente e caixa de correio, como cópias de bancos de dados, certificados, filas de transporte e conectores de Envio, diretórios virtuais e protocolos de acesso para cliente.</p></td>
</tr>
<tr class="even">
<td><p><a href="help-desk-exchange-2013-help.md">Suporte Técnico</a></p></td>
<td><p>Usuários que sejam membros do grupo de função Suporte Técnico podem realizar gerenciamento de destinatário limitado nos destinatários do Exchange 2013.</p></td>
</tr>
<tr class="odd">
<td><p><a href="hygiene-management-exchange-2013-help.md">Gerenciamento de Higienização</a></p></td>
<td><p>Os administradores que forem membros do grupo de função Gerenciamento de Higienização podem configurar os recursos de antimalware e antispam do Exchange 2013. Programas que terceiros que se integram ao Exchange 2013 podem adicionar contas de serviço a este grupo de função, para conceder, a essas programas, acesso aos cmdlets necessários para recuperar e configurar o Exchange.</p></td>
</tr>
<tr class="even">
<td><p><a href="compliance-management-exchange-2013-help.md">Gerenciamento de Conformidade</a></p></td>
<td><p>Usuários que sejam membros do grupo de funções Gerenciamento de Conformidade podem configurar e gerenciar as configurações de conformidade do Exchange, de acordo com suas políticas.</p></td>
</tr>
<tr class="odd">
<td><p><a href="public-folder-management-exchange-2013-help.md">Gerenciamento de Pasta Pública</a></p></td>
<td><p>Administradores que são membros do grupo de funções Gerenciamento de Pasta Pública podem gerenciar pastas públicas em servidores com o Exchange 2013.</p></td>
</tr>
<tr class="even">
<td><p><a href="delegated-setup-exchange-2013-help.md">Configuração Delegada</a></p></td>
<td><p>Os administradores que são membros do grupo de funções da instalação delegada podem implantar servidores executando o Exchange 2013 que tenham sido previamente configurados por um membro do grupo de funções Gerenciamento da Organização.</p></td>
</tr>
</tbody>
</table>


Voltar ao início

## Grupos de função vinculados

Os grupos de função vinculados são usados em organizações que instalam o Exchange 2013 em uma floresta de recursos dedicada e que posicionam os usuários em outras florestas externas confiáveis. Os grupos de função vinculados, como o nome sugere, criam um vínculo entre um grupo de função na floresta do Exchange e um USG em uma floresta externa. Isso é útil quando as contas de usuário dos AD DS (serviços de domínio do Active Directory) dos administradores que você deseja administrar no Exchange não residem na mesma floresta de recursos que o Exchange. Grupos de função vinculados só podem ser associados a um USG externo. Além disso, não é preciso criar uma confiança bidirecional entre a floresta do Exchange e a floresta externa. A floresta do Exchange precisa confiar na floresta externa mas a floresta externa não precisa confiar na floresta do Exchange.

Para obter mais informações sobre permissões em topologias de várias florestas, consulte [Compreendendo as permissões de várias florestas](understanding-multiple-forest-permissions-exchange-2013-help.md).

Um grupo de função vinculado consiste em duas partes:

  - **Grupo de função vinculado** O grupo de função vinculado é um objeto contêiner que associa o USG externo às atribuições de função de gerenciamento atribuídas ao grupo de função.

  - **USG Externo** O USG externo contém os membros que devem receber permissões fornecidas pelo grupo de função vinculado.

Ao criar um grupo de função vinculado, você fornece um controlador de domínio na floresta externa que contém os usuários que você deseja que gerenciem a floresta do Exchange e o USG que contém esses usuários como membros, o nome do USG externo e as credenciais exigidas para acessar a floresta externa. O Exchange adiciona o SID (identificador de segurança) do USG externo ao grupo de função vinculado. Como o SID do USG é a única identificação do USG externo, recomendamos fortemente que você especifique a floresta externa no nome do grupo de função se tiver mais de uma floresta externa.

Um grupo de função vinculado não contém quaisquer membros. Todos os membro desse grupo de função são gerenciados usando o USG externo. Isso significa que não é possível usar os cmdlets **Update-RoleGroupMember**, **Add-RoleGroupMember** ou **Remove-RoleGroupMember** para adicionar ou remover membros do grupo de função. Ao adicionar membros ao USG externo, serão concedidas permissões a eles fornecidas pelo grupo de função vinculado.

Não é possível mudar um grupo de função padrão, que contém seus próprios membros, para um grupo de função vinculado e vice-versa. Se quiser transformar um grupo de função padrão em um grupo de função vinculado, crie um novo grupo de função vinculado e replique as atribuições de função de gerenciamento presentes no grupo de função padrão no grupo de função vinculado. Isso também se aplica a grupos de função internos, pois são grupos de função padrão. Se quiser realizar todo o gerenciamento de sua floresta do Exchange a partir de uma floresta externa, será preciso criar novos grupos de funções vinculados e adicionar as funções de gerenciamento existentes nos grupos de funções internos aos grupos de funções vinculados. Para mais informações sobre como fazer isto, consulte [Criar grupos de função vinculado que espelham grupos de função internos](create-linked-role-groups-that-mirror-built-in-role-groups-exchange-2013-help.md).

Voltar ao início

## Delegação de grupo de funções

Por padrão, os membros do grupo de função Gerenciamento da Organização podem adicionar e remover membros de grupos de função. Entretanto, você pode querer habilitar usuários que não sejam membros do grupo de função Gerenciamento da Organização a adicionar e remover membros de grupos de função. Nesse caso, você pode usar a delegação de grupo de função.

A delegação de grupo de função é controlada pela propriedade **ManagedBy** em cada grupo de função. A propriedade **ManagedBy** contém uma lista de usuários que podem adicionar ou remover membros desse grupo de função ou alterar a configuração de um grupo de função. Os usuários não recebem permissões dadas pelo grupo de função a não ser que também sejam membros dele.

Se a propriedade **ManagedBy** for definida em um grupo de função, apenas os usuários listados como gerenciadores de grupo de função nessa propriedade poderão modificar um grupo de função ou a associação de um grupo de função por padrão. Entretanto, um parâmetro opcional em cmdlets que modificam grupos de função ou associações de um grupo de função pode ignorar essa restrição. A opção *BypassSecurityGroupManagerCheck* pode ser usada por usuários que sejam membros da função Gerenciamento da Organização ou que estejam atribuídos, direta ou indiretamente, à função de gerenciamento Gerenciamento de Função. Quando essa opção é usada, a propriedade **ManagedBy** é ignorada e o usuário pode modificar o grupo de função ou a associação de grupo de função.

Se a propriedade **ManagedBy** não estiver definida em um grupo de função, apenas os usuários que forem membros da função Gerenciamento da Organização ou que estejam atribuídos, direta ou indiretamente, à função de gerenciamento Gerenciamento de Função poderão modificar um grupo de função ou uma associação de grupo de função.


> [!TIP]  
> As funções atribuídas a um grupo de função podem ser atribuídas usando atribuições de função de delegação. Com as atribuições de função de delegação, os membros de um grupo de função atribuído a uma função delegada podem atribuir essa função a outro grupo de função, diretiva de atribuição, usuário ou USG. Os membros do grupo de função podem atribuir apenas essa função e não podem delegar o grupo de função, a não ser que também tenham sido adicionados à propriedade <STRONG>ManagedBy</STRONG>. Para obter mais informações sobre as atribuições de função delegadas, consulte <A href="understanding-management-role-assignments-exchange-2013-help.md">Noções básicas sobre as atribuições de função de gerenciamento</A>.



Para obter mais informações sobre como gerenciar a delegação de grupo de função, consulte [Gerenciar grupos de função](manage-role-groups-exchange-2013-help.md).

Voltar ao início

## Associação de grupo de função

Quando um usuário se torna membro de um grupo de função, as funções de gerenciamento atribuídas ao grupo de função são atribuídas ao usuário. Se um usuário for membro de vários grupos de função, as funções de gerenciamento de cada grupo de função são agregadas e atribuídas ao usuário. Usuários, USGs e outros grupos de função podem ser membros de grupos de função.

Apenas os usuários que forem membros dos grupos de função Gerenciamento de Função ou Gerenciamento da Organização e os usuários aos quais foi delegada a capacidade de adicionar e remover usuários de grupos de função podem gerenciar associações de grupos de função.

Para mais informações sobre como gerenciar a delegação de grupo de funções, consulte [Gerenciar membros do grupo de função](manage-role-group-members-exchange-2013-help.md).

## Fluxo de trabalho de criação do grupo de funções

Como mencionado anteriormente, um grupo de função é composto de várias camadas. Para ajudá-lo a entender o que acontece quando um grupo de função é criado, considere o seguinte exemplo, que cria um novo grupo de função.

    New-RoleGroup -Name "Seattle Recipient Management" -Roles "Mail Recipients", "Distribution Groups", "Move Mailboxes", "UM Mailboxes" -CustomRecipientWriteScope "Seattle Users", -ManagedBy "Brian", "David", "Katie" -Members "Ray", "Jenn", "Maria", "Chris", "Maija", "Carter", "Jenny", "Sam", "Lukas", "Isabel", "Katie"

Quando o comando anterior é executado, acontece o seguinte:

1.  Um novo objeto de função, que é um USG especial, chamado Gerenciamento de Destinatários de Seattle, é criado.

2.  As caixas de correio de Ray, Jenn, Maria, Chris, Maija, Carter, Jenny, Sam, Lukas, Isabel e Katie são adicionadas como membros do grupo de funções. Esses usuários receberão as permissões fornecidas por esse grupo de função.

3.  Os usuários Brian e David são adicionados à propriedade **ManagedBy** do grupo de função. Esses usuários podem adicionar e remover membros do grupo de função, mas não receberão permissões fornecidas pelo grupo de função porque não são membros. Katie também é adicionada à propriedade **ManagedBy** do grupo de função. Como ela foi adicionada à propriedade **ManagedBy** e é membro do grupo de função, ela pode adicionar ou remover membros do grupo de função, e também recebe as permissões fornecidas pelo grupo de função.

4.  As seguintes atribuições de função de gerenciamento são criadas. As atribuições de função atribuem cada função de gerenciamento especificado no comando ao grupo de função. O escopo de gerenciamento Usuários de Seattle é adicionado a cada atribuição de função. O nome de cada atribuição de função é uma combinação da função de gerenciamento que está sendo atribuída e do nome do grupo de função.
    
      - `Mail Recipients_Seattle Recipient Management`
    
      - `Distribution Groups_Seattle Recipient Management`
    
      - `Move Mailboxes_Seattle Recipient Management`
    
      - `UM Mailboxes_Seattle Recipient Management`

Se comparar os resultados desse comando à figura de camadas de grupo de função de Gerenciamento vista anteriormente neste tópico, você verá onde cada etapa se correlaciona às camadas do grupo de função. Você poderá então consultar os tópicos de gerenciamento de grupo de funções de Gerenciamento em "Gerenciamento de grupo de funções", anteriormente neste tópico, para gerenciar cada camada de grupo de funções.

Voltar ao início

