---
title: 'Listas de endereços: Exchange 2013 Help'
TOCTitle: Listas de endereços
ms:assetid: 8ee2672a-3a45-4897-8cc0-fa23c374dbf9
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Bb232119(v=EXCHG.150)
ms:contentKeyID: 50486145
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Listas de endereços

 

_**Aplica-se a:** Exchange Online, Exchange Server 2013_

_**Tópico modificado em:** 2014-12-02_

Uma *lista de endereços* é um conjunto de destinatários e objetos do Active Directory. Cada lista de endereços pode conter um ou mais tipos de objetos (por exemplo, usuários, contatos, grupos, pastas públicas e recursos de sala e equipamentos). Você pode usar listas de endereços para organizar destinatários e recursos, facilitando a busca pelos destinatários e recursos que você deseja. Listas de endereços são atualizadas dinamicamente. Portanto, quando novos destinatários são adicionados à sua organização, eles são automaticamente incluídos nas listas de endereços adequadas.

Como ilustrado na figura a seguir, aplicativos clientes, como o Microsoft Outlook, exibem as listas de endereços disponíveis que o Exchange oferece.

**Lista de endereços global, como exibida no Microsoft Office Outlook 2007**

![Listas de endereços exibidas no Outlook 2007](images/Bb232119.54d7729c-2e28-4863-8944-b0c37dabbbb3(EXCHG.150).gif "Listas de endereços exibidas no Outlook 2007")

Listas de endereços residem em Active Directory. Portanto, usuários móveis que estejam desconectados da rede são também desconectados dessas listas de endereços no lado do servidor. Entretanto, você pode criar catálogos de endereços offline (OABs) para usuários que estejam desconectados da rede. Esses OABs podem ser baixados para o disco rígido de um usuário. Frequentemente, para conservar recursos, os OABs são subconjuntos das informações das listas de endereços reais que residem em seus servidores. Para mais informações, consulte [Catálogos de endereços offline](offline-address-books-exchange-2013-help.md).

**Sumário**

Default address lists

Custom address lists

Best practices for creating address lists

## Listas de endereços padrão

Quando os usuários desejam usar seu aplicativo cliente para encontrar informações de destinatários, eles podem selecionar das listas de endereços disponíveis. Várias listas de endereços, como a lista de endereços global (GAL), são criadas por padrão. O Exchange contém as seguintes listas de endereços padrão, que depois são preenchidas automaticamente com novos usuários, contatos, grupos ou salas, à medida que eles forem adicionados à sua organização:

  - **Todos os Contatos**   Esta lista de endereços contém todos os contatos habilitados para email de sua organização. Os contatos habilitados para email são os destinatários que têm um endereço de email externo. Se você desejar que as informações de contatos habilitados para email estejam disponíveis a todos os usuários de sua organização, será necessário incluir o contato na GAL. Para saber mais sobre contatos de email, consulte [Destinatários](recipients-exchange-2013-help.md).

  - **Todas as Listas de Distribuição**   Esta lista de endereços contém grupos habilitados para email, como grupos de segurança habilitados para email, grupos de distribuição e grupos de distribuição dinâmicos em sua organização. Os grupos habilitados para email são listas de destinatários criados para agilizar o envio em massa de mensagens de email e outras informações. Quando uma mensagem de email é enviada para um grupo habilitado para email, todos os membros dessa lista recebem uma cópia da mensagem. Para saber mais sobre os grupos habilitados para email, consulte [Destinatários](recipients-exchange-2013-help.md).

  - **Todas as Salas**   Esta lista de endereços contém todos os recursos que foram designados como uma sala de sua organização. Salas são recursos da organização que podem ser agendados enviando uma solicitação de reunião a partir de um aplicativo cliente. A conta de usuário associada a uma sala fica desabilitada. Para saber mais sobre caixas de correio de recursos, consulte [Destinatários](recipients-exchange-2013-help.md).

  - **Todos os Usuários**   Esta lista de endereços contém todos os usuários habilitados para email de sua organização. Um usuário habilitado para email representa um usuário fora da organização do Exchange. Cada usuário habilitado para email tem um endereço de email externo. Todas as mensagens enviadas para usuários habilitados para email são roteadas para esse endereço de email externo. Um usuário habilitado para email é semelhante a um contato de email, com a diferença de que um usuário habilitado para email tem credenciais de logon do Active Directory e pode acessar recursos. Para saber mais sobre usuários habilitados para email, consulte [Destinatários](recipients-exchange-2013-help.md).

  - **Lista de Endereços Global Padrão**   Esta lista de endereços contém todos os usuários, contatos, grupos ou salas habilitados para email da organização. Durante a instalação, o Exchange cria várias listas de endereços padrão. A lista de endereços mais familiar é a GAL. Por padrão, a GAL contém todos os destinatários de uma organização do Exchange. Em outras palavras, qualquer objeto habilitado para caixa de correio ou para email em uma floresta do Active Directory que tenha o Exchange instalado está listado na GAL. Para facilitar o uso, a GAL é organizada por nome, não por endereço de email. Para obter mais informações, consulte [Criar uma lista de endereços global](create-a-global-address-list-exchange-2013-help.md).

  - **Pastas Públicas**   Esta lista de endereços contém todas as pastas públicas de sua organização. As permissões de acesso determinam quem pode exibir e usar as pastas. As pastas publicas são armazenadas em computadores com o Exchange. Para obter mais informações sobre pastas públicas no Exchange 2013, consulte [Pastas públicas](public-folders-exchange-2013-help.md). Para obter mais informações sobre pastas públicas no Exchange Online, consulte [Pastas públicas no Office 365 e Exchange Online](https://technet.microsoft.com/pt-br/library/jj200758\(v=exchg.150\)).

## Listas de endereços personalizadas

Uma organização do Exchange pode conter milhares de destinatários. Se você compilar todos os destinatários nas listas de endereços padrão, essas listas podem ficar muito grandes. Para evitar isso, você pode criar listas de endereços personalizadas para ajudar os usuários de sua organização a encontrar mais facilmente o que procuram.

Por exemplo, considere uma empresa com duas grandes divisões e uma organização do Exchange. Uma divisão, chamada Fourth Coffee, importa e vende grãos de café. A outra divisão, Contoso, Ltd, subscreve apólices de seguro. Para a maior parte das atividades diárias, os funcionários da Fourth Coffee não se comunicam com os funcionários da Contoso, Ltd. Portanto, para facilitar a busca de destinatários apenas em uma das divisões, você pode criar duas novas listas de endereços personalizadas - uma para a Fourth Coffee e outra para a Contoso, Ltd. Ao buscar destinatários em sua divisão, essas listas de endereços personalizadas permitem que os funcionários selecionem apenas a lista de endereços específica de sua divisão. Entretanto, se um funcionário não tiver certeza sobre a divisão em que o destinatário está, ele pode pesquisar na GAL, que contém todos os destinatários de ambas as divisões.

Você também pode criar subcategorias de listas de endereços chamadas listas de endereços hierárquicas. Por exemplo, você pode criar uma lista de endereços que contenha todos os destinatários em Manchester e outra com todos os em Stuttgart.

## Práticas recomendadas para criação de listas de endereços

Embora as listas de endereços sejam ferramentas úteis para usuários, listas de endereços mal planejadas podem ser frustrantes. Para garantir que suas listas de endereços sejam práticas para os usuários, considere as práticas recomendadas a seguir:

  - Evite criar tantas listas de endereços que os usuários não saibam em qual delas buscar os destinatários.

  - As listas de endereços devem facilitar aos usuários a localização de endereços na GAL.

  - Nomeie suas listas de endereços de modo que os usuários saibam imediatamente, ao olhar para elas, que tipos de destinatários estão contidos na lista. Se você tiver dificuldades para nomear as listas de endereços, crie menos listas e lembre os usuários de que eles podem encontrar qualquer pessoa da organização usando a GAL.
    

    > [!NOTE]
    > Por padrão, no Exchange Online, a função de Lista de Endereços não é atribuída a nenhum grupo de funções. Para usar quaisquer cmdlets que exijam a função Lista de Endereços, é necessário adicionar essa função a um grupo de funções. Para saber mais, confira a seção "Adicionar uma função a um grupo de funções" do tópico <A href="manage-role-groups-exchange-2013-help.md">Gerenciar grupos de função</A>.



Para obter instruções detalhadas sobre como criar uma lista de endereços no Exchange 2013, consulte [Criar uma lista de endereços](create-an-address-list-exchange-2013-help.md). Para obter instruções detalhadas sobre como criar uma lista de endereços no Exchange Online, consulte [Gerenciar listas de endereços no Exchange Online](https://technet.microsoft.com/pt-br/library/jj983798\(v=exchg.150\)).

