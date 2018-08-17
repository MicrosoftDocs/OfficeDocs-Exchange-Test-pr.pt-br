---
title: 'Distribuição de caixa de correio automática: Exchange 2013 Help'
TOCTitle: Distribuição de caixa de correio automática
ms:assetid: f4db4636-948c-466b-839c-300c1a3a9544
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Ff477621(v=EXCHG.150)
ms:contentKeyID: 59635886
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Distribuição de caixa de correio automática

 

_**Aplica-se a:** Exchange Server 2010 Service Pack 2 (SP2), Exchange Server 2013_

_**Tópico modificado em:** 2013-08-13_

Ao criar ou mudar uma caixa de correio ou habilitar para email um usuário existente, essa caixa de correio precisa ser armazenada em um banco de dados de caixa de correio. No Microsoft Exchange Server 2013, você tem a opção de permitir que o Exchange escolha o banco de dados para você usando a distribuição de caixa de correio automática.

Com a distribuição de caixa de correio automática, o Exchange olha para os bancos de dados de caixa de correio em sua organização, exclui os bancos de dados que não são adequadas usando os critérios discutidos mais adiante neste tópico e, em seguida, escolhe aleatoriamente um banco de dados onde a caixa de correio deve estar localizada. Este processo distribui aleatoriamente caixas de correio em todos os bancos de dados de caixa de correio adequados em sua organização.

Distribuição automática é usada quando você não especifica o parâmetro nos cmdles *Database***New-Mailbox** e **Enable-Mailbox** ou o parâmetro *TargetDatabase* no cmdlet **New-MoveRequest**.


> [!NOTE]
> A distribuição de caixa de correio automática é executada somente quando uma caixa de correio é criada em um servidor Exchange 2013, mudado para um servidor&nbsp;Exchange 2013, ou quando um usuário estiver habilitado para email. Os cmdlets <STRONG>New-Mailbox</STRONG>, <STRONG>New-MoveRequest</STRONG> e <STRONG>Enable-Mailbox</STRONG> devem ser executados a partir de um servidor executando o Exchange 2013. O Exchange não redistribui caixas de correio para distribuir a carga entre bancos de dados automaticamente com base na carga do servidor.



O processo a seguir é usado para encontrar um banco de dados de caixa de correio adequado onde uma nova caixa de correio ou mudada deve ser localizada:

1.  O Exchange recupera uma lista de todos os bancos de dados de caixa de correio na organização Exchange 2013.

2.  Qualquer banco de dados de caixa de correio marcada para exclusão a partir do processo de distribuição é removido da lista de banco de dados disponível. Você pode controlar quais bancos de dados são excluídos. Para obter mais informações, consulte Exclude Databases from Automatic Distribution, posteriormente neste tópico.

3.  Qualquer banco de dados de caixa de correio fora dos escopos de gerenciamento do banco de dados aplicado ao administrador executando a operação é removida da lista de bancos de dados disponível. Para obter mais informações, consulte Database Scopes, posteriormente neste tópico.

4.  Qualquer banco de dados de caixa de correio fora do site Active Directory local onde a operação está sendo executada é removido da lista de bancos de dados disponível.

5.  A partir da lista remanescente de bancos de dados de caixa de correio, Exchange escolha um banco de dados aleatoriamente. Se o banco de dados estiver on-line e saudável, o banco de dados é usado pelo Exchange. Se estiver off-line ou não estiver saudável, um outro banco de dados é escolhido aleatoriamente. Se nenhum banco de dados on-line ou saudável for encontrado, a operação falha com um erro.

O processo de selecionar um banco de dados de caixa de correio é executado pelo agente de extensão do cmdlet Agente de Gerenciamento de Recursos de Caixa de Correio. O `Mailbox Resources Management Agent` é um dos vários agentes de extensão cmdlet que estende a funcionalidade de cmdlets sendo executados. Para mais informações sobre agentes de extensão de cmdlet, consulte [Agentes de extensão de cmdlet](cmdlet-extension-agents-exchange-2013-help.md).

Se você nunca quiser que caixas de correio sejam distribuídas automaticamente, você poderá desabilitar o `Mailbox Resources Management Agent`. Ao desabilitar o agente, a mudança é aplicada a toda a organização do Exchange. Para obter mais informações sobre como desabilitar agentes de extensão cmdlet, consulte [Gerenciar agentes de extensão de cmdlet](manage-cmdlet-extension-agents-exchange-2013-help.md).

## Excluir Bancos de dados de distribuição automática

Por padrão, todos os bancos de dados de correio saudáveis nos servidores Exchange 2013 no site local Active Directory podem ser escolhidos por distribuição automática de caixa de correio para armazenar uma nova caixa de correio ou mudada. Entretanto, talvez você deseje excluir alguns bancos de dados do processo de distribuição por vários motivos. Por exemplo, você pode designar um banco de dados de caixa de correio como uma banco de dados de diário no qual quaisquer caixas de correio que você especificar manualmente deve ser localizada. Ou você talvez deseje remover temporariamente um banco de dados de rotação para executar manutenção agendada. O Exchange 2013 fornece a opção de excluir banco de dados permanente ou temporariamente do processo de exclusão usando o parâmetro *IsExcludedFromProvisioning* que pode ser definido usando o cmdlet **Set-MailboxDatabase**.


> [!NOTE]
> Dois outros parâmetros, <EM>IsSuspendedFromProvisioning</EM> e <EM>IsExcludedFromInitialProvisioning</EM>, também estão disponíveis no cmdlet <STRONG>Set-MailboxDatabase</STRONG>. Esses parâmetros serão removidos em uma versão futura do Exchange e seu uso não é suportado.



O parâmetro *IsExcludedFromProvisioning* tem dois valores válidos, `$True` e `$False`. Quando você define essa propriedade para `$True`, o banco de dados da caixa de correio é excluído do processo de distribuição automática. Quando você a define para `$False`, o banco de dados da caixa de correio é incluído do processo de distribuição automática. O valor padrão é `$False`.

Para excluir um banco de dados de caixa de correio da distribuição automática, use o seguinte comando:

    Set-MailboxDatabase <database name> -IsExcludedFromProvisioning $True

Quando um banco de dados de caixa de correio excluído da distribuição automática, a única forma de criar uma caixa de correio no ou mudar uma caixa de correio para o banco de dados é usar o parâmetro *Database* nos cmdlets **New-Mailbox** e **Enable-Mailbox** ou o parâmetro *TargetDatabase* no cmdlet **New-MoveRequest**.

## Escopos do Banco de dados

Os escopos do gerenciamento de banco de dados são um nível adicional de controle do processo de distribuição de caixa de correio automática, os quais estão disponíveis em Exchange 2013. Se um banco de dados de caixa de correio estiver online e íntegro, ele estará no site local Active Directory, e não é excluído do processo de distribuição automática, o Exchange 2013 verifica para ver se o banco de dados de caixa de correio está incluso no escopo do banco de dados aplicado ao administrador executando o cmdlet. Se estiver incluído no escopo do banco de dados, está incluído na lista de bancos de dados disponível para o administrador.

Os escopos do banco de dados fazem parte do modelo de permissões RBAC (controle de acesso baseado na função). Para obter mais informações sobre RBAC e escopos do banco de dados, consulte os seguintes tópicos:

  - [Controle de acesso baseado em função de compreensão](understanding-role-based-access-control-exchange-2013-help.md)

  - [Noções básicas sobre escopos da função de gerenciamento](understanding-management-role-scopes-exchange-2013-help.md)

Os escopos do banco de dados podem ser úteis se você tiver muitos bancos de dados de caixa de correio em seu site local Active Directory que estão disponíveis para distribuição automática, mas você deseja limitar quais bancos de dados podem ser usados por determinados conjuntos de administradores. Por exemplo, seus servidores Exchange 2013 podem servir várias agências, mas você somente deseja permitir que cada agência crie ou mude caixas de correio para bancos de dados de caixa de correio que estão alocados a elas.

Por padrão, todos os administradores em um organização do Exchange 2013 pode consultar os bancos de dados de caixa de correio na organização. Para limitar os bancos de dados que eles podem consultar, e portanto, limitar os bancos de dados que eles podem potencialmente criar caixas de correio ou mudar caixas de correio para, você deve fazer o seguinte:

1.  Criar um escopo de gerenciamento de banco de dados customizado usando o cmdlet **New-ManagementScope** que inclui somente os bancos de dados de caixa de correio que você deseja que os administradores usem.

2.  Associar o novo escopo do banco de dados com atribuição de função de gerenciamento em uma das seguintes formas:
    
      - Adicionar o novo escopo de banco de dados a uma atribuição de função de gerenciamento existente usando o parâmetro *CustomConfigWriteScope* no cmdlet **Set-ManagementRoleAssignment**. O escopo do banco de dados está agora aplicado ao grupo de funções de gerenciamento, grupo de segurança universal (USG) ou usuário atribuído à atribuição de função.
    
      - Criar uma atribuição de função de gerenciamento usando o cmdlet **New-ManagementRoleAssignment** e usar o parâmetro *CustomConfigWriteScope* para especificar o novo escopo do banco de dados. Você pode criar uma atribuição de função entre uma função de gerenciamento e um grupo de funções, USG ou usuário.

3.  Se você criou uma atribuição de função para um grupo de funções ou USG, adicione usuários para o grupo de funções ou USG de forma que a atribuição de função e escopo de banco de dados sejam aplicados a usuários.

4.  Se aplicável, remova o usuário (ou usuários que são membros de grupos de funções ou USGs que você criou nas fases precedentes) você atribuiu a nova atribuição de função a partir de qualquer outro grupo de funções ou USGs para as quais pode ser atribuído um escopo de banco de dados que contém bancos de dados que você não quer que eles acessem.

5.  Verificar se os administradores têm acesso somente aos bancos de dados aos quais devem ter acesso.

Depois de concluir essas etapas, os administradores que têm atribuições de funções com os escopos de banco de dados que você criou somente poderão criar caixas de correio em ou mudar caixas de correio para os bancos de dados que você especificou.

Para obter mais informações sobre como usar os escopos de banco de dados para limitar os bancos de dados de caixa de correio estão disponíveis para administradores, consulte [Controlar a distribuição automática de caixa de correio usando escopos de banco de dados](control-automatic-mailbox-distribution-using-database-scopes-exchange-2013-help.md).

