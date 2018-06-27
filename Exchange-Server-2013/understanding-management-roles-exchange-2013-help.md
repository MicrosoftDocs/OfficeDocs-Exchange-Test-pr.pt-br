---
title: 'Noções básicas sobre funções de gerenciamento: Exchange 2013 Help'
TOCTitle: Noções básicas sobre funções de gerenciamento
ms:assetid: 887b0a64-84b1-4b8c-9547-e456ea6f5dbd
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Dd298116(v=EXCHG.150)
ms:contentKeyID: 50486100
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Noções básicas sobre funções de gerenciamento

 

_**Aplica-se a:**Exchange Server 2013_

_**Tópico modificado em:**2015-04-07_

Funções de gerenciamento são parte do modelo de permissões RBAC (controle de acesso baseado na função) usado no Microsoft Exchange Server 2013. As funções atuam como um agrupamento lógico de cmdlets que são combinados para fornecer acesso à exibição ou modificação da configuração de componentes do Exchange 2013, como caixas de correio, regras de transporte e destinatários. As funções de gerenciamento podem ser combinadas em agrupamentos maiores denominados grupos de funções de gerenciamento e políticas de atribuição de funções de gerenciamento, que permitem o gerenciamento de áreas de recursos e configuração de destinatários. Os grupos de funções e as diretivas de atribuição de funções atribuem permissões a administradores e usuários finais, respectivamente. Para mais informações sobre o grupos de funções de gerenciamento e diretivas de atribuição de funções, consulte [Controle de acesso baseado em função de compreensão](understanding-role-based-access-control-exchange-2013-help.md).


> [!TIP]
> Este tópico concentra-se na funcionalidade avançada de RBAC. Se você quiser gerenciar permissões básicas do Exchange 2013, como usar o Centro de Administração do Exchange (EAC) para adicionar e remover membros de grupos de funções, criar e modificar grupos de funções ou criar e modificar políticas de atribuição de função, consulte <A href="permissions-exchange-2013-help.md">Permissões</A>.



**Sumário**

Built-in management roles

Unscoped top-level management roles

Custom management roles

Management role hierarchy

Management role entries

Unscoped top-level role entries

Management role types

For more information

Os escopos e as atribuições de funções de gerenciamento são componentes importantes para a operação de funções de gerenciamento. Para obter mais informações sobre esses componentes, consulte os tópicos a seguir:

  - [Noções básicas sobre escopos da função de gerenciamento](understanding-management-role-scopes-exchange-2013-help.md)

  - [Noções básicas sobre as atribuições de função de gerenciamento](understanding-management-role-assignments-exchange-2013-help.md)

Procurando tarefas de gerenciamento relacionadas às funções de gerenciamento? Consulte [Permissões](permissions-exchange-2013-help.md).

## Funções de gerenciamento internas

Exchange 2013 oferece muitas funções de gerenciamento internas que podem ser usadas para administrar a sua organização. Cada função inclui os cmdlets e os parâmetros necessários para que os usuários gerenciem componentes específicos do Exchange. A seguir, exemplos de algumas funções de gerenciamento internas:

  - **Destinatários de Email** Permite que os administradores gerenciem caixas de correio, contatos e usuários de email.

  - **Regras de Transporte**   Permite que os administradores ou usuários especializados atribuídos à função gerenciem o recurso de regras de transporte.

  - **Grupos de Distribuição**   Permite que os administradores ou usuários especializados atribuídos à função gerenciem grupos de distribuição e membros de grupos de distribuição.

  - **Minhas Informações Pessoais** Permite que usuários finais modifiquem seus próprios números de telefone e endereço de site na Web.

Para obter uma lista completa das funções de gerenciamento incluídas com o Exchange 2013, consulte [Funções de gerenciamento internas](built-in-management-roles-exchange-2013-help.md).

As funções internas fornecidas com o Exchange 2013 podem ser combinadas de todas as maneiras para criar um modelo de permissões que funcione para o seu negócio. Por exemplo, se quiser que os membros de um grupo de funções gerenciem destinatários e pastas públicas, atribua as funções de Destinatário de Email e Pastas Públicas ao grupo de funções. Com frequência, atribua funções a grupos ou diretivas de atribuição de funções. Você poderál também atribuir funções de gerenciamento diretamente aos usuários se quiser controlar as permissões em um nível granular. Recomendamos usar os grupos de funções e as diretivas de atribuição de função em vez da atribuição de função de usuário direta para simplificar o modelo de permissões.


> [!TIP]
> Você só pode atribuir funções de gerenciamento de usuário final a diretivas de atribuição de função.



Funções de gerenciamento internas não podem ser alteradas. Entretanto, você pode criar funções de gerenciamento baseadas nas funções de gerenciamento internas e atribuir as novas a grupos ou diretivas de atribuição de funções. Você pode alterar as novas funções de gerenciamento para atender às suas necessidades. Essa é uma tarefa avançada que raramente precisará ser executada.

Para obter mais informações sobre a criação de funções personalizadas com base nas funções do Exchange internas, consulte Custom Management Roles posteriormente neste tópico.

Você precisa atribuir funções de gerenciamento para que elas tenham efeito. Com frequência, atribua funções de gerenciamento a grupos e diretivas de atribuição de funções. Em certas circunstâncias, convém atribuir funções diretamente a usuários, embora essa seja uma tarefa avançada que raramente precisará ser executada.

Para obter mais informações sobre a atribuição de funções de gerenciamento, consulte os seguintes tópicos:

  - [Gerenciar grupos de função](manage-role-groups-exchange-2013-help.md)

  - [Gerenciar políticas de atribuição de função](manage-role-assignment-policies-exchange-2013-help.md)

  - [Adicionar uma função a um usuário ou USG](add-a-role-to-a-user-or-usg-exchange-2013-help.md)

Para mais informações sobre as atribuições da função de gerenciamento, consulte [Noções básicas sobre as atribuições de função de gerenciamento](understanding-management-role-assignments-exchange-2013-help.md).

Voltar ao início

## Funções de gerenciamento de nível superior sem escopo

As funções de gerenciamento de nível superior sem escopo são um tipo especial de função de gerenciamento que permite conceder acesso a scripts personalizados e cmdlets que não sejam do Exchange a usuários que utilizam RBAC. Funções de gerenciamento regulares fornecem acesso somente a cmdlets Exchange. Se você precisar oferecer acesso a cmdlets não-Exchange executados em um servidor do Exchange ou se precisar publicar um script que possa ser executado pelos seus usuários, será preciso adicioná-los a uma função sem escopo. Elas são chamadas de função de nível superior porque quando uma função sem escopo é criada sem derivação de uma função pai, ela não tem nenhum pai e é um par das funções de gerenciamento internas fornecidas com o Exchange 2013. Para indicar que quer criar uma entrada de função de nível superior sem escopo, use a opção *UnscopedTopLevel* com o cmdlet **New-ManagementRole**.

As funções sem escopo são nomeadas dessa forma porque, ao contrato das funções de gerenciamento normais, elas não podem ter escopo definido para um destino específico. As funções sem escopo são sempre em toda a organização. Isso significa que alguém com uma função sem escopo atribuída pode modificar qualquer objeto na organização do Exchange 2013. Por esse motivo, deve tomar cuidado para se ter certeza de que os scripts e os cmdlets disponibilizados por meio de uma função sem escopo sejam testados completamente, para que você saiba o que eles modificarão, e que você tenha atribuído as funções sem escopo cuidadosamente.

As funções sem escopo podem ser atribuídas a destinatários de função, como grupos de funções, funções de gerenciamento, usuários e grupos de segurança universal (USGs). Elas não podem ser atribuídas a diretivas de atribuição de função de gerenciamento.

Embora os cmdlets de Exchange não possam ser adicionados como uma entrada de função de gerenciamento em uma função sem escopo, eles podem ser incluídos em scripts adicionados como entradas de função. Isso lhe permite criar scripts personalizados que executam tarefas do Exchange que podem ser atribuídas aos usuários. Um cenário útil é quando um usuário precisa executar uma tarefa com altos privilégios que normalmente fica fora do seu nível administrativo, e quando a criação de uma nova função de gerenciamento ou grupo de funções é problemática. Você pode criar um script que execute essa função específica, adicioná-lo a uma função sem escopo e atribuir a função sem escopo ao usuário. O usuário pode executar apenas a função específica fornecida pelo script.

As entradas de função adicionadas a uma função sem escopo devem também ser designadas como uma entrada de função de nível superior sem escopo. Para mais informações sobre entradas de função sem escopo, consulte Unscoped Top-Level Role Entries mais adiante neste tópico.

O grupo de funções Gerenciamento da Organização, por padrão, não tem permissões para criar ou gerenciar grupos de funções sem escopo. Isso serve para impedir que grupos de funções sem escopo sejam criados ou modificados erroneamente. O grupo de funções Gerenciamento da Organização pode delegar a função de gerenciamento Gerenciamento de Função sem Escopo a si mesmo e a outros destinatários de função. Para mais informações sobre como criar uma função de gerenciamento de nível superior sem escopo, consulte [Criar uma função sem escopo](create-an-unscoped-role-exchange-2013-help.md).

Voltar ao início

## Funções de gerenciamento personalizadas

Você pode criar funções de gerenciamento personalizadas com base em funções internas do Exchange quando as funções de gerenciamento internas não corresponderem às necessidades dos usuários. Quando você cria uma função de gerenciamento personalizada, a nova função filha herda todas as entradas de função de gerenciamento da função pai. Você pode escolher quais entradas de função de gerenciamento deseja manter na função de gerenciamento personalizada e remover todas as entradas indesejadas.

As funções personalizadas se tornam filhas da função usada para criar a nova função. É possível usar as entradas de função de gerenciamento apenas na nova função filha existente na função pai. Para obter mais informações, consulte as seções a seguir mais adiante neste tópico:

  - Management Role Hierarchy

  - Management Role Entries

A criação de funções de gerenciamento personalizadas requer várias etapas e é uma tarefa avançada que precisará raramente ser executada. Antes de criar uma função de gerenciamento personalizada, verifique se uma das funções de gerenciamento internas existentes não fornece as permissões necessárias. Para obter mais informações sobre as funções de gerenciamento internas ou se quiser criar funções de gerenciamento personalizadas, consulte os seguintes tópicos:

  - [Funções de gerenciamento internas](built-in-management-roles-exchange-2013-help.md)

  - [Permissões avançadas](advanced-permissions-exchange-2013-help.md)

Para mais informações sobre como criar uma função de gerenciamento, consulte [Criar uma função](create-a-role-exchange-2013-help.md).

Voltar ao início

## Hierarquia de funções de gerenciamento

Há funções de gerenciamento em uma hierarquia pai e uma filha. No topo da hierarquia estão as funções de gerenciamento internas fornecidas no Exchange 2013 por padrão. Quando uma função for criada, será feita uma cópia da função pai. A nova função é filha da função de que foi efetuada a cópia. Você pode personalizar a nova função para atender às necessidades dos administradores ou usuários aos quais deseja atribuí-la.

Funções personalizadas podem ser usadas para criar funções. Ao se criar uma função a partir de uma função personalizada existente, essa função existente continuará filha de sua função pai, mas também se tornará o pai da nova função. Toda vez que uma função for copiada, a nova função filha poderá conter apenas as entradas de função existentes na função pai imediata.

Cada função de gerenciamento recebe um tipo de função que não pode ser alterado. O tipo de função define o contexto base de uso da função. O tipo de função é copiado da função pai quando a função filha é criada.

**Hierarquia de funções de gerenciamento**

![Diagrama hierárquico de funções de gerenciamento de RBAC](images/Dd298116.6851c829-ca8f-40e7-a67c-cc9e85c33953(EXCHG.150).gif "Diagrama hierárquico de funções de gerenciamento de RBAC")

A figura anterior mostra a relação hierárquica das várias funções de gerenciamento. As funções Destinatários de Email e Suporte Técnico são internas. Todas as funções filhas derivadas dessas funções herdam o tipo de função de cada função interna. Por exemplo, todas as funções filhas derivadas direta ou indiretamente da função Destinatários de Email herdam o tipo de função `MailRecipients`.

A função personalizada Administradores de Destinatários de Seattle é filha da função interna Destinatários de Email, mas é também pai da função personalizada Administradores de Destinatários de Vendas de Seattle e da função personalizada Administradores de Destinatários Legalizados de Seattle. A função personalizada Administradores de Destinatários de Seattle contém apenas um subconjunto de cmdlets, que está disponível na função Destinatários de Email. As funções filhas da função personalizada Administradores de Destinatários de Seattle podem apenas conter cmdlets também existentes nessa função. Por exemplo, se houver um cmdlet na função Destinatários de Email, mas o cmdlet não existir na função personalizada Administradores de Destinatários de Seattle, o cmdlet não poderá ser adicionado à função personalizada Administradores de Destinatários de Vendas de Seattle.

Todas as funções personalizadas seguem o mesmo padrão das funções discutidas anteriormente. Para obter mais informações sobre como o acesso a cmdlets é controlado em funções de gerenciamento, consulte Management Role Entries a seguir neste tópico.

Voltar ao início

## Entradas de função de gerenciamento

Cada função de gerenciamento, seja ela uma função do Exchange personalizada ou uma sem escopo, deve ter pelo menos uma entrada de função de gerenciamento. Uma entrada é composta por um único cmdlet e seus parâmetros, um script ou uma permissão especial que você quer disponibilizar. Se um cmdlet ou script não aparecer como entrada em uma função de gerenciamento, esse cmdlet ou script não poderá ser acessado por meio dessa função. Da mesma forma, se um parâmetro não existir em uma entrada, o parâmetro nesse cmdlet ou script não poderá ser acessado por meio dessa função.

O Exchange 2013 permite gerenciar entradas de função com base em funções de nível superior de gerenciamento internas do Exchange e entradas de função com base em funções de gerenciamento de nível superior sem escopo. Funções baseadas em funções de nível superior internas do Exchange podem apenas conter entradas de função que sejam cmdlets do Exchange 2013. Para adicionar scripts personalizados ou cmdlets que não sejam do Exchange para que seus usuários possam utilizá-los, será preciso adicioná-los como entradas de função sem escopo a uma função de nível superior sem escopo. Para obter mais informações sobre entradas de função sem escopo, consulte Unscoped Top-Level Role Entries mais adiante neste tópico.

Todas as entradas de função, independentemente de a entrada de função ser baseada em cmdlet de Exchange ou ser sem escopo, siga os mesmos princípios explicados nas seções seguintes.

Para obter mais informações sobre o gerenciamento de entradas de função, consulte [Entradas de função e funções de gerenciamento](management-roles-and-role-entries-exchange-2013-help.md).

## Relacionamento da função de gerenciamento de pai e filho

Conforme mencionado anteriormente, uma entrada de função de gerenciamento, incluindo o cmdlet e seus parâmetros, deve existir na função pai imediata para adicionar a entrada à função filha. Por exemplo, se a função pai não tiver uma entrada para **New-Mailbox**, a função filha não poderá ser atribuída a esse cmdlet. Além disso, se **Set-Mailbox** estiver na função pai, mas o parâmetro *Database* tiver sido removido da entrada, o parâmetro *Database* no cmdlet **Set-Mailbox** não poderá ser adicionado à entrada na função filha.

Como você não pode adicionar entradas de função de gerenciamento a funções filhas se as entradas não aparecerem em funções pai, e como a função é baseada em um tipo de função específico, escolha cuidadosamente a função pai a ser copiada quando você quiser criar uma função personalizada.

Voltar ao início

## Nomes de entrada de função de gerenciamento

Os nomes de entrada de função de gerenciamento são uma combinação da função de gerenciamento a que eles estão associados e o nome do cmdlet ou do script. O nome da função e o cmdlet ou o script são separados por um caractere de barra invertida (\\). Por exemplo, o nome de entrada da função do cmdlet **Set-Mailbox** na função Destinatários de Email é `Mail Recipients\Set-Mailbox`. Se o nome de uma entrada de função contiver espaços, coloque-o entre aspas (").

O caractere curinga (\*) pode ser usado no nome de entrada principal para retornar todas as entradas de função correspondentes à entrada fornecida. O caractere curinga pode ser usado em cada lado do caractere de barra invertida. A tabela a seguir contém poucas variações em relação ao modo como você pode usar o caractere curinga em um nome de entrada de função.

**Nome de entrada de função de gerenciamento com caracteres curinga**


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Exemplo</th>
<th>Descrição</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code>*\*</code></p></td>
<td><p>Retorna uma lista de todas as entradas de função de todas as funções.</p></td>
</tr>
<tr class="even">
<td><p><code>*\Set-Mailbox</code></p></td>
<td><p>Retorna uma lista de todas as entradas de função que contêm o cmdlet <strong>Set-Mailbox</strong>.</p></td>
</tr>
<tr class="odd">
<td><p><code>Mail Recipients\*</code></p></td>
<td><p>Retorna uma lista de todas as entradas de função na função Destinatários de Email.</p></td>
</tr>
<tr class="even">
<td><p><code>Mail Recipients\*Mailbox</code></p></td>
<td><p>Retorna uma lista de todas as entradas de função na função Destinatários de Email que contêm cmdlets que terminem em Caixa de Correio.</p></td>
</tr>
<tr class="odd">
<td><p><code>My*\*Group*</code></p></td>
<td><p>Retorna uma lista de todas as entradas de função que contenham a cadeia de caracteres Grupo no nome do cmdlet de todas as funções que comecem com Meu.</p></td>
</tr>
</tbody>
</table>


## Entradas de função de nível superior sem escopo

As entradas de função de nível superior sem escopo são usadas com funções de gerenciamento de nível superior sem escopo para criar funções com base em scripts personalizados ou cmdlets que não sejam do Exchange. Cada entrada de função sem escopo é associada a um único script personalizado ou a um cmdlet não-Exchange. Para indicar que deseja criar uma entrada de função sem escopo em uma função sem escopo, é preciso especificar o parâmetro *UnscopedTopLevel* no cmdlet **Add-ManagementRoleEntry**.

Quando você adiciona a entrada de função sem escopo, é preciso especificar todos os parâmetros que podem ser usados com o script ou o cmdlet não-Exchange. As tentativas do Exchange de verificar os parâmetros fornecidos ao se adicionar a entrada de função. Apenas os parâmetros adicionados à entrada de função quando ela for criada estarão disponíveis aos usuários atribuídos à função sem escopo. Se você adicionar os parâmetros ao script ou ao cmdlet não-Exchange ou se um parâmetro for renomeado, será preciso atualizar a entrada de função manualmente. Exchange não verifica se os parâmetros existentes em uma entrada de função sem escopo foram alterados. Se um parâmetro de uma entrada de função for alterado em um script e você tentar usar esse parâmetro, o comando falhará.

Os scripts adicionados a uma entrada de função sem escopo devem residir no diretório de scripts do Exchange 2013 em cada servidor a que os administradores e usuários se conectam usando o Shell de Gerenciamento do Exchange. Se você tentar adicionar uma entrada de função sem escopo baseada em um script que não existe no diretório de scripts do Exchange 2013 no servidor sendo usado para adicionar a entrada de função, ocorrerá um erro. O local padrão de instalação do diretório de scripts do Exchange 2013 é C:\\Arquivos de Programas\\Microsoft\\Exchange Server\\V15\\RemoteScripts.

Os cmdlets não-Exchange adicionados a uma entrada de função sem escopo devem ser instalados em cada servidor do Exchange 2013 a que os administradores e usuários se conectam usando o Shell e querem usar os cmdlets. Se você tentar adicionar uma entrada de função sem escopo baseada em um cmdlet não-Exchange que não está instalado no servidor do Exchange 2013 sendo usado para adicionar a entrada de função, ocorrerá um erro. Ao adicionar um cmdlet que não seja do Exchange, é necessário especificar o nome do snap-in do Windows PowerShell que contém o cmdlet que não é do Exchange.

Para obter mais informações sobre como adicionar uma entrada de função de gerenciamento sem escopo, consulte [Adicionar uma entrada de função a uma função](add-a-role-entry-to-a-role-exchange-2013-help.md).

Voltar ao início

## Tipos de função de gerenciamento

Os tipos de função de gerenciamento são a base de todas as funções de gerenciamento. Os tipos definem os escopos implícitos definidos em todas as funções de gerenciamento de um tipo de função especificado e também atuam como um agrupamento lógico de funções relacionadas. Todas as funções de gerenciamento derivadas da função de gerenciamento interna pai têm o mesmo tipo de função. Consulte a figura de hierarquia da função de gerenciamento já mencionada neste tópico para ver esse relacionamento. Os tipos de função de gerenciamento também representam o conjunto máximo de cmdlets e seus parâmetros que podem ser adicionados a uma função associada a um tipo de função.

Os tipos de função de gerenciamento são divididos em categorias a seguir:

  - **Administrativa ou especializada**   As funções associadas aos tipos de função administrativa ou especializada têm um escopo mais amplo de impacto na organização do Exchange. As funções desse tipo de função permitem tarefas como gerenciamento de servidor ou de destinatário, configuração da organização, administração de conformidade, auditoria etc.

  - **Focada no usuário**   As funções associadas a um tipo de função focada no usuário têm um escopo de impacto bem vinculado a um usuário individual. As funções desse tipo de função permitem tarefas como configuração e autogerenciamento de perfil do usuário, gerenciamento de grupos de distribuição de propriedade do usuário etc.
    
    Os nomes das funções associadas a tipos de função focada no usuário e nomes de tipo de função focada no usuário começam com Meu.

  - **Especializada**   Funções associadas a tipos de função especializada permitem tarefas que não são tipos de função focada no usuário ou administrativa. As funções desse tipo de função permitem tarefas como representação de aplicativo e o uso de scripts ou cmdlets não-Exchange.

A tabela a seguir lista todos os tipos de função de gerenciamento administrativa no Exchange 2013 e se a configuração permitida pelo tipo de função é aplicada em toda a organização do Exchange ou apenas a um servidor individual. Para mais informações sobre as funções de gerenciamento associadas a esses tipos de função, incluindo uma descrição de cada função, que podem se beneficiar por estarem associadas à função, e outras informações, consulte [Funções de gerenciamento internas](built-in-management-roles-exchange-2013-help.md).

**Tipos de função administrativa**


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Tipo de função de gerenciamento</th>
<th>Função de gerenciamento integrada</th>
<th>Descrição</th>
<th>Organização ou servidor</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code>ActiveDirectoryPermissions</code></p></td>
<td><p><a href="active-directory-permissions-role-exchange-2013-help.md">Papel de permissões do diretório ativo</a></p></td>
<td><p>Esse tipo de função é associado a funções que permitem que administradores configurem permissões do Active Directory em uma organização. Alguns recursos que usam permissões do Active Directory ou uma ACL (lista de controle de acesso) incluem conectores de Envio e Recebimento, e as permissões Enviar como e Enviar em nome de para caixas de correio.</p>

> [!TIP]
> As permissões definidas diretamente em objetos Active Directory podem não ser impostas por meio de RBAC.


</td>
<td><p>Organization</p></td>
</tr>
<tr class="even">
<td><p><code>AddressLists</code></p></td>
<td><p><a href="address-lists-role-exchange-2013-help.md">Função de listas de endereços</a></p></td>
<td><p>Esse tipo de função é associado a funções que permitem que administradores gerenciem listas de endereços, a GAL (lista de endereços global) e listas de endereços offline em uma organização.</p></td>
<td><p>Organização</p></td>
</tr>
<tr class="odd">
<td><p><code>ApplicationImpersonation</code></p></td>
<td><p><a href="applicationimpersonation-role-exchange-2013-help.md">Função ApplicationImpersonation</a></p></td>
<td><p>Esse tipo de função é associado a funções que permitem que aplicativos se passem por usuários em uma organização para executar tarefas em nome do usuário.</p></td>
<td><p>Organização</p></td>
</tr>
<tr class="even">
<td><p><code>ArchiveApplication</code></p></td>
<td><p><a href="archiveapplication-role-exchange-2013-help.md">Função ArchiveApplication</a></p></td>
<td><p>Esse tipo de função é associado a funções que permitem que aplicativos de parceiros arquivem itens em caixas de correio de usuários de uma organização.</p></td>
<td><p>Organização</p></td>
</tr>
<tr class="odd">
<td><p><code>AuditLogs</code></p></td>
<td><p><a href="audit-logs-role-exchange-2013-help.md">Função de Logs de auditoria</a></p></td>
<td><p>Esse tipo de função é associado a funções que permitem que administradores gerenciem a configuração de log de auditoria de administrador em uma organização.</p></td>
<td><p>Organização</p></td>
</tr>
<tr class="even">
<td><p><code>CmdletExtensionAgents</code></p></td>
<td><p><a href="cmdlet-extension-agents-role-exchange-2013-help.md">Função de agentes de extensão de cmdlet</a></p></td>
<td><p>Esse tipo de função é associado a funções que permitem que administradores gerenciem agentes de extensão de cmdlet em uma organização.</p></td>
<td><p>Organização</p></td>
</tr>
<tr class="odd">
<td><p><code>DataLossPrevention</code></p></td>
<td><p><a href="data-loss-prevention-role-exchange-2013-help.md">Função de prevenção de perda de dados</a></p></td>
<td><p>Esse tipo de função é associado com funções que criam e gerenciam políticas de prevenção de perda de dados (DLP) e as regras delas em uma organização.</p></td>
<td><p>Organização</p></td>
</tr>
<tr class="even">
<td><p><code>DatabaseAvailabilityGroups</code></p></td>
<td><p><a href="database-availability-groups-role-exchange-2013-help.md">Função de grupos de disponibilidade de banco de dados</a></p></td>
<td><p>Esse tipo de função é associado a funções que permitem que administradores gerenciem DAGs (grupos de disponibilidade de banco de dados) em uma organização. Os administradores aos quais essa função tenha sido atribuída direta ou indiretamente são os administrados de mais alto nível responsáveis pela configuração de alta disponibilidade em uma organização.</p></td>
<td><p>Organização</p></td>
</tr>
<tr class="odd">
<td><p><code>DatabaseCopies</code></p></td>
<td><p><a href="database-copies-role-exchange-2013-help.md">Função de cópias de banco de dados</a></p></td>
<td><p>Esse tipo de função é associado a funções que permitem que administradores gerenciem cópias de banco de dados em servidores individuais.</p></td>
<td><p>Servidor</p></td>
</tr>
<tr class="even">
<td><p><code>Databases</code></p></td>
<td><p><a href="databases-role-exchange-2013-help.md">Função de bancos de dados</a></p></td>
<td><p>Esse tipo de função é associado a funções que permitem que administradores criem, gerenciem, montem e desmontem bancos de dados de caixa de correio em servidores individuais.</p></td>
<td><p>Servidor</p></td>
</tr>
<tr class="odd">
<td><p><code>DisasterRecovery</code></p></td>
<td><p><a href="disaster-recovery-role-exchange-2013-help.md">Função de recuperação de desastres</a></p></td>
<td><p>Esse tipo de função é associado a funções que permitem que administradores restaurem caixas de correio e bancos de dados de caixa de correio, criem bancos de dados de caixa de correio, e executem alternâncias e switchbacks de datacenter para grupos de disponibilidade de banco de dados em uma organização.</p></td>
<td><p>Organização</p></td>
</tr>
<tr class="even">
<td><p><code>DistributionGroups</code></p></td>
<td><p><a href="distribution-groups-role-exchange-2013-help.md">Função de grupos de distribuição</a></p></td>
<td><p>Esse tipo de função é associado a funções que permitem que administradores criem e gerenciem grupos de distribuição e membros de grupos de distribuição em uma organização.</p></td>
<td><p>Organização</p></td>
</tr>
<tr class="odd">
<td><p><code>EdgeSubscriptions</code></p></td>
<td><p><a href="edge-subscriptions-role-exchange-2013-help.md">Função de inscrições de borda</a></p></td>
<td><p>Esse tipo de função é associado a funções que permitem que administradores gerenciem configuração de assinatura e sincronização de borda entre os servidores de transporte de borda de Exchange 2010 e Exchange 2013 servidores de caixa de correio em uma organização.</p></td>
<td><p>Organização</p></td>
</tr>
<tr class="even">
<td><p><code>EmailAddressPolicies</code></p></td>
<td><p><a href="e-mail-address-policies-role-exchange-2013-help.md">Função de diretivas de endereço de email</a></p></td>
<td><p>Esse tipo de função é associado a funções que permitem que administradores gerenciem políticas de endereço de email em uma organização.</p></td>
<td><p>Organização</p></td>
</tr>
<tr class="odd">
<td><p><code>ExchangeConnectors</code></p></td>
<td><p><a href="exchange-connectors-role-exchange-2013-help.md">Função de conectores do Exchange</a></p></td>
<td><p>Esse tipo de função é associado a funções que habilitam os administradores a criar, modificar, exibir e remover conectores de agentes de entrega.</p></td>
<td><p>Organização</p></td>
</tr>
<tr class="even">
<td><p><code>ExchangeServerCertificates</code></p></td>
<td><p><a href="exchange-server-certificates-role-exchange-2013-help.md">Função de certificados de servidor do Exchange</a></p></td>
<td><p>Esse tipo de função é associado a funções que permitem que administradores criem, importem, exportem e gerenciem certificados de servidor do Exchange em servidores individuais.</p></td>
<td><p>Servidor</p></td>
</tr>
<tr class="odd">
<td><p><code>ExchangeServers</code></p></td>
<td><p><a href="exchange-servers-role-exchange-2013-help.md">Função de servidores do Exchange</a></p></td>
<td><p>Esse tipo de função é associado a funções que permitem que administradores gerenciem configuração de servidor do Exchange em servidores individuais.</p></td>
<td><p>Servidor</p></td>
</tr>
<tr class="even">
<td><p><code>ExchangeVirtualDirectories</code></p></td>
<td><p><a href="exchange-virtual-directories-role-exchange-2013-help.md">Função de diretórios virtuais do Exchange</a></p></td>
<td><p>Esse tipo de função é associado a funções que permitem que administradores gerenciem o Outlook Web App, Microsoft ActiveSync, catálogo de endereços offline (OAB), Descoberta Automática, Windows PowerShell e diretórios virtuais do Centro de Administração do Exchange em servidores individuais.</p></td>
<td><p>Servidor</p></td>
</tr>
<tr class="odd">
<td><p><code>FederatedSharing</code></p></td>
<td><p><a href="federated-sharing-role-exchange-2013-help.md">Função de compartilhamento federada</a></p></td>
<td><p>Esse tipo de função é associado a funções que permitem que administradores gerenciem o compartilhamento entre florestas e entre organizações em uma organização.</p></td>
<td><p>Organização</p></td>
</tr>
<tr class="even">
<td><p><code>InformationRightsManagement</code></p></td>
<td><p><a href="information-rights-management-role-exchange-2013-help.md">Função de gerenciamento de direitos de informação</a></p></td>
<td><p>Esse tipo de função é associado a funções que permitem que administradores gerenciem os recursos do Gerenciamento de Direitos de Informação (IRM) do Exchange em uma organização.</p></td>
<td><p>Organização</p></td>
</tr>
<tr class="odd">
<td><p><code>Journaling</code></p></td>
<td><p><a href="journaling-role-exchange-2013-help.md">Função de registro no diário</a></p></td>
<td><p>Esse tipo de função é associado a funções que permitem que administradores gerenciem a configuração de registro no diário em uma organização.</p></td>
<td><p>Organização</p></td>
</tr>
<tr class="even">
<td><p><code>LegalHold</code></p></td>
<td><p><a href="legal-hold-role-exchange-2013-help.md">Função de isenção legal</a></p></td>
<td><p>Esse tipo de função é associado a funções que permitem que administradores configurem se os dados de uma caixa de correio devem ser retidos para fins de litígio em uma organização.</p></td>
<td><p>Organização</p></td>
</tr>
<tr class="odd">
<td><p><code>MailboxImportExport</code></p></td>
<td><p><a href="mailbox-import-export-role-exchange-2013-help.md">Função Importar Exportar Caixa de Correio</a></p></td>
<td><p>Esse tipo de função é associado a funções que permitem que administradores importem e exportem conteúdo de caixa de correio e eliminem seu conteúdo indesejado.</p></td>
<td><p>Organização</p></td>
</tr>
<tr class="even">
<td><p><code>MailboxSearch</code></p></td>
<td><p><a href="mailbox-search-role-exchange-2013-help.md">Função de pesquisa de caixa de correio</a></p></td>
<td><p>Esse tipo de função é associado a funções que permitem que administradores pesquisem o conteúdo de uma ou mais caixas de correio em uma organização.</p></td>
<td><p>Organização</p></td>
</tr>
<tr class="odd">
<td><p><code>MailboxSearchApplication</code></p></td>
<td><p><a href="mailboxsearchapplication-role-exchange-2013-help.md">Função MailboxSearchApplication</a></p></td>
<td><p>Esse tipo de função é associado a funções que permitem que aplicativos de parceiros definam e exibam o status de retenção legal de uma caixa de correio de uma organização.</p></td>
<td><p>Organização</p></td>
</tr>
<tr class="even">
<td><p><code>MailEnabledPublicFolders</code></p></td>
<td><p><a href="mail-enabled-public-folders-role-exchange-2013-help.md">Função de pastas públicas habilitadas para email</a></p></td>
<td><p>Esse tipo de função é associado a funções que permitem aos administradores configurar se pastas públicas individuais serão habilitadas para email ou não em uma organização.</p>
<p>Esse tipo de função permite gerenciar apenas as propriedades de email de pastas públicas. Ele não permite gerenciar as propriedades de pastas públicas que não sejam propriedades de email. Para gerenciar propriedades de pastas públicas que não sejam propriedades de email, você precisa ter uma função associada ao tipo de função de <code>PublicFolders</code>.</p></td>
<td><p>Organização</p></td>
</tr>
<tr class="odd">
<td><p><code>MailRecipientCreation</code></p></td>
<td><p><a href="mail-recipient-creation-role-exchange-2013-help.md">Função de criação de destinatário do email</a></p>
<p></p></td>
<td><p>Esse tipo de função é associado a funções que permitem que administradores criem caixas de correio, usuários de email, contatos de email, grupos de distribuição e grupos de distribuição dinâmica em uma organização. As funções associadas a esse tipo de função podem ser combinadas às associadas ao tipo de função de <code>MailRecipients</code> para habilitar a criação e o gerenciamento de destinatários.</p>
<p>Esse tipo de função não permite que você habilite por email as pastas públicas. Para habilitar pastas públicas por email, você precisa ter uma função associada ao tipo de função de <code>MailEnabledPublicFolders</code>.</p>
<p>Caso a sua organização mantenha um modelo de permissões dividido, no qual a criação de destinatário é feita por um grupo diferente do grupo que executa o gerenciamento de destinatários, atribua a função de <code>MailRecipientCreation</code> ao grupo que executa a criação de destinatários, e a função de <code>MailRecipients</code> ao grupo que executa o gerenciamento de destinatários.</p></td>
<td><p>Organização</p></td>
</tr>
<tr class="even">
<td><p><code>MailRecipients</code></p></td>
<td><p><a href="mail-recipients-role-exchange-2013-help.md">Função de destinatários de email</a></p></td>
<td><p>Esse tipo de função é associado a funções que permitem que administradores gerenciem caixas de correio existentes, usuários de email, contatos de email, grupos de distribuição e grupos de distribuição dinâmica em uma organização. As funções associadas a esse tipo de função não podem criar esses destinatários, mas podem ser combinadas com as associadas ao tipo de função de <code>MailRecipientCreation</code> para habilitar a criação e o gerenciamento de destinatários.</p>
<p>Esse tipo de função não habilita você a gerenciar pastas públicas ou grupos de distribuição habilitados para email. Para gerenciar pastas públicas habilitadas por email, você precisa ter uma função associada ao tipo de função de <code>MailEnabledPublicFolders</code>. Para gerenciar grupos de distribuição, você precisa ter uma função associada ao tipo de função de <code>DistributionGroups</code>.</p>
<p>Caso a sua organização mantenha um modelo de permissões dividido, no qual a criação de destinatário é feita por um grupo diferente do grupo que executa o gerenciamento de destinatários, atribua a função de <code>MailRecipientCreation</code> ao grupo que executa a criação de destinatários, e a função de <code>MailRecipients</code> ao grupo que executa o gerenciamento de destinatários.</p></td>
<td><p>Organização</p></td>
</tr>
<tr class="odd">
<td><p><code>MailTips</code></p></td>
<td><p><a href="mail-tips-role-exchange-2013-help.md">Função de dicas de email</a></p></td>
<td><p>Esse tipo de função é associado a funções que permitem que administradores gerenciem Dicas de Email em uma organização.</p></td>
<td><p>Organização</p></td>
</tr>
<tr class="even">
<td><p><code>MessageTracking</code></p></td>
<td><p><a href="message-tracking-role-exchange-2013-help.md">Função de controle de mensagem</a></p></td>
<td><p>Esse tipo de função é associado a funções que permitem que administradores acompanhem mensagens em uma organização.</p></td>
<td><p>Organização</p></td>
</tr>
<tr class="odd">
<td><p><code>Migration</code></p></td>
<td><p><a href="migration-role-exchange-2013-help.md">Função de migração</a></p></td>
<td><p>Esse tipo de função é associado a funções que permitem que administradores migrem caixas de correio e o conteúdo da caixa de correio para um servidor ou para fora dele.</p></td>
<td><p>Servidor</p></td>
</tr>
<tr class="even">
<td><p><code>Monitoring</code></p></td>
<td><p><a href="monitoring-role-exchange-2013-help.md">Função de monitoramento</a></p></td>
<td><p>Esse tipo de função é associado a funções que permitem que administradores monitorem os serviços do Microsoft Exchange e a disponibilidade de componentes em uma organização. Além dos administradores, as funções associadas a esse tipo de função podem ser usadas com a conta de serviço usada pelos aplicativos de monitoramento para coletar informações sobre o estado dos servidores do Exchange.</p></td>
<td><p>Organização</p></td>
</tr>
<tr class="odd">
<td><p><code>MoveMailboxes</code></p></td>
<td><p><a href="move-mailboxes-role-exchange-2013-help.md">Mover caixas de correio função</a></p></td>
<td><p>Esse tipo de função é associado a funções que permitem que administradores movam caixas de correio entre servidores em uma organização e entre servidores na organização e em outra organização.</p></td>
<td><p>Organização</p></td>
</tr>
<tr class="even">
<td><p><code>OfficeExtensionApplication</code></p></td>
<td><p><a href="officeextensionapplication-role-exchange-2013-help.md">Função OfficeExtensionApplication</a></p></td>
<td><p>Esse tipo de função é associado a funções que permitem que aplicativos de extensão do Microsoft Office acessem caixas de correio de usuário de uma organização.</p></td>
<td><p>Organização</p></td>
</tr>
<tr class="odd">
<td><p><code>OrgCustomApps</code></p></td>
<td><p><a href="org-custom-apps-role-exchange-2013-help.md">Função org personalizado Apps</a></p></td>
<td><p>Esse tipo de função é associado a funções que permitem que administradores exibam e modifiquem os aplicativos personalizados de sua organização.</p></td>
<td><p>Organização</p></td>
</tr>
<tr class="even">
<td><p><code>OrgMarketplaceApps</code></p></td>
<td><p><a href="org-marketplace-apps-role-exchange-2013-help.md">Função de aplicativos do Marketplace org</a></p></td>
<td><p>Esse tipo de função é associado a funções que permitem que administradores exibam e modifiquem os aplicativos do marketplace de sua organização.</p></td>
<td><p>Organização</p></td>
</tr>
<tr class="odd">
<td><p><code>OrganizationClientAccess</code></p></td>
<td><p><a href="organization-client-access-role-exchange-2013-help.md">Função de acesso para cliente da organização</a></p></td>
<td><p>Esse tipo de função é associado a funções que permitem que administradores gerenciem configurações de servidor de Acesso ao Cliente em uma organização.</p></td>
<td><p>Organização</p></td>
</tr>
<tr class="even">
<td><p><code>OrganizationConfiguration</code></p></td>
<td><p><a href="organization-configuration-role-exchange-2013-help.md">Função de configuração de organização</a></p></td>
<td><p>Esse tipo de função é associado a funções que permitem que administradores gerenciem as configurações de toda a organização em uma organização. A configuração da organização que pode ser controlada com esse tipo de função inclui o seguinte e mais:</p>
<ul>
<li><p>Se as Dicas de Email estão habilitadas ou não para a organização.</p></li>
<li><p>A URL da home page de pasta gerenciada.</p></li>
<li><p>O endereço SMTP do destinatário do Microsoft Exchange e endereços de email alternativos.</p></li>
<li><p>A configuração de esquema de propriedade de caixa de correio de recurso.</p></li>
<li><p>As URLs de Ajuda para o Centro de Administração do Exchange e o Outlook Web App.</p></li>
</ul>
<p>Esse tipo de função não inclui as permissões incluídas nos tipos de função de <code>OrganizationClientAccess</code> ou <code>OrganizationTransportSettings</code>.</p></td>
<td><p>Organização</p></td>
</tr>
<tr class="odd">
<td><p><code>OrganizationTransportSettings</code></p></td>
<td><p><a href="organization-transport-settings-role-exchange-2013-help.md">Função de configurações de transporte da organização</a></p></td>
<td><p>Esse tipo de função é associado a funções que permitem que administradores gerenciem configurações de transporte em toda a organização, como mensagens de sistema, configuração de site Active Directory e outras configurações de transporte em toda a organização.</p>
<p>Essa função não permite a você criar ou gerenciar conectores de Recebimento ou Envio de transporte, filas, higienização, domínios remotos e aceitos ou regras. Para criar ou gerenciar todos os recursos de transporte, você precisa ter funções associadas aos seguintes tipos de função:</p>
<ul>
<li><p><strong>Conectores de recebimento</strong>   <code>ReceiveConnectors</code></p></li>
<li><p><strong>Conectores de envio</strong>   <code>SendConnectors</code></p></li>
<li><p><strong>Filas de transporte</strong>   <code>TransportQueues</code></p></li>
<li><p><strong>Higienização de transporte</strong>   <code>TransportHygiene</code></p></li>
<li><p><strong>Agentes de transporte</strong>   <code>TransportAgents</code></p></li>
<li><p><strong>Domínios remotos e aceitos</strong>   <code>RemoteAndAcceptedDomains</code></p></li>
<li><p><strong>Regras de transporte</strong>   <code>TransportRules</code></p></li>
</ul></td>
<td><p>Organização</p></td>
</tr>
<tr class="even">
<td><p><code>POP3AndIMAP4Protocols</code></p></td>
<td><p><a href="pop3-and-imap4-protocols-role-exchange-2013-help.md">Função de POP3 e IMAP4 protocolos</a></p></td>
<td><p>Esse tipo de função é associado a funções que permitem que administradores gerenciem configuração POP3 e IMAP4, como definições de autenticação e conexão, em servidores individuais.</p></td>
<td><p>Servidor</p></td>
</tr>
<tr class="odd">
<td><p><code>PublicFolders</code></p></td>
<td><p><a href="public-folders-role-exchange-2013-help.md">Função de Pastas Públicas</a></p></td>
<td><p>Esse tipo de função é associado a funções que permitem que administradores gerenciem pastas públicas em uma organização.</p>
<p>Esse tipo de função não permite que você gerencie se as pastas públicas são habilitadas para email. Para habilitar ou desabilitar uma pasta pública por email, você precisa ter uma função associada ao tipo de função de <code>MailEnabledPublicFolders</code>.</p></td>
<td><p>Organização</p></td>
</tr>
<tr class="even">
<td><p><code>ReceiveConnectors</code></p></td>
<td><p><a href="receive-connectors-role-exchange-2013-help.md">Função de conectores de recebimento</a></p></td>
<td><p>Esse tipo de função é associado a funções que permitem que administradores gerenciem a configuração do conector de Recebimento de transporte, como limites de tamanho em um servidor individual.</p></td>
<td><p>Servidor</p></td>
</tr>
<tr class="odd">
<td><p><code>RecipientPolicies</code></p></td>
<td><p><a href="recipient-policies-role-exchange-2013-help.md">Função de políticas de destinatário</a></p></td>
<td><p>Esse tipo de função é associado a funções que permitem que administradores gerenciem políticas de destinatário, como políticas de provisionamento e de dispositivos móveis, em uma organização.</p></td>
<td><p>Organização</p></td>
</tr>
<tr class="even">
<td><p><code>RemoteAndAcceptedDomains</code></p></td>
<td><p><a href="remote-and-accepted-domains-role-exchange-2013-help.md">Remoto e a função de domínios aceitos</a></p></td>
<td><p>Esse tipo de função é associado a funções que permitem que administradores gerenciem domínios remotos e aceitos em uma organização.</p></td>
<td><p>Organização</p></td>
</tr>
<tr class="odd">
<td><p><code>ResetPassword</code></p></td>
<td><p><a href="reset-password-role-exchange-2013-help.md">Redefinir senha função</a></p></td>
<td><p>Esse tipo de função é associado a funções que permitem que usuários redefinam suas próprias senhas e os administradores redefinam as senhas dos usuários em uma organização.</p></td>
<td><p>Organização</p></td>
</tr>
<tr class="even">
<td><p><code>RetentionManagement</code></p></td>
<td><p><a href="retention-management-role-exchange-2013-help.md">Função de gerenciamento de retenção</a></p></td>
<td><p>Esse tipo de função é associado a funções que permitem que administradores gerenciem diretivas de retenção em uma organização.</p></td>
<td><p>Organização</p></td>
</tr>
<tr class="odd">
<td><p><code>RoleManagement</code></p></td>
<td><p><a href="role-management-role-exchange-2013-help.md">Função de gerenciamento de função</a></p></td>
<td><p>Esse tipo de função é associado a funções que permitem que administradores gerenciem grupos de funções de gerenciamento, diretivas de atribuição de função, funções de gerenciamento, entradas de função, atribuições e escopos em uma organização.</p>
<p>Funções atribuídas a usuários com esse tipo de função podem substituir a propriedade <strong>role group managed by</strong>, configurar qualquer grupo de funções e adicionar ou remover membros a ou de qualquer grupo de funções.</p></td>
<td><p>Organização</p></td>
</tr>
<tr class="even">
<td><p><code>SecurityGroupCreationAndMembership</code></p></td>
<td><p><a href="security-group-creation-and-membership-role-exchange-2013-help.md">Criação de grupos de segurança e a associação de função</a></p></td>
<td><p>Esse tipo de função é associado a funções que permitem que administradores criem e gerenciem USGs e suas associações em uma organização.</p>
<p>Se sua organização mantiver um modelo de permissões divididas, no qual a criação e o gerenciamento de USGs são realizados por um grupo diferente do grupo que gerencia servidores do Exchange, atribua funções associadas a esse tipo de função a esse grupo.</p></td>
<td><p>Organização</p></td>
</tr>
<tr class="odd">
<td><p><code>SendConnectors</code></p></td>
<td><p><a href="send-connectors-role-exchange-2013-help.md">Função de conectores de envio</a></p></td>
<td><p>Esse tipo de função é associado a funções que permitem que administradores gerenciem conectores de envio de transporte em uma organização.</p></td>
<td><p>Organização</p></td>
</tr>
<tr class="even">
<td><p><code>SupportDiagnostics</code></p></td>
<td><p><a href="support-diagnostics-role-exchange-2013-help.md">Função Diagnóstico de Suporte</a></p></td>
<td><p>Esse tipo de função é associado a funções que permitem que administradores realizem um diagnóstico avançado sob a orientação dos serviços de suporte da Microsoft em uma organização.</p>

> [!WARNING]
> As funções associadas a esse tipo de função concedem permissões a cmdlets e scripts que devem ser usados apenas sob a orientação do Suporte e Atendimento ao Cliente Microsoft.


</td>
<td><p>Organização</p></td>
</tr>
<tr class="odd">
<td><p><code>TeamMailboxes</code></p></td>
<td><p><a href="team-mailboxes-role-exchange-2013-help.md">Função de caixas de correio de equipe</a></p></td>
<td><p>Esse tipo de função é associado a funções que permitem que os administradores definam uma ou mais políticas de provisionamento de caixa de correio de site e gerenciem caixas de correio de site em uma organização. Os administradores que receberam funções associadas a esse tipo de função podem gerenciar caixas de correio de site que não lhes pertencem.</p></td>
<td><p>Organização</p></td>
</tr>
<tr class="even">
<td><p><code>TeamMailboxLifecycleApplication</code></p></td>
<td><p><a href="teammailboxlifecycleapplication-role-exchange-2013-help.md">Função TeamMailboxLifecycleApplication</a></p></td>
<td><p>Esse tipo de função é associado a funções que permitem que aplicativos de parceiros atualizem estados de ciclo de vida de caixas de correio de site em uma organização.</p></td>
<td><p>Organização</p></td>
</tr>
<tr class="odd">
<td><p><code>TransportAgents</code></p></td>
<td><p><a href="transport-agents-role-exchange-2013-help.md">Função de agentes de transporte</a></p></td>
<td><p>Esse tipo de função é associado a funções que permitem que administradores gerenciem agentes de transporte em uma organização.</p></td>
<td><p>Organização</p></td>
</tr>
<tr class="even">
<td><p><code>TransportHygiene</code></p></td>
<td><p><a href="transport-hygiene-role-exchange-2013-help.md">Função de higienização de transporte</a></p></td>
<td><p>Esse tipo de função é associado a funções que permitem que administradores gerenciem recursos antispam e antimalware em uma organização.</p></td>
<td><p>Organização</p></td>
</tr>
<tr class="odd">
<td><p><code>TransportQueues</code></p></td>
<td><p><a href="transport-queues-role-exchange-2013-help.md">Função de filas de transporte</a></p></td>
<td><p>Esse tipo de função é associado a funções que permitem que administradores gerenciem filas de transporte em um servidor individual.</p></td>
<td><p>Servidor</p></td>
</tr>
<tr class="even">
<td><p><code>TransportRules</code></p></td>
<td><p><a href="transport-rules-role-exchange-2013-help.md">Função de regras de transporte</a></p></td>
<td><p>Esse tipo de função é associado a funções que permitem que administradores gerenciem regras de transporte em uma organização.</p></td>
<td><p>Organização</p></td>
</tr>
<tr class="odd">
<td><p><code>UMMailboxes</code></p></td>
<td><p><a href="um-mailboxes-role-exchange-2013-help.md">Função de caixas de correio de Unificação de mensagens</a></p></td>
<td><p>Esse tipo de função é associado a funções que permitem que administradores gerenciem a configuração de Unificação de Mensagens de caixas de correio em uma organização.</p></td>
<td><p>Organização</p></td>
</tr>
<tr class="even">
<td><p><code>UMPrompts</code></p></td>
<td><p><a href="um-prompts-role-exchange-2013-help.md">Função de Prompts de UM</a></p></td>
<td><p>Esse tipo de função é associado a funções que permitem que administradores criem e gerenciem prompts de voz de UM em uma organização.</p></td>
<td><p>Organização</p></td>
</tr>
<tr class="odd">
<td><p><code>UnifiedMessaging</code></p></td>
<td><p><a href="unified-messaging-role-exchange-2013-help.md">Função Unificação de mensagens</a></p></td>
<td><p>Esse tipo de função é associado a funções que permitem que administradores gerenciem serviços de Unificação de Mensagens em uma organização.</p>
<p>Essa função não permite a você gerenciar configurações de caixas de correio específicas da UM nem prompts da UM. Para gerenciar configuração de caixa de correio específica de UM, use funções associadas ao tipo de função <code>UMMailboxes</code>. Para gerenciar prompts de UM, use as funções associadas com o tipo de função <code>UMPrompts</code>.</p></td>
<td><p>Organização</p></td>
</tr>
<tr class="even">
<td><p><code>UnScopedRoleManagement</code></p></td>
<td><p><a href="unscoped-role-management-role-exchange-2013-help.md">Função de gerenciamento de função sem escopo</a></p></td>
<td><p>Esse tipo de função é associado a funções que permitem que administradores criem e gerenciem funções de gerenciamento de nível superior sem escopo em uma organização.</p></td>
<td><p>Organização</p></td>
</tr>
<tr class="odd">
<td><p><code>UserOptions</code></p></td>
<td><p><a href="user-options-role-exchange-2013-help.md">Função de opções do usuário</a></p></td>
<td><p>Esse tipo de função é associado a funções que permitem que administradores vejam as opções de Outlook Web App em uma organização. As funções associadas a esse tipo de função podem ser usadas para ajudar um usuário a diagnosticar problemas de sua configuração.</p></td>
<td><p>Organização</p></td>
</tr>
<tr class="even">
<td><p><code>UserApplication</code></p></td>
<td><p><a href="userapplication-role-exchange-2013-help.md">Função UserApplication</a></p></td>
<td><p>Esse tipo de função é associado a funções que permitem que aplicativos de parceiros ajam em nome de usuários finais de uma organização.</p></td>
<td><p>Organização</p></td>
</tr>
<tr class="odd">
<td><p><code>ViewOnlyAuditLogs</code></p></td>
<td><p><a href="view-only-audit-logs-role-exchange-2013-help.md">Função de Logs de auditoria somente para exibição</a></p></td>
<td><p>Esse tipo de função é associado a funções que permitem que administradores pesquisem no log de auditoria de administrador em uma organização.</p></td>
<td><p>Organização</p></td>
</tr>
<tr class="even">
<td><p><code>ViewOnlyConfiguration</code></p></td>
<td><p><a href="view-only-configuration-role-exchange-2013-help.md">Função de configuração de somente leitura</a></p></td>
<td><p>Esse tipo de função é associado a funções que permitem que administradores vejam todas as definições de configuração de Exchange que não são de destinatário em uma organização. Exemplos de configurações que podem ser exibidas são a configuração do servidor, a configuração de transporte, a configuração do banco de dados e a configuração geral da organização.</p>
<p>As funções associadas a esse tipo de função podem ser combinadas às associadas ao tipo de função de <code>ViewOnlyRecipients</code> para criar uma função que possa exibir cada objeto de uma organização.</p></td>
<td><p>Organização</p></td>
</tr>
<tr class="odd">
<td><p><code>ViewOnlyRecipients</code></p></td>
<td><p><a href="view-only-recipients-role-exchange-2013-help.md">Função destinatários de somente leitura</a></p></td>
<td><p>Esse tipo de função é associado a funções que permitem que administradores vejam a configuração de destinatários, como caixas de correio, usuários de email, contatos de email, grupos de distribuição e grupos de distribuição dinâmica.</p>
<p>As funções associadas a esse tipo de função podem ser combinadas às associadas ao tipo de função de <code>ViewOnlyConfiguration</code> para criar uma função que possa exibir cada objeto da organização.</p></td>
<td><p>Organização</p></td>
</tr>
<tr class="even">
<td><p><code>WorkloadManagement</code></p></td>
<td><p><a href="workloadmanagement-role-exchange-2013-help.md">Função WorkloadManagement</a></p></td>
<td><p>Esse tipo de função é associado a funções que permitem que administradores gerenciem políticas de gerenciamento de carga de trabalho em uma organização. Os administradores podem configurar definições de integridade de recursos e classificações de carga de trabalho, além de habilitar ou desabilitar o gerenciamento de cargas de trabalho.</p></td>
<td><p>Organização</p></td>
</tr>
</tbody>
</table>


A tabela a seguir lista todos os tipos de função de gerenciamento voltados para o usuário e suas funções de gerenciamento internas associadas no Exchange 2013.

**Tipos de função voltados para o usuário**


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Tipo de função de gerenciamento</th>
<th>Funções internas com foco no usuário</th>
<th>Descrição</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code>MyBaseOptions</code></p></td>
<td><p><a href="mybaseoptions-role-exchange-2013-help.md">Função MyBaseOptions</a></p></td>
<td><p>Esse tipo de função é associado a funções que permitem que usuários individuais vejam e modifiquem a configuração básica de sua própria caixa de correio e as definições associadas.</p></td>
</tr>
<tr class="even">
<td><p><code>MyContactInformation</code></p></td>
<td><p><a href="myaddressinformation-role-exchange-2013-help.md">Função MyAddressInformation</a></p>
<p><a href="mycontactinformation-role-exchange-2013-help.md">Função MyContactInformation</a></p>
<p><a href="mymobileinformation-role-exchange-2013-help.md">Função MyMobileInformation</a></p>
<p><a href="mypersonalinformation-role-exchange-2013-help.md">Função minhas informações pessoais</a></p></td>
<td><p>Esse tipo de função é associado a funções que permitem que usuários individuais modifiquem suas informações de contato. Essas informações incluem seus números de telefone e endereço.</p></td>
</tr>
<tr class="odd">
<td><p>MyCustomApps</p></td>
<td><p><a href="my-custom-apps-role-exchange-2013-help.md">Minha função personalizada Apps</a></p></td>
<td><p>Esse tipo de função é associado a funções que permitem que usuários individuais exibam e modifiquem seus aplicativos personalizados.</p></td>
</tr>
<tr class="even">
<td><p>MyDiagnostics</p></td>
<td><p><a href="mydiagnostics-role-exchange-2013-help.md">Função MyDiagnostics</a></p></td>
<td><p>Esse tipo de função é associado a funções que permitem que usuários individuais façam um diagnóstico básico de sua caixa de correio, como recuperar as informações de diagnóstico de calendário.</p></td>
</tr>
<tr class="odd">
<td><p><code>MyDistributionGroupMembership</code></p></td>
<td><p><a href="mydistributiongroupmembership-role-exchange-2013-help.md">Função MyDistributionGroupMembership</a></p></td>
<td><p>Esse tipo de função é associado a funções que permitem que usuários individuais vejam e modifiquem sua associação em grupos de distribuição em uma organização, contanto que esses grupos de distribuição permitam a manipulação da associação do grupo.</p></td>
</tr>
<tr class="even">
<td><p><code>MyDistributionGroups</code></p></td>
<td><p><a href="mydistributiongroups-role-exchange-2013-help.md">Função MyDistributionGroups</a></p></td>
<td><p>Esse tipo de função é associado a funções que permitem que usuários individuais criem, modifiquem e exibam grupos de distribuição e modifiquem, exibam, removam e adicionem membros a grupos de distribuição de sua propriedade.</p></td>
</tr>
<tr class="odd">
<td><p><code>MyProfileInformation</code></p></td>
<td><p><a href="mydisplayname-role-exchange-2013-help.md">Função MyDisplayName</a></p>
<p><a href="myname-role-exchange-2013-help.md">Função MyName</a></p>
<p><a href="myprofileinformation-role-exchange-2013-help.md">Função MyProfileInformation</a></p></td>
<td><p>Esse tipo de função é associado a funções que permitem que usuários individuais modifiquem seu nome.</p></td>
</tr>
<tr class="even">
<td><p>MyMarketplaceApps</p></td>
<td><p><a href="my-marketplace-apps-role-exchange-2013-help.md">Minha função de aplicativos do Marketplace</a></p></td>
<td><p>Esse tipo de função é associado a funções que permitem que usuários individuais exibam e modifiquem seus aplicativos do marketplace.</p></td>
</tr>
<tr class="odd">
<td><p><code>MyRetentionPolicies</code></p></td>
<td><p><a href="myretentionpolicies-role-exchange-2013-help.md">Função MyRetentionPolicies</a></p></td>
<td><p>Esse tipo de função é associado a funções que permitem que usuários individuais exibam as marcas de retenção e exibam e modifiquem os padrões e as configurações de marca de retenção.</p></td>
</tr>
<tr class="even">
<td><p>MyTeamMailboxes</p></td>
<td><p><a href="myteammailboxes-role-exchange-2013-help.md">Função MyTeamMailboxes</a></p></td>
<td><p>Esse tipo de função é associado a funções que permitem que usuários individuais criem caixas de correio de site e as conectem a sites do Microsoft SharePoint.</p></td>
</tr>
<tr class="odd">
<td><p><code>MyTextMessaging</code></p></td>
<td><p><a href="mytextmessaging-role-exchange-2013-help.md">Função MyTextMessaging</a></p></td>
<td><p>Esse tipo de função é associado a funções que permitem que usuários individuais criem, exibam e modifiquem suas configurações de mensagens.</p></td>
</tr>
<tr class="even">
<td><p><code>MyVoiceMail</code></p></td>
<td><p><a href="myvoicemail-role-exchange-2013-help.md">Função MyVoiceMail</a></p></td>
<td><p>Esse tipo de função é associado a funções que permitem que usuários individuais exibam e modifiquem suas configurações de caixa postal.</p></td>
</tr>
</tbody>
</table>


Voltar ao início

## Para obter mais informações

[New-ManagementRole](https://technet.microsoft.com/pt-br/library/dd298073\(v=exchg.150\))

[New-ManagementRoleAssignment](https://technet.microsoft.com/pt-br/library/dd335193\(v=exchg.150\))

[Set-ManagementRoleAssignment](https://technet.microsoft.com/pt-br/library/dd335173\(v=exchg.150\))

[New-ManagementScope](https://technet.microsoft.com/pt-br/library/dd335137\(v=exchg.150\))

[Set-ManagementScope](https://technet.microsoft.com/pt-br/library/dd297996\(v=exchg.150\))

[New-ManagementRoleAssignment](https://technet.microsoft.com/pt-br/library/dd335193\(v=exchg.150\))

[Set-ManagementRoleAssignment](https://technet.microsoft.com/pt-br/library/dd335173\(v=exchg.150\))

