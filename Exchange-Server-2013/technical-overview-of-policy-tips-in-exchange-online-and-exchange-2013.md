---
title: 'Dicas de política: Exchange 2013 Help'
TOCTitle: Dicas de política
ms:assetid: 4266b83c-dd8a-4b3d-99ff-402e68fc810c
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/JJ150512(v=EXCHG.150)
ms:contentKeyID: 50484690
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Dicas de política

 

_**Aplica-se a:** Exchange Online, Exchange Server 2013_

_**Tópico modificado em:** 2015-07-22_

Você pode ajudar a impedir a sua organização Microsoft Outlook, Outlook Web App (OWA) e OWA para usuários de email de dispositivos inadequadamente enviando informações confidenciais através da criação de políticas de (DLP) de prevenção de perda de dados que incluem mensagens de notificação de *Dica de política* . Assim como as dicas de email que foram introduzidas no Microsoft Exchange Server 2010, mensagens de notificação de dica de política são exibidas aos usuários em Outlook enquanto eles estão redigindo uma mensagem de email. Mensagens de notificação de dica de política só aparecerão se algo sobre a mensagem de email do remetente parece violar uma política de DLP que você tem instalada e que a diretiva inclui uma regra para notificar o remetente quando as condições que você estabelece forem atendidas. Assista a este vídeo para saber mais.

> [!VIDEO https://www.microsoft.com/pt-br/videoplayer/embed/dd629bb7-063d-49f3-b7e1-8f2e0aa4de13]

Para mostrar Dicas de Política aos seus remetentes de e-mail, as suas regras devem incluir a ação **Notificar o remetente com uma Dica de Política**. Você pode adicionar isso ao editor de regras pelo Centro de Administração de Exchange. Para mais informações, consulte [Gerenciar dicas de política](how-to-configure-and-manage-policy-tips-a-dlp-feature-exchange.md).

O agente de regras de transporte que aplica as diretivas de DLP não faz diferenciação entre anexos de mensagens de e-mail, corpo do texto ou linhas de assunto ao avaliar as mensagens e as condições de suas diretivas. Por exemplo, se um usuário criar uma mensagem de email que inclua um número de cartão de crédito no corpo da mensagem e tentar enviá-la a um destinatário de fora da sua organização, uma mensagem de notificação de Dica de Política será exibida àquele usuário no Outlook ou no Outlook Web App, lembrando-o das expectativas de sua empresa para tais informações. Porém, esse tipo de notificação será exibido somente se você tiver configurado uma política de DLP que restrinja as ações descritas no exemplo, nesse caso, adicionando um alias de email externo ao cabeçalho de uma mensagem com dados de cartão de crédito. Há uma grande variedade de condições, ações e exceções que você pode escolher ao criar diretivas DLP. Essa variedade permite que você ajuste as suas ações de prevenção de perda de dados da maneira apropriada às necessidades específicas da sua organização.

Sempre que você usar a ação de notificar o remetente ou uma ação de substituição em uma regra, recomendamos que você também inclua a condição de que a mensagem foi envida da sua organização. Você pode fazer isso usando o editor de regras de política para adicionar a seguinte condição: **O remetente está localizado…** \> **dentro da organização**. Saiba mais sobre a alteração de políticas de DLP existentes em [Gerenciar políticas de DLP](manage-dlp-policies-exchange-2013-help.md). Essa é uma recomendação de prática porque a ação de notificar o remetente é aplicada como parte da sua experiência da criação de mensagem da sua empresa. Os remetentes mencionados pela ação são os autores das mensagens em sua empresa. A interação do usuário apresentada por Dicas de Política não pode ter ações de seus usuários para mensagens de entrada e será ignorada quando o remetente estiver localizado fora da sua organização. Você pode aplicar políticas DLP para verificar mensagens de entrada e tomar uma variedade de ações, mas, ao fazer isso, não adicione a ação de notificar o remetente.

Se os remetentes do email em sua organização que estiverem compondo uma mensagem forem avisados em tempo real sobre os padrões e expectativas da sua organização pelas notificações de Dica de Política, a probabilidade de que eles violem os padrões que sua organização quer aplicar será menor.


> [!TIP]
> <UL>
> <LI>
> <P>Exchange Online: DLP é um recurso premium que exige uma assinatura do Plano 2 do Exchange Online. Para saber mais, confira <A href="https://go.microsoft.com/fwlink/p/?linkid=286154">Licenciamento do Exchange Online</A>.</P>
> <LI>
> <P>Exchange 2013: DLP é um recurso premium que exige uma licença dos Serviços da Enterprise CAL do Exchange. Para saber mais sobre CALs e sobre licenciamento de servidor, confira o artigo <A href="https://go.microsoft.com/fwlink/p/?linkid=237292">Licenciamento do Exchange Server</A>.</P>
> <LI>
> <P>Se a sua organização estiver usando o Exchange 2013 SP1 ou o Exchange Online, as Dicas de Política estarão disponíveis para as pessoas que enviam email do Outlook 2013, do Outlook Web App ou do OWA para dispositivos. Se a sua organização estiver usando o Exchange 2013, as Dicas de Política estarão disponíveis para as pessoas que enviam email do Outlook 2013.</P></LI></UL>



## Texto padrão para Dicas de Política e opções de regras

Você tem uma variedade de opções possíveis ao adicionar regras de notificação para o remetente às diretivas DLP. Ao adicionar uma regra para notificar o remetente usando a ação **Notificar o remetente com uma Dica de Política** em uma política de DLP, você pode escolher o nível de restrição. As opções de notificação na tabela a seguir estão disponíveis. Para informações gerais sobre como editar diretivas, consulte [Gerenciar políticas de DLP](manage-dlp-policies-exchange-2013-help.md). Para obter informações específicas sobre como criar Dicas de Política, consulte [Gerenciar dicas de política](how-to-configure-and-manage-policy-tips-a-dlp-feature-exchange.md).


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Regra de notificação</th>
<th>Significado</th>
<th>Mensagem de notificação padrão de Dica de Política que os usuários do Outlook visualizarão</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>Apenas notificar</strong></p></td>
<td><p>De modo semelhante aos MailTips, isso gera uma mensagem de notificação de Dica de Política informativa sobre uma violação de diretiva. O remetente pode impedir que esse tipo de dica seja exibido usando uma caixa de diálogo de opções de Dicas de Política que pode ser acessada no Outlook.</p></td>
<td><p>Esta mensagem pode ter conteúdo confidencial. Todos os destinatários devem ser autorizados a receber este conteúdo.</p></td>
</tr>
<tr class="even">
<td><p><strong>Rejeitar mensagem</strong></p></td>
<td><p>A mensagem não será entregue até que a condição não esteja mais presente. O remetente recebe a opção de indicar que sua mensagem de e-mail não inclui conteúdo confidencial. Isso também é conhecido como uma sobreposição de falso positivo. Se o remetente indicar isso, o Outlook permitirá que a mensagem saia da caixa de saída para que o relatório do usuário seja auditado, mas o Exchange bloqueará o envio da mensagem.</p></td>
<td><p>Esta mensagem pode ter conteúdo confidencial. Sua organização não irá permitir que essa mensagem seja enviada até que o conteúdo seja removido.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Rejeitar exceto em caso de sobreposição de falso positivo</strong></p></td>
<td><p>O resultado dessa regra de notificação é semelhante ao da regra de notificação <strong>Rejeitar mensagem</strong>. Porém, se você selecionar essa regra, o Exchange permitirá que a mensagem seja enviada ao destinatário pretendido em vez de bloquear a mensagem.</p></td>
<td><p><strong>Antes de o remetente selecionar uma opção para sobrepor:</strong> Essa mensagem pode ter conteúdo confidencial. Sua organização não irá permitir que essa mensagem seja enviada até que o conteúdo seja removido.</p>
<p><strong>Depois que o remetente selecionar uma substituição de opção:</strong> O seu comentário será enviado ao seu administrador quando a mensagem for enviada.</p></td>
</tr>
<tr class="even">
<td><p><strong>Rejeitar exceto em caso de sobreposição silenciosa</strong></p></td>
<td><p>A mensagem não será entregue até que a condição não esteja mais presente ou o remetente indique uma sobreposição. O remetente receberá a opção de indicar que ele deseja sobrepor a diretiva.</p></td>
<td><p><strong>Antes de o remetente selecionar uma opção para sobrepor:</strong> Essa mensagem pode ter conteúdo confidencial. Sua organização não irá permitir que essa mensagem seja enviada até que o conteúdo seja removido.</p>
<p><strong>Depois que o remetente selecionar uma substituição de opção:</strong> Você substituiu a política de conteúdo confidencial da sua organização nesta mensagem. Sua ação será auditada pela organização.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Rejeitar exceto em caso de sobreposição explícita</strong></p></td>
<td><p>O resultado desta regra de notificação é semelhante ao da regra de notificação <strong>Rejeitar exceto em caso de sobreposição silenciosa</strong> exceto que neste caso, quando o remetente tenta sobrepor a diretiva, ele deve fornecer uma justificativa para sobrepor a diretiva.</p></td>
<td><p><strong>Antes de o remetente selecionar uma opção para sobrepor:</strong> Essa mensagem pode ter conteúdo confidencial. Sua organização não irá permitir que essa mensagem seja enviada até que o conteúdo seja removido.</p>
<p><strong>Depois que o remetente selecionar uma substituição de opção:</strong> Você substituiu a política de conteúdo confidencial da sua organização nesta mensagem. Sua ação será auditada pela organização.</p></td>
</tr>
</tbody>
</table>


## Personalizar suas mensagens de notificação de dica de política

Para personalizar o texto de uma notificação de dica de política que os remetentes de email vê no seu programa de email, selecione **Gerenciar dicas de política**, na página de prevenção de perda de dados. Na ordem de qualquer um dos seu texto personalizado para aparecer, uma regra de política DLP deve incluir a ação **notificar o remetente com uma dica de política**. Adicione a ação a uma regra usando o editor de regras DLP.

Para obter os procedimentos que explicam como criar suas próprias dicas de política, consulte [Gerenciar dicas de política](how-to-configure-and-manage-policy-tips-a-dlp-feature-exchange.md). O texto personalizado que você criar pode substituir o texto padrão mostrado na tabela anterior.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Configurações e ações de notificação de dica de política</th>
<th>Significado</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>Notificar o remetente</strong></p></td>
<td><p>O texto aparece somente quando uma ação <strong>notificar o remetente, mas permitir que eles enviem</strong> é iniciada.</p></td>
</tr>
<tr class="even">
<td><p><strong>Permitir que o remetente substitua</strong></p></td>
<td><p>O texto aparece somente quando as seguintes ações são iniciadas: <strong>Bloquear a mensagem, a menos que ele seja um falso positivo</strong>, <strong>Bloquear a mensagem, mas permitir que o remetente sobreponha e envie</strong>.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Bloquear a mensagem</strong></p></td>
<td><p>O texto aparece somente quando uma ação <strong>Bloquear a mensagem</strong> é iniciada.</p></td>
</tr>
<tr class="even">
<td><p><strong>Link para URL de conformidade</strong></p></td>
<td><p>A URL de conformidade é um link para uma página da web onde você pode explicar a conformidade e políticas de substituição. Este link é exibido na dica de política, quando um usuário clica no link <strong>mais detalhes</strong>.</p></td>
</tr>
</tbody>
</table>


## Para obter mais informações

[Prevenção de perda de dados](technical-overview-of-dlp-data-loss-prevention-in-exchange.md)

[Gerenciar políticas de DLP](manage-dlp-policies-exchange-2013-help.md)

[Gerenciar dicas de política](how-to-configure-and-manage-policy-tips-a-dlp-feature-exchange.md)

