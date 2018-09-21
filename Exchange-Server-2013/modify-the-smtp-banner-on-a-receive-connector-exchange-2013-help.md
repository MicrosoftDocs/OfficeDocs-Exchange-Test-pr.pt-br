---
title: 'Modificar o banner SMTP em um conector de recebimento: Exchange 2013 Help'
TOCTitle: Modificar o banner SMTP em um conector de recebimento
ms:assetid: d667704e-fd69-4aca-9c35-eef7006944b2
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Bb124740(v=EXCHG.150)
ms:contentKeyID: 52058893
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Modificar o banner SMTP em um conector de recebimento

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2015-04-08_

O *Banner SMTP* é a resposta de conexão SMTP que um servidor de mensagens SMTP remoto recebe após se conectar a um conector de recebimento configurado em um computador executando o Microsoft Exchange Server 2013.

Esta é a resposta padrão recebida por um servidor de mensagens SMTP remoto depois que ele se conecta ao conector de recebimento:

    220 <Servername> Microsoft ESMTP MAIL service ready at <RegionalDay-Date-24HourTimeFormat> <RegionalTimeZoneOffset>

Quando você especifica um valor personalizado para um banner SMTP em um conector de Recebimento, um servidor de mensagem SMTP remoto que se conecta a esse conector de Recebimento SMTP recebe a seguinte resposta.

```powershell
220 <Banner Text>
```

Talvez você deseje modificar o banner SMTP de conectores de recebimento SMTP voltados para a Internet para que o nome do servidor e o software do servidor de mensagens não sejam revelados pelo banner SMTP.

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: 5 minutos

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Conectores de recebimento" no tópico [Permissões de fluxo de email](mail-flow-permissions-exchange-2013-help.md).

  - Você só pode usar o Shell para executar esse procedimento.

  - A cadeia de caracteres de texto da faixa SMTP de substituição deve ser sempre iniciada com `220`. Conforme definido no RFC 2821, o código de resposta padrão SMTP de serviço pronto é 220.

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>.



## Use o Shell para modificar o banner SMTP em um conector de Recebimento

Execute o seguinte comando:

```powershell
Set-ReceiveConnector <ConnectorIdentity> -Banner "220 <Banner Text>"
```

Este exemplo modifica o banner SMTP no conector de Recebimento existente nomeado Da Internet para que o banner SMTP mostre `220 Contoso Corporation`.

```powershell
Set-ReceiveConnector "From the Internet" -Banner "220 Contoso Corporation"
```

Este exemplo remove o banner SMTP personalizado no conector de Recebimento nomeado Da Internet, o que retorna o banner SMTP para o valor padrão.

```powershell
Set-ReceiveConnector "From the Internet" -Banner $null
```

## Como saber se funcionou?

Para verificar se você modificou com êxito o banner SMTP em um conector de Recebimento, faça o seguinte:

1.  Abra um Cliente Telnet em um computador que possa acessar o conector de recebimento e execute o seguinte comando:
    
    ```powershell
open <Connector FQDN or IP address> <Port>
```

2.  Verifique se a resposta do conector de Recebimento contém o banner SMTP que você configurou.

Observe que este procedimento só funciona em conectores de recebimento que permitem a autenticação anônima ou básica. Para obter mais informações, consulte [Usar Telnet para testar a comunicação SMTP](use-telnet-to-test-smtp-communication-exchange-2013-help.md).

