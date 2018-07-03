---
title: 'Avisos de isenção de responsabilidade, assinaturas, rodapés ou cabeçalhos para toda a organização: Exchange 2013 Help'
TOCTitle: Avisos de isenção de responsabilidade, assinaturas, rodapés ou cabeçalhos para toda a organização
ms:assetid: e45e33c9-e53b-427c-ada5-70901bc399b8
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Dn600437(v=EXCHG.150)
ms:contentKeyID: 61060506
ms.date: 01/10/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Avisos de isenção de responsabilidade, assinaturas, rodapés ou cabeçalhos para toda a organização

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2015-03-09_

Você pode adicionar um aviso de isenção de responsabilidade, aviso de isenção legal, declaração, assinatura ou outras informações à parte superior ou inferior das mensagens de email que entram ou saem de sua organização. Isso pode ser necessária por motivos jurídicos, comerciais ou regulamentares, a fim de identificar mensagens de email possivelmente inseguras, ou por outros motivos exclusivos de sua organização.

Para configurar um aviso de isenção de responsabilidade, crie uma regra de transporte que contenha as condições, como quando o remetente estiver em um grupo específico ou quando a mensagem contiver padrões de texto específicos, e o texto a ser adicionado. Para aplicar vários avisos de isenção a uma única mensagem de email, use várias regras de transporte.


> [!IMPORTANT]
> <UL>
> <LI>
> <P>Se quiser que as informações sejam adicionadas somente às mensagens de saída, adicione uma condição, como destinatários localizados fora da organização. Por padrão, as regras de transporte são aplicadas às mensagens de entrada e de saída.</P></LI></UL>



**Sumário**

Exemplos

Escopo de seu aviso de isenção de responsabilidade

Formatar seu aviso de isenção de responsabilidade

Opções alternativas caso o aviso de isenção de responsabilidade não possa ser adicionado

Para saber mais

Procurando procedimentos? Consulte [Avisos de isenção de mensagem em toda a organização, assinaturas, rodapés ou cabeçalhos no Office 365](https://technet.microsoft.com/pt-br/library/dn600323\(v=exchg.150\)).

## Exemplos

Eis algumas ideias de como usar os avisos de isenção de responsabilidade.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Tipo</th>
<th>Exemplo de texto adicionado</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Jurídico: mensagens de saída</p></td>
<td><p>Esse email e quaisquer arquivos transmitidos com ele são confidenciais e destinados exclusivamente para uso pelo indivíduo ou pela entidade a quem estão endereçados. Se você recebeu este email por engano, notifique o administrador do sistema.</p></td>
</tr>
<tr class="even">
<td><p>Jurídico: mensagens de entrada</p></td>
<td><p>Os funcionários são expressamente obrigados a não fazer declarações difamatórias e não violar ou autorizar qualquer violação de direitos autorais ou qualquer outro direito legal por meio de comunicações por email. Os funcionários que receberem tais emails devem notificar seu supervisor imediatamente.</p></td>
</tr>
<tr class="odd">
<td><p>Observe que essa mensagem foi enviada para um alias</p></td>
<td><p>Essa mensagem foi enviada para o grupo Discussão de vendas.</p></td>
</tr>
<tr class="even">
<td><p>Assinatura: obter dados de cada funcionário</p></td>
<td><p>Lara Cardoso<br />
Departamento de vendas<br />
Contoso<br />
www.contoso.com<br />
lara@contoso.com<br />
celular: 11-9-2222-1234</p></td>
</tr>
<tr class="odd">
<td><p>Anúncio</p></td>
<td><p>Clique aqui para ver as promoções especiais de março</p></td>
</tr>
</tbody>
</table>


Os exemplos neste artigo não são destinados para uso como estão. Altere-os de acordo com suas necessidades.

## Escopo de seu aviso de isenção de responsabilidade

Ao trabalhar nas isenções de responsabilidade, considere a quais mensagens elas devem ser aplicadas. Por exemplo, você pode querer avisos de isenção de responsabilidade diferentes para mensagens internas e externas, ou para mensagens enviadas por usuários em determinados departamentos. Para garantir que apenas a primeira mensagem em uma conversa receba um aviso de isenção de responsabilidade, adicione uma exceção que procura por um texto exclusivo no seu aviso de isenção de responsabilidade.

Eis alguns exemplos de condições e exceções que você pode usar.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Descrição</th>
<th>Condições e exceções no EAC</th>
<th>Condições e exceções no Shell</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Fora de sua organização, se a mensagem original não incluir o texto de isenção de responsabilidade, como &quot;AVISO LEGAL DA CONTOSO&quot;</p></td>
<td><p>Condição: <strong>O destinatário está localizado em</strong> &gt; <strong>Fora da organização</strong></p>
<p>Exceção: <strong>Assunto ou corpo da mensagem</strong> &gt; <strong>o assunto ou corpo corresponde a estes padrões de texto</strong> &gt; <strong>AVISO LEGAL DA CONTOSO</strong></p></td>
<td><pre><code>-FromScope NotInOrganization -ExceptIf -SubjectOrBodyMatches &quot;CONTOSO LEGAL NOTICE&quot;</code></pre></td>
</tr>
<tr class="even">
<td><p>Mensagens de entrada com anexos executáveis</p></td>
<td><p>Condição 1: <strong>O remetente está localizado em</strong> &gt; <strong>Fora da organização</strong></p>
<p>Condição 2: <strong>Qualquer anexo</strong> &gt; <strong>possui conteúdo executável</strong></p></td>
<td><pre><code>-FromScope NotInOrganization -AttachmentHasExecutableContent</code></pre></td>
</tr>
<tr class="odd">
<td><p>O remetente faz parte do departamento de Marketing</p></td>
<td><p>Condição: <strong>O remetente</strong> &gt; <strong>é um membro deste grupo</strong> &gt; <strong>nome do grupo</strong></p></td>
<td><pre><code>-FromMemberOf &quot;Marketing Team&quot;</code></pre></td>
</tr>
<tr class="even">
<td><p>Todas as mensagens que vêm de um remetente externo para o grupo Discussão de vendas</p></td>
<td><p>Condição 1: <strong>O remetente está localizado em</strong> &gt; <strong>Fora da organização</strong></p>
<p>Condição 2: <strong>A mensagem</strong> &gt; <strong>A caixa Para ou Cc contém essa pessoa</strong> &gt; <strong>nome do grupo</strong></p></td>
<td><pre><code>-FromScope NotInOrganization -SentTo &quot;Sales Discussion Group&quot; -PrependSubject &quot;Sent to Sales Discussion Group: &quot;</code></pre></td>
</tr>
<tr class="odd">
<td><p>Preceder com um anúncio para mensagens enviadas por um mês</p></td>
<td><p>Condição 1: <strong>O destinatário está localizado em</strong> &gt; <strong>Fora da organização</strong></p>
<p>Especifique as datas na parte inferior da caixa de diálogo <strong>Nova regra</strong>.</p></td>
<td><p>-ApplyHtmlDisclaimerLocation 'Prepend' -SentToScope 'NotInOrganization' –ActivationDate ‘03/1/2014’ –ExpiryDate ‘03/31/2014’</p></td>
</tr>
</tbody>
</table>


Para obter uma lista completa de condições de regra de transporte que você pode usar para avisos de isenção de responsabilidade, confira um destes procedimentos:

  - [Exceções (predicados) e condições de regra de fluxo de email no Exchange Online](https://technet.microsoft.com/pt-br/library/jj919235\(v=exchg.150\)) (Exchange Online)

  - [Condições de regra de transporte (predicados)](mail-flow-rule-conditions-and-exceptions-predicates-in-exchange-2013-exchange-2013-help.md) (Exchange 2013)

  - [Exceções (predicados) e condições de regra de fluxo de email no Exchange Online](https://technet.microsoft.com/pt-br/library/jj919235\(v=exchg.150\)) (Exchange Online Protection)

## Formatar seu aviso de isenção de responsabilidade

Você pode formatar seu aviso de isenção de responsabilidade conforme necessário. Eis o que pode ser incluído no seu texto de isenção de responsabilidade.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Tipo de informação</th>
<th>Descrição</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Texto</p></td>
<td><p>O comprimento máximo é de 5.000 caracteres, incluindo as marcas HTML e folhas de estilos em cascata (CSS) embutidas.</p></td>
</tr>
<tr class="even">
<td><p>HTML e CSS inline</p></td>
<td><p>Você pode usar HTML e estilos CSS inline para formatar o texto. Por exemplo, use a marca <code>&lt;HR&gt;</code> para adicionar uma linha antes da isenção de responsabilidade.</p>
<p>HTML em um aviso de isenção de responsabilidade é ignorado se o aviso de isenção de responsabilidade for adicionado a uma mensagem de texto sem formatação.</p></td>
</tr>
<tr class="odd">
<td><p>Adicionar imagens</p></td>
<td><p>Use a marca <code>&lt;IMG&gt;</code> para apontar para uma imagem disponível na Internet. Por exemplo, <code>&lt;IMG src=&quot;http://contoso.com/images/companylogo.gif&quot; alt=&quot;Contoso logo&quot;&gt;</code></p>
<p>Lembre-se que o Outlook Web App e o Outlook bloqueiam conteúdo Web externo (incluindo imagens) por padrão. Os usuários podem precisar executar uma ação específica se quiserem visualizar o conteúdo externo bloqueado. Portanto, imagens adicionadas a avisos de isenção em HTML que usam a marca <code>IMG</code> podem não ser visíveis por padrão. É recomendável que você teste os avisos de isenção com marcas <code>IMG</code> nos clientes de email que seus destinatários provavelmente usarão para garantir que sejam exibidas.</p></td>
</tr>
<tr class="even">
<td><p>Adicionar informações a assinaturas personalizadas</p></td>
<td><p>Se quiser que todos tenham assinaturas formatados da mesma maneira com as mesmas informações, adicione informações exclusivas para cada funcionário, tais como <code>DisplayName</code>, <code>FirstName</code>, <code>LastName</code>, <code>PhoneNumber</code>, <code>Email</code>, <code>FaxNumber</code> e <code>Department</code>. Essas informações devem ser colocadas entre sinais de porcentagem (%), dois de cada lado da informação. Por exemplo, para usar <code>DisplayName</code>, você deve usar <strong>%%DisplayName%%</strong> no seu aviso de isenção de responsabilidade.</p>
<p>Quando uma regra de isenção de responsabilidade é acionada, os valores correspondentes para esse usuário são inseridos. Os dados vêm da conta de usuário do Active Directory do remetente (para o servidor do Exchange no local) ou da conta do Office 365 do remetente para o Exchange Online.</p>
<p>Para obter uma lista completa dos atributos que podem ser usados em aviso de isenção de responsabilidade e assinaturas personalizadas, confira a descrição da propriedade <code>ADAttribute</code> no <a href="mail-flow-rule-conditions-and-exceptions-predicates-in-exchange-2013-exchange-2013-help.md">Condições de regra de transporte (predicados)</a> (Exchange Server), no <a href="https://technet.microsoft.com/pt-br/library/jj919235(v=exchg.150)">Exceções (predicados) e condições de regra de fluxo de email no Exchange Online</a> (Exchange Online) ou no <a href="https://technet.microsoft.com/pt-br/library/jj919234(v=exchg.150)">Condições de regra de fluxo e email exceções (predicados) no Exchange Online Protection</a> (Exchange Online Protection).</p></td>
</tr>
</tbody>
</table>


Por exemplo, eis um exemplo de um aviso de isenção de responsabilidade em HTML que inclui uma assinatura, uma marca `IMG` e CSS incorporada.

    <div style="font-size:9pt;  font-family: 'Calibri',sans-serif;">
    %%displayname%%</br>
    %%title%%</br>
    %%company%%</br>
    %%street%%</br>
    %%city%%, %%state%% %%zipcode%%</div>
    &nbsp;</br>
    <div style="background-color:#D5EAFF; border:1px dotted #003333; padding:.8em; ">
    <div><img alt="Fabrikam"  src="http://fabrikam.com/images/fabrikamlogo.png"></div>
    <span style="font-size:12pt;  font-family: 'Cambria','times new roman','garamond',serif; color:#ff0000;">HTML Disclaimer Title</span></br>
    <p style="font-size:8pt; line-height:10pt; font-family: 'Cambria','times roman',serif;">This message contains confidential information and is intended only for the individual(s) addressed in the message. If you are not the named addressee, you should not disseminate, distribute, or copy this e-mail. If you are not the intended recipient, you are notified that disclosing, distributing, or copying this e-mail is strictly prohibited.  </p>
    <span style="padding-top:10px; font-weight:bold; color:#CC0000; font-size:10pt; font-family: 'Calibri',Arial,sans-serif; "><a href="http://www.fabrikam.com">Fabrikam, Inc. </a></span></br></br>
    </div>

## Opções alternativas caso o aviso de isenção de responsabilidade não possa ser adicionado

Algumas mensagens, como mensagens criptografadas, impedem que o Exchange altere o conteúdo da mensagem original. Você pode controlar como a organização lida com essas mensagens. Especifique se deseja encapsular uma mensagem que não pode ser alterada em um envelope de mensagem que contenha o aviso de isenção de responsabilidade, rejeitar a mensagem se o aviso não puder ser adicionado ou ignorar a ação do aviso de isenção de responsabilidade e entregar a mensagem sem ele.

A lista a seguir descreve cada ação alternativa:

  - **Encapsular**   Se o aviso de isenção de responsabilidade não puder ser inserido na mensagem original, o Exchange incluirá, ou "encapsulará", a mensagem original em um novo envelope de mensagem. Em seguida, o aviso de isenção de responsabilidade será inserido na nova mensagem. Se a mensagem original não puder ser encapsulada em um novo envelope de mensagem, a mensagem original não será entregue. O remetente da mensagem receberá uma notificação de falha na entrega que explicará porquê a mensagem não foi entregue.
    

    > [!IMPORTANT]
    > Se uma mensagem original for encapsulada em um novo envelope de mensagem, as regras de transporte subsequentes serão aplicadas ao novo envelope de mensagem, e não à mensagem original. Portanto, você deve configurar regras de transporte com ações de aviso de isenção que encapsulam as mensagens originais em um novo corpo de mensagem após a configuração de outras regras de transporte.



  - **Rejeitar**   Se o aviso de isenção de responsabilidade não puder ser inserido na mensagem original, o Exchange não entregará a mensagem. O remetente da mensagem receberá uma notificação de falha na entrega que explicará porquê a mensagem não foi entregue.

  - **Ignorar**   Se o aviso de isenção de responsabilidade não puder ser inserido na mensagem original, o Exchange entrega a mensagem original inalterada. Nenhum aviso de isenção de responsabilidade é adicionado.

## Para saber mais

[Avisos de isenção de mensagem em toda a organização, assinaturas, rodapés ou cabeçalhos no Office 365](https://technet.microsoft.com/pt-br/library/dn600323\(v=exchg.150\))

[Regras de fluxo de emails ou de transporte](mail-flow-rules-transport-rules-in-exchange-2013-exchange-2013-help.md) (Exchange Server 2013)

[Regras de fluxo de emails (regras de transporte) no Exchange Online](https://technet.microsoft.com/pt-br/library/jj919238\(v=exchg.150\)) (Exchange Online)

[Regras de fluxo de emails (regras de transporte) no Exchange Online Protection](https://technet.microsoft.com/pt-br/library/dn271424\(v=exchg.150\)) (Exchange Online Protection)

