---
title: 'Gerenciar grupos de função vinculado: Exchange 2013 Help'
TOCTitle: Gerenciar grupos de função vinculado
ms:assetid: e2a07395-90c2-4d62-b15d-ac3ff28fe786
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/JJ657502(v=EXCHG.150)
ms:contentKeyID: 50486888
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Gerenciar grupos de função vinculado

 

_**Aplica-se a:**Exchange Server 2013_

_**Tópico modificado em:**2012-10-09_

Você pode usar um grupo de funções de gerenciamento vinculados para permitir que membros de um grupo de segurança universal (USG) em uma floresta estrangeira Active Directory gerenciar uma organização do Microsoft Exchange Server 2013 em uma floresta de recursos Active Directory. Associando um USG em uma floresta externa um grupo de função vinculado, os membros que USG são concedidas as permissões fornecidas pelas funções de gerenciamento atribuídas ao grupo de função vinculado. Para obter mais informações sobre grupos de função vinculado, consulte [Noções básicas sobre grupos de funções de gerenciamento](understanding-management-role-groups-exchange-2013-help.md).

Para criar e configurar grupos de função vinculado, você precisa usar os cmdlets **New-RoleGroup** e **Set-RoleGroup** . Para detalhadas sobre sintaxe e informações de parâmetro, consulte os tópicos a seguir:

  - [New-RoleGroup](https://technet.microsoft.com/pt-br/library/dd638181\(v=exchg.150\))

  - [Set-RoleGroup](https://technet.microsoft.com/pt-br/library/dd638182\(v=exchg.150\))

Para tarefas de gerenciamento adicionais relacionadas a grupos de funções, consulte [Permissões](permissions-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para concluir cada procedimento: 5 a 10 minutos

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Grupos de função" no tópico [Permissões de gerenciamento de função](role-management-permissions-exchange-2013-help.md) .

  - Você não pode usar o Centro de administração do Exchange (EAC) para criar ou configurar os grupos de função vinculado. Você deve usar o Shell de gerenciamento do Exchange.

  - No mínimo, configurar um grupo de função vinculado requer que uma relação de confiança unidirecional é estabelecida entre a floresta de Active Directory de recursos no qual residirá o grupo de função vinculado e estrangeira Active Directory floresta em que os usuários ou USGs residem. Floresta de recursos deve confiar na floresta externa.

  - Você deve possuir as seguintes informações sobre a floresta externa do Active Directory:
    
      - **Credenciais**   Você deve ter um nome de usuário e senha que pode acessar a floresta estrangeira Active Directory. Essa informação é usada com o parâmetro *LinkedCredential* nos cmdlets de **New-RoleGroup** e **Set-RoleGroup** .
    
      - **Controlador de domínio**   Você deve ter o nome de domínio totalmente qualificado (FQDN) de um controlador de domínio na floresta estrangeira Active DirectoryActive Directory. Essa informação é usada com o parâmetro *LinkedDomainController* nos cmdlets de **New-RoleGroup** e **Set-RoleGroup** .
    
      - **USG externo**   Você deve ter o nome completo de um USG na floresta estrangeira Active Directory que contém os membros que você deseja associar ao grupo de função vinculado. Essa informação é usada com o parâmetro *LinkedForeignGroup* no cmdlet **New-RoleGroup** e **Set-RoleGroup** .

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>.



## O que você deseja fazer?

## Criar um grupo de função vinculado

## Usar o Shell para criar um grupo de função vinculado sem escopo

Para criar um grupo de função vinculado e atribuir funções de gerenciamento ao grupo de função vinculado, faça o seguinte:

1.  Armazene as credenciais da floresta externa do Active Directory em uma variável.
    
        $ForeignCredential = Get-Credential

2.  Criar o grupo de função vinculado usando a sintaxe a seguir.
    
        New-RoleGroup <role group name> -LinkedForeignGroup <name of foreign USG> -LinkedDomainController <FQDN of foreign Active Directory domain controller> -LinkedCredential $ForeignCredential -Roles <role1, role2, role3...>

3.  Adicionar ou remover membros ao/do USG externo usando Usuários e Computadores do Active Directory em um computador na floresta externa do Active Directory.

Este exemplo faz o seguinte:

  - Recupera as credenciais da floresta externa users.contoso.com do Active Directory. Essas credenciais são usadas para conectar ao controlador de domínio DC01.users.contoso.com na floresta externa.

  - Cria um grupo de função vinculado chamado grupo de função de conformidade na floresta de recursos onde Exchange 2013 está instalado.

  - Vincula o novo grupo de função ao USG Administradores de Conformidade na floresta externa users.contoso.com do Active Directory.

  - Atribui as funções de gerenciamento Regras de Transporte e Registro em Diário ao novo grupo de função vinculado.

<!-- end list -->

    $ForeignCredential = Get-Credential
    New-RoleGroup "Compliance Role Group" -LinkedForeignGroup "Compliance Administrators" -LinkedDomainController DC01.users.contoso.com -LinkedCredential $ForeignCredential -Roles "Transport Rules", "Journaling"

## Usar o Shell para criar um grupo de função vinculado com um escopo de gerenciamento personalizado

É possível criar grupos de função vinculados com escopos de gerenciamento de destinatário personalizados, escopos de gerenciamento de configuração personalizados ou ambos. Para criar um grupo de função vinculado e atribuir funções de gerenciamento com escopos personalizados a ele, faça o seguinte:

1.  Armazene as credenciais da floresta externa do Active Directory em uma variável.
    
        $ForeignCredential = Get-Credential

2.  Criar o grupo de função vinculado usando a sintaxe a seguir.
    
        New-RoleGroup <role group name> -LinkedForeignGroup <name of foreign USG> -LinkedDomainController <FQDN of foreign Active Directory domain controller> -CustomConfigWriteScope <name of configuration scope> -CustomRecipientWriteScope <name of recipient scope> -LinkedCredential $ForeignCredential -Roles <role1, role2, role3...>

3.  Adicionar ou remover membros ao/do USG externo usando Usuários e Computadores do Active Directory em um computador na floresta externa do Active Directory.

Este exemplo faz o seguinte:

  - Recupera as credenciais da floresta externa users.contoso.com do Active Directory. Essas credenciais são usadas para conectar ao controlador de domínio DC01.users.contoso.com na floresta externa.

  - Cria um grupo de função vinculado chamado grupo de função de conformidade de Seattle na floresta de recursos onde Exchange 2013 está instalado.

  - Vincula o novo grupo de função ao USG Administradores de Conformidade de Seattle na floresta externa users.contoso.com do Active Directory.

  - Atribui as funções de gerenciamento Regras de Transporte e Registro em Diário ao novo grupo de função vinculado com o escopo de destinatário personalizado Destinatários de Seattle.

<!-- end list -->

    $ForeignCredential = Get-Credential
    New-RoleGroup "Seattle Compliance Role Group" -LinkedForeignGroup "Seattle Compliance Administrators" -LinkedDomainController DC01.users.contoso.com -LinkedCredential $ForeignCredential -CustomRecipientWriteScope "Seattle Recipients" -Roles "Transport Rules", "Journaling"

Para obter mais informações sobre escopos de gerenciamento, consulte [Noções básicas sobre escopos da função de gerenciamento](understanding-management-role-scopes-exchange-2013-help.md).

## Usar o Shell para criar um grupo de função vinculado com um escopo de OU

Você pode criar grupos de função vinculados que usam um escopo de destinatário OU. Para criar um grupo de função vinculado e atribuir funções de gerenciamento a ele com um escopo de OU, faça o seguinte:

1.  Armazene as credenciais da floresta externa do Active Directory em uma variável.
    
        $ForeignCredential = Get-Credential

2.  Criar o grupo de função vinculado usando a sintaxe a seguir.
    
        New-RoleGroup <role group name> -LinkedForeignGroup <name of foreign USG> -LinkedDomainController <FQDN of foreign Active Directory domain controller> -LinkedCredential $ForeignCredential -RecipientOrganizationalUnitScope <OU name> -Roles <role1, role2, role3...>

3.  Adicionar ou remover membros ao/do USG externo usando Usuários e Computadores do Active Directory em um computador na floresta externa do Active Directory.

Este exemplo faz o seguinte:

  - Recupera as credenciais da floresta externa users.contoso.com do Active Directory. Essas credenciais são usadas para conectar ao controlador de domínio DC01.users.contoso.com na floresta externa.

  - Cria um grupo de função vinculado chamado grupo de função de conformidade executivos na floresta de recursos onde Exchange 2013 está instalado.

  - Vincula o novo grupo de função ao USG Administradores de Conformidade de Executivos na floresta externa users.contoso.com do Active Directory.

  - Atribui as funções de gerenciamento Regras de Transporte e Registro em Diário ao novo grupo de função vinculado com o escopo de destinatário de OU OU de Executivos.

<!-- end list -->

    $ForeignCredential = Get-Credential
    New-RoleGroup "Executives Compliance Role Group" -LinkedForeignGroup "Executives Compliance Administrators" -LinkedDomainController DC01.users.contoso.com -LinkedCredential $ForeignCredential -RecipientOrganizationalUnitScope "Executives OU" -Roles "Transport Rules", "Journaling"

Para obter mais informações sobre escopos de gerenciamento, consulte [Noções básicas sobre escopos da função de gerenciamento](understanding-management-role-scopes-exchange-2013-help.md).

## Alterar o USG externo em um grupo de função vinculado

## Use o Shell para alterar o USG externo em um grupo de função vinculado

Para alterar o USG externo associado a um grupo de função vinculado, faça o seguinte:

1.  Armazene as credenciais da floresta externa do Active Directory em uma variável.
    
        $ForeignCredential = Get-Credential

2.  Altere o USG externo no grupo de função vinculado existente usando a seguinte sintaxe.
    
        Set-RoleGroup <role group name> -LinkedForeignGroup <name of foreign USG> -LinkedDomainController <FQDN of foreign Active Directory domain controller> -LinkedCredential $ForeignCredential 

Este exemplo faz o seguinte:

  - Recupera as credenciais da floresta externa users.contoso.com do Active Directory. Essas credenciais são usadas para conectar ao controlador de domínio DC01.users.contoso.com na floresta externa.

  - Altera o USG externo no grupo de funções de grupo de função de conformidade para oficiais de conformidade normativa.

<!-- end list -->

    $ForeignCredential = Get-Credential
    Set-RoleGroup "Compliance Role Group" -LinkedForeignGroup "Regulatory Compliance Officers" -LinkedDomainController DC01.users.contoso.com -LinkedCredential $ForeignCredential

