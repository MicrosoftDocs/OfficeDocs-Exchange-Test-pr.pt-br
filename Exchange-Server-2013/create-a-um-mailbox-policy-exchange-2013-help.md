---
title: 'Criar uma política de caixa de correio da UM: Exchange 2013 Help'
TOCTitle: Criar uma política de caixa de correio da UM
ms:assetid: 7f20874b-c46c-4505-9a78-f63eacb578ff
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Bb123510(v=EXCHG.150)
ms:contentKeyID: 50556210
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
f1_keywords:
- Microsoft.Exchange.Management.SnapIn.Esm.Servers.UnifiedMessaging.CreateUMMailboxPolicyWizardForm.CreateUMMailboxPolicyWizardPage
ms.translationtype: MT
---

# Criar uma política de caixa de correio da UM

 

_**Aplica-se a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Tópico modificado em:** 2013-03-08_

Você pode criar uma política de caixa de correio de Unificação de mensagens (UM) para aplicar um conjunto comum de configurações de diretiva de Unificação de mensagens, como configurações de diretiva PIN ou restrições de discagem, a uma coleção de caixas de correio habilitadas para UM. UM políticas de caixa de correio vincular a um usuário habilitado com um plano de discagem de Unificação de mensagens e aplicam um conjunto comum de políticas ou configurações de segurança para um conjunto de caixas de correio habilitadas para UM. UM a políticas de caixa de correio são úteis para a aplicação e padronização das definições de configuração de Unificação de mensagens para usuários habilitados para UM.

Por padrão, quando um plano de discagem UM é criado, uma política de caixa de correio de Unificação de mensagens também é criada. Você pode precisar criar diretivas de caixa de correio de Unificação de mensagens adicionais ou modificar políticas de caixa de correio de Unificação de mensagens existentes após implantar a Unificação de mensagens em sua organização.

Para conhecer tarefas de gerenciamento adicionais relacionadas a políticas de caixa de correio de UM, consulte [Procedimentos de diretiva de caixa de correio de Unificação de mensagens](um-mailbox-policy-procedures-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: 3 minutos.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Diretivas de caixa de correio da UM" no tópico [Permissões de mensagens unificadas](unified-messaging-permissions-exchange-2013-help.md).

  - Antes de executar esses procedimentos, confirme se um plano de discagem da UM foi criado. Para obter etapas detalhadas, consulte [Criar um plano de discagem de UM](create-a-um-dial-plan-exchange-2013-help.md).

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>..



## O que você deseja fazer?

## Usar o EAC para criar uma política de caixa de correio de Unificação de mensagens

1.  
    
    No EAC, navegue até **Unificação de Mensagens** \> **Planos de discagem de UM**. Na exibição de lista, selecione o plano de discagem de UM que você deseja alterar e clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").

2.  Na página de **Plano de discagem de UM**, em **Diretivas de caixa de correio de UM**, clique em **New**![Ícone Adicionar](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Ícone Adicionar").

3.  Na página **diretiva de caixa de correio de UM novo**, na caixa **nome**, digite o nome da nova diretiva de caixa de correio de Unificação de mensagens.
    
    Use esta caixa para especificar um nome exclusivo para a diretiva de caixa de correio de Unificação de mensagens. Este é um nome de exibição que aparece no EAC. Se você precisar alterar o nome de exibição da diretiva de caixa de correio de Unificação de mensagens após ele ter sido criado, você deve primeiro excluir a diretiva de caixa de correio de Unificação de mensagens existente e, em seguida, criar outra política de caixa de correio de Unificação de mensagens que tem o nome adequado. Se todos os usuários habilitados para UM estão associados ele, você não pode excluir uma política de caixa de correio de Unificação de mensagens.
    
    O nome de diretiva de caixa de correio de Unificação de mensagens é obrigatório, mas ele é usado apenas para exibição. Como sua organização pode usar várias políticas de caixa de correio de Unificação de mensagens, recomendamos que você use nomes significativos para suas políticas de caixa de correio de Unificação de mensagens. O comprimento máximo de um nome de política de caixa de correio de Unificação de mensagens é de 64 caracteres e pode incluir espaços. No entanto, ele não pode incluir qualquer um dos seguintes caracteres: "/ \\ \[\]:; | = , + \* ? \< \>.

4.  Clique em **Salvar** para salvar a nova política de caixa de correio de UM. Quando você salva a política de caixa de correio de UM, todas as configurações padrão, incluindo as políticas de PIN, os recursos de caixa postal e as configurações de Caixa Postal Protegida, são habilitadas. Se quiser personalizar ou alterar configurações padrão, use o cmdlet **Set-UMMailbox** para alterar as configurações da política de caixa de correio de UM recém-criada.

## Usar o Shell para criar uma diretiva de caixa de correio de UM

Esse exemplo cria uma diretiva de caixa de correio de UM chamada `MyUMMailboxPolicy`, que é associada a um plano de discagem de UM chamado `MyUMDialPlan`.

    New-UMMailboxPolicy -Name MyUMMailboxPolicy -UMDialPlan MyUMDialPlan

