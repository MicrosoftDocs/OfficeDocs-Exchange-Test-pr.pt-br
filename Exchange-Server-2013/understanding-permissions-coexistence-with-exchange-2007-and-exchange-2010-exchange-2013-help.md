---
title: 'Noções básicas sobre coexistência de permissões no Exchange 2007 e 2010'
TOCTitle: Noções básicas sobre a coexistência de permissões com o Exchange 2007 e Exchange 2010
ms:assetid: 28ab1433-23ee-4914-8f21-9a32578792e5
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Dd335157(v=EXCHG.150)
ms:contentKeyID: 54913442
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Noções básicas sobre a coexistência de permissões com o Exchange 2007 e Exchange 2010

 

_**Aplica-se a:** Exchange Server 2010 Service Pack 2 (SP2), Exchange Server 2013_

_**Tópico modificado em:** 2015-04-07_

Quando você instala o Microsoft Exchange Server 2013 em uma organização existente do Microsoft Exchange Server 2010 ou do Microsoft Exchange Server 2007, é necessário entender como as permissões funcionarão na nova organização. Leia a seção abaixo que se aplica à sua organização.

  - Installing Exchange 2013 into an existing Exchange 2010 organization

  - Installing Exchange 2013 into an existing Exchange 2007 organization

## Instalação do Exchange 2013 em uma organização do Exchange 2010 existente

Exchange 2013 usa o mesmo modelo de permissões de controle de acesso com base da função (RBAC) que é usado em Exchange 2010. Quando você instala o Exchange 2013 em uma organização existente do Exchange 2010, o mesmo grupos de funções de gerenciamento, funções de gerenciamento e escopos de gerenciamento se aplicam ao servidores Exchange 2013 e Exchange 2010 e destinatários. Membros de grupos de função ou usuários atribuídos às funções, podem administrar qualquer servidor Exchange 2013 ou Exchange 2013 ou um destinatário que está incluído no escopo da função ou grupo de função. Se você não usar escopos em sua organização, e você deseja que os membros de seus grupos de função existente para gerenciar destinatários e servidores Exchange 2010 e Exchange 2013, você não precisa fazer qualquer outra coisa. Os administradores poderão gerenciar servidores Exchange 2013 e destinatários que são adicionados à organização. Se você precisar de um lembrete em como as permissões funcionam no Exchange 2010 e Exchange 2013, consulte [Permissões](permissions-exchange-2013-help.md).

Na nova organização, convém separar a administração dos servidores e destinatários do Exchange 2010 e do Exchange 2013. Talvez o grupo de administradores responsáveis por administrar os servidores e destinatários do Exchange 2010 não tenham permissão para administrar os servidores e destinatários do Exchange 2013, e vice-versa. Nesse caso, você pode usar os escopos de gerenciamento para definir os servidores e destinatários que cada grupo de administradores pode gerenciar. Depois de criar os escopos que você quiser, copie os grupos de função existentes, adicione os administradores que devem ser membro de cada um e adicione os escopos a esses grupos de função. Depois de concluir, os membros de cada grupo de funções poderão administrar apenas os servidores e destinatários que correspondem aos seus respectivos escopos.

Para obter mais informações sobre os grupos de função, escopos, cópia dos grupos de função e adição dos escopos aos grupos de função, consulte os seguintes tópicos:

  - [Gerenciar grupos de função](manage-role-groups-exchange-2013-help.md)

  - [Criar um escopo regular ou exclusivo](create-a-regular-or-exclusive-scope-exchange-2013-help.md)

  - [Noções básicas sobre grupos de funções de gerenciamento](understanding-management-role-groups-exchange-2013-help.md)

  - [Noções básicas sobre escopos da função de gerenciamento](understanding-management-role-scopes-exchange-2013-help.md)

## Instalação do Exchange 2013 em uma organização do Exchange 2007 existente

Exchange 2013 inclui permissões RBAC (Controle de Acesso com Base em Função) que substituem o modelo de autorização baseado em ACE (entrada de controle de acesso) do Active Directory usado no Microsoft Exchange Server 2007. O RBAC é o mecanismo de autorização usado para a maior parte do gerenciamento do Exchange 2013. Esse mecanismo inclui as seguintes áreas de gerenciamento:

  - Shell de Gerenciamento do Exchange

  - Centro de administração do Exchange (EAC)

  - Serviços Web do Exchange

Para mais informações sobre como planejar a coexistência entre o Exchange 2013 e o Exchange 2007, consulte [Atualização do Exchange 2007 para o Exchange 2013](upgrade-from-exchange-2007-to-exchange-2013-exchange-2013-help.md).

Procurando tarefas de gerenciamento relacionadas a permissões? Consulte [Permissões](permissions-exchange-2013-help.md).

## Permissões do Exchange 2013

O modelo de permissões RBAC do Exchange 2013 consiste em grupos de funções de gerenciamento aos quais foram atribuídas várias funções de gerenciamento. As funções de gerenciamento contêm permissões que possibilitam aos administradores a execução de tarefas na organização do Exchange. Os administradores são adicionados como membros dos grupos de funções e recebem todas as permissões fornecidas pelas funções. A tabela a seguir fornece um exemplo dos grupos de funções, algumas das funções que foram atribuídas a eles e uma descrição do tipo de usuário que poderia ser um membro do grupo de funções.

### Exemplos de grupos de funções e funções no Exchange 2013

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Grupo de funções de gerenciamento</th>
<th>Funções de gerenciamento</th>
<th>Membros deste grupo de funções</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Gerenciamento da Organização</p></td>
<td><p>Algumas das funções atribuídas a este grupo de funções são mostradas a seguir:</p>
<ul>
<li><p>Listas de Endereços</p></li>
<li><p>Servidores Exchange</p></li>
<li><p>Registro no diário</p></li>
<li><p>Destinatários de Email</p></li>
<li><p>Pastas Públicas</p></li>
</ul></td>
<td><p>Os usuários que gerenciam toda a organização do Exchange 2013 devem ser membros deste grupo de funções. Com algumas exceções, os membros deste grupo de funções conseguem gerenciar praticamente todos os aspectos da organização do Exchange 2013.</p>
<p>Por padrão, a conta de usuário usada para preparar o Active Directory para o Exchange 2013 é um membro deste grupo de funções.</p>
<p>Para mais informações sobre este grupo de funções, além de uma lista completa das funções atribuídas a este grupo de funções, consulte <a href="organization-management-exchange-2013-help.md">Gerenciamento da Organização</a>.</p></td>
</tr>
<tr class="even">
<td><p>Gerenciamento de Organizações Somente Exibição</p></td>
<td><p>As funções atribuídas a esse grupo de funções são mostradas a seguir:</p>
<ul>
<li><p>Monitoramento</p></li>
<li><p>Configuração Somente para Exibição</p></li>
<li><p>Destinatários Somente para Exibição</p></li>
</ul></td>
<td><p>Os usuários que veem a configuração de toda a organização do Exchange 2013 devem ser membros deste grupo de funções. Estes usuários devem conseguir visualizar as configurações do servidor e as informações do destinatário, além de executar as funções de gerenciamento sem a habilidade de alterar a configuração da organização ou do destinatário.</p>
<p>Para mais informações sobre este grupo de funções, consulte <a href="view-only-organization-management-exchange-2013-help.md">Gerenciamento da organização somente exibição</a>.</p></td>
</tr>
<tr class="odd">
<td><p>Gerenciamento de Destinatários</p></td>
<td><p>As funções atribuídas a esse grupo de funções são mostradas a seguir:</p>
<ul>
<li><p>Grupos de distribuição</p></li>
<li><p>Pastas públicas habilitadas para email</p></li>
<li><p>Criação de Destinatário de Email</p></li>
<li><p>Destinatários de Email</p></li>
<li><p>Controle de Mensagens</p></li>
<li><p>Migração</p></li>
<li><p>Mudança de Caixas de Correio</p></li>
<li><p>Diretivas de Destinatário</p></li>
</ul></td>
<td><p>Os usuários que gerenciam destinatários, como caixas de correio, contatos e grupos de distribuição na organização do Exchange 2013, devem ser membros deste grupo de funções. Estes usuários podem criar destinatários, modificar ou excluir destinatários já existentes ou mover caixas de correio.</p>
<p>Para mais informações sobre este grupo de funções, além de uma lista completa das funções atribuídas a este grupo de funções, consulte <a href="recipient-management-exchange-2013-help.md">Gerenciamento de Destinatários</a>.</p></td>
</tr>
<tr class="even">
<td><p>Gerenciamento do Servidor</p></td>
<td><p>Algumas das funções atribuídas a este grupo de funções são mostradas a seguir:</p>
<ul>
<li><p>Bancos de Dados</p></li>
<li><p>Conectores do Exchange</p></li>
<li><p>Servidores Exchange</p></li>
<li><p>Conectores de recebimento</p></li>
<li><p>Filas de Transporte</p></li>
</ul></td>
<td><p>Os usuários que gerenciam a configuração do servidor do Exchange, como conectores de Recebimento, certificados, bancos de dados e diretórios virtuais, devem ser membros deste grupo de funções. Estes usuários conseguem modificar a configuração do servidor do Exchange e criar bancos de dados, além de reiniciar e manipular filas de transporte.</p>
<p>Para mais informações sobre este grupo de funções, além de uma lista completa das funções atribuídas a este grupo de funções, consulte <a href="server-management-exchange-2013-help.md">Gerenciamento de Servidor</a>.</p></td>
</tr>
<tr class="odd">
<td><p>Gerenciamento de Descobertas</p></td>
<td><p>As funções atribuídas a esse grupo de funções são mostradas a seguir:</p>
<ul>
<li><p>Guarda Legal</p></li>
<li><p>Pesquisa de Caixa de Correio</p></li>
</ul></td>
<td><p>Os usuários que realizam pesquisas de caixas de correio, para dar suporte a procedimentos legais ou configurar guardas de documentos, devem ser membros deste grupo de funções.</p>
<p>Este é um exemplo de um grupo de funções que pode conter administradores que não são do Exchange, como os funcionários do departamento jurídico. O pessoal do jurídico pode desempenhar suas funções sem a intervenção de administradores do Exchange.</p>
<p>Para mais informações sobre este grupo de funções, além de uma lista completa das funções atribuídas a este grupo de funções, consulte <a href="discovery-management-exchange-2013-help.md">Gerenciamento de Descobertas</a>.</p></td>
</tr>
</tbody>
</table>


Essa tabela mostra que o Exchange 2013 fornece um nível granular de controle sobre as permissões que você concede aos seus administradores. Você pode escolher entre 12 grupos de funções no Exchange 2013. Para uma lista completa dos grupos de funções e das permissões fornecidas, consulte [Grupos de funções internos](built-in-role-groups-exchange-2013-help.md).

Como Exchange 2013 oferece vários grupos de função e porque ainda mais personalização seja possível criando grupos de função que possuem combinações de função diferentes, a manipulação de controle de acesso ACLs (listas) nos objetos Active Directory não é mais necessário e não tem efeito. ACLs não são usadas para aplicar permissões a administradores individuais ou grupos em Exchange 2013. Todas as tarefas, como um administrador de criação de uma caixa de correio ou de um usuário acesse uma caixa de correio, são gerenciadas pelo RBAC. RBAC autoriza a tarefa e então Exchange realiza a tarefa em nome do usuário se permitido. Exchange realiza a tarefa do grupo de segurança universal de subsistema confiável de Exchange (USG). Com algumas exceções, todas as ACLs em objetos em Active Directory que Exchange 2010 tem para acesso são concedidas aos Exchange USG do subsistema confiável. Esta é uma alteração fundamental de como as permissões são manipuladas em Exchange 2007.

As permissões concedidas a um usuário no Active Directory são separadas das permissões concedidas ao usuário pelo RBAC quando esse usuário está usando as ferramentas de gerenciamento do Exchange 2013.

Para mais informações sobre o RBAC, consulte [Controle de acesso baseado em função de compreensão](understanding-role-based-access-control-exchange-2013-help.md).

## Permissões do Exchange 2007

O modelo administrativo do Exchange 2007 utiliza as florestas do Active Directory para definir os limites de segurança. Não existe nenhum isolamento das permissões de segurança em uma floresta específica. Os proprietários de floresta e os administradores corporativos podem sempre ganhar acesso a todos os recursos em qualquer domínio. No Exchange 2007, pode ser preciso conceder direitos de administrador corporativo e direitos de administrador de domínio de nível superior apenas temporariamente.

O Exchange 2007 fornece as seguintes funções de administrador predefinidas:

  - **Função de Administrador da Organização do Exchange**   Essa função concede permissões para controlar todos os aspectos da organização do Exchange 2007. Além disso, um administrador que tem essa função pode conceder permissões a outros administradores do Exchange. Essa função é concedida à conta que você usa para instalar o Exchange 2007.

  - **Função de Administrador Somente para Exibição do Exchange**   Essa função concede permissões para exibir a configuração do Exchange. Entretanto, um administrador que tem essa função não pode modificar objetos na organização do Exchange 2007.

  - **Função de Administrador de Destinatários do Exchange**   Essa função concede permissões para gerenciar destinatários de email. Um administrador que tem essa função pode modificar itens relacionados ao Exchange para usuários, grupos, contatos e grupos de distribuição.

  - **Função de Administrador de Servidores do Exchange**   Essa função concede permissões para gerenciar um servidor específico. Entretanto, essa função não concede permissões para executar ações que tenham um impacto global na organização do Exchange 2007.

  - **Função de Administrador de Pasta Pública do Exchange**   Essa função foi adicionada no Exchange 2007 Service Pack 1**.** Essa função concede permissões para gerenciar pastas públicas na organização do Exchange 2007.

Esse modelo de permissões usa USGs para todas as funções, exceto para a função de Administrador de Servidor do Exchange. Ao executar o comando Exchange 2007**Setup /PrepareAD**, o programa de Instalação cria os USGs no domínio raiz e apresenta um escopo de toda a floresta aos USGs. Os USGs recebem ACLs para gerenciar objetos do Exchange em todo o Active Directory.

No Exchange 2007, você pode separar administradores atribuindo a eles várias funções. As permissões são atribuídas diretamente ao usuário ou ao USG do qual o usuário é membro. Quaisquer ações realizadas pelo usuário acontecem no contexto da conta do Active Directory desse usuário. A tabela a seguir lista as funções de administrador do Exchange 2007 e as permissões relacionadas do Exchange.

### Funções de administrador do Exchange 2007

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Função de administrador</th>
<th>Membros</th>
<th>Membro de</th>
<th>Permissões do Exchange</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Administrador da organização do Exchange</p></td>
<td><p>A conta Administrador ou a conta usada para instalar o primeiro servidor Exchange 2007</p></td>
<td><p>Administrador de destinatários do Exchange</p>
<p>Grupo local de administradores do <em>&lt;nome do servidor&gt;</em></p></td>
<td><p>Total controle sobre o contêiner do Microsoft Exchange no Active Directory</p></td>
</tr>
<tr class="even">
<td><p>Administrador somente para exibição do Exchange</p></td>
<td><p>Administradores de destinatários do Exchange</p>
<p>Administradores de servidor Exchange (<em>&lt;nome do servidor</em>&gt;)</p></td>
<td><p>Administradores de destinatários do Exchange</p>
<p>Administradores do Exchange Server</p></td>
<td><p>Acesso de leitura ao contêiner do Microsoft Exchange no Active Directory.</p>
<p>Acesso de leitura a todos os domínios do Windows que têm destinatários do Exchange.</p></td>
</tr>
<tr class="odd">
<td><p>Administrador de destinatários do Exchange</p></td>
<td><p>Administradores da organização do Exchange</p></td>
<td><p>Administradores somente para exibição do Exchange</p></td>
<td><p>Total controle sobre propriedades do Exchange nos objetos de usuário do Active Directory</p></td>
</tr>
<tr class="even">
<td><p>Administrador do servidor Exchange</p></td>
<td><p>Administradores da organização do Exchange</p></td>
<td><p>Administradores somente para exibição do Exchange</p>
<p>Grupo local de administradores do <em>&lt;nome do servidor</em>&gt;</p></td>
<td><p>Total controle sobre o Exchange <em>&lt;nome do servidor</em>&gt;</p></td>
</tr>
<tr class="odd">
<td><p>Servidor Exchange</p></td>
<td><p>Cada conta de computador do Exchange 2007</p></td>
<td><p>Administradores somente para exibição do Exchange</p></td>
<td><p>Especial</p></td>
</tr>
<tr class="even">
<td><p>Administrador de pasta pública do Exchange</p></td>
<td><p>Administradores da organização do Exchange</p></td>
<td><p>Administradores somente para exibição do Exchange</p></td>
<td><p>Controle total para gerenciar todas as pastas públicas (concedido o direito estendido Criar pasta pública de nível superior)</p></td>
</tr>
</tbody>
</table>


Se precisar criar atribuições de permissão mais granulares, você poderá modificar as ACLs em objetos do Exchange 2007 individuais, como lista de endereços ou bancos de dados. Você deve adicionar o usuários ou o grupo de segurança de que o usuário é membro diretamente à ACL. Em seguida, as ações são executadas no contexto de um usuário específico.

Para mais informações sobre como gerenciar permissões no Exchange 2007, consulte [Configurando permissões no Exchange Server 2007](http://go.microsoft.com/fwlink/?linkid=90671).

## Permissões de coexistência do Exchange 2013 e do Exchange 2007

Como os modelos de permissões do Exchange 2013 e do Exchange 2007 são diferentes, as atribuições de permissão do Exchange 2013 são separadas das atribuições de permissão do Exchange 2007. Isso é verdadeiro mesmo que ambas as versões do Exchange estejam instaladas na mesma floresta. Sem configuração adicional, os administradores do Exchange 2013 não têm as permissões solicitadas para gerenciar os servidores baseados no Exchange 2007 e os administradores do Exchange 2007 não têm as permissões solicitadas para gerenciar os servidores baseados no Exchange 2013. Você deve considerar as seguintes perguntas:

  - Você deseja conceder acesso aos administradores do Exchange 2013 para que gerenciem os servidores do Exchange 2007?

  - Você deseja conceder acesso aos administradores do Exchange 2007 para que gerenciem os servidores do Exchange 2013?

  - Você deseja personalizar as permissões do Exchange 2013 para que elas correspondam às personalizações feitas para as ACLs do Exchange 2007?

## Concessão de permissões do Exchange 2013 para administradores do Exchange 2007

Se quiser que os administradores do Exchange 2007 gerenciem servidores do Exchange 2013, os administradores do Exchange 2007 deverão ser adicionados como membros de um ou mais grupos de funções do Exchange 2013. Você pode adicionar tanto usuários quanto USGs a grupos de funções. Desta maneira, as permissões concedidas aos grupos de funções são aplicadas aos usuários ou USGs que você adicionar como membros.


> [!IMPORTANT]
> Se você usar grupos de segurança do Active Directory de domínio local ou global, será necessário mudá-los para USGs caso você queira adicioná-los como membros de um grupo de funções do Exchange 2013. O Exchange 2013 suporta apenas USGs.



A tabela a seguir descreve o mapeamento entre as funções de administrador do Exchange 2007 e os grupos de funções do Exchange 2013.

### Funções de administrador do Exchange 2007 e grupos de funções do Exchange 2010

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Funções de administrador do Exchange 2007</th>
<th>Grupo de funções do Exchange 2013</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Administrador da organização do Exchange</p></td>
<td><p>Gerenciamento da Organização</p></td>
</tr>
<tr class="even">
<td><p>Administrador de destinatários do Exchange</p></td>
<td><p>Gerenciamento de Destinatários</p></td>
</tr>
<tr class="odd">
<td><p>Administrador do servidor Exchange</p></td>
<td><p>Gerenciamento do Servidor</p></td>
</tr>
<tr class="even">
<td><p>Administrador somente para exibição do Exchange</p></td>
<td><p>Gerenciamento de Organizações Somente Exibição</p></td>
</tr>
<tr class="odd">
<td><p>Servidor Exchange</p></td>
<td><p>Nenhum grupo de funções equivalente no Exchange 2013</p>
<p>(Para mais informações sobre como criar grupos de funções personalizados, consulte <a href="manage-role-groups-exchange-2013-help.md">Gerenciar grupos de função</a>.)</p></td>
</tr>
<tr class="even">
<td><p>Administrador de pasta pública do Exchange</p></td>
<td><p>Gerenciamento de Pasta Pública</p></td>
</tr>
</tbody>
</table>


Se todos os seus administradores do Exchange 2007 forem membros de uma das três funções administrativas do Exchange 2007, você poderá adicionar os membros de cada um dos grupos administrativos ao seu grupo de funções do Exchange 2013 equivalente. Por exemplo, se quiser conceder a todos os administradores da organização do Exchange 2007 acesso total aos objetos do Exchange 2013, adicione o USG de administradores da organização do Exchange ao grupo de funções Gerenciamento da Organização.

Para mais informações sobre como adicionar usuários e USGs aos grupos de funções, consulte [Gerenciar membros do grupo de função](manage-role-group-members-exchange-2013-help.md).

Se modificar as ACLs nos objetos do Exchange 2007 a fim de conceder mais permissões granulares aos administradores do Exchange 2007 e quiser atribuir permissões similares para os servidores Exchange 2013 desses administradores, siga estas etapas:

1.  Verifique as personalizações da ACL que foram feitas nos objetos do Exchange 2007 e identifique os administradores aos quais foram concedidas permissões para cada um desses objetos.

2.  Categorize cada objeto do Exchange 2007. Por exemplo, determine se o objeto é um banco de dados, servidor ou objeto de destinatário.

3.  Mapeie os objetos para o grupo de funções do Exchange 2013 correspondente. Para obter uma lista de grupos de funções internos, consulte [Grupos de funções internos](built-in-role-groups-exchange-2013-help.md).

4.  Adicione os USGs ou os usuários de cada tipo de objeto aos grupos de funções do Exchange 2013 correspondentes. Para mais informações sobre como adicionar usuários e USGs aos grupos de funções, consulte [Gerenciar membros do grupo de função](manage-role-group-members-exchange-2013-help.md).

Após concluir essas etapas, o administradores do Exchange 2007 serão os membros do grupo de funções específico mapeado para os objetos do Exchange 2013 apropriados. Os administradores do Exchange 2007 podem usar as ferramentas de gerenciamento do Exchange 2013 para administrar os destinatários e servidores do Exchange 2013.


> [!IMPORTANT]
> Em geral, os destinatários e servidores do Exchange 2007 devem ser administrados pelas uso das ferramentas de gerenciamento do Exchange 2007, enquanto os destinatários e servidores do Exchange 2013 devem ser administrados pelo uso das ferramentas de gerenciamento do Exchange 2013.



Se os grupos de funções internos não fornecerem o conjunto específico de permissões que você deseja conceder para determinados administradores, você poderá criar grupos de funções personalizados. Ao criar um grupo de funções personalizado, é possível escolher quais funções adicionar a ele. Você pode definir os recursos específicos que os membros do grupo de funções gerenciarão. Por exemplo, se quiser que os administradores gerenciem apenas os grupos de distribuição, você poderá criar um grupo de funções personalizado e escolher somente a função de Grupos de Distribuição. Após você fazer isso, os membros desse grupo de funções personalizado poderão gerenciar apenas os grupos de distribuição. Para mais informações sobre como criar grupos de funções personalizados, consulte [Gerenciar grupos de função](manage-role-groups-exchange-2013-help.md).

Se você atribuir permissões seletivas a certos objetos do Exchange 2007 (por exemplo, permitir que administradores administrem somente bancos de dados específicos) e se quiser aplicar a mesma configuração aos seus servidores do Exchange 2013, consulte "Recriar a personalização de ACL do Exchange 2007 usando os escopos de gerenciamento do Exchange 2013" posteriormente neste tópico.

## Concessão de permissões do Exchange 2007 para administradores do Exchange 2013

Se quiser que os administradores do Exchange 2013 gerenciem servidores do Exchange 2007, adicione os administradores do Exchange 2013 aos USGs ou ao grupo de segurança correspondente à função de administrador do Exchange 2007 em particular. Como alternativa, se você tiver configurações de ACL personalizadas, adicione os administradores às ACLs apropriadas. Os grupos de funções são USGs, portanto, os grupos de funções podem ser adicionados diretamente aos USGs da função de administrador do Exchange 2007.

Quando você terminar, os administradores do Exchange 2013 serão membros da função ou das funções de administrador do Exchange 2007. Os administradores do Exchange 2013 podem usar as ferramentas de gerenciamento do Exchange 2007 para administrar os destinatários e servidores do Exchange 2007.

## Recriação da personalização de ACL do Exchange 2007 usando os escopos de gerenciamento do Exchange 2013

No Exchange 2007, se você quiser restringir quem poderá administrar um armazenamento de caixa de correio específico, administrar usuários específicos ou controlar em qual armazenamento de caixa de correio serão criadas as caixas de correio, será necessário modificar as ACLs nos objetos que você deseja restringir. O Exchange 2013 oferece as mesmas capacidades, mas sem a necessidade de modificar quaisquer ACLs Isso é feito por meio do uso de escopos de gerenciamento, que são um componente do RBAC.

Os escopos de gerenciamento oferecem escopos internos e escopos personalizados para definir quais objetos os administradores podem gerenciar. Ao aplicar escopos de gerenciamento, você pode definir quais destinatários podem ser administrados, em quais bancos de dados de caixa de correio as caixas de correio podem ser criadas e quais destinatários ou servidores devem ser administrados somente por um pequeno grupo de administradores.

É possível criar os seguintes tipos de escopos de gerenciamento:

  - **Relativo predefinido**   Os escopos relativos predefinidos estão incluídos no Exchange 2013. Você pode controlar o que um usuário pode ver e modificar. Por exemplo, os escopos relativos predefinidos podem controlar se os usuários veem somente informações sobre eles mesmos ou sobre toda a organização.

  - **Destinatário**   Os escopos de destinatário controlam quais destinatários podem ser criados, modificados ou excluídos por um administrador. Essas seleções podem estar baseados em uma UO (Unidade Organizacional), um filtro de destinatário ou em ambos. Os filtros de destinatário especificam os critérios que um destinatário precisa cumprir a fim de ser incluído em um escopo. Por exemplo, você pode criar um escopo de filtro de destinatário que inclua todos os usuários em determinado local ou em um departamento específico. Você pode até mesmo combinar UOs e filtros de destinatários para correspondência apenas com usuários que estejam em uma UO específica e se reportam somente para um determinado administrador.

  - **Servidor**   Os escopos de servidor controlam quais servidores podem ser administrados por um administrador. Você pode especificar listas de servidores ou filtros de servidores. Para listas de servidores, você define uma lista estática de servidores que podem ser gerenciados. Os filtros de servidores funcionam da mesma forma que filtros de destinatários em que você pode especificar os critérios que precisam ter correspondência. Por exemplo, você pode criar um escopo de servidor que vise todos os servidores em um site do Active Directory em particular.

  - **Banco de dados**   Os escopos de banco de dados controlam quais bancos de dados podem ser gerenciados por um administrador. Eles também controlam em quais bancos de dados as caixas de correio podem ser criadas ou para quais serão movidas. Como escopos de servidor, eles podem ser definidos como listas ou filtros. Por exemplo, é possível criar uma lista ou filtro que possibilite aos administradores criar caixas de correio em determinados bancos de dados de caixa de correio (ou mover essas caixas para eles) gerenciadas por uma subsidiária específica.

  - **Exclusivo**   Os escopos de destinatário, servidor e banco de dados podem também ser criados como escopos exclusivos. Os escopos exclusivos trabalham do mesmo modo que negar acesso de ACEs em ACLs. Se alguma coisa correspondem a um escopo exclusivo, somente os administradores atribuídos a um escopo exclusivo podem gerenciar esse objeto. Isso será verdadeiro se outro escopo que não é exclusivo corresponder ao mesmo objeto. Isso é útil especialmente quando você decidir que apenas poucas pessoas de alta confiança podem gerenciar a caixa de correio de um executivo. Mesmo que outro escopo de destinatário regular seja mais amplo e inclua a caixa de correio do executivo no escopo, os administradores aos quais foi atribuído esse escopo regular mais amplo não poderão gerenciar a caixa de correio desse executivo, a menos que seja atribuído a eles o escopo exclusivo.

Os escopos de gerenciamento são usados com funções de gerenciamento, atribuições de função de gerenciamento e grupos de funções de gerenciamento a fim de controlar quem pode gerenciar quais objetos e de qual maneira. Para mais informações, consulte estes tópicos:

  - [Noções básicas sobre escopos da função de gerenciamento](understanding-management-role-scopes-exchange-2013-help.md)

  - [Noções básicas sobre escopos exclusivos](understanding-exclusive-scopes-exchange-2013-help.md)

  - [Noções básicas sobre as atribuições de função de gerenciamento](understanding-management-role-assignments-exchange-2013-help.md)

  - [Noções básicas sobre grupos de funções de gerenciamento](understanding-management-role-groups-exchange-2013-help.md)

  - [Noções básicas sobre funções de gerenciamento](understanding-management-roles-exchange-2013-help.md)

Para criar o mesmo modelo de permissões do Exchange 2013, usando os escopos de gerenciamento que podem ter sido definidos com o uso de ACLs personalizadas, você terá que fazer o inventário das ACLs personalizadas e criar escopos de gerenciamento correspondentes a elas. Você pode usar as propriedades filtráveis que estão disponíveis nos objetos de banco de dados, servidor ou destinatário a fim de criar escopos de gerenciamento que incluam os objetos aos quais você deseja que cada escopo de gerenciamento possa controlar o acesso. Para mais informações sobre as propriedades que você pode usar com os filtros de escopo de gerenciamento, consulte [Noções básicas sobre filtros do escopo de função de gerenciamento](understanding-management-role-scope-filters-exchange-2013-help.md).

Para obter mais informações sobre como criar escopos de gerenciamento, consulte [Criar um escopo regular ou exclusivo](create-a-regular-or-exclusive-scope-exchange-2013-help.md).

