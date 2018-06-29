---
title: 'Permissões: Exchange 2013 Help'
TOCTitle: Permissões
ms:assetid: d8dd605e-0af1-4e18-9ce6-e51d04e161ba
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Dd351175(v=EXCHG.150)
ms:contentKeyID: 50486800
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Permissões

 

_**Aplica-se a:**Exchange Server, Exchange Server 2013_

_**Tópico modificado em:**2015-03-09_

Microsoft Exchange Server 2013 inclui um amplo conjunto de permissões predefinidas, baseada no modelo de permissões do controle de acesso com base da função (RBAC), que você pode usar imediatamente facilmente conceder permissões a administradores e usuários. Você pode usar os recursos de permissões no Exchange 2013 para que você possa obter sua nova organização para cima e funcionando com rapidez.


> [!TIP]
> Diversos recursos e conceitos de RBAC não são discutidos neste tópico porque são recursos avançados. Caso a funcionalidade discutida neste tópico não atenda às suas necessidades e você queira personalizar mais seu modelo de permissões, consulte <A href="understanding-role-based-access-control-exchange-2013-help.md">Controle de acesso baseado em função de compreensão</A>.



Procurando uma lista de todos os tópicos de permissões? Consulte a documentação de permissões.

**Sumário**

Permissões baseadas em função

Grupos de função e políticas de atribuição de função

Trabalhar com grupos de função

Trabalhar com políticas de atribuição de função

## Permissões baseadas em função

Em Exchange 2013, as permissões concedidas aos administradores e usuários são baseadas em funções de gerenciamento. Uma função define o conjunto de tarefas que um administrador ou um usuário pode executar. Por exemplo, uma função de gerenciamento chamada `Mail Recipients` define as tarefas que pode ser executadas por alguém em um conjunto de caixas de correio, contatos e grupos de distribuição. Quando uma função for atribuída a um administrador ou usuário, essa pessoa recebe as permissões fornecidas pela função.

Existem dois tipos de funções, funções administrativas e de usuário final:

  - **Funções administrativas**   Essas funções contêm permissões que podem ser atribuídas aos administradores ou usuários especialistas utilizando grupos de função que gerenciam uma parte da organização Exchange, como destinatários, servidores ou bancos de dados.

  - **Funções de usuário final**   Essas funções, atribuídas por meio de diretivas de atribuição de função, permitem que os usuários gerenciem aspectos de suas próprias caixas de correio e grupos de distribuição de sua propriedade. As funções de usuário final começam com o prefixo `My`.

Funções conceder permissões para executar tarefas para administradores e usuários, tornando cmdlets disponíveis para aqueles que são atribuídas as funções. Porque o Centro de administração do Exchange (EAC) e Exchange Management Shell usam cmdlets para gerenciar Exchange, conceder acesso a um cmdlet concede a permissão de usuário ou administrador para executar a tarefa em cada uma do gerenciamento de Exchange interfaces.

Exchange 2013 inclui aproximadamente 86 funções que você pode usar para conceder permissões. Para obter uma lista das funções incluídas com Exchange 2013, consulte [Funções de gerenciamento internas](built-in-management-roles-exchange-2013-help.md).

Voltar ao início

## grupos de função e políticas de atribuição de função

Funções concedem permissões para executar tarefas em Exchange 2013, mas você precisa de uma maneira fácil de atribuí-las aos administradores e usuários. Exchange 2013 oferece as seguintes opções para ajudá-lo a fazer isso:

  - **Grupos de funções**   Os grupos de funções permitem conceder permissões a administradores e usuários especialistas.

  - **Diretivas de atribuição de função**   As diretivas de atribuição de função permitem conceder permissões a usuários finais para alterar as configurações em suas próprias caixas de correio ou grupos de distribuição.

Para obter mais informações sobre grupos de funções e diretivas de atribuição de função, consulte as próximas seções.

## Grupos de função

Cada administrador que gerencia Exchange 2013 deve ser atribuída a pelo menos uma ou mais funções. Os administradores podem ter mais de uma função porque eles podem executar funções que se expandem várias áreas em Exchange. Por exemplo, um administrador pode gerenciar destinatários e Exchange servidores. Nesse caso, esse administrador pode ser atribuída funções `Mail Recipients` tanto o `Exchange Servers` .

Para facilitar a atribuir várias funções para um administrador, Exchange 2013 inclui grupos de função. Função são grupos de segurança universais especiais (USGs) usados pelo Exchange 2013 que pode conter usuários Active Directory, USGs e outros grupos de função. Quando uma função for atribuída a um grupo de funções, as permissões concedidas pela função são concedidas para todos os membros do grupo de função. Isso permite que você atribua muitas funções aos membros do grupo de função muitas ao mesmo tempo. Normalmente, os grupos de função abrangem amplas áreas de gerenciamento, como gerenciamento de destinatários. Eles são usados apenas com funções administrativas e não as funções de usuário final.


> [!TIP]
> É possível atribuir uma função diretamente a um usuário ou USG sem usar um grupo de funções. Entretanto, esse método de atribuição de função é um procedimento avançado e não é discutido neste tópico. Recomendamos que você use grupos de funções para gerenciar permissões.



A figura a seguir mostra a relação entre usuários, grupos de funções e funções.

**Funções, grupos de função e membros de grupo de função do**

![Função, grupo de funções e relacionamentos de membros](images/Dd351175.3fb0b47d-333a-4953-ae38-d710d327bde0(EXCHG.150).gif "Função, grupo de funções e relacionamentos de membros")

Exchange 2013 inclui vários grupos de função internos, cada um fornecendo permissões para gerenciar as áreas específicas em Exchange 2013. Alguns grupos de função podem sobrepor-se com outras pessoas. A tabela a seguir lista cada grupo de função com uma descrição de usá-las. Se você deseja ver as funções atribuídas a cada grupo de função, clique no nome do grupo de funções, na coluna "Grupo de função" e, em seguida, abra a seção "Funções atribuídas a esse grupo de funções gerenciamento".

### Grupos de funções internos

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Grupo de função</th>
<th>Descrição</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="organization-management-exchange-2013-help.md">Gerenciamento da Organização</a></p></td>
<td><p>Os administradores que são membros do grupo de função Gerenciamento da Organização tem acesso administrativo para a organização inteira Exchange 2013 e podem executar quase qualquer tarefa contra qualquer objeto Exchange 2013, com algumas exceções, como a função <code>Discovery Management</code> .</p>

> [!IMPORTANT]
> Como o grupo de funções Gerenciamento da Organização é uma função muito poderosa, somente usuários ou USGs que executar tarefas administrativas em nível organizacional potencial para afetar a organização inteira Exchange devem ser membros desse grupo de função.


</td>
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
<td><p>Administradores que sejam membros de UM gerenciamento de grupo de função pode gerenciar recursos na organização de Exchange como a configuração do serviço de Unificação de mensagens (UM), as propriedades UM em caixas de correio, solicita a Unificação de mensagens e a configuração attendant automática de Unificação de mensagens.</p></td>
</tr>
<tr class="odd">
<td><p><a href="help-desk-exchange-2013-help.md">Suporte Técnico</a></p></td>
<td><p>O grupo de função Help Desk, por padrão, permite que membros exibir e modificar as opções do Microsoft OfficeOutlook Web App de qualquer usuário na organização. Essas opções podem incluir a modificação do nome para exibição do usuário, endereço e número de telefone. Eles não incluem as opções que não estão disponíveis nas opções de Outlook Web App, modificando o tamanho de uma caixa de correio ou configurar o banco de dados de caixa de correio no qual uma caixa de correio está localizada.</p></td>
</tr>
<tr class="even">
<td><p><a href="hygiene-management-exchange-2013-help.md">Gerenciamento de Higienização</a></p></td>
<td><p>Os administradores que são membros do grupo de funções de gerenciamento de higienização podem configurar os recursos de antivírus e antispam do Exchange 2013. Programas de terceiros que integram com Exchange 2013 podem adicionar contas de serviço a esse grupo de função para conceder acesso desses programas para os cmdlets necessários para recuperar e configurar a configuração Exchange.</p></td>
</tr>
<tr class="odd">
<td><p><a href="records-management-exchange-2013-help.md">Gerenciamento de Registros</a></p></td>
<td><p>Os usuários que forem membros do grupo de função Gerenciamento de Registros podem configurar recursos de conformidade, como marcas de diretivas de retenção, classificações de mensagens e regras de transporte.</p></td>
</tr>
<tr class="even">
<td><p><a href="discovery-management-exchange-2013-help.md">Gerenciamento de Descobertas</a></p></td>
<td><p>Os administradores ou usuários que sejam membros do grupo de função Gerenciamento de Descobertas podem realizar pesquisas de caixas de correio na organização Exchange para os dados que atenda a critérios específicos e também podem configurar os armazenamentos legais em caixas de correio.</p></td>
</tr>
<tr class="odd">
<td><p><a href="public-folder-management-exchange-2013-help.md">Gerenciamento de Pasta Pública</a></p></td>
<td><p>Administradores que são membros do grupo de funções Gerenciamento de Pasta Pública podem gerenciar pastas públicas em servidores com o Exchange 2013.</p></td>
</tr>
<tr class="even">
<td><p><a href="server-management-exchange-2013-help.md">Gerenciamento de Servidor</a></p></td>
<td><p>Administradores que sejam membros do grupo de funções de Gerenciamento de Servidor podem definir configurações específicas de recursos de servidor de transporte, Unificação de Mensagens, acesso para cliente e caixa de correio, como cópias de bancos de dados, certificados, filas de transporte e conectores de Envio, diretórios virtuais e protocolos de acesso para cliente.</p></td>
</tr>
<tr class="odd">
<td><p><a href="delegated-setup-exchange-2013-help.md">Configuração Delegada</a></p></td>
<td><p>Os administradores que são membros do grupo de funções da instalação delegada podem implantar servidores executando o Exchange 2013 que tenham sido previamente configurados por um membro do grupo de funções Gerenciamento da Organização.</p></td>
</tr>
<tr class="even">
<td><p><a href="compliance-management-exchange-2013-help.md">Gerenciamento de Conformidade</a></p></td>
<td><p>Os usuários que são membros do grupo de funções de gerenciamento de conformidade podem configurar e gerenciar configurações de conformidade do Exchange de acordo com a política da sua organização.</p></td>
</tr>
</tbody>
</table>


Se você trabalha em uma pequena organização que tem apenas alguns administradores, talvez seja necessário adicionar os administradores para o grupo de funções Gerenciamento da Organização apenas e nunca talvez seja necessário usar os outros grupos de função. Se você trabalha em uma grande organização, talvez você tenha os administradores que executam tarefas específicas administrando Exchange, como o destinatário ou o servidor de gerenciamento. Nesses casos, é possível adicionar um administrador para o grupo de funções Gerenciamento de Destinatários e outro administrador ao grupo de funções de gerenciamento de servidor. Os administradores podem gerenciar suas áreas específicas da Exchange 2013, mas não terão permissões para gerenciar as áreas que eles não estejam responsáveis por.

Se os grupos de função internos em Exchange 2013 não coincidir com a função de trabalho dos seus administradores, você pode criar grupos de funções e adicionar funções a eles. Para obter mais informações, consulte trabalhar com os grupos de função posteriormente neste tópico.

Voltar ao início

## Diretivas de atribuição de função

Exchange 2013 fornece diretivas de atribuição de função, de modo que você pode controlar quais configurações podem ser definidas por seus usuários em suas próprias caixas de correio e nos grupos de distribuição são proprietários. Essas configurações incluem seu nome para exibição, informações de contato, configurações de caixa postal e a associação de grupo de distribuição.

Sua organização Exchange 2013 pode ter várias políticas de atribuição de função que oferecem diferentes níveis de permissões para os diferentes tipos de usuários em suas organizações. Alguns usuários podem ter permissão para alterar seu endereço ou criar grupos de distribuição, enquanto outros não, dependendo da política de atribuição de função associada à sua caixa de correio. Políticas de atribuição de função são adicionadas diretamente às caixas de correio, e cada caixa de correio só pode ser associada a política de atribuição de uma função por vez.

Entre as diretivas de atribuição de função em sua organização, uma é identificada como padrão. A diretiva de atribuição de função padrão é associada a novas caixas de correio que não tenham uma diretiva de atribuição de função específica explicitamente atribuída ao serem criadas. A diretiva de atribuição de função padrão deve conter as permissões que serão aplicadas à maioria de suas caixas de correio.

As permissões são adicionadas às diretivas de atribuição de função por meio de funções de usuário final. As funções de usuário final começam com `My` e concedem permissões para que os usuários gerenciem apenas suas próprias caixas de correio ou grupos de distribuição. Elas não podem ser usadas para gerenciar qualquer outra caixa de correio. Somente funções de usuário final podem ser atribuídas às diretivas de atribuição de função.

Quando uma função de usuário final é atribuída a uma diretiva de atribuição de função, todas as caixas de correio associadas a essa diretiva recebem as permissões concedidas pela função. Isso permite adicionar ou remover permissões de conjuntos de usuários sem ter de configurar as caixas de correio individuais. A figura a seguir mostra:

  - Funções de usuário final são atribuídas a diretivas de atribuição de função. Diretivas de atribuição de função podem compartilhar as mesmas funções de usuário final.

  - Diretivas de atribuição de função são associadas a caixas de correio. Cada caixa de correio só pode ser associada a uma diretiva de atribuição de função.

  - Quando uma caixa de correio é associada a uma política de atribuição de função, as funções de usuário final são aplicadas a essa caixa de correio. As permissões concedidas pelas funções são concedidas ao usuário da caixa de correio.

**Funções, diretivas de atribuição de função e caixas de correio**

![Função, diretiva de atribuição de função, relacionamento de caixa de correio](images/Dd351175.82e07b3d-da59-465b-b349-e0bfde369ace(EXCHG.150).gif "Função, diretiva de atribuição de função, relacionamento de caixa de correio")

A política de atribuição de função de política de atribuição de função padrão está incluída no Exchange 2013. Como o nome implica, é a política de atribuição de função padrão. Se você deseja alterar as permissões fornecidas por essa política de atribuição de função, ou se você deseja criar políticas de atribuição de função, consulte trabalhar com políticas de atribuição de função posteriormente neste tópico.

## Trabalhar com grupos de funções

Para gerenciar suas permissões usando grupos de função no Exchange 2013, recomendamos que você use o Centro de administração do Exchange. Quando você usar o EAC para gerenciar grupos de função, você pode adicionar e remover membros e funções, crie grupos de função e copiar os grupos de função com poucos cliques do mouse. O EAC fornece caixas de diálogo simples, como a caixa de diálogo **novo grupo de funções**, mostrada na figura a seguir, para executar essas tarefas.

**Caixa de diálogo de nova grupo de funções no EAC**

![Caixa de diálogo de novo grupo de funções no EAC](images/Dd351175.e0577090-73e6-4671-ae98-78a8064fde87(EXCHG.150).jpg "Caixa de diálogo de novo grupo de funções no EAC")

Exchange 2013 inclui vários grupos de função que separam permissões em áreas administrativas específicas. Se esses grupos de função existente fornecem as permissões que os administradores precisam gerenciar sua organização Exchange 2013, você só precisa adicionar os seus administradores como membros dos grupos de função adequada. Depois de adicionar administradores a um grupo de funções, eles podem administrar os recursos relacionados a esse grupo de função. Para adicionar ou remover membros de um grupo de funções, abra o grupo de funções no EAC e adicionar ou remover membros da lista de membros. Para obter uma lista de grupos de funções internas, consulte [Grupos de funções internos](built-in-role-groups-exchange-2013-help.md).


> [!IMPORTANT]
> Se um administrador é um membro de mais de um grupo de funções, Exchange 2013 concede o administrador todas as permissões fornecidas pelos grupos de função, de que ele é um membro.



Se nenhum dos grupos de função incluídos Exchange 2013 tiver as permissões que necessárias, você pode usar o EAC para criar um grupo de funções e adicionar as funções que têm as permissões que necessárias. Para seu novo grupo de função, você irá:

1.  Escolher um nome para o grupo de funções.

2.  Selecionar as funções que deseja adicionar ao grupo de funções.

3.  Adicionar membros ao grupo de funções.

4.  Salvar o grupo de funções.

Após ter criado o grupo de funções, você o gerencia como qualquer outro grupo de funções.

Caso exista um grupo de funções contendo algumas, mas não todas as permissões de que você precisa, você pode copiá-lo e fazer alterações para criar um grupo de funções. É possível copiar um grupo de funções existente e fazer alterações nele sem afetar o grupo de funções original.Como parte da cópia do grupo de funções, é possível atribuir um novo nome e descrição, adicionar e remover funções desse novo grupo de funções e adicionar novos membros. Para criar ou copiar um grupo de funções, é usada a mesma caixa de diálogo mostrada na figura anterior.

Grupos de função existentes também podem ser modificados. Você pode adicionar e remover funções dos grupos de função existente e adicionar e remover membros a partir ao mesmo tempo, usando uma caixa de diálogo EAT similar na figura anterior. Adicionando e Removendo funções para e de grupos de função, você ativar e desativar recursos administrativos para que os membros desse grupo de função. Para obter uma lista das funções que você pode adicionar a um grupo de funções, consulte [Funções de gerenciamento internas](built-in-management-roles-exchange-2013-help.md).


> [!TIP]
> Embora seja possível alterar as funções atribuídas aos grupos de funções internos, recomendamos copiar esses grupos de funções, alterar a cópia e então adicionar os membros ao grupo de funções copiado.



Voltar ao início

## Trabalhar com políticas de atribuição de função

Para gerenciar as permissões que você conceda a usuários finais para gerenciar suas próprias caixas de correio em Exchange 2013, recomendamos que você use o EAC. Quando você usar o EAC para gerenciar permissões de usuário final, você pode adicionar funções, remover funções e criar políticas de atribuição de função com poucos cliques do mouse. O EAC fornece caixas de diálogo simples, como a caixa de diálogo **política de atribuição de função**, mostrada na figura a seguir, para executar essas tarefas.

**Caixa de diálogo de política de atribuição de funções no EAC**

![Caixa de diálogo de política de atribuição de funções no EAC](images/Dd351175.ecdf3cd4-d50e-4014-95f8-1bd5dafacaff(EXCHG.150).jpg "Caixa de diálogo de política de atribuição de funções no EAC")

Exchange 2013 inclui uma política de atribuição de função denominada política de atribuição de função padrão. Esta política de atribuição de função permite que os usuários cujas caixas de correio estão associadas ele para fazer o seguinte:

  - Associar-se ou sair de grupos de distribuição que permitam aos membros gerenciar suas próprias associações.

  - Exibir e modificar configurações básicas de suas caixas de correio, como regras da Caixa de Entrada, comportamento da correção ortográfica, configurações de lixo eletrônico, e dispositivos do Microsoft ActiveSync.

  - Modificar suas informações de contato, como endereço comercial e número de telefone, número de telefone celular e número de pager.

  - Criar, modificar ou exibir configurações de mensagens de texto.

  - Exibir ou modificar as configurações de caixa postal.

  - Exibir e modificar seus aplicativos do marketplace.

  - Criar caixas de correio de equipe e conectá-las às listas do Microsoft SharePoint.

Se quiser adicionar ou remover permissões da Política de Atribuição de Função Padrão ou de qualquer outra política de atribuição de função, você pode usar o EAC. A caixa de diálogo usada é semelhante à da figura anterior. Ao abrir a política de atribuição de função no EAC, marque a caixa de seleção ao lado das funções que você deseja atribuir e desmarque a caixa de seleção das funções que você deseja remover. A alteração feita na diretiva de atribuição de função é aplicada a todas as caixas de correio associadas a ela.

Caso queira atribuir diferentes permissões de usuário final aos vários tipos de usuários em sua organização, você pode criar diretivas de atribuição de função. Ao criar uma política de atribuição de função, será exibida uma caixa de diálogo semelhante à da figura anterior. Você pode especificar um novo nome para a política de atribuição de função e então selecionar as funções que deseja atribuir à política de atribuição de função. Depois de criar uma política de atribuição de função, você poderá associá-la a caixas de correio usando o EAC.

Se quiser alterar a diretiva de atribuição de função padrão, você terá que usar o Shell. Quando a política de atribuição de função padrão é alterada, todas as caixas de correio criadas serão associadas à nova política de atribuição de função se nenhuma política for explicitamente especificada. A diretiva de atribuição de função associada às caixas de correio existentes não muda quando é selecionada uma nova diretiva de atribuição de função padrão.


> [!TIP]
> Se você marcar a caixa de seleção de uma função com funções filhas, as caixas de seleção das funções filhas também serão marcadas. Se você desmarcar a caixa de seleção de uma função com funções filhas, as caixas de seleção das funções filhas também serão desmarcadas.<BR>Para obter uma descrição detalhada de como criar diretivas de atribuição de função ou fazer alterações nas diretivas de atribuição de função existentes, consulte os seguintes tópicos: 
> <UL>
> <LI>
> <P><A href="manage-role-assignment-policies-exchange-2013-help.md">Gerenciar políticas de atribuição de função</A></P>
> <LI>
> <P><A href="change-the-assignment-policy-on-a-mailbox-exchange-2013-help.md">Alterar a política de atribuição de uma caixa de correio</A></P></LI></UL>



Voltar ao início

## Documentação de permissões

A tabela a seguir contém links para tópicos que ajudarão você a aprender sobre e gerenciar permissões no Exchange 2013.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Tópico</th>
<th>Descrição</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="understanding-role-based-access-control-exchange-2013-help.md">Controle de acesso baseado em função de compreensão</a></p></td>
<td><p>Conheça cada um dos componentes que compõem do RBAC e saiba como é possível criar modelos de permissões avançados se os grupos de função e as funções de gerenciamento não forem suficientes.</p></td>
</tr>
<tr class="even">
<td><p><a href="understanding-multiple-forest-permissions-exchange-2013-help.md">Compreendendo as permissões de várias florestas</a></p></td>
<td><p>Saiba mais sobre como implementar as permissões de RBAC em organizações com as florestas de conta e de recurso.</p></td>
</tr>
<tr class="odd">
<td><p><a href="understanding-split-permissions-exchange-2013-help.md">Compreendendo as permissões de divisão</a></p></td>
<td><p>Saiba mais sobre a divisão do Exchange e o gerenciamento de entidade de segurança usando o Active Directory e RBAC dividir permissões.</p></td>
</tr>
<tr class="even">
<td><p><a href="understanding-permissions-coexistence-with-exchange-2007-and-exchange-2010-exchange-2013-help.md">Noções básicas sobre a coexistência de permissões com o Exchange 2007 e Exchange 2010</a></p></td>
<td><p>Configure permissões para habilitar a administração do Exchange 2013 em organizações existentes do Exchange 2007 e Exchange 2010.</p></td>
</tr>
<tr class="odd">
<td><p><a href="manage-role-groups-exchange-2013-help.md">Gerenciar grupos de função</a></p></td>
<td><p>Configure permissões para administradores do Exchange e usuários especialistas utilizando grupos de função.</p></td>
</tr>
<tr class="even">
<td><p><a href="manage-role-group-members-exchange-2013-help.md">Gerenciar membros do grupo de função</a></p></td>
<td><p>Adicione membros de e para grupos de função. Adicionando e removendo membros para e de grupos de função, você configurar quem é possível administrar recursos do Exchange.</p></td>
</tr>
<tr class="odd">
<td><p><a href="manage-linked-role-groups-exchange-2013-help.md">Gerenciar grupos de função vinculado</a></p></td>
<td><p>Configure permissões para administradores do Exchange e usuários especialistas em implantações do Exchange de várias florestas.</p></td>
</tr>
<tr class="even">
<td><p><a href="manage-role-assignment-policies-exchange-2013-help.md">Gerenciar políticas de atribuição de função</a></p></td>
<td><p>Configure a quais recursos os usuários finais têm acesso em suas caixas de correio usando políticas de atribuição de função.</p></td>
</tr>
<tr class="odd">
<td><p><a href="change-the-assignment-policy-on-a-mailbox-exchange-2013-help.md">Alterar a política de atribuição de uma caixa de correio</a></p></td>
<td><p>Configure qual política de atribuição de função é aplicada a uma ou mais caixas de correio.</p></td>
</tr>
<tr class="even">
<td><p><a href="create-linked-role-groups-that-mirror-built-in-role-groups-exchange-2013-help.md">Criar grupos de função vinculado que espelham grupos de função internos</a></p></td>
<td><p>Recriar os grupos de função internos como grupos de função vinculado em implantações do Exchange de várias florestas.</p></td>
</tr>
<tr class="odd">
<td><p><a href="view-effective-permissions-exchange-2013-help.md">Exibir permissões efetivas</a></p></td>
<td><p>Modo de exibição que tenha permissões para administrar recursos do Exchange.</p></td>
</tr>
<tr class="even">
<td><p><a href="feature-permissions-exchange-2013-help.md">Permissões de recurso</a></p></td>
<td><p>Saiba mais sobre as permissões necessárias para gerenciar os serviços e recursos do Exchange.</p></td>
</tr>
<tr class="odd">
<td><p><a href="advanced-permissions-exchange-2013-help.md">Permissões avançadas</a></p></td>
<td><p>Use os recursos avançados de RBAC para criar modelos de permissão altamente personalizada para atender às necessidades de qualquer organização.</p></td>
</tr>
</tbody>
</table>

