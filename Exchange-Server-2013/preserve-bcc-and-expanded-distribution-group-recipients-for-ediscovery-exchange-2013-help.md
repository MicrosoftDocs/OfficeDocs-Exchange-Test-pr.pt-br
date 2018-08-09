---
title: 'Manter Cco e destinatários do grupo de distribuição expandido para eDiscovery'
TOCTitle: Preservar Cco e os destinatários do grupo de distribuição expandido para eDiscovery
ms:assetid: eb8ddf15-0080-457e-9d83-e73e193da334
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Dn770225(v=EXCHG.150)
ms:contentKeyID: 62516663
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Preservar Cco e os destinatários do grupo de distribuição expandido para eDiscovery

 

_**Aplica-se a:** Exchange Online, Exchange Server 2013, Office 365 Enterprise_

_**Tópico modificado em:** 2017-06-19_

Bloqueio in-loco, retenção de litígio e [políticas de retenção do Office 365](http://go.microsoft.com/fwlink/?linkid=827811) (criados no Centro de Conformidade e Segurança do Office 365 ) permitem que você preserve conteúdo de caixa de correio para atender aos requisitos de descoberta eletrônica e de conformidade a normas. Informações sobre destinatários endereçada diretamente em para e Cc campos de uma mensagem é incluída em todas as mensagens por padrão, mas sua organização pode exigir a capacidade de pesquisar e reproduza detalhes sobre todos os destinatários de uma mensagem. Isso inclui:

  - **Destinatários endereçados utilizando o campo Cco de uma mensagem**   Destinatários Cco são armazenados na mensagem na caixa de correio do remetente, mas não são incluídos em cabeçalhos da mensagem entregue aos destinatários.

  - **Destinatários do grupo de distribuição expandido**   Destinatários que a mensagem porque eles são membros de um grupo de distribuição para o qual a mensagem foi tratada, tanto em para, Cc ou Cco campos.

Exchange Online e Exchange Server 2013 (atualização cumulativa 7 e versões posteriores) mantêm informações sobre Cco e os destinatários do grupo de distribuição expandido. Você pode procurar essas informações usando uma pesquisa de descoberta eletrônica In-loco no Centro de administração do Exchange (EAC) ou uma pesquisa de conteúdo no Centro de Conformidade e Segurança.

## Como destinatários Cco e os destinatários do grupo de distribuição expandido são preservados

Conforme mencionado anteriormente, as informações sobre destinatários Bcc'ed serão armazenadas com a mensagem na caixa de correio do remetente. Essa informação é indexada e disponíveis para pesquisas de descoberta eletrônica e retenções.

Informações sobre os destinatários do grupo de distribuição expandido são armazenadas com a mensagem após colocar uma caixa de correio em bloqueio In-loco ou retenção de litígio. Office 365, essas informações também são armazenadas quando uma política de retenção Office 365 é aplicada a uma caixa de correio. A associação ao grupo de distribuição é determinada no momento em que a mensagem é enviada. A lista de destinatários expandida armazenada com a mensagem não é afetada pelas alterações à associação do grupo, depois que a mensagem é enviada.


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Informações sobre...</th>
<th>É armazenado no …</th>
<th>São armazenadas por padrão?</th>
<th>É acessível aos …</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Para e Cc destinatários</p></td>
<td><p>Propriedades de mensagem no remetente e caixas de correio dos destinatários.</p></td>
<td><p>Sim</p></td>
<td><p>Oficiais de conformidade de remetente e destinatários</p></td>
</tr>
<tr class="even">
<td><p>Destinatários Cco</p></td>
<td><p>Propriedade de mensagem na caixa de correio do remetente.</p></td>
<td><p>Sim</p></td>
<td><p>Oficiais de conformidade e de remetente</p></td>
</tr>
<tr class="odd">
<td><p>Destinatários do grupo de distribuição expandido</p></td>
<td><p>Propriedades da mensagem na caixa de correio do remetente.</p></td>
<td><p>Não. Informações de destinatário de grupo de distribuição expandido são armazenadas após uma caixa de correio for colocada em retenção In-loco ou retenção de litígio ou atribuídas a uma política de retenção Office 365.</p></td>
<td><p>Oficiais de conformidade</p></td>
</tr>
</tbody>
</table>


## Procurando por mensagens enviadas para Cco e os destinatários do grupo de distribuição expandido

Ao procurar por mensagens enviadas para um destinatário, os resultados da pesquisa de descoberta eletrônica agora incluem mensagens enviadas a um grupo de distribuição que o destinatário é um membro de. A tabela a seguir mostra os cenários em que as mensagens enviadas para Cco e os destinatários do grupo de distribuição expandido são retornadas em pesquisas de descoberta eletrônica.

Cenário 1: John é um membro do grupo de distribuição de vendas dos EUA. Esta tabela mostra os resultados da pesquisa de descoberta eletrônica quando Bob envia uma mensagem para John direta ou indiretamente por meio de um grupo de distribuição.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Quando você pesquisa de caixa de correio de Bob para mensagens enviadas …</th>
<th>E a mensagem é enviada com …</th>
<th>Os resultados incluem mensagem?</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Como: John</p></td>
<td><p>John logon em</p></td>
<td><p>Sim</p></td>
</tr>
<tr class="even">
<td><p>Como: John</p></td>
<td><p>US-Sales logon em</p></td>
<td><p>Sim</p></td>
</tr>
<tr class="odd">
<td><p>Como: vendas dos EUA</p></td>
<td><p>US-Sales logon em</p></td>
<td><p>Sim</p></td>
</tr>
<tr class="even">
<td><p>Cc:John</p></td>
<td><p>John em CC</p></td>
<td><p>Sim</p></td>
</tr>
<tr class="odd">
<td><p>Cc:John</p></td>
<td><p>US-vendas em CC</p></td>
<td><p>Sim</p></td>
</tr>
<tr class="even">
<td><p>Cc:US-vendas</p></td>
<td><p>US-vendas em CC</p></td>
<td><p>Sim</p></td>
</tr>
</tbody>
</table>


Cenário 2: Bob envia um email para John (para / Cc) e a tomada (diretamente, Cco ou indiretamente por meio de um grupo de distribuição). A tabela a seguir mostra os resultados da pesquisa de descoberta eletrônica.


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Quando você pesquisa …</th>
<th>Para mensagens enviadas …</th>
<th>Os resultados incluem mensagem?</th>
<th>Observações</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Caixa de correio de Bob</p></td>
<td><p>Para / Cc:John</p></td>
<td><p>Sim</p></td>
<td><p>Apresenta uma indicação de que o conector foi Bcc'ed.</p></td>
</tr>
<tr class="even">
<td><p>Caixa de correio de Bob</p></td>
<td><p>BCC:Jack</p></td>
<td><p>Sim</p></td>
<td><p>Apresenta uma indicação de que o conector foi Bcc'ed.</p></td>
</tr>
<tr class="odd">
<td><p>Caixa de correio de Bob</p></td>
<td><p>BCC:Jack (por meio do grupo de distribuição)</p></td>
<td><p>Sim</p></td>
<td><p>Lista de membros do grupo de distribuição Bcc'ed expandidos quando a mensagem foi enviada, é visível em logs, a exportação e a visualização da pesquisa de descoberta eletrônica.</p></td>
</tr>
<tr class="even">
<td><p>Caixa de correio de John</p></td>
<td><p>Para / Cc:John</p></td>
<td><p>Sim</p></td>
<td><p>Nenhuma indicação de destinatários Cco.</p></td>
</tr>
<tr class="odd">
<td><p>Caixa de correio de John</p></td>
<td><p>BCC:Jack (diretamente ou por meio da distribuição de grupo)</p></td>
<td><p>Não</p></td>
<td><p>Informações de Cco não são armazenadas na mensagem entregue aos destinatários. Você deve pesquisar a caixa de correio do remetente.</p></td>
</tr>
<tr class="even">
<td><p>Caixa de correio de tomada.</p></td>
<td><p>Para / Cc:John (diretamente ou por meio da distribuição de grupo)</p></td>
<td><p>Sim</p></td>
<td><p>Para / Cc informações são incluídas na mensagem entregue a todos os destinatários.</p></td>
</tr>
<tr class="odd">
<td><p>Caixa de correio de tomada.</p></td>
<td><p>BCC:Jack (diretamente ou por meio da distribuição de grupo)</p></td>
<td><p>Não</p></td>
<td><p>Informações de Cco não são armazenadas na mensagem entregue aos destinatários. Você deve pesquisar a caixa de correio do remetente.</p></td>
</tr>
</tbody>
</table>


## Perguntas frequentes

**P. quando e onde são armazenadas as informações de destinatário Cco?**  
Informações do destinatário Cco r. são preservadas por padrão na mensagem original na caixa de correio do remetente. Se o destinatário Cco for um grupo de distribuição, a associação de grupo de distribuição é expandida se a caixa de correio do remetente está em retenção ou atribuída a uma política de retenção Office 365 somente.

**P. quando e onde está a lista de distribuição expandido destinatários do grupo armazenados?**  
a associação ao grupo de r. é expandida no momento em que a mensagem é enviada. A lista de membros do grupo de distribuição expandido é armazenada na mensagem original na caixa de correio do remetente. Caixa de correio do remetente deve estar em bloqueio In-loco, retenção de litígio, ou atribuído a uma política de retenção Office 365.

**P. pode para / destinatários Cc consulte quais destinatários foram Bcc'ed?**  
Não a.... Essas informações não estão incluídas nos cabeçalhos de mensagem e não são visíveis para / Cc os destinatários. O remetente pode ver o campo Cco armazenado na mensagem original armazenada em suas caixas de correio. Oficiais de conformidade podem ver essa informação ao pesquisar a caixa de correio do remetente.

**P. como garantir os destinatários do grupo de distribuição expandido sempre são preservados?**  
A. Para garantir que membros do grupo de distribuição expandido sempre são preservados com uma mensagem, [Colocar todas as caixas de correio em espera](place-all-mailboxes-on-hold-exchange-2013-help.md) ou criar uma política de retenção de toda a organização Office 365.

**P. quais tipos de grupos são suportados?**  
Grupos de distribuição A., grupos de segurança habilitados para email e grupos dinâmicos de distribuição são suportados.

**P. existe um limite no número de distribuição destinatários do grupo que são expandidos e armazenados na mensagem?**  
R. até 10.000 membros de um grupo de distribuição é preservado.

**P. são aninhadas grupos de distribuição suportados?**  
A. Sim, 25 níveis de grupos de distribuição aninhados são expandidos.

**P. qual é a Cco e a distribuição expandido agrupa informações do destinatário visíveis?**  
Destinatários do grupo de distribuição expandido e Cco r. informações são visíveis para oficiais de conformidade ao executar uma pesquisa de descoberta eletrônica. Cco e os destinatários do grupo de distribuição expandido são incluídos nos resultados de pesquisa copiados para uma caixa de correio de descoberta ou exportado para um arquivo PST e no log de descoberta eletrônica incluído nos resultados da pesquisa. Informações do destinatário Cco também estão disponíveis na visualização da pesquisa.

**P. o que acontece se um membro de um grupo de distribuição é oculto da lista de endereços global (GAL) da organização?**  
Nenhum impacto do r. lá. Se os destinatários estiverem ocultos da GAL, eles ainda estiver incluídos na lista de destinatários para o grupo de distribuição expandido.

