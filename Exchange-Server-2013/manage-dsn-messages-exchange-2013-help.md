---
title: 'Gerenciar mensagens DSN: Exchange 2013 Help'
TOCTitle: Gerenciar mensagens DSN
ms:assetid: 23c9d844-6fc7-44c9-a308-587338281611
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Aa996803(v=EXCHG.150)
ms:contentKeyID: 50485186
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Gerenciar mensagens DSN

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2013-02-20_

O Microsoft Exchange Server 2013 usa notificações de status de entrega (DSN) para oferece notificações de falha de entrega (NDRs) e outras mensagens de status para remetentes de mensagens. Você pode usar os DSNs integrados ou pode criar mensagens DSN personalizadas que atendam às necessidades da sua organização.

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: 15 minutos

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "DSNs" no tópico [Permissões de fluxo de email](mail-flow-permissions-exchange-2013-help.md).

  - Você não pode remover uma mensagem DSN interna que está incluída no Exchange. Para alterar a mensagem DSN interna, você deve criar uma mensagem DSN personalizada para o código DSN que você deseja personalizar. Ao remover uma mensagem DSN personalizada, o código DSN associado à mensagem reverte à mensagem DSN original incluída no Exchange.

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>.



## O que você deseja fazer?

## Usar o Shell para exibir as mensagens de DSN internas e personalizadas

Para exibir uma lista resumida de todas as mensagens DSN incluídas com o Exchange 2013, execute este comando:

```powershell
Get-SystemMessage -Original
```

Para exibir uma lista resumida de todas as mensagens DSN na sua organização, execute este comando:

```powershell
Get-SystemMessage
```

Para exibir informações detalhadas da mensagem DSN para o código DSN 5.1.2 que é enviada a remetentes internos em inglês, execute este comando:

```powershell
Get-SystemMessage En\Internal\5.1.2 | Format-List
```

## Usar o Shell para criar uma mensagem DSN personalizada

Execute o seguinte comando:

    New-SystemMessage -Internal <$true | $false> -Language <Locale> -DSNCode <x.y.z> -Text "<DSN text>"

Este exemplo cria uma mensagem DSN personalizada em texto simples para o código DSN 5.1.2 que é enviada para remetentes internos em inglês.

    New-SystemMessage -Internal $true -Language En -DSNCode 5.1.2 -Text "You tried to send a message to a disabled mailbox that's no longer accepting messages. Please contact the Help Desk at extension 123 for assistance."

Este exemplo cria uma mensagem DSN personalizada em texto simples para o código DSN 5.1.2 que é enviada para remetentes externos em inglês.

    New-SystemMessage -Internal $false -Language En -DSNCode 5.1.2 -Text "You tried to send a message to a disabled mailbox that's no longer accepting messages. Please contact your System Administrator for more information."

Este exemplo cria uma mensagem DSN personalizada em HTML para o código DSN 5.1.2 que é enviada para remetentes internos em inglês.

    New-SystemMessage -DSNCode 5.1.2 -Internal $true -Language En -Text 'You tried to send a message to a <B>disabled</B> mailbox. Please visit <A HREF="http://it.contoso.com">Internal Support</A> or contact &quot;InfoSec&quot; for more information.'

## Como saber se funcionou?

Para verificar se você criou com êxito uma mensagem DNS personalizada, faça o seguinte:

1.  Execute o seguinte comando:
    
    ```powershell
Get-SystemMessge -DSNCode <x.y.z> | Format-List Name,Internal,Text,Language
```

2.  Verifique se os valores exibidos são os valores que você configurou.

3.  Envie uma mensagem de teste que irá gerar o DSN personalizado você configurou.

## Usar o shell para alterar o texto de uma mensagem DSN personalizada

Para alterar o texto de uma mensagem DSN personalizada, use o seguinte comando:

    Set-SystemMessage <Locale>\<Internal | External>\<DSNcode> -Text "<DSN text>"

Este exemplo altera o texto atribuído à mensagem DSN personalizada para o código DSN 5.1.2 que é enviada para remetentes internos em inglês.

    Set-SystemMessage En\Internal\5.1.2 -Text "The mailbox you tried to send an e-mail message to is disabled and is no longer accepting messages. Please contact the Help Desk at extension 123 for assistance."

## Como saber se funcionou?

Para verificar se você alterou com êxito o texto de uma mensagem DNS personalizada, faça o seguinte:

1.  Execute o seguinte comando: `Get-SystemMessage`.
    
    ```powershell
Set-SystemMessage <Locale>\<Internal | External>\<DSNcode> | Format-List -Text
```

2.  Verifique se o valor apresentado é o valor que você configurou.

## Usar o Shell para remover uma mensagem DSN personalizada

Execute o seguinte comando:

```powershell
Remove-SystemMessage <Local>\<Internal | External>\<DSNcode>
```

Este exemplo remove uma mensagem DSN personalizada para o código DSN 5.1.2 que é enviada para remetentes internos em inglês.

```powershell
Remove-SystemMessage En\Internal\5.1.2
```

## Como saber se funcionou?

Para verificar se você removeu com êxito uma mensagem DNS personalizada, faça o seguinte:

1.  Execute o comando: `Get-SystemMessage`.

2.  Verifique o DSN, para ver se o local, os destinatários internos e externos e o código DSN que você excluiu não estão listados.

## Encaminhar cópias das mensagens DSN para a caixa de correio de destinatário do Exchange

Você pode especificar uma lista de códigos DSN que você deseja monitorar, copiando as mensagens DSN para a caixa de correio do destinatário do Exchange. Entretanto, por padrão, nenhuma caixa de correio é atribuída ao destinatário do Exchange, de modo que nenhuma mensagem enviada ao destinatário do Exchange é descartada. Para enviar cópias das mensagens DSN para a caixa de correio de destinatário do Exchange, você precisa atribuir uma caixa de correio ao destinatário do Exchange e especificar os códigos DSN que você deseja monitorar. Por padrão, os seguintes códigos de notificação de status de entrega são monitorados: `5.4.8`, `5.4.6`, `5.4.4`, `5.2.4`, `5.2.0` e `5.1.4`.

## Etapa 1: Usar o Shell para atribuir uma caixa de correio ao destinatário do Exchange

Para atribuir uma caixa de correio ao destinatário do Exchange, siga estas instruções:

1.  Devido ao volume potencialmente alto de emails, considere criar uma caixa de correio dedicada e uma conta de usuário do Active Directory para o destinatário do Exchange. Para obter mais informações, consulte [Criar caixas de correio do usuário](create-user-mailboxes-exchange-2013-help.md). Do contrário, identifique a caixa de correio existente que você deseja associar ao destinatário do Exchange.

2.  Execute o seguinte comando:
    
    ```powershell
Set-OrganizationConfig -MicrosoftExchangeRecipientReplyRecipient <MailboxIdentity>
```
    
    Por exemplo, para atribuir a caixa de correio existente chamada "Contoso System Mailbox" ao destinatário do Exchange, execute o seguinte comando:
    
    ```powershell
Set-OrganizationConfig -MicrosoftExchangeRecipientReplyRecipient "Contoso System Mailbox"
```

## Etapa 2: Especificar os códigos DSN que você deseja monitorar

## Usar o EAC para especificar os códigos DSN

1.  No EAC, navegue até **Fluxo de email** \> **Conectores de recebimento** \> **Mais opções**![Ícone Mais opções](images/JJ150550.5381819e-3b21-4873-8714-e9b956290b28(EXCHG.150).gif "Ícone Mais opções") \> **Configurações de transporte da organização** \> **Entrega**.

2.  Na seção **Códigos DNS**, digite os códigos DSN que você deseja monitorar, usando o formato *\<x.y.z\>* e clique em **Adicionar**![Ícone Adicionar](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Ícone Adicionar"). Selecione uma entrada existente e clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição"), para modificá-la, ou em **Remover**![ícone Remover](images/JJ657492.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "ícone Remover"), para removê-la. Quando você tiver concluído, clique em **Salvar**.

## Usar o Shell para especificar os códigos DSN

Para substituir os valores existentes, execute o seguinte comando:

```powershell
Set-TransportConfig -GenerateCopyOfDSNFor <x.y.z>,<x.y.z>...
```

Este exemplo configura a organização do Exchange para encaminhar todas as mensagens DSN que tenham os códigos DSN 5.7.1, 5.7.2 e 5.7.3 para o destinatário do Exchange.

```powershell
Set-TransportConfig -GenerateCopyOfDSNFor 5.7.1,5.7.2,5.7.3
```

Para adicionar ou remover entradas sem modificar quaisquer valores existentes, execute este comando:

    Set-TransportConfig -GenerateCopyOfDSNFor @{Add="<x.y.z>","<x.y.z>"...; Remove="<x.y.z>","<x.y.z>"...}

Este exemplo adiciona o código DSN 5.7.5 e remove o código DSN 5.7.1 da lista existente de mensagens DSN que são encaminhadas para o destinatário do Exchange.

```powershell
Set-TransportConfig -GenerateCopyOfDSNFor @{Add="5.7.5"; Remove="5.7.1"}
```

## Como saber se funcionou?

Para verificar se você configurou com êxito cópias das mensagens DNS a serem enviadas para a caixa de correio do destinatário do Exchange, monitore a caixa de correio que é associada ao destinatário do Exchange e verifique se as mensagens DSN contêm os códigos DSN que você especificou.

