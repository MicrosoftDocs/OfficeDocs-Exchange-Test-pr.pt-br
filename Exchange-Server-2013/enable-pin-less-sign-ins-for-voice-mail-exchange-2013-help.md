---
title: 'Habilitar o PIN sem entradas para caixa postal: Exchange 2013 Help'
TOCTitle: Habilitar o PIN sem entradas para caixa postal
ms:assetid: 54133753-317c-42ef-9b0d-ca9f2d2d6bd7
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Gg602127(v=EXCHG.150)
ms:contentKeyID: 54651965
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Habilitar o PIN sem entradas para caixa postal

 

_**Aplica-se a:** Exchange Server 2010 Service Pack 2 (SP2), Exchange Server 2013, Exchange Server 2016_

_**Tópico modificado em:** 2015-04-08_

Você pode configurar a Unificação de Mensagens para que os usuários possam entrar no seu correio de voz sem usar um PIN. Por padrão, os usuários do Outlook Voice Access são solicitados a inserir um PIN para entrar em suas caixas de correio e acessar suas caixas postais, emails, calendários, contatos pessoais, diretórios e opções pessoais.


> [!WARNING]
> Habilitar entradas com menos PIN para um único usuário ou um grupo de usuários habilitados para caixa postal diminui o nível de segurança para o correio de voz e representa um risco de segurança para sua organização.



Para habilitar entradas com menos PIN, defina o parâmetro *AllowPinlessVoiceMailAccess* como `$true` na política de caixa de correio de UM e defina o parâmetro *PinlessAccessToVoiceMailEnabled* como `$true` na caixa de correio de UM. Por padrão, os dois parâmetros são definidos como `$false`, o que exige que um usuário do Outlook Voice Access informe seu PIN ao acessar a caixa postal.

Configurar os dois parâmetros como `$true` permite habilitar entradas sem PIN para um grupo grande de usuários associados a uma caixa de correio de UM e também permite entradas sem PIN para uma única caixa de correio de UM ou um subconjunto de caixas de correio de UM. Mesmo que você habilite entradas sem PIN para um grupo de usuários habilitados para a UM ou para um único usuário habilitado para a UM, eles terão que informar o PIN para ter acesso ao email, ao calendário, aos contatos pessoais, ao diretório ou às opções pessoais.

Para habilitar entradas sem PIN na caixa postal para um usuário, as condições a seguir devem ser atendidas:

  - Você deve ter executado o seguinte cmdlet na política de caixa de correio de UM: `Set-UMMailboxPolicy -id MyUMMailboxPolicy -AllowPinlessVoiceMailAccess $true`

  - Você deve ter executado o seguinte cmdlet na caixa de correio do usuário habilitado para a UM: `Set-UMMailbox -id tonys@contoso.com -PinlessAccessToVoiceMailEnabled $true`

  - O usuário habilitado para a UM está associado à mesma política de caixa de correio de UM para a qual as entradas sem PIN foram habilitadas.

  - O usuário habilitado para a UM disca para o Outlook Voice Access a partir de um número de telefone que foi atribuído a ele.

  - Você só pode usar o Shell para executar esse procedimento. Para saber como abrir o Shell de Gerenciamento do Exchange em sua organização Exchange local, confira [Abra o shell.](https://technet.microsoft.com/pt-br/library/dd638134\(v=exchg.150\)). Para saber como usar o Windows PowerShell para se conectar ao Exchange Online, confira o artigo [Conectar-se ao Exchange Online PowerShell](https://go.microsoft.com/fwlink/p/?linkid=396554).

Para outras tarefas relacionadas a políticas de caixa de correio de UM, consulte [Procedimentos de diretiva de caixa de correio de Unificação de mensagens](https://docs.microsoft.com/pt-br/exchange/voice-mail-unified-messaging/set-up-voice-mail/um-mailbox-policy-procedures).

Para tarefas adicionais relacionadas às caixas de correio da UM, consulte [Procedimentos do usuário habilitado para email de voz](https://docs.microsoft.com/pt-br/exchange/voice-mail-unified-messaging/set-up-voice-mail/voice-mail-enabled-user-procedures).

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: 3 minutos.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Políticas de caixa de correio de UM", no tópico [Permissões de mensagens unificadas](unified-messaging-permissions-exchange-2013-help.md).

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Caixas de correio de UM", no tópico [Permissões de mensagens unificadas](unified-messaging-permissions-exchange-2013-help.md).

  - Antes de executar esses procedimentos, confirme se um plano de discagem de UM foi criado. Para conhecer etapas detalhadas, consulte [Criar um plano de discagem de UM](https://docs.microsoft.com/pt-br/exchange/voice-mail-unified-messaging/connect-voice-mail-system/create-um-dial-plan).

  - Antes de executar esses procedimentos, verifique se uma política de caixa de correio de UM foi criada. Para conhecer etapas detalhadas, consulte [Criar uma política de caixa de correio da UM](https://docs.microsoft.com/pt-br/exchange/voice-mail-unified-messaging/set-up-voice-mail/create-um-mailbox-policy).

  - Antes de executar esses procedimentos, confirme se o usuário ou usuários foram habilitados para o correio de voz e UM. Para conhecer etapas detalhadas, consulte [Habilitar um usuário para caixa postal](https://docs.microsoft.com/pt-br/exchange/voice-mail-unified-messaging/set-up-voice-mail/enable-a-user-for-voice-mail).

## O que você deseja fazer?

## Usar o Shell para habilitar acesso sem PIN à caixa postal para usuários habilitados para a UM em uma diretiva de caixa de correio da UM

Este exemplo permite o acesso à caixa postal sem PIN em uma política de caixa de correio da UM chamada `MyUMMailboxPolicy` para usuários associados à política de caixa de correio que discarem para o Outlook Voice Access.

```powershell
Set-UMMailboxPolicy -id MyUMMailboxPolicy -AllowPinlessVoiceMailAccess $true
```

## Usar o Shell para habilitar acesso sem PIN à caixa postal em uma caixa de correio de usuário habilitado para a UM

Este exemplo permite o acesso à caixa postal sem PIN para o usuário que discar para o Outlook Voice Access para alcançar a caixa de correio chamada `tonys@contoso.com`.

```powershell
Set-UMMailbox -id tonys@contoso.com -PinlessAccessToVoiceMailEnabled $true
```

