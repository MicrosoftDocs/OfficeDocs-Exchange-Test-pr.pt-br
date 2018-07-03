---
title: 'Não há suporte para caracteres para nomes de objeto do Exchange 2013: Exchange 2013 Help'
TOCTitle: Não há suporte para caracteres para nomes de objeto do Exchange 2013
ms:assetid: 76fa4e23-f0f6-473b-9227-70ded907578f
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Dn169553(v=EXCHG.150)
ms:contentKeyID: 54651976
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Não há suporte para caracteres para nomes de objeto do Exchange 2013

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2015-03-09_

Este artigo descreve os caracteres que não podem ser usados em nomes de objeto ou componente no Exchange 2013. Quando você cria nomes de objetos ou componentes no Exchange 2013, os nomes não podem conter caracteres não suportados, mesmo que você poderá criar um objeto usando um caractere sem suporte. Além disso, se você tentar importar ou conecte-se aos objetos cujos nomes contêm caracteres não suportados, você pode receber uma mensagem de erro ou enfrentar um comportamento inesperado.

## Caracteres sem suporte

A seguinte tabela lista caracteres que não são suportados para uso nos nomes de objetos ou componentes relacionados com o Exchange. A tabela também lista o cenário em que os problemas podem ocorrer se forem utilizados caracteres não suportados. Note que existe um máximo de comprimento de 64 caracteres para cada objeto listado na tabela.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Objeto ou componente do Exchange</th>
<th>Cenário do Exchange</th>
<th>Caracteres sem suporte</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Nome de domínio do email</p></td>
<td><p>Conector do protocolo SMTP</p></td>
<td><p><code>~ ` ! @ # $ % ^ &amp; * ( ) + = { } | [ ] \ : &quot; ; &lt; &gt; , . ? /</code></p></td>
</tr>
<tr class="even">
<td><p>Nome do host do espaço de endereço do conector</p></td>
<td><p>Fluxo de mensagens</p></td>
<td><p><code>..</code> (dois pontos finais)</p></td>
</tr>
<tr class="odd">
<td><p>Nome do host para servidore Exchange</p></td>
<td><p>SMTP</p></td>
<td><p><code>_</code> (sublinhado)</p></td>
</tr>
<tr class="even">
<td><p>Nome da organizaçã ou do site</p></td>
<td><p>Executar o programa de Instalação ou mover caixas de correio</p></td>
<td><p><code>~ ` ! @ # $ % ^ &amp; * ( ) _ + = { } | [ ] \ : &quot; ; '  &lt; &gt; , . ? /</code></p></td>
</tr>
<tr class="odd">
<td><p>Nome do diretório interno da organização</p></td>
<td><p>Directory</p></td>
<td><p><code>~ ` ! @ # $ % ^ &amp; * ( ) _ + = { } | [ ] \ : &quot; ; '  &lt; &gt; , . ? /</code></p></td>
</tr>
<tr class="even">
<td><p>Nome da árvore de pasta pública</p></td>
<td><p>Exibindo e criando a pasta pública</p></td>
<td><p><code>: ;</code></p></td>
</tr>
<tr class="odd">
<td><p>Nome do destinatário</p></td>
<td><p>SMTP</p></td>
<td><p><code>' &quot;</code></p></td>
</tr>
<tr class="even">
<td><p>Endereço SMTP da diretiva do destinatário</p></td>
<td><p>Exibindo a hierarquia de pasta pública</p></td>
<td><p><code>~ ` ! @ # $ % ^ &amp; * ( ) + = { } | [ ] \ : &quot; ; &lt; &gt; , . ? /</code></p></td>
</tr>
<tr class="odd">
<td><p>Nome de host de endereço SMTP de diretiva de destinatário</p></td>
<td><p>Fluxo de mensagens</p></td>
<td><p><code>..</code> (dois pontos finais)</p></td>
</tr>
<tr class="even">
<td><p>Nome do diretório interno do site</p></td>
<td><p>Exibindo a hierarquia de pasta pública</p></td>
<td><p><code>? ( ) *</code></p></td>
</tr>
<tr class="odd">
<td><p>Nome do host inteligente</p></td>
<td><p>SMTP</p></td>
<td><p>Espaços no início ou no fim</p></td>
</tr>
</tbody>
</table>

