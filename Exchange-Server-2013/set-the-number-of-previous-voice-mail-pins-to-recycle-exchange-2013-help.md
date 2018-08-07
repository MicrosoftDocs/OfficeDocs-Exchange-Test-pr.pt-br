---
title: 'Definir número anterior de PINs de reciclagem de correio de voz'
TOCTitle: Definir o número de anterior PINs reciclagem de correio de voz
ms:assetid: b094e68e-c493-4576-a6b1-4c780e635405
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Bb124254(v=EXCHG.150)
ms:contentKeyID: 50556275
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Definir o número de anterior PINs reciclagem de correio de voz

 

_**Aplica-se a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Tópico modificado em:** 2013-02-22_

Quando os usuários do Voice Access Outlook discar para um número do Outlook Voice Access, eles serão solicitados a digitar seu PIN para que o sistema de caixa postal pode autenticá-los. Depois que eles estiver autenticados, eles podem acessar a caixa postal, email, calendário e informações de contato pessoal em suas caixas de correio de qualquer telefone.

Várias configurações relacionadas ao PIN podem ser configuradas em uma diretiva de caixa de correio de Unificação de mensagens (UM). A configuração de **contagem de reciclagem do PIN** Especifica que o número de usuários exclusivos de PINs deve usar antes que eles podem reutilizar um PIN antigo. Você pode definir o valor dessa configuração entre 1 e 20. Na maioria das organizações, este valor deve ser definido como 5 PINs, que é o padrão. A definição desse valor muito alto pode perturbar os usuários, pois pode ser difícil para os usuários criem e memorizar PINs muitos. Defini-la muito baixo pode apresentar uma ameaça de segurança à sua rede.


> [!IMPORTANT]
> A contagem de reciclagem do PIN não pode ser desabilitada.



Para tarefas adicionais relacionadas à segurança do PIN do Outlook Voice Access, consulte [Procedimentos de segurança PIN](pin-security-procedures-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: Menos de 1 minuto.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Diretivas de caixa de correio da UM" no tópico [Permissões de mensagens unificadas](unified-messaging-permissions-exchange-2013-help.md).

  - Antes de executar esses procedimentos, confirme se um plano de discagem da UM foi criado. Para obter etapas detalhadas, consulte [Criar um plano de discagem de UM](create-a-um-dial-plan-exchange-2013-help.md).

  - Antes de executar esses procedimentos, verifique se uma política de caixa de correio de UM foi criada. Para obter etapas detalhadas, consulte [Criar uma política de caixa de correio da UM](create-a-um-mailbox-policy-exchange-2013-help.md).

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>..



## O que você deseja fazer?

## Usar o EAC para alterar a contagem de reciclagem do PIN

1.  No EAC, navegue até **Unificação de Mensagens** \> **Planos de discagem de UM**.

2.  Na exibição de lista, selecione o plano de discagem que você deseja alterar e clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").

3.  Na página **Plano de discagem de UM**, em **Políticas de Caixa de Correio de UM**, selecione a política de caixa de correio de UM que você deseja alterar e clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").

4.  Clique em **diretivas de PIN** e, ao lado de **contagem de reciclagem do PIN**, digite um valor entre 1 e 20.

5.  Clique em **Salvar**.

## Use o Shell para alterar a contagem de reciclagem do PIN

Este exemplo define a contagem de reciclagem do PIN de de diretiva de caixa de correio `MyUMMailboxPolicy` Unificação de mensagens como 10.

    Set-UMMailboxPolicy -Identity MyUMMailboxPolicy -PINHistoryCount 10

