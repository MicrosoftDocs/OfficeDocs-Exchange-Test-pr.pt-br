---
title: 'Ativar uma saudação personalizada para os usuários do Outlook Voice Access: Exchange 2013 Help'
TOCTitle: Ativar uma saudação personalizada para os usuários do Outlook Voice Access
ms:assetid: abd418ec-2c65-4720-859d-c11a2698dc06
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Bb124125(v=EXCHG.150)
ms:contentKeyID: 50556269
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Ativar uma saudação personalizada para os usuários do Outlook Voice Access

 

_**Aplica-se a:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Tópico modificado em:**2016-12-09_

Por padrão, cada plano de discagem de Unificação de mensagens (UM) usa um arquivo. wav de padrão para a saudação de boas-vindas que tem reproduzido para chamadores, incluindo Outlook usuários de acesso de voz que discam para um número do Outlook Voice Access foi configurado. No entanto, você pode criar um arquivo. wav ou. wma para a saudação de boas-vindas e, em seguida, habilitá-lo no plano de discagem de Unificação de MENSAGENS.

Por exemplo, você talvez queira alterar a saudação de boas-vindas padrão e em vez disso, forneça uma saudação de boas-vindas que é específica para sua empresa, como "Bem-vindo ao Outlook acesso de voz para o Woodgrove Bank". Para fazer isso, você pode gravar a saudação de boas-vindas personalizada e salvá-lo como um arquivo. wav ou. wma. Em seguida, você pode configurar o plano de discagem para usar a saudação de boas-vindas personalizada.

Para obter mais informações sobre as opções de menu disponíveis para usuários do Outlook Voice Access, consulte o guia de referência rápida para Outlook Voice Access, que é disponível a partir do [Centro de Download da Microsoft](https://go.microsoft.com/fwlink/p/?linkid=272767).

Para mais tarefas de gerenciamento relacionadas a planos de discagem de UM, consulte [Procedimentos de plano de discagem de UM](um-dial-plan-procedures-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: Menos de 1 minuto.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Planos de discagem de UM" no tópico [Permissões de mensagens unificadas](unified-messaging-permissions-exchange-2013-help.md).

  - Antes de executar esses procedimentos, confirme se um plano de discagem da UM foi criado. Para obter etapas detalhadas, consulte [Criar um plano de discagem de UM](create-a-um-dial-plan-exchange-2013-help.md).

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>..



## O que você deseja fazer?

## Usar o EAC para habilitar uma saudação de boas-vindas personalizada

1.  No EAC, navegue até **Unificação de Mensagens** \> **Planos de discagem de UM**.

2.  Na exibição de lista, selecione o plano de discagem de Unificação de MENSAGENS que você deseja modificar e, em seguida, clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").

3.  Na página **Plano de discagem de UM**, clique em **Configurar**.

4.  No **Outlook Voice Access**, em **boas-vindas de saudação**, clique em **Alterar** e clique em **Procurar** para localizar o arquivo de saudação.
    

    > [!IMPORTANT]
    > O arquivo que você pode usar para a saudação de boas-vindas deve ser um arquivo. wav ou. wma.



5.  Depois de ter localizado o arquivo, clique em **Abrir** e em **Salvar**.

## Use o Shell para habilitar uma saudação de boas-vindas personalizada

Este exemplo habilita uma saudação de boas-vindas que usa o arquivo de C:\\UMPrompts\\welcome.wav em um plano de discagem de UM chamado `MyUMDialPlan`.

    Set-UMDialPlan -Identity MyUMDialPlan -WelcomeGreetingEnabled $true -WelcomeGreetingFilename c:\UMPrompts\welcome.wav

