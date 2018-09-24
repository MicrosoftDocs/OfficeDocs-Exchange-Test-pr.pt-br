---
title: 'Logs de rastreamento de mensagens de pesquisa: Exchange 2013 Help'
TOCTitle: Logs de rastreamento de mensagens de pesquisa
ms:assetid: e1678327-bcd5-42d4-a363-67f33067fe9a
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Bb124926(v=EXCHG.150)
ms:contentKeyID: 51407924
ms.date: 01/10/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Logs de rastreamento de mensagens de pesquisa

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2013-02-25_

No Microsoft Exchange Server 2013, o log de controle de mensagens é um registro detalhado de todas as atividades de mensagem à medida que as mensagens são transferidas de e para o serviço de Transporte em servidores de Caixa de Correio, caixas de correio em servidores de Caixa de Correio e servidores de Transporte de Borda.

Você pode usar o cmdlet **Get-MessageTrackingLog** no Shell de Gerenciamento do Exchange para procurar entradas no log de ​​controle de mensagens usando critérios de pesquisa específicos.

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: 30 minutos

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Acompanhamento de mensagens" no tópico [Permissões de fluxo de email](mail-flow-permissions-exchange-2013-help.md).

  - Pesquisar nos logs de controle de mensagens exige que o serviço Pesquisa de Log de Transporte do Microsoft Exchange esteja em execução. Se você desabilitar ou interromper esse serviço, não poderá pesquisar nos logs de controle de mensagens nem executar relatórios de entrega. No entanto, interromper este serviço não afeta outros recursos no Exchange.

  - Os nomes dos campos mostrados nos resultados do cmdlet **Get-MessageTrackingLog** são similares aos nomes de campos reais usados nos logs de acompanhamento de mensagens. As diferenças maiores são:
    
      - Os traços são removidos dos nomes de campo. Por exemplo, **internal-message-id** é exibido como `InternalMessageId`.
    
      - O campo **date-time** é exibido como `Timestamp`.
    
      - O campo **recipient-address** é exibido como `Recipients`.
    
      - O campo **sender-address** é exibido como `Sender`.

  - O campo **date-time** no log de controle de mensagens armazena informações no formato UTC (Tempo Universal Coordenado). Contudo, você deve inserir os critérios de pesquisa de data e hora para os parâmetros *Start* ou *End* no formato de data e hora regional do computador que você estiver usando para realizar a pesquisa.

  - Não é possível copiar os arquivos de controle de mensagens de um servidor do Exchange e depois pesquisá-los usando o cmdlet **Get-MessageTrackingLog**. Além disso, se você salvar manualmente um arquivo de log de controle de mensagens, a mudança no carimbo de data e hora do arquivo quebra a lógica de consulta que o Exchange usa para pesquisar os logs de controle de mensagens.

  - O cmdlet Exchange 2013**Get-MessageTrackingLog** consegue pesquisar os logs de controle de mensagens nos servidores do Exchange 2007 e do Exchange 2010 no mesmo site do Active Directory.

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>.



## O que você deseja fazer?

## Use o Shell para pesquisar os logs de controle de mensagens

Para procurar eventos específicos nas entradas do log de rastreamento de mensagens, use a seguinte sintaxe.

    Get-MessageTrackingLog [-Server <ServerIdentity.] [-ResultSize <Integer> | Unlimited] [-Start <DateTime>] [-End <DateTime>] [-EventId <EventId>] [-InternalMessageId <InternalMessageId>] [-MessageId <MessageId>] [-MessageSubject <Subject>] [-Recipients <RecipientAddress1,RecipientAddress2...>] [-Reference <Reference>] [-Sender <SenderAddress>]

Para exibir as 1000 entradas de log de controle de mensagens mais recentes no servidor, execute o seguinte comando:

```powershell
Get-MessageTrackingLog
```

Este exemplo pesquisa nos logs de controle de mensagens do servidor local todas as entradas de 28/3/2013 8h a 28/3/2013 17h de todos os eventos de **FAIL** nas quais o remetente da mensagem era davi@contoso.com.

    Get-MessageTrackingLog -ResultSize Unlimited -Start "3/28/2013 8:00AM" -End "3/28/2013 5:00PM" -EventId "Fail" -Sender "pat@contoso.com"

## Use o Shell para controlar a saída de uma pesquisa de log de controle de mensagens

Use a sintaxe a seguir:

    Get-MessageTrackingLog <SearchFilters> | <Format-Table | Format-List> [<FieldNames>] [<OutputFileOptions>]

Este exemplo pesquisa nos logs de controle de mensagens usando os seguintes critérios de pesquisa:

  - Retorna resultados para os primeiros 1.000 eventos de **Send**.

  - Exiba os resultados no formato de lista.

  - Exiba apenas os nomes de campo que começam com `Send` ou `Recipient`.

  - Grave a saída em um novo arquivo chamado `D:\Send Search.txt`

<!-- end list -->

    Get-MessageTrackingLog -EventId Send | Format-List Send*,Recipient* > "D:\Send Search.txt"

## Use o Shell para procurar nos logs de controle de mensagens entradas de mensagens em vários servidores

Normalmente, o valor no campo do cabeçalho **MessageID:**  permanece constante enquanto a mensagem é transmitida por toda a organização do Exchange. Essa propriedade é denominada **InternetMessageId** nos utilitários de visualização de filas e **MessageId** nos utilitários de visualização de log de controle de mensagens. Depois de ter determinado o valor `MessageID:` de uma mensagem específica, você pode procurar informações sobre essa mensagem nos logs de controle de mensagens em cada servidor de Caixa de Correio na organização do Exchange.

Para procurar todas as entradas de log de ​​controle de mensagens para uma mensagem específica em todos os servidores de Caixa de Correio, use a seguinte sintaxe.

    Get-ExchangeServer | where {$_.isHubTransportServer -eq $true -or $_.isMailboxServer -eq $true} | Get-MessageTrackingLog -MessageId <MessageID> | Select-Object <CommaSeparatedFieldNames> | Sort-Object -Property <FieldName>

Este exemplo pesquisa nos logs de controle de mensagens em todos os servidores de caixa de correio do Exchange 2013 usando os seguintes critérios de pesquisa:

  - Encontre todas as entradas relacionadas a uma mensagem que tem um valor de **MessageID:** `<ba18339e-8151-4ff3-aeea-87ccf5fc9796@mailbox01.contoso.com>`. Observe que você pode omitir os colchetes angulares (`<``>`). Se você não o fizer, será preciso colocar todo o valor **MessageID:**  entre aspas.

  - Para cada entrada, exiba os campos **date-time**, **server-hostname**, **client-hostname**, **source**, **event-id** e **recipient-address**.

  - Classifique os resultados pelo campo **date-time**.

<!-- end list -->

    Get-ExchangeServer | where {$_.isHubTransportServer -eq $true -or $_.isMailboxServer -eq $true} | Get-MessageTrackingLog -MessageId ba18339e-8151-4ff3-aeea-87ccf5fc9796@mailbox01.contoso.com | Select-Object Timestamp,ServerHostname,ClientHostname,Source,EventId,Recipients | Sort-Object -Property Timestamp

## Use o EAC para pesquisar os logs de controle de mensagens

Você pode usar os Relatórios de Entrega do recurso de administradores no Centro de Administração do Exchange (EAC) para procurar nos logs de controle de mensagens informações sobre as mensagens enviadas ou recebidas por uma caixa de correio específica em sua organização. Para saber mais, confira [Acompanhar mensagens com notificações de entrega](track-messages-with-delivery-reports-exchange-2013-help.md).

