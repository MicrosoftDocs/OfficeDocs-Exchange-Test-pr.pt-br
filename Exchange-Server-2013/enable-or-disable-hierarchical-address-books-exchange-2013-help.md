---
title: 'Habilitar/desabilitar catálogos de endereços hierárquicos: Exchange 2013 Help'
TOCTitle: Habilitar ou desabilitar catálogos de endereços hierárquico
ms:assetid: b4c3a175-ce5e-4bfb-a4a0-92d25f3644b3
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Ff607473(v=EXCHG.150)
ms:contentKeyID: 50486447
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Habilitar ou desabilitar catálogos de endereços hierárquico

 

_**Aplica-se a:** Exchange Online, Exchange Server 2013_

_**Tópico modificado em:** 2016-12-09_

Você pode configurar um catálogo de endereços hierárquico (HAB), que é um recurso disponíveis para usuários finais do Microsoft Outlook 2010 ou mais recente. Com um HAB, usuários podem procurar destinatários na sua organização Exchange usando uma hierarquia organizacional baseada em estrutura de tempo de serviço ou gestão. Para saber mais sobre HABs, consulte [Catálogos de endereços hierárquicos](https://docs.microsoft.com/pt-br/exchange/address-books/hierarchical-address-books/hierarchical-address-books).

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: 1 hora.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Grupos de distribuição" no tópico [Permissões de destinatários](recipients-permissions-exchange-2013-help.md).

  - Você não pode usar o Centro de Administração do Exchange (EAC) para executar esse procedimento. É necessário usar o Shell.

  - Antes de começar, leia o tópico [Catálogos de endereços hierárquicos](https://docs.microsoft.com/pt-br/exchange/address-books/hierarchical-address-books/hierarchical-address-books). Você deve compreender se um HAB é apropriado para a sua organização do Exchange.

  - Entenda como as unidades organizacionais (UOs), grupos, usuários e contatos estão configurados atualmente em sua organização do Exchange.

  - Entenda os cmdlets e os parâmetros associados, que são necessários para configurar um HAB, na tabela a seguir.
    
    
    <table>
    <colgroup>
    <col style="width: 50%" />
    <col style="width: 50%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th>Cmdlet</th>
    <th>Parâmetro</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td><p><a href="https://technet.microsoft.com/pt-br/library/aa997443(v=exchg.150)">Set-OrganizationConfig</a></p></td>
    <td><p><em>HierarchicalAddressBookRoot</em></p></td>
    </tr>
    <tr class="even">
    <td><p><a href="https://technet.microsoft.com/pt-br/library/bb123770(v=exchg.150)">Set-Group</a></p></td>
    <td><p><em>IsHierarchicalGroup</em></p>
    <p><em>SeniorityIndex</em></p>
    <p><em>PhoneticDisplayName</em></p></td>
    </tr>
    <tr class="odd">
    <td><p><a href="https://technet.microsoft.com/pt-br/library/aa998221(v=exchg.150)">Set-User</a></p></td>
    <td><p><em>SeniorityIndex</em></p>
    <p><em>PhoneticDisplayName</em></p></td>
    </tr>
    <tr class="even">
    <td><p><a href="https://technet.microsoft.com/pt-br/library/bb124535(v=exchg.150)">Set-Contact</a></p></td>
    <td><p><em>SeniorityIndex</em></p>
    <p><em>PhoneticDisplayName</em></p></td>
    </tr>
    </tbody>
    </table>


  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>.



## O que você deseja fazer?

## Usar o Shell para habilitar um HAB


> [!TIP]
> Embora não seja possível usar o EAC para habilitar HABs, após habilitar o HAB você poderá usar o EAC para gerenciar a associação dos grupos na hierarquia organizacional.



Neste exemplo, uma UO chamada HAB será criada para o HAB. O nome do domínio para a organização é Contoso-dom, e Contoso,Ltd será o nome da organização de nível superior na hierarquia (a *organização raiz*). Grupos subordinados chamados Corporate Office, Product Support Organization e Sales & Marketing Organization serão criados como organizações filhas sob Contoso,Ltd. Adicionalmente, os grupos Human Resources, Accounting Group e Administration Group serão criados como organizações filhas sob Corporate Office.

Para obter informações detalhadas sobre a criação de grupos dinâmicos de distribuição, consulte [Criar e gerenciar grupos de distribuição](https://docs.microsoft.com/pt-br/exchange/recipients-in-exchange-online/manage-distribution-groups/manage-distribution-groups).

1.  Crie uma UO chamada HAB na organização Contoso. Você pode usar Usuários e Computadores do Active Directory ou digitar o seguinte em um prompt de comando.
    

    > [!TIP]
    > Alternativamente, você pode usar uma UO existente em sua floresta do Exchange.

    
        dsadd ou "OU=HAB,DC=Contoso-dom,DC=Contoso,DC=com"
    

    > [!TIP]
    > Para obter informações detalhadas, consulte <A href="https://go.microsoft.com/fwlink/p/?linkid=198986">criar uma nova unidade organizacional</A>.



2.  Crie o grupo de distribuição raiz Contoso,Ltd para o HAB.
    

    > [!TIP]
    > Para os fins deste tópico, o exemplo do Shell é fornecido. Entretanto, você também pode usar o EAC para criar um grupo de distribuição. Para obter detalhes, consulte <A href="https://docs.microsoft.com/pt-br/exchange/recipients-in-exchange-online/manage-distribution-groups/manage-distribution-groups">Criar e gerenciar grupos de distribuição</A>.

    
        New-DistributionGroup -Name "Contoso,Ltd" -DisplayName "Contoso,Ltd" -Alias "ContosoRoot" -OrganizationalUnit "Contoso-dom.Contoso.com/HAB" -SamAccountName "ContosoRoot" -Type "Distribution"

3.  Designe Contoso,Ltd como organização raiz do HAB.
    
        Set-OrganizationConfig -HierarchicalAddressBookRoot "Contoso,Ltd"

4.  Crie grupos de distribuição para as outras camadas do HAB. Para este exemplo, você criaria os seguintes grupos: Corporate Office, Product Support Organization, Sales & Marketing Organization, Human Resources, Accounting Group e Administration Group. Este exemplo cria o grupo de distribuição Corporate Office.
    

    > [!TIP]
    > Para os fins deste tópico, o exemplo do Shell é fornecido. Entretanto, você também pode usar o EAC para criar grupos de distribuição. Para detalhes, consulte <A href="https://docs.microsoft.com/pt-br/exchange/recipients-in-exchange-online/manage-distribution-groups/manage-distribution-groups">Criar e gerenciar grupos de distribuição</A>.

    
        New-DistributionGroup -Name "Corporate Office" -DisplayName "Corporate Office" -Alias "CorporateOffice" -OrganizationalUnit "Contoso-dom.Contoso.com/HAB" -SamAccountName "CorporateOffice" -Type "Distribution"

5.  Designe cada um dos grupos como membro do HAB. Para este exemplo, você designaria os seguintes grupos como grupos hierárquicos: Contoso,Ltd, Corporate Office, Product Support Organization, Sales & Marketing Organization, Human Resources, Accounting Group e Administration Group. Este exemplo designa o grupo de distribuição Contoso,Ltd como membro do HAB.
    
        Set-Group -Identity "Contoso,Ltd" -IsHierarchicalGroup $true

6.  Adicione cada grupo subordinado como membro da organização raiz. Para este exemplo, os grupos de distribuição Corporate Office, Product Support Organization, e Sales & Marketing Organization são adicionados como membros da organização raiz Contoso,Ltd no HAB. Este exemplo adiciona o grupo de distribuição Corporate Office como membro do grupo de distribuição raiz Contoso,Ltd.
    

    > [!TIP]
    > Este exemplo usa o alias dos grupos de distribuição.

    
        Add-DistributionGroupMember -Identity "ContosoRoot" -Member "CorporateOffice"

7.  Adicione cada grupo subordinado ao grupo de distribuição Corporate Office como membro do grupo. Para este exemplo, os grupos de distribuição Human Resources, Accounting Group e Administration Group são adicionados como membros do grupo de distribuição Corporate Office. Este exemplo adiciona o grupo de distribuição Human Resources como membro do grupo de distribuição Corporate Office.
    

    > [!TIP]
    > Este exemplo usa o alias dos grupos de distribuição e presume que o alias do grupo de distribuição Human Resources seja HumanResources.

    
        Add-DistributionGroupMember -Identity "CorporateOffice" -Member "HumanResources"

8.  Adicione usuários aos grupos no HAB. Para este exemplo, David Hamilton (endereço SMTP DHamilton@contoso.com) é um usuário existente na UO Contoso-dom.Contoso.com/Users e será adicionado ao grupo Corporate Office. Repita essa etapa para adicionar outros usuários a grupos no HAB.
    
        Add-DistributionGroupMember -Identity "CorporateOffice" -Member "DHamilton"

9.  Defina o parâmetro *SeniorityIndex* para grupos no HAB. Para este exemplo, o grupo Corporate Office contém três grupos filhos: Human Resources, Accounting Group e Administration Group. Em vez de listar os grupos em ordem alfabética crescente, que é o padrão, a classificação preferencial será Human Resources (*SeniorityIndex* = 100), Accounting Group (*SeniorityIndex* = 50) e depois Administration Group (*SeniorityIndex* = 25). Este exemplo define o parâmetro *SeniorityIndex* para o grupo Human Resources como 100.
    
        Set-Group -Identity "Human Resources" -SeniorityIndex 100
    

    > [!TIP]
    > O parâmetro <EM>SeniorityIndex</EM> é um valor numérico usado para classificar grupos ou usuários em ordem numérica decrescente em um HAB. Se o parâmetro <EM>SeniorityIndex</EM> não for definido ou for igual para dois ou mais usuários, a ordem de classificação do HAB usará o valor do parâmetro <EM>PhoneticDisplayName</EM> para listar os usuários em ordem alfabética crescente. Se o valor <EM>PhoneticDisplayName</EM> não for definido, a ordem de classificação do HAB adotará como padrão o valor do parâmetro <EM>DisplayName</EM> e listará os usuários em ordem alfabética crescente.



10. Defina o parâmetro *SeniorityIndex* para usuários nos grupos do HAB. Para este exemplo, o grupo Corporate Office contém três usuários: Amy Alberts, David Hamilton e Rajesh M. Patel. Em vez de listar os usuários em ordem alfabética crescente por padrão, a classificação preferencial será David Hamilton (*SeniorityIndex* = 100), Rajesh M. Patel (*SeniorityIndex* = 50) e depois Amy Alberts (*SeniorityIndex* = 25). Este exemplo define o parâmetro *SeniorityIndex* para o usuário David Hamilton como 100.
    
        Set-User -Identity "DHamilton@contoso.com" -SeniorityIndex 100

Após a conclusão das etapas anteriores, o HAB estará visível no Outlook. Para exibir o HAB, abra o Outlook e clique em **Catálogo de Endereços**. O HAB é exibido na guia **Organização**, como é mostrado na figura a seguir.

**HAB de exemplo para Contoso,Ltd**

![Caixa de diálogo Catálogo de Endereços Hierárquico](images/Ff607473.d8cc782f-61cd-44c4-9c74-432ebea0c3db(EXCHG.150).gif "Caixa de diálogo Catálogo de Endereços Hierárquico")

Após criar o HAB, você poderá usar o EAC para gerenciar a associação dos grupos na hierarquia organizacional. Entretanto, é necessário usar o Shell para modificar o parâmetro *SeniorityIndex* de qualquer novo grupo ou usuário.

Para obter informações detalhadas sobre sintaxe e parâmetros, consulte os seguintes tópicos:

  - [New-DistributionGroup](https://technet.microsoft.com/pt-br/library/aa998856\(v=exchg.150\))

  - [Set-OrganizationConfig](https://technet.microsoft.com/pt-br/library/aa997443\(v=exchg.150\))

  - [Set-Group](https://technet.microsoft.com/pt-br/library/bb123770\(v=exchg.150\))

  - [Add-DistributionGroupMember](https://technet.microsoft.com/pt-br/library/bb124340\(v=exchg.150\))

  - [Set-User](https://technet.microsoft.com/pt-br/library/aa998221\(v=exchg.150\))

## Usar o Shell para desabilitar um catálogo de endereços hierárquico

Este exemplo desabilita a organização raiz usada para o HAB.

    Set-OrganizationConfig -HierarchicalAddressBookRoot $null


> [!TIP]
> Este comando não exclui a organização raiz ou os grupos filhos usados na estrutura do HAB, nem redefine os valores de <EM>SeniorityIndex</EM> para grupos ou usuários. Ele apenas impede que o HAB seja exibido no Outlook. Para habilitar novamente o HAB com os mesmos parâmetros de configuração, basta habilitar novamente a organização raiz.



Para informações detalhadas de sintaxes e de parâmetros, consulte [Set-OrganizationConfig](https://technet.microsoft.com/pt-br/library/aa997443\(v=exchg.150\)).

