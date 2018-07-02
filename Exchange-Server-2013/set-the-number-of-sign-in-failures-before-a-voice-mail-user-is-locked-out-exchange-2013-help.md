---
title: 'Definir o número de falhas de entrada antes que um usuário de email de voz é bloqueado: Exchange 2013 Help'
TOCTitle: Definir o número de falhas de entrada antes que um usuário de email de voz é bloqueado
ms:assetid: 855e1980-2868-4983-b097-0b5f63f202b8
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Bb123544(v=EXCHG.150)
ms:contentKeyID: 50556220
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Definir o número de falhas de entrada antes que um usuário de email de voz é bloqueado

 

_**Aplica-se a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Tópico modificado em:** 2013-02-22_

Você pode configurar o número de falhas de entrar permitidas antes que um usuário de acesso de voz Outlook é bloqueado suas caixas de correio. O número de falhas de entrar permitidas antes que um usuário de email de voz é bloqueado está configurado em uma diretiva de caixa de correio de Unificação de mensagens (UM) e se aplica a todos os usuários habilitados para UM associados com a diretiva de caixa de correio de Unificação de mensagens. Por padrão, ela é definida como 15.

Para aumentar a segurança, diminua o número máximo de tentativas com falha. No entanto, lembre-se de que se você a diminuir a um número muito menor do que o padrão, os usuários podem ser bloqueados desnecessariamente. A Unificação de mensagens irá gerar eventos de aviso, que você pode exibir usando o Visualizador de eventos se a autenticação de PIN falhar para usuários habilitados para UM ou, se os usuários são bem sucedidos quando tentarem entrar no sistema. Essa configuração deve ser maior do que a configuração para o número de falhas de entrada antes do PIN ser redefinido.

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

## Usar o EAC para configurar o número de falhas de entrada antes de um usuário de email de voz está bloqueada

1.  No EAC, navegue até **Unificação de Mensagens** \> **Planos de discagem de UM**.

2.  Na exibição de lista, selecione o plano de discagem de UM que você deseja modificar e clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").

3.  Na página **Plano de discagem de UM**, em **Políticas de Caixa de Correio de UM**, selecione a política de caixa de correio de UM que você deseja alterar e clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").

4.  Clique em **diretivas de PIN** e, ao lado do **número de falhas de entrada antes do bloqueio**, digite um valor entre 1 e 999.

5.  Clique em **Salvar**.

## Use o Shell para configurar o número de falhas de entrada antes de um usuário de email de voz está bloqueada

Este exemplo define as máxima números entrar tentativas a 10 para usuários habilitados para Unificação de mensagens que estão associados a uma diretiva de caixa de correio de UM chamado `MyUMMailboxPolicy`.

    Set-UMMailboxPolicy -Identity MyUMMailboxPolicy -MaxLogonAttempts 10

Este exemplo define o número de falhas de entrada antes do Outlook Voice Access PIN do usuário é redefinido como 3, o número máximo de tentativas de entrar como 5 e um tamanho mínimo do PIN e 9 para usuários habilitados para Unificação de mensagens que estão associados a uma diretiva de caixa de correio de UM chamado `MyUMMailboxPolicy`.

    Set-UMMailboxPolicy -Identity MyUMMailboxPolicy -LogonFailuresBeforePINReset 3
    -MaxLogonAttempts 5 -MinPINLength 9

