---
title: 'Criar grupos de função vinculado que espelham grupos de função internos: Exchange 2013 Help'
TOCTitle: Criar grupos de função vinculado que espelham grupos de função internos
ms:assetid: 89dfcbb3-0568-4bbf-a885-746b91ba307e
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Dd876918(v=EXCHG.150)
ms:contentKeyID: 50486111
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Criar grupos de função vinculado que espelham grupos de função internos

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2012-10-03_

Usando grupos de funções de gerenciamento vinculadas no Microsoft Exchange Server 2013, você pode vincular um grupo de funções em uma floresta de recurso Exchange 2013 com um grupo de segurança universal (USG) em uma floresta de usuário externo. Isso é útil quando você deseja que os administradores com contas na floresta de usuário para gerenciar os servidores que executam o Exchange na floresta de recursos. Para obter mais informações sobre grupos de função vinculado, consulte [Noções básicas sobre grupos de funções de gerenciamento](understanding-management-role-groups-exchange-2013-help.md).

Por padrão, Exchange 2013 inclui um número de grupos de função internos que fornecem as permissões para gerenciar uma variedade de recursos e funções de trabalho. Cada grupo de função é adaptado para fornecer permissões específicas para cada função de recurso e trabalho. No entanto, esses grupos de função não podem ser vinculados a USGs em uma floresta externa. Eles só podem conter usuários e USGs da floresta de recurso local. Felizmente, é possível replicar esses grupos de função internos usando os grupos de função vinculado.

Você pode recriar cada grupo de funções internas como um grupo de função vinculado. Todas as funções de gerenciamento e escopos de gerenciamento atribuídos a cada grupo de função são adicionadas ao novo grupo de função vinculado. Para obter mais informações sobre escopos e funções de gerenciamento, consulte os tópicos a seguir:

  - [Noções básicas sobre funções de gerenciamento](understanding-management-roles-exchange-2013-help.md)

  - [Noções básicas sobre escopos da função de gerenciamento](understanding-management-role-scopes-exchange-2013-help.md)

Procurando outras tarefas de gerenciamento relacionadas a grupos de funções? Confira [Permissões](permissions-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para finalizar cada procedimento: 10 minutos

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Grupos de função" no tópico [Permissões de gerenciamento de função](role-management-permissions-exchange-2013-help.md) .

  - Você deve usar o Shell para executar estes procedimentos.

  - Configurar um grupo de função vinculado requer uma relação de confiança unidirecional entre a floresta de Active Directory de recursos no qual residirá o grupo de função vinculado e estrangeira Active Directory floresta em que os usuários ou USGs residem. Floresta de recursos deve confiar na floresta externa.

  - Você deve possuir as seguintes informações sobre a floresta externa do Active Directory:
    
      - **Credenciais**   Você deve ter um nome de usuário e senha que pode acessar a floresta estrangeira Active Directory. Essa informação é usada com o parâmetro *LinkedCredential* no cmdlet **New-RoleGroup** . Essas informações são obtidas executando o cmdlet **Get-Credential** . O formato do nome do usuário é *domain*\\*username*.
    
      - **Controlador de domínio**   Você deve ter um nome de domínio totalmente qualificado (FQDN) de um controlador de domínio do Active Directory na floresta externa do Active Directory. Essa informação é usada com o parâmetro *LinkedDomainController* no cmdlet **New-RoleGroup**.
    
      - **USG Externo** Você deve ter o nome completo de um USG na floresta externa do Active Directory que contenha os membros que você deseja associar ao grupo de função vinculado. Essa informação é usada com o parâmetro *LinkedForeignGroup* no cmdlet **New-RoleGroup**.

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>.



## Usar o Shell para criar grupos de função vinculado que replicar grupos de função internos

Cada uma das seções a seguir mostra como criar novamente a cada grupo de função como um grupo de função vinculado. Conclua os procedimentos em cada seção para recriar todos os grupos de função internos como grupos de função vinculado.

## Criar o grupo de função vinculado de gerenciamento da organização

Para recriar o grupo de funções Gerenciamento da Organização como um grupo de função vinculado, você deve executar um procedimento que é diferente do procedimento usado para recriar em outros grupos de função internos. Isso ocorre porque o grupo de funções Gerenciamento da Organização tem delegando atribuições de função entre ele e todas as funções de gerenciamento. Criar novamente as atribuições da função de delegação requer uma etapa adicional.

1.  Crie um USG na floresta externa que será vinculada ao grupo de funções Gerenciamento da Organização.

2.  Armazene as credenciais da floresta externa do Active Directory em uma variável.
    
        $ForeignCredential = Get-Credential

3.  Armazene todas as funções atribuídas ao grupo de função do Gerenciamento da Organização em uma variável.
    
        $OrgMgmt  = Get-RoleGroup "Organization Management"

4.  Crie o grupo de função vinculado Gerenciamento da Organização e adicione as funções atribuídas ao grupo de funções internas Gerenciamento da Organização.
    
        New-RoleGroup "Organization Management - Linked" -LinkedForeignGroup <name of foreign USG> -LinkedDomainController <FQDN of foreign Active Directory domain controller> -LinkedCredential $ForeignCredential -Roles $OrgMgmt.Roles

5.  Remover todas as atribuições regulares entre o novo grupo de função vinculado Gerenciamento da Organização e a minha \* funções de usuário final.
    
        Get-ManagementRoleAssignment -RoleAssignee "Organization Management - Linked" -Role My* | Remove-ManagementRoleAssignment

6.  Adicione as atribuições de função de delegação entre o novo grupo de função vinculado Gerenciamento da Organização e todas as funções de gerenciamento.
    
        Get-ManagementRole | New-ManagementRoleAssignment -SecurityGroup "Organization Management - Linked" -Delegating

Este exemplo presume que os seguintes valores são usados para cada parâmetro:

  - **LinkedForeignGroup**   `Organization Management Administrators`

  - **LinkedDomainController**   `DC01.users.contoso.com`

Usando os valores anteriores, este exemplo recria o grupo de funções Gerenciamento da Organização como um grupo de função vinculado.

    $ForeignCredential = Get-Credential
    $OrgMgmt  = Get-RoleGroup "Organization Management"
    New-RoleGroup "Organization Management - Linked" -LinkedForeignGroup "Organization Management Administrators" -LinkedDomainController DC01.users.contoso.com -LinkedCredential $ForeignCredential -Roles $OrgMgmt.Roles
    Get-ManagementRoleAssignment -RoleAssignee "Organization Management - Linked" -Role My* | Remove-ManagementRoleAssignment
    Get-ManagementRole | New-ManagementRoleAssignment -SecurityGroup "Organization Management - Linked" -Delegating

## Criar todos os outros grupos de função vinculado

Para recriar os grupos de função internos (que não seja o grupo de funções Gerenciamento da Organização ) como grupos de função vinculado, use o procedimento a seguir para cada grupo.

1.  Crie um USG na floresta externa para cada grupo de função que será vinculado a cada novo grupo de função.

2.  Armazene as credenciais de floresta estrangeira Active Directory em uma variável. Você precisará fazer isso vez.
    
        $ForeignCredential = Get-Credential

3.  Recupere uma lista de grupos de função usando o cmdlet a seguir.
    
        Get-RoleGroup

4.  Para cada grupo de função, que não seja o grupo de funções Gerenciamento da Organização, faça o seguinte.
    
        $RoleGroup = Get-RoleGroup <name of role group to re-create>
        New-RoleGroup "<role group name> - Linked" -LinkedForeignGroup <name of foreign USG> -LinkedDomainController <FQDN of foreign Active Directory domain controller> -LinkedCredential $ForeignCredential -Roles $RoleGroup.Roles

5.  Repita a etapa anterior para cada grupo de funções internas que deseja recriar como um grupo de função vinculado.

Este exemplo presume que os seguintes valores são usados para cada parâmetro:

  - **LinkedDomainController**   `DC01.users.contoso.com`

  - **Grupos de função internos para ser recriada como grupos de função vinculado** `Recipient Management, Server Management`   

  - **Grupo externo para o grupo de função vinculado Recipient Management** `Recipient Management Administrators`   

  - **Grupo estrangeiro para o grupo de função vinculado de gerenciamento de servidor** `Server Management Administrators`   

Usando os valores anteriores, este exemplo recria os grupos de funções de gerenciamento de servidor e Gerenciamento de Destinatários como grupos de função vinculado.

    $ForeignCredential = Get-Credential
    Get-RoleGroup
    $RoleGroup = Get-RoleGroup "Recipient Management"
    New-RoleGroup "Recipient Management - Linked" -LinkedForeignGroup "Recipient Management Administrators" -LinkedDomainController DC01.users.contoso.com -LinkedCredential $ForeignCredential -Roles $RoleGroup.Roles
    $RoleGroup = Get-RoleGroup "Server Management"
    New-RoleGroup "Server Management - Linked" -LinkedForeignGroup "Server Management Administrators" -LinkedDomainController DC01.users.contoso.com -LinkedCredential $ForeignCredential -Roles $RoleGroup.Roles

## Outras tarefas

Depois de criar os grupos de função vinculado, você também pode querer:

Adicione membros as USGs estrangeira usando Active Directory usuários e computadores na floresta externa.

Remova membros de grupos de funções internas. Para obter mais informações, consulte [Gerenciar membros do grupo de função](manage-role-group-members-exchange-2013-help.md).

Adicionar, remover ou alterar o escopo das funções nos novos grupos de função vinculado. Para obter mais informações, consulte [Gerenciar grupos de função](manage-role-groups-exchange-2013-help.md).

Crie grupos de função vinculado adicionais. Para obter mais informações, consulte [Gerenciar grupos de função vinculado](manage-linked-role-groups-exchange-2013-help.md).

