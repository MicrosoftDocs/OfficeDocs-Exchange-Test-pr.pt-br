---
title: 'Criar um grupo de busca de UM: Exchange 2013 Help'
TOCTitle: Criar um grupo de busca de UM
ms:assetid: 43ecb1ec-5f82-4516-9010-de8f954d3758
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Aa997679(v=EXCHG.150)
ms:contentKeyID: 50556175
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
f1_keywords:
- Microsoft.Exchange.Management.SnapIn.Esm.Servers.UnifiedMessaging.CreateUMHuntGroupWizardForm.CreateUMHuntGroupWizardPage1
ms.translationtype: MT
---

# Criar um grupo de busca de UM

 

_**Aplica-se a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Tópico modificado em:** 2013-04-16_

Um grupo de busca da Unificação de Mensagens (UM) é uma representação lógica de um grupo de busca existente para PBX ou PBX IP. Um grupo de busca de UM atua como uma conexão ou um link entre um gateway IP da UM e um plano de discagem da UM.


> [!TIP]
> Se ao criar um gateway IP de UM você associá-lo a um plano de discagem de UM, também será criado um grupo de busca de UM.




> [!TIP]
> Se desejar alterar as configurações do grupo de busca de UM, será necessário excluir o grupo de busca e criar outro grupo de busca com as configurações adequadas.



Para conhecer tarefas de gerenciamento adicionais relacionadas a grupos de busca de UM, consulte [Procedimentos de grupo de busca de Unificação de mensagens](um-hunt-group-procedures-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: 2 minutos.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Grupos de busca da UM" no tópico [Permissões de mensagens unificadas](unified-messaging-permissions-exchange-2013-help.md).

  - Antes de executar esses procedimentos, confirme se um plano de discagem da UM foi criado. Para obter etapas detalhadas, consulte [Criar um plano de discagem de UM](create-a-um-dial-plan-exchange-2013-help.md).

  - Antes de executar esses procedimentos, verifique se um gateway IP da UM foi criado. Para obter etapas detalhadas, consulte [Criar um gateway IP de UM](create-a-um-ip-gateway-exchange-2013-help.md).

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>..



## O que você deseja fazer?

## Usar o EAC para criar um grupo de busca de UM

1.  No EAC, navegue até **Unificação de Mensagens** \> **Planos de discagem de UM**. Na exibição de lista, selecione o plano de discagem de UM que você deseja alterar e clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").

2.  Na página **Plano de Discagem da UM**, em **Grupos de Busca da UM**, clique em **Novo**![Ícone Adicionar](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Ícone Adicionar").

3.  Na página **Novo grupo de busca da UM**, insira as seguintes informações:
    
      - **Nome**   Use esta caixa para criar o nome de exibição do grupo de busca da UM. Um nome para o grupo de busca de UM é necessário e deve ser exclusivo, mas é usado apenas para fins de exibição no EAC e no Shell. Se você precisar alterar o nome de exibição do grupo de busca depois da sua criação, primeiro exclua o grupo de busca existente e depois crie outro grupo de busca com o nome apropriado.
        
        Se a sua organização usa vários grupos de busca, convém usar nomes significativos para eles. O comprimento máximo do nome do grupo de busca de UM é 64 caracteres e pode incluir espaços. Entretanto, ele não pode incluir nenhum destes caracteres: " / \\ \[ \] : ; | = , + \* ? \< \>.
    
      - **Gateway IP da UM**   Use essa caixa para especificar o gateway IP da UM a ser usado. Clique em **Procurar** para selecionar o gateway IP da UM e clique em **OK**.
    
      - **Identificador piloto**   Use essa caixa para especificar uma cadeia de caracteres que identifique exclusivamente o identificador piloto configurado no PBX ou no IP PBX.
        
        É possível usar um número de ramal ou um URI (Uniform Resource Identifier) SIP (Session Initiation Protocol) nesta caixa. Caracteres alfanuméricos são aceitos nesta caixa. Para PBXs herdados, é usado um valor numérico com identificador piloto. No entanto, alguns IP-PBXs podem usar URIs SIP.

4.  
    
    Clique em **Salvar**.

## Usar o Shell para criar um grupo de busca da UM

Este exemplo cria um grupo de busca da UM chamado `MyUMHuntGroup` que possui um identificador piloto igual a 12345.

    New-UMHuntGroup -Name MyUMHuntGroup -PilotIdentifier 12345 -UMDialplan MyUMDialPlan -UMIPGateway MyUMIPGateway

Este exemplo cria um grupo de busca da UM chamado `MyUMHuntGroup` que possui vários identificadores piloto.

    New-UMHuntGroup -Name MyUMHuntGroup -PilotIdentifier 5551234,55555 -UMDialplan MyUMDialPlan -UMIPGateway MyUMIPGateway

