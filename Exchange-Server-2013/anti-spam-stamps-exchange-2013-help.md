---
title: 'Carimbos anti-spam: Exchange 2013 Help'
TOCTitle: Carimbos anti-spam
ms:assetid: 28d3a5c2-8509-4b25-9876-763536e77c27
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Aa996878(v=EXCHG.150)
ms:contentKeyID: 50485198
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Carimbos anti-spam

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2016-12-09_

Carimbos antispam ajudam a diagnosticar problemas relacionados a spam através da aplicação de metadados de diagnóstico, ou carimbos, como informações específicas do remetente, resultados de validação do quebra-cabeça e resultados da filtragem de conteúdo, a mensagens na medida em que elas passam pelos recursos antispam que filtram mensagens de entrada provenientes da Internet. Existem três carimbos antispam: o carimbo de nível de confiança de phishing, o carimbo de nível de confiança de spam e o carimbo ID de Remetente.

Você pode usar os carimbos anti-spam como ferramentas de diagnóstico, para determinar as ações a serem tomadas, por ocasião de falsos positivos e de mensagens de spam suspeitas recebidas pelos usuários em suas caixas de correio.

## Exibir carimbos antispam

Você pode exibir os carimbos antispam usando o Microsoft Outlook. Para mais informações, consulte [Exibir carimbos de antispam no Outlook](view-anti-spam-stamps-in-outlook-exchange-2013-help.md).

## Noções básicas sobre o relatório antispam

O relatório antispam é um resumo dos resultados dos filtros antispam aplicados a um email. O agente do Filtro de Conteúdo aplica esse carimbo ao envelope da mensagem na forma de um Cabeçalho X, como descrito a seguir:

```powershell
    X-MS-Exchange-Organization-Antispam-Report: DV:<DATVersion>;CW:CustomList;PCL:PhishingVerdict <verdict>;P100:PhishingBlock;PP:Presolve;SID:SenderIDStatus <status>;TIME:<SendReceiveDelta>;MIME:MimeCompliance 
```

A tabela a seguir descreve as informações do filtro que podem constar em um relatório antispam.


> [!NOTE]
> O relatório anti-spam só exibe informações dos filtros aplicados à mensagem específica. Um relatório antispam geralmente não contém todas as informações listadas na tabela a seguir. Por exemplo, você pode receber o seguinte relatório antispam: <CODE>DV:3.1.3924.1409;SID:SenderIDStatus Fail;PCL:PhishingLevel SUSPICIOUS;CW:CustomList;PP:Presolved;TIME:TimeBasedFeatures</CODE>.



### Informações de filtro em um relatório antispam

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Carimbo</th>
<th>Descrição</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>SID</p></td>
<td><p>O carimbo ID de Remetente (SID) se baseia na estrutura de política de remetente (SPF) que autoriza o uso de domínios em emails. A SPF é exibida no envelope da mensagem como <code>Received-SPF</code>. O processo de avaliação do ID de Remetente cria um status do ID do Remetente para a mensagem. Esse status pode ser retornado como um dos seguintes valores:</p>
<ul>
<li><p><strong>Aprovado</strong>    Tanto o Endereço IP quanto o PRA (Endereço Responsável pela Expressão) passaram pela verificação da ID do Remetente.</p></li>
<li><p><strong>Neutro</strong>   Os dados publicados da ID do Remetente são explicitamente inconclusos.</p></li>
<li><p><strong>Falha suave</strong>   O endereço IP do PRA pode fazer parte do conjunto de não-permitidos.</p></li>
<li><p><strong>Reprovado</strong>   O endereço IP não é permitido; nenhum PRA foi encontrado no email de entrada ou o domínio de envio não existe.</p></li>
<li><p><strong>None</strong>   Não existem dados de SPF publicados no DNS do remetente.</p></li>
<li><p><strong>TempError</strong>   Ocorreu uma falha de DNS temporária, como um servidor DNS indisponível.</p></li>
<li><p><strong>PermError</strong> A gravação de DNS é inválida, como um erro no formato de gravação.</p></li>
</ul>
<p>O carimbo ID de Remetente é exibido como um Cabeçalho X no envelope da mensagem, da seguinte forma:</p>

```powershell
X-MS-Exchange-Organization-SenderIdResult:<status>
```

<p>Para obter mais informações sobre ID de Remetente, consulte <a href="sender-id-exchange-2013-help.md">ID de remetente</a>.</p></td>
</tr>
<tr class="even">
<td><p>DV</p></td>
<td><p>O carimbo DV (versão DAT) indica a versão do arquivo de definição de spam usado ao verificar a mensagem.</p></td>
</tr>
<tr class="odd">
<td><p>SA</p></td>
<td><p>O carimbo SA (ação de assinatura) indica que a mensagem foi recuperada ou excluída por causa de uma assinatura encontrada na mensagem.</p></td>
</tr>
<tr class="even">
<td><p>SV</p></td>
<td><p>O carimbo SV (versão DAT de assinatura) indica a versão do arquivo de assinatura usado ao verificar a mensagem.</p></td>
</tr>
<tr class="odd">
<td><p>PCL</p></td>
<td><p>O carimbo de nível de confiança de phishing (PCL) mostra a classificação da mensagem, com base em seu conteúdo, e é aplicado quando a mensagem é processada pelo agente Filtro de Conteúdo. Esse status pode ser retornado como um dos seguintes valores:</p>
<ul>
<li><p><strong>Neutral</strong>   O conteúdo da mensagem provavelmente não é phishing.</p></li>
<li><p><strong>Suspicious</strong>   O conteúdo da mensagem provavelmente é phishing.</p></li>
</ul>
<p>O valor do PCL pode variar de 1 a 8. Uma classificação de PCL de 1 a 3 retorna um status de <code>Neutral</code>. Isso significa que o conteúdo da mensagem provavelmente não é phishing. Uma classificação PCL de 4 a 8 retorna um status de <code>Suspicious</code>. Isso significa que a mensagem provavelmente é phishing.</p>
<p>Os valores são usados para determinar que ação o Outlook toma em relação às mensagens. O Outlook usa o carimbo PCL para bloquear o conteúdo de mensagens suspeitas.</p>
<p>O carimbo de PCL é exibido como um cabeçalho X no envelope da mensagem, como descrito a seguir:</p>

```powershell 
X-MS-Exchange-Organization-PCL:&lt;status&gt;
```
<tr class="even">
<td><p>SCL</p></td>
<td><p>O SCL (nível de confiança de spam) da mensagem exibe a classificação da mensagem, com base em seu conteúdo. O agente do Filtro de Conteúdo usa a tecnologia Microsoft SmartScreen para avaliar o conteúdo de uma mensagem e atribuir uma classificação SCL a cada mensagem. O valor de SCL está entre 0 e 9, em que 0 é considerado a menor probabilidade de spam e 9 é considerado a maior probabilidade de spam. As ações que o Exchange e o Outlook adotam dependem das configurações de limites de SCL.</p>
<p>Esse carimbo é exibido como um cabeçalho X no envelope da mensagem, como descrito a seguir:</p>

```powershell 
X-MS-Exchange-Organization-SCL
```
Para obter mais informações sobre ações e limites de SCL, consulte <a href="spam-confidence-level-threshold-exchange-2013-help.md">Limite do Nível de Confiança de Spam</a>.</p></td>
</tr>
<tr class="odd">
<td><p>CW</p></td>
<td><p>O carimbo de peso personalizado (CW) de uma mensagem indica que ela contém uma palavra ou frase não aprovada e que o respectivo valor de SCL (o &quot;peso&quot;) foi aplicado à pontuação final de SCL:</p>
<ul>
<li><p>Frases não aprovadas (ou expressões de bloqueio) têm peso máximo e alteram a pontuação de SCL para 9.</p></li>
<li><p>Palavras ou frases aprovadas (ou expressões de permissão) têm peso mínimo e alteram o SCL para 0.</p></li>
</ul>
<p>Para mais informações sobre como adicionar palavras ou frases aprovadas e não aprovadas ao agente Filtragem de Conteúdo, consulte <a href="manage-content-filtering-exchange-2013-help.md">Gerenciar filtragem de conteúdo</a>.</p></td>
</tr>
<tr class="even">
<td><p>PP</p></td>
<td><p>O carimbo quebra-cabeça pré-resolvido (PP) indica que, se a mensagem de um remetente contiver um carimbo postal computacional válido e resolvido, baseado na funcionalidade de validação de Carimbo Postal de Email do Outlook, é pouco provável que o remetente seja mal-intencionado. Nesse caso, o agente do Filtro de Conteúdo reduziria a classificação de SCL.</p>
<p>O agente Filtro de Conteúdo não altera a classificação de SCL se o recurso de validação de Marcação de Envio de Email estiver habilitado e uma das seguintes condições for verdadeira:</p>
<ul>
<li><p>Uma mensagem de entrada não contém um cabeçalho de carimbo postal computacional.</p></li>
<li><p>O cabeçalho de marcação de carimbo postal computacional não é válido.</p></li>
</ul>
<p>Para mais informações sobre o recurso de validação de marcação de envio, consulte <a href="content-filtering-exchange-2013-help.md">Filtragem de conteúdo</a>.</p></td>
</tr>
<tr class="odd">
<td><p>TIME:TimeBasedFeatures</p></td>
<td><p>O carimbo TIME indica que houve uma demora significativa entre a hora de envio e a hora de recebimento da mensagem. O carimbo TIME é usado para determinar a classificação final de SCL da mensagem.</p></td>
</tr>
<tr class="even">
<td><p>MIME:MIMECompliance</p></td>
<td><p>O carimbo MIME indica que o email não é compatível com MIME.</p></td>
</tr>
<tr class="odd">
<td><p>P100:PhishingBlock</p></td>
<td><p>O carimbo P100 indica que a mensagem contém uma URL presente em um arquivo de definição de phishing.</p></td>
</tr>
<tr class="even">
<td><p>IPOnAllowList</p></td>
<td><p>O carimbo IPOnAllowList indica que o endereço IP do remetente está na lista de Permissões de IP. Para mais informações sobre a Lista de IP Permitidos, consulte <a href="http://go.microsoft.com/fwlink/?linkid=268732">Noções Básicas Sobre Filtragem por Remetente</a>.</p></td>
</tr>
<tr class="odd">
<td><p>MessageSecurityAntispamBypass</p></td>
<td><p>O carimbo MessageSecurityAntispamBypass indica que o conteúdo da mensagem não foi filtrado e que o remetente recebeu permissão para ignorar os filtros antispam.</p></td>
</tr>
<tr class="even">
<td><p>SenderBypassed</p></td>
<td><p>O carimbo SenderBypassed indica que o agente Filtro de Conteúdo não processa qualquer filtragem de conteúdo de mensagens recebidas deste remetente. Para mais informações, consulte <a href="manage-content-filtering-exchange-2013-help.md">Gerenciar filtragem de conteúdo</a>.</p></td>
</tr>
<tr class="odd">
<td><p>AllRecipientsBypassed</p></td>
<td><p>O carimbo AllRecipientsBypassed indica que uma das seguintes condições foi atendida para todos os destinatários listados na mensagem:</p>
<ul>
<li><p>O parâmetro <em>AntispamBypassedEnabled</em> na caixa de correio do destinatário está definido como <code>$true</code>. Essa é uma configuração por destinatário que só pode ser definida por um administrador, usando o cmdlet <strong>Set-Mailbox</strong>.</p></li>
<li><p>O remetente da mensagem está na Lista de Remetentes Seguros do Outlook do destinatário. Para obter mais informações sobre a Lista de Remetentes Seguros, consulte <a href="manage-safelist-aggregation-exchange-2013-help.md">Gerenciar agregação de lista segura</a>.</p></li>
<li><p>O agente Filtro de Conteúdo não processa qualquer filtragem de conteúdo de mensagens enviadas a este destinatário. Para mais informações sobre exceções de destinatário, consulte <a href="manage-content-filtering-exchange-2013-help.md">Gerenciar filtragem de conteúdo</a>.</p></li>
</ul></td>
</tr>
</tbody>
</table>

