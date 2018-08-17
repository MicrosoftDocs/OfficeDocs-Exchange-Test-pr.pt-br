---
title: 'Compreendendo as permissões de divisão: Exchange 2013 Help'
TOCTitle: Compreendendo as permissões de divisão
ms:assetid: 2b709e15-63a2-4841-94bc-b289b71166d0
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Dd638106(v=EXCHG.150)
ms:contentKeyID: 50485225
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Compreendendo as permissões de divisão

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2015-04-07_

As organizações que separam o gerenciamento de objetos do Microsoft Exchange Server 2013 e Active Directory usam o que é chamado um modelo de *permissões de divisão* . Permissões de divisão permitem que as organizações atribuir permissões específicas e tarefas relacionadas a grupos específicos dentro da organização. Essa separação de trabalho ajuda a manter os padrões e fluxos de trabalho, e ajuda a controlar alterar na organização.

O nível mais alto de permissões de divisão é a separação de gerenciamento de Exchange e Active Directory. Muitas organizações têm dois grupos: administradores que gerenciam a infra-estrutura de Exchange da organização, incluindo servidores e destinatários e os administradores que gerenciam a infra-estrutura de Active Directory. Este é uma separação importante para muitas organizações porque a infraestrutura de Active Directory geralmente abrange muitos locais, domínios, serviços, aplicativos e até mesmo as florestas de Active Directory. os administradores Active Directory devem assegurar que as alterações feitas em Active Directory não afetem negativamente nenhum outro serviço. Como resultado, normalmente um pequeno grupo de administradores tem permissão para gerenciar o que a infra-estrutura.

Ao mesmo tempo, a infraestrutura de Exchange, incluindo servidores e destinatários, também pode ser complexa e exige conhecimento especializado. Além disso, o Exchange armazena informações extremamente confidenciais sobre os negócios da organização. os administradores Exchange potencialmente podem acessar essas informações. Limitando o número de Exchange administradores, os limites de organização que pode fazer alterações à configuração de Exchange e quem pode acessar informações confidenciais.

Permissões de divisão geralmente fazer uma distinção entre a criação de entidades de segurança no Active Directory, como usuários e grupos de segurança e a configuração subsequente desses objetos. Isso ajuda a reduzir a chance de acesso não autorizado à rede por meio do controle quem pode criar objetos que concedem acesso a ele. A maioria dos administradores Active Directory frequentemente somente pode criar entidades de segurança, enquanto outros administradores, como os administradores Exchange, pode gerenciar atributos específicos nos objetos de Active Directory existentes.

Para atender as necessidades variadas para separar o gerenciamento de Exchange e Active Directory, o Exchange 2013 permite que você escolha se deseja que um modelo de permissões compartilhadas ou um modelo de permissões divididas. Exchange 2013 oferece dois tipos de modelos de permissões de divisão: RBAC e Active Directory. padrões de Exchange 2013 em um modelo de permissões compartilhadas.

**Sumário**

Explicação da função com base em Active Directory e controle de acesso

Permissões compartilhadas

Permissões de divisão

Permissões de divisão de RBAC

Permissões de divisão do Active Directory

## Explicação da função com base em Active Directory e controle de acesso


Para entender as permissões de divisão, você precisa entender como o modelo de permissões de controle de acesso com base da função (RBAC) no Exchange 2013 funciona com Active Directory. Os controles de modelo RBAC quem pode executar as ações e em quais objetos essas ações podem ser executadas. Para obter mais informações sobre os vários componentes do RBAC são abordadas neste tópico, consulte [Controle de acesso baseado em função de compreensão](understanding-role-based-access-control-exchange-2013-help.md).

Em Exchange 2013, todas as tarefas que são executadas em objetos Exchange devem ser realizadas por meio de Exchange Shell de gerenciamento ou a interface do Centro de administração (EAC) Exchange. Ambos dessas ferramentas de gerenciamento usam o RBAC para autorizar todas as tarefas que são executadas.

RBAC é um componente que existe em cada servidor executando o Exchange 2013. RBAC verifica se o usuário que está executando uma ação está autorizado a fazer isso:

  - Se o usuário não está autorizado a executar a ação, RBAC não permite a ação continuar.

  - Se o usuário está autorizado a executar a ação, RBAC verifica se o usuário está autorizado a executar a ação contra o objeto específico que está sendo solicitada:
    
      - Se o usuário for autorizado, o RBAC permite que a ação continuar.
    
      - Se o usuário não está autorizado, RBAC não permite a ação continuar.

Se o RBAC permite que uma ação continuar, a ação é executada no contexto do Exchange do subsistema confiável e não o contexto do usuário. Exchange do subsistema confiável é um grupo de segurança universal com altos privilégios (USG) que tenha acesso de leitura/gravação para cada Exchange-objeto relacionado na organização Exchange. Também é membro do grupo de segurança local Administradores e Exchange USG de permissões do Windows, que permite Exchange criar e gerenciar objetos de Active Directory.


> [!CAUTION]
> Não faça as alterações manualmente para a associação do grupo de segurança Exchange subsistema confiável. Além disso, não adicioná-lo ao ou removê-lo da listas de controle de acesso (ACLs) do objeto. Fazendo alterações Exchange USG do subsistema confiável sozinho, você poderá causar dano irreparável à sua organização Exchange.



É importante entender que não importa quais permissões Active Directory um usuário tem quando usando as ferramentas de gerenciamento de Exchange. Se o usuário for autorizado, por meio de RBAC, para executar uma ação nas ferramentas de gerenciamento de Exchange, o usuário pode executar a ação independentemente das permissões de Active Directory seu. De modo oposto, se um usuário é um administrador da empresa no Active Directory, mas não está autorizado a executar uma ação, como criar uma caixa de correio, no Exchange ferramentas de gerenciamento, a ação não terá êxito porque o usuário não tem as permissões necessárias de acordo com o RBAC.


> [!IMPORTANT]
> Embora o modelo de permissões de RBAC não se aplica à ferramenta de gerenciamento de computadores e Active Directory usuários, Active Directory usuários e computadores não é possível gerenciar a configuração de Exchange. Então embora um usuário pode ter acesso ao modificar alguns atributos em objetos de Active Directory, tais como o nome de exibição de um usuário, o usuário deve usar as ferramentas de gerenciamento de Exchange e, portanto, deve ser autorizado pelo RBAC, para gerenciar os atributos de Exchange.



Voltar ao início

## Permissões compartilhadas

O modelo de permissões compartilhadas é o modelo padrão para Exchange 2013. Você não precisará alterar nada se este for o modelo de permissões que você deseja usar. Este modelo não separa o gerenciamento de objetos Exchange e Active Directory a partir das ferramentas de gerenciamento de Exchange. Ele permite que os administradores usando as ferramentas de gerenciamento de Exchange para criar entidades de segurança no Active Directory.

A tabela a seguir mostra as funções que permitem a criação de entidades de segurança no Exchange e os grupos de função de gerenciamento que estiver atribuídos por padrão.

### Funções de gerenciamento de entidade de segurança

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Função de gerenciamento</th>
<th>Grupo de função</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="mail-recipient-creation-role-exchange-2013-help.md">Função de criação de destinatário do email</a></p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gerenciamento da Organização</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Gerenciamento de Destinatários</a></p></td>
</tr>
<tr class="even">
<td><p><a href="security-group-creation-and-membership-role-exchange-2013-help.md">Criação de grupos de segurança e a associação de função</a></p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gerenciamento da Organização</a></p></td>
</tr>
</tbody>
</table>


Somente os grupos de função, usuários ou USGs atribuídos à função de criação de destinatário de email podem criar entidades de segurança como usuários Active Directory. Por padrão, os grupos de função Gerenciamento da Organização e Gerenciamento de Destinatários são atribuídos a essa função. Portanto, os membros desses grupos de função podem criar entidades de segurança.

Somente os grupos de função, usuários ou USGs atribuídos à função de criação de grupos de segurança e a associação podem criar grupos de segurança ou gerenciar suas associações. Por padrão, o grupo de funções Gerenciamento da Organização é atribuído a essa função. Portanto, somente os membros do grupo de funções Gerenciamento da Organização podem criar ou gerenciar a associação de grupos de segurança.

Você pode atribuir a função de criação de destinatário de email e a função de criação de grupos de segurança e a associação a outros grupos de função, usuários ou USGs se quiser que outros usuários possam criar entidades de segurança.

Para habilitar o gerenciamento de entidades de segurança existente no Exchange 2013, função destinatários de email é atribuída aos grupos de função Gerenciamento da Organização e Gerenciamento de Destinatários por padrão. Somente os grupos de função, usuários ou USGs atribuídos à função de destinatários de email podem gerenciar as entidades de segurança existente. Se desejar que outros grupos de função, usuários ou USGs possam gerenciar as entidades de segurança existente, você deve atribuir a função destinatários de email para eles.

Para obter mais informações sobre como adicionar funções a grupos de função, usuários ou USGs, consulte os tópicos a seguir:

  - [Gerenciar grupos de função](manage-role-groups-exchange-2013-help.md)

  - [Adicionar uma função a um usuário ou USG](add-a-role-to-a-user-or-usg-exchange-2013-help.md)

Se você alternou para um modelo de permissões divididas e deseja alterar para um modelo de permissões compartilhadas, consulte [Configurar o Exchange 2013 para permissões compartilhadas](configure-exchange-2013-for-shared-permissions-exchange-2013-help.md).

Voltar ao início

## Permissões de divisão

Se sua organização separa o gerenciamento de Exchange e Active Directory, você precisará configurar Exchange para suportar o modelo de permissões de divisão. Quando configurado corretamente, somente os administradores que você deseja criar objetos de segurança, como os administradores Active Directory, poderá fazê-lo e apenas os administradores Exchange poderá modificar os atributos de Exchange em entidades de segurança existente. Essa divisão de permissões também cai aproximadamente juntamente com as linhas das partições de domínio e a configuração em Active Directory. Partições também são chamadas de contextos de nomenclatura. A partição de domínio armazena os usuários, grupos e outros objetos para um domínio específico. Partição de configuração armazena as informações de configuração de toda a floresta para os serviços que usado Active Directory, como Exchange. Dados que estão armazenados na partição de domínio normalmente são gerenciados por administradores Active Directory, embora os objetos que podem conter Exchange-atributos específicos que podem ser gerenciados pelos administradores Exchange. Dados que estão armazenados na partição de configuração são gerenciados por administradores para cada serviço respectivo que armazena os dados nesta partição. Para Exchange, esse é normalmente Exchange administradores.

Exchange 2013 suporta os dois seguintes tipos de permissões de divisão:

  - **Permissões de divisão de RBAC**   Permissões para criar objetos de segurança na partição de domínio Active Directory são controladas pela RBAC. Somente Exchange servidores, serviços e aqueles que são membros dos grupos de função adequada podem criar entidades de segurança.

  - **Permissões de divisão do Active Directory**   Permissões para criar objetos de segurança na partição de domínio Active Directory completamente são removidas do qualquer usuário Exchange, serviço ou servidor. Nenhuma opção é fornecida no RBAC para criar entidades de segurança. Criação de entidades de segurança no Active Directory deve ser executada usando as ferramentas de gerenciamento de Active Directory.
    

    > [!IMPORTANT]
    > Embora Active Directory dividir permissões podem ser habilitadas ou desabilitadas executando a instalação em um computador que tenha o Exchange 2013 instalado, divisão Active Directory configuração de permissões se aplicará aos servidores Exchange 2013 e o Exchange 2010. Impacto no entanto, não, é necessário nos servidores do Microsoft Exchange Server 2007.



Se sua organização optar por usar um modelo de permissões divididas em vez de permissões compartilhadas, recomendamos que você use o modelo de permissões de divisão RBAC. O modelo de permissões de divisão RBAC fornece significativamente mais flexibilidade fornecendo a separação de administração quase mesmo como Active Directory dividir permissões, com exceção de que Exchange os servidores e serviços podem criar entidades de segurança no RBAC modelo de permissões divididas.

Você será solicitado se deseja habilitar Active Directory dividir permissões durante a instalação. Se você optar por habilitar Active Directory dividir permissões, você só pode alterar para permissões compartilhadas ou RBAC dividir permissões executando novamente o programa de instalação e desabilitar Active Directory dividir permissões. Essa opção se aplica a todos os servidores de Exchange 2010 e Exchange 2013 na organização.

As seções a seguir descrevem RBAC e Active Directory dividir permissões em mais detalhes.

Voltar ao início

## Permissões de divisão de RBAC

O modelo de segurança RBAC modifica as atribuições de funções de gerenciamento padrão para separar quem pode criar entidades de segurança na partição de domínio Active Directory daquelas que administram os dados da organização Exchange na partição de configuração Active Directory. Entidades de segurança, como os usuários com caixas de correio e grupos de distribuição, podem ser criadas por administradores que sejam membros da criação de destinatário de email e criação de grupos de segurança e a associação de funções. Essas permissões permanecerão separadas das permissões necessárias para criar objetos de segurança fora o Exchange ferramentas de gerenciamento. os administradores de Exchange que não foram atribuídos a criação de destinatário do email ou funções de criação de grupos de segurança e a associação ainda podem modificar a Exchange-relacionados atributos de entidades de segurança. os administradores Active Directory também tem a opção de usar as ferramentas de gerenciamento de Exchange para criar Active Directory entidades de segurança.

servidores Exchange e o Exchange o subsistema confiável também têm permissões para criar entidades de segurança no Active Directory em nome de usuários e programas de terceiros que integram com o RBAC.

Dividir permissões de RBAC é uma boa opção para sua organização se as seguintes condições forem verdadeiras:

  - Sua organização não exige que a criação de entidade de segurança ser realizadas usando apenas as ferramentas de gerenciamento Active Directory e apenas por usuários que receberam permissões específicas Active Directory.

  - A organização permite que os serviços, como servidores de Exchange, para criar entidades de segurança.

  - Você deseja simplificar o processo necessário para criar caixas de correio, usuários habilitados para email, grupos de distribuição e grupos de função, permitindo sua criação a partir do Exchange ferramentas de gerenciamento.

  - Você deseja gerenciar a associação de grupos de distribuição e grupos de função dentro das ferramentas de gerenciamento de Exchange.

  - Você tem programas de terceiros que exigem que os servidores de Exchange ser capazes de criar objetos de segurança em nome deles.

Se sua organização requer uma separação completa de administração Exchange e Active Directory onde nenhuma administração Active Directory pode ser executada usando as ferramentas de gerenciamento de Exchange ou pelos serviços de Exchange, consulte a seção Permissões de divisão do Active Directory mais adiante neste tópico.

Troca de permissões compartilhadas para dividir permissões de RBAC é um processo manual, onde você pode remover as permissões necessárias para criar objetos de segurança dos grupos de função que recebem por padrão. A tabela a seguir mostra as funções que permitem a criação de entidades de segurança no Exchange e os grupos de função de gerenciamento que estiver atribuídos por padrão.

### Funções de gerenciamento de entidade de segurança

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Função de gerenciamento</th>
<th>Grupo de função</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="mail-recipient-creation-role-exchange-2013-help.md">Função de criação de destinatário do email</a></p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gerenciamento da Organização</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Gerenciamento de Destinatários</a></p></td>
</tr>
<tr class="even">
<td><p><a href="security-group-creation-and-membership-role-exchange-2013-help.md">Criação de grupos de segurança e a associação de função</a></p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gerenciamento da Organização</a></p></td>
</tr>
</tbody>
</table>


Por padrão, membros dos grupos de função de Gerenciamento da Organização e Gerenciamento de Destinatários podem criar entidades de segurança. Você deve transferir a capacidade de criar entidades de segurança dos grupos de função internos para um novo grupo de função que você criar.

Para configurar permissões de divisão de RBAC, faça o seguinte:

1.  Desabilite permissões de divisão de Active Directory se estivesse habilitada.

2.  Crie um grupo de função, que conterá os administradores Active Directory que poderão criar entidades de segurança.

3.  Crie as atribuições de função comuns e de delegação entre a função de criação de destinatário de email e o novo grupo de função.

4.  Crie as atribuições de função comuns e de delegação entre a função de criação de grupos de segurança e a associação e o novo grupo de função.

5.  Remova o regulares e delegando atribuições de função de gerenciamento entre a função de criação de destinatário de email e os grupos de função Gerenciamento da Organização e Gerenciamento de Destinatários.

6.  Remova o regulares e delegando atribuições de função entre a função de criação de grupos de segurança e a associação e o grupo de funções Gerenciamento da Organização.

Depois de fazer isso, somente os membros do novo grupo de função que você criar será capazes de criar objetos de segurança, como caixas de correio. O novo grupo só poderá criar os objetos. Ele não será capaz de configurar os atributos de Exchange no novo objeto. Administrador Active Directory, que é membro do novo grupo, será necessário criar o objeto e, em seguida, um administrador Exchange precisará configurar os atributos de Exchange no objeto. os administradores Exchange não conseguirá usar os seguintes cmdlets:

  - **New-Mailbox**

  - **New-MailContact**

  - **New-MailUser**

  - **New-RemoteMailbox**

  - **Remove-Mailbox**

  - **Remove-MailContact**

  - **Remove-MailUser**

  - **Remove-RemoteMailbox**

Exchange os administradores, no entanto, serão capazes de criar e gerenciar Exchange-específicas objetos, como regras de transporte, grupos de distribuição e assim por diante e gerenciar Exchange-relacionados atributos em qualquer objeto.

Além disso, os recursos associados no EAC e Outlook Web App, como o novo Assistente de caixa de correio, também não ficarão mais disponíveis ou irá gerar um erro se você tentar usá-los.

Se desejar que o novo grupo de função também sejam capazes de gerenciar os atributos de Exchange no novo objeto, função destinatários de email também deve ser atribuído ao novo grupo de função.

Para obter mais informações sobre como configurar um modelo de permissões divididas, consulte [Configure o Exchange 2013 para permissões de divisão](configure-exchange-2013-for-split-permissions-exchange-2013-help.md).

Voltar ao início

## Permissões de divisão do Active Directory

Com Active Directory dividir permissões, a criação de entidades de segurança na partição de domínio Active Directory, como caixas de correio e grupos de distribuição deve ser executada usando as ferramentas de gerenciamento de Active Directory. Várias alterações são feitas nas permissões concedidas para os servidores de subsistema confiável e ExchangeExchange para limitar o que os administradores Exchange e servidores podem fazer. As seguintes alterações na funcionalidade ocorrerem quando você habilita Active Directory dividir permissões:

  - Criação de caixas de correio, usuários habilitados para email, grupos de distribuição e outras entidades de segurança é removida das ferramentas de gerenciamento de Exchange.

  - Adicionando e removendo membros do grupo de distribuição não podem ser feitas a partir das ferramentas de gerenciamento de Exchange.

  - Todas as permissões concedidas para os servidores de subsistema confiável e ExchangeExchange para criar entidades de segurança serão removidas.

  - servidores de Exchange e as ferramentas de gerenciamento de Exchange só podem modificar os atributos de Exchange de entidades de segurança existente no Active Directory.

Por exemplo, para criar uma caixa de correio com Active Directory permissões de divisão habilitadas, um usuário deve primeiro ser criado usando as ferramentas de Active Directory por um usuário com as permissões necessárias Active Directory. Em seguida, o usuário pode ser usando as ferramentas de gerenciamento de Exchange habilitado para caixa de correio. Somente o Exchange-relacionados atributos da caixa de correio que podem ser modificados por administradores de Exchange usando as ferramentas de gerenciamento de Exchange.

Active Directory dividir permissões é uma boa opção para sua organização se as seguintes condições forem verdadeiras:

  - Sua organização requer que as entidades de segurança ser criados com as ferramentas de gerenciamento Active Directory ou apenas por usuários que são concedidos permissões específicas no Active Directory.

  - Você deseja separar completamente a capacidade de criar entidades de segurança daquelas que gerenciam a organização Exchange.

  - Você deseja executar todas as gerenciamento do grupo de distribuição, incluindo a criação de grupos de distribuição e adicionando e removendo membros desses grupos, usando as ferramentas de gerenciamento de Active Directory.

  - Você não quer Exchange servidores ou programas de terceiros que usam Exchange em nome para criar objetos de segurança.


> [!IMPORTANT]
> Alternando Active Directory dividir permissões é uma opção que você pode fazer quando você instala o Exchange 2013 usando o Assistente de instalação ou usando o parâmetro <EM>ActiveDirectorySplitPermissions</EM> enquanto executa <CODE>setup.exe</CODE> da linha de comando. Também é possível habilitar ou desabilitar Active Directory dividir permissões após ter instalado Exchange 2013 executando novamente <CODE>setup.exe</CODE> da linha de comando. Para habilitar Active Directory dividir permissões, defina o parâmetro <EM>ActiveDirectorySplitPermissions</EM> para <CODE>true</CODE>. Para desativá-la, defina-o para <CODE>false</CODE>. Você sempre deve especificar a opção <EM>PrepareAD</EM> juntamente com o parâmetro <EM>ActiveDirectorySplitPermissions</EM> .<BR>Se você tiver vários domínios dentro da mesma floresta, você também deve especificar a opção <EM>PrepareAllDomains</EM> quando você aplica Active Directory dividir permissões ou executar a instalação com a opção <EM>PrepareDomain</EM> em cada domínio. Se você optar por executar a instalação com a opção <EM>PrepareDomain</EM> em cada domínio em vez de usar a opção <EM>PrepareAllDomains</EM> , você deve preparar todos os domínios que contém servidores Exchange, objetos habilitados para email ou servidores de catálogo global que possa ser acessados por um servidor Exchange.




> [!IMPORTANT]
> Não será possível habilitar Active Directory dividir permissões se você instalou Exchange 2010 ou Exchange 2013 em um controlador de domínio.<BR>Depois de habilitar ou desabilitar Active Directory dividir permissões, é recomendável que você reinicie os servidores Exchange 2010 e Exchange 2013 na sua organização para impor o pegue o novo token de acesso de Active Directory com as permissões atualizadas.



Exchange 2013 atinge Active Directory permissões de divisão, removendo permissões e membros do grupo de segurança de permissões de ExchangeWindows. Este grupo de segurança, em permissões compartilhadas e permissões de divisão RBAC, recebe permissões para muitos não -Exchange objetos e atributos em toda a Active Directory. Removendo as permissões e a associação a este grupo de segurança, serviços e Exchange administradores são impedidos de criar ou modificar os objetos deActive Directory não -Exchange.

Para obter uma lista das alterações que ocorrem para o grupo de segurança de permissões deWindowsExchange e outros componentes Exchange quando você ativar ou desativar Active Directory dividir permissões, consulte a tabela a seguir.


> [!NOTE]
> Atribuições de função a grupos de funções que permitem que administradores Exchange criar objetos de segurança são removidas quando Active Directory dividir permissões está habilitado. Isso é feito para remover o acesso aos cmdlets que, caso contrário, poderia gerar um erro quando são executados, porque eles não têm permissões para criar o objeto associado Active Directory.



### Alterações de permissões de divisão do Active Directory

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Ação</th>
<th>Alterações feitas pelo Exchange</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Habilitar Active Directory dividida permissões durante a primeira instalação do servidor Exchange 2013</p></td>
<td><p>Acontece o seguinte quando você habilita Active Directory dividir permissões por meio do Assistente de instalação ou executando <code>setup.exe</code> com os parâmetros <code>/PrepareAD</code> e <code>/ActiveDirectorySplitPermissions:true</code> :</p>
<ul>
<li><p>Uma unidade organizacional (UO) chamada <strong>Grupos protegido do Microsoft Exchange</strong> é criada.</p></li>
<li><p>O grupo de segurança de <strong>Permissões do Exchange Windows</strong> é criado nos <strong>Grupos do Microsoft Exchange protegido</strong> UO.</p></li>
<li><p>O grupo de segurança de <strong>Subsistema confiável do Exchange</strong> não será adicionado ao grupo de segurança de <strong>Permissões do Exchange Windows</strong>.</p></li>
<li><p>Criação não delegando gerenciamento de atribuições de função às funções de gerenciamento com os seguintes tipos de função de gerenciamento é ignorada:</p>
<ul>
<li><p><code>MailRecipientCreation</code></p></li>
<li><p><code>SecurityGroupCreationandMembership</code></p></li>
</ul></li>
<li><p>Entradas de controle de acesso (ACEs) que seriam tiverem sido atribuídas ao grupo de segurança de <strong>Permissões do Exchange Windows</strong> não são adicionadas ao objeto de domínio Active Directory.</p></li>
</ul>
<p>Se você executar a instalação com a opção <em>PrepareAllDomains</em> ou <em>PrepareDomain</em> , acontece o seguinte em cada domínio filho que está preparado:</p>
<ul>
<li><p>Todas as ACEs atribuídas ao grupo de segurança do <strong>Exchange permissões do Windows</strong> são removidas do objeto de domínio.</p></li>
<li><p>ACEs são definidas em cada domínio com a exceção qualquer ACEs atribuído ao grupo de segurança do <strong>Exchange permissões do Windows</strong>.</p></li>
</ul>
<p></p></td>
</tr>
<tr class="even">
<td><p>Alternar de permissões compartilhadas ou dividir permissões para Active Directory dividir permissões de RBAC</p></td>
<td><p>Acontece o seguinte quando você executa o comando <code>setup.exe</code> com os parâmetros <code>/PrepareAD</code> e <code>/ActiveDirectorySplitPermissions:true</code> :</p>
<ul>
<li><p>Uma unidade Organizacional chamada <strong>Grupos protegido do Microsoft Exchange</strong> é criada.</p></li>
<li><p>O grupo de segurança de <strong>Permissões do Exchange Windows</strong> é movido para a UO dos grupos <strong>Protegido do Microsoft Exchange</strong>.</p></li>
<li><p>O grupo de segurança de <strong>Subsistema confiável do Exchange</strong> é removido do grupo de segurança do <strong>Exchange permissões do Windows</strong>.</p></li>
<li><p>Quaisquer atribuições de função não delegando às funções de gerenciamento com os seguintes tipos de função são removidas:</p>
<ul>
<li><p><code>MailRecipientCreation</code></p></li>
<li><p><code>SecurityGroupCreationandMembership</code></p></li>
</ul></li>
<li><p>Todas as ACEs atribuídas ao grupo de segurança do <strong>Exchange permissões do Windows</strong> são removidas do objeto de domínio.</p></li>
</ul>
<p>Se você executar a instalação com qualquer um a opção <em>PrepareAllDomains</em> ou <em>PrepareDomain</em> , acontece o seguinte em cada domínio filho que está preparado:</p>
<ul>
<li><p>Todas as ACEs atribuídas ao grupo de segurança do <strong>Exchange permissões do Windows</strong> são removidas do objeto de domínio.</p></li>
<li><p>ACEs são definidas em cada domínio com a exceção qualquer ACEs atribuído ao grupo de segurança do <strong>Exchange permissões do Windows</strong>.</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Alternar entre Active Directory dividir permissões para permissões compartilhadas ou as permissões de divisão RBAC</p></td>
<td><p>Acontece o seguinte quando você executa o comando <code>setup.exe</code> com os parâmetros <code>/PrepareAD</code> e <code>/ActiveDirectorySplitPermissions:false</code> :</p>
<ul>
<li><p>O grupo de segurança de <strong>Permissões do Exchange Windows</strong> é movido para os <strong>Grupos de segurança do Microsoft Exchange</strong> UO.</p></li>
<li><p>A UO de <strong>Grupos do Microsoft Exchange protegido</strong> foi removida.</p></li>
<li><p>O grupo de segurança <strong>Subsistemas confiáveis do Exchange</strong> é adicionado ao grupo de segurança de <strong>Permissões do Exchange Windows</strong>.</p></li>
<li><p>ACEs são adicionadas ao objeto de domínio para o grupo de segurança de <strong>Permissões do Exchange Windows</strong>.</p></li>
</ul>
<p>Se você executar a instalação com qualquer um a opção <em>PrepareAllDomains</em> ou <em>PrepareDomain</em> , acontece o seguinte em cada domínio filho que está preparado:</p>
<ul>
<li><p>ACEs são adicionadas ao objeto de domínio para o grupo de segurança de <strong>Permissões do Exchange Windows</strong>.</p></li>
<li><p>ACEs são definidas em cada domínio incluindo ACEs atribuídos ao grupo de segurança do <strong>Exchange permissões do Windows</strong>.</p></li>
</ul>
<p>Atribuições de função para a criação de destinatário de email e criação de grupos de segurança e funções de associação não são criadas automaticamente quando a troca de Active Directory dividida para permissões compartilhadas. Se as atribuições de função de delegação foram personalizadas antes da Active Directory dividir permissões que está sendo habilitadas, as personalizações permanecem intactas. Para criar as atribuições de função entre essas funções e o grupo de funções Gerenciamento da Organização, consulte <a href="configure-exchange-2013-for-shared-permissions-exchange-2013-help.md">Configurar o Exchange 2013 para permissões compartilhadas</a>.</p></td>
</tr>
</tbody>
</table>


Após habilitar Active Directory dividir permissões, os cmdlets a seguir não estão mais disponíveis:

  - **New-Mailbox**

  - **New-MailContact**

  - **New-MailUser**

  - **New-RemoteMailbox**

  - **Remove-Mailbox**

  - **Remove-MailContact**

  - **Remove-MailUser**

  - **Remove-RemoteMailbox**

Após habilitar Active Directory dividir permissões, os cmdlets a seguir são acessíveis, mas você não pode usá-los para criar grupos de distribuição ou modificar a associação de grupo de distribuição:

  - **Add-DistributionGroupMember**

  - **New-DistributionGroup**

  - **Remove-DistributionGroup**

  - **Remove-DistributionGroupMember**

  - **Update-DistributionGroupMember**

Alguns cmdlets, embora ainda está disponível, podem oferecer apenas uma funcionalidade limitada quando usado com Active Directory dividir permissões. Isso acontece porque elas podem permitir que você configure objetos de destinatário que estão na partição do domínio Active Directory e Exchange objetos de configuração que estão na partição configuração Active Directory. Eles também permitem que você configure Exchange-relacionados atributos nos objetos armazenados na partição de domínio. Tenta usar os cmdlets para criar objetos ou modificar não -Exchange-relacionados atributos nos objetos, na partição de domínio resultará em erro. Por exemplo, o cmdlet **Add-ADPermission** retornará um erro se você tentar adicionar permissões a uma caixa de correio. No entanto, o cmdlet **Add-ADPermission** terá êxito se você configurar permissões em um conector de recebimento. Isso ocorre porque uma caixa de correio é armazenada na partição de domínio, enquanto os conectores de recebimento são armazenados na partição de configuração.

Além disso, os recursos associados em Exchange Centro de administração e o Outlook Web App, como o Assistente de nova caixa de correio, também não ficarão mais disponíveis ou irá gerar um erro se você tentar usá-los.

Exchange os administradores, no entanto, serão capazes de criar e gerenciar Exchange-objetos específicos, como regras de transporte e assim por diante.

Para obter mais informações sobre como configurar um Active Directory modelo de permissões divididas, consulte [Configure o Exchange 2013 para permissões de divisão](configure-exchange-2013-for-split-permissions-exchange-2013-help.md).

Voltar ao início

