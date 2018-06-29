---
title: 'Destinatários: Exchange 2013 Help'
TOCTitle: Destinatários
ms:assetid: 40300ed4-85a5-463d-bb3a-cf787bd44e9d
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Bb201680(v=EXCHG.150)
ms:contentKeyID: 50485415
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Destinatários

 

_**Aplica-se a:**Exchange Online, Exchange Server 2013_

_**Tópico modificado em:**2015-03-09_

As pessoas e os recursos que enviam e recebem mensagens são a parte principal de qualquer sistema de colaboração e de mensagens. Em uma organização do Exchange, essas pessoas e esses recursos são chamados de *destinatários*. Um destinatário é qualquer objeto habilitado para email no Active Directory para o qual o Microsoft Exchange pode entregar e rotear mensagens.

## Tipos de destinatários do Exchange

O Exchange inclui vários tipos de destinatários explícitos. Cada tipo de destinatário é identificado no Centro de Administração do Exchange (EAC) e tem um valor único na propriedade *RecipientTypeDetails* do Shell de Gerenciamento do Exchange. O uso de tipos de destinatários explícitos tem os seguintes benefícios:

  - De imediato, você pode diferenciar entre vários tipos de destinatários.

  - Você pode pesquisar e classificar por cada tipo de destinatário.

  - É mais fácil executar operações de gerenciamento em massa para tipo selecionados de destinatário.

  - É mais fácil visualizar as propriedades de destinatário porque o EAC usa os tipos de destinatários para processar diferentes páginas de propriedade. Por exemplo, a capacidade do recurso é exibida para uma caixa de correio da sala, mas não está presente para uma caixa de correio de usuário.

A tabela a seguir lista os tipos de destinatários disponíveis. Todos esses tipos de destinatários são abordados em mais detalhes posteriormente neste tópico.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Tipo de destinatário</th>
<th>Descrição</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Grupo dinâmico de distribuição</p></td>
<td><p>Um grupo de distribuição que usa filtros e condições de destinatários para determinar sua associação no momento em que as mensagens são enviadas.</p></td>
</tr>
<tr class="even">
<td><p>Caixa de correio de equipamento</p></td>
<td><p>Uma caixa de correio de recurso atribuída a um recurso que não tem um local específico, como um computador portátil, projetor, microfone ou carro da empresa. As caixas de correio de equipamento podem ser incluídas como recursos nas solicitações de reuniões, proporcionando um modo simples e eficaz de usar os recursos para seus usuários.</p></td>
</tr>
<tr class="odd">
<td><p>Caixa de correio vinculada</p></td>
<td><p>Uma caixa de correio atribuída a um usuário individual em uma floresta confiável separada.</p></td>
</tr>
<tr class="even">
<td><p>Contato de email</p></td>
<td><p>Um contato do Active Directory habilitado para email que contém informações sobre pessoas ou organizações que existem fora da organização do Exchange. Cada contato de email tem um endereço de email externo. Todas as mensagens enviadas ao contato de email são roteadas para esse endereço de email externo.</p></td>
</tr>
<tr class="odd">
<td><p>Contato da floresta de email</p></td>
<td><p>Um contato de email que representa um objeto de destinatário de outra floresta. Os contatos da floresta de email geralmente são criados por sincronização do MIIS (Microsoft Identity Integration Server).</p>

> [!IMPORTANT]
> Contatos de floresta de email são objetos de destinatário somente leitura atualizados apenas através do MIIS ou uma sincronização personalizada similar. Não é possível remover ou modificar um contato de floresta de email usando o EAC ou o Shell.


</td>
</tr>
<tr class="even">
<td><p>Usuário de email</p></td>
<td><p>Um usuário do Active Directory habilitado para email que representa um usuário fora da organização do Exchange. Cada usuário de email tem um endereço de email externo. Todas as mensagens enviadas ao usuário de email são roteadas para esse endereço de email externo.</p>
<p>Um usuário de email é semelhante a um contato de email, exceto que um usuário de email tem credenciais de logon do Active Directory e pode acessar recursos.</p></td>
</tr>
<tr class="odd">
<td><p>Grupo não universal habilitado para email</p></td>
<td><p>Um objeto de grupo local ou global do Active Directory habilitado para email. Os grupos não universais habilitados para email foram descontinuados no Exchange Server 2007 e só podem existir se tiverem sido migrados do Exchange 2003 ou de versões anteriores do Exchange. Não é possível usar o Exchange Server 2013 para criar novos grupos de distribuição não universais.</p></td>
</tr>
<tr class="even">
<td><p>Pasta pública habilitada para email</p></td>
<td><p>Uma pasta pública do Exchange configurada para receber mensagens.</p></td>
</tr>
<tr class="odd">
<td><p>Grupos de Distribuição</p></td>
<td><p>Um grupo de distribuição é um objeto de grupo de distribuição do Active Directory habilitado para email que pode ser usado apenas para distribuir mensagens a um grupo de destinatários.</p></td>
</tr>
<tr class="even">
<td><p>Grupo de segurança habilitado para email</p></td>
<td><p>Um grupo de segurança habilitado para email é um objeto de grupo de segurança universal do Active Directory que pode ser usado para atribuir permissões de acesso a recursos no Active Directory e que também pode ser usado para distribuir mensagens.</p></td>
</tr>
<tr class="odd">
<td><p>Destinatário do Microsoft Exchange</p></td>
<td><p>Um objeto de destinatário especial que fornece um remetente de mensagem conhecido e unificado que diferencia as mensagens geradas pelo sistema de outras mensagens. Ele substitui o remetente Administrador do Sistema usado para mensagens geradas pelo sistema nas versões anteriores do Exchange.</p></td>
</tr>
<tr class="even">
<td><p>Caixa de correio de sala</p></td>
<td><p>Uma caixa de correio de recurso atribuída a um local de reuniões, como uma sala de conferência, um auditório ou uma sala de treinamento. As caixas de correio de sala podem ser incluídas como recursos nas solicitações de reuniões, fornecendo um modo simples e eficaz de organizar as reuniões para seus usuários.</p></td>
</tr>
<tr class="odd">
<td><p>Caixa de correio compartilhada</p></td>
<td><p>Uma caixa de correio que não está inicialmente associada a um único usuário e que geralmente está configurada para permitir acesso a vários usuários.</p></td>
</tr>
<tr class="even">
<td><p>Caixa de correio de Site</p></td>
<td><p>Uma caixa de correio composta de uma caixa de correio do Exchange para armazenar mensagens de email e um site do SharePoint para armazenar documentos. Os usuários podem acessar tanto as mensagens de email quanto os documentos usando a mesma interface de cliente. Para mais informações, consulte <a href="site-mailboxes-exchange-2013-help.md">Caixas de correio locais</a>.</p></td>
</tr>
<tr class="odd">
<td><p>Caixa de correio do usuário</p></td>
<td><p>Uma caixa de correio atribuída a um usuário individual na organização do Exchange. Geralmente, ela contém mensagens, itens de calendário, contatos, tarefas, documentos e outros dados comerciais importantes.</p></td>
</tr>
<tr class="even">
<td><p>Caixa de correio do Office 365</p></td>
<td><p>Em implementações híbridas, uma caixa de correio do Office 365 consiste em um usuário de email que existe no Active Directory local e uma caixa de correio em nuvem associada que existe no Exchange Online.</p></td>
</tr>
<tr class="odd">
<td><p>Usuário vinculado</p></td>
<td><p>Um usuário vinculado é um usuário cuja caixa de correio reside em uma floresta diferente da floresta na qual o usuário em si reside.</p></td>
</tr>
</tbody>
</table>


## Caixas de correio

Caixas de correio são o tipo de destinatário mais comum usado pelos operadores de informações em uma organização do Exchange. Cada caixa de correio é associada a uma conta de usuário do Active Directory. O usuário pode usar a caixa de correio para enviar e receber mensagens, bem como para armazenar mensagens, compromissos, tarefas, anotações e documentos. As caixas de correios são as principais ferramentas de mensagens e colaboração para os usuários na sua organização do Exchange.

## Componentes da caixa de correio

Cada caixa de correio é constituída de um usuário do Active Directory e dos dados da caixa de correio que são armazenados no banco de dados de caixa de correio do Exchange (como mostra a figura a seguir). Todos os dados de configuração da caixa de correio são armazenados nos atributos do Exchange do objeto de usuário do Active Directory. O banco de dados de caixa de correio contém os dados reais contidos na caixa de correio associada à conta de usuário.


> [!IMPORTANT]
> Quando você cria uma caixa de correio para um usuário novo ou existente, os atributos do Exchange&nbsp;exigidos para uma caixa de correio são adicionados ao objeto de usuário no Active Directory. Os dados da caixa de correio associada não são criados até a caixa de correio receba uma mensagem ou o usuário entre nela.



**Componentes da caixa de correio**

![Partes que compõem uma caixa de correio](images/Bb201680.5fcb5e6d-656e-42ae-871f-0eef8aea456b(EXCHG.150).gif "Partes que compõem uma caixa de correio")


> [!WARNING]
> Se você remover uma caixa de correio, os dados armazenados no banco de dados de caixa de correio do Exchange&nbsp;serão marcados para exclusão e a conta de usuário associada também será excluída do Active Directory. Para reter a conta de usuário e excluir apenas os dados da caixa de correio, desabilite a caixa de correio.



## Tipos de caixas de correio

O Exchange oferece suporte aos seguintes tipos de caixas de correio:

  - **Caixas de correio do usuário   **As caixas de correio do usuário são atribuídas a usuários individuais em sua organização do Exchange. As caixas de correio do usuário fornecem a seus usuários uma rica plataforma de colaboração. Os usuários podem enviar e receber mensagens, gerenciar seus contatos, agendar reuniões e manter uma lista de tarefas. Eles também podem ter mensagens de voz entregues em suas caixas de correio. As caixas de correio do usuário são o tipo de caixa de correio mais comumente usado e, geralmente, são o tipo de caixa de correio atribuído a usuários em sua organização.

  - **Caixas de correio vinculadas**   As caixas de correio vinculadas são caixas de correio que são acessadas por usuários em uma floresta separada e confiável. As caixas de correio vinculadas podem ser necessárias para organizações que implantem o Exchange em uma floresta de recursos. O cenário de floresta de recursos permite que uma organização centralize o Exchange em uma única floresta, ao mesmo tempo em que permite o acesso à organização do Exchange com contas de usuário em uma ou mais florestas confiáveis.
    
    Como já foi dito, cada caixa de correio deve ter uma conta de usuário associada a ela. No entanto, a conta de usuário que acessará a caixa de correio vinculada não existe na floresta em que o Exchange é implantado. Portanto, uma conta de usuário desabilitada existente na mesma floresta do Exchange está associada a cada caixa de correio vinculada. A figura a seguir ilustra o relacionamento entre a conta de usuário vinculada que será usada para acessar a caixa de correio vinculada e a conta de usuário desabilitada na floresta de recursos do Exchange que está associada à caixa de correio vinculada.
    
    **Caixa de correio vinculada**
    
    ![Organização complexa do Exchange com floresta de recursos](images/Aa998031.706725cf-e520-4b89-a275-acd8fb58943a(EXCHG.150).gif "Organização complexa do Exchange com floresta de recursos")  

  - **Caixas de correio do Office 365   **Quando você cria uma caixa de correio do Office 365 no Exchange Online em uma implantação híbrida, o usuário de email é criado no Active Directory local. A sincronização de diretório, se for configurada, sincronizará automaticamente esse novo objeto de usuário com o Office 365, que depois o converterá em uma caixa de correio em nuvem no Exchange Online. É possível criar caixas de correio do Office 365 como caixas de correio de usuário comum, como caixas de correio de recursos para salas de reunião e equipamentos, e como caixas de correio compartilhadas.

  - **Caixas de correio compartilhadas**   As caixas de correio compartilhadas não são associadas inicialmente a usuários individuais, e geralmente são configuradas para permitir acesso a vários usuários.
    
    Embora seja possível atribuir permissões de acesso de logon a usuários adicionais em qualquer tipo de caixa de correio, as caixas de correio compartilhadas são dedicadas a essa funcionalidade. O usuário do Active Directory associado a uma caixa de correio compartilhada deve ser uma conta desabilitada. Após criar uma caixa de correio compartilhada, você precisa atribuir permissões a todos os usuários que necessitem acessá-la.

  - **Caixa de correio de recursos**   As caixas de correio de recursos são caixas de correio especiais projetadas para serem usadas para agendar recursos. Assim como todos os tipos de caixas de correio, uma caixa de correio de recursos tem uma conta de usuário associada do Active Directory, mas ela deve ser uma conta desabilitada. Estes são os tipos de caixas de correio de recurso:
    
      - **Caixas de correio de sala**   Essas caixas de correio são atribuídas a locais de reunião, como salas de conferência, auditórios e salas de treinamento.
    
      - **Caixas de correio de equipamento**   Essas caixas de correio são atribuídas a recursos que não têm um local específico, como computadores portáteis, projetores, microfones ou carros da empresa.
    
    Você pode incluir os dois tipos de caixas de correio de recursos nas solicitações de reuniões, fornecendo um modo simples e eficaz para que seus usuários utilizem recursos. É possível configurar as caixas de correio de recursos para processar automaticamente solicitações de reuniões de entrada com base nas diretivas de reserva de recursos definidas pelos proprietários dos recursos. Por exemplo, você pode configurar uma sala de conferência para aceitar automaticamente solicitações de reuniões de entrada, exceto reuniões recorrentes, que podem estar sujeitas à aprovação pelo proprietário do recurso.

## Caixas de correio de sistema

As caixas de correio do sistema são criadas pelo Exchange no domínio raiz da floresta do Active Directory durante a instalação. Usuários e administradores não conseguem entrar nessas caixas de correio. Caixas de correio de sistema são criados por recursos do Exchange como Unificação de Mensagens (UM), migração, aprovação de mensagens e Descoberta Eletrônica In-loco. Esta tabela lista informações sobre caixas de correio do sistema, como elas são exibidas em Active Directory.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Caixa de Correio</th>
<th>Nome</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Organização</p></td>
<td><p>SystemMailbox {bb558c35-97f1-4cb9-8ff7-d53741dc928c}</p></td>
</tr>
<tr class="even">
<td><p>Aprovação de mensagem</p></td>
<td><p>SystemMailbox {1f05a927-<em>xxxx</em>- <em>xxxx</em> - <em>xxxx</em> -<em>xxxxxxxxxxxx</em>}</p>
<p>em que <em>x</em> é um número único atribuído aleatoriamente a cada floresta do Exchange</p></td>
</tr>
<tr class="odd">
<td><p>Armazenamento de dados da UM</p></td>
<td><p>SystemMailbox {e0dc1c29-89c3-4034-b678-e6c29d823ed9}</p></td>
</tr>
<tr class="even">
<td><p>Descoberta</p></td>
<td><p>DiscoverySearchMailbox {D919BA05-46A6-415f-80AD-7E09334BB852}</p></td>
</tr>
<tr class="odd">
<td><p>E-mail federado</p></td>
<td><p>FederatedEmail.4c1f4d8b-8179-4148-93bf-00a95fa1e042</p></td>
</tr>
<tr class="even">
<td><p>Migração</p></td>
<td><p>Migration.8f3e7716-2011-43e4-96b1-aba62d229136</p></td>
</tr>
</tbody>
</table>


Se quiser descomissionar o último servidor de Caixa de Correio da sua organização no Exchange, primeiro desative essas caixas de correio de sistema usando o cmdlet [Disable-Mailbox](https://technet.microsoft.com/pt-br/library/aa997210\(v=exchg.150\)). Ao descomissionar um servidor de Caixa de Correio que contenha essas caixas de correio de sistema, você deve movê-las para outro servidor de Caixa de Correio para garantir que não haja perda de funcionalidade.

## Planejar caixas de correio

As caixas de correio são criadas em bancos de dados de caixas de correio em servidores Exchange com a função de servidor Caixa de Correio instalada. Para ajudar a fornecer uma plataforma eficaz e confiável para os usuários de caixas de correio, o planejamento detalhado para a implantação de servidores e bancos de dados de Caixa de Correio é essencial. Para saber mais sobre como planejar bancos de dados e servidores de Caixas de Correio, consulte [Planejamento e implantação](planning-and-deployment-for-exchange-2013-installation-instructions.md).

## Grupos de Distribuição

Grupos de distribuição são objetos de grupos do Active Directory habilitados para email que são usados principalmente para distribuir mensagens a vários destinatários. Qualquer tipo de destinatário pode ser um membro de um grupo de distribuição.


> [!IMPORTANT]
> Observe as diferenças de terminologia entre Active Directory e o Exchange. No Active Directory, um grupo de distribuição se refere a qualquer grupo que não tenha um contexto de segurança, seja ele habilitado para email ou não. No Exchange, todos os grupos habilitados para email são chamados de grupos de distribuição, tenham ou não um contexto de segurança.



O Exchange aceita os seguintes tipos de grupos de distribuição:

  - **Grupos de distribuição**   Esses são objetos de grupos de distribuição universais do Active Directory que estão habilitados para email. Eles podem ser usados apenas para distribuir mensagens para um grupo de destinatários.

  - **Grupos de segurança habilitados para email**   Esses são objetos de grupos de segurança universais do Active Directory que são habilitados para email. Eles podem ser usados para atribuir permissões de acesso a recursos no Active Directory e também podem ser usados para distribuir mensagens.

  - **Grupos não universais habilitados para email**   São os objetos de grupo local ou global Active Directory que são habilitados para email. Você pode criar ou habilitar para email somente grupos de distribuição universais. Você pode ter grupos habilitados para email que tenham sido migrados de versões anteriores do Exchange e que não são grupos universais. Esses grupos também podem ser gerenciados usando o EAC ou o Shell.
    

    > [!TIP]
    > Para converter um grupo global ou de domínio local em um grupo universal, você pode usar o cmdlet <A href="https://technet.microsoft.com/pt-br/library/bb123770(v=exchg.150)">Set-Group</A> no Shell.



## Grupos dinâmicos de distribuição

Os grupos dinâmicos de distribuição são grupos de distribuição cuja associação é aceita com base em filtros específicos de destinatários em vez de um conjunto definido de destinatários.

Ao contrário de grupos regulares de distribuição, a lista de associações de grupos dinâmicos de distribuição é calculada sempre que uma mensagem é enviada a eles, com base nos filtros e nas condições que você especifica. Quando uma mensagem de email for enviada para um grupo dinâmico de distribuição, ele será entregue a todos os destinatários da organização que correspondam aos critérios definidos para aquele grupo dinâmico de distribuição.


> [!IMPORTANT]
> Um grupo dinâmico de distribuição inclui qualquer destinatário no Active Directory&nbsp;com atributos que correspondam ao filtro do grupo no momento em que uma mensagem é enviada. Se as propriedades de um destinatário forem modificadas para corresponder ao filtro do grupo, esse destinatário poderá se tornar acidentalmente um membro do grupo e iniciar o recebimento de mensagens que são enviadas ao grupo dinâmico de distribuição. Processos de configuração de conta consistentes e bem definidos poderão reduzir as chances de isso acontecer.



Para ajudar a criar filtros de destinatários para grupos dinâmicos de distribuição, você pode usar filtros predefinidos. Um *filtro predefinido* é um filtro normalmente usado para atender a diversos critérios de filtragem de destinatários. Esses filtros podem ser usados para especificar os tipos de destinatários que você deseja incluir no grupo dinâmico de distribuição. Além disso, você também pode especificar uma lista de condições que os destinatários devem atender. Você pode criar condições predefinidas com base nas seguintes propriedades:

  - Atributos personalizados 1–15

  - Estado

  - Empresa

  - Departamento

  - Contêiner de destinatário

Você também pode especificar condições com base em propriedades de destinatário diferentes daquelas listadas anteriormente. Para isso, use o Shell para criar uma consulta personalizada para o grupo dinâmico de distribuição. Lembre-se de que as configurações de filtro e as condições para os grupos dinâmicos de distribuição que tenham filtros de destinatário personalizados podem ser gerenciadas somente usando-se o Shell. Para obter um exemplo de como criar um grupo dinâmico de distribuição usando uma consulta personalizada, consulte [Gerenciar grupos dinâmicos de distribuição](manage-dynamic-distribution-groups-exchange-2013-help.md).

## Contatos de email

Os contatos de email geralmente contêm informações sobre pessoas ou organizações existentes fora da organização do Exchange. Os contatos de email podem aparecer no catálogo compartilhado de endereços da sua organização (também chamado de lista de endereços global ou GAL) e em outras listas de endereços, e podem ser adicionados como membros a grupos de distribuição. Cada contato tem um endereço de email externo e todas as mensagens de email enviadas a um contato são automaticamente encaminhadas para esse endereço. Os contatos são ideais para representar pessoas externas à sua organização do Exchange (no catálogo compartilhado de endereços) que não precisem de acesso a nenhum recurso interno. Estes são os tipos de contatos de email:

  - **Contatos de email**   São contatos do Active Directory habilitados para email que contêm informações sobre pessoas ou organizações existentes fora da organização do Exchange.

  - **Contatos da floresta de email**   Representam os objetos de destinatário de outra floresta. Esses contatos geralmente são criados por sincronização de diretório. Os contatos de floresta de email são objetos de destinatário somente leitura que podem ser atualizados ou removidos somente por meio de sincronização. As interfaces de gerenciamento do Exchange não podem ser usadas para modificar ou remover um contato da floresta de email.

## Usuários de email

Usuários de email são semelhantes a contatos de email. Ambos têm endereços de email externos, ambos contêm informações sobre pessoas de fora da organização do Exchange e ambos podem ser exibidos no catálogo compartilhado de endereços e em outras listas de endereços. No entanto, ao contrário de um contato de email, os usuários de email têm credenciais de logon do Active Directory e podem acessar recursos cujas permissões tenham sido atribuídas aos usuários.

Se uma pessoa fora de sua organização exigir acesso a recursos em sua rede, você deverá criar um usuário de email, em vez de um contato de email. Por exemplo, talvez você queira criar usuários de email para consultores de curto prazo que precisem acessar a sua infraestrutura de servidor, mas que usarão seus próprios endereços externos.

Outro cenário é criar usuários de email em sua organização para quem você não deseja manter uma caixa de correio do Exchange. Por exemplo, após uma aquisição, a empresa adquirida poderá manter sua infra-estrutura de mensagens separada, mas talvez precise ter acesso a recursos de sua rede. Para esses usuários, você pode desejar criar usuários de email, em vez de usuários de caixas de correio.


> [!TIP]
> No EAC, você usa a página <STRONG>Destinatários</STRONG> &gt; <STRONG>Contatos</STRONG> para gerenciar usuários de email. Não há uma página separada para usuários de email.



## Pastas públicas habilitadas para mensagens

As pastas públicas foram projetadas para servir como um repositório de informações compartilhadas entre muitos usuários. A habilitação para email de uma pasta pública oferece um nível extra de funcionalidade aos usuários. Além de poder postar mensagens para a pasta, os usuários podem enviar mensagens de email para a pasta pública e, às vezes, recebê-las. Cada pasta habilitada para email tem um objeto no Active Directory que armazena seu endereço de email, o nome do catálogo de endereços e outros atributos relacionados a email.

Você pode gerenciar pastas públicas usando o EAC ou o Shell. Para obter mais informações sobre como gerenciar pastas públicas, consulte [Pastas públicas](public-folders-exchange-2013-help.md).

## Destinatário do Microsoft Exchange

O destinatário do Microsoft Exchange é um objeto de destinatário especial que fornece um remetente de mensagem conhecido e unificado que diferencia as mensagens geradas pelo sistema de outras mensagens. Ele substitui o remetente Administrador do Sistema que era usado para mensagens geradas pelo sistema nas versões anteriores do Exchange.

O destinatário do Microsoft Exchange não é um objeto de destinatário comum, como uma caixa de correio, usuário de email ou contato de email, e não é gerenciado com ferramentas de destinatário comuns. No entanto, você pode usar o cmdlet [Set-OrganizationConfig](https://technet.microsoft.com/pt-br/library/aa997443\(v=exchg.150\)) no Shell para configurar o destinatário do Microsoft Exchange.


> [!TIP]
> Quando mensagens geradas pelo sistema são enviadas para um remetente externo, o destinatário do Microsoft Exchange não é usado como o remetente da mensagem. Em vez disso, o endereço de email especificado pelo parâmetro <EM>ExternalPostmasterAddress</EM> no cmdlet <A href="https://technet.microsoft.com/pt-br/library/bb124151(v=exchg.150)">Set-TransportConfig</A> é usado.



## Documentação de destinatários

A tabela a seguir contém links para tópicos que o ajudarão a gerenciar e a saber mais sobre destinatários do Exchange.


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
<td><p><a href="create-user-mailboxes-exchange-2013-help.md">Criar caixas de correio do usuário</a></p></td>
<td><p>Saiba como criar caixas de correio de usuário usando o Centro de administração do Exchange ou o Shell de Gerenciamento do Exchange.</p></td>
</tr>
<tr class="even">
<td><p><a href="manage-user-mailboxes-exchange-2013-help.md">Gerenciar caixas de correio do usuário</a></p></td>
<td><p>Saiba como criar caixas de correio de usuários, alterar propriedades de caixa de correio e editar em massa propriedades selecionadas para várias caixas de correio.</p></td>
</tr>
<tr class="odd">
<td><p><a href="manage-linked-mailboxes-exchange-2013-help.md">Gerenciar caixas de correio vinculadas</a></p></td>
<td><p>Saiba mais sobre os requisitos de caixas de correio vinculadas, como criá-las e vinculá-las a uma conta mestre e como alterar propriedades de caixas de correio vinculadas.</p></td>
</tr>
<tr class="even">
<td><p><a href="create-and-manage-distribution-groups-exchange-2013-help.md">Criar e gerenciar grupos de distribuição</a></p></td>
<td><p>Saiba como criar e gerenciar grupos de distribuição e como criar uma diretiva de nomeação de grupo para a sua organização.</p></td>
</tr>
<tr class="odd">
<td><p><a href="manage-mail-enabled-security-groups-exchange-2013-help.md">Gerenciar grupos de segurança habilitados para email</a></p></td>
<td><p>Saiba como criar e gerenciar grupos de segurança habilitados para email.</p></td>
</tr>
<tr class="even">
<td><p><a href="manage-dynamic-distribution-groups-exchange-2013-help.md">Gerenciar grupos dinâmicos de distribuição</a></p></td>
<td><p>Saiba como criar grupos de distribuição dinâmicos e gerenciar propriedades de grupos de distribuição dinâmicos, como por exemplo utilizar atributos personalizados e outras propriedades para determinar a associação ao grupo.</p></td>
</tr>
<tr class="odd">
<td><p><a href="manage-mail-contacts-exchange-2013-help.md">Gerenciar contatos de email</a></p></td>
<td><p>Saiba como criar e gerenciar contatos de email.</p></td>
</tr>
<tr class="even">
<td><p><a href="manage-mail-users-exchange-2013-help.md">Gerenciar usuários de email</a></p></td>
<td><p>Saiba como criar e gerenciar usuários de email.</p></td>
</tr>
<tr class="odd">
<td><p><a href="create-and-manage-room-mailboxes-exchange-2013-help.md">Criar e gerenciar caixas de correio de sala</a></p></td>
<td><p>Saiba como criar caixas de correio de sala e gerenciar propriedades de caixas de correio de sala, como por exemplo habilitar reuniões recorrentes e configurar opções de agendamento.</p></td>
</tr>
<tr class="even">
<td><p><a href="manage-equipment-mailboxes-exchange-2013-help.md">Gerenciar caixas de correio de equipamento</a></p></td>
<td><p>Saiba como criar caixas de correio de equipamento, configurar opções de agendamento e gerenciar outras propriedades de caixa de correio.</p></td>
</tr>
<tr class="odd">
<td><p><a href="disconnected-mailboxes-exchange-2013-help.md">Caixas de correio desconectadas</a></p></td>
<td><p>Saiba mais sobre os dois tipos de caixas de correio desconectadas e sobre como trabalhar com eles.</p></td>
</tr>
<tr class="even">
<td><p><a href="custom-attributes-exchange-2013-help.md">Atributos personalizados</a></p></td>
<td><p>Saiba como adicionar informações sobre um destinatário usando atributos personalizados.</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://technet.microsoft.com/pt-br/library/bb124268(v=exchg.150)">Filtros de destinatários comandos do Shell</a></p></td>
<td><p>Saiba como usar filtros predefinidos e personalizados com comandos para filtrar um conjunto de destinatários.</p></td>
</tr>
<tr class="even">
<td><p><a href="manage-permissions-for-recipients-exchange-online-help.md">Gerenciar permissões para destinatários</a></p></td>
<td><p>Saiba como usar o EAC ou o Shell para atribuir permissões a usuários e grupos.</p></td>
</tr>
<tr class="odd">
<td><p><a href="automatic-mailbox-distribution-exchange-2013-help.md">Distribuição de caixa de correio automática</a></p></td>
<td><p>Saiba como funciona a distribuição de caixa de correio automática e como controlar que bancos de dados de caixa de correio são selecionados para caixas de correio novas e movidas.</p></td>
</tr>
</tbody>
</table>

