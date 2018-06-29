---
title: 'Definir o número de falhas de entrada antes de uma redefinição de PIN de caixa postal: Exchange 2013 Help'
TOCTitle: Definir o número de falhas de entrada antes de uma redefinição de PIN de caixa postal
ms:assetid: 4de38499-0a6f-4f00-8697-eeff805d7266
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Aa997939(v=EXCHG.150)
ms:contentKeyID: 50556185
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Definir o número de falhas de entrada antes de uma redefinição de PIN de caixa postal

 

_**Aplica-se a:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Tópico modificado em:**2013-02-22_

Você pode configurar o número de falhas de logon permitidas antes que um PIN seja redefinido para um usuário do Outlook Voice Acess em um valor de 1 até 998. O padrão é 5. O número de falhas de logon permitidas antes que um PIN seja redefinido é configurado em uma política de caixa de correio de Unificação de Mensagens (UM) e se aplica a todos os usuários do Outlook Voice Access associados à política de caixa de correio de UM.


> [!TIP]
> É possível aumentar a segurança definindo a configuração <STRONG>Número de falhas de entrada antes da redefinição do PIN</STRONG> para um número menor que 5. Você diminuirá a segurança se definir a configuração para um número maior que 5.



Para tarefas adicionais relacionadas à segurança do PIN do Outlook Voice Access, consulte [Procedimentos de segurança PIN](pin-security-procedures-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: 3 minutos.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Diretivas de caixa de correio da UM" no tópico [Permissões de mensagens unificadas](unified-messaging-permissions-exchange-2013-help.md).

  - Antes de executar esses procedimentos, confirme se um plano de discagem da UM foi criado. Para obter etapas detalhadas, consulte [Criar um plano de discagem de UM](create-a-um-dial-plan-exchange-2013-help.md).

  - Antes de executar esses procedimentos, verifique se uma política de caixa de correio de UM foi criada. Para obter etapas detalhadas, consulte [Criar uma política de caixa de correio da UM](create-a-um-mailbox-policy-exchange-2013-help.md).

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>..



## O que você deseja fazer?

## Usar o EAC para configurar o número de falhas de logon antes que um PIN seja redefinido

1.  No EAC, navegue até **Unificação de Mensagens** \> **Planos de discagem de UM**.

2.  Na exibição de lista, selecione o plano de discagem de UM que você deseja modificar e clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").

3.  Na página **Plano de discagem de UM**, em **Políticas de Caixa de Correio de UM**, selecione a política de caixa de correio de UM que você deseja alterar e clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").

4.  Na guia **Políticas de PIN** e ao lado de **Número de falhas de entrada antes da redefinição do PIN**, insira um valor entre 0 e 999.

5.  Clique em **Salvar**.

## Usar o Shell para configurar o número de falhas de logon antes que um PIN seja redefinido

Este exemplo define o número de falhas de logon para que o PIN do usuário seja redefinido como 3 para usuários habilitados para UM que estejam associados a uma política de caixa de correio de UM denominada `MyUMMailboxPolicy`.

    Set-UMMailboxPolicy -Identity MyUMMailboxPolicy -LogonFailuresBeforePINReset 3

Este exemplo define o número de falhas de logon para que o PIN do usuário seja redefinido como 3, o número máximo de tentativas de logon como 5 e o tamanho mínimo de PIN como 9 para usuários habilitados para UM que estejam associados a uma política de caixa de correio de UM denominada `MyUMMailboxPolicy`.

    Set-UMMailboxPolicy -Identity MyUMMailboxPolicy -LogonFailuresBeforePINReset 3 -MaxLogonAttempts 5 -MinPINLength 9

