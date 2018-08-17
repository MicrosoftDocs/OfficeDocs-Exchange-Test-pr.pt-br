---
title: 'Exibir permissões efetivas: Exchange 2013 Help'
TOCTitle: Exibir permissões efetivas
ms:assetid: ae6cb7cf-f998-44a6-a69a-02ad736c8260
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Dd638167(v=EXCHG.150)
ms:contentKeyID: 50486375
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Exibir permissões efetivas

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2012-10-09_

Permissões no Microsoft Exchange Server 2013 são concedidas usando funções de gerenciamento que são atribuídas a grupos de funções de gerenciamento, diretivas de atribuição de função de gerenciamento, segurança universal USGs (grupos) ou diretamente aos usuários. Os usuários são concedidos as permissões se ele estiver membros dos grupos de função ou USGs, ou se estiverem atribuídos diretivas de atribuição de função.

A maioria das permissões são concedidas com base em associação à função de grupo ou a atribuição de políticas de atribuição aos usuários finais. Embora o uso de grupos de função e políticas de atribuição torna fácil conceder permissões a um grande número de usuários, que você pode não estar ciente de que é um membro de um grupo de funções ou que tenha sido atribuído a uma diretiva de atribuição. Isso é onde a opção *GetEffectiveUsers* no cmdlet **Get-ManagementRoleAssignment** é útil. Ele mostra o que os usuários recebem suas permissões determinadas por uma função de gerenciamento através de grupos de funções, diretivas de atribuição e USGs atribuídos a eles.

A opção *GetEffectiveUsers* é usada com o cmdlet **Get-ManagementRoleAssignment** quando o parâmetro *Role* é usado. Especificando este comutador com uma determinada função, o cmdlet **Get-ManagementRoleAssignment** examina todas os função os destinatários atribuídos à função, como grupos de funções, diretivas de atribuição e USGs e lista os membros de cada uma delas.


> [!NOTE]
> A opção <EM>GetEffectiveUser</EM> não lista os usuários que são membros de um grupo de função estrangeira vinculado. Em vez de uma lista de usuários, se for encontrado um grupo de função vinculado, <STRONG>Todos os membros do grupo vinculados</STRONG> é exibida. Para obter mais informações sobre permissões em várias florestas, consulte <A href="understanding-multiple-forest-permissions-exchange-2013-help.md">Compreendendo as permissões de várias florestas</A>.



Para obter mais informações sobre funções de gerenciamento, grupos de função e políticas de atribuição, consulte [Controle de acesso baseado em função de compreensão](understanding-role-based-access-control-exchange-2013-help.md). Para obter mais informações sobre atribuições de função de gerenciamento, consulte [Noções básicas sobre as atribuições de função de gerenciamento](understanding-management-role-assignments-exchange-2013-help.md).

Procurando outras tarefas de gerenciamento relacionadas ao gerenciamento de permissões? Confira [Permissões](permissions-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para concluir cada procedimento: 5 minutos

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entradas de "Política de atribuição de função" no tópico [Permissões de gerenciamento de função](role-management-permissions-exchange-2013-help.md) ou de "Grupos de função".

  - Os procedimentos neste tópico só podem ser executados no Shell. Você não pode usar o Centro de administração do Exchange (EAC) para exibir permissões efetivas.

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>.



## Usar o Shell para listar todos os usuários eficazes

Para listar todos os usuários que são concedidos as permissões fornecidas por uma função de gerenciamento, use a seguinte sintaxe.

    Get-ManagementRoleAssignment -Role <role name> -GetEffectiveUsers

Este exemplo lista todos os usuários que são concedidos com permissões fornecidas pela função destinatários de email.

    Get-ManagementRoleAssignment -Role "Mail Recipients" -GetEffectiveUsers

Se você deseja alterar as propriedades que são retornadas na lista ou exportar a lista para um arquivo de valores separados por vírgula (. csv), consulte Use o Shell para personalizar a saída e exibi-la posteriormente neste tópico.

Para informações detalhadas de sintaxes e de parâmetros, consulte [Get-ManagementRoleAssignment](https://technet.microsoft.com/pt-br/library/dd351024\(v=exchg.150\)).

## Use o Shell para localizar um usuário específico em uma função

Para localizar um usuário específico que recebeu permissões por uma função de gerenciamento, use o cmdlet de **Get-ManagementRoleAssignment** para recuperar uma lista de todos os usuários efetivas e, em seguida, canalize a saída do cmdlet para o cmdlet **Where** . O cmdlet **Where** filtra a saída e retorna apenas o usuário que você especificou. Use a seguinte sintaxe.

    Get-ManagementRoleAssignment -Role <role name> -GetEffectiveUsers | Where { $_.EffectiveUserName -Eq "<name of user>" }

Este exemplo localiza o usuário David Strome na função de registro no diário.

    Get-ManagementRoleAssignment -Role Journaling -GetEffectiveUsers | Where { $_.EffectiveUserName -Eq "David Strome" }

Se você quiser alterar as propriedades que são retornadas na lista ou exportar a lista para um arquivo. csv, consulte Use o Shell para personalizar a saída e exibi-la posteriormente neste tópico.

Para informações detalhadas de sintaxes e de parâmetros, consulte [Get-ManagementRoleAssignment](https://technet.microsoft.com/pt-br/library/dd351024\(v=exchg.150\)).

## Use o Shell para localizar um usuário específico em todas as funções

Para souber que um usuário recebe permissões de função de cada, você deve usar o cmdlet **Get-ManagementRoleAssignment** para recuperar todos os usuários efetivos em todas as funções de gerenciamento e, em seguida, canalize a saída do cmdlet para o cmdlet **Where** . O cmdlet **Where** filtra a saída e retorna apenas atribuições da função que conceder as permissões de usuário.

    Get-ManagementRoleAssignment -GetEffectiveUsers | Where { $_.EffectiveUserName -Eq "<name of user>" }

Este exemplo localiza todas as atribuições de função que concedem permissões para o usuário Kim Akers.

    Get-ManagementRoleAssignment -GetEffectiveUsers | Where { $_.EffectiveUserName -Eq "Kim Akers" }

Se você quiser alterar as propriedades que são retornadas na lista ou exportar a lista para um arquivo CSV, consulte Use o Shell para personalizar a saída e exibi-la posteriormente neste tópico.

Para informações detalhadas de sintaxes e de parâmetros, consulte [Get-ManagementRoleAssignment](https://technet.microsoft.com/pt-br/library/dd351024\(v=exchg.150\)).

## Usar o Shell para personalizar a saída e exibi-la

A saída padrão do cmdlet **Get-ManagementRoleAssignment** talvez não tenha as informações que você deseja. A saída do cmdlet contém mais propriedades que você pode acessar. A seguir estão algumas das propriedades que podem ser úteis:

  - **EffectiveUserName**   Nome do usuário.

  - **Função**   Função que está concedendo permissões.

  - **RoleAssigneeName**   Grupo de função, diretiva de atribuição ou USG que é atribuída à função e contém o usuário na propriedade `EffectiveUserName` .

  - **RoleAssigneeType**   Indica se a atribuição de função é para um grupo de função, diretiva de atribuição, USG ou usuário.

  - **Assignmentmethod for utilizado**   Indica se a atribuição entre a função e o destinatário da função diretas ou indiretas.

  - **Parâmetros CustomRecipientWriteScope**   Indica o escopo de gravação do destinatário personalizado, se houver, que foi aplicada à atribuição de função quando ele foi criado. O escopo especificado nessa propriedade substitui o escopo de gravação do destinatário implícita especificado na propriedade `RecipientWriteScope` .

  - **CustomConfigWriteScope**   Indica o escopo de gravação da configuração personalizada, se houver, que foi aplicada à atribuição de função quando ele foi criado. O escopo especificado nessa propriedade substitui o escopo de gravação da configuração implícita especificado na propriedade `ConfigWriteScope` .

  - **RecipientReadScope**   Indica o que escopo que é aplicado à função de leitura do destinatário implícito.

  - **RecipientWriteScope**   Indica o escopo de gravação do destinatário implícita que é aplicado à função.

  - **ConfigReadScope**   Indica que a configuração implícita ler o escopo que é aplicado à função.

  - **ConfigWriteScope**   Indica o escopo de gravação implícita que é aplicado à função.

Para selecionar as propriedades que você deseja exibir em sua lista, você deve usar comandos semelhantes àquelas usadas nas seções a usar o Shell para listar todos os usuários efetivos, Use o Shell para localizar um usuário específico em uma funçãoe usar o Shell para localizar um usuário específico em todas as funções . A diferença é que você canaliza os resultados desses comandos para os cmdlets **Format-Table** ou **Select-Object** . O cmdlet **Format-Table** é útil para a lista de resultados para a tela de saída. O cmdlet **Select-Object** é útil para a lista dos resultados para um arquivo. csv de saída.

Ambos os cmdlets permitem que você especifique as propriedades que você deseja ver e na ordem em que você deseja vê-los. O cmdlet **Format-Table** oferece mais opções quando você lista resultados para uma tela enquanto **Select-Object** não modifica a saída de forma alguma, que é útil ao canalizar a lista para um arquivo. csv.

Para obter mais informações sobre os cmdlets **Format-Table** e **Select-Object** , consulte [Trabalhando com a saída do comando](working-with-command-output-exchange-2013-help.md).

## Uma lista personalizada para a tela de saída

1.  Escolha as informações que você deseja ver e encontre o comando associado a partir de um dos seguintes procedimentos:
    
      - Usar o Shell para listar todos os usuários eficazes
    
      - Use o Shell para localizar um usuário específico de uma função
    
      - Use o Shell para localizar um usuário específico em todas as funções

2.  Escolha as propriedades que você deseja ver em sua lista.

3.  Use a sintaxe a seguir para exibir a lista.
    
        <command to retrieve list > | Format-Table <property 1>, <property 2>, <property ...>

Este exemplo localiza o usuário David Strome em todas as funções e exibe o `EffectiveUserName`, `Role`, `CustomRecipientWriteScope`e `CustomConfigWriteScope` propriedades.

    Get-ManagementRoleAssignment -GetEffectiveUsers | Where { $_.EffectiveUserName -Eq "David Strome" } | Format-Table EffectiveUserName, Role, CustomRecipientWriteScope, CustomConfigWriteScope

Para informações detalhadas de sintaxes e de parâmetros, consulte [Get-ManagementRoleAssignment](https://technet.microsoft.com/pt-br/library/dd351024\(v=exchg.150\)).

## Saída de uma lista personalizada para um arquivo. csv

Para exportar uma lista para um arquivo. csv, você precisará canaliza os resultados do comando **Get-ManagementRoleAssignment** do procedimento apropriado listado anteriormente para o cmdlet **Select-Object** . A saída do cmdlet **Select-Object** será então canalizada para o cmdlet de **Export-CSV** , que salva a saída. csv para um nome de arquivo que você especificar.

1.  Escolha as informações que você deseja ver e encontre o comando associado a partir de um dos seguintes procedimentos:
    
      - Usar o Shell para listar todos os usuários eficazes
    
      - Use o Shell para localizar um usuário específico de uma função
    
      - Use o Shell para localizar um usuário específico em todas as funções

2.  Escolha as propriedades que você deseja ver em sua lista.

3.  Use a seguinte sintaxe para exportar a lista para um arquivo. csv.
    
        <command to retrieve list > | Select-Object <property 1>, <property 2>, <property ...> | Export-CSV <filename>

Este exemplo localiza o usuário David Strome em todas as funções e exibe o `EffectiveUserName`, `Role`, `CustomRecipientWriteScope`e `CustomConfigWriteScope` propriedades.

    Get-ManagementRoleAssignment -GetEffectiveUsers | Where { $_.EffectiveUserName -Eq "David Strome" } | Select-Object EffectiveUserName, Role, CustomRecipientWriteScope, CustomConfigWriteScope | Export-CSV c:\output.csv

Agora você pode exibir o arquivo. csv em um visualizador de sua escolha.

Para informações detalhadas de sintaxes e de parâmetros, consulte [Get-ManagementRoleAssignment](https://technet.microsoft.com/pt-br/library/dd351024\(v=exchg.150\)).

