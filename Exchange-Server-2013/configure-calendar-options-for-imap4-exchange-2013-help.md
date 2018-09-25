---
title: 'Configurar opções de calendário para o IMAP4: Exchange 2013 Help'
TOCTitle: Configurar opções de calendário para o IMAP4
ms:assetid: 6679c8b2-3f0f-449a-a17c-a7b30001538c
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Aa998606(v=EXCHG.150)
ms:contentKeyID: 50556214
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configurar opções de calendário para o IMAP4

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2012-11-27_

Você pode usar o Shell para definir configurações de acesso a calendário para seus usuários que se conectam às suas caixas de correio usando conexões IMAP4. As configurações que você especifica determinam como seus usuários IMAP4 podem acessar suas informações de calendário e calendário do Exchange (por exemplo, envio ou resposta a uma solicitação de reunião) com outros usuários.

Para mais informações relacionadas a IMAP4, consulte [POP3 e IMAP4 no Exchange Server 2013](pop3-and-imap4-in-exchange-server-2013-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: 5 minutos.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Configurações IMAP4" no tópico [Permissões de dispositivos móveis e clientes](clients-and-mobile-devices-permissions-exchange-2013-help.md).

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]  
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>..



## Usar o Shell para definir as opções de calendário para IMAP4

Este exemplo permite que os usuários de IMAP4 utilizem o padrão iCalendar, um padrão para trocar informações de calendário.

```powershell
Set-ImapSettings -Identity CAS01 -CalendarItemRetrievalOption iCalendar
```

Este exemplo permite que os usuários do IMAP4 acessem informações de calendário de um servidor interno.

  ```powershell
  Set-ImapSettings -Identity CAS01 -CalendarItemRetrievalOption IntranetUrl 
  ```

Este exemplo permite que os usuários do IMAP4 acessem informações de calendário na Internet em um servidor interno.

```powershell
Set-ImapSettings -CalendarItemRetrievalOption InternetUrl
```

Este exemplo permite que os usuários do IMAP4 acessem informações de calendário usando uma URL do Outlook Web App direta. Se estiver usando `Custom`, você deverá especificar uma URL do Outlook Web App utilizando o parâmetro *OWAServerUrl*.

```powershell
Set-Imap4Settings -CalendarItemRetrievalOption Custom -OwaServerUrl "https://OwaServer01"
```

Após especificar as opções de calendário para IMAP4, é preciso reiniciar os serviços IMAP4. Para informações sobre como reiniciar os serviços IMAP4, consulte [Iniciar e interromper os serviços de IMAP4](start-and-stop-the-imap4-services-exchange-2013-help.md).

Para obter mais informações sobre sintaxe e parâmetros, consulte [Set-ImapSettings](https://technet.microsoft.com/pt-br/library/aa998252\(v=exchg.150\)).

## Como saber se funcionou?

Para verificar se definiu com êxito as opções de calendário, faça o seguinte:

Execute o seguinte comando no Shell.

```powershell
Get-ImapSettings | format-list
```

Verifique se as configurações de calendário estão corretas.

## Para mais informações

Após definir as opções de calendário para IMAP4, você poderá também:

[Configurar opções de formato de recuperação mensagem POP3 e IMAP4](configure-pop3-and-imap4-message-retrieval-format-options-exchange-2013-help.md)

[Definir limites de tempo limite de conexão para IMAP4](set-connection-time-out-limits-for-imap4-exchange-2013-help.md)