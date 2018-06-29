---
title: 'Criar uma função: Exchange 2013 Help'
TOCTitle: Criar uma função
ms:assetid: e614ad8f-5946-4135-b130-89ea626afcd4
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Dd351214(v=EXCHG.150)
ms:contentKeyID: 50486904
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Criar uma função

 

_**Aplica-se a:**Exchange Server 2013_

_**Tópico modificado em:**2012-10-17_

Você pode criar uma função de gerenciamento, altere as entradas de função de gerenciamento, adicione um escopo, se necessário e, em seguida, atribuir a função a um destinatário de função. Você deve raramente precisa executar esse procedimento. Recomendamos que você verifique se uma função de gerenciamento internas pode ser usada ao invés de criar uma função de gerenciamento. Para obter uma lista das funções de gerenciamento internas, consulte [Funções de gerenciamento internas](built-in-management-roles-exchange-2013-help.md).

Para obter mais informações sobre as funções de gerenciamento no Microsoft Exchange Server 2013, consulte [Noções básicas sobre funções de gerenciamento](understanding-management-roles-exchange-2013-help.md).


> [!TIP]
> Este tópico não aborda como criar uma função de gerenciamento sem escopo. Para obter informações sobre como criar uma função de gerenciamento sem escopo, consulte <A href="create-an-unscoped-role-exchange-2013-help.md">Criar uma função sem escopo</A>.



Procurando outras tarefas de gerenciamento relacionadas a funções? Consulte [Permissões avançadas](advanced-permissions-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão do procedimento: 10 minutos

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "funções de gerenciamento" no tópico [Permissões de gerenciamento de função](role-management-permissions-exchange-2013-help.md).

  - Você deve usar o Shell para executar estes procedimentos.

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>.



## Como fazer isso?

## Etapa 1: Criar a função de gerenciamento

Novas funções de gerenciamento são baseadas em funções existentes. Quando você cria uma função, uma função existente e suas entradas de função de gerenciamento são copiadas para a nova função. A função existente se torna o pai para a nova função filho. Você deve escolher sempre uma função que contém todos os cmdlets e parâmetros, que você precisará usar e aqueles que não deseja remover. Funções filhas não podem ter entradas de função de gerenciamento que não existem na função pai.

Use a sintaxe a seguir para criar a nova função.

    New-ManagementRole -Parent <existing role to copy> -Name <name of new role>

Este exemplo copia a função destinatários de email e suas entradas de função de gerenciamento para a função de destinatários de email de Seattle.

    New-ManagementRole -Parent "Mail Recipients" -Name "Seattle Mail Recipients"

Para informações detalhadas de sintaxes e de parâmetros, consulte [New-ManagementRole](https://technet.microsoft.com/pt-br/library/dd298073\(v=exchg.150\)).

## Etapa 2: Alterar as entradas de função de gerenciamento da nova função

Depois de criar sua função, você precisará alterar as entradas da função. Você pode remover uma entrada de função inteira, que remove completamente o acesso ao cmdlet associado. Ou então, você pode remover parâmetros de uma entrada de função para remover o acesso a esses parâmetros específicos no cmdlet associado.

Você não pode adicionar novas entradas de função ou parâmetros nas entradas de função, a menos que existem na função pai. Porque você acabou de criar uma função de uma função pai na etapa 1, você não pode adicionar quaisquer entradas de função adicionais ou parâmetros nas entradas de função porque não existirem na função pai.

Ao alterar uma entrada de função em uma função, você pode realizar um destes procedimentos:

  - Remover uma única entrada de função inteira.

  - Remover várias entradas de função inteiras.

  - Remover parâmetros de uma entrada de função.

Para remover entradas de função de sua nova função, consulte [Remover uma entrada de função de uma função](remove-a-role-entry-from-a-role-exchange-2013-help.md).

## Etapa 3: Criar um escopo de função de gerenciamento personalizado, se necessário

Escopos da função de gerenciamento determinam os objetos torná-los disponíveis para um usuário para exibir ou alterar usando as entradas de função configuradas na etapa 2. Novas funções de gerenciamento herdam a leitura e gravação gerenciamento escopos de função da função de seu pai. Estes são chamados *escopos implícitos*. No entanto, pode haver casos em que você deseja alterar o escopo de gravação da nova função para atender às suas necessidades de negócios. Quando você cria um escopo personalizado, você pode substituir o escopo de gravação implícita da função. Não altera o escopo de leitura implícito da função. Para obter mais informações sobre escopos da função de gerenciamento, consulte [Noções básicas sobre escopos da função de gerenciamento](understanding-management-role-scopes-exchange-2013-help.md).

Você pode criar um escopo personalizado, criar um escopo exclusivo, use um escopo predefinido ou uma atribuição a uma unidade organizacional (UO) de escopo. O novo escopo deve estar dentro do escopo de leitura implícito da função. Para usar um escopo predefinido ou especifique uma unidade organizacional, pule para a etapa 4.

Para adicionar um escopo personalizado à nova função, consulte [Criar um escopo regular ou exclusivo](create-a-regular-or-exclusive-scope-exchange-2013-help.md).

## Etapa 4: Atribuir a nova função de gerenciamento

A etapa final ao criar e configurar uma função é atribuí-la a um destinatário de função.

Quando você cria uma atribuição de função, você pode optar por fazer uma das seguintes opções:

  - Crie a atribuição de função com nenhum escopo.

  - Crie a atribuição de função com um escopo predefinido.

  - Crie a atribuição de função com uma UO sem um filtro de restrição de domínio.

  - Crie a atribuição de função com o escopo personalizado ou exclusivo que você criou na etapa 3.
    

    > [!TIP]
    > Quando você cria uma atribuição entre uma função e uma diretiva de atribuição de função de gerenciamento, é possível especificar um escopo.



Você pode atribuir a nova função a um grupo de funções, uma política de atribuição de função, um usuário ou um grupo de segurança universal (USG). Para obter mais informações, consulte os tópicos a seguir:

  - [Gerenciar grupos de função](manage-role-groups-exchange-2013-help.md)

  - [Gerenciar políticas de atribuição de função](manage-role-assignment-policies-exchange-2013-help.md)

  - [Adicionar uma função a um usuário ou USG](add-a-role-to-a-user-or-usg-exchange-2013-help.md)

