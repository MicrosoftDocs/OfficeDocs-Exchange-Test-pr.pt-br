---
title: 'MailTips: Exchange 2013 Help'
TOCTitle: MailTips
ms:assetid: 9c989167-cc0c-40a6-82ba-383f573bd2d5
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/JJ649091(v=EXCHG.150)
ms:contentKeyID: 50486220
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# MailTips

 

_**Aplica-se a:**Exchange Online, Exchange Server 2013_

_**Tópico modificado em:**2017-04-28_

Dicas de Email são mensagens informativas exibidas aos usuários enquanto eles compõem uma mensagem. O Microsoft Exchange Server 2013 analisa a mensagem, incluindo a lista de destinatários a que ela é endereçada. Se um problema potencial for detectado, o usuário será notificado com Dicas de Email antes do envio da mensagem. Com a ajuda das informações fornecidas pelas Dicas de Email, os remetentes podem ajustar a mensagem que estão escrevendo para evitar situações indesejáveis ou notificações de falha na entrega.

## Como funcionam as Dicas de Email

As Dicas de Email são implementadas como um serviço Web no Exchange 2013. Quando um remetente compõe uma mensagem, o software cliente faz uma chamada do serviço Web do Exchange ao servidor de Acesso para Cliente, para obter a lista de Dicas de Email. O servidor responde com a lista de Dicas de Email aplicáveis a essa mensagem, e o software cliente exibe as Dicas de Email ao remetente.

Os seguintes cenários de mensagens improdutivos são comuns em qualquer ambiente de sistema de mensagens:

  - Notificações de falha na entrega de mensagens que violam as restrições configuradas em uma organização, como restrições de tamanho da mensagem ou número máximo de destinatários por mensagem.

  - Notificações de falha na entrega de mensagens enviadas a destinatários que não existem, com restrição ou a usuários cujas caixas de correio estão cheias.

  - Enviar mensagens a usuários com Respostas automáticas configuradas.

Todos esses cenários envolvem o envio de uma mensagem pelo usuário, a sua entrega e, em vez de essa entrega ocorrer, o usuário recebe uma resposta informando que a mensagem não foi entregue. Mesmo no melhor dos cenários, como a resposta automática, esses eventos resultam em perda de produtividade. No caso de uma notificação de falha na entrega, esse cenário poderá resultar em uma chamada dispendiosa ao suporte técnico.

Há também vários cenários em que o envio de uma mensagem não resultará em erro, mas poderá ter consequências indesejáveis, até mesmo desagradáveis:

  - Mensagens enviadas a grupos de distribuição muito grandes.

  - Mensagens enviadas a grupos de distribuição inadequados.

  - Mensagens enviadas inadvertidamente a destinatários fora da organização.

  - Seleção de **Responder a Todos** para uma mensagem que foi recebida como destinatário Cco.

Todos esses cenários problemáticos poderão ser atenuados se os usuários forem informados sobre o resultado possível do envio da mensagem à medida que eles compuserem essa mensagem. Por exemplo, se os remetentes souberem que o tamanho da mensagem que estão tentando enviar excede a diretiva da empresa, eles não tentarão enviar a mensagem. Da mesma forma, se os remetentes forem notificados de que a mensagem sendo enviada será entregue a pessoas fora da organização, eles estarão mais propensos a garantir que o conteúdo e o tom da mensagem sejam apropriados.

Os seguintes clientes de mensagens são compatíveis com Dicas de Email:

  - Outlook Web App

  - Microsoft Outlook 2010 ou posterior

## Dicas de Email no Exchange

A tabela a seguir lista as Dicas de Email disponíveis no Exchange 2013.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Dica de Email</th>
<th>Disponibilidade</th>
<th>Cenário</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Destinatário interno inválido</p></td>
<td><p>Outlook</p></td>
<td><p>A Dica de Email de Destinatário Interno Inválido será exibida se o remetente adicionar um destinatário que aparenta fazer parte da organização, mas não existe nela.</p>
<p>Isso poderá ocorrer se o remetente enviar mensagem a um usuário que não está mais na empresa, mas seu endereço continuar válido no cache de resolução de nomes ou ainda estiver na pasta Contatos do remetente. Isso também poderá ocorrer se o remetente digitar um endereço SMTP com um domínio para o qual o Exchange seja autoritativo e o endereço não resolver para um destinatário existente.</p>
<p>A Dica de Email indica o destinatário inválido e dá ao remetente a opção de remover o destinatário da mensagem.</p></td>
</tr>
<tr class="even">
<td><p>Caixa de Correio Cheia</p></td>
<td><p>Outlook</p>
<p>Outlook Web App</p></td>
<td><p>A Dica de Email de caixa de correio cheia será exibida se o remetente adicionar um destinatário cuja caixa de correio esteja cheia e sua organização tiver implementado uma restrição de recebimento proibido para caixas de correio de um determinado tamanho.</p>
<p>A Dica de Email indica o destinatário com a caixa de correio cheia e dá ao remetente a opção de remover o destinatário da mensagem.</p>
<p>A Dica de Email é precisa no momento da exibição. Se a mensagem não for enviada imediatamente, a Dica de email será atualizada a cada duas horas. Isso também se aplica às mensagens que foram salvas na pasta Rascunhos e reabertas após duas horas.</p></td>
</tr>
<tr class="odd">
<td><p>Respostas Automáticas</p></td>
<td><p>Outlook</p>
<p>Outlook Web App</p></td>
<td><p>A Dica de email de Respostas automáticas é exibida se o remetente adicionar um destinatário que tiver habilitado as Respostas automáticas.</p>
<p>A dica de email indica o destinatário tenha as respostas automáticas ativado e também exibe os primeiros 175 caracteres da resposta automática configurada pelo destinatário.</p>
<p>A Dica de Email é precisa no momento da exibição. Se a mensagem não for enviada imediatamente, a Dica de email será atualizada a cada duas horas. Isso também se aplica às mensagens que foram salvas na pasta Rascunhos e reabertas após duas horas.</p>
<p>Se parte de suas caixas de correio de usuário estiverem hospedadas no Exchange Online e você estiver em coexistência com o cenário do Exchange Online, a configuração no objeto de domínio remoto que representa a parte remota de sua organização terá efeito direto sobre como essa Dica de Email é processada.</p>
<p>No Exchange 2013, os usuários podem configurar Respostas automáticas diferentes para remetentes internos e externos. Se o domínio remoto estiver configurado como um domínio interno (ao configurar o parâmetro <em>IsInternal</em> no objeto de domínio remoto para <code>$true</code>), a resposta automática interna será retornada a todos os usuários na organização, independentemente de onde a caixa de correio resida. Contudo, se o domínio remoto não estiver configurado como um domínio interno, a resposta automática interna será retornada a todos os usuário cujas caixas de correio estejam no domínio local, e a resposta automática externa será retornada aos usuário cujas caixas de correio estejam no domínio remoto.</p></td>
</tr>
<tr class="even">
<td><p>Personalizada</p></td>
<td><p>Outlook</p>
<p>Outlook Web App</p></td>
<td><p>Uma Dica de Email personalizada será exibida se o remetente adicionar um destinatário para o qual uma Dica de Email personalizada está configurada.</p>
<p>Uma Dica de Email personalizada pode ser útil para o fornecimento de informações específicas sobre um destinatário. Por exemplo, você pode criar uma Dica de Email personalizada para um grupo de distribuição, explicando sua finalidade para reduzir o uso indevido. Para obter mais informações, consulte <a href="configure-custom-mailtips-for-recipients-exchange-2013-help.md">Configurar Dicas de Email personalizadas para destinatários</a>.</p>
<p>Por padrão, as Dicas de Email personalizadas não serão exibidas se o remetente não tiver permissão para enviar a esse destinatário. Nesse caso, a Dica de Email de destinatário restrito é exibida. Entretanto, você pode alterar essa configuração e exibir também a Dica de Email personalizada.</p></td>
</tr>
<tr class="odd">
<td><p>Destinatário restrito</p></td>
<td><p>Outlook</p>
<p>Outlook Web App</p></td>
<td><p>A Dica de Email de destinatário restrito será exibida se o remetente adicionar um destinatário com restrições de entrega configuradas, impedindo esse remetente de enviar mensagens.</p>
<p>A Dica de Email indica o destinatário ao qual o remetente não tem permissão para enviar mensagens e dá ao remetente a opção de remover o destinatário da mensagem. Ela também informa claramente o remetente de que a mensagem não será entregue se enviada.</p>
<p>Se o destinatário restrito for externo ou for um grupo de distribuição com destinatários externos, essas informações também serão fornecidas ao remetente. No entanto, as seguintes Dicas de Email, se aplicável, serão suprimidas:</p>
<ul>
<li><p>Respostas Automáticas</p></li>
<li><p>Caixa de Correio Cheia</p></li>
<li><p>Dica de Email personalizada</p></li>
<li><p>Destinatário moderado</p></li>
<li><p>Mensagem com tamanho excessivo</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Destinatários externos</p></td>
<td><p>Outlook</p>
<p>Outlook Web App</p></td>
<td><p>A Dica de Email de destinatários externos será exibida se o remetente adicionar um destinatário externo ou adicionar um grupo de distribuição que tenha destinatários externos.</p>
<p>Essa Dica de Email informará os remetentes se uma mensagem que estiverem compondo for enviada para fora da organização, ajudando-os a tomar as decisões corretas a respeito do estilo, do tom e do conteúdo.</p>
<p>Por padrão, essa Dica de Email fica desabilitada. É possível habilitá-la usando o cmdlet <strong>Set-OrganizationConfig</strong>. Para detalhes, consulte <a href="mailtips-over-organization-relationships-exchange-2013-help.md">Dicas de email sobre relacionamentos da organização</a>.</p>
<p>Se parte de suas caixas de correio de usuário estiver hospedada no Exchange Online e você estiver em coexistência com o cenário do Exchange Online, a configuração no objeto de domínio remoto que representa a parte remota de sua organização terá efeito direto sobre como essa Dica de email é processada.</p>
<p>Se o domínio remoto estiver configurado como um domínio interno (ao configurar o parâmetro <em>IsInternal</em> no objeto de domínio remoto para <code>$true</code>), quaisquer destinatários nesse domínio remoto serão tratados como internos e, portanto, a Dica de email dos Destinatários externos não será exibida. Contudo, se o domínio remoto não estiver configurado como um domínio interno, os destinatários naquele domínio serão considerados externos e essa Dica de email será exibida quando uma mensagem estiver sendo redigida para aqueles destinatários.</p>

> [!TIP]
> Essa Dica de email não é avaliada quando uma mensagem é redigida para um grupo de distribuição no domínio remoto.


</td>
</tr>
<tr class="odd">
<td><p>Grande público</p></td>
<td><p>Outlook</p>
<p>Outlook Web App</p></td>
<td><p>A Dica de Email de grande público será exibida se o remetente adicionar um grupo de distribuição com contagem maior do que o tamanho de público configurado em sua organização. Por padrão, o Exchange exibe a Dica de Email de mensagens para grupos de distribuição que tenham mais de 25 membros. Para obter detalhes, consulte <a href="configure-the-large-audience-size-for-your-organization-exchange-2013-help.md">Configurar o tamanho grande público para sua organização</a>.</p>
<p>O tamanho dos grupos de distribuição não é calculado sempre. Em vez disso, as informações do grupo de distribuição são lidas a partir de dados de medição de grupo.</p></td>
</tr>
<tr class="even">
<td><p>Destinatário moderado</p></td>
<td><p>Outlook</p>
<p>Outlook Web App</p></td>
<td><p>A Dica de Email de destinatário moderado será exibida se o remetente adicionar um destinatário moderado.</p>
<p>A Dica de Email mostra qual destinatário é moderado e informa o remetente que isso pode resultar em atraso da entrega.</p>
<p>Se o remetente for também é o moderador, essa Dica de Email não será exibida. Ela também não será exibida se o remetente tiver permissão para enviar mensagens ao destinatário (adicionando o nome do remetente à lista Aceitar mensagens somente de, para o destinatário).</p>
<p>Para ver instruções de como configurar destinatários moderados no Exchange 2013, consulte <a href="common-message-approval-scenarios-exchange-2013-help.md">Cenários comuns de aprovação de mensagem</a>.</p>
<p>Para ver instruções de como configurar destinatários moderados no Exchange Online, consulte <a href="https://technet.microsoft.com/pt-br/library/jj983442(v=exchg.150)">Configurar um destinatário moderado no Exchange Online</a>.</p></td>
</tr>
<tr class="odd">
<td><p>Responder a Todos com Cco</p></td>
<td><p>Outlook Web App</p></td>
<td><p>A Dica de Email Responder a Todos com Cco será exibida se o remetente receber uma cópia oculta de uma mensagem e selecionar <strong>Responder a Todos</strong>.</p>
<p>Quando o usuário seleciona <strong>Responder a Todos</strong> para essa mensagem, o fato é que o usuário que recebeu uma Cco dessa mensagem será revelado ao restante do público a que a mensagem foi enviada. Em quase todos os casos, essa é uma situação indesejável, e esta Dica de Email informa o usuário sobre essa condição.</p></td>
</tr>
<tr class="even">
<td><p>Mensagem com tamanho excessivo</p></td>
<td><p>Outlook</p></td>
<td><p>A Dica de Email de mensagem com tamanho excessivo será exibida se a mensagem composta pelo remetente for maior do que os limites de tamanho de mensagem configurados em sua organização.</p>
<p>A Dica de Email será exibida se o tamanho da mensagem violar uma das seguintes restrições de tamanho:</p>
<ul>
<li><p>Configuração de tamanho máximo de envio na caixa de correio do remetente</p></li>
<li><p>Configuração de tamanho máximo de recebimento na caixa de correio do destinatário</p></li>
<li><p>Restrição de tamanho máximo da mensagem para a organização</p></li>
</ul>

> [!TIP]
> Devido à complexidade da implementação, os limites de tamanho da mensagem nos conectores de sua organização não são levados em consideração.


</td>
</tr>
</tbody>
</table>


## Restrições de Dica de Email

As Dicas de Email estão sujeitas às seguintes restrições:

  - As Dicas de Email não têm suporte quando se trabalha no modo offline do Outlook.

  - Quando uma mensagem é endereçada a um grupo de distribuição, as Dicas de Email de destinatários individuais pertencentes a esse grupo de distribuição não são avaliadas. Entretanto, se algum dos membros for um destinatário externo, a Dica de Email de destinatários externos será exibida, que mostra ao remetente o número de destinatários externos no grupo de distribuição.

  - Se a mensagem for endereçada a mais de 200 destinatários, as Dicas de Email de caixa de correio individuais não serão avaliadas por motivos de desempenho.

  - Dicas de email personalizadas estão limitadas a 175 caracteres.

  - Enquanto o Exchange 2010 seria popular dicas de email na íntegra, Exchange 2013 só exibirá até 1000 caracteres.

  - Se o remetente começar a redigir uma mensagem e deixá-la aberta por um longo período, as Dicas de email de Respostas automáticas e de Caixa de correio cheia serão avaliadas a cada duas horas.

