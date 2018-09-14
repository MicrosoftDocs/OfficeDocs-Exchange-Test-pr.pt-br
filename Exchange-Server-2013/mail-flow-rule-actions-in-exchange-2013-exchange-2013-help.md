---
title: 'Ações de regra de transporte: Exchange 2013 Help'
TOCTitle: Ações de regra de fluxo de email
ms:assetid: 5d11a955-b1cc-4150-a0b9-a8cc48ba9bde
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Aa998315(v=EXCHG.150)
ms:contentKeyID: 50485693
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Ações de regra de transporte

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2017-05-03_

Ações de regras de fluxo de correio (também conhecido como regras de transporte) especificam o que você deseja fazer a mensagens que correspondam às condições da regra. Por exemplo, você pode criar uma regra que encaminha as mensagens de remetentes específicos para um moderador ou adiciona um aviso de isenção ou personalizadas de assinatura a todas as mensagens de saída.

Ações normalmente exigem propriedades adicionais. Por exemplo, quando a regra redireciona uma mensagem, você precisará especificar onde redirecionar a mensagem. Algumas ações têm várias propriedades que estão disponíveis ou necessário. Por exemplo, quando a regra adiciona um campo de cabeçalho ao cabeçalho da mensagem, você precisará especificar o nome e o valor do cabeçalho. Quando a regra adiciona um aviso de isenção às mensagens, é preciso especificar o texto de isenção de responsabilidade, mas você também pode especificar onde inserir o texto ou o que fazer se a isenção de responsabilidade não pode ser adicionada à mensagem. Normalmente, você pode configurar várias ações em uma regra, mas algumas ações são exclusivas. Por exemplo, uma regra não é possível rejeitar e redirecionar a mesma mensagem.

Para obter mais informações sobre regras de fluxo de email no Exchange Server 2013, consulte [Regras de fluxo de emails ou de transporte](mail-flow-rules-transport-rules-in-exchange-2013-exchange-2013-help.md).

Para obter mais informações sobre condições e exceções em regras de fluxo de email, consulte [Condições de regra de transporte (predicados)](mail-flow-rule-conditions-and-exceptions-predicates-in-exchange-2013-exchange-2013-help.md).

Para obter mais informações sobre ações de regras de fluxo de correio em Exchange Online ou Proteção do Exchange Online, consulte [Email ações de regra de fluxo no Exchange Online](https://technet.microsoft.com/pt-br/library/jj919237\(v=exchg.150\)) ou [De email ações de regra de fluxo no Exchange Online Protection](https://technet.microsoft.com/pt-br/library/jj920117\(v=exchg.150\)).

## Ações de regras de fluxo de correio em servidores de caixa de correio

As ações que estão disponíveis em regras de fluxo de correio em servidores de caixa de correio são descritas na tabela a seguir. Os valores válidos para cada propriedade são descritos na seção valores de propriedade .

**Observações**:

  - Depois de selecionar uma ação na Centro de administração do Exchange (EAC), o valor que basicamente é mostrado no campo **fazer o seguinte** é geralmente diferente do caminho click selecionada. Além disso, quando você cria novas regras, você pode às vezes (dependendo das seleções feitas) selecione um nome curto de ação de um modelo (uma lista filtrada de ações), em vez de seguindo o caminho completo click. Os nomes curtos e completo, clique em caminho valores são mostrados na coluna EAT na tabela.

  - Os nomes de algumas das ações que são retornadas pelo cmdlet **Get-TransportRuleAction** são diferentes dos nomes de parâmetro correspondente e vários parâmetros podem ser necessários para uma ação.


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
<th>Ação no EAC</th>
<th>Parâmetro de ação na Shell de Gerenciamento do Exchange</th>
<th>Propriedade</th>
<th>Descrição</th>
<th>Disponível em</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>Encaminhar a mensagem para aprovação para essas pessoas</strong></p>
<p><strong>Encaminhar a mensagem para aprovação</strong> &gt; <strong>para que essas pessoas</strong></p></td>
<td><p><em>ModerateMessageByUser</em></p></td>
<td><p><code>Addresses</code></p></td>
<td><p>Encaminhe a mensagem para os moderadores especificados como um anexo em uma solicitação de aprovação. Para obter mais informações, consulte <a href="https://docs.microsoft.com/pt-br/exchange/security-and-compliance/mail-flow-rules/common-message-approval-scenarios">Cenários comuns de aprovação de mensagem</a>. Você não pode usar um grupo de distribuição como um moderador.</p></td>
<td><p>Exchange 2010 ou posterior</p></td>
</tr>
<tr class="even">
<td><p><strong>Encaminhar a mensagem para aprovação para o gerente do remetente</strong></p>
<p><strong>Encaminhar a mensagem para aprovação</strong> &gt; <strong>ao gerente do remetente</strong></p></td>
<td><p><em>ModerateMessageByManager</em></p></td>
<td><p>n/d</p></td>
<td><p>Encaminhe a mensagem ao gerente do remetente para aprovação.</p>
<p>Essa ação só funciona se o atributo do remetente <strong>Manager</strong> é definido em Active Directory. Caso contrário, a mensagem é entregue aos destinatários sem moderação.</p></td>
<td><p>Exchange 2010 ou posterior</p></td>
</tr>
<tr class="odd">
<td><p><strong>Redirecionar a mensagem para esses destinatários</strong></p>
<p><strong>Redirecionar a mensagem</strong> &gt; <strong>esses destinatários</strong></p></td>
<td><p><em>RedirectMessageTo</em></p></td>
<td><p><code>Addresses</code></p></td>
<td><p>Redireciona a mensagem para os destinatários especificados. A mensagem não entregue aos destinatários originais e nenhuma notificação é enviada para o remetente ou destinatários originais.</p></td>
<td><p>Exchange 2007 ou posterior</p></td>
</tr>
<tr class="even">
<td><p><strong>Rejeitar a mensagem com a explicação</strong></p>
<p><strong>Bloquear a mensagem</strong> &gt; <strong>Rejeitar a mensagem e incluir uma explicação</strong></p></td>
<td><p><em>RejectMessageReasonText</em></p></td>
<td><p><code>String</code></p></td>
<td><p>Retorna a mensagem ao remetente em um relatório de falha na entrega (também conhecido como uma mensagem de notificação de falha na ou rejeição) com o texto especificado como o motivo de rejeição. O destinatário não receber a mensagem original ou a notificação.</p>
<p>O código de status avançado de padrão usada é <code>5.7.1</code>.</p>
<p>Quando você cria ou modificar a regra na Shell de Gerenciamento do Exchange, você pode especificar o código DSN usando o parâmetro <em>RejectMessageEnhancedStatusCode</em> .</p></td>
<td><p>Exchange 2007 ou posterior</p></td>
</tr>
<tr class="odd">
<td><p><strong>Rejeitar a mensagem com o código de status avançado</strong></p>
<p><strong>Bloquear a mensagem</strong> &gt; <strong>Rejeitar a mensagem com o código de status avançado</strong></p></td>
<td><p><em>RejectMessageEnhancedStatusCode</em></p></td>
<td><p><code>DSNEnhancedStatusCode</code></p></td>
<td><p>Retorna a mensagem ao remetente em uma NDR com o código de notificação (DSN) de status aprimorado de entrega especificado. O destinatário não receber a mensagem original ou a notificação.</p>
<p>Códigos DSN válidos são <code>5.7.1</code> ou <code>5.7.900</code> por meio de <code>5.7.999</code>.</p>
<p>O texto padrão de razão que é usado é <code>Delivery not authorized, message refused</code>.</p>
<p>Quando você cria ou modificar a regra no Shell de Gerenciamento do Exchange, você pode especificar o texto do motivo de rejeição, usando o parâmetro <em>RejectMessageReasonText</em> .</p></td>
<td><p>Exchange 2007 ou posterior</p></td>
</tr>
<tr class="even">
<td><p><strong>Excluir a mensagem sem notificar ninguém</strong></p>
<p><strong>Bloquear a mensagem</strong> &gt; <strong>Excluir a mensagem sem notificar ninguém</strong></p></td>
<td><p><em>DeleteMessage</em></p></td>
<td><p>n/d</p></td>
<td><p>Descarta silenciosamente a mensagem sem enviar a notificação para o destinatário ou o remetente.</p></td>
<td><p>Exchange 2007 ou posterior</p></td>
</tr>
<tr class="odd">
<td><p><strong>Adicionar destinatários à caixa Cco</strong></p>
<p><strong>Adicionar destinatários</strong> &gt; <strong>à caixa Cco</strong></p></td>
<td><p><em>BlindCopyTo</em></p></td>
<td><p><code>Addresses</code></p></td>
<td><p>Adiciona um ou mais destinatários ao campo <strong>Bcc</strong> da mensagem. Os destinatários originais não são notificados e eles não podem ver os endereços adicionais.</p></td>
<td><p>Exchange 2007 ou posterior</p></td>
</tr>
<tr class="even">
<td><p><strong>Adicionar destinatários à caixa Para</strong></p>
<p><strong>Adicionar destinatários</strong> &gt; <strong>à caixa</strong></p></td>
<td><p><em>AddToRecipients</em></p></td>
<td><p><code>Addresses</code></p></td>
<td><p>Adiciona um ou mais destinatários ao campo <strong>To</strong> da mensagem. Os destinatários originais podem ver os endereços adicionais.</p></td>
<td><p>Exchange 2007 ou posterior</p></td>
</tr>
<tr class="odd">
<td><p><strong>Adicionar destinatários à caixa Cc</strong></p>
<p><strong>Adicionar destinatários</strong> &gt; <strong>à caixa Cc</strong></p></td>
<td><p><em>CopyTo</em></p></td>
<td><p><code>Addresses</code></p></td>
<td><p>Adiciona um ou mais destinatários ao campo <strong>Cc</strong> da mensagem. Os destinatários originais podem ver o endereço adicional.</p></td>
<td><p>Exchange 2007 ou posterior</p></td>
</tr>
<tr class="even">
<td><p><strong>Adicionar o gerente do remetente como um destinatário</strong></p>
<p><strong>Adicionar destinatários</strong> &gt; <strong>Adicionar o gerente do remetente como um destinatário</strong></p></td>
<td><p><em>AddManagerAsRecipientType</em></p></td>
<td><p><code>AddedManagerAction</code></p></td>
<td><p>Adiciona o gerente do remetente à mensagem como o tipo de destinatário especificado (<strong>To</strong>, <strong>Cc</strong>, <strong>Bcc</strong>) ou redireciona a mensagem para o gerente do remetente sem notificar o remetente ou destinatário.</p>
<p>Essa ação só funciona se o atributo do remetente <strong>Manager</strong> é definido no Active Directory.</p></td>
<td><p>Exchange 2010 ou posterior</p></td>
</tr>
<tr class="odd">
<td><p><strong>Acrescentar o aviso de isenção de responsabilidade</strong></p>
<p><strong>Aplicar um aviso de isenção à mensagem</strong> &gt; <strong>acrescentar um aviso de isenção</strong></p></td>
<td><p><em>ApplyHtmlDisclaimerText</em></p>
<p><em>ApplyHtmlDisclaimerFallbackAction</em></p>
<p><em>ApplyHtmlDisclaimerTextLocation</em></p></td>
<td><p>Primeira propriedade: <code>DisclaimerText</code></p>
<p>Segunda propriedade: <code>DisclaimerFallbackAction</code></p>
<p>Propriedade terceira (somenteShell de Gerenciamento do Exchange ): <code>DisclaimerTextLocation</code></p></td>
<td><p>Aplica a isenção de responsabilidade HTML especificada até o final da mensagem.</p>
<p>Quando você cria ou modificar a regra na Shell de Gerenciamento do Exchange, use o parâmetro <em>ApplyHtmlDisclaimerTextLocation</em> com o valor <code>Append</code>.</p></td>
<td><p>Exchange 2007 ou posterior</p></td>
</tr>
<tr class="even">
<td><p><strong>Preceder o aviso de isenção de responsabilidade</strong></p>
<p><strong>Aplicar um aviso de isenção à mensagem</strong> &gt; <strong>preceda um aviso de isenção</strong></p></td>
<td><p><em>ApplyHtmlDisclaimerText</em></p>
<p><em>ApplyHtmlDisclaimerFallbackAction</em></p>
<p><em>ApplyHtmlDisclaimerTextLocation</em></p></td>
<td><p>Primeira propriedade: <code>DisclaimerText</code></p>
<p>Segunda propriedade: <code>DisclaimerFallbackAction</code></p>
<p>Propriedade terceira (somenteShell de Gerenciamento do Exchange ): <code>DisclaimerTextLocation</code></p></td>
<td><p>Aplica a isenção de responsabilidade HTML especificada para o início da mensagem.</p>
<p>Quando você cria ou modificar a regra no Shell de Gerenciamento do Exchange, use o parâmetro <em>ApplyHtmlDisclaimerTextLocation</em> com o valor <code>Prepend</code>.</p>
<p></p></td>
<td><p>Exchange 2007 ou posterior</p></td>
</tr>
<tr class="odd">
<td><p><strong>Remover este cabeçalho</strong></p>
<p><strong>Modificar as propriedades da mensagem</strong> &gt; <strong>Remover o cabeçalho da mensagem</strong></p></td>
<td><p><em>RemoveHeader</em></p></td>
<td><p><code>MessageHeaderField</code></p></td>
<td><p>Remove o campo de cabeçalho especificado do cabeçalho da mensagem.</p></td>
<td><p>Exchange 2007 ou posterior</p></td>
</tr>
<tr class="even">
<td><p><strong>Definir o cabeçalho da mensagem como este valor</strong></p>
<p><strong>Modificar as propriedades da mensagem</strong> &gt; <strong>definir o cabeçalho da mensagem</strong></p></td>
<td><p><em>SetHeaderName</em></p>
<p><em>SetHeaderValue</em></p></td>
<td><p>Primeira propriedade: <code>MessageHeaderField</code></p>
<p>Segunda propriedade: <code>String</code></p></td>
<td><p>Adiciona ou modifica o campo de cabeçalho especificado no cabeçalho da mensagem e define o campo de cabeçalho ao valor especificado.</p></td>
<td><p>Exchange 2007 ou posterior</p></td>
</tr>
<tr class="odd">
<td><p><strong>Aplicar uma classificação de mensagem</strong></p>
<p><strong>Modificar as propriedades da mensagem</strong> &gt; <strong>Aplicar uma classificação de mensagem</strong></p></td>
<td><p><em>ApplyClassification</em></p></td>
<td><p><code>MessageClassification</code></p></td>
<td><p>Aplica a classificação de mensagem especificado na mensagem.</p></td>
<td><p>Exchange 2007 ou posterior</p></td>
</tr>
<tr class="even">
<td><p><strong>Definir o nível de confiança de spam (SCL)</strong></p>
<p><strong>Modificar as propriedades da mensagem</strong> &gt; <strong>definir o nível de confiança de spam (SCL)</strong></p></td>
<td><p><em>SetSCL</em></p></td>
<td><p><code>SCLValue</code></p></td>
<td><p>Define o nível de confiança de spam (SCL) da mensagem para o valor especificado.</p></td>
<td><p>Exchange 2007 ou posterior</p></td>
</tr>
<tr class="odd">
<td><p><strong>Aplicar proteção de direito à mensagem com</strong></p>
<p><strong>Modificar a segurança da mensagem</strong> &gt; <strong>Aplicar proteção de direitos</strong></p></td>
<td><p><em>ApplyRightsProtectionTemplate</em></p></td>
<td><p><code>RMSTemplate</code></p></td>
<td><p>Aplica o modelo de Rights Management Services (RMS) na mensagem.</p>
<p>RMS exige licenças de acesso para cliente Enterprise Exchange (CALs) para cada caixa de correio. Para obter mais informações sobre CALs, consulte <a href="https://go.microsoft.com/fwlink/p/?linkid=237292">Licenciamento do Exchange Server</a>.</p></td>
<td><p>Exchange 2010 ou posterior</p></td>
</tr>
<tr class="even">
<td><p><strong>Exigir criptografia TLS</strong></p>
<p><strong>Modificar a segurança da mensagem</strong> &gt; <strong>Exigir criptografia TLS</strong></p></td>
<td><p><em>RouteMessageOutboundRequireTls</em></p></td>
<td><p><code>n/a</code></p></td>
<td><p>Força as mensagens de saída a serem roteadas sobre um TLS criptografada conexão.</p></td>
<td><p>Exchange 2013 ou posterior</p></td>
</tr>
<tr class="odd">
<td><p><strong>Preceder o assunto da mensagem com</strong></p></td>
<td><p><em>PrependSubject</em></p></td>
<td><p><code>String</code></p></td>
<td><p>Adiciona o texto especificado para o início do campo <strong>Subject</strong> da mensagem. Considere o uso de um espaço ou dois-pontos (:) como o último caractere do texto especificado, para diferenciá-lo de que o texto do assunto original.</p>
<p>Para impedir que a mesma cadeia de caracteres que está sendo adicionado às mensagens que já contêm o texto no assunto (por exemplo, respostas), adicione a exceção <strong>inclui o assunto</strong> (<em>ExceptIfSubjectContainsWords</em>) à regra.</p></td>
<td><p>Exchange 2007 ou posterior</p></td>
</tr>
<tr class="even">
<td><p><strong>Notificar o remetente com uma Dica de Política</strong></p></td>
<td><p><em>NotifySender</em></p>
<p><em>RejectMessageReasonText</em></p>
<p><em>RejectMessageEnhancedStatusCode</em> (Shell de Gerenciamento do Exchange somente)</p></td>
<td><p>Primeira propriedade: <code>NotifySenderType</code></p>
<p>Segunda propriedade: <code>String</code></p>
<p>Propriedade terceira (somenteShell de Gerenciamento do Exchange ): <code>DSNEnhancedStatusCode</code></p></td>
<td><p>Notifica o remetente ou bloqueia a mensagem quando a mensagem corresponder a uma política de DLP.</p>
<p>Quando você usa esta ação, você precisará usar o <strong>a mensagem contém informações confidenciais</strong> (<em>MessageContainsDataClassification</em> condição.</p>
<p>Quando você cria ou modificar a regra no Shell de Gerenciamento do Exchange, o parâmetro <em>RejectMessageReasonText</em> é opcional. Se você não usar esse parâmetro, o texto do padrão <code>Delivery not authorized, message refused</code> será usado.</p>
<p>No Shell de Gerenciamento do Exchange, você também pode usar o parâmetro <em>RejectMessageEnhancedStatusCode</em> para especificar o código de status avançado. Se você não usar esse parâmetro, o de código de status padrão enhanced <code>5.7.1</code> será usado.</p>
<p>Essa ação limita as condições, exceções e ações que você pode definir na regra.</p></td>
<td><p>Exchange 2013 ou posterior</p></td>
</tr>
<tr class="odd">
<td><p><strong>Gerar relatório de incidente e enviá-lo para</strong></p></td>
<td><p><em>GenerateIncidentReport</em></p>
<p><em>IncidentReportContent</em></p></td>
<td><p>Primeira propriedade: <code>Addresses</code></p>
<p>Segunda propriedade: <code>IncidentReportContent</code></p></td>
<td><p>Envia um relatório de incidente que contém o conteúdo especificado para os destinatários especificados.</p>
<p>Um relatório de incidente é gerado para mensagens que correspondam às políticas de (DLP) de prevenção de perda de dados em sua organização.</p></td>
<td><p>Exchange 2013 ou posterior</p></td>
</tr>
<tr class="even">
<td><p><strong>Notificar o destinatário com uma mensagem</strong></p></td>
<td><p><em>GenerateNotification</em></p></td>
<td><p><code>NotificationMessageText</code></p></td>
<td><p>Especifica o texto, marcas HTML e palavras-chave de mensagem para incluir na mensagem de notificação é enviada aos destinatários da mensagem. Por exemplo, você pode notificar destinatários que a mensagem foi rejeitada pela regra, ou marcada como spam e entregue a sua pasta de lixo eletrônico.</p></td>
<td><p>Exchange 2013 ou posterior</p></td>
</tr>
<tr class="odd">
<td><p>Seção de <strong>propriedades desta regra</strong> &gt; <strong>Auditar esta regra com nível de severidade</strong></p></td>
<td><p><em>SetAuditSeverity</em></p></td>
<td><p><code>AuditSeverityLevel</code></p></td>
<td><p>Especifica se deve ser:</p>
<ul>
<li><p>Impedir que a geração de um relatório de incidente e a entrada correspondente no log de acompanhamento de mensagens.</p></li>
<li><p>Gere um relatório de incidente e a entrada correspondente no log de rastreamento de mensagem com o nível de severidade especificado (baixo, médio ou alto).</p></li>
</ul></td>
<td><p>Exchange 2013 ou posterior</p></td>
</tr>
<tr class="even">
<td><p>Seção de <strong>propriedades desta regra</strong> &gt; <strong>Parar o processamento de mais regras</strong></p>
<p><strong>Mais opções</strong> &gt; seção de <strong>propriedades desta regra</strong> &gt; <strong>Parar o processamento de mais regras</strong></p></td>
<td><p><em>StopRuleProcessing</em></p></td>
<td><p>n/d</p></td>
<td><p>Especifica que, depois que a mensagem será afetada pela regra, a mensagem é isenta de processamento de outras regras.</p></td>
<td><p>Exchange 2013 ou posterior</p></td>
</tr>
</tbody>
</table>


Voltar ao início

## Ações de regras de fluxo de correio nos servidores de transporte de borda

Um pequeno subconjunto de ações que estão disponíveis em servidores de caixa de correio também estão disponíveis nos servidores de transporte de borda, mas também há algumas ações que só estão disponíveis nos servidores de transporte de borda. Não há nenhuma EAT nos servidores de transporte de borda, portanto você só pode gerenciar regras de fluxo de email no Shell de Gerenciamento do Exchange do servidor de transporte de borda local. As ações são descritas na tabela a seguir. Os tipos de propriedades são descritos na seção valores de propriedade .


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
<th>Parâmetro de ação na Shell de Gerenciamento do Exchange</th>
<th>Propriedade</th>
<th>Descrição</th>
<th>Disponível em</th>
<th>Disponível em</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>AddToRecipients</em></p></td>
<td><p><code>Addresses</code></p></td>
<td><p>Adiciona um ou mais destinatários ao campo <strong>To</strong> da mensagem. Os destinatários originais podem ver os endereços adicionais.</p></td>
<td><p>Servidores de caixa de correio e servidores de transporte de borda</p></td>
<td><p>Exchange 2007 ou posterior</p></td>
</tr>
<tr class="even">
<td><p><em>BlindCopyTo</em></p></td>
<td><p><code>Addresses</code></p></td>
<td><p>Adiciona um ou mais destinatários ao campo <strong>Bcc</strong> da mensagem. Os destinatários originais não são notificados e eles não podem ver os endereços adicionais.</p></td>
<td><p>Servidores de caixa de correio e servidores de transporte de borda</p></td>
<td><p>Exchange 2007 ou posterior</p></td>
</tr>
<tr class="odd">
<td><p><em>CopyTo</em></p></td>
<td><p><code>Addresses</code></p></td>
<td><p>Adiciona um ou mais destinatários ao campo <strong>Cc</strong> da mensagem. Os destinatários originais podem ver o endereço adicional.</p></td>
<td><p>Servidores de caixa de correio e servidores de transporte de borda</p></td>
<td><p>Exchange 2007 ou posterior</p></td>
</tr>
<tr class="even">
<td><p><em>DeleteMessage</em></p></td>
<td><p>n/d</p></td>
<td><p>Descarta silenciosamente a mensagem sem enviar a notificação para o destinatário ou o remetente.</p></td>
<td><p>Servidores de caixa de correio e servidores de transporte de borda</p></td>
<td><p>Exchange 2007 ou posterior</p></td>
</tr>
<tr class="odd">
<td><p><em>Disconnect</em></p></td>
<td><p>n/d</p></td>
<td><p>Termina a conexão SMTP entre o servidor de envio e o servidor de transporte de borda sem gerar uma NDR.</p></td>
<td><p>Somente servidores de transporte de borda</p></td>
<td><p>Exchange 2007 ou posterior</p></td>
</tr>
<tr class="even">
<td><p><em>LogEventText</em></p></td>
<td><p><code>String</code></p></td>
<td><p>Gera um evento com o texto especificado no log do aplicativo do servidor local de transporte de borda. A entrada contém as seguintes informações:</p>
<ul>
<li><p><strong>Nível</strong> <code>Information</code>   </p></li>
<li><p><strong>Fonte</strong> <code>MSExchange Messaging Policies</code>   </p></li>
<li><p><strong>ID do evento</strong> <code>4000</code>   </p></li>
<li><p><strong>Categoria da tarefa</strong> <code>Rules</code>   </p></li>
<li><p><strong>EventData</strong>   <code>The following message is logged by an action in the rules: &lt;text you specify&gt;.</code></p></li>
</ul></td>
<td><p>Apenas os servidores de transporte de borda</p></td>
<td><p>Exchange 2007 ou posterior</p></td>
</tr>
<tr class="odd">
<td><p><em>PrependSubject</em></p></td>
<td><p><code>String</code></p></td>
<td><p>Adiciona o texto especificado para o início do campo <strong>Subject</strong> da mensagem. Considere o uso de um espaço ou dois-pontos (:) como o último caractere do texto especificado diferenciá-lo de assunto original.</p></td>
<td><p>Servidores de caixa de correio e servidores de transporte de borda</p></td>
<td><p>Exchange 2007 ou posterior</p></td>
</tr>
<tr class="even">
<td><p><em>Quarantine</em></p></td>
<td><p>n/d</p></td>
<td><p>Entrega a mensagem na caixa de correio de quarentena definida no configuração no servidor de transporte de borda de filtragem de conteúdo. Para obter mais informações, consulte <a href="configure-a-spam-quarantine-mailbox-exchange-2013-help.md">Configurar uma caixa de correio de quarentena de spam</a>.</p>
<p>Se a caixa de correio de quarentena não estiver configurada, a mensagem é retornada ao remetente em uma NDR.</p></td>
<td><p>Somente servidores de transporte de borda</p></td>
<td><p>Exchange 2010 ou posterior</p></td>
</tr>
<tr class="odd">
<td><p><em>RedirectMessageTo</em></p></td>
<td><p><code>Addresses</code></p></td>
<td><p>Redireciona a mensagem para os destinatários especificados. A mensagem não entregue aos destinatários originais e nenhuma notificação é enviada para o remetente ou destinatários originais.</p></td>
<td><p>Servidores de caixa de correio e servidores de transporte de borda</p></td>
<td><p>Exchange 2007 ou posterior</p></td>
</tr>
<tr class="even">
<td><p><em>RemoveHeader</em></p></td>
<td><p><code>MessageHeaderField</code></p></td>
<td><p>Remove o campo de cabeçalho especificado do cabeçalho da mensagem.</p></td>
<td><p>Servidores de caixa de correio e servidores de transporte de borda</p></td>
<td><p>Exchange 2007 ou posterior</p></td>
</tr>
<tr class="odd">
<td><p><em>SetHeaderName</em></p>
<p><em>SetHeaderValue</em></p></td>
<td><p>Primeira propriedade: <code>MessageHeaderField</code></p>
<p>Segunda propriedade: <code>String</code></p></td>
<td><p>Adiciona ou modifica o campo de cabeçalho especificado no cabeçalho da mensagem e define o campo de cabeçalho ao valor especificado.</p></td>
<td><p>Servidores de caixa de correio e servidores de transporte de borda</p></td>
<td><p>Exchange 2007 ou posterior</p></td>
</tr>
<tr class="even">
<td><p><em>SetSCL</em></p></td>
<td><p><code>SCLValue</code></p></td>
<td><p>Define o SCL da mensagem com o valor especificado.</p></td>
<td><p>Servidores de caixa de correio e servidores de transporte de borda</p></td>
<td><p>Exchange 2007 ou posterior</p></td>
</tr>
<tr class="odd">
<td><p><em>SmtpRejectMessageRejectText</em></p>
<p><em>SmtpRejectMessageRejectStatusCode</em></p></td>
<td><p>Primeira propriedade: <code>String</code></p>
<p>Segunda propriedade: <code>SMTPStatusCode</code></p></td>
<td><p>Termina a conexão SMTP entre o servidor de envio e o servidor de transporte de borda com o código de status SMTP especificado e o texto de rejeição especificado. O destinatário não receber a mensagem original ou a notificação.</p>
<p>Valores válidos para o código de status SMTP são números inteiros de <code>400</code> por meio de <code>500</code> como definido no RFC 3463.</p>
<p>Se você especificar o texto de rejeição sem especificar o código de status SMTP, o código do padrão <code>550</code> é usado.</p>
<p>Se você especificar o código de status de SMTP sem especificar o texto de rejeição, o texto que é usado é <code>Delivery not authorized, message refused</code>.</p></td>
<td><p>Apenas os servidores de transporte de borda</p></td>
<td><p>Exchange 2007 ou posterior</p></td>
</tr>
<tr class="even">
<td><p><em>StopRuleProcessing</em></p></td>
<td><p>n/d</p></td>
<td><p>Especifica que, depois que a mensagem será afetada pela regra, a mensagem é isenta de processamento de outras regras.</p></td>
<td><p>Servidores de caixa de correio e servidores de transporte de borda</p></td>
<td><p>Exchange 2013 ou posterior</p></td>
</tr>
</tbody>
</table>


## Valores de propriedades

Os valores de propriedade são usados para ações de regras de fluxo de correio são descritos na tabela a seguir.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Propriedade</th>
<th>Valores válidos</th>
<th>Descrição</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code>AddedManagerAction</code></p></td>
<td><p>Um dos seguintes valores:</p>
<ul>
<li><p><strong>Para</strong></p></li>
<li><p><strong>Cc</strong></p></li>
<li><p><strong>Cco</strong></p></li>
<li><p><strong>Redirecionar</strong></p></li>
</ul></td>
<td><p>Especifica como incluir o gerente do remetente em mensagens.</p>
<ul>
<li><p>Se você selecionar <strong>para</strong>, <strong>Cc</strong> ou <strong>Cco</strong>, o gerente do remetente é adicionado como um destinatário no campo especificado.</p></li>
<li><p>Se você selecionar <strong>Redirecionar</strong>, a mensagem é entregue apenas para o gerente do remetente sem notificar o remetente ou destinatário.</p></li>
</ul>
<p>Essa ação só funciona se o atributo do remetente <strong>Manager</strong> é definido em Active Directory.</p></td>
</tr>
<tr class="even">
<td><p><code>Addresses</code></p></td>
<td><p>destinatários Exchange</p></td>
<td><p>Dependendo da ação, você poderá especificar qualquer objeto habilitado para email na organização ou você pode ser limitado a um tipo de objeto específico. Normalmente, você pode selecionar vários destinatários, mas você só pode enviar um relatório de incidente para um destinatário.</p></td>
</tr>
<tr class="odd">
<td><p><code>AuditSeverityLevel</code></p></td>
<td><p>Um dos seguintes valores:</p>
<ul>
<li><p>Desmarque <strong>Auditar esta regra com nível de severidade</strong> ou selecione <strong>Auditar esta regra com nível de severidade</strong>, com o valor <strong>especificado não</strong> (<code>DoNotAudit</code>)</p></li>
<li><p><strong>Baixo</strong></p></li>
<li><p><strong>Médio</strong></p></li>
<li><p><strong>Alta</strong></p></li>
</ul></td>
<td><p>Os valores de <strong>baixa</strong>, <strong>média</strong> ou <strong>alta</strong> especificam o nível de severidade atribuído para o relatório de incidente e a entrada correspondente no log de acompanhamento de mensagens.</p>
<p>O outro valor impede que um relatório de incidente sendo gerado e impede que a entrada correspondente sendo gravado para a log de acompanhamento de mensagens.</p></td>
</tr>
<tr class="even">
<td><p><code>DisclaimerFallbackAction</code></p></td>
<td><p>Um dos seguintes valores:</p>
<ul>
<li><p><strong>Quebra automática</strong></p></li>
<li><p><strong>Ignorar</strong></p></li>
<li><p><strong>Rejeitar</strong></p></li>
</ul></td>
<td><p>Especifica o que fazer se a isenção de responsabilidade não pode ser aplicada a uma mensagem. Existem situações em que o conteúdo de uma mensagem não pode ser alterado (por exemplo, a mensagem é criptografada). As ações de fallback disponíveis são:</p>
<ul>
<li><p><strong>Quebrar</strong>    A mensagem original é contida em um novo envelope de mensagem e o texto de isenção de responsabilidade é inserido da nova mensagem. Este é o valor padrão.</p>
<p><strong>Observações</strong>:</p>
<ul>
<li><p>Regras de fluxo de correio subsequentes são aplicadas ao envelope de mensagem nova, não à mensagem original. Portanto, configure essas regras com uma prioridade menor do que outras regras.</p></li>
<li><p>Se a mensagem original não pode ser disposta em um novo envelope de mensagem, a mensagem original não é entregue. A mensagem é retornada ao remetente em uma NDR.</p></li>
</ul></li>
<li><p><strong>Ignorar</strong>    A regra é ignorada e a mensagem é entregue sem o aviso de isenção</p></li>
<li><p><strong>Rejeitar</strong>    A mensagem é retornada ao remetente em uma NDR.</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p><code>DisclaimerText</code></p></td>
<td><p>Cadeia de caracteres HTML</p></td>
<td><p>Especifica o texto de isenção de responsabilidade, que pode incluir marcas HTML, marcas CSS (folha) de estilo em cascata embutidas e imagens usando a marca IMG. O comprimento máximo é de 5000 caracteres, inclusive as marcas.</p></td>
</tr>
<tr class="even">
<td><p><code>DisclaimerTextLocation</code></p></td>
<td><p>Valor único: <code>Append</code> ou <code>Prepend</code></p></td>
<td><p>A Shell de Gerenciamento do Exchange, você usa o <em>ApplyHtmlDisclaimerTextLocation</em> para especificar o local do texto de isenção de responsabilidade na mensagem:</p>
<ul>
<li><p><code>Append</code>   Adicione a isenção de responsabilidade até o final do corpo da mensagem. Este é o valor padrão.</p></li>
<li><p><code>Prepend</code>   Adicione a isenção de responsabilidade para o início do corpo da mensagem.</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p><code>DSNEnhancedStatusCode</code></p></td>
<td><p>Valor de código DSN único:</p>
<ul>
<li><p><code>5.7.1</code></p></li>
<li><p><code>5.7.900</code> por meio de <code>5.7.999</code></p></li>
</ul></td>
<td><p>Especifica o código DSN que é usado. Você pode criar DSNs personalizados usando o cmdlet <strong>New-SystemMessage</strong> .</p>
<p>Se você não especificar o texto do motivo de rejeição, juntamente com o código DSN, o texto padrão de razão que é usado é <code>Delivery not authorized, message refused</code>.</p>
<p>Quando você cria ou modificar a regra no Shell de Gerenciamento do Exchange, você pode especificar o texto do motivo de rejeição, usando o parâmetro <em>RejectMessageReasonText</em> .</p></td>
</tr>
<tr class="even">
<td><p><code>IncidentReportContent</code></p></td>
<td><p>Um ou mais dos seguintes valores:</p>
<ul>
<li><p><strong>Remetente</strong></p></li>
<li><p><strong>Destinatários</strong></p></li>
<li><p><strong>Assunto</strong></p></li>
<li><p><strong>Cc distr destinatários</strong> (<code>Cc</code>)</p></li>
<li><p><strong>Destinatários de distr Cco</strong> (<code>Bcc</code>)</p></li>
<li><p><strong>Severidade</strong></p></li>
<li><p><strong>Informações de substituição do remetente</strong> (<code>Override</code>)</p></li>
<li><p><strong>Regras de correspondência</strong> (<code>RuleDetections</code>)</p></li>
<li><p><strong>Relatórios de positivos falsos</strong> (<code>FalsePositive</code>)</p></li>
<li><p><strong>Classificações de dados detectado</strong> (<code>DataClassifications</code>)</p></li>
<li><p><strong>Correspondendo o conteúdo</strong> (<code>IdMatch</code>)</p></li>
<li><p><strong>Email original</strong> (<code>AttachOriginalMail</code>)</p></li>
</ul></td>
<td><p>Especifica as propriedades da mensagem original para incluir no relatório de incidentes. Você pode optar por incluir qualquer combinação dessas propriedades. Além das propriedades que você especificar, a ID da mensagem é sempre incluída. As propriedades disponíveis são:</p>
<ul>
<li><p><strong>Remetente</strong>   O remetente da mensagem original.</p></li>
<li><p><strong>Destinatários</strong>, <strong>os destinatários de distr Cc</strong> e <strong>Cco distr destinatários</strong> todos os destinatários da mensagem ou somente os destinatários nos campos <strong>Cc</strong> ou <strong>Bcc</strong> . Para cada propriedade, somente os 10 primeiros destinatários estão incluídos no relatório de incidentes.</p></li>
<li><p><strong>Assunto</strong>    O campo <strong>Subject</strong> da mensagem original.</p></li>
<li><p><strong>Severidade</strong>    A gravidade da auditoria da regra que tiver sido disparada. Logs de rastreamento de mensagem incluem todos os níveis de severidade de auditoria e podem ser filtrados por gravidade da auditoria. No EAC, se você desmarcar a caixa de seleção <strong>Auditar esta regra com nível de severidade</strong> (no Shell de Gerenciamento do Exchange, o de valor do parâmetro <em>SetAuditSeverity</em><code>DoNotAudit</code>), correspondências de regra não aparecem nos relatórios de regras. Se uma mensagem é processada por mais de uma regra, a gravidade mais alta está incluída no quaisquer relatórios de incidentes.</p></li>
<li><p><strong>Informações de substituição do remetente</strong>    A substituição se o remetente optou por substituir uma dica de política. Se o remetente fornecida uma justificativa, os 100 primeiros caracteres da justificação também são incluídos.</p></li>
<li><p><strong>Regras de correspondência</strong>    A lista de regras desencadeada pela mensagem.</p></li>
<li><p><strong>Relatórios de positivos falsos</strong>    O falso positivo se o remetente tiver marcado a mensagem como um falso positivo para uma dica de política.</p></li>
<li><p><strong>Classificações de dados detectado</strong>    A lista de tipos de informações confidenciais detectados na mensagem.</p></li>
<li><p><strong>Correspondendo o conteúdo</strong>    O tipo de informação confidencial detectado, o conteúdo correspondente exato da mensagem e os 150 caracteres antes e depois da informação confidencial correspondente.</p></li>
<li><p><strong>Email original</strong>   A mensagem inteira que disparou a regra está anexada ao relatório de incidentes.</p></li>
</ul>
<p>No Shell de Gerenciamento do Exchange, especifique vários valores separados por vírgulas.</p></td>
</tr>
<tr class="odd">
<td><p><code>MessageClassification</code></p></td>
<td><p>Objeto único de classificação da mensagem</p></td>
<td><p>No EAC, selecione da lista de classificações de mensagem disponíveis.</p>
<p>No Shell de Gerenciamento do Exchange, use o cmdlet de <strong>Get-MessageClassification</strong> para ver os objetos de classificação de mensagem que estão disponíveis.</p></td>
</tr>
<tr class="even">
<td><p><code>MessageHeaderField</code></p></td>
<td><p>Cadeia de caracteres única</p></td>
<td><p>Especifica o campo de cabeçalho de mensagem SMTP para adicionar, remover ou modificar.</p>
<p>O <em>cabeçalho da mensagem</em> é uma coleção de campos obrigatórios e opcionais de cabeçalho na mensagem. Exemplos de campos de cabeçalho são <strong>To</strong>, <strong>From</strong>, <strong>Received</strong>e <strong>Content-Type</strong>. Campos de cabeçalho oficial são definidos na RFC 5322. Campos de cabeçalho não oficiais começam com <strong>X-</strong> e são conhecidos como <em>cabeçalhos X</em>.</p></td>
</tr>
<tr class="odd">
<td><p><code>NotificationMessageText</code></p></td>
<td><p>Qualquer combinação de palavras-chave, marcas HTML e texto sem formatação</p></td>
<td><p>Especificado o texto a ser usado em uma mensagem de notificação do destinatário.</p>
<p>Além de texto sem formatação e marcas HTML, você pode especificar as seguintes palavras-chave que usam valores a partir da mensagem original:</p>
<ul>
<li><p><code>%%From%%</code></p></li>
<li><p><code>%%To%%</code></p></li>
<li><p><code>%%Cc%%</code></p></li>
<li><p><code>%%Subject%%</code></p></li>
<li><p><code>%%Headers%%</code></p></li>
<li><p><code>%%MessageDate%%</code></p></li>
</ul></td>
</tr>
<tr class="even">
<td><p><code>NotifySenderType</code></p></td>
<td><p>Um dos seguintes valores:</p>
<ul>
<li><p><strong>Notificar o remetente, mas permitir que eles enviem</strong> (<code>NotifyOnly</code>)</p></li>
<li><p><strong>Bloquear a mensagem</strong> (<code>RejectMessage</code>)</p></li>
<li><p><strong>Bloquear a mensagem, a menos que ele seja um falso positivo</strong> (<code>RejectUnlessFalsePositiveOverride</code>)</p></li>
<li><p><strong>Bloquear a mensagem, mas permitir que o remetente sobreponha e envie</strong> (<code>RejectUnlessSilentOverride</code>)</p></li>
<li><p><strong>Bloquear a mensagem, mas permitir que o remetente sobreponha com uma justificativa comercial e envie</strong> (<code>RejectUnlessExplicitOverride</code>)</p></li>
</ul></td>
<td><p>Especifica o tipo de dica de política que o remetente recebe se a mensagem violar uma política de DLP. As configurações são descritas na lista a seguir:</p>
<ul>
<li><p><strong>Notificar o remetente, mas permitir que eles enviem</strong> O remetente é notificado, mas a mensagem é entregue normalmente.</p></li>
<li><p><strong>Bloquear a mensagem</strong> A mensagem é rejeitada, e o remetente é notificado.</p></li>
<li><p><strong>Bloquear a mensagem, a menos que ele seja um falso positivo</strong> A mensagem é rejeitada a menos que seja marcada como um falso positivo pelo remetente.</p></li>
<li><p><strong>Bloquear a mensagem, mas permitir que o remetente sobreponha e enviar</strong> A mensagem é rejeitada a menos que o remetente tenha optado por substituir a restrição de política.</p></li>
<li><p><strong>Bloquear a mensagem, mas permitir que o remetente sobreponha com uma justificativa comercial e enviar</strong> Este é semelhante ao tipo de <strong>Bloquear a mensagem, mas permitir que o remetente sobreponha e envie</strong>, mas o remetente também oferece uma justificativa para anular a restrição de política.</p></li>
</ul>
<p>Quando você usa esta ação, você precisará usar a condição <strong>a mensagem contém informações confidenciais</strong> (<em>MessageContainsDataClassification</em>).</p></td>
</tr>
<tr class="odd">
<td><p><code>RMSTemplate</code></p></td>
<td><p>Único objeto de modelo do RMS</p></td>
<td><p>Especifica o modelo de Rights Management Services (RMS) que é aplicado à mensagem.</p>
<p>No EAC, você pode selecionar o modelo do RMS em uma lista.</p>
<p>No Shell de Gerenciamento do Exchange, use o cmdlet de <strong>Get-RMSTemplate</strong> para ver os modelos de RMS disponíveis.</p>
<p>RMS exige licenças de acesso para cliente Enterprise Exchange (CALs) para cada caixa de correio. Para obter mais informações sobre CALs, consulte <a href="https://go.microsoft.com/fwlink/p/?linkid=237292">Licenciamento do Exchange Server</a>.</p></td>
</tr>
<tr class="even">
<td><p><code>SCLValue</code></p></td>
<td><p>Um dos seguintes valores:</p>
<ul>
<li><p><strong>Ignorar filtragem de spam</strong> (<code>-1</code>)</p></li>
<li><p>Números inteiros de 0 a 9</p></li>
</ul></td>
<td><p>Especifica o nível de confiança de spam (SCL) que é atribuído à mensagem. Um valor SCL superior indica que uma mensagem é mais provável de ser spam.</p></td>
</tr>
<tr class="odd">
<td><p><code>String</code></p></td>
<td><p>Cadeia de caracteres única</p></td>
<td><p>Especifica o texto que é aplicado à entrada de log de eventos, NDR ou campo da cabeçalho especificado da mensagem.</p>
<p>No Shell de Gerenciamento do Exchange, se o valor contiver espaços, coloque-o valor entre aspas (&quot;).</p></td>
</tr>
</tbody>
</table>


Voltar ao início

## Para saber mais

[Gerenciar regras de fluxo de emails](https://docs.microsoft.com/pt-br/exchange/security-and-compliance/mail-flow-rules/manage-mail-flow-rules)

[Regras de fluxo de emails ou de transporte](mail-flow-rules-transport-rules-in-exchange-2013-exchange-2013-help.md)

[Condições de regra de transporte (predicados)](mail-flow-rule-conditions-and-exceptions-predicates-in-exchange-2013-exchange-2013-help.md)

[Email ações de regra de fluxo no Exchange Online](https://technet.microsoft.com/pt-br/library/jj919237\(v=exchg.150\)) para Exchange Online

[De email ações de regra de fluxo no Exchange Online Protection](https://technet.microsoft.com/pt-br/library/jj920117\(v=exchg.150\)) para o Exchange Online Protection

[Avisos de isenção de mensagem em toda a organização, assinaturas, rodapés ou cabeçalhos no Office 365](https://technet.microsoft.com/pt-br/library/dn600323\(v=exchg.150\))

