---
title: 'Definir o comprimento mínimo do PIN para caixa postal: Exchange 2013 Help'
TOCTitle: Definir o comprimento mínimo do PIN para caixa postal
ms:assetid: b2ecab54-42e6-45af-8322-615cc1f68dd9
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Bb124271(v=EXCHG.150)
ms:contentKeyID: 50556264
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Definir o comprimento mínimo do PIN para caixa postal

 

_**Aplica-se a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Tópico modificado em:** 2013-02-22_

Você pode definir o tamanho mínimo do PIN para os usuários do Outlook Voice Access habilitados para Unificação de mensagens (UM). As configurações de PIN que você define em uma diretiva de caixa de correio UM se aplicará a todos os usuários habilitados para UM associados com a diretiva de caixa de correio de Unificação de mensagens.

Outlook Acesso de voz é usado pelo usuários habilitados para acessar sua caixa postal, email, calendário e informações de contato pessoal, localizada em suas caixas de correio. No entanto, antes que eles possam acessar suas caixas de correio, eles devem digitar um PIN para que possam ser autenticados pelo sistema de correio de voz.


> [!TIP]
> Se você alterar o valor de comprimento mínimo do PIN, os usuários existentes do Outlook Voice Access deverá inserir um novo PIN que contém o novo número mínimo de dígitos antes que possam continuar. O padrão é 6.



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

## Usar o EAC para configurar o tamanho mínimo do PIN do Outlook Voice Access

1.  No EAC, navegue até **Unificação de Mensagens** \> **Planos de discagem de UM**.

2.  Na exibição de lista, selecione o plano de discagem que você deseja alterar e clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").

3.  Na página **Plano de discagem de UM**, em **Políticas de Caixa de Correio de UM**, selecione a política de caixa de correio de UM que você deseja alterar e clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").

4.  Clique em **diretivas de PIN** e, ao lado de **tamanho mínimo do PIN**, digite um valor entre 4 e 24.

5.  Clique em **Salvar**.

## Use o Shell para configurar o tamanho mínimo do PIN do Outlook Voice Access

Este exemplo define o tamanho mínimo do PIN 8 dígitos para usuários do Outlook Voice Access que estão associados com a política de caixa de correio de Unificação de mensagens chamada `MyUMMailboxPolicy`.

    Set-UMMailboxPolicy -Identity MyUMMailboxPolicy -MinPINLength 8

Este exemplo define o tamanho mínimo do PIN 8 dígitos e define o número de vezes que um entrar pode falhar antes que o PIN do usuário é redefinido como 3. Isso se aplica aos usuários habilitados para UM associados com a diretiva de caixa de correio de Unificação de mensagens denominada `MyUMMailboxPolicy`.

    Set-UMMailboxPolicy -Identity MyUMMailboxPolicy -LogonFailuresBeforePINReset 3 -MinPINLength 8

