---
title: 'Configurar opções de calendário para POP3: Exchange 2013 Help'
TOCTitle: Configurar opções de calendário para POP3
ms:assetid: ac3d60a0-8697-4c06-9e93-f8d2c4b157b6
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Bb124133(v=EXCHG.150)
ms:contentKeyID: 50556261
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configurar opções de calendário para POP3

 

_**Aplica-se a:**Exchange Server 2013_

_**Tópico modificado em:**2012-11-27_

Você pode usar o Shell para definir configurações de acesso de calendário para os usuários que se conectam a suas caixas de correio usando POP3 conexões. As configurações especificadas determinam como os seus usuários POP3 podem acessar suas informações de calendário de calendário e do exchange (por exemplo, enviar ou responder a uma solicitação de reunião) com outros usuários.

Para mais informações relacionadas a POP3, consulte [POP3 e IMAP4 no Exchange Server 2013](pop3-and-imap4-in-exchange-server-2013-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: 5 minutos.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Configurações POP3" no tópico [Permissões de dispositivos móveis e clientes](clients-and-mobile-devices-permissions-exchange-2013-help.md).

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>..



## Use o Shell para definir as opções de calendário para POP3

Este exemplo habilita usuários POP3 usar o padrão de iCalendar, um padrão de troca de informações de calendário.

    Set-PopSettings -Identity CAS01 -CalendarItemRetrievalOption iCalendar

Este exemplo habilita usuários POP3 acessar informações de calendário de um servidor interno.

    Set-PopSettings -Identity CAS01 -CalendarItemRetrievalOption IntranetUrl 

Este exemplo habilita usuários POP3 acessar informações do calendário da Internet em um servidor externo.

    Set-PopSettings -CalendarItemRetrievalOption InternetUrl

Este exemplo habilita usuários POP3 para acessar informações de calendário usando uma URL direta Outlook Web App. Se você estiver usando `Custom`, você deve especificar uma URL do Outlook Web App usando o parâmetro *OWAServerUrl* .

    Set-PopSettings -CalendarItemRetrievalOption Custom -OwaServerUrl "https://OwaServer01"

Após especificar as opções de calendário para POP3, você deve reiniciar os serviços POP3. Para obter informações sobre como reiniciar os serviços POP3, consulte [Iniciar e interromper os serviços POP3](start-and-stop-the-pop3-services-exchange-2013-help.md).

Para obter mais informações sobre sintaxe e parâmetros, consulte [Set-PopSettings](https://technet.microsoft.com/pt-br/library/aa997154\(v=exchg.150\)).

## Como saber se funcionou?

Para verificar se definiu com êxito as opções de calendário, faça o seguinte:

Execute o seguinte comando no Shell.

    Get-PopSettings | format-list

Verifique se as configurações de calendário estão corretas.

## Para mais informações

Depois de definir as opções de calendário para POP3, você também pode querer:

[Configurar opções de formato de recuperação mensagem POP3 e IMAP4](configure-pop3-and-imap4-message-retrieval-format-options-exchange-2013-help.md)

[Definir limites de tempo limite de conexão para POP3](set-connection-time-out-limits-for-pop3-exchange-2013-help.md)

