---
title: 'Criar um escopo de gerenciamento personalizado para pesquisas de Descoberta Eletrônica In-loco: Exchange 2013 Help'
TOCTitle: Criar um escopo de gerenciamento personalizado para pesquisas de Descoberta Eletrônica In-loco
ms:assetid: 1543aefe-3709-402c-b9cd-c11fe898aad1
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Dn741464(v=EXCHG.150)
ms:contentKeyID: 62219840
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Criar um escopo de gerenciamento personalizado para pesquisas de Descoberta Eletrônica In-loco

 

_**Aplica-se a:**Exchange Online, Exchange Server 2013_

_**Tópico modificado em:**2015-01-21_

Você pode usar um escopo de gerenciamento personalizado para permitir que pessoas ou grupos específicos usem a Descoberta Eletrônica In-loco para pesquisar um subconjunto de caixas de correio em sua organização do Exchange 2013 ou do Exchange Online. Por exemplo, convém permitir que um gerente de descoberta pesquise apenas as caixas de correio de usuários em um local ou departamento específico. Você pode fazer criando um escopo de gerenciamento personalizado. Esse escopo de gerenciamento personalizado usa um filtro de destinatário para controlar quais caixas de correio podem ser pesquisadas. Escopos de filtro de destinatário usam filtros para direcionar a destinatários específicos com base no tipo de destinatário ou em outras propriedades de destinatário.

Para a Descoberta In-loco, a única propriedade em uma caixa de correio de usuário de usuário que você pode usar para criar um filtro de destinatário para um escopo personalizado é a associação de grupo de distribuição (o nome real da propriedade é *MemberOfGroup*). Se você usar outras propriedades, como *CustomAttributeN*, *Department* ou *PostalCode*, a pesquisa falhará quando for executada por um membro do grupo de função que recebeu o escopo personalizado.

Para saber mais sobre escopos de gerenciamento, consulte:

  - [Noções básicas sobre escopos da função de gerenciamento](understanding-management-role-scopes-exchange-2013-help.md)

  - [Noções básicas sobre filtros do escopo de função de gerenciamento](understanding-management-role-scope-filters-exchange-2013-help.md)

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: 15 minutos

  - Conforme indicado anteriormente, você pode usar a associação de grupo apenas como o filtro de destinatário para criar um escopo de filtro de destinatário personalizado a fim de ser usado para Descoberta Eletrônica. Outras propriedades de destinatário não podem ser usadas para criar um escopo personalizado para pesquisas de Descoberta Eletrônica. Observe que também não é possível usar a associação em um grupo de distribuição dinâmica.

  - Execute as etapas um a três para permitir que um gerente de descoberta exporte os resultados de uma pesquisa de Descoberta Eletrônica que usa um escopo de gerenciamento personalizado.

  - Se seu gerente de descoberta não precisar visualizar os resultados da pesquisa, vá para a etapa 4.

  - Se seu gerente de descoberta não precisar copiar os resultados da pesquisa, vá para a etapa 5.

## Etapa 1: organizar os usuários em grupos de distribuição para Descoberta Eletrônica

Para pesquisar uma sub-rede de caixas de correio em sua organização ou para estreitar o escopo de caixas de correio de origem no qual um gerente de descoberta pode pesquisar, será necessário agrupar o subconjunto de caixas de correio em um ou mais grupos de distribuição. Quando você cria um escopo de gerenciamento personalizado na etapa 2, você usa esses grupos de distribuição como o filtro de destinatário para criar um escopo de gerenciamento personalizado. Isso permite que um gerente de descoberta pesquise apenas as caixas de correio dos usuários membros de um grupo especificado.

Você pode usar grupos de distribuição existentes para fins de Descoberta Eletrônica ou pode criar novos. Consulte Mais informações ao final deste tópico para obter dicas sobre como criar grupos de distribuição que podem ser usados para definir escopos de pesquisas de Descoberta Eletrônica.

## Etapa 2: criar um escopo de gerenciamento personalizado

Agora, você criará um escopo de gerenciamento personalizado definido pela associação de um grupo de distribuição (usando o filtro de destinatário *MemberOfGroup*). Quando esse escopo for aplicado a um grupo de função usado para Descoberta Eletrônica, os membros do grupo de função poderão pesquisar nas caixas de correio dos usuários membros do grupo de distribuição usado para criar o escopo de gerenciamento personalizado.

Esse procedimento usa os comandos do Shell de Gerenciamento do Exchange para criar um escopo personalizado chamado Ottawa Users eDiscovery Scope. Ele especifica o grupo de distribuição chamado Ottawa Users para o filtro de destinatário do escopo personalizado.

1.  Execute este comando para obter e salvar as propriedades do grupo Ottawa Users em uma variável, que serão usadas no próximo comando.
    
        $DG = Get-DistributionGroup -Identity "Ottawa Users"

2.  Execute este comando para criar um escopo de gerenciamento personalizado com base na associação do grupo de distribuição Ottawa Users.
    
        New-ManagementScope "Ottawa Users eDiscovery Scope" -RecipientRestrictionFilter "MemberOfGroup -eq '$($DG.DistinguishedName)'"
    
    O nome diferenciado do grupo de distribuição, contido na variável **$DG**, é usado para criar o filtro de destinatário para o novo escopo de gerenciamento.

## Etapa 3: criar um grupo de funções de gerenciamento

Nesta etapa, crie um novo grupo de função de gerenciamento e atribua o escopo personalizado criado na etapa 2. Adicione as funções Retenção legal e Pesquisa de caixa de correio de modo que os membros do grupo de função possam executar pesquisas de Descoberta Eletrônica In-loco e colocar as caixas de correio em Bloqueio In-loco ou Retenção de litígio. Você também pode adicionar membros a este grupo de função de modo que eles possam pesquisar nas caixas de correio dos membros do grupo de distribuição usado para criar o escopo personalizado na etapa 2.

Nos exemplos a seguir, o grupo de segurança Ottawa Users eDiscovery Managers será adicionado como membro deste grupo de função. Você pode usar o Shell ou o EAC para esta etapa.

## Usar o Shell para criar um grupo de funções de gerenciamento

Execute este comando para criar um novo grupo de função que usa o escopo personalizado criado na etapa 2. O comando também adiciona as funções de Retenção legal e Pesquisa de caixa de correio, e adiciona o grupo de segurança Ottawa Users eDiscovery Managers como membro do novo grupo de função.

    New-RoleGroup "Ottawa Discovery Management" -Roles "Mailbox Search","Legal Hold" -CustomRecipientWriteScope "Ottawa Users eDiscovery Scope" -Members "Ottawa Users eDiscovery Managers"

## Usar o EAC para criar um grupo de função

1.  No EAC, navegue até **Permissões** \> **Funções de administrador** e clique em **Novo**![Ícone Adicionar](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Ícone Adicionar").

2.  Em **Novo grupo de função**, forneça as seguintes informações:
    
      - **Nome**   Forneça um nome descritivo para o novo grupo de função. Para este exemplo, use **Gerenciamento de descoberta de Ottawa**.
    
      - **Escopo de gravação**   Selecione o escopo de gerenciamento personalizado criado na etapa 2. Esse escopo será aplicado ao novo grupo de função.
    
      - **Funções**   Clique em **Adicionar**![Ícone Adicionar](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Ícone Adicionar") e adicione as funções **Retenção legal** e **Pesquisa de caixa de correio** ao novo grupo de função.
    
      - **Membros**   Clique em **Adicionar**![Ícone Adicionar](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Ícone Adicionar") e selecione os usuários, o grupo de segurança ou os grupos de função que você deseja adicionar como membros do novo grupo de função. Para este exemplo, os membros do grupo de segurança **Ottawa Users eDiscovery Managers** poderão pesquisar apenas as caixas de correio de usuários membros do grupo de distribuição **Ottawa Users**.

3.  Clique em **Salvar** para criar o grupo de funções.
    
    Veja um exemplo da aparência da janela **Novo grupo de função** quando você terminar.
    
    ![Criar um novo grupo de função para um escopo personalizado](images/Dn741464.a6e3419f-d5d9-404f-890d-ad35f499756f(EXCHG.150).gif "Criar um novo grupo de função para um escopo personalizado")  

## (Opcional) Etapa 4: adicionar gerentes de descoberta como membros do grupo de distribuição usado para criar o escopo de gerenciamento personalizado

Será necessário executar essa etapa somente se você quiser permitir que o gerente de descoberta visualize os resultados de pesquisa de Descoberta Eletrônica.

Execute esse comando para adicionar o grupo de segurança Ottawa Users eDiscovery Managers como membro do grupo de distribuição Ottawa Users.

    Add-DistributionGroupMember -Identity "Ottawa Users" -Member "Ottawa Users eDiscovery Managers"

Você também pode usar o EAC para adicionar membros a um grupo de distribuição. Para obter mais informações, consulte [Criar e gerenciar grupos de distribuição](create-and-manage-distribution-groups-exchange-2013-help.md).

## (Opcional) Etapa 5: adicionar uma caixa de correio de descoberta como membro do grupo de distribuição usado para criar o escopo de gerenciamento personalizado

Será necessário executar essa etapa somente se você quiser permitir que o gerente de descoberta copie os resultados de pesquisa de Descoberta Eletrônica.

Execute esse comando para adicionar uma caixa de correio de descoberta chamada Ottawa Discovery Mailbox como membro do grupo de distribuição Ottawa Users.

    Add-DistributionGroupMember -Identity "Ottawa Users" -Member "Ottawa Discovery Mailbox"


> [!TIP]
> Para abrir uma caixa de correio de descoberta e ver os resultados da pesquisa, os gerentes de descoberta precisam receber permissões de Acesso Completo para a caixa de correio de descoberta. Para obter mais informações, consulte <A href="create-a-discovery-mailbox-exchange-2013-help.md">Criar uma caixa de correio de descoberta</A>.



## Como saber se funcionou?

Veja algumas maneiras de verificar se você implementou com êxito os escopos de gerenciamento personalizados para Descoberta Eletrônica. Ao verificar, verifique se o usuário que está executando as pesquisas de Descoberta Eletrônica é membro do grupo de função que usa o escopo de gerenciamento personalizado.

  - Crie uma pesquisa de Descoberta Eletrônica e selecione o grupo de distribuição usado para criar o escopo de gerenciamento personalizado como a fonte de caixas de correio a ser pesquisada. Todas as caixas de correio devem ser pesquisadas com êxito.

  - Crie uma pesquisa de Descoberta Eletrônica e pesquise nas caixas de correio dos usuários que não são membros do grupo de distribuição usado para criar o escopo de gerenciamento personalizado. A pesquisa deve falhar, pois o gerente de descoberta pode pesquisar apenas nas caixas de correio de usuários membros do grupo de distribuição usado para criar o escopo de gerenciamento personalizado. Nesse caso, um erro como "Não é possível pesquisar na caixa de correio \<*nome da caixa de correio*\>, pois o usuário atual não tem permissões para acessar a caixa de correio" retornará.

  - Crie uma pesquisa de Descoberta Eletrônica e pesquise nas caixas de correio dos usuários membros do grupo de distribuição usado para criar o escopo de gerenciamento personalizado. Na mesma pesquisa, inclua as caixas de correio de usuários que não são membros. A pesquisa deve ter um êxito parcial. As caixas de correio de membros do grupo de distribuição usado para criar o escopo de gerenciamento personalizado devem ser pesquisadas com êxito. A pesquisa de caixas de correio para os usuários que não são membros do grupo deve falhar.

## Mais informações

  - Como os grupos de distribuição são usados nesse cenário para definir o escopo das pesquisas de Descoberta Eletrônica e não para entrega de mensagens, considere o seguinte ao criar e configurar grupos de distribuição para a Descoberta Eletrônica:
    
      - Crie grupos de distribuição com uma associação fechada, assim os membros podem ser adicionados ou removidos do grupo somente pelos proprietários do grupo. Se você estiver criando o grupo no Shell, use a sintaxe `MemberJoinRestriction closed` e `MemberDepartRestriction closed`.
    
      - Habilite a moderação do grupo de modo que qualquer mensagem enviada ao grupo seja enviada primeiro aos moderadores do grupo, que podem aprovar ou rejeitar a mensagem, conforme o apropriado. Se você estiver criando o grupo no Shell, use a sintaxe `ModerationEnabled $true`. Se você estiver usando o EAC, será possível habilitar a moderação após a criação do grupo.
    
      - Oculte o grupo de distribuição do catálogo de endereços compartilhado da organização. Use o EAC ou o cmdlet **Set-DistributionGroup** após a criação do grupo. Se você estiver usando o Shell, use a sintaxe `HiddenFromAddressListsEnabled $true`.
    
    No exemplo a seguir, o primeiro comando cria um grupo de distribuição com associação fechada e moderação habilitada. O segundo comando oculta o grupo do catálogo de endereços compartilhado.
    
        New-DistributionGroup -Name "Vancouver Users eDiscovery Scope" -Alias VancouverUserseDiscovery -MemberJoinRestriction closed -MemberDepartRestriction closed -ModerationEnabled $true
    
        Set-DistributionGroup "Vancouver Users eDiscovery Scope" -HiddenFromAddressListsEnabled $true
    
    Para obter mais informações sobre como criar e gerenciar grupos de distribuição, consulte [Criar e gerenciar grupos de distribuição](create-and-manage-distribution-groups-exchange-2013-help.md).

  - Embora seja possível usar a associação de grupo de distribuição apenas como o filtro de destinatário de um escopo de gerenciamento personalizado usado para Descoberta Eletrônica, você poderá usar outras propriedades de destinatário para adicionar usuários a esse grupo de distribuição. Veja alguns exemplos de como usar os cmdlets **Get-Mailbox** e **Get-Recipient** para retornar um grupo específico de usuários com base em atributos comuns de usuário ou de caixa de correio.
    
        Get-Recipient -RecipientTypeDetails UserMailbox -ResultSize unlimited -Filter 'Department -eq "HR"'
    
        Get-Mailbox -RecipientTypeDetails UserMailbox -ResultSize unlimited -Filter 'CustomAttribute15 -eq "VancouverSubsidiary"'
    
        Get-Recipient -RecipientTypeDetails UserMailbox -ResultSize unlimited -Filter 'PostalCode -eq "98052"'
    
        Get-Recipient -RecipientTypeDetails UserMailbox -ResultSize unlimited -Filter 'StateOrProvince -eq "WA"'
    
        Get-Mailbox -RecipientTypeDetails UserMailbox -ResultSize unlimited -OrganizationalUnit "namsr01a002.sdf.exchangelabs.com/Microsoft Exchange Hosted Organizations/contoso.onmicrosoft.com"

  - Em seguida, você pode usar os exemplos do marcador anterior para criar uma variável que possa ser usada com o cmdlet **Add-DistributionGroupMember** a fim de adicionar um grupo de usuários a um grupo de distribuição. No exemplo a seguir, o primeiro comando cria uma variável com todas as caixas de correio de usuário que contenham o valor **Vancouver** para a propriedade *Department* na conta de usuário. O segundo comando adiciona esses usuários ao grupo de distribuição Vancouver Users.
    
        $members = Get-Recipient -RecipientTypeDetails UserMailbox -ResultSize unlimited -Filter 'Department -eq "Vancouver"'
    
        $members | ForEach {Add-DistributionGroupMember "Ottawa Users" -Member $_.Name}

  - Você pode usar o cmdlet **Add-RoleGroupMember** para adicionar um membro a um grupo de função existente usado para definir o escopo de pesquisas de Descoberta Eletrônica. Por exemplo, o comando a seguir adiciona o usuário admin@ottawa.contoso.com ao grupo de função Gerenciamento de descoberta de Ottawa.
    
        Add-RoleGroupMember "Vancouver Discovery Management" -Member paralegal@vancouver.contoso.com
    
    Você também pode usar o EAC para adicionar membros a um grupo de funções. Para obter mais informações, consulte a seção "Adicionar membros a um grupo de funções" no [Gerenciar membros do grupo de função](manage-role-group-members-exchange-2013-help.md).

  - Exchange Online, um escopo de gerenciamento personalizado usado para descoberta eletrônica não pode ser usado para pesquisar caixas de correio inativas. Isso ocorre porque uma caixa de correio inativa não pode ser um membro de um grupo de distribuição. Por exemplo, suponha que um usuário é um membro de um grupo de distribuição que foi usado para criar um escopo de gerenciamento personalizado para descoberta eletrônica. Depois que o usuário sai da organização e suas caixas de correio é feita inativa (por colocar um litígio ou In-loco bloqueio na caixa de correio e excluindo a conta de usuário correspondente do Office 365). O resultado é que o usuário será removido como membro do grupo de distribuição, incluindo o grupo que foi usado para criar o escopo de gerenciamento personalizado usado para descoberta eletrônica. Se um gerente de descoberta (que é um membro do grupo de função que atribuiu o escopo de gerenciamento personalizado) tentam pesquisar a caixa de correio inativa, a pesquisa falhará. Para pesquisar caixas de correio inativas, um gerente de descoberta deve ser membro do grupo de funções de gerenciamento de descoberta ou qualquer grupo de função que tenha permissões para pesquisar toda a organização.
    
    Para obter mais informações sobre caixas de correio inativas, consulte [Caixas de correio inativas no Exchange Online](https://technet.microsoft.com/pt-br/library/dn798632\(v=exchg.150\)).

