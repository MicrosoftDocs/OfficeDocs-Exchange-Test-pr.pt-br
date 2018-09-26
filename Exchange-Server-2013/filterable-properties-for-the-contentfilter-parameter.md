---
title: 'Propriedades filtráveis para o parâmetro - ContentFilter: Exchange 2013 Help'
TOCTitle: Propriedades filtráveis para o parâmetro - ContentFilter
ms:assetid: cf504a59-1938-489c-bb48-b27b2ac3234e
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Ff601762(v=EXCHG.150)
ms:contentKeyID: 50556291
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Propriedades filtráveis para o parâmetro - ContentFilter

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2015-09-10_

Este tópico lista as propriedades filtráveis do parâmetro *ContentFilter*. O parâmetro *ContentFilter* é usado para exportar mensagens para um arquivo .pst que combine com o filtro. O parâmetro *ContentFilter* é usado no cmdlet [New-MailboxExportRequest](https://technet.microsoft.com/pt-br/library/ff607299\(v=exchg.150\)).

## Propriedades filtráveis

Várias propriedades do parâmetro *ContentFilter* aceitam caracteres curinga. Se você usar um caractere curinga, utilize o operador **-like** em vez do operador **-eq**. O operador **-like** é usado para localizar correspondências de padrão de tipos avançados, como uma cadeia de caracteres, enquanto o operador **-eq** é usado para localizar uma correspondência exata.

A tabela a seguir contém uma lista das propriedades filtráveis do parâmetro *ContentFilter*. Esta tabela lista o nome da propriedade, uma descrição, os valores aceitáveis e um exemplo de sintaxe. Para mais informações sobre filtros OPATH, consulte [Filtros de destinatários comandos do Shell](https://technet.microsoft.com/pt-br/library/bb124268\(v=exchg.150\)).


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Property</th>
<th>Descrição</th>
<th>Valores</th>
<th>Exemplo de sintaxe</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Tudo</p></td>
<td><p>Essa propriedade retorna todas as mensagens que tenham uma cadeia de caracteres em particular, em todas as propriedades indexadas. Por exemplo, use essa propriedade se você quiser exportar todas as mensagens que tenham "Ayla" como destinatário, remetente ou em que esse nome apareça no corpo da mensagem.</p></td>
<td><p>Cadeia de caracteres</p>
<p>Curinga</p></td>
<td>

```powershell
-ContentFilter {All -like '*Ayla*'}
```
</td>
</tr>
<tr class="even">
<td><p>Anexo</p></td>
<td><p>Essa propriedade retorna mensagens que tenham a cadeia de caracteres especificada no conteúdo de um anexo ou no nome de arquivo do anexo.</p></td>
<td><p>Cadeia de caracteres</p>
<p>Curinga</p></td>
<td>

```powershell
-ContentFilter {Attachment -like '*.jpg'}
```
</td>
</tr>
<tr class="odd">
<td><p>BCC</p></td>
<td><p>Essa propriedade retorna as mensagens enviadas que tenham o destinatário especificado no campo Cco.</p></td>
<td><p>Nome para exibição</p>
<p>Alias</p>
<p>Endereço SMTP</p>
<p>LegacyDN</p>
<p>Curinga</p></td>
<td>

```powershell
-ContentFilter {(BCC -eq 'ayla@contoso.com') -or (BCC -eq 'tony@contoso.com')}
```
</td>
</tr>
<tr class="even">
<td><p>Body</p></td>
<td><p>Essa propriedade retorna as mensagens que tenham a cadeia de caracteres especificada dentro do corpo da mensagem.</p></td>
<td><p>Cadeia de caracteres</p>
<p>Curinga</p></td>
<td>

```powershell
-ContentFilter {Body -like '*prospectus*'}
```
</td>
</tr>
<tr class="odd">
<td><p>Category</p></td>
<td><p>Essa propriedade retorna mensagens quem tenham uma categoria correspondente. As categorias são definidas pelos usuários ou pelas regras da Caixa de Entrada.</p></td>
<td><p>Cadeia de caracteres</p>
<p>Curinga</p></td>
<td>

```powershell
-ContentFilter {Category -like '*Blue*'}
```
</td>
</tr>
<tr class="even">
<td><p>CC</p></td>
<td><p>Essa propriedade retorna as mensagens enviadas que tenham o destinatário especificado no campo Cc.</p></td>
<td><p>Nome para exibição</p>
<p>Alias</p>
<p>Endereço SMTP</p>
<p>LegacyDN</p>
<p>Curinga</p></td>
<td>

```powershell
-ContentFilter {(CC -eq 'ayla@contoso.com') -or (CC -eq 'tony@contoso.com')}
```
</td>
</tr>
<tr class="odd">
<td><p>Expires</p></td>
<td><p>Essa propriedade retorna as mensagens com um carimbo de data de validade especificada.</p></td>
<td><p>Carimbo de data e hora</p></td>
<td>

```powershell
-ContentFilter {Expires -lt '01/01/2013'}
```
</td>
</tr>
<tr class="even">
<td><p>HasAttachment</p></td>
<td><p>Essa propriedade retorna mensagens com ou sem anexos.</p></td>
<td><p>Booleano</p>
<p><code>$true</code> ou  <code>$false</code></p></td>
<td>

```powershell
-ContentFilter {HasAttachment -eq $true}
```
</td>
</tr>
<tr class="odd">
<td><p>Importance</p></td>
<td><p>Essa propriedade retorna mensagens quem tenham um nível de prioridade especificado.</p></td>
<td><p>0 ou "Low" (baixo)</p>
<p>1 ou "Normal"</p>
<p>2 ou "High" (alto)</p></td>
<td>

```powershell
-ContentFilter {Importance -eq 'high'}</code></pre>
<pre><code>-ContentFilter {Importance -eq 2}
```
</td>
</tr>
<tr class="even">
<td><p>IsFlagged</p></td>
<td><p>Essa propriedade retorna mensagens que foram sinalizadas pelo usuário ou pela regra da Caixa de Entrada.</p></td>
<td><p>Booleano</p>
<p><code>$true</code> ou <code>$false</code></p></td>
<td>

```powershell
-ContentFilter {IsFlagged -eq $true}
```
</td>
</tr>
<tr class="odd">
<td><p>IsRead</p></td>
<td><p>Essa propriedade retorna mensagens que já foram lidas ou ainda não foram lidas pelo usuário.</p></td>
<td><p>Booleano</p>
<p><code>$true</code> ou <code>$false</code></p></td>
<td>

```powershell
-ContentFilter {IsRead -eq $true}
```
</td>
</tr>
<tr class="even">
<td><p>MessageKind</p></td>
<td><p>Essa propriedade retorna as mensagens que são do tipo especificado.</p></td>
<td><p>Calendário</p>
<p>Contato</p>
<p>Documento</p>
<p>Email</p>
<p>Fax</p>
<p>Mensagem Instantânea</p>
<p>Journal</p>
<p>Observação</p>
<p>Postagem</p>
<p>Feed RSS</p>
<p>Tarefa</p>
<p>Voicemail</p></td>
<td>

```powershell
-ContentFilter {MessageKind -eq 'Calendar'}</code></pre>
<pre><code>-ContentFilter {MessageKind -ne 'Email'}
```
</td>
</tr>
<tr class="odd">
<td><p>MessageLocalee</p></td>
<td><p>Essa propriedade retorna as mensagens que são da localidade especificada.</p></td>
<td><p>CultureInfo</p></td>
<td>

```powershell
-ContentFilter {MessageLocale -ne 'en-US'}</code></pre>
<pre><code>-ContentFilter {MessageLocale -eq 'tr-TR'}
```
</td>
</tr>
<tr class="even">
<td><p>Participants</p></td>
<td><p>Essa propriedade retorna as mensagens enviadas que tenham o destinatário especificado nos campos Para, Cco ou Cc.</p></td>
<td><p>Nome para exibição</p>
<p>Alias</p>
<p>Endereço SMTP</p>
<p>LegacyDN</p>
<p>Curinga</p></td>
<td>

```powershell
-ContentFilter {(Participants -eq 'ayla@contoso.com') -or (Participants -eq 'tony@contoso.com')}
```
</td>
</tr>
<tr class="odd">
<td><p>PolicyTag</p></td>
<td><p>Essa propriedade retorna mensagens quem tenham uma marca de diretiva. O repositório do Exchange mantém as marcas de diretivas como GUIDs. Assim, a cadeia de caracteres pode conter um valor de GUID explícito, que é pesquisado pela cadeia de caracteres PR_POLICY_TAG ou por um curinga.</p>
<p>Se o valor fornecido não for um GUID, o comando usa as informações do Active Directory para resolver os nomes para GUIDs.</p></td>
<td><p>Cadeia de caracteres</p>
<p>Curinga</p></td>
<td>

```powershell
-ContentFilter {PolicyTag -ne '00000000-0000-0000-0000-000000000000'}
```
</td>
</tr>
<tr class="even">
<td><p>Received</p></td>
<td><p>Essa propriedade retorna mensagens que são recebidas com o carimbo de data/hora Recebido.</p></td>
<td><p>Carimbo de data e hora</p></td>
<td>

```powershell
-ContentFilter {Received -lt '01/01/2013 9:00'}</code></pre>
<pre><code>-ContentFilter {(Received -lt '01/01/2013') -and (Received -gt '01/01/2012')}
```
</td>
</tr>
<tr class="odd">
<td><p>Sender</p></td>
<td><p>Essa propriedade retorna mensagens que foram recebidas do remetente especificado.</p></td>
<td><p>Nome para exibição</p>
<p>Alias</p>
<p>Endereço SMTP</p>
<p>LegacyDN</p>
<p>Curinga</p></td>
<td>

```powershell
ContentFilter {Sender -eq 'tony'}
```
</td>
</tr>
<tr class="even">
<td><p>Sent</p></td>
<td><p>Essa propriedade retorna mensagens que são enviadas com o carimbo de data/hora Enviado.</p></td>
<td><p>Carimbo de data e hora</p></td>
<td>

```powershell
-ContentFilter {Sent -lt '01/01/2013 9:00'}</code></pre>
<pre><code>-ContentFilter {(Sent -lt '01/01/2013') -and (Sent -gt '01/01/2012')}
```
</td>
</tr>
<tr class="odd">
<td><p>Size</p></td>
<td><p>Essa propriedade retorna as mensagens que são do tamanho especificado.</p></td>
<td><p>B (bytes)</p>
<p>KB (quilobytes)</p>
<p>MB (megabytes)</p></td>
<td>

```powershell
-ContentFilter {Size -gt '10KB'}
```
</td>
</tr>
<tr class="even">
<td><p>Subject</p></td>
<td><p>Essa propriedade retorna as mensagens que tenham a cadeia de caracteres especificada dentro do assunto da mensagem.</p></td>
<td><p>Cadeia de caracteres</p>
<p>Curinga</p></td>
<td>

```powershell
-ContentFilter {Subject -like '*meeting*'}
```
</td>
</tr>
<tr class="odd">
<td><p>To</p></td>
<td><p>Essa propriedade retorna as mensagens enviadas que tenham o destinatário especificado no campo Para.</p></td>
<td><p>Nome para exibição</p>
<p>Alias</p>
<p>Endereço SMTP</p>
<p>LegacyDN</p>
<p>Curinga</p></td>
<td>

```powershell
-ContentFilter {To -eq 'aylakol'}
```
</td>
</tr>
</tbody>
</table>