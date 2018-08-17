---
title: 'Texto da mensagem DSN: Exchange 2013 Help'
TOCTitle: Texto da mensagem DSN
ms:assetid: eae4a050-5ecb-4c87-b377-74edb93a5995
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Bb125135(v=EXCHG.150)
ms:contentKeyID: 50486907
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Texto da mensagem DSN

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2015-03-09_

Você pode incluir texto em uma mensagem de notificação (DSN) de status de entrega personalizada no Microsoft Exchange Server 2013 e você pode formatar o texto em HTML.

Você pode incluir qualquer informação que você deseja exibir para o destinatário da mensagem DSN. Por exemplo, você pode incluir uma descrição detalhada do DSN, informações de contato para seu help desk e um link para o site da Web do seu departamento de suporte. Cada mensagem DSN pode conter um máximo de 512 caracteres.

Porque mensagens DSN podem ser exibidas em HTML, é possível incorporar a formatação do texto de DSN as marcas HTML. Por exemplo, se você quiser fazer parte do texto na sua mensagem DSN negrito, coloque o texto no \< B \> e marcas \< /B \> HTML. A tabela a seguir fornece alguns exemplos de marcas HTML válidas que podem ser usados no texto da mensagem DSN.

### Marcas HTML válidas para uso em mensagens DSN

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Marca HTML</th>
<th>Descrição</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>&lt; B &gt;</p></td>
<td><p>Negrito começar</p></td>
</tr>
<tr class="even">
<td><p>&lt; /B &gt;</p></td>
<td><p>End negrito</p></td>
</tr>
<tr class="odd">
<td><p>&lt; A HREF = &quot;url&quot; &gt;</p></td>
<td><p>Hiperlink de começar</p></td>
</tr>
<tr class="even">
<td><p>&lt; /a&gt; &gt;</p></td>
<td><p>Fim do hiperlink</p></td>
</tr>
<tr class="odd">
<td><p>&lt; BR &gt;</p></td>
<td><p>Quebra de link</p></td>
</tr>
<tr class="even">
<td><p>&lt; EM &gt;</p></td>
<td><p>Começar itálico</p></td>
</tr>
<tr class="odd">
<td><p>&lt; /EM &gt;</p></td>
<td><p>End itálico</p></td>
</tr>
<tr class="even">
<td><p>&lt; P &gt;</p></td>
<td><p>Início do parágrafo</p></td>
</tr>
<tr class="odd">
<td><p>&lt; /P &gt;</p></td>
<td><p>Final do parágrafo</p></td>
</tr>
</tbody>
</table>



> [!NOTE]
> Por padrão, o Exchange envia HTML DSN mensagens, mas você pode configurar se o Exchange envia mensagens DSN HTML para remetentes internos, remetentes externos ou ambos. Para definir esse comportamento, modifique o parâmetro <EM>InternalDsnSendHtml</EM> e <EM>ExternalDsnSendHtml</EM> com o comando <STRONG>Set-TransportService</STRONG> .<BR>Se o parâmetro <EM>InternalDsnSendHtml</EM> é definido como <CODE>$false</CODE>, Exchange suprime as marcas HTML em mensagens DSN enviadas para remetentes internos. Se o parâmetro <EM>ExternalDsnSendHtml</EM> é definido como <CODE>$false</CODE>, Exchange suprime as marcas HTML em mensagens DSN enviadas para remetentes externos.



Os seguintes caracteres que o Exchange usa no texto da mensagem DSN têm significado especial:

  - Sinal maior que (\>)

  - Menor que (\<) de entrada

  - E comercial (&)

  - Aspas (")

Esses caracteres são usados para determinar onde as marcas HTML começam e terminam e onde o texto que deve ser exibido para os remetentes é iniciado e interrompido. Se você deseja exibir esses caracteres em suas mensagens DSN, você deve usar os códigos de escape na tabela a seguir.

Por exemplo, se você deseja exibir a mensagem `"Please contact the Help Desk at <1234>."`, você deve adicionar `"Please contact the Help Desk at &lt;1234&gt;." `para o texto da mensagem DSN.

### Códigos de escape de caractere de mensagem DSN

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Código de escape</th>
<th>Caractere</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>&amp; lt;</p></td>
<td><p>&lt;</p></td>
</tr>
<tr class="even">
<td><p>&amp; gt;</p></td>
<td><p>&gt;</p></td>
</tr>
<tr class="odd">
<td><p>&amp; quot;</p></td>
<td><p>&quot;</p></td>
</tr>
<tr class="even">
<td><p>&amp; amp;</p></td>
<td><p>&amp;</p></td>
</tr>
</tbody>
</table>



> [!IMPORTANT]
> Se você incluir uma marca HTML no texto da sua mensagem DSN que contém as aspas ("), como <CODE>&lt;A HREF="url"&gt;</CODE>, você deve usar aspas simples (') ao redor do texto da mensagem DSN inteiro. Você receberá uma mensagem de erro se você usar aspas duplas ao redor do texto da mensagem DSN todo e ao redor de uma marca HTML.


