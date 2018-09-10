---
title: 'Formatos de arquivo indexados pela pesquisa do Exchange: Exchange 2013 Help'
TOCTitle: Formatos de arquivo indexados pela pesquisa do Exchange
ms:assetid: e5110ac1-28e1-4554-acc3-85d08c997bc5
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Ee633485(v=EXCHG.150)
ms:contentKeyID: 52058883
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Formatos de arquivo indexados pela pesquisa do Exchange

 

_**Aplica-se a:** Exchange Online, Exchange Server 2013_

_**Tópico modificado em:** 2015-07-21_

No MicrosoftExchange Server 2013 e no Exchange Online, a Pesquisa do Exchange inclui filtros para indexar os tipos mais comuns de formatos de arquivo usados como anexos em mensagens. Você também pode instalar filtros para indexar tipos de arquivo adicionais.


> [!NOTE]
> No Exchange 2013, não é obrigatório instalar e registrar o Microsoft Office Filter Pack.<BR>Por padrão, o tamanho máximo de arquivo que pode ser indexado pela Exchange Server 2013 local é de 32 MB. Para aumentar esse limite de tamanho, você deve adicionar a seguinte chave do registro em todas as autoridades de certificação e servidores de várias funções em sua organização:<BR><CODE>@"SOFTWARE\Microsoft\ExchangeServer\V15\Search\SystemParameters" DWORD: "MaxAttachmentSize"</CODE>



Ao gerenciar ou usar a Pesquisa do Exchange e os recursos dependentes (como [Descoberta Eletrônica In-loco](https://docs.microsoft.com/pt-br/exchange/security-and-compliance/in-place-ediscovery/in-place-ediscovery)), considere as diferenças entre itens que não podem ser pesquisados e formatos de arquivo que estão desativados para indexação ou que contêm conteúdo que não pode ser indexado:

  - **Itens não pesquisáveis**   Quando a Pesquisa do Exchange não conseguir indexar um tipo de arquivo específico por qualquer razão (por exemplo, se um filtro não está instalado), a pesquisa para o tipo de arquivo falha. Mensagens que contêm anexos desse tipo são marcadas como *parcialmente indexadas*. Os itens que não podem ser pesquisados podem ser recuperados usando o cmdlet [Get-FailedContentIndexDocuments](https://technet.microsoft.com/pt-br/library/dd351154\(v=exchg.150\)). Ao copiar resultados de pesquisa eDiscovery In-Loco para uma caixa de correio de descoberta ou ao exportar resultados de pesquisa para um arquivo PST, você pode incluir itens não pesquisáveis. Para obter mais informações, consulte [Itens não pesquisáveis na descoberta eletrônica do Exchange](unsearchable-items-in-exchange-ediscovery-exchange-2013-help.md).

  - **Formatos de arquivo com conteúdo que não pode ser indexado**   Determinados tipos de arquivo, como o Windows Media Video (WMV), não contêm conteúdo que pode ser indexado e, portanto, não são indexados. As mensagens contendo anexos desses tipos de arquivo também são retornadas como itens não pesquisáveis, nas pesquisas eDiscovery In-Loco.

  - **Formatos de arquivo desativados** Em organizações locais, um administrador pode desativar a indexação de um formato específico de arquivo. As mensagens contendo um anexo com formato desabilitado são retornadas como itens não pesquisáveis.


> [!IMPORTANT]
> Embora um anexo de mensagem possa ser não pesquisável ou estar em um formato de arquivo não indexável, o assunto, o corpo e outros metadados da mensagem podem ser indexados para que a mensagem possa ser retornada em pesquisas.



Para conhecer tarefas de gerenciamento adicionais relacionadas à Pesquisa do Exchange em organizações locais, consulte [Procedimentos de pesquisa do Exchange](exchange-search-procedures-exchange-2013-help.md).

## Filtros padrão

A tabela a seguir lista os filtros de pesquisa padrão instalados em um servidor de Caixa de Correio do Exchange 2013 e no Exchange Online. Você pode ver a lista de filtros padrão usando o cmdlet [Get-SearchDocumentFormat](https://technet.microsoft.com/pt-br/library/jj873755\(v=exchg.150\)).


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Filtrar</th>
<th>Extensão de arquivo</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Mensagem de email</p></td>
<td><p>.eml</p></td>
</tr>
<tr class="even">
<td><p>Graphics Interchange Format</p></td>
<td><p>.gif</p></td>
</tr>
<tr class="odd">
<td><p>JPEG</p></td>
<td><p>.jpeg</p></td>
</tr>
<tr class="even">
<td><p>Microsoft Excel</p></td>
<td><p>.xls, .xlt, .xlsx, .xlsm, .xlb, .xlc, .xlsb</p></td>
</tr>
<tr class="odd">
<td><p>Arquivo do Excel</p></td>
<td><p>odbcexcel</p></td>
</tr>
<tr class="even">
<td><p>Microsoft InfoPath</p></td>
<td><p>.infopathml</p></td>
</tr>
<tr class="odd">
<td><p>Microsoft Office Binder</p></td>
<td><p>.obt, obd</p></td>
</tr>
<tr class="even">
<td><p>Microsoft PowerPoint</p></td>
<td><p>.pptx, .pptm, .ppt, .ppsx, .ppsm, .pps, .ppam, .potm, .pot, .potx</p></td>
</tr>
<tr class="odd">
<td><p>Microsoft Publisher</p></td>
<td><p>.pub</p></td>
</tr>
<tr class="even">
<td><p>Microsoft Word</p></td>
<td><p>.doc, .docm, .dotx, .dotm, .dot, .docx</p></td>
</tr>
<tr class="odd">
<td><p>Microsoft XML Paper Specification</p></td>
<td><p>.xps</p></td>
</tr>
<tr class="even">
<td><p>OneNote</p></td>
<td><p>.one</p></td>
</tr>
<tr class="odd">
<td><p>OpenDocument Presentation</p></td>
<td><p>.odp</p></td>
</tr>
<tr class="even">
<td><p>OpenDocument Spreadsheet</p></td>
<td><p>.ods</p></td>
</tr>
<tr class="odd">
<td><p>OpenDocument Text</p></td>
<td><p>.odt</p></td>
</tr>
<tr class="even">
<td><p>Item do Outlook</p></td>
<td><p>.msg</p></td>
</tr>
<tr class="odd">
<td><p>Portable Document Format</p></td>
<td><p>.pdf</p></td>
</tr>
<tr class="even">
<td><p>Rich Text</p></td>
<td><p>.rtf</p></td>
</tr>
<tr class="odd">
<td><p>Texto</p></td>
<td><p>.txt</p></td>
</tr>
<tr class="even">
<td><p>vCalendar</p></td>
<td><p>.vcs</p></td>
</tr>
<tr class="odd">
<td><p>vCard</p></td>
<td><p>.vcf</p></td>
</tr>
<tr class="even">
<td><p>Visio</p></td>
<td><p>.vdw, .vsd, .vss, .vst, .vsx, .vtx, .vssx, .vssm, .vsdm, .vstx, .vstm, .vdx</p></td>
</tr>
<tr class="odd">
<td><p>Arquivo da Web</p></td>
<td><p>.mhtml</p></td>
</tr>
<tr class="even">
<td><p>Página da Web</p></td>
<td><p>.html</p></td>
</tr>
<tr class="odd">
<td><p>Documento XML</p></td>
<td><p>.xml</p></td>
</tr>
<tr class="even">
<td><p>Arquivo ZIP</p></td>
<td><p>.zip</p></td>
</tr>
</tbody>
</table>


## Formatos de arquivo desabilitados

A tabela a seguir lista os filtros de pesquisa que, por padrão, estão desabilitados para indexação em um servidor de caixas de correio do Exchange 2013 e no Exchange Online. No Exchange 2013, os administradores podem desabilitar ou reabilitar um formato de arquivo compatível para indexação usando o cmdlet [Set-SearchDocumentFormat](https://technet.microsoft.com/pt-br/library/jj873756\(v=exchg.150\)). Esse cmdlet não está disponível no Exchange Online.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Filtro</th>
<th>Extensão de arquivo</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>AVI</p></td>
<td><p>.avi</p></td>
</tr>
<tr class="even">
<td><p>Bitmap</p></td>
<td><p>.bmp</p></td>
</tr>
<tr class="odd">
<td><p>MP3</p></td>
<td><p>.mp3</p></td>
</tr>
<tr class="even">
<td><p>MPEG</p></td>
<td><p>.mpeg</p></td>
</tr>
<tr class="odd">
<td><p>PNG</p></td>
<td><p>.png</p></td>
</tr>
<tr class="even">
<td><p>Microsoft Windows Wave Audio</p></td>
<td><p>.wav</p></td>
</tr>
</tbody>
</table>

