---
title: 'Condições de regra de transporte (predicados): Exchange 2013 Help'
TOCTitle: Condições de regra de fluxo de email e exceções (predicados)
ms:assetid: c918ea00-1e68-4b8b-8d51-6966b4432e2d
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Dd638183(v=EXCHG.150)
ms:contentKeyID: 50486643
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Condições de regra de transporte (predicados)

 

_**Aplica-se a:**Exchange Server 2013_

_**Tópico modificado em:**2017-12-20_

Condições e exceções em regras de fluxo de email (também conhecido como regras de transporte) identificam as mensagens que a regra é aplicada a ou não é aplicada ao. Por exemplo, se a regra adiciona um aviso de isenção às mensagens, você pode configurar a regra seja aplicada apenas às mensagens que contêm palavras específicas, as mensagens enviadas por usuários específicos, ou a todas as mensagens, exceto aqueles enviadas pelos membros de um grupo específico. Coletivamente, as condições e exceções em regras de fluxo de email são também conhecido como *predicados*, porque cada condição, há uma exceção correspondente que usa as mesmas configurações exatas e a sintaxe. A única diferença é que condições especificam mensagens para incluir, enquanto exceções especificam mensagens a serem excluídas.

A maioria das condições e exceções tem uma propriedade que requer um ou mais valores. Por exemplo, a condição **o remetente é** requer o remetente da mensagem. Algumas condições têm duas propriedades. Por exemplo, a condição de **mensagem de um cabeçalho inclui qualquer uma destas palavras** requer uma propriedade para especificar o campo de cabeçalho de mensagem e uma segunda propriedade para especificar o texto para procurar no campo de cabeçalho. Algumas condições ou exceções não têm propriedades. Por exemplo, a condição de **qualquer anexo tem conteúdo executável** simplesmente procura anexos em mensagens que possuem conteúdo executável.

Para obter mais informações sobre regras de fluxo de email no Exchange Server 2013, consulte [Regras de fluxo de emails ou de transporte](mail-flow-rules-transport-rules-in-exchange-2013-exchange-2013-help.md).

Para obter mais informações sobre condições e exceções em regras de fluxo de email em Proteção do Exchange Online ou Exchange Online, consulte [Exceções (predicados) e condições de regra de fluxo de email no Exchange Online](https://technet.microsoft.com/pt-br/library/jj919235\(v=exchg.150\)) ou [Condições de regra de fluxo e email exceções (predicados) no Exchange Online Protection](https://technet.microsoft.com/pt-br/library/jj919234\(v=exchg.150\)).

## Condições e exceções para regras de fluxo de correio em servidores de caixa de correio

As tabelas nas seções a seguir descrevem as condições e exceções que estão disponíveis em regras de fluxo de correio em servidores de caixa de correio. Os tipos de propriedades são descritos na seção tipos de propriedade .

Remetentes

Destinatários

Assunto da mensagem ou no corpo

Anexos

Quaisquer destinatários

Tipos de informações confidenciais da mensagem para e Cc valores, tamanho e conjuntos de caracteres

Remetente e destinatário

Propriedades da mensagem

Cabeçalhos de mensagem

**Observações**:

  - Depois de selecionar uma condição ou exceção no Centro de administração do Exchange (EAC), o valor exibido no campo **Aplicar esta regra se** ou **exceto se** basicamente é geralmente diferente (menor) que o valor de caminho click selecionado. Além disso, quando você cria novas regras com base em um modelo (uma lista filtrada de cenários), você pode selecionar um nome de condição curto em vez de seguindo o caminho completo click com frequência. Os nomes curtos e completo, clique em caminho valores são mostrados na coluna EAT nas tabelas.

  - Se você selecionar **\[aplicar a todas as mensagens\]** no EAC, você não pode especificar outras condições. O equivalente no Shell de Gerenciamento do Exchange é criar uma regra sem especificar quaisquer parâmetros de condição.

  - As configurações e propriedades são o mesmo em condições e exceções, portanto a saída do cmdlet **Get-TransportRulePredicate** não lista exceções separadamente. Além disso, os nomes de alguns dos predicados que são retornados por este cmdlet são diferentes dos nomes de parâmetro correspondente e um predicado pode exigir vários parâmetros.

## Remetentes

Para condições e exceções que examinam o endereço do remetente, você pode especificar onde a regra de procura para o endereço do remetente.

No EAC, na seção de **propriedades desta regra**, clique em **endereço de remetente de correspondência da mensagem**. Observe que você talvez precise clique em **mais opções** para ver essa configuração. O Shell de Gerenciamento do Exchange, o parâmetro é *SenderAddressLocation*. Os valores disponíveis são:

  - **Cabeçalho**    Examine somente remetentes em cabeçalhos de mensagem (por exemplo, os campos **From**, **Sender**ou **Reply-To** ). Isso é o valor padrão e é a maneira como as regras de fluxo de correio funcionou antes Exchange 2013 a atualização cumulativa 1 (CU1).

  - **Envelope**    Examine somente os remetentes de envelope da mensagem (o valor de **MAIL FROM** que foi usado na transmissão SMTP, que normalmente é armazenado no campo **Return-Path** ). Observe que a pesquisa de envelope de mensagem está disponível somente para as seguintes condições (e as exceções correspondentes):
    
      - **O remetente é** (*From*)
    
      - **O remetente é um membro de** (*FromMemberOf*)
    
      - **O endereço do remetente inclui** (*FromAddressContainsWords*)
    
      - **O endereço do remetente corresponde** (*FromAddressMatchesPatterns*)
    
      - **É o domínio do remetente** (*SenderDomainIs*)

  - **Cabeçalho ou envelope** (`HeaderOrEnvelope`)   Examine os remetentes no cabeçalho da mensagem e o envelope da mensagem.


<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>Condição ou exceção no EAC</th>
<th>Parâmetros de condição e exceção no Shell de Gerenciamento do Exchange</th>
<th>Tipo de propriedade</th>
<th>Descrição</th>
<th>Disponível em</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>O remetente é...</strong></p>
<p><strong>O remetente</strong> &gt; <strong>é essa pessoa</strong></p></td>
<td><p><em>From</em></p>
<p><em>ExceptIfFrom</em></p></td>
<td><p><code>Addresses</code></p></td>
<td><p>Mensagens enviadas pelas caixas de correio especificadas, os usuários de email ou contatos de email na organização Exchange.</p></td>
<td><p>Exchange 2007 ou posterior</p></td>
</tr>
<tr class="even">
<td><p><strong>O remetente está em...</strong></p>
<p><strong>O remetente</strong> &gt; <strong>é interno/externo</strong></p></td>
<td><p><em>FromScope</em></p>
<p><em>ExceptIfFromScope</em></p></td>
<td><p><code>UserScopeFrom</code></p></td>
<td><p>Mensagens enviadas por remetentes internos ou remetentes externos.</p></td>
<td><p>Exchange 2007 ou posterior</p></td>
</tr>
<tr class="odd">
<td><p><strong>O remetente é um membro de...</strong></p>
<p><strong>O remetente</strong> &gt; <strong>é um membro deste grupo</strong></p></td>
<td><p><em>FromMemberOf</em></p>
<p><em>ExceptIfFromMemberOf</em></p></td>
<td><p><code>Addresses</code></p></td>
<td><p>Mensagens enviadas por um membro do grupo especificado.</p></td>
<td><p>Exchange 2007 ou posterior</p></td>
</tr>
<tr class="even">
<td><p><strong>O endereço do remetente inclui...</strong></p>
<p><strong>O remetente</strong> &gt; <strong>endereço inclui qualquer uma destas palavras</strong></p></td>
<td><p><em>FromAddressContainsWords</em></p>
<p><em>ExceptIfFromAddressContainsWords</em></p></td>
<td><p><code>Words</code></p></td>
<td><p>Mensagens que contêm as palavras especificadas no endereço de email do remetente.</p></td>
<td><p>Exchange 2007 ou posterior</p></td>
</tr>
<tr class="odd">
<td><p><strong>O endereço do remetente corresponde a</strong></p>
<p><strong>O remetente</strong> &gt; <strong>endereço corresponde a qualquer um desses padrões de texto</strong></p></td>
<td><p><em>FromAddressMatchesPatterns</em></p>
<p><em>ExceptIfFromAddressMatchesPatterns</em></p></td>
<td><p><code>Patterns</code></p></td>
<td><p>Mensagens em que o endereço de email do remetente contém padrões de texto que coincidem com as expressões regulares especificadas.</p></td>
<td><p>Exchange 2007 ou posterior</p></td>
</tr>
<tr class="even">
<td><p><strong>As propriedades especificadas do remetente incluem qualquer uma destas palavras</strong></p>
<p><strong>O remetente</strong> &gt; <strong>tem propriedades específicas, incluindo qualquer uma destas palavras</strong></p></td>
<td><p><em>SenderADAttributeContainsWords</em></p>
<p><em>ExceptIfSenderADAttributeContainsWords</em></p></td>
<td><p>Primeira propriedade: <code>ADAttribute</code></p>
<p>Segunda propriedade: <code>Words</code></p></td>
<td><p>Mensagens em que o atributo especificado Active Directory do remetente contém qualquer uma das palavras especificadas.</p>
<p>Observe que o atributo <strong>Country</strong> requer que o valor de código de país com duas letras (por exemplo, DE para Alemanha).</p></td>
<td><p>Exchange 2010 ou posterior</p></td>
</tr>
<tr class="odd">
<td><p><strong>As propriedades especificadas do remetente correspondem a estes padrões de texto</strong></p>
<p><strong>O remetente</strong> &gt; <strong>tem propriedades específicas de correspondência a esses padrões de texto</strong></p></td>
<td><p><em>SenderADAttributeMatchesPatterns</em></p>
<p><em>ExceptIfSenderADAttributeMatchesPatterns</em></p></td>
<td><p>Primeira propriedade: <code>ADAttribute</code></p>
<p>Segunda propriedade: <code>Patterns</code></p></td>
<td><p>Mensagens em que o atributo especificado Active Directory do remetente contém padrões de texto que coincidem com as expressões regulares especificadas.</p></td>
<td><p>Exchange 2010 ou posterior</p></td>
</tr>
<tr class="even">
<td><p><strong>O remetente substituiu a Dica de Política</strong></p>
<p><strong>O remetente</strong> &gt; <strong>substituiu a dica de política</strong></p></td>
<td><p><em>HasSenderOverride</em></p>
<p><em>ExceptIfHasSenderOverride</em></p></td>
<td><p>n/d</p></td>
<td><p>Mensagens em que o remetente tenha escolhido substituir uma política de prevenção (DLP) de perda de dados. Para obter mais informações sobre políticas de DLP, consulte <a href="technical-overview-of-dlp-data-loss-prevention-in-exchange.md">Prevenção de perda de dados</a>.</p></td>
<td><p>Exchange 2013 ou posterior</p></td>
</tr>
<tr class="odd">
<td><p><strong>Endereço IP do remetente é o intervalo</strong></p>
<p><strong>O remetente</strong> &gt; <strong>em qualquer uma destas intervalos de endereço IP ou corresponde exatamente a</strong></p></td>
<td><p><em>SenderIPRanges</em></p>
<p><em>ExceptIfSenderIPRanges</em></p></td>
<td><p><code>IPAddressRanges</code></p></td>
<td><p>Mensagens em que o endereço IP do remetente corresponde ao endereço IP especificado ou esteja dentro do intervalo de endereços IP especificado.</p></td>
<td><p>Exchange 2013 ou posterior</p></td>
</tr>
<tr class="even">
<td><p><strong>O domínio do remetente é</strong></p>
<p><strong>O remetente</strong> &gt; <strong>domínio é</strong></p></td>
<td><p><em>SenderDomainIs</em></p>
<p><em>ExceptIfSenderDomainIs</em></p></td>
<td><p><code>DomainName</code></p></td>
<td><p>Mensagens em que o domínio do endereço de email do remetente corresponde ao valor especificado.</p>
<p>Se você precisar localizar o remetente domínios que <em>contêm</em> o domínio especificado (por exemplo, qualquer subdomínio de um domínio), use <strong>o endereço do remetente corresponde</strong> (<em>FromAddressMatchesPatterns</em>) condição e especifique o domínio usando a sintaxe: <code>'@domain\.com$'</code>.</p></td>
<td><p>Exchange 2013 ou posterior</p></td>
</tr>
</tbody>
</table>


Voltar ao início

## Destinatários


<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>Condição ou exceção no EAC</th>
<th>Parâmetros de condição e exceção no Shell de Gerenciamento do Exchange</th>
<th>Tipo de propriedade</th>
<th>Descrição</th>
<th>Disponível em</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>O destinatário é...</strong></p>
<p><strong>O destinatário</strong> &gt; <strong>é essa pessoa</strong></p></td>
<td><p><em>SentTo</em></p>
<p><em>ExceptIfSentTo</em></p></td>
<td><p><code>Addresses</code></p></td>
<td><p>Entre em contato com mensagens onde um dos destinatários é a caixa de correio especificada, o usuário de email ou mail na organização Exchange. Os destinatários podem ser nos campos <strong>To</strong>, <strong>Cc</strong>ou <strong>Bcc</strong> da mensagem.</p>
<p><strong>Observação:</strong> você não pode especificar grupos de distribuição ou grupos de segurança habilitados para email. Se você precisar agir em mensagens que são enviadas a um grupo, use a condição <strong>para a caixa contém</strong> (<em>AnyOfToHeader</em>).</p></td>
<td><p>Exchange 2007 ou posterior</p></td>
</tr>
<tr class="even">
<td><p><strong>O destinatário está em...</strong></p>
<p><strong>O destinatário</strong> &gt; <strong>é externo/externo</strong></p></td>
<td><p><em>SentToScope</em></p>
<p><em>ExceptIfSentToScope</em></p></td>
<td><p><code>UserScopeTo</code></p></td>
<td><p>Mensagens enviadas a destinatários internos, destinatários externos, os destinatários externos em organizações parceiras ou destinatários externos nas organizações não-parceiros.</p></td>
<td><p>Exchange 2007 ou posterior</p></td>
</tr>
<tr class="odd">
<td><p><strong>O destinatário é um membro de</strong></p>
<p><strong>O destinatário</strong> &gt; <strong>é um membro deste grupo</strong></p></td>
<td><p><em>SentToMemberOf</em></p>
<p><em>ExceptIfSentToMemberOf</em></p></td>
<td><p><code>Addresses</code></p></td>
<td><p>Mensagens que contêm destinatários que são membros do grupo especificado. O grupo pode ser nos campos <strong>To</strong>, <strong>Cc</strong>ou <strong>Bcc</strong> da mensagem.</p></td>
<td><p>Exchange 2007 ou posterior</p></td>
</tr>
<tr class="even">
<td><p><strong>O endereço do destinatário inclui</strong></p>
<p><strong>O destinatário</strong> &gt; <strong>endereço inclui qualquer uma destas palavras</strong></p></td>
<td><p><em>RecipientAddressContainsWords</em></p>
<p><em>ExceptIfRecipientAddressContainsWords</em></p></td>
<td><p><code>Words</code></p></td>
<td><p>Mensagens que contêm as palavras especificadas no endereço de email do destinatário.</p>
<p><strong>Observação:</strong> Essa condição não considera mensagens que são enviadas a endereços proxy de destinatários. Ela só faz a correspondência de mensagens que são enviadas ao endereço de email principal do destinatário.</p></td>
<td><p>Exchange 2010 ou posterior</p></td>
</tr>
<tr class="odd">
<td><p><strong>O endereço do destinatário corresponde</strong></p>
<p><strong>O destinatário</strong> &gt; <strong>endereço corresponde a qualquer um desses padrões de texto</strong></p></td>
<td><p><em>RecipientAddressMatchesPatterns</em></p>
<p><em>ExceptIfRecipientAddressMatchesPatterns</em></p></td>
<td><p><code>Patterns</code></p></td>
<td><p>Mensagens em que o endereço de email do destinatário contém padrões de texto que coincidem com as expressões regulares especificadas.</p>
<p><strong>Observação:</strong> Essa condição não considera mensagens que são enviadas a endereços proxy de destinatários. Ela só faz a correspondência de mensagens que são enviadas ao endereço de email principal do destinatário.</p></td>
<td><p>Exchange 2010 ou posterior</p></td>
</tr>
<tr class="even">
<td><p><strong>As propriedades especificadas do destinatário incluem qualquer uma destas palavras</strong></p>
<p><strong>O destinatário</strong> &gt; <strong>tem propriedades específicas, incluindo qualquer uma destas palavras</strong></p></td>
<td><p><em>RecipientADAttributeContainsWords</em></p>
<p><em>ExceptIfRecipientADAttributeContainsWords</em></p></td>
<td><p>Primeira propriedade: <code>ADAttribute</code></p>
<p>Segunda propriedade: <code>Words</code></p></td>
<td><p>Mensagens em que o atributo especificado Active Directory de um destinatário contém qualquer uma das palavras especificadas.</p>
<p>Observe que o atributo <strong>Country</strong> requer que o valor de código de país com duas letras (por exemplo, DE para Alemanha).</p></td>
<td><p>Exchange 2010 ou posterior</p></td>
</tr>
<tr class="odd">
<td><p><strong>As propriedades especificadas do destinatário correspondem a estes padrões de texto</strong></p>
<p><strong>O destinatário</strong> &gt; <strong>tem propriedades específicas de correspondência a esses padrões de texto</strong></p></td>
<td><p><em>RecipientADAttributeMatchesPatterns</em></p>
<p><em>ExceptIfRecipientADAttributeMatchesPatterns</em></p></td>
<td><p>Primeira propriedade: <code>ADAttribute</code></p>
<p>Segunda propriedade: <code>Patterns</code></p></td>
<td><p>Mensagens em que o atributo especificado Active Directory de um destinatário contém padrões de texto que coincidem com as expressões regulares especificadas.</p></td>
<td><p>Exchange 2010 ou posterior</p></td>
</tr>
<tr class="even">
<td><p><strong>O domínio do destinatário é</strong></p>
<p><strong>O destinatário</strong> &gt; <strong>domínio é</strong></p></td>
<td><p><em>RecipientDomainIs</em></p>
<p><em>ExceptIfRecipientDomainIs</em></p></td>
<td><p><code>DomainName</code></p></td>
<td><p>Mensagens em que o domínio do endereço de email do destinatário corresponde ao valor especificado.</p>
<p>Se você precisar localizar domínios do destinatário que <em>contêm</em> o domínio especificado (por exemplo, qualquer subdomínio de um domínio), use <strong>o endereço do destinatário corresponde</strong> (<em>RecipientAddressMatchesPatterns</em>) condição e especifique o domínio usando a sintaxe <code>'@domain\.com$'</code>.</p></td>
<td><p>Exchange 2013 ou posterior</p></td>
</tr>
</tbody>
</table>


Voltar ao início

## Assunto da mensagem ou no corpo


> [!TIP]
> A pesquisa de palavras ou padrões de texto nos campos de cabeçalho assunto ou outros na mensagem ocorre <EM>após</EM> a mensagem ter sido decodificada do método de codificação de transferência de conteúdo MIME, usado para transmitir a mensagem binária entre os servidores SMTP em texto ASCII. Não é possível usar condições ou exceções para buscar os valores codificados brutos (tipicamente com base64) dos campos de cabeçalho assunto ou outros nas mensagens.




<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>Condição ou exceção no EAC</th>
<th>Parâmetros de condição e exceção no Shell de Gerenciamento do Exchange</th>
<th>Tipo de propriedade</th>
<th>Descrição</th>
<th>Disponível em</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>O assunto ou o corpo inclui</strong></p>
<p><strong>O assunto ou corpo</strong> &gt; <strong>assunto ou corpo inclui qualquer uma destas palavras</strong></p></td>
<td><p><em>SubjectOrBodyContainsWords</em></p>
<p><em>ExceptIfSubjectOrBodyContainsWords</em></p></td>
<td><p><code>Words</code></p></td>
<td><p>Mensagens que tenham as palavras especificadas no corpo da mensagem ou campo <strong>Subject</strong> .</p></td>
<td><p>Exchange 2007 ou posterior</p></td>
</tr>
<tr class="even">
<td><p><strong>O assunto ou o corpo corresponde</strong></p>
<p><strong>O assunto ou corpo</strong> &gt; <strong>assunto ou corpo corresponde a esses padrões de texto</strong></p></td>
<td><p><em>SubjectOrBodyMatchesPatterns</em></p>
<p><em>ExceptIfSubjectOrBodyMatchesPatterns</em></p></td>
<td><p><code>Patterns</code></p></td>
<td><p>Mensagens onde o campo <strong>Subject</strong> ou mensagem corpo contêm texto padrões que coincidem com as expressões regulares especificadas.</p></td>
<td><p>Exchange 2007 ou posterior</p></td>
</tr>
<tr class="odd">
<td><p><strong>O assunto inclui</strong></p>
<p><strong>O assunto ou corpo</strong> &gt; <strong>subject inclui qualquer uma destas palavras</strong></p></td>
<td><p><em>SubjectContainsWords</em></p>
<p><em>ExceptIfSubjectContainsWords</em></p></td>
<td><p><code>Words</code></p></td>
<td><p>Mensagens que tenham as palavras especificadas no campo <strong>Subject</strong> .</p></td>
<td><p>Exchange 2007 ou posterior</p></td>
</tr>
<tr class="even">
<td><p><strong>O assunto corresponde</strong></p>
<p><strong>O assunto ou corpo</strong> &gt; <strong>assunto corresponde a esses padrões de texto</strong></p></td>
<td><p><em>SubjectMatchesPatterns</em></p>
<p><em>ExceptIfSubjectMatchesPatterns</em></p></td>
<td><p><code>Patterns</code></p></td>
<td><p>Mensagens em que o campo <strong>Subject</strong> contém padrões de texto que coincidem com as expressões regulares especificadas.</p></td>
<td><p>Exchange 2007 ou posterior</p></td>
</tr>
</tbody>
</table>


Voltar ao início

## Anexos

Para obter mais informações sobre como regras de fluxo de correio inspecionar anexos de mensagens, consulte [Usar regras de transporte para inspecionar anexos de mensagens](use-transport-rules-to-inspect-message-attachments-exchange-2013-help.md).


<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>Condição ou exceção no EAC</th>
<th>Parâmetros de condição e exceção no Shell de Gerenciamento do Exchange</th>
<th>Tipo de propriedade</th>
<th>Descrição</th>
<th>Disponível em</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>O conteúdo de qualquer anexo inclui</strong></p>
<p><strong>Qualquer anexo</strong> &gt; <strong>conteúdo inclui qualquer uma destas palavras</strong></p></td>
<td><p><em>AttachmentContainsWords</em></p>
<p><em>ExceptIfAttachmentContainsWords</em></p></td>
<td><p><code>Words</code></p></td>
<td><p>Mensagens em que um anexo contém as palavras especificadas.</p></td>
<td><p>Exchange 2010 ou posterior</p></td>
</tr>
<tr class="even">
<td><p><strong>Corresponde a qualquer conteúdo de anexos</strong></p>
<p><strong>Qualquer anexo</strong> &gt; <strong>conteúdo corresponde a esses padrões de texto</strong></p></td>
<td><p><em>AttachmentMatchesPatterns</em></p>
<p><em>ExceptIfAttachmentMatchesPatterns</em></p></td>
<td><p><code>Patterns</code></p></td>
<td><p>Mensagens em que um anexo contém padrões de texto que coincidem com as expressões regulares especificadas.</p>
<p><strong>Observação:</strong> somente os primeiros 150 kilobytes (KB) os anexos são examinados.</p></td>
<td><p>Exchange 2010 ou posterior</p></td>
</tr>
<tr class="odd">
<td><p><strong>O conteúdo de qualquer anexo não pode ser inspecionado</strong></p>
<p><strong>Qualquer anexo</strong> &gt; <strong>conteúdo não pode ser inspecionado</strong></p></td>
<td><p><em>AttachmentIsUnsupported</em></p>
<p><em>ExceptIfAttachmentIsUnsupported</em></p></td>
<td><p>n/d</p></td>
<td><p>Mensagens em que um anexo nativamente não é reconhecido pelo Exchange e o IFilter necessário não está instalado no servidor de caixa de correio. Para obter mais informações, consulte <a href="register-filter-pack-ifilters-with-exchange-2013-exchange-2013-help.md">Registrar IFilters do Filter Pack com o Exchange 2013</a>.</p></td>
<td><p>Exchange 2010 ou posterior</p></td>
</tr>
<tr class="even">
<td><p><strong>O nome de arquivo de qualquer anexo corresponde</strong></p>
<p><strong>Qualquer anexo</strong> &gt; <strong>nome de arquivo corresponde a esses padrões de texto</strong></p></td>
<td><p><em>AttachmentNameMatchesPatterns</em></p>
<p><em>ExceptIfAttachmentNameMatchesPatterns</em></p></td>
<td><p><code>Patterns</code></p></td>
<td><p>Mensagens em que o nome de arquivo do anexo contém padrões de texto que coincidem com as expressões regulares especificadas.</p></td>
<td><p>Exchange 2010 ou posterior</p></td>
</tr>
<tr class="odd">
<td><p><strong>A extensão de arquivo de qualquer anexo corresponde</strong></p>
<p><strong>Qualquer anexo</strong> &gt; <strong>extensão de arquivo inclui essas palavras</strong></p></td>
<td><p><em>AttachmentExtensionMatchesWords</em></p>
<p><em>ExceptIfAttachmentExtensionMatchesWords</em></p></td>
<td><p><code>Words</code></p></td>
<td><p>Mensagens onde uma extensão de arquivo anexo corresponde a qualquer uma das palavras especificadas.</p></td>
<td><p>Exchange 2013 ou posterior</p></td>
</tr>
<tr class="even">
<td><p><strong>Qualquer anexo é maior ou igual a</strong></p>
<p><strong>Qualquer anexo &gt; tamanho é maior que ou igual a</strong></p></td>
<td><p><em>AttachmentSizeOver</em></p>
<p><em>ExceptIfAttachmentSizeOver</em></p></td>
<td><p><code>Size</code></p></td>
<td><p>Mensagens onde qualquer anexo é maior ou igual ao valor especificado.</p>
<p>No EAC, você só pode especificar o tamanho em kilobytes (KB).</p></td>
<td><p>Exchange 2007 ou posterior</p></td>
</tr>
<tr class="odd">
<td><p><strong>A verificação da mensagem não foi concluída</strong></p>
<p><strong>Qualquer anexo</strong> &gt; <strong>não completou a digitalização</strong></p></td>
<td><p><em>AttachmentProcessingLimitExceeded</em></p>
<p><em>ExceptIfAttachmentProcessingLimitExceeded</em></p></td>
<td><p>n/d</p></td>
<td><p>Onde o mecanismo de regras não foi possível concluir a verificação dos anexos de mensagens. Você pode usar essa condição para criar regras que trabalham juntos para identificar e processar mensagens onde o conteúdo não puderam ser verificado totalmente.</p></td>
<td><p>Exchange 2013 ou posterior</p></td>
</tr>
<tr class="even">
<td><p><strong>Qualquer anexo inclui conteúdo executável</strong></p>
<p><strong>Qualquer anexo</strong> &gt; <strong>tem conteúdo executável</strong></p></td>
<td><p><em>AttachmentHasExecutableContent</em></p>
<p><em>ExceptIfAttachmentHasExecutableContent</em></p></td>
<td><p>n/d</p></td>
<td><p>Mensagens em que um anexo é um arquivo executável. O sistema verifica se as propriedades do arquivo, em vez de confiar na extensão do arquivo.</p></td>
<td><p>Exchange 2013 ou posterior</p></td>
</tr>
<tr class="odd">
<td><p><strong>Algum anexo está protegido por senha</strong></p>
<p><strong>Qualquer anexo</strong> &gt; <strong>é protegido por senha</strong></p></td>
<td><p><em>AttachmentIsPasswordProtected</em></p>
<p><em>ExceptIfAttachmentIsPasswordProtected</em></p></td>
<td><p>n/d</p></td>
<td><p>Onde um anexo é a senha de mensagens protegidas (e, portanto, não podem ser verificadas). Detecção de senha funciona apenas para Office documentos e arquivos. zip.</p></td>
<td><p>Exchange 2013 ou posterior</p></td>
</tr>
</tbody>
</table>


Voltar ao início

## Quaisquer destinatários

As condições e exceções nesta seção fornecem um recurso exclusivo que afeta *todos os* destinatários quando a mensagem contém pelo menos um dos destinatários especificados. Por exemplo, digamos que você tenha uma regra que rejeita mensagens. Se você usar uma condição de destinatário a partir da seção de destinatários , a mensagem será rejeitada somente para os destinatários especificados. Por exemplo, se a regra localiza o destinatário especificado em uma mensagem, mas a mensagem contém cinco outros destinatários. A mensagem é rejeitada para que um destinatário e é entregue aos cinco outros destinatários.

Se você adicionar uma condição de destinatário a partir desta seção, a mesma mensagem é rejeitada para o destinatário detectado e outros cinco destinatários.

Por outro lado, uma exceção destinatário desta seção *impede* a ação de regra seja aplicada a *todos os* destinatários da mensagem, não apenas para os destinatários detectados.

**Observação:** Essa condição não considera mensagens que são enviadas a endereços proxy de destinatários. Ela só faz a correspondência de mensagens que são enviadas ao endereço de email principal do destinatário.


<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>Condição ou exceção no EAC</th>
<th>Parâmetros de condição e exceção no Shell de Gerenciamento do Exchange</th>
<th>Tipo de propriedade</th>
<th>Descrição</th>
<th>Disponível em</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>Qualquer endereço do destinatário inclui</strong></p>
<p><strong>Qualquer destinatário</strong> &gt; <strong>endereço inclui qualquer uma destas palavras</strong></p></td>
<td><p><em>AnyOfRecipientAddressContainsWords</em></p>
<p><em>ExceptIfAnyOfRecipientAddressContainsWords</em></p></td>
<td><p><code>Words</code></p></td>
<td><p>Mensagens que contêm as palavras especificadas nos campos <strong>To</strong>, <strong>Cc</strong>ou <strong>Bcc</strong> da mensagem.</p></td>
<td><p>Exchange 2013 ou posterior</p></td>
</tr>
<tr class="even">
<td><p><strong>Qualquer endereço do destinatário corresponde</strong></p>
<p><strong>Qualquer destinatário</strong> &gt; <strong>endereço corresponde a qualquer um desses padrões de texto</strong></p></td>
<td><p><em>AnyOfRecipientAddressMatchesPatterns</em></p>
<p><em>ExceptIfAnyOfRecipientAddressMatchesPatterns</em></p></td>
<td><p><code>Patterns</code></p></td>
<td><p>Mensagens em que os campos <strong>To</strong>, <strong>Cc</strong>ou <strong>Bcc</strong> contêm padrões de texto que coincidem com as expressões regulares especificadas.</p></td>
<td><p>Exchange 2013 ou posterior</p></td>
</tr>
</tbody>
</table>


Voltar ao início

## Tipos de informações confidenciais da mensagem para e Cc valores, tamanho e conjuntos de caracteres

As condições nesta seção aquela aparência para os valores dos campos **To** e **Cc** se comportam como condições na seção de qualquer destinatário (o*todos os* destinatários da mensagem são afetados pela regra, não apenas o detectou destinatários).

**Observação:** Essa condição não considera mensagens que são enviadas a endereços proxy de destinatários. Ela só faz a correspondência de mensagens que são enviadas ao endereço de email principal do destinatário.


<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>Condição ou exceção no EAC</th>
<th>Parâmetros de condição e exceção no Shell de Gerenciamento do Exchange</th>
<th>Tipo de propriedade</th>
<th>Descrição</th>
<th>Disponível em</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>A mensagem contém informações confidenciais</strong></p>
<p><strong>A mensagem</strong> &gt; <strong>contém qualquer um desses tipos de informações confidenciais</strong></p></td>
<td><p><em>MessageContainsDataClassifications</em></p>
<p><em>ExceptIfMessageContainsDataClassifications</em></p></td>
<td><p><code>SensitiveInformationTypes</code></p></td>
<td><p>Mensagens que contêm informações confidenciais, conforme definido pelas políticas de (DLP) de prevenção de perda de dados.</p>
<p>Essa condição é exigida para regras que usam a ação <strong>notificar o remetente com uma dica de política</strong> (<em>NotifySender</em>).</p></td>
<td><p>Exchange 2013 ou posterior</p></td>
</tr>
<tr class="even">
<td><p><strong>A caixa Para contém</strong></p>
<p><strong>A mensagem</strong> &gt; <strong>à caixa contém essa pessoa</strong></p></td>
<td><p><em>AnyOfToHeader</em></p>
<p><em>ExceptIfAnyOfToHeader</em></p></td>
<td><p><code>Addresses</code></p></td>
<td><p>Mensagens onde o campo <strong>To</strong> inclui qualquer um dos destinatários especificados.</p></td>
<td><p>Exchange 2007 ou posterior</p></td>
</tr>
<tr class="odd">
<td><p><strong>A caixa Para contém um membro de</strong></p>
<p><strong>A mensagem</strong> &gt; <strong>à caixa contém um membro deste grupo</strong></p></td>
<td><p><em>AnyOfToHeaderMemberOf</em></p>
<p><em>ExceptIfAnyOfToHeaderMemberOf</em></p></td>
<td><p><code>Addresses</code></p></td>
<td><p>Mensagens em que o campo <strong>To</strong> contém um destinatário que é um membro do grupo especificado.</p></td>
<td><p>Exchange 2007 ou posterior</p></td>
</tr>
<tr class="even">
<td><p><strong>A caixa Cc contém</strong></p>
<p><strong>A mensagem</strong> &gt; <strong>caixa Cc contém essa pessoa</strong></p></td>
<td><p><em>AnyOfCcHeader</em></p>
<p><em>ExceptIfAnyOfCcHeader</em></p></td>
<td><p><code>Addresses</code></p></td>
<td><p>Mensagens onde o campo <strong>Cc</strong> inclui qualquer um dos destinatários especificados.</p></td>
<td><p>Exchange 2007 ou posterior</p></td>
</tr>
<tr class="odd">
<td><p><strong>A caixa Cc contém um membro de</strong></p>
<p><strong>A mensagem</strong> &gt; <strong>contém um membro deste grupo</strong></p></td>
<td><p><em>AnyOfCcHeaderMemberOf</em></p>
<p><em>ExceptIfAnyOfCcHeaderMemberOf</em></p></td>
<td><p><code>Addresses</code></p></td>
<td><p>Mensagens em que o campo <strong>Cc</strong> contém um destinatário que é um membro do grupo especificado.</p></td>
<td><p>Exchange 2007 ou posterior</p></td>
</tr>
<tr class="even">
<td><p><strong>A caixa Para ou Cc contém</strong></p>
<p><strong>A mensagem</strong> &gt; <strong>para ou caixa Cc contém essa pessoa</strong></p></td>
<td><p><em>AnyOfToCcHeader</em></p>
<p><em>ExceptIfAnyOfToCcHeader</em></p></td>
<td><p><code>Addresses</code></p></td>
<td><p>Mensagens em que os campos <strong>To</strong> ou <strong>Cc</strong> contêm qualquer um dos destinatários especificados.</p></td>
<td><p>Exchange 2007 ou posterior</p></td>
</tr>
<tr class="odd">
<td><p><strong>A caixa Para ou Cc contém um membro do</strong></p>
<p><strong>A mensagem</strong> &gt; <strong>para ou caixa Cc contém um membro desse grupo</strong></p></td>
<td><p><em>AnyOfToCcHeaderMemberOf</em></p>
<p><em>ExceptIfAnyOfToCcHeaderMemberOf</em></p></td>
<td><p><code>Addresses</code></p></td>
<td><p>Mensagens em que os campos <strong>To</strong> ou <strong>Cc</strong> contêm um destinatário que é um membro do grupo especificado.</p></td>
<td><p>Exchange 2007 ou posterior</p></td>
</tr>
<tr class="even">
<td><p><strong>O tamanho da mensagem é maior ou igual a</strong></p>
<p><strong>A mensagem</strong> &gt; <strong>tamanho é maior que ou igual a</strong></p></td>
<td><p><em>MessageSizeOver</em></p>
<p><em>ExceptIfMessageSizeOver</em></p></td>
<td><p><code>Size</code></p></td>
<td><p>Mensagens onde o tamanho total (mensagem mais anexos) é maior que ou igual ao valor especificado.</p>
<p>No EAC, você só pode especificar o tamanho em kilobytes (KB).</p>
<p><strong>Observação:</strong> os limites de tamanho de mensagem em caixas de correio são avaliados antes de regras de fluxo de correio. Uma mensagem que é muito grande para uma caixa de correio será rejeitada antes de uma regra com essa condição é capaz de atuar na mensagem.</p></td>
<td><p>Exchange 2013 ou posterior</p></td>
</tr>
<tr class="odd">
<td><p><strong>O nome do conjunto de caracteres da mensagem inclui qualquer uma destas palavras</strong></p>
<p><strong>A mensagem</strong> &gt; <strong>nome do conjunto de caracteres inclui qualquer uma destas palavras</strong></p></td>
<td><p><em>ContentCharacterSetContainsWords</em></p>
<p><em>ExceptIfContentCharacterSetContainsWords</em></p></td>
<td><p><code>CharacterSets</code></p></td>
<td><p>Mensagens que contêm qualquer um do caractere especificado definir nomes.</p></td>
<td><p>Exchange 2013 ou posterior</p></td>
</tr>
</tbody>
</table>


Voltar ao início

## Remetente e destinatário


<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>Condição ou exceção no EAC</th>
<th>Parâmetros de condição e exceção no Shell de Gerenciamento do Exchange</th>
<th>Tipo de propriedade</th>
<th>Descrição</th>
<th>Disponível em</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>O remetente é uma do destinatário</strong></p>
<p><strong>O remetente e o destinatário</strong> &gt; <strong>relacionamento do remetente para um destinatário é</strong></p></td>
<td><p><em>SenderManagementRelationship</em></p>
<p><em>ExceptIfSenderManagementRelationship</em></p></td>
<td><p><code>ManagementRelationship</code></p></td>
<td><p>Mensagens em que o remetente é o gerente de um destinatário ou o remetente é gerenciado por um destinatário.</p></td>
<td><p>Exchange 2010 ou posterior</p></td>
</tr>
<tr class="even">
<td><p><strong>A mensagem está entre os membros desses grupos</strong></p>
<p><strong>O remetente e o destinatário</strong> &gt; <strong>a mensagem é entre membros desses grupos</strong></p></td>
<td><p><em>BetweenMemberOf1</em> e <em>BetweenMemberOf2</em></p>
<p><em>ExceptIfBetweenMemberOf1</em> e <em>ExceptIfBetweenMemberOf2</em></p></td>
<td><p><code>Addresses</code></p></td>
<td><p>Mensagens enviadas entre membros dos grupos especificados.</p></td>
<td><p>Exchange 2007 ou posterior</p></td>
</tr>
<tr class="odd">
<td><p><strong>O gerente do remetente ou destinatário é</strong></p>
<p><strong>O remetente e o destinatário</strong> &gt; <strong>o gerente do remetente ou destinatário é essa pessoa</strong></p></td>
<td><p><em>ManagerForEvaluatedUser</em> e <em>ManagerAddress</em></p>
<p><em>ExceptIfManagerForEvaluatedUser</em> e <em>ExceptIfManagerAddress</em></p></td>
<td><p>Primeira propriedade: <code>EvaluatedUser</code></p>
<p>Segunda propriedade: <code>Addresses</code></p></td>
<td><p>Mensagens em que um usuário especificado é o gerente do remetente, ou um usuário especificado é o gerente de um destinatário.</p></td>
<td><p>Exchange 2010 ou posterior</p></td>
</tr>
<tr class="even">
<td><p><strong>A propriedade do remetente e de qualquer destinatário se compara a</strong></p>
<p><strong>O remetente e o destinatário</strong> &gt; <strong>o remetente e a propriedade destinatário se comparam com</strong></p></td>
<td><p><em>ADAttributeComparisonAttribute</em> e <em>ADComparisonOperator</em></p>
<p><em>ExceptIfADAttributeComparisonAttribute</em> e <em>ExceptIfADComparisonOperator</em></p></td>
<td><p>Primeira propriedade: <code>ADAttribute</code></p>
<p>Segunda propriedade: <code>Evaluation</code></p></td>
<td><p>Mensagens em que o atributo especificado Active Directory para o remetente e o destinatário corresponder ou não coincidem.</p></td>
<td><p>Exchange 2010 ou posterior</p></td>
</tr>
</tbody>
</table>


Voltar ao início

## Propriedades da mensagem


<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>Condição ou exceção no EAC</th>
<th>Parâmetros de condição e exceção no Shell de Gerenciamento do Exchange</th>
<th>Tipo de propriedade</th>
<th>Descrição</th>
<th>Disponível em</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>O tipo de mensagem é</strong></p>
<p><strong>As propriedades da mensagem</strong> &gt; <strong>incluem o tipo de mensagem</strong></p></td>
<td><p><em>MessageTypeMatches</em></p>
<p><em>ExceptIfMessageTypeMatches</em></p></td>
<td><p><code>MessageType</code></p></td>
<td><p>Mensagens do tipo especificado.</p>

> [!TIP]
> Quando Outlook ou Outlook Web App estiver configurada para encaminhar uma mensagem, a propriedade <STRONG>ForwardingSmtpAddress</STRONG> é adicionada à mensagem. O tipo de mensagem não é alterado para <CODE>AutoForward</CODE>.


</td>
<td><p>Exchange 2010 ou posterior</p></td>
</tr>
<tr class="even">
<td><p><strong>A mensagem foi classificada como</strong></p>
<p><strong>As propriedades da mensagem</strong> &gt; <strong>incluir essa classificação</strong></p></td>
<td><p><em>HasClassification</em></p>
<p><em>ExceptIfHasClassification</em></p></td>
<td><p><code>MessageClassification</code></p></td>
<td><p>Mensagens que têm a classificação de mensagem especificado. Esta é uma classificação de mensagem personalizado que você pode criar usando o cmdlet <strong>New-MessageClassification</strong> em sua organização.</p></td>
<td><p>Exchange 2007 ou posterior</p></td>
</tr>
<tr class="odd">
<td><p><strong>A mensagem não foi marcada com qualquer classificação</strong></p>
<p><strong>As propriedades da mensagem</strong> &gt; <strong>não incluir qualquer classificação</strong></p></td>
<td><p><em>HasNoClassification</em></p>
<p><em>ExceptIfHasNoClassification</em></p></td>
<td><p>n/d</p></td>
<td><p>Mensagens que não têm uma classificação de mensagem.</p></td>
<td><p>Exchange 2010 ou posterior</p></td>
</tr>
<tr class="even">
<td><p><strong>A mensagem tem um SCL maior ou igual a</strong></p>
<p><strong>As propriedades da mensagem</strong> &gt; <strong>incluir um SCL maior ou igual a</strong></p></td>
<td><p><em>SCLOver</em></p>
<p><em>ExceptIfSCLOver</em></p></td>
<td><p><code>SCLValue</code></p></td>
<td><p>Mensagens que são atribuídas a um nível de confiança de spam (SCL) é maior que ou igual ao valor especificado.</p></td>
<td><p>Exchange 2007 ou posterior</p></td>
</tr>
<tr class="odd">
<td><p><strong>A importância da mensagem foi definida como</strong></p>
<p><strong>As propriedades da mensagem</strong> &gt; <strong>incluem o nível de importância</strong></p></td>
<td><p><em>WithImportance</em></p>
<p><em>ExceptIfWithImportance</em></p></td>
<td><p><code>Importance</code></p></td>
<td><p>Mensagens que estão marcadas com o nível de importância especificado.</p></td>
<td><p>Exchange 2007 ou posterior</p></td>
</tr>
</tbody>
</table>


Voltar ao início

## Cabeçalhos de mensagem


> [!TIP]
> A pesquisa de palavras ou padrões de texto nos campos de cabeçalho assunto ou outros na mensagem ocorre <EM>após</EM> a mensagem ter sido decodificada do método de codificação de transferência de conteúdo MIME, usado para transmitir a mensagem binária entre os servidores SMTP em texto ASCII. Não é possível usar condições ou exceções para buscar os valores codificados brutos (tipicamente com base64) dos campos de cabeçalho assunto ou outros nas mensagens.




<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>Condição ou exceção no EAC</th>
<th>Parâmetros de condição e exceção no Shell de Gerenciamento do Exchange</th>
<th>Tipo de propriedade</th>
<th>Descrição</th>
<th>Disponível em</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>O cabeçalho da mensagem inclui</strong></p>
<p><strong>O cabeçalho da mensagem</strong> &gt; <strong>inclui qualquer uma destas palavras</strong></p></td>
<td><p><em>HeaderContainsMessageHeader</em> e <em>HeaderContainsWords</em></p>
<p><em>ExceptIfHeaderContainsMessageHeader</em> e <em>ExceptIfHeaderContainsWords</em></p></td>
<td><p>Primeira propriedade: <code>MessageHeaderField</code></p>
<p>Segunda propriedade: <code>Words</code></p></td>
<td><p>Mensagens que contêm o campo de cabeçalho especificado e o valor do campo cabeçalho contém as palavras especificadas.</p>
<p>O nome do campo do cabeçalho e o valor do campo de cabeçalho sempre são usados juntos.</p></td>
<td><p>Exchange 2007 ou posterior</p></td>
</tr>
<tr class="even">
<td><p><strong>O cabeçalho da mensagem corresponde</strong></p>
<p><strong>O cabeçalho da mensagem</strong> &gt; <strong>corresponde a esses padrões de texto</strong></p></td>
<td><p><em>HeaderMatchesMessageHeader</em> e <em>HeaderMatchesPatterns</em></p>
<p><em>ExceptIfHeaderMatchesMessageHeader</em> e <em>ExceptIfHeaderMatchesPatterns</em></p></td>
<td><p>Primeira propriedade: <code>MessageHeaderField</code></p>
<p>Segunda propriedade: <code>Patterns</code></p></td>
<td><p>Mensagens que contêm o campo de cabeçalho especificado e o valor do campo cabeçalho contém as expressões regulares especificadas.</p>
<p>O nome do campo do cabeçalho e o valor do campo de cabeçalho sempre são usados juntos.</p></td>
<td><p>Exchange 2007 ou posterior</p></td>
</tr>
</tbody>
</table>


Voltar ao início

## Condições e exceções para regras de fluxo de correio nos servidores de transporte de borda

As condições e exceções que estão disponíveis em regras de fluxo de correio nos servidores de transporte de borda são um subconjunto pequeno do que está disponível em servidores de caixa de correio. Não há nenhuma EAT nos servidores de transporte de borda, portanto você só pode gerenciar regras de fluxo de email no Shell de Gerenciamento do Exchange no servidor local de transporte de borda. As condições e exceções são descritas na tabela a seguir. Os tipos de propriedades são descritos na seção tipos de propriedade .


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Parâmetros de condição e exceção no Shell de Gerenciamento do Exchange</th>
<th>Tipo de propriedade</th>
<th>Descrição</th>
<th>Disponível em</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>AnyOfRecipientAddressContainsWords</em></p>
<p><em>ExceptIfAnyOfRecipientAddressContainsWords</em></p></td>
<td><p><code>Words</code></p></td>
<td><p>Mensagens que contêm as palavras especificadas nos campos <strong>To</strong>, <strong>Cc</strong>ou <strong>Bcc</strong> .</p>
<p>Quando uma mensagem contém o destinatário especificado, a ação de regra é aplicada (ou não aplicada) para <em>todos os</em> destinatários da mensagem. Por exemplo, a mensagem será rejeitada para todos os destinatários da mensagem, não apenas para o destinatário especificado.</p></td>
<td><p>Exchange 2013 ou posterior</p></td>
</tr>
<tr class="even">
<td><p><em>AnyOfRecipientAddressMatchesPatterns</em></p>
<p><em>ExceptIfAnyOfRecipientAddressMatchesPatterns</em></p></td>
<td><p><code>Patterns</code></p></td>
<td><p>Mensagens em que os campos <strong>To</strong>, <strong>Cc</strong>ou <strong>Bcc</strong> contêm padrões de texto que coincidem com as expressões regulares especificadas.</p>
<p>Quando uma mensagem contém o destinatário especificado, a ação de regra é aplicada (ou não aplicada) para <em>todos os</em> destinatários da mensagem. Por exemplo, a mensagem será rejeitada para todos os destinatários da mensagem, não apenas para o destinatário especificado.</p></td>
<td><p>Exchange 2013 ou posterior</p></td>
</tr>
<tr class="odd">
<td><p><em>AttachmentSizeOver</em></p>
<p><em>ExceptIfAttachmentSizeOver</em></p></td>
<td><p><code>Size</code></p></td>
<td><p>Mensagens com anexos onde qualquer anexo é maior ou igual ao valor especificado.</p></td>
<td><p>Exchange 2007 ou posterior</p></td>
</tr>
<tr class="even">
<td><p><em>FromAddressContainsWords</em></p>
<p><em>ExceptIfFromAddressContainsWords</em></p></td>
<td><p><code>Words</code></p></td>
<td><p>Mensagens que contêm as palavras especificadas no endereço de email do remetente.</p></td>
<td><p>Exchange 2007 ou posterior</p></td>
</tr>
<tr class="odd">
<td><p><em>FromAddressMatchesPatterns</em></p>
<p><em>ExceptIfFromAddressMatchesPatterns</em></p></td>
<td><p><code>Patterns</code></p></td>
<td><p>Mensagens em que o endereço de email do remetente contém padrões de texto que coincidem com as expressões regulares especificadas.</p></td>
<td><p>Exchange 2007 ou posterior</p></td>
</tr>
<tr class="even">
<td><p><em>FromScope</em></p>
<p><em>ExceptIfFromScope</em></p></td>
<td><p><code>UserScopeFrom</code></p></td>
<td><p>Mensagens enviadas por remetentes internos ou remetentes externos.</p></td>
<td><p>Exchange 2007 ou posterior</p></td>
</tr>
<tr class="odd">
<td><p><em>HeaderContainsMessageHeader</em> e <em>HeaderContainsWords</em></p>
<p><em>ExceptIfHeaderContainsMessageHeader</em> e <em>ExceptIfHeaderContainsWords</em></p></td>
<td><p>Primeira propriedade: <code>MessageHeaderField</code></p>
<p>Segunda propriedade: <code>Words</code></p></td>
<td><p>Mensagens que contêm o campo de cabeçalho especificado e o valor do campo cabeçalho contém as palavras especificadas.</p>
<p>O nome do campo do cabeçalho e o valor do campo de cabeçalho sempre são usados juntos.</p></td>
<td><p>Exchange 2007 ou posterior</p></td>
</tr>
<tr class="even">
<td><p><em>HeaderMatchesMessageHeader</em> e <em>HeaderMatchesPatterns</em></p>
<p><em>ExceptIfHeaderMatchesMessageHeader</em> e <em>ExceptIfHeaderMatchesPatterns</em></p></td>
<td><p>Primeira propriedade: <code>MessageHeaderField</code></p>
<p>Segunda propriedade: <code>Patterns</code></p></td>
<td><p>Mensagens que contêm o campo de cabeçalho especificado e o valor do campo cabeçalho contém as expressões regulares especificadas.</p>
<p>O nome do campo do cabeçalho e o valor do campo de cabeçalho sempre são usados juntos.</p></td>
<td><p>Exchange 2007 ou posterior</p></td>
</tr>
<tr class="odd">
<td><p><em>MessageSizeOver</em></p>
<p><em>ExceptIfMessageSizeOver</em></p></td>
<td><p><code>Size</code></p></td>
<td><p>Mensagens onde o tamanho total (mensagem mais anexos) é maior que ou igual ao valor especificado.</p></td>
<td><p>Exchange 2013 ou posterior</p></td>
</tr>
<tr class="even">
<td><p><em>SCLOver</em></p>
<p><em>ExceptIfSCLOver</em></p></td>
<td><p><code>SCLValue</code></p></td>
<td><p>Mensagens que são atribuídas a um SCL maior ou igual ao valor especificado.</p></td>
<td><p>Exchange 2007 ou posterior</p></td>
</tr>
<tr class="odd">
<td><p><em>SubjectContainsWords</em></p>
<p><em>ExceptIfSubjectContainsWords</em></p></td>
<td><p><code>Words</code></p></td>
<td><p>Mensagens que contêm as palavras especificadas no campo <strong>Subject</strong> .</p></td>
<td><p>Exchange 2007 ou posterior</p></td>
</tr>
<tr class="even">
<td><p><em>SubjectMatchesPatterns</em></p>
<p><em>ExceptIfSubjectMatchesPatterns</em></p></td>
<td><p><code>Patterns</code></p></td>
<td><p>Mensagens em que o campo <strong>Subject</strong> contém padrões de texto que coincidem com as expressões regulares especificadas.</p></td>
<td><p>Exchange 2007 ou posterior</p></td>
</tr>
<tr class="odd">
<td><p><em>SubjectOrBodyContainsWords</em></p>
<p><em>ExceptIfSubjectOrBodyContainsWords</em></p></td>
<td><p><code>Words</code></p></td>
<td><p>Mensagens que contêm as palavras especificadas no corpo da mensagem ou campo <strong>Subject</strong> .</p></td>
<td><p>Exchange 2007 ou posterior</p></td>
</tr>
<tr class="even">
<td><p><em>SubjectOrBodyMatchesPatterns</em></p>
<p><em>ExceptIfSubjectOrBodyMatchesPatterns</em></p></td>
<td><p><code>Patterns</code></p></td>
<td><p>Mensagens onde o campo <strong>Subject</strong> ou mensagem corpo contêm texto padrões que coincidem com as expressões regulares especificadas.</p></td>
<td><p>Exchange 2007 ou posterior</p></td>
</tr>
</tbody>
</table>


Voltar ao início

## Tipos de propriedade

Os tipos de propriedade são usados em condições e exceções são descritos na tabela a seguir.


> [!TIP]
> Se a propriedade for uma cadeia de caracteres, os espaços à direita não serão permitidos.




<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Tipo de propriedade</th>
<th>Valores válidos</th>
<th>Descrição</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code>ADAttribute</code></p></td>
<td><p>Selecione uma lista de atributos de Active Directory predefinida</p></td>
<td><p>UNRESOLVED_TOKENBLOCK_VAL(PD_Transport_Rules_ADAttributes_Snippet)</p>
<p>No EAC, para especificar várias palavras ou padrões de texto para o mesmo atributo, separe os valores com vírgulas. Por exemplo, o valor <strong>são Francisco, Palo Alto</strong> para o atributo <strong>cidade</strong> procura por &quot;É igual a cidade são Francisco&quot; ou cidade é igual a Palo Alto&quot;.</p>
<p>No Shell de Gerenciamento do Exchange, use a sintaxe <code>&quot;AttributeName1:Value1,Value 2 with spaces,Value3...&quot;,&quot;AttributeName2:Word4,Value 5 with spaces,Value6...&quot;</code>, onde <code>Value</code> é o padrão de palavra ou texto que você deseja corresponder.</p>
<p>Por exemplo, <code>&quot;City:San Francisco,Palo Alto&quot;</code> ou <code>&quot;City:San Francisco,Palo Alto&quot;</code>,<code>&quot;Department:Sales,Finance&quot;</code>.</p>
<p>Quando você especifica vários atributos ou vários valores para o mesmo atributo, o operador de <strong>or</strong> é usado. Não use valores com espaços à direita ou.</p>
<p>Observe que o atributo <strong>Country</strong> requer o valor de código duas letras ISO 3166-1 país (por exemplo, DE para Alemanha). Para procurar por valores, consulte <a href="https://go.microsoft.com/fwlink/p/?linkid=331680">https://go.microsoft.com/fwlink/p/?LinkId=331680</a>.</p></td>
</tr>
<tr class="even">
<td><p><code>Addresses</code></p></td>
<td><p>destinatários Exchange</p></td>
<td><p>Dependendo da natureza da exceção ou condição, você poderá especificar qualquer objeto habilitado para email na organização (por exemplo, condições relacionados a destinatários) ou você pode ser limitado a um tipo de objeto específico (por exemplo, grupos de participação em grupo condições). E a condição ou exceção pode exigir um valor ou permitir vários valores.</p>
<p>No Shell de Gerenciamento do Exchange, separe os vários valores por vírgulas.</p>
<p><strong>Observação:</strong> Essa condição não considera mensagens que são enviadas a endereços proxy de destinatários. Ela só faz a correspondência de mensagens que são enviadas ao endereço de email principal do destinatário.</p></td>
</tr>
<tr class="odd">
<td><p><code>CharacterSets</code></p></td>
<td><p>Matriz de nomes de conjunto de caracteres</p></td>
<td><p>Conjuntos de caracteres de conteúdo de um ou mais que existem em uma mensagem. Por exemplo:</p>
<ul>
<li><p><code>Arabic/iso-8859-6</code></p></li>
<li><p><code>Chinese/big5</code></p></li>
<li><p><code>Chinese/euc-cn</code></p></li>
<li><p><code>Chinese/euc-tw</code></p></li>
<li><p><code>Chinese/gb2312</code></p></li>
<li><p><code>Chinese/iso-2022-cn</code></p></li>
<li><p><code>Cyrillic/iso-8859-5</code></p></li>
<li><p><code>Cyrillic/koi8-r</code></p></li>
<li><p><code>Cyrillic/windows-1251</code></p></li>
<li><p><code>Greek/iso-8859-7</code></p></li>
<li><p><code>Hebrew/iso-8859-8</code></p></li>
<li><p><code>Japanese/euc-jp</code></p></li>
<li><p><code>Japanese/iso-022-jp</code></p></li>
<li><p><code>Japanese/shift-jis</code></p></li>
<li><p><code>Korean/euc-kr</code></p></li>
<li><p><code>Korean/johab</code></p></li>
<li><p><code>Korean/ks_c_5601-1987</code></p></li>
<li><p><code>Turkish/windows-1254</code></p></li>
<li><p><code>Turkish/iso-8859-9</code></p></li>
<li><p><code>Vietnamese/tcvn</code></p></li>
</ul></td>
</tr>
<tr class="even">
<td><p><code>DomainName</code></p></td>
<td><p>Matriz de domínios SMTP</p></td>
<td><p>Por exemplo, <code>contoso.com</code> ou <code>eu.contoso.com</code>.</p>
<p>No Shell de Gerenciamento do Exchange, você pode especificar vários domínios separados por vírgulas.</p></td>
</tr>
<tr class="odd">
<td><p><code>EvaluatedUser</code></p></td>
<td><p>Valor único de <strong>remetente</strong> ou <strong>destinatário</strong></p></td>
<td><p>Especifica se a regra está procurando o gerente do remetente ou o gerente do destinatário.</p></td>
</tr>
<tr class="even">
<td><p><code>Evaluation</code></p></td>
<td><p>Valor único de <strong>Equal</strong> ou <strong>não igual</strong> (<code>NotEqual</code>)</p></td>
<td><p>Ao comparar o atributo Active Directory entre o remetente e destinatários, especifica se os valores devem corresponder ou não coincidem.</p></td>
</tr>
<tr class="odd">
<td><p><code>Importance</code></p></td>
<td><p>Valor único de <strong>baixa</strong>, <strong>Normal</strong> ou <strong>alta</strong></p></td>
<td><p>O nível de importância que foi atribuído à mensagem pelo remetente em Outlook ou Outlook Web App.</p></td>
</tr>
<tr class="even">
<td><p><code>IPAddressRanges</code></p></td>
<td><p>Matriz de endereços IP ou intervalos de endereços</p></td>
<td><p>Você inserir os endereços IPv4 usando a seguinte sintaxe:</p>
<ul>
<li><p><strong>Endereço IP único</strong>   Por exemplo, <code>192.168.1.1</code>.</p></li>
<li><p><strong>Intervalo de endereços IP</strong>   Por exemplo, <code>192.168.0.1-192.168.0.254</code>.</p></li>
<li><p><strong>Intervalo de endereços IP de roteamento entre domínios (CIDR)</strong>   Por exemplo, <code>192.168.0.1/25</code>.</p></li>
</ul>
<p>No Shell de Gerenciamento do Exchange, você pode especificar vários endereços IP ou intervalos separados por vírgulas.</p></td>
</tr>
<tr class="odd">
<td><p><code>ManagementRelationship</code></p></td>
<td><p>Valor único de <strong>Manager</strong> ou <strong>subordinado direto</strong> (<code>DirectReport</code>)</p></td>
<td><p>Especifica a relação entre o remetente e qualquer um dos destinatários. A regra verifica se o atributo <strong>Manager</strong> em Active Directory para verificar se o remetente é o gerente de um destinatário, ou se o remetente é gerenciado por um destinatário.</p></td>
</tr>
<tr class="even">
<td><p><code>MessageClassification</code></p></td>
<td><p>Classificação de mensagem única</p></td>
<td><p>No EAC, selecione da lista de classificações de mensagem que você criou.</p>
<p>No Shell de Gerenciamento do Exchange, você pode usar o cmdlet <strong>Get-MessageClassification</strong> para identificar a classificação de mensagem. Por exemplo, use o seguinte comando para buscar mensagens com a classificação de <code>Company Internal</code> e preceder o assunto da mensagem com o valor <code>CompanyInternal</code>.</p>
<p><code>New-TransportRule &quot;Rule Name&quot; -HasClassification @(Get-MessageClassification &quot;Company Internal&quot;).Identity -PrependSubject &quot;CompanyInternal&quot;</code></p></td>
</tr>
<tr class="odd">
<td><p><code>MessageHeaderField</code></p></td>
<td><p>Cadeia de caracteres única</p></td>
<td><p>Especifica o nome do campo de cabeçalho. O nome do campo de cabeçalho sempre é emparelhado com o valor no campo de cabeçalho (word ou o texto padrão correspondente).</p>
<p>O <em>cabeçalho da mensagem</em> é uma coleção de campos obrigatórios e opcionais de cabeçalho na mensagem. Exemplos de campos de cabeçalho são <strong>To</strong>, <strong>From</strong>, <strong>Received</strong>e <strong>Content-Type</strong>. Campos de cabeçalho oficial são definidos na RFC 5322. Campos de cabeçalho não oficiais começam com <strong>X-</strong> e são conhecidos como <em>cabeçalhos X</em>.</p></td>
</tr>
<tr class="even">
<td><p><code>MessageType</code></p></td>
<td><p>Valor de tipo de mensagem única</p></td>
<td><p>Especifica um dos seguintes tipos de mensagem:</p>
<ul>
<li><p><strong>Resposta automática</strong> (<code>OOF</code>)</p></li>
<li><p><strong>Encaminhar automaticamente</strong> (<code>AutoForward</code>)</p></li>
<li><p><strong>Criptografadas</strong></p></li>
<li><p><strong>Calendário</strong></p></li>
<li><p><strong>Permissão controlada</strong> (<code>PermissionControlled</code>)</p></li>
<li><p><strong>Caixa postal</strong></p></li>
<li><p><strong>Assinado</strong></p></li>
<li><p><strong>Solicitação de aprovação</strong> (<code>ApprovalRequest</code>)</p></li>
<li><p><strong>Confirmação de leitura</strong> (<code>ReadReceipt</code>)</p></li>
</ul>

> [!TIP]
> Quando Outlook ou Outlook Web App estiver configurada para encaminhar uma mensagem, a propriedade <STRONG>ForwardingSmtpAddress</STRONG> é adicionada à mensagem. O tipo de mensagem não é alterado para <CODE>AutoForward</CODE>.


</td>
</tr>
<tr class="odd">
<td><p><code>Patterns</code></p></td>
<td><p>Matriz de expressões regulares</p></td>
<td><p>Especifica um ou mais expressões regulares que são usadas para identificar padrões de texto em valores. Para obter mais informações, consulte <a href="https://go.microsoft.com/fwlink/p/?linkid=180327">Sintaxe de expressão Regular</a>.</p>
<p>No Shell de Gerenciamento do Exchange, você especificar várias expressões regulares, separadas por vírgulas, e você coloque cada expressão regular aspas (&quot;).</p></td>
</tr>
<tr class="even">
<td><p><code>SCLValue</code></p></td>
<td><p>Um dos seguintes valores:</p>
<ul>
<li><p><strong>Ignorar filtragem de spam</strong> (<code>-1</code>)</p></li>
<li><p>Números inteiros de 0 a 9</p></li>
</ul></td>
<td><p>Especifica o nível de confiança de spam (SCL) que é atribuído a uma mensagem. Um valor SCL superior indica que uma mensagem é mais provável de ser spam.</p></td>
</tr>
<tr class="odd">
<td><p><code>SensitiveInformationTypes</code></p></td>
<td><p>Matriz de tipos de informações confidenciais</p></td>
<td><p>Especifica um ou mais tipos de informações confidenciais que são definidos na sua organização. Para obter uma lista dos tipos de informações confidenciais internas, consulte <a href="what-the-sensitive-information-types-in-exchange-look-for-exchange-online-help.md">O que os tipos de informações confidenciais no Exchange procurar</a>.</p>
<p>No Shell de Gerenciamento do Exchange, use a sintaxe <code>@{&lt;SensitiveInformationType1&gt;},@{&lt;SensitiveInformationType2&gt;},...</code>. Por exemplo, para procurar por conteúdo que contenha pelo menos dois números de cartão de crédito e pelo menos um número de roteamento ABA, use o valor <code>@{Name=&quot;Credit Card Number&quot;; minCount=&quot;2&quot;},@{Name=&quot;ABA Routing Number&quot;; minCount=&quot;1&quot;}</code>.</p></td>
</tr>
<tr class="even">
<td><p><code>Size</code></p></td>
<td><p>Valor único de tamanho</p></td>
<td><p>Especifica o tamanho de um anexo ou toda a mensagem.</p>
<p>No EAC, você só pode especificar o tamanho em kilobytes (KB).</p>
<p>No Shell de Gerenciamento do Exchange, quando você inserir um valor, qualifique-o valor com uma das seguintes unidades:</p>
<ul>
<li><p><code>B</code> (bytes)</p></li>
<li><p><code>KB</code> (quilobytes)</p></li>
<li><p><code>MB</code> (megabytes)</p></li>
<li><p><code>GB</code> (gigabytes)</p></li>
</ul>
<p>Por exemplo, <code>20MB</code></p>
<p>Geralmente, os valores não qualificados são tratados como bytes, mas valores menores podem ser arredondados para o quilobyte mais próximo.</p></td>
</tr>
<tr class="odd">
<td><p><code>UserScopeFrom</code></p></td>
<td><p>Valor único de <strong>dentro da organização</strong> (<code>InOrganization</code>) ou de <strong>fora da organização</strong> (<code>NotInOrganization</code>)</p></td>
<td><p>Um remetente é considerado como estando dentro da organização se uma das seguintes condições for verdadeira:</p>
<ul>
<li><p>O remetente é uma caixa de correio, usuário de email, grupo ou pasta pública habilitada para email que existe no Active Directory da organização.</p></li>
<li><p>Endereço de email do remetente está em um domínio aceito que esteja configurado como um domínio autoritativo ou um domínio de retransmissão interna, <strong>e</strong> a mensagem foi enviada ou recebida por uma conexão autenticada. Para obter mais informações sobre domínios aceitos, consulte <a href="accepted-domains-exchange-2013-help.md">Domínios aceitos</a>.</p></li>
</ul>
<p>Um remetente é considerado como fora da organização se uma das seguintes condições for verdadeira:</p>
<ul>
<li><p>Endereço de email do remetente não estiver em um domínio aceito.</p></li>
<li><p>Endereço de email do remetente está em um domínio aceito que esteja configurado como um domínio de retransmissão externo.</p></li>
</ul>

> [!TIP]
> Para determinar se os contatos de email são considerados como estando dentro ou fora da organização, o endereço do remetente é comparado com os domínios aceitos da organização.


</td>
</tr>
<tr class="even">
<td><p><code>UserScopeTo</code></p></td>
<td><p>Um dos seguintes valores:</p>
<ul>
<li><p><strong>Dentro da organização</strong> (<code>InOrganization</code>)</p></li>
<li><p><strong>Fora da organização</strong> (<code>NotInOrganization</code>)</p></li>
<li><p><strong>Em uma organização de parceiro externo</strong> (<code>ExternalPartner</code>)</p></li>
<li><p><strong>Em uma organização de não-parceiros externa</strong> (<code>ExternalNonPartner</code>)</p></li>
</ul></td>
<td><p>Um destinatário é considerado como estando dentro da organização se uma das seguintes condições for verdadeira:</p>
<ul>
<li><p>O destinatário é uma caixa de correio, usuário de email, grupo ou pasta pública habilitada para email que existe no Active Directory da organização.</p></li>
<li><p>Endereço de email do destinatário está em um domínio aceito que esteja configurado como um domínio autoritativo ou um domínio de retransmissão interna, <strong>e</strong> a mensagem foi enviada ou recebida por uma conexão autenticada.</p></li>
</ul>
<p>Um destinatário é considerado como fora da organização se uma das seguintes condições for verdadeira:</p>
<ul>
<li><p>Endereço de email do destinatário não estiver em um domínio aceito.</p></li>
<li><p>Endereço de email do destinatário está em um domínio aceito que esteja configurado como um domínio de retransmissão externo.</p></li>
</ul>
<p>As organizações parceiras externos são onde você configurou a segurança de domínio (autenticação de TLS mútua) para enviar email de domínios externos.</p>
<p>Organizações externas de parceiro não são todos os outros domínios externos que não são considerados domínios de parceiros.</p></td>
</tr>
<tr class="odd">
<td><p><code>Words</code></p></td>
<td><p>Matriz de cadeias de caracteres</p></td>
<td><p>Especifica uma ou mais palavras para procurar. As palavras não diferencia maiusculas de minúsculas e podem ser circundadas por marcas de pontuação e espaços. Caracteres curinga e correspondências parciais não são suportadas.</p>
<p>Por exemplo, &quot;contoso&quot; corresponde a &quot;Contoso&quot;. No entanto, se o texto está rodeado por outros caracteres, ele não é considerado uma correspondência. Por exemplo, &quot;contoso&quot; não coincidem com os seguintes valores:</p>
<ul>
<li><p>Acontoso</p></li>
<li><p>Contosoa</p></li>
<li><p>Acontosob</p></li>
</ul>
<p>O asterisco (*) é tratado como um caractere literal e não é usado como um caractere curinga.</p></td>
</tr>
</tbody>
</table>


Voltar ao início

## Para saber mais

[Regras de fluxo de emails ou de transporte](mail-flow-rules-transport-rules-in-exchange-2013-exchange-2013-help.md)

[Ações de regra de transporte](mail-flow-rule-actions-in-exchange-2013-exchange-2013-help.md)

[Procedimentos de regra de transporte ou de fluxo de email](mail-flow-or-transport-rule-procedures-exchange-2013-help.md)

[Exceções (predicados) e condições de regra de fluxo de email no Exchange Online](https://technet.microsoft.com/pt-br/library/jj919235\(v=exchg.150\)) para Exchange Online

[Condições de regra de fluxo e email exceções (predicados) no Exchange Online Protection](https://technet.microsoft.com/pt-br/library/jj919234\(v=exchg.150\)) para Proteção do Exchange Online

