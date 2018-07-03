---
title: 'Recuperar informações de PIN de caixa postal: Exchange 2013 Help'
TOCTitle: Recuperar informações de PIN de caixa postal
ms:assetid: 01517cca-99fe-46b2-b586-19e8d2707728
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Aa995900(v=EXCHG.150)
ms:contentKeyID: 54651925
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Recuperar informações de PIN de caixa postal

 

_**Aplica-se a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Tópico modificado em:** 2013-04-03_

Você pode recuperar as informações do PIN de um usuário habilitado para UM (Unificação de Mensagens). Após um usuário ser habilitado para UM e um PIN ser gerado ou criado, o PIN é criptografado e armazenado na caixa de correio do usuário.

Quando você recupera as informações de PIN de um usuário habilitado para UM, as informações retornadas são calculadas com base nos dados do PIN criptografados, que são armazenados em um formato criptografado na caixa de correio do usuário. Isso permite exibir as informações da caixa de correio do usuário e também indica se o usuário teve sua caixa de correio bloqueada.

Para tarefas adicionais relacionadas à segurança do PIN, consulte [Procedimentos de segurança PIN](pin-security-procedures-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: Menos de 1 minuto.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Planos de discagem de UM" no tópico [Permissões de mensagens unificadas](unified-messaging-permissions-exchange-2013-help.md).

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Caixas de correio de UM", no tópico [Permissões de mensagens unificadas](unified-messaging-permissions-exchange-2013-help.md).

  - Antes de executar esses procedimentos, confirme se um plano de discagem de UM foi criado. Para conhecer etapas detalhadas, consulte [Criar um plano de discagem de UM](create-a-um-dial-plan-exchange-2013-help.md).

  - Antes de executar esses procedimentos, verifique se uma política de caixa de correio de UM foi criada. Para conhecer etapas detalhadas, consulte [Criar uma política de caixa de correio da UM](create-a-um-mailbox-policy-exchange-2013-help.md).

  - Antes de você executar esses procedimentos, verifique se a caixa de correio de usuário foi habilitada para UM. Para conhecer etapas detalhadas, consulte [Habilitar um usuário para caixa postal](enable-a-user-for-voice-mail-exchange-2013-help.md).

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>..



## O que você deseja fazer?

## Use o EAC para recuperar as informações do PIN de um usuário habilitador para UM

1.  No EAC, navegue até **Destinatários**. Na exibição de lista, selecione a caixa de correio de usuário que você deseja atualizar.

2.  No painel de detalhes, em **Telefone e Recursos de Voz**, clique em **Visualizar detalhes**.

3.  Na página **Caixa de Correio de UM** \> **Configurações de caixa de correio da UM**, veja o **Status do PIN** para o usuário. Nessa página, você também pode redefinir o PIN da caixa postal para o usuário.

## Use o Shell para recuperar as informações do PIN de um usuário habilitador para UM

Este exemplo exibe a ID do usuário, se o PIN expirou, se a caixa de correio da UM está bloqueada e se Tony é um usuário iniciante.

    Get-UMMailboxPIN -identity tony@contoso.com

