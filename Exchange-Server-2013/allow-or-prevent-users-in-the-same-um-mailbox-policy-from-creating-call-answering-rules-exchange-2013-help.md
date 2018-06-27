---
title: 'Permitir ou impedir que os usuários na mesma política de caixa de correio de Unificação de mensagens criando regras de atendimento de chamada: Exchange 2013 Help'
TOCTitle: Permitir ou impedir que os usuários na mesma política de caixa de correio de Unificação de mensagens criando regras de atendimento de chamada
ms:assetid: e44acaa6-d5a8-41e8-94aa-100be0bd6391
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Dd351209(v=EXCHG.150)
ms:contentKeyID: 50556302
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Permitir ou impedir que os usuários na mesma política de caixa de correio de Unificação de mensagens criando regras de atendimento de chamada

 

_**Aplica-se a:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Tópico modificado em:**2013-02-22_

Você pode permitir que os usuários que estão associados uma diretiva de caixa de correio de Unificação de mensagens (UM) para configurar as regras de atendimento de chamada ou impedir isso. Se a opção de configurar regras de atendimento de chamada é desabilitada em um plano de discagem de UM, o recurso de regras de atendimento de chamada não estará disponível para usuários habilitados para UM associados com a diretiva de caixa de correio de Unificação de mensagens. A configuração padrão é ativada.

Para tarefas de gerenciamento adicionais relacionadas a permitindo que os usuários encaminhar chamadas, consulte [Encaminhamento de chamadas de procedimentos](forwarding-calls-procedures-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: 2 minutos.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Diretivas de caixa de correio da UM" no tópico [Permissões de mensagens unificadas](unified-messaging-permissions-exchange-2013-help.md).

  - Antes de executar esses procedimentos, confirme se um plano de discagem da UM foi criado. Para obter etapas detalhadas, consulte [Criar um plano de discagem de UM](create-a-um-dial-plan-exchange-2013-help.md).

  - Antes de executar esses procedimentos, verifique se uma política de caixa de correio de UM foi criada. Para obter etapas detalhadas, consulte [Criar uma política de caixa de correio da UM](create-a-um-mailbox-policy-exchange-2013-help.md).

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>..



## O que você deseja fazer?

## Usar o EAC para habilitar ou desabilitar regras em uma diretiva de caixa de correio de Unificação de mensagens de atendimento de chamadas

1.  No EAC, navegue até **Unificação de Mensagens** \> **Planos de discagem de UM**. Na exibição de lista, selecione o plano de discagem de UM que você deseja modificar e clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").

2.  Em **Políticas de Caixa de Correio de UM**, selecione a política de caixa de correio de UM que você deseja gerenciar e clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").

3.  Na página **Diretiva de caixa de correio de UM**, marque ou desmarque a caixa de seleção ao lado de **Permitir que os usuários para configurar as regras de atendimento de chamada**.

4.  Clique em **Salvar**.

## Usar o Shell para habilitar ou desabilitar regras em uma diretiva de caixa de correio de Unificação de mensagens de atendimento de chamadas

Este exemplo permite que os usuários que estão associados a UM política de caixa de correio `MyUMMailboxPolicy` para criar regras de atendimento de chamada.

    Set-UMMailboxPolicy -identity MyUMMailboxPolicy -AllowCallAnsweringRules $true

Este exemplo impede que os usuários que estão associados a UM política de caixa de correio `MyUMMailboxPolicy` desde a criação de regras de atendimento de chamada.

    Set-UMMailboxPolicy -identity MyUMMailboxPolicy -AllowCallAnsweringRules $false

