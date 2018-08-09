---
title: 'Adicionar caixa de correio de Federação ao AD RMS Super: Exchange 2013 Help'
TOCTitle: Adicionar a caixa de correio de Federação ao grupo de usuários do AD RMS Super
ms:assetid: 44618df9-54f0-4474-a450-dcba48a02901
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Ee424431(v=EXCHG.150)
ms:contentKeyID: 50485451
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Adicionar a caixa de correio de Federação ao grupo de usuários do AD RMS Super

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2016-12-09_

Para os seguintes Microsoft Exchange Server 2013 gerenciamento de direitos de informação (IRM) recursos estejam habilitados, você deve adicionar a caixa de correio de Federação (uma caixa de correio sistema criada pelo Exchange 2013 instalação) ao grupo de superusuários no cluster do [Active Directory Rights Management Services (AD RMS)](https://technet.microsoft.com/en-us/library/hh831364.aspx) da sua organização:

  - IRM no Microsoft Office Outlook Web App

  - IRM no Exchange ActiveSync

  - Descriptografia de relatório de diário

  - Descriptografia de transporte

Você pode configurar um grupo de distribuição habilitado para email como grupo de superusuários no AD RMS. Os membros do grupo de distribuição recebem uma licença de usuário de proprietário quando solicitam uma licença ao cluster do AD RMS. Isso permite a eles descriptografar todo o conteúdo protegido por RMS publicado por esse cluster. Se você usar um grupo de distribuição existente ou criar um grupo de distribuição e configurá-lo como grupo de superusuários no AD RMS, recomendamos dedicar o grupo de distribuição para essa finalidade e configurar as definições apropriadas para aprovar, auditar e monitorar alterações de associação.


> [!WARNING]
> Configurando um grupo de superusuários no AD RMS permite que os membros de grupo descriptografar conteúdo protegido por IRM. Recomendamos que você tomar as medidas adequadas para controlar e monitorar a associação de grupo e habilitar a auditoria acompanhar as alterações de associação. Você também pode limitar as alterações indesejadas para a associação ao grupo, definindo o grupo como um grupo restrito usando a diretiva de grupo. Para obter detalhes, consulte <A href="https://technet.microsoft.com/en-us/library/cc756802(v=ws.10).aspx">Configurações de diretiva de grupos restritos</A>.



Para tarefas de gerenciamento adicionais relacionadas a IRM, consulte [Procedimentos de gerenciamento de direitos de informação](information-rights-management-procedures-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: 15 minutos.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Grupos de distribuição" no tópico [Permissões de destinatários](recipients-permissions-exchange-2013-help.md).

  - Um cluster do AD RMS deve ser implantado na floresta do Active Directory.

  - Se um grupo de superusuários já estiver configurado em um cluster do AD RMS, qualquer modificação na associação do grupo de distribuição poderá levar até 24 horas para ser atualizada pelo cluster do AD RMS. Isso é o resultado de se armazenar em cache a associação de grupo no cluster.

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>.



## Como fazer isso?

## Etapa 1: Usar o Shell para adicionar uma caixa de correio Federada a um grupo de distribuição

Se um grupo de distribuição tiver sido criado e configurado como grupo de superusuários no cluster do AD RMS, você poderá adicionar a caixa de correio Federada do Exchange 2013 como um membro desse grupo. Se um grupo de superusuários não estiver configurado, você deverá criar um grupo de distribuição e adicionar a caixa de correio Federada como membro.

1.  Crie um grupo de distribuição dedicado para uso como um grupo de superusuários do AD RMS. Para obter detalhes, consulte [Criar e gerenciar grupos de distribuição](create-and-manage-distribution-groups-exchange-2013-help.md).

2.  Adicione o usuário **FederatedEmail.4c1f4d8b-8179-4148-93bf-00a95fa1e042** ao novo grupo de distribuição. A caixa de correio Federação é uma caixa de correio de sistema e, portanto, não fica visível no EAC. Para adicioná-la a um grupo de distribuição, você deve usar o cmdlet [Add-DistributionGroupMember](https://technet.microsoft.com/pt-br/library/bb124340\(v=exchg.150\)) do Shell.
    
    Este exemplo adiciona a caixa de correio Federada ao grupo de distribuição ADRMSSuperUsers.
    
        Add-DistributionGroupMember ADRMSSuperUsers -Member FederatedEmail.4c1f4d8b-8179-4148-93bf-00a95fa1e042

Para obter informações detalhadas de sintaxes e de parâmetros, consulte [Add-DistributionGroupMember](https://technet.microsoft.com/pt-br/library/bb124340\(v=exchg.150\)).

## Etapa 2: Use AD RMS para configurar um grupo de superusuários

Execute o procedimento a seguir em um cluster do AD RMS. A conta usada para executar esse procedimento deve ser membro do grupo local de Administradores Corporativos do AD RMS no servidor do AD RMS.

1.  Abra o console do Active Directory Rights Management Services e expanda o seu cluster.

2.  Na árvore de console, expanda **Diretivas de Segurança** e clique em **Superusuários**.

3.  No painel de ação, clique em **Habilitar Superusuários**.

4.  No painel de resultados, clique em **Alterar Grupo de Superusuários** para abrir a folha de propriedades de **Superusuários**.

5.  Na caixa **Grupo de superusuários**, digite o endereço de email do grupo de distribuição criado no procedimento anterior ou clique em **Procurar** para selecionar um grupo de distribuição.

## Como saber se funcionou?

Após adicionar a caixa de correio Federação a um grupo de distribuição novo ou já existente, use o cmdlet [Get-DistributionGroupMember](https://technet.microsoft.com/pt-br/library/aa996367\(v=exchg.150\)) para verificar a associação do grupo.

Para um exemplo de como verificar a associação ao grupo de distribuição, consulte [Examples](https://technet.microsoft.com/pt-br/aa996367\(exchg.150\)#examples) em **Get-DistributionGroupMember**.

Após usar o AD RMS para configurar um grupo de super usuários, você pode usar os métodos a seguir para verificar se o grupo de super usuários foi configurado corretamente. Além disso, você pode usar o cmdlet [Test-IRMConfiguration](https://technet.microsoft.com/pt-br/library/dd979798\(v=exchg.150\)) para verificar a funcionalidade do IRM.

  - Use o console do AD RMS para verificar se o grupo correto foi configurado como grupo de super usuários.

  - Execute o seguinte comando do PowerShell a seguir em um servidor AD RMS para recuperar o grupo de superusuários.
    

    > [!IMPORTANT]
    > O módulo do PowerShell ADRMSAdmin está disponível no Windows Server 2008 R2 ou posterior.

    
        Import-Module ADRMSAdmin
        New-PSDrive -Name MyRmsAdmin -PsProvider AdRmsAdmin -Root https://localhost 
        Get-ItemProperty -Path MyRmsAdmin:\SecurityPolicy\SuperUser

