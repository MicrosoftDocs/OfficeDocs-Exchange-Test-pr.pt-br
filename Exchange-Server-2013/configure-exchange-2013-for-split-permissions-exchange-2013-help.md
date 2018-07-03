---
title: 'Configure o Exchange 2013 para permissões de divisão: Exchange 2013 Help'
TOCTitle: Configure o Exchange 2013 para permissões de divisão
ms:assetid: 8c74f893-a6f3-4869-8571-3bc0f662cc87
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Dd638155(v=EXCHG.150)
ms:contentKeyID: 50486121
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configure o Exchange 2013 para permissões de divisão

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2015-04-07_

Permissões de divisão permitem que dois grupos separados, como os administradores Active Directory e administradores de Exchange Server 2013 da Microsoft, para gerenciar seus respectivos serviços, objetos e atributos. Active Directory administradores gerenciam as entidades de segurança, como usuários, que fornecem permissões para acessar uma floresta Active Directory. Exchange administradores gerenciam as Exchange-relacionados atributos nos objetos Active Directory e Exchange-objeto específico de criação e gerenciamento.

Microsoft Exchange Server 2013 oferece os seguintes tipos de modelos de permissões de divisão:

  - **Permissões de divisão de RBAC**   Permissões para criar objetos de segurança na partição de domínio Active Directory são controladas pela função com base em acesso de controle (RBAC). Somente aqueles que são membros dos grupos de função adequada podem criar entidades de segurança.

  - **Permissões de divisão do Active Directory**   Permissões para criar objetos de segurança na partição de domínio Active Directory completamente são removidas do qualquer usuário Exchange, serviço ou servidor. Nenhuma opção é fornecida no RBAC para criar entidades de segurança. Criação de entidades de segurança no Active Directory deve ser executada usando as ferramentas de gerenciamento de Active Directory.
    

    > [!TIP]
    > as permissões de divisão de Active Directory estão disponíveis nas organizações que executa o Microsoft Exchange Server 2010 Service Pack 1 (SP1) ou posterior, ou ambas as versões do ExchangeExchange 2013.



O modelo que você escolher depende a estrutura e as necessidades da sua organização. Escolha o procedimento a seguir que se aplicam ao modelo do qual que você deseja configurar. Recomendamos que você use o modelo de permissões de divisão RBAC. O modelo de permissões de divisão RBAC fornece significativamente mais flexibilidade fornecendo a mesma separação de administração conforme Active Directory dividir permissões.

Para obter mais informações sobre compartilhados e divididos permissões, consulte [Compreendendo as permissões de divisão](understanding-split-permissions-exchange-2013-help.md).

Para obter mais informações sobre grupos de funções de gerenciamento, funções de gerenciamento e atribuições de função de gerenciamento comuns e de delegação, consulte os tópicos a seguir:

  - [Controle de acesso baseado em função de compreensão](understanding-role-based-access-control-exchange-2013-help.md)

  - [Noções básicas sobre grupos de funções de gerenciamento](understanding-management-role-groups-exchange-2013-help.md)

  - [Noções básicas sobre funções de gerenciamento](understanding-management-roles-exchange-2013-help.md)

  - [Noções básicas sobre as atribuições de função de gerenciamento](understanding-management-role-assignments-exchange-2013-help.md)

Procurando outras tarefas de gerenciamento relacionadas às permissões? Confira [Permissões avançadas](advanced-permissions-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para concluir cada procedimento: 5 minutos

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o entrada "permissões de divisão deActive Directory " no tópico [Permissões de gerenciamento de função](role-management-permissions-exchange-2013-help.md) .

  - Você deve usar o Windows PowerShell, Shell de comando do Windows ou ambos, para executar estes procedimentos. Para obter mais informações, consulte cada procedimento.

  - Se você tiver servidores Exchange 2010 em sua organização, o modelo de permissões que você selecionar também será aplicado para esses servidores.

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>.



## O que você deseja fazer?

## Alternar para dividir permissões de RBAC

Você pode configurar sua organização Exchange 2013 RBAC dividir permissões. Quando terminar, somente os administradores Active Directory será capazes de criar Active Directory entidades de segurança. Isso significa que os administradores Exchange não poderão usar os cmdlets a seguir:

  - **New-Mailbox**

  - **New-MailContact**

  - **New-MailUser**

  - **New-RemoteMailbox**

  - **Remove-Mailbox**

  - **Remove-MailContact**

  - **Remove-MailUser**

  - **Remove-RemoteMailbox**

administradores de Exchange só poderá gerenciar os atributos de Exchange em entidades de segurança Active Directory existente. No entanto, eles serão capazes de criar e gerenciar Exchange-objetos específicos, como regras de transporte e grupos de distribuição. Para obter mais informações, consulte a seção "Permissões de divisão de RBAC" em [Compreendendo as permissões de divisão](understanding-split-permissions-exchange-2013-help.md).

Para configurar Exchange 2013 para permissões de divisão, você deve atribuir a função de criação de destinatário de email e a função de criação de grupos de segurança e a associação a um grupo de função que contém os membros que estão Active Directory administradores. Em seguida, você deve remover as atribuições entre essas funções e qualquer grupo de função ou grupo de segurança universal (USG) que contém Exchange administradores.

Para configurar permissões de divisão de RBAC, faça o seguinte:

1.  Se sua organização estiver configurada para Active Directory dividir permissões, faça o seguinte em um prompt shell Windows.
    
    1.  Desabilite Active Directory dividir permissões executando o comando a seguir a partir da mídia de instalação Exchange 2013.
        
            setup.exe /PrepareAD /ActiveDirectorySplitPermissions:false
    
    2.  Reinicie os servidores de Exchange 2013 em sua organização ou aguardar até que o token de acesso Active Directory replicar para todos os servidores de Exchange 2013.
        

        > [!TIP]
        > Se você tiver servidores Exchange 2010 em sua organização, você também precisará reiniciar esses servidores.



2.  Faça o seguinte de Exchange Shell de gerenciamento:
    
    1.  Crie um grupo de funções para os administradores Active Directory. Além de criar o grupo de funções, o comando cria atribuições da função regular entre o novo grupo de função e a função de criação de destinatário de email e criação de grupos de segurança e função de associação.
        
            New-RoleGroup "Active Directory Administrators" -Roles "Mail Recipient Creation", "Security Group Creation and Membership"
        

        > [!TIP]
        > Se desejar que os membros desse grupo de função possam criar atribuições de função, inclua a função de gerenciamento de função. Você não precisa adicionar essa função agora. No entanto, se você nunca deseja atribuir a função de criação de destinatário de email ou a criação de grupos de segurança e a associação de função para os outros destinatários de função, a função de gerenciamento de função deve ser atribuída a esse novo grupo de função. Etapas a seguir configure o grupo de funções administradores Active Directory como o grupo de função única que pode delegar essas funções.

    
    2.  Crie delegação atribuições de função entre o novo grupo de função e a função de criação de destinatário de email e criação de grupos de segurança e função de associação usando os seguintes comandos.
        
            New-ManagementRoleAssignment -Role "Mail Recipient Creation" -SecurityGroup "Active Directory Administrators" -Delegating
            New-ManagementRoleAssignment -Role "Security Group Creation and Membership" -SecurityGroup "Active Directory Administrators" -Delegating
    
    3.  Adicione membros ao novo grupo de função usando o seguinte comando.
        
            Add-RoleGroupMember "Active Directory Administrators" -Member <user to add>
    
    4.  Substitua a lista de representantes no novo grupo de função para que apenas os membros do grupo de função podem adicionar ou remover membros.
        
            Set-RoleGroup "Active Directory Administrators" -ManagedBy "Active Directory Administrators"
        

        > [!IMPORTANT]
        > Membros do grupo de funções Gerenciamento da Organização ou aqueles que são atribuídos a função de gerenciamento de função, seja diretamente ou por meio de outro grupo de funções ou USG, poderá ignorar essa verificação de segurança de representante. Se você deseja impedir que qualquer administrador Exchange adicionando se ao novo grupo de função, você deve removem a atribuição de função entre a função de gerenciamento de função e qualquer administrador Exchange e atribuí-la para outro grupo de função.

    
    5.  Encontre todos os regulares e delegando atribuições de função para a função de criação de destinatário de email usando o seguinte comando. O comando exibe apenas as propriedades **Name**, **Role**e **RoleAssigneeName** .
        
            Get-ManagementRoleAssignment -Role "Mail Recipient Creation" | Format-Table Name, Role, RoleAssigneeName -Auto
    
    6.  Remova todos os regulares e delegando atribuições de função para a função de criação de destinatário de email que não estejam associadas um novo grupo de funções ou quaisquer outros grupos de função, USGs ou diretas atribuições que você deseja manter usando o seguinte comando.
        
            Remove-ManagementRoleAssignment <Mail Recipient Creation role assignment to remove>
        

        > [!TIP]
        > Se você deseja remover todos os regulares e delegando atribuições de função para a função de criação de destinatário de email em qualquer destinatário da função que não seja o grupo de funções administradores Active Directory, use o seguinte comando. A opção <EM>WhatIf</EM> permite ver quais atribuições de função serão removidas. Remover o comutador <EM>WhatIf</EM> e execute o comando novamente para remover as atribuições de função.

        
            Get-ManagementRoleAssignment -Role "Mail Recipient Creation" | Where { $_.RoleAssigneeName -NE "Active Directory Administrators" } | Remove-ManagementRoleAssignment -WhatIf
    
    7.  Encontre todos os regulares e delegando atribuições de função para a função de associação e de criação de grupos de segurança usando o seguinte comando. O comando exibe apenas as propriedades **Name**, **Role**e **RoleAssigneeName** .
        
            Get-ManagementRoleAssignment -Role "Security Group Creation and Membership" | Format-Table Name, Role, RoleAssigneeName -Auto
    
    8.  Remova todos os regulares e delegando atribuições de função para a função de associação e de criação de grupos de segurança que não estejam associadas um novo grupo de funções ou quaisquer outros grupos de função, USGs ou diretas atribuições que você deseja manter usando o seguinte comando.
        
            Remove-ManagementRoleAssignment <Security Group Creation and Membership role assignment to remove>
        

        > [!TIP]
        > Você pode usar o mesmo comando na observação anterior para remover todos os regulares e delegando atribuições de função para a função de criação de grupos de segurança e a associação no qualquer destinatário da função que não seja o grupo de função de administradores Active Directory, conforme mostrado neste exemplo.

        
            Get-ManagementRoleAssignment -Role "Security Group Creation and Membership" | Where { $_.RoleAssigneeName -NE "Active Directory Administrators" } | Remove-ManagementRoleAssignment -WhatIf

Para obter informações detalhadas sobre sintaxes e parâmetros, consulte os seguintes tópicos:

  - [New-RoleGroup](https://technet.microsoft.com/pt-br/library/dd638181\(v=exchg.150\))

  - [New-ManagementRoleAssignment](https://technet.microsoft.com/pt-br/library/dd335193\(v=exchg.150\))

  - [Add-RoleGroupMember](https://technet.microsoft.com/pt-br/library/dd638207\(v=exchg.150\))

  - [Set-RoleGroup](https://technet.microsoft.com/pt-br/library/dd638182\(v=exchg.150\))

  - [Get-ManagementRoleAssignment](https://technet.microsoft.com/pt-br/library/dd351024\(v=exchg.150\))

  - [Remove-ManagementRoleAssignment](https://technet.microsoft.com/pt-br/library/dd351205\(v=exchg.150\))

## Alternar para divididas permissões do Active Directory

Você pode configurar sua organização de Exchange 2013 para Active Directory dividir permissões. permissões de divisão de Active Directory remover completamente as permissões que permitem que administradores Exchange e servidores de criação de entidades de segurança em Active Directory ou modificação de atributos de não -Exchange esses objetos de. Quando terminar, somente os administradores Active Directory será capazes de criar Active Directory entidades de segurança. Isso significa que os administradores Exchange não poderão usar os cmdlets a seguir:

  - **Add-DistributionGroupMember**

  - **New-DistributionGroup**

  - **New-Mailbox**

  - **New-MailContact**

  - **New-MailUser**

  - **New-RemoteMailbox**

  - **Remove-DistributionGroup**

  - **Remove-DistributionGroupMember**

  - **Remove-Mailbox**

  - **Remove-MailContact**

  - **Remove-MailUser**

  - **Remove-RemoteMailbox**

  - **Update-DistributionGroupMember**

servidores e administradores Exchange apenas será capazes de gerenciar os atributos de Exchange nos entidades de segurança Active Directory existente. No entanto, eles serão capazes de criar e gerenciar Exchange-planos de discagem de objetos específicos, como regras de transporte e Unificação de mensagens.


> [!WARNING]
> Após habilitar Active Directory dividir permissões, servidores e administradores Exchange não mais poderão criar entidades de segurança no Active Directory e eles não poderão gerenciar a associação de grupo de distribuição. Essas tarefas devem ser executadas usando as ferramentas de gerenciamento de Active Directory com as permissões necessárias Active Directory. Antes de fazer essa alteração, você deve compreender o impacto que haverá nos seus processos de administração e os aplicativos de terceiros que integram com Exchange 2013 e o modelo de permissões de RBAC.<BR>Para obter mais informações, consulte a seção "permissões de divisão deActive Directory " <A href="understanding-split-permissions-exchange-2013-help.md">Compreendendo as permissões de divisão</A>.



Para alternar entre compartilhados ou RBAC dividir permissões para Active Directory dividir permissões, faça o seguinte:

1.  A partir de um shell de comando Windows, execute o seguinte comando na mídia de instalação Exchange 2013 para permitir que as permissões de divisão de Active Directory.
    
        setup.exe /PrepareAD /ActiveDirectorySplitPermissions:true

2.  Se você tiver vários domínios de Active Directory em sua organização, você deve executar `setup.exe /PrepareDomain` em cada domínio filho que contenha servidores Exchange ou objetos ou executar `setup.exe /PrepareAllDomains` a partir de um site que tenha um servidor Active Directory em qualquer domínio.

3.  Reinicie os servidores de Exchange 2013 em sua organização ou aguardar até que o token de acesso Active Directory replicar para todos os servidores de Exchange 2013.
    

    > [!TIP]
    > Se você tiver servidores Exchange 2010 em sua organização, você também precisará reiniciar esses servidores.


