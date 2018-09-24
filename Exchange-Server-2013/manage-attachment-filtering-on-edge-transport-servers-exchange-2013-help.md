---
title: 'Filtragem de anexos em servidores de transporte de borda: Exchange 2013 Help'
TOCTitle: Gerenciar filtragem de anexos nos servidores de transporte de borda
ms:assetid: 2ec91cc6-6ade-48ee-88bb-66153874393d
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Aa997139(v=EXCHG.150)
ms:contentKeyID: 60829927
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Gerenciar filtragem de anexos nos servidores de transporte de borda

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2015-04-08_

A filtragem de anexo é fornecida pelo agente de Filtro de Anexo disponível somente em servidores Transporte de Borda. A filtragem de anexo pode ajudar a impedir que arquivos anexados a mensagens de email entrem em sua organização. É possível configurar uma ou mais entradas de filtro de anexo para filtrar anexos por tipo de conteúdo ou nome de arquivo.

## O que você precisa saber antes de começar?

  - Tempo estimado para concluir cada procedimento: 10 minutos.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Recursos antispam" no tópico [Permissões antispam e antimalware](anti-spam-and-anti-malware-permissions-exchange-2013-help.md) e entrada "Agentes de transporte" no tópico [Permissões de fluxo de email](mail-flow-permissions-exchange-2013-help.md).

  - As alterações de configuração feitas na filtragem de anexo em um servidor de Transporte de Borda são feitas somente no computador local. Se você tiver vários servidores de Transporte de Borda em sua rede de perímetro, precisará configurar a filtragem de anexo em cada servidor de Transporte de Borda separadamente.

  - Você só pode usar o Shell para executar esse procedimento.

  - Quando você desabilita a filtragem de anexo e reinicia o serviço de Transporte do Microsoft Exchange, todos os recursos de filtragem de anexo param de funcionar.

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>.



## O que você deseja fazer?

## Usar o Shell para habilitar ou desabilitar a filtragem de anexos

Quando você habilita ou desabilita o agente de Filtragem de Anexos, a alteração entra em vigor após o reinício do serviço de Transporte do Microsoft Exchange. Quando você reinicia o serviço de Transporte do Microsoft Exchange em um servidor de Transporte de Borda, o fluxo de mensagens no servidor é temporariamente interrompido.

Para desabilitar a filtragem de anexos, execute o seguinte comando:

```powershell
Disable-TransportAgent "Attachment Filtering Agent"
```

Para habilitar a filtragem de anexos, execute o seguinte comando:

```powershell
Enable-TransportAgent "Attachment Filtering Agent"
```

Depois de habilitar ou desabilitar a filtragem de anexos, reinicie o serviço de Transporte do Microsoft Exchange executando o seguinte comando:

```powershell
Restart-Service MSExchangeTransport
```

## Como saber se funcionou?

Para verificar se você habilitou ou desabilitou com êxito a filtragem de anexos, faça o seguinte:

1.  Execute o seguinte comando:
    
    ```powershell
Get-TransportAgent "Attachment Filtering Agent"
```

2.  Se o valor de **Enabled** for `True`, a filtragem de anexos estará habilitada. Se o valor for `False`, a filtragem de anexos estará desabilitada.

## Usar o Shell para exibir entradas de filtragem de anexos

As entradas de filtragem de anexos definem os anexos de mensagem que você deseja manter fora de sua organização. Para exibir as entradas de filtragem de anexos usadas pelo agente de Filtragem de Anexos, execute o seguinte comando:

```powershell
Get-AttachmentFilterEntry | Format-Table
```

Para exibir uma entrada de tipo de conteúdo MIME específica, use a sintaxe a seguir:

```powershell
Get-AttachmentFilteringEntry ContentType:<MIMEContentType>
```

Por exemplo, para exibir a entrada de tipo de conteúdo para imagens JPEG, execute o seguinte comando:

```powershell
Get-AttachmentFilteringEntry ContentType:image/jpeg
```

Para exibir uma entrada de nome de arquivo ou de extensão de nome de arquivo específica, use a sintaxe a seguir:

```powershell
Get-AttachmentFilteringEntry FileName:<FileName or FileNameExtension>
```

Por exemplo, para exibir a entrada de extensão de nome de arquivo para anexos JPEG, execute este comando:

    Get-AttachmentFilteringEntry FileName:*.jpg

## Usar o Shell para adicionar entradas de filtragem de anexos

Para adicionar uma entrada de filtragem de anexos que filtre anexos por tipo de conteúdo MIME, use a seguinte sintaxe:

```powershell
Add-AttachmentFilterEntry -Name <MIMEContentType> -Type ContentType
```

O exemplo a seguir adiciona uma entrada de tipo de conteúdo MIME para filtrar imagens JPEG.

```powershell
Add-AttachmentFilterEntry -Name image/jpeg -Type ContentType
```

Para adicionar uma entrada de filtragem de anexos que filtre anexos por nome de arquivo ou por extensão de nome de arquivo, use a seguinte sintaxe:

```powershell
Add-AttachmentFilterEntry -Name <FileName or FileNameExtension> -Type FileName
```

O exemplo a seguir filtra anexos com a extensão de nome de arquivo .jpg.

    Add-AttachmentFilterEntry -Name *.jpg -Type FileName

## Como saber se funcionou?

Para verificar se você adicionou com êxito uma entrada de filtragem de anexo, faça o seguinte:

1.  Execute o seguinte comando para verificar se a entrada de filtragem existe.
    
    ```powershell
Get-AttachmentFilterEntry | Format-Table
```

2.  Envie uma mensagem de teste que contenha um anexo proibido de uma caixa de correio externa para um destinatário interno e verifique se a mensagem foi rejeitada, removida ou excluída.

## Usar o Shell para remover entradas de filtragem de anexos

Para remover uma entrada de filtragem de anexos para filtrar anexos por tipo de conteúdo MIME, use a seguinte sintaxe:

```powershell
Remove-AttachmentFilterEntry ContentType:<ContentType>
```

O exemplo a seguir remove uma entrada de tipo de conteúdo MIME para imagens JPEG.

```powershell
Remove-AttachmentFilterEntry ContentType:image/jpeg
```

Para remover uma entrada de filtragem de anexos para filtrar anexos por nome de arquivo ou por extensão de nome de arquivo, use a seguinte sintaxe:

```powershell
Remove-AttachmentFilterEntry FileName:<FileName or FileNameExtension>
```

O exemplo a seguir remove a entrada de nome de arquivo da extensão de nome de arquivo .jpg.

    Remove-AttachmentFilterEntry FileName:*.jpg

## Como saber se funcionou?

Para verificar se você removeu com êxito uma entrada de filtragem de anexo, faça o seguinte:

1.  Execute o seguinte comando para verificar se a entrada de filtragem foi removida.
    
    ```powershell
Get-AttachmentFilterEntry | Format-Table
```

2.  Envie uma mensagem de teste que contenha um anexo permitido de uma caixa de correio externa para um destinatário interno e verifique se a mensagem foi entregue com êxito com o anexo.

## Usar o Shell para exibir a ação de filtragem de anexos

Para exibir a ação de filtragem de anexo usada quando um anexo proibido for detectado em uma mensagem, execute este comando:

```powershell
Get-AttachmentFilterListConfig
```

## Usar o Shell para configurar a ação de filtragem de anexos

Para configurar a ação de filtragem de anexo usada quando um anexo proibido for detectado em uma mensagem, execute este comando:

    Set-AttachmentFilterListConfig [-Action <Reject | Strip | SilentDelete>] [-RejectResponse "<Message text>"] [-AdminMessage "<Replacement file text>"] [-ExceptionConnectors <ConnectorGUID>]

Este exemplo faz as seguintes alterações na configuração da filtragem de anexos:

  - Rejeitar (bloquear) mensagens com anexos proibidos.

  - Usar uma resposta personalizada para mensagens rejeitadas.

<!-- end list -->

    Set-AttachmentFilterListConfig -Action Reject -RejectResponse "This message contains a prohibited attachment. Your message can't be delivered. Please resend the message without the attachment."

Para obter mais informações, consulte [Set-AttachmentFilterListConfig](https://technet.microsoft.com/pt-br/library/bb123483\(v=exchg.150\)).

## Como saber se funcionou?

Para verificar se você configurou com êxito a ação de filtragem de anexos, envie uma mensagem de teste que contenha um anexo proibido de uma caixa de correio externa para um destinatário interno e verifique se a mensagem e o anexo são processados como esperado.

