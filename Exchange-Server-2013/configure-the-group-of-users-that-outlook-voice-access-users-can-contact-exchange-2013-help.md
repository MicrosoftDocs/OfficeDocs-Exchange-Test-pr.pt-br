---
title: 'Configurar grupo de usuários que usuários do Outlook Voice Access contatam'
TOCTitle: Configurar o grupo de usuários que os usuários do Outlook Voice Access podem contatar
ms:assetid: a8dc0f9e-dc86-4128-af63-d4e550aed5bb
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Ee423551(v=EXCHG.150)
ms:contentKeyID: 50486323
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configurar o grupo de usuários que os usuários do Outlook Voice Access podem contatar

 

_**Aplica-se a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Tópico modificado em:** 2012-11-09_

Você pode especificar quais usuários podem receber chamadas transferidas ou mensagens de caixa postal dos usuários do Outlook Voice Access. Por padrão, a **Este plano de discagem** opção está selecionada. Você pode alterar essa configuração para permitir que os usuários do Outlook Voice Access transferir chamadas ou enviar mensagens de voz aos usuários localizados em toda a organização, para Atendedor, um automático de UM existente ou para um número de ramal específico.

Para tarefas adicionais relacionadas a planos de discagem de UM, consulte [Procedimentos de plano de discagem de UM](um-dial-plan-procedures-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: Menos de 1 minuto.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Planos de discagem de UM" no tópico [Permissões de mensagens unificadas](unified-messaging-permissions-exchange-2013-help.md).

  - Antes de executar esses procedimentos, confirme se um plano de discagem da UM foi criado. Para obter etapas detalhadas, consulte [Criar um plano de discagem de UM](create-a-um-dial-plan-exchange-2013-help.md).

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>..



## O que você deseja fazer?

## Usar o EAC para configurar o grupo de usuários que os usuários do Outlook Voice Access podem contatar

1.  No EAC, navegue até **Unificação de Mensagens** \> **Planos de discagem de UM**.

2.  Na exibição de lista, selecione o plano de discagem de UM que você deseja alterar e clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").

3.  Na página **Plano de discagem de UM**, clique em **Configurar**.

4.  Na **transferência & pesquisa**, em **Permitir que os chamadores para procurar usuários por nome ou alias**, selecione uma das seguintes opções:
    
      - **Em somente este plano de discagem**    Use esta opção para permitir que os usuários do Outlook Voice Access que ligam para um número do Outlook Voice Access para localizar e contatar os usuários que estão no mesmo plano de discagem.
    
      - **Em toda a organização**    Use esta opção para permitir que os usuários do Outlook Voice Access que ligam para um número do Outlook Voice Access para localizar e contatar qualquer pessoa em toda a organização. Isso inclui todos os usuários que foram habilitados para caixa de correio.
    
      - **Somente neste atendedor automático**    Use esta opção para permitir que os usuários do Outlook Voice Access que ligam para um número de acesso de voz do Outlook para se conectar a um atendedor automático específico. Antes que você especificar aqui, você deve criar o atendedor automático. Isso permite que os usuários do Outlook Voice Access a ser transferida para outro atendedor. O atendedor automático que você escolher aqui pode ser um atendedor automático habilitado para fala ou não habilitados para fala.
    
      - **Somente para essa extensão**    Use esta opção para permitir que os usuários do Outlook Voice Access para se conectar a um número de ramal que você especificar. Você pode usar apenas os dígitos numéricos para a extensão. O número de dígitos que você define neste campo deve corresponder ao número de dígitos nos números de ramal configurados em UM plano de discagem.

5.  Clique em **Salvar**.

## Use o Shell para configurar o grupo de usuários que os usuários do Outlook Voice Access podem contatar

Este exemplo define o grupo de usuários que os usuários do Outlook Voice Access podem entrar em contato para um plano de discagem de UM chamado `MyUMDialPlan` para toda a organização.

    Set-UMDialPlan -Identity MyUMDialPlan -ContactScope 'GlobalAddressList' -UMAutoAttendant $null -AllowDialPlanSubscribers $false -AllowExtensions $false

Este exemplo define o grupo de usuários que podem entrar em contato para um plano de discagem de UM chamado `MyUMDialPlan` para o `DialPlan`usuários do Outlook Voice Access.

    Set-UMDialPlan -Identity MyUMDialPlan -ContactScope DialPlan -AllowDialPlanSubscribers $false -AllowExtensions $false

