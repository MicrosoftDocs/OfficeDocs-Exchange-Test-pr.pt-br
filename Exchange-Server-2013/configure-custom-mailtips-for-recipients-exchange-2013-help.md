---
title: 'Configurar Dicas de Email personalizadas para destinatários: Exchange 2013 Help'
TOCTitle: Configurar Dicas de Email personalizadas para destinatários
ms:assetid: df8ee7ae-2486-4890-b057-cda87b4cb1ec
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Dd638199(v=EXCHG.150)
ms:contentKeyID: 52058514
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configurar Dicas de Email personalizadas para destinatários

 

_**Aplica-se a:**Exchange Online, Exchange Server 2013_

_**Tópico modificado em:**2014-06-01_

*Dicas de email* são mensagens informativas exibidas aos usuários na barra de informações no Outlook Web App e no Microsoft Outlook 2010 ou posterior quando um usuário realiza qualquer uma das seguintes ações ao criar uma mensagem de email:

  - Adiciona um destinatário

  - Adiciona um anexo

  - Responde ou responde a todos

  - Abre uma mensagem na pasta Rascunhos que já esteja endereçada aos destinatários

Além das Dicas de Email integradas que estão disponíveis, você pode criar dicas de email personalizadas para todos os tipos de destinatários. Para obter mais informações sobre as dicas de email integradas, consulte [MailTips](mailtips-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: 10 minutos

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Dicas de Email" no tópico [Permissões de fluxo de email](mail-flow-permissions-exchange-2013-help.md).

  - Você pode configurar a dica de email primária no Centro de Administração do Exchange (EAC) ou no Shell. No entanto, você só pode configurar traduções de dicas de email adicionais no Shell.

  - Quando você adiciona uma dica de email a um destinatário, duas coisas acontecem:
    
      - As marcas HTML serão adicionadas automaticamente ao texto. Por exemplo, se você inserir o texto: `This mailbox is not monitored`, a dica de email automaticamente se tornará: `<html><body>This mailbox is not monitored</body></html>`. Não há suporte para marcas HTML adicionais nas Dicas de Email.
    
      - O texto será adicionado automaticamente à propriedade *MailTipTranslations* do destinatário, como o valor padrão. Se você modificar o texto da dica de email, o valor padrão será atualizado automaticamente na propriedade *MailTipTranslations*.

  - O comprimento de uma dica de email não pode exceder 175 caracteres exibidos.

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>.



## O que você deseja fazer?

## Configurar dicas de email para destinatários

## Usar o EAC para configurar as dicas de email para os destinatários

1.  No EAC, navegue até **Destinatários**.

2.  Selecione qualquer uma das seguintes guias de destinatários com base no tipo de destinatário:
    
      - **Caixas de correio**
    
      - **Grupos**
    
      - **Recursos**
    
      - **Contacts**
    
      - **Shared**

3.  Na guia Destinatário, selecione o destinatário que você deseja modificar e clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").

4.  Na página propriedades do destinatário que aparece, clique em **Dicas de email**.

5.  Digite o texto da dica de email. Quando terminar, clique em **Salvar**.

## Usar o Shell para configurar as dicas de email para os destinatários

Para configurar uma dica de email para um recipiente, use a seguinte sintaxe.

    Set-<RecipientType> <RecipientIdentity> -MailTip "<MailTip text>"

*\<RecipientType\>* pode ser qualquer tipo de destinatário. Por exemplo, `Mailbox`, `MailUser`, `MailContact`, `DistributionGroup` ou `DynamicDistributionGroup`.

Por exemplo, suponha que você tenha uma caixa de correio denominada "Assistência técnica" para que os usuários enviem solicitações de suporte e que o tempo de resposta prometido seja de duas horas. Para configurar uma dica de email personalizada explicando isso, execute este comando:

    Set-Mailbox "Help Desk" -MailTip "A Help Desk representative will contact you within 2 hours."

## Use o Shell para configurar dicas de email personalizadas em idiomas diferentes

Para configurar conversões de dica de email adicionais sem afetar o texto da dica de email existente nem outras traduções de dica de email existentes, use a seguinte sintaxe:

    Set-<RecipientType> -MailTipTranslations @{Add="<culture1>:<localized text 1>","<culture2>:<localized text 2>"...; Remove="<culture1>:<localized text 1>","<culture2>:<localized text 2>"...}

*\<culture\>* é um código de cultura ISO 639 válido de duas letras associado ao idioma.

Por exemplo, suponha que a caixa de correio chamada "Notificações" atualmente tenha a dica de email: "Esta caixa de correio não é monitorada." Para adicionar a tradução para o espanhol, execute o seguinte comando:

    Set-Mailbox -MailTipTranslations @{Add="ES:Esta caja no se supervisa."}

## Como saber se funcionou?

Para verificar se você configurou com êxito a dica de email para um destinatário, faça o seguinte:

1.  No Outlook Web App, no Outlook 2010 ou posterior, escreva uma mensagem de email endereçada ao destinatário, mas não a envie.

2.  Verifique se a Dica de Email aparece na Barra de Informações.

3.  Se você configurou traduções de dica de email adicionais, escreva a mensagem no Outlook Web App onde a configuração de idioma corresponde ao idioma da tradução da dica de email, a fim de verificar os resultados.

