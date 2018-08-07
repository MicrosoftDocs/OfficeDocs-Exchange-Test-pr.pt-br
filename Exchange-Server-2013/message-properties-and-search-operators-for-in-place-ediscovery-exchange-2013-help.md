---
title: 'Operadores de pesquisa e propr. de mensagem para Descoberta Eletrônica In-loco'
TOCTitle: Operadores de pesquisa e propriedades de mensagem para descoberta eletrônica In-loco
ms:assetid: 402b74e4-8853-4c51-9737-1a9c19f8e3dd
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Dn774955(v=EXCHG.150)
ms:contentKeyID: 62618518
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Operadores de pesquisa e propriedades de mensagem para descoberta eletrônica In-loco

 

_**Aplica-se a:** Exchange Online, Exchange Server 2013_

_**Tópico modificado em:** 2016-12-09_

Este tópico descreve as propriedades de Exchange mensagens de email que você pode pesquisar usando a descoberta eletrônica In-loco & bloqueio no Exchange Server 2013 e Exchange Online. O tópico também descreve os operadores de pesquisa booleana e outras técnicas de consulta de pesquisa que você pode usar para refinar os resultados da pesquisa de descoberta eletrônica.

Descoberta eletrônica in-loco usa a linguagem de consulta de palavra-chave (KQL). Para obter mais detalhes, consulte [referência de sintaxe de linguagem de consulta de palavra-chave](https://go.microsoft.com/fwlink/?linkid=269603).

## Propriedades pesquisáveis no Exchange

A tabela a seguir lista as propriedades da mensagem de email que podem ser pesquisadas usando uma pesquisa de descoberta eletrônica In-loco ou usando o **New-MailboxSearch** ou o cmdlet **Set-MailboxSearch** . A tabela inclui um exemplo da sintaxe *property:value* para cada propriedade e uma descrição dos resultados da pesquisa retornados pelos exemplos.


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Propriedade</th>
<th>Descrição da propriedade</th>
<th>Exemplos</th>
<th>Resultados de pesquisa retornados pelos exemplos</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Attachment</p></td>
<td><p>Os nomes dos arquivos anexados a uma mensagem de email.</p></td>
<td><p>attachment:annualreport.ppt</p>
<p>attachment:anual*</p></td>
<td><p>Mensagens que têm um arquivo anexado denominado annualreport.ppt.</p>
<p>No segundo exemplo, usar o caractere curinga retorna as mensagens com a palavra &quot;anual&quot; no nome do arquivo de anexo.</p></td>
</tr>
<tr class="even">
<td><p>Cco</p></td>
<td><p>O campo Cco de uma mensagem de email.1</p></td>
<td><p>bcc:pilarp@contoso.com</p>
<p>cco:brendaf</p>
<p>cco:&quot;Brenda Fernandes&quot;</p></td>
<td><p>Todos os exemplos retornam mensagens com Brenda Fernandes incluída no campo Cco.</p></td>
</tr>
<tr class="odd">
<td><p>Categoria</p></td>
<td><p>As categorias a serem pesquisadas. As categorias podem ser definidas pelos usuários usando o Outlook ou o Outlook Web App. Os valores possíveis são:</p>
<ul>
<li><p>azul</p></li>
<li><p>verde</p></li>
<li><p>laranja</p></li>
<li><p>roxo</p></li>
<li><p>vermelho</p></li>
<li><p>amarelo</p></li>
</ul></td>
<td><p>category:&quot;Categoria Vermelho&quot;</p></td>
<td><p>Mensagens que foram atribuídas à categoria vermelho nas caixas de correio de origem.</p></td>
</tr>
<tr class="even">
<td><p>Cc</p></td>
<td><p>O campo CC de uma mensagem de email.1</p></td>
<td><p>cc:pilarp@contoso.com</p>
<p>cc:&quot;Brenda Fernandes&quot;</p></td>
<td><p>Em ambos os exemplos, mensagens com Brenda Fernandes especificada no campo CC.</p></td>
</tr>
<tr class="odd">
<td><p>De</p></td>
<td><p>O remetente de uma mensagem de email.1</p></td>
<td><p>from:pilarp@contoso.com</p>
<p>from:contoso.com</p></td>
<td><p>Mensagens enviadas pelo usuário especificado ou enviadas de um domínio especificado.</p></td>
</tr>
<tr class="even">
<td><p>Importância</p></td>
<td><p>A prioridade de uma mensagem de email, que um remetente pode especificar ao enviar uma mensagem. Por padrão, as mensagens são enviadas com prioridade normal, a menos que o remetente defina a prioridade como <strong>alta</strong> ou <strong>baixa</strong>.</p></td>
<td><p>importância:alta</p>
<p>importance:média</p>
<p>importance:baixa</p></td>
<td><p>Mensagens marcadas como alta prioridade, prioridade média ou baixa prioridade.</p></td>
</tr>
<tr class="odd">
<td><p>Tipo</p></td>
<td><p>Tipo de mensagem para pesquisar. Valores possíveis:</p>
<ul>
<li><p>contatos</p></li>
<li><p>documentos</p></li>
<li><p>email</p></li>
<li><p>faxes</p></li>
<li><p>mensagem instantânea</p></li>
<li><p>diários</p></li>
<li><p>reuniões</p></li>
<li><p>observações</p></li>
<li><p>postagens</p></li>
<li><p>rssfeeds</p></li>
<li><p>tarefas</p></li>
<li><p>caixa postal</p></li>
</ul></td>
<td><p>kind:email</p>
<p>kind:email OU kind:mensagens instantâneas ou kind:caixa postal</p></td>
<td><p>Mensagens de email que atendem aos critérios de pesquisa. O segundo exemplo retorna mensagens de email, conversas de mensagens instantâneas e mensagens de voz que atendem aos critérios de pesquisa.</p></td>
</tr>
<tr class="even">
<td><p>Participantes</p></td>
<td><p>Todos os campos de pessoas em uma mensagem de email; os campos são De, Para, Cc e Cco.1</p></td>
<td><p>participants:garthf@contoso.com</p>
<p>participants:contoso.com</p></td>
<td><p>As mensagens enviadas por ou enviados para garthf@contoso.com.</p>
<p>O segundo exemplo retorna todas as mensagens enviadas por ou enviada a um usuário no domínio contoso.com.</p></td>
</tr>
<tr class="odd">
<td><p>Recebido</p></td>
<td><p>A data em que uma mensagem de email foi recebida pelo destinatário.</p></td>
<td><p>received:15/04/2014</p>
<p>received&gt;=01/01/2014 AND received&lt;=31/03/2014</p></td>
<td><p>Mensagens que foram recebidas em 15 de abril de 2014. O segundo exemplo retorna todas as mensagens recebidas entre 1º de janeiro de 2014 e 31 de março de 2014.</p></td>
</tr>
<tr class="even">
<td><p>Destinatários</p></td>
<td><p>Todos os campos de destinatários em uma mensagem de email; esses campos são Para, CC e Cco.1</p></td>
<td><p>recipients:garthf@contoso.com</p>
<p>recipients:contoso.com</p></td>
<td><p>Mensagens enviadas a garthf@contoso.com.</p>
<p>O segundo exemplo retorna as mensagens enviadas para qualquer destinatário no domínio contoso.com.</p></td>
</tr>
<tr class="odd">
<td><p>Enviado</p></td>
<td><p>A data em que uma mensagem de email foi enviada pelo remetente.</p></td>
<td><p>sent:01/07/2014</p>
<p>sent&gt;=01/06/2014 AND sent&lt;=01/07/2014</p></td>
<td><p>Mensagens que foram enviadas na data especificada ou dentro do intervalo de datas especificado.</p></td>
</tr>
<tr class="even">
<td><p>Size</p></td>
<td><p>O tamanho de um item, em bytes.</p></td>
<td><p>size&gt;26214400</p>
<p>size:1..1048576</p></td>
<td><p>Mensagens maiores do que 25 MB.</p>
<p>O segundo exemplo retorna as mensagens de 1 a 1.048.576 bytes (1 MB) de tamanho.</p></td>
</tr>
<tr class="odd">
<td><p>Assunto</p></td>
<td><p>O texto na linha de assunto de uma mensagem de email.</p></td>
<td><p>assunto:&quot;Finanças trimestrais&quot;</p>
<p>subject:northwind</p></td>
<td><p>Mensagens que contêm os exatamente frase &quot;Finanças trimestrais&quot; em qualquer lugar no texto da linha de assunto.</p>
<p>O segundo exemplo retorna todas as mensagens que contêm a palavra northwind na linha assunto.</p></td>
</tr>
<tr class="even">
<td><p>Para</p></td>
<td><p>O campo Para de uma mensagem de email.1</p></td>
<td><p>to:annb@contoso.com</p>
<p>to:clarab</p>
<p>para:&quot;Ann Beebe&quot;</p></td>
<td><p>Todos os exemplos retornam mensagens em que Clara Barbosa é especificada na linha Para:.</p></td>
</tr>
</tbody>
</table>



> [!TIP]
> 1&nbsp;&nbsp;&nbsp;Para o valor de uma propriedade de destinatário, você pode usar o endereço SMTP, o nome para exibição ou o alias para especificar um usuário. Por exemplo, você pode usar clarab@contoso.com, clarab ou "Clara Barbosa" para especificar o usuário Clara Barbosa.



## Operadores de pesquisa com suporte

Operadores de pesquisa booleana, como **AND**, **OR**, ajudarão-lo a definir pesquisas de caixa de correio com mais preciso, incluindo ou excluindo palavras específicas na consulta de pesquisa. Outras técnicas, como o uso de operadores de propriedade (como \> = ou …), aspas, parênteses e caracteres curinga, ajudá-lo a refinar consultas de pesquisa de descoberta eletrônica. A tabela a seguir lista os operadores que você pode usar para limitar ou ampliar os resultados da pesquisa.


> [!IMPORTANT]
> Você deve usar os operadores booleanos letras maiusculas em uma consulta de pesquisa. Por exemplo, use <STRONG>AND</STRONG>; Não use <STRONG>and</STRONG>. Usar operadores minúsculos em consultas de pesquisa retornará um erro.




<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Operador</th>
<th>Uso</th>
<th>Descrição</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>AND</p></td>
<td><p>palavra-chave1 AND palavra-chave2</p></td>
<td><p>Retorna as mensagens que incluem todas as palavras-chave especificadas ou expressões <code>property:value</code> .</p></td>
</tr>
<tr class="even">
<td><p>+</p></td>
<td><p>keyword1 + keyword2 + keyword3</p></td>
<td><p>Retorna os itens que contêm <em><code>keyword2 </code>ou <code>keyword3</code><em>e</em></em>que também contêm <code>keyword1</code>. Portanto, este exemplo é equivalente à consulta <code>(keyword2 OR keyword3) AND keyword1</code>.</p>
<p>Observe que a consulta <code>keyword1 + keyword2</code> (com um espaço após o <strong>+</strong> símbolo) não é o mesmo que usar o operador <strong>AND</strong> . Esta consulta seria equivalente à <code>&quot;keyword1 + keyword2&quot;</code> e retornar itens com a frase exata <code>&quot;keyword1 + keyword2&quot;</code>.</p></td>
</tr>
<tr class="odd">
<td><p>OR</p></td>
<td><p>palavra-chave1 OR palavra-chave2</p></td>
<td><p>Retorna as mensagens que incluem um ou mais palavras-chave especificadas ou expressões <code>property:value</code> .</p></td>
</tr>
<tr class="even">
<td><p>NOT</p></td>
<td><p>palavra-chave1 NOT palavra-chave2</p>
<p>NOT from:&quot;Clara Barbosa&quot;</p></td>
<td><p>Exclui mensagens especificadas por uma palavra-chave ou uma expressão de <code>property:value</code> . Por exemplo, <code>NOT from:&quot;Ann Beebe&quot;</code> exclui mensagens enviadas pelo Ann Beebe.</p></td>
</tr>
<tr class="odd">
<td><p>-</p></td>
<td><p>palavra-chave1 -palavra-chave2</p></td>
<td><p>O mesmo que o operador <strong>NÃO</strong> . Esta consulta retorna itens que contenham <code>keyword1</code> e exclui os itens que contenham <code>keyword2</code>.</p></td>
</tr>
<tr class="even">
<td><p>NEAR</p></td>
<td><p>palavra-chave1 NEAR(n) palavra-chave2</p></td>
<td><p>Retorna as mensagens com palavras próximos uns aos outros, onde n é igual o número de palavras separadamente. Por exemplo, <code>best NEAR(5) worst</code> retorna as mensagens onde a palavra &quot;pior&quot; é dentro de cinco palavras das &quot;melhor&quot;. Se nenhum número for especificado, a distância padrão é oito palavras.</p></td>
</tr>
<tr class="odd">
<td><p>:</p></td>
<td><p>property:valor</p></td>
<td><p>Os dois-pontos (:) na sintaxe <code>property:value</code> Especifica se o valor da propriedade está sendo procurado é igual ao valor especificado. Por exemplo, <code>recipients:garthf@contoso.com</code> retorna qualquer mensagem enviada ao garthf@contoso.com.</p></td>
</tr>
<tr class="even">
<td><p>&lt;</p></td>
<td><p>property&lt;valor</p></td>
<td><p>Indica que a propriedade que está sendo pesquisada é menor do que o valor especificado. 1</p></td>
</tr>
<tr class="odd">
<td><p>&gt;</p></td>
<td><p>property&gt;valor</p></td>
<td><p>Indica que a propriedade que está sendo pesquisada é maior do que o valor especificado.1</p></td>
</tr>
<tr class="even">
<td><p>&lt;=</p></td>
<td><p>property&lt;=valor</p></td>
<td><p>Indica que a propriedade que está sendo pesquisada é menor ou igual a um valor específico.1</p></td>
</tr>
<tr class="odd">
<td><p>&gt;=</p></td>
<td><p>property&gt;=valor</p></td>
<td><p>Indica que a propriedade que está sendo pesquisada é maior ou igual a um valor específico.1</p></td>
</tr>
<tr class="even">
<td><p>..</p></td>
<td><p>property:value1..value2</p></td>
<td><p>Indica que a propriedade que está sendo pesquisada é maior ou igual a valor1 e menor ou igual a valor2.1</p></td>
</tr>
<tr class="odd">
<td><p>&quot; &quot;</p></td>
<td><p>&quot;valor justo&quot;</p>
<p>assunto:&quot;Finanças trimestrais&quot;</p></td>
<td><p>Use aspas duplas (&quot; &quot;) para pesquisar uma frase ou um termo exato na palavra-chave e em consultas de pesquisa de <code>property:value</code>.</p></td>
</tr>
<tr class="even">
<td><p>*</p></td>
<td><p>cat*</p>
<p>subject:set*</p></td>
<td><p>Pesquisas de curinga prefixo (onde o asterisco é colocado no final de uma palavra) correspondam para zero ou mais caracteres nas palavras-chave ou consultas de <code>property:value</code> . Por exemplo, <code>subject:set*</code> retorna mensagens que contêm o conjunto do word, o programa de instalação e configuração (e outras palavras que começam com &quot;set&quot;) na linha de assunto.</p></td>
</tr>
<tr class="odd">
<td><p>( )</p></td>
<td><p>(BOM OU livre) E from:contoso.com</p>
<p>(IPO OR inicial) AND (ação OR títulos)</p>
<p>(finanças trimestrais)</p></td>
<td><p>Os parênteses agrupam frases Boolianas, itens de <code>property:value</code> e palavras-chave. Por exemplo, <code>(quarterly financials)</code> retorna itens que contêm as palavras trimestrais e finanças.</p></td>
</tr>
</tbody>
</table>



> [!TIP]
> 1&nbsp;&nbsp;&nbsp;Use esse operador para propriedades que têm valores numéricos ou de data.



## Não há suporte para caracteres em consultas de pesquisa

Não há suporte para caracteres em uma consulta de pesquisa geralmente causam um erro de pesquisa ou retornam resultados inesperados. Não há suporte para caracteres geralmente estão ocultos e normalmente são adicionados a uma consulta ao copiar a consulta ou partes da consulta de outros aplicativos (por exemplo, Microsoft Word ou Microsoft Excel) e copiá-los para a caixa de palavra-chave na página consulta de pesquisa de descoberta eletrônica In-loco.

Aqui está uma lista dos caracteres não suportados para uma consulta de pesquisa de descoberta eletrônica In-loco.

  - **Aspas inglesas**   Single e double aspas inglesas (também chamadas de *aspas curvas*) não são suportadas. Somente as aspas normais pode ser usadas em uma consulta de pesquisa.

  - **Caracteres não imprimíveis e controle**   Caracteres não imprimíveis e controle não representam um símbolo escrito, como um caractere alfanumérico. Exemplos de não-imprimíveis e caracteres de controle incluem caracteres que formatar texto ou em linhas separadas de texto.

  - **Marca da esquerda para a direita e da direita para a esquerda**   Estes são os caracteres usados para indicar a direção do texto para a esquerda para a direita (por exemplo, inglês e espanhol) e idiomas da direita para a esquerda (por exemplo, árabe e hebraico) do controle.

  - **Operadores booleanos minúsculo**   Anterior conforme explicado, você precisa usar operadores booleanos letras maiusculas, como **AND** e **OU**, em uma consulta de pesquisa. Observe que a sintaxe de consulta com frequência indicará que um operador booleano está sendo usado, mesmo que poderiam ser usadas operadores minúsculas; Por exemplo, `(WordA or WordB) and (WordC or WordD)`.

**Como impedir que os caracteres não suportados em suas consultas de pesquisa?** Basta digitar a consulta na caixa de palavra-chave é a melhor maneira de impedir que os caracteres não suportados. Como alternativa, você pode copiar uma consulta do Word ou Excel e colá-lo no arquivo em um editor de texto sem formatação, como o Microsoft Notepad. Em seguida, salve o arquivo de texto e selecione **ANSI** na lista suspensa **codificação**. Isto irá remover quaisquer caracteres não suportados e formatação. Você pode, em seguida, copie e cole a consulta do arquivo de texto para a caixa de consulta de palavra-chave.

## Dicas e truques de pesquisa

  - As pesquisas de palavra-chave não diferenciam maiúsculas de minúsculas. Por exemplo, **gato** e **GATO** retornam os mesmos resultados.

  - Um espaço entre duas palavras-chave ou duas expressões `property:value` é o mesmo que usar **AND**. Por exemplo, `from:"Sara Davis" subject:reorganization` retorna todas as mensagens enviadas por Sara Davis que contenham a palavra **reorganização** na linha de assunto.

  - Use a sintaxe que coincida com o formato de `property:value` . Valores não diferenciam maiusculas de minúsculas e eles não podem ter um espaço depois do operador. Se houver um espaço, seu valor pretendido apenas será pesquisado de texto completo. Por exemplo **para: pilarp** pesquisas para "pilarp" como uma palavra-chave, em vez de para mensagens enviadas para pilarp.

  - Ao pesquisar uma propriedade de destinatário, como To, From, Cc ou Recipients, você pode usar um endereço SMTP, um alias ou um nome de exibição para indicar um destinatário. Por exemplo, você pode usar brendaf@contoso.com, brendaf ou "Brenda Fernandes".

  - Você pode usar as pesquisas prefixo de curinga — por exemplo, **cat \*** ou **set \***. Sufixo de pesquisas de caractere curinga (\* cat) ou subcadeia de caracteres curinga pesquisas (\* cat \*) não são suportados.

  - Ao pesquisar uma propriedade, usar aspas duplas ("") se o valor de pesquisa consiste em várias palavras. Por exemplo, **Assunto: orçamento T1** retorna mensagens que contêm o **orçamento** na na linha de assunto e que contêm **T1** em qualquer lugar na mensagem ou em qualquer uma das propriedades de mensagem. Usando **Assunto: "orçamento T1"** retorna todas as mensagens que contêm o **orçamento T1** em qualquer lugar na linha de assunto.

