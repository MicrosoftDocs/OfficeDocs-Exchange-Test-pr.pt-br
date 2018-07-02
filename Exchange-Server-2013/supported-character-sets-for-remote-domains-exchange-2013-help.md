---
title: 'Conjuntos de caracteres suportados para domínios remotos: Exchange 2013 Help'
TOCTitle: Conjuntos de caracteres suportados para domínios remotos
ms:assetid: 66023a62-1fd3-4019-be2b-4e7147db148a
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Aa998600(v=EXCHG.150)
ms:contentKeyID: 52058427
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Conjuntos de caracteres suportados para domínios remotos

 

_**Aplica-se a:** Exchange Online, Exchange Server 2013_

_**Tópico modificado em:** 2015-03-09_

Os conjuntos de caracteres a seguir podem ser especificados para mensagens enviadas para domínios remotos.

  - No Exchange admin center (EAC), na página Configurações do **domínio remoto**, selecione o nome nas listas suspensas **do conjunto de caracteres MIME** e **conjunto de caracteres não MIME**.

  - No Shell, use o valor na coluna nome na tabela a seguir para o parâmetro *CharacterSet* ou *NonMimeCharacterSet* no cmdlet [Set-RemoteDomain](https://technet.microsoft.com/pt-br/library/aa997857\(v=exchg.150\)) .

### Conjuntos de caracteres com suporte para configuração de domínio remoto

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Nome</th>
<th>Descrição</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>big5</p></td>
<td><p>Chinês tradicional (Big5)</p></td>
</tr>
<tr class="even">
<td><p>DIN_66003</p></td>
<td><p>Alemão (IA5)</p></td>
</tr>
<tr class="odd">
<td><p>euc-jp</p></td>
<td><p>Japonês (EUC)</p></td>
</tr>
<tr class="even">
<td><p>euc-kr</p></td>
<td><p>Coreano (EUC)</p></td>
</tr>
<tr class="odd">
<td><p>GB18030</p></td>
<td><p>Chinês simplificado (GB18030)</p></td>
</tr>
<tr class="even">
<td><p>gb2312</p></td>
<td><p>Chinês simplificado (GB2312)</p></td>
</tr>
<tr class="odd">
<td><p>hz-gb-2312</p></td>
<td><p>Chinês simplificado (HZ)</p></td>
</tr>
<tr class="even">
<td><p>iso-2022-jp</p></td>
<td><p>Japonês (JIS)</p></td>
</tr>
<tr class="odd">
<td><p>iso-2022-kr</p></td>
<td><p>Coreano (ISO)</p></td>
</tr>
<tr class="even">
<td><p>iso-8859-1</p></td>
<td><p>Europeu Ocidental (ISO)</p></td>
</tr>
<tr class="odd">
<td><p>iso-8859-2</p></td>
<td><p>Europeu Central (ISO)</p></td>
</tr>
<tr class="even">
<td><p>iso-8859-3</p></td>
<td><p>Latim 3 (ISO)</p></td>
</tr>
<tr class="odd">
<td><p>iso-8859-4</p></td>
<td><p>Báltico (ISO)</p></td>
</tr>
<tr class="even">
<td><p>iso-8859-5</p></td>
<td><p>Cirílico (ISO)</p></td>
</tr>
<tr class="odd">
<td><p>iso-8859-6</p></td>
<td><p>Árabe (ISO)</p></td>
</tr>
<tr class="even">
<td><p>iso-8859-7</p></td>
<td><p>Grego (ISO)</p></td>
</tr>
<tr class="odd">
<td><p>iso-8859-8</p></td>
<td><p>Hebraico (ISO)</p></td>
</tr>
<tr class="even">
<td><p>iso-8859-9</p></td>
<td><p>Turco (ISO)</p></td>
</tr>
<tr class="odd">
<td><p>iso-8859-13</p></td>
<td><p>Estoniano (ISO)</p></td>
</tr>
<tr class="even">
<td><p>iso-8859-15</p></td>
<td><p>Latim 9 (ISO)</p></td>
</tr>
<tr class="odd">
<td><p>koi8-r</p></td>
<td><p>Cirílico (KOI8-R)</p></td>
</tr>
<tr class="even">
<td><p>koi8-u</p></td>
<td><p>Cirílico (KOI8-U)</p></td>
</tr>
<tr class="odd">
<td><p>ks_c_5601-1987</p></td>
<td><p>Coreano (Windows)</p></td>
</tr>
<tr class="even">
<td><p>NS_4551-1</p></td>
<td><p>Norueguês (IA5)</p></td>
</tr>
<tr class="odd">
<td><p>SEN_850200_B</p></td>
<td><p>Sueco (IA5)</p></td>
</tr>
<tr class="even">
<td><p>shift_jis</p></td>
<td><p>Japonês (Shift-JIS)</p></td>
</tr>
<tr class="odd">
<td><p>utf-8</p></td>
<td><p>Unicode (UTF-8)</p></td>
</tr>
<tr class="even">
<td><p>windows-1250</p></td>
<td><p>Europeu Central (Windows)</p></td>
</tr>
<tr class="odd">
<td><p>windows-1251</p></td>
<td><p>Cirílico (Windows)</p></td>
</tr>
<tr class="even">
<td><p>windows-1252</p></td>
<td><p>Europeu Ocidental (Windows)</p></td>
</tr>
<tr class="odd">
<td><p>windows-1253</p></td>
<td><p>Grego (Windows)</p></td>
</tr>
<tr class="even">
<td><p>windows-1254</p></td>
<td><p>Turco (Windows)</p></td>
</tr>
<tr class="odd">
<td><p>windows-1255</p></td>
<td><p>Hebraico (Windows)</p></td>
</tr>
<tr class="even">
<td><p>windows-1256</p></td>
<td><p>Árabe (Windows)</p></td>
</tr>
<tr class="odd">
<td><p>windows-1257</p></td>
<td><p>Báltico (Windows)</p></td>
</tr>
<tr class="even">
<td><p>windows-1258</p></td>
<td><p>Vietnamita (Windows)</p></td>
</tr>
<tr class="odd">
<td><p>windows-874</p></td>
<td><p>Tailandês (Windows)</p></td>
</tr>
</tbody>
</table>

