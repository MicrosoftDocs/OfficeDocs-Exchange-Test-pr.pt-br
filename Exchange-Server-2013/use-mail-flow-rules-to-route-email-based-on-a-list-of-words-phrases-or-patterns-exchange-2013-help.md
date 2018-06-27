---
title: 'Usar regras de fluxo de email com base em uma lista de palavras, frases ou padrões de emails de rota: Exchange 2013 Help'
TOCTitle: Usar regras de fluxo de email com base em uma lista de palavras, frases ou padrões de emails de rota
ms:assetid: 4c5bee1b-58b5-4152-baef-86fa103050ae
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Dn951131(v=EXCHG.150)
ms:contentKeyID: 65210899
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Usar regras de fluxo de email com base em uma lista de palavras, frases ou padrões de emails de rota

 

_**Aplica-se a:**Exchange Online, Exchange Online Protection, Exchange Server 2013_

_**Tópico modificado em:**2017-10-30_

Para ajudar seus usuários a cumprir as políticas de email da sua organização, você pode usar as regras de transporte de Exchange para determinar como e-mail contendo palavras específicas ou padrões é encaminhada. Para uma pequena lista de palavras ou frases, você pode usar o Centro de administração do Exchange. Para obter uma lista mais tempo, convém usar o Exchange módulo para Windows PowerShell para ler a lista de um arquivo de texto.

  - O exemplo 1: Usar uma pequena lista de palavras inaceitáveis

  - Exemplo 2: Usar uma longa lista de palavras inaceitáveis

Se sua organização usa Data Loss Prevention (DLP), consulte [Prevenção de perda de dados](technical-overview-of-dlp-data-loss-prevention-in-exchange.md) para obter outras opções para identificar e roteamento de email que contém informações confidenciais.

## O exemplo 1: Usar uma pequena lista de palavras inaceitáveis

Se sua lista de palavras ou frases for curta, você pode criar uma regra usando o Centro de administração do Exchange. Por exemplo, se você quiser certificar-se de que ninguém envia email com palavras incorretas ou com erros de ortografia do seu nome de empresa, acrônimos internos ou nomes de produto, você pode criar uma regra para bloquear a mensagem e informar ao remetente. Observe que padrões, frases e palavras não diferenciam maiusculas de minúsculas.

Este exemplo bloqueia as mensagens com erros ortográficos comuns.

![Regra mostrando o bloqueio de uma mensagem com base em padrões de texto](images/Dn951131.a8489cbb-be59-4890-ae30-1431703eeb88(EXCHG.150).png "Regra mostrando o bloqueio de uma mensagem com base em padrões de texto")

## Exemplo 2: Usar uma longa lista de palavras inaceitáveis

Se sua lista de palavras, frases ou padrões for longa, você pode colocá-los em um arquivo de texto com cada palavra, frase ou padrão em sua própria linha. Use o Exchange módulo para Windows PowerShell para ler na lista de palavras-chave em uma variável, criar uma regra de transporte e atribua a variável com as palavras-chave para a condição de regra de transporte. Por exemplo, o script a seguir usa uma lista de erros de ortografia de um arquivo chamado misspelled\_companyname.txt.

    $keywords=Import-Content  .\misspelled_companyname.txt
    New-TransportRule -Name "Block messages with unacceptable words" -SubjectOrBodyContainsWords $keywords -SentToScope "NotInOrganization" -RejectMessageReasonText "Do not use internal acronyms, product names, or misspellings in external communications."

## Usando padrões e frases no arquivo de texto

O arquivo de texto pode conter expressões regulares para padrões. Essas expressões não diferenciam maiúsculas de minúsculas. As expressões regulares comuns incluem:


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p><strong>Expressão</strong></p></td>
<td><p><strong>Correspondências</strong></p></td>
</tr>
<tr class="even">
<td><p><strong>.</strong></p></td>
<td><p>Qualquer caractere único</p></td>
</tr>
<tr class="odd">
<td><p><strong>*</strong></p></td>
<td><p>Todos os caracteres adicionais</p></td>
</tr>
<tr class="even">
<td><p><strong>\d</strong></p></td>
<td><p>Qualquer dígito decimal</p></td>
</tr>
<tr class="odd">
<td><p>[<em>grupo_de_caracteres</em>]</p></td>
<td><p>Qualquer caractere único em um <em>grupo_de_caracteres</em>.</p></td>
</tr>
</tbody>
</table>


Por exemplo, esse arquivo de texto contém erros de ortografia comuns de Microsoft.

    [mn]sft
    [mn]icrosft
    [mn]icro soft
    [mn].crosoft

Para saber como especificar os padrões de uso de expressões regulares, consulte [Referência de expressão Regular](https://go.microsoft.com/fwlink/p/?linkid=532394).

