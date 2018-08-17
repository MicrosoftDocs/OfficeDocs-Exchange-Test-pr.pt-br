---
title: 'Configurar o Exchange 2013 para permissões compartilhadas: Exchange 2013 Help'
TOCTitle: Configurar o Exchange 2013 para permissões compartilhadas
ms:assetid: 7d119977-b420-4b66-acf0-0a978b188cdd
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Dd638146(v=EXCHG.150)
ms:contentKeyID: 50485979
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configurar o Exchange 2013 para permissões compartilhadas

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2015-04-07_

Permissões compartilhadas permitem que você, como administrador do Microsoft Exchange Server 2013, criar Active Directory entidades de segurança, como usuários, e, em seguida, configurá-los como Exchange destinatários. Ao contrário de permissões de divisão, que separam as tarefas de gerenciamento entre grupos de administradores de Exchange e Active Directory administradores, há sem separação de tarefas com permissões compartilhadas.

Para obter mais informações sobre compartilhados e divididos permissões, consulte [Compreendendo as permissões de divisão](understanding-split-permissions-exchange-2013-help.md).

Você pode configurar sua organização de Exchange 2013 para permissões compartilhadas, se você tiver configurado anteriormente sua organização para permissões de divisão. O procedimento para alternar para permissões compartilhadas é diferente, dependendo se você está usando no momento Role Based acesso controle (RBAC) dividir permissões ou Active Directory dividir permissões. Escolha o procedimento a seguir que se aplicam à sua configuração atual. Se a seguir forem verdadeira, sua organização estiver usando permissões de divisão de Active Directory:

  - A unidade organizacional do Microsoft Exchange grupos protegido (UO) existe.

  - O grupo de segurança de permissões deWindowsExchange está localizado na Microsoft Exchange grupos protegidos UO.

  - O grupo de segurança de subsistema confiável de Exchange é um membro do grupo de segurança ExchangeWindows permissões.

  - Não há nenhuma atribuição de função de gerenciamento regular para a função de criação de destinatário do email ou criação de grupos de segurança e a associação.

Se você nunca tiver configurado sua organização para permissões de divisão, você não precisará executar esse procedimento. Exchange 2013 é configurado para permissões compartilhadas por padrão.

Para obter mais informações sobre grupos de funções de gerenciamento, funções de gerenciamento e atribuições de função de gerenciamento comuns e de delegação, consulte os tópicos a seguir:

  - [Controle de acesso baseado em função de compreensão](understanding-role-based-access-control-exchange-2013-help.md)

  - [Noções básicas sobre grupos de funções de gerenciamento](understanding-management-role-groups-exchange-2013-help.md)

  - [Noções básicas sobre funções de gerenciamento](understanding-management-roles-exchange-2013-help.md)

  - [Noções básicas sobre as atribuições de função de gerenciamento](understanding-management-role-assignments-exchange-2013-help.md)

Procurando outras tarefas de gerenciamento relacionadas às permissões? Confira [Permissões avançadas](advanced-permissions-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para concluir cada procedimento: 5 minutos

  - Os procedimentos neste tópico exigem permissões específicas. Consulte cada procedimento para ver informações sobre permissões.

  - Você deve usar o Shell de comando do Windows, Windows PowerShell ou ambas, para executar estes procedimentos. Para obter mais informações, consulte cada procedimento.

  - A organização Exchange 2013 atualmente deve ser configurada para RBAC ou Active Directory dividir permissões.

  - Se você tiver servidores do Microsoft Exchange Server 2010 em sua organização, o modelo de permissões que você selecionar também será aplicado para esses servidores.

  - Você deve ter permissões para delegar a função de gerenciamento de criação de destinatário de email e criação de grupos de segurança e função de gerenciamento a associação ao grupo de função de gerenciamento de Gerenciamento da Organização ou outro grupo de função que atribuiu a função destinatários de email.

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>.



## O que você deseja fazer?

## Alternar de RBAC dividir permissões para permissões compartilhadas

Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Grupos de função" no tópico [Permissões de gerenciamento de função](role-management-permissions-exchange-2013-help.md) .

Para alternar de RBAC dividir permissões para permissões Exchange 2013 compartilhados, você deve atribuir a função de criação de destinatário de email e a função de criação de grupos de segurança e a associação a um grupo de função que também tiver atribuído a função destinatários de email e tem administradores Exchange 2013 como membros. Na configuração padrão permissões compartilhadas, o grupo de função Gerenciamento da Organização contém cada uma dessas funções. Dessa forma, o grupo de funções Gerenciamento da Organização é neste procedimento.

## Configurar permissões compartilhadas

Para configurar permissões compartilhadas no grupo de funções Gerenciamento da Organização, faça o seguinte usando uma conta que tenha permissões para delegar atribuições de função para a função de criação de destinatário de email e a função de criação de grupos de segurança e a associação:

1.  Adicione delegação atribuições de função para a função de criação de destinatário de email e a função de criação de grupos de segurança e a associação ao grupo de funções Gerenciamento da Organização usando os seguintes comandos.
    
        New-ManagementRoleAssignment -Role "Mail Recipient Creation" -SecurityGroup "Organization Management" -Delegating
        New-ManagementRoleAssignment -Role "Security Group Creation and Membership" -SecurityGroup "Organization Management" -Delegating
    

    > [!NOTE]
    > Grupo de função (neste procedimento, o grupo de funções administradores Active Directory ) que possui delegando atribuições de função para a função de criação de destinatário de email e criação de grupos de segurança e a associação de função deve ser atribuído a função de gerenciamento de função para executar o cmdlet <STRONG>New-ManagementRoleAssignment</STRONG> . O destinatário da função que pode delegar a função de gerenciamento de função deve atribuir essa função ao grupo de função de administradores de Active Directory.



2.  Adicione as atribuições da função regular para a função de criação de destinatário de email para os grupos de função Gerenciamento da Organização e Gerenciamento de Destinatários usando os seguintes comandos.
    
        New-ManagementRoleAssignment -Role "Mail Recipient Creation" -SecurityGroup "Organization Management"
        New-ManagementRoleAssignment -Role "Security Group Creation and Membership" -SecurityGroup "Recipient Management"

3.  Adicione uma atribuição de função regular para a função de criação de grupos de segurança e a associação ao grupo de funções Gerenciamento da Organização usando o seguinte comando.
    
        New-ManagementRoleAssignment -Role "Security Group Creation and Membership" -SecurityGroup "Organization Management"

Para informações detalhadas de sintaxes e de parâmetros, consulte [New-ManagementRoleAssignment](https://technet.microsoft.com/pt-br/library/dd335193\(v=exchg.150\)).

## Remover permissões de administradores do Active Directory (opcional)

Opcionalmente, você pode remover as permissões concedidas aos administradores Active Directory se não quiser mais eles possam criar ou gerenciar objetos de Active Directory usando as ferramentas de gerenciamento de Exchange. Se você deseja remover permissões de administradores Active Directory, execute este procedimento.


> [!NOTE]
> Embora não seja possível remover permissões para administradores Active Directory gerenciar objetos de Active Directory usando as ferramentas de gerenciamento de Exchange, Active Directory administradores podem continuar a gerenciar objetos Active Directory usando ferramentas de gerenciamento de Active Directory, se suas permissões Active Directory permitirem. No entanto, não, poderá gerenciar Exchange-atributos específicos nos objetos Active Directory. Para obter mais informações, consulte <A href="understanding-split-permissions-exchange-2013-help.md">Compreendendo as permissões de divisão</A>.



Para remover Exchange-permissões de divisão relacionados dos administradores Active Directory, faça o seguinte:

1.  Remova o regulares e delegando atribuições da função que atribuir a função de criação de destinatário de email para o grupo de funções ou grupo de segurança universal (USG) que contém os administradores Active Directory como membros usando o seguinte comando. Esse comando usa o grupo de funções administradores Active Directory como um exemplo. A opção *WhatIf* permite ver quais atribuições de função serão removidas. Remover o comutador *WhatIf* e execute o comando novamente para remover as atribuições de função.
    
        Get-ManagementRoleAssignment -Role "Mail Recipient Creation" | Where { $_.RoleAssigneeName -EQ "Active Directory Administrators" } | Remove-ManagementRoleAssignment -WhatIf

2.  Remova o regulares e delegando atribuições da função que atribuir a função de criação de grupos de segurança e a associação ao grupo de função ou USG que contém os administradores Active Directory como membros usando o seguinte comando. Esse comando usa o grupo de funções administradores Active Directory como um exemplo. A opção *WhatIf* permite ver quais atribuições de função serão removidas. Remover o comutador *WhatIf* e execute o comando novamente para remover as atribuições de função.
    
        Get-ManagementRoleAssignment -Role "Security Group Creation and Membership" | Where { $_.RoleAssigneeName -EQ "Active Directory Administrators" } | Remove-ManagementRoleAssignment -WhatIf

3.  Opcional. Se você deseja remover todas as permissões de Exchange dos administradores Active Directory, você pode remover o grupo de função ou o USG nos quais eles são membros. Para obter mais informações sobre como remover um grupo de funções, consulte [Gerenciar grupos de função](manage-role-groups-exchange-2013-help.md).

Para detalhadas sobre sintaxe e informações de parâmetro, consulte [Get-ManagementRoleAssignment](https://technet.microsoft.com/pt-br/library/dd351024\(v=exchg.150\)) ou [Remove-ManagementRoleAssignment](https://technet.microsoft.com/pt-br/library/dd351205\(v=exchg.150\)).

## Alternar de permissões para permissões compartilhadas de divididas do Active Directory

Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o entrada "permissões de divisão deActive Directory " no tópico [Permissões de gerenciamento de função](role-management-permissions-exchange-2013-help.md) .

Para alternar das permissões de divisão de Active Directory para Exchange 2013 shared permissões, você deve executar novamente Exchange Setup para desativar as permissões de divisão de Active Directory na organização Exchange e crie as atribuições de função entre um grupo de funções e a função de criação de destinatário de email e criação de grupos de segurança e a associação de função. Na configuração padrão permissões compartilhadas, o grupo de função Gerenciamento da Organização contém cada uma dessas funções. Dessa forma, o grupo de funções Gerenciamento da Organização é neste procedimento.


> [!IMPORTANT]
> O comando setup.com neste procedimento faz alterações Active Directory. Você deve usar uma conta que tenha as permissões necessárias para fazer essas alterações. Esta conta não pode ser a mesma conta que tenha permissões para criar as atribuições de função usando o cmdlet <STRONG>New-ManagementRoleAssignment</STRONG> . Use a conta ou contas, com as permissões necessárias para concluir com êxito a cada etapa deste procedimento.



Para alternar entre Active Directory dividir permissões para permissões compartilhadas, faça o seguinte:

1.  A partir de um shell de comando Windows, execute o seguinte comando na mídia de instalação Exchange 2013 para desabilitar permissões de divisão de Active Directory.
    
        setup.exe /PrepareAD /ActiveDirectorySplitPermissions:false

2.  Da Exchange Management Shell, execute os seguintes comandos para adicionar as atribuições da função regular entre a função de criação de destinatário de email e criação de grupos de segurança e função de gerenciamento e os grupos de função Gerenciamento da Organização e Gerenciamento de Destinatários.
    
        New-ManagementRoleAssignment "Mail Recipient Creation_Organization Management" -Role "Mail Recipient Creation" -SecurityGroup "Organization Management"
        New-ManagementRoleAssignment "Security Group Creation and Membership_Org Management" -Role "Security Group Creation and Membership" -SecurityGroup "Organization Management"
        New-ManagementRoleAssignment "Mail Recipient Creation_Recipient Management" -Role "Mail Recipient Creation" -SecurityGroup "Recipient Management"

3.  Reinicie os servidores de Exchange 2013 em sua organização.
    

    > [!NOTE]
    > Se você tiver servidores Exchange 2010 em sua organização, você também precisará reiniciar esses servidores.



Para informações detalhadas de sintaxes e de parâmetros, consulte [New-ManagementRoleAssignment](https://technet.microsoft.com/pt-br/library/dd335193\(v=exchg.150\)).

