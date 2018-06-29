---
title: 'Definir diretivas de PIN do Outlook Voice Access: Exchange 2013 Help'
TOCTitle: Definir diretivas de PIN do Outlook Voice Access
ms:assetid: 5b2800b7-bfa6-4282-975c-0706ae25ad64
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Aa998285(v=EXCHG.150)
ms:contentKeyID: 50556206
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Definir diretivas de PIN do Outlook Voice Access

 

_**Aplica-se a:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Tópico modificado em:**2013-02-22_

Você pode definir diretivas de PIN em uma diretiva de caixa de correio de UM (Unificação de Mensagens). As políticas de caixa de correio da UM podem ser configuradas para aumentar o nível de segurança dos usuários habilitados pela UM que usam o Outlook Voice Access ao solicitar que os usuários atuem de acordo com as políticas de PIN predefinidas da sua organização.

Para definir políticas de PIN para usuários do Outlook Voice Access, crie uma nova política de caixa de correio de UM ou modifique uma política de caixa de correio de UM existente. Depois de criar uma nova diretiva de caixa de correio do UM, você poderá configurar a diretiva de caixa de correio do UM, definindo as seguintes configurações de PIN:

  - `MinPasswordLength`

  - `PINLifetime`

  - `LogonFailuresBeforePINReset`

  - `MaxLogonAttempts`

  - `AllowCommonPatterns`

  - `PINHistoryCount`

É uma prática recomendada de segurança implementar requisitos de PIN fortes para usuários de UM. Isso pode ser reforçado pela criação de diretivas de PIN de UM que exigem 6 ou mais dígitos para PINs e aumentam o nível de segurança da rede.

Quando você altera a diretiva de PIN, as novas configurações de PIN são aplicadas aos usuários associados à diretiva de caixa de correio do UM atual. Por exemplo, se você modificar a diretiva de caixa de correio de UM e alterar o comprimento mínimo do PIN de 7 para 10 dígitos, na próxima vez em que os usuários fizerem logon, eles serão forçados a alterar os respectivos PINs para atender ao requisito do PIN alterado.

Para tarefas adicionais relacionadas à segurança do PIN do Outlook Voice Access, consulte [Procedimentos de segurança PIN](pin-security-procedures-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: 5 minutos.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Diretivas de caixa de correio da UM" no tópico [Permissões de mensagens unificadas](unified-messaging-permissions-exchange-2013-help.md).

  - Antes de executar esses procedimentos, confirme se um plano de discagem da UM foi criado. Para obter etapas detalhadas, consulte [Criar um plano de discagem de UM](create-a-um-dial-plan-exchange-2013-help.md).

  - Antes de executar esses procedimentos, verifique se uma política de caixa de correio de UM foi criada. Para obter etapas detalhadas, consulte [Criar uma política de caixa de correio da UM](create-a-um-mailbox-policy-exchange-2013-help.md).

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>..



## O que você deseja fazer?

## Usar o EAC para definir políticas de PIN para usuários do Outlook Voice Access

1.  No EAC, navegue até **Unificação de Mensagens** \> **Planos de discagem de UM**. No modo de exibição de lista, clique no plano de discagem de UM que deseja editar e clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").

2.  Na página **Plano de Discagem de UM**, em **Políticas de Caixa de Correio de UM**, selecione a política de caixa de correio de UM que deseja editar e clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").

3.  Clique em **Propriedades**.

4.  Na página **Política de caixa de correio de UM**, clique na guia **Políticas de PIN**.

5.  Na página **Políticas de PIN**, defina as configurações de PIN dos usuários do Outlook Voice Access associados a esta política de caixa de correio de UM e clique em **Salvar**.

## Usar o Shell para definir políticas de PIN para usuários do Outlook Voice Access

Este exemplo define as configurações de PIN para usuários associados à diretiva de caixa de correio de UM `MyUMMailboxPolicy`.

    Set-UMMailboxPolicy -Identity MyUMMailboxPolicy -LogonFailuresBeforePINReset 8 -MaxLogonAttempts 12 -MinPINLength 8 -PINHistoryCount 10 -PINLifetime 60 -ResetPINText "The PIN used to allow you access to your mailbox using Outlook Voice Access has been reset."

