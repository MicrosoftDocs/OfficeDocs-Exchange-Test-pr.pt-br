---
title: 'Criar relatórios de incidentes de detecção de política DLP: Exchange 2013 Help'
TOCTitle: Criar relatórios de incidentes para detecções de política DLP
ms:assetid: 8e807f94-384c-43f5-be6f-06c5587175a0
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/JJ150534(v=EXCHG.150)
ms:contentKeyID: 50484749
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Criar relatórios de incidentes para detecções de política DLP

 

_**Aplica-se a:** Exchange Online, Exchange Server 2013_

_**Tópico modificado em:** 2015-04-07_

Em Exchange Server 2013, é possível estabelecer uma ação para criar um relatório de incidente dentro de um conjunto de regras de política DLP. Além disso, você pode indicar a quem o relatório deve ser enviado e o que fazer com a mensagem original. O relatório de incidente pode conter qualquer uma das seguintes informações.

## Conteúdo de um relatório de incidentes de gerenciamento

A ação de **Gerar relatório de incidente** permite que os usuários desejam enviar relatórios de incidentes para uma caixa de correio de gerenciamento de incidentes. Será gerado um relatório de incidente único para cada mensagem somente se a ação de **Gerar relatório de incidente** é aplicada dentro de uma diretiva.

O exemplo a seguir é uma lista completa dos nomes de linha no modelo de relatório de incidente. A coluna do formato descreve como reconhecer cada campo no relatório. A coluna de campo opcional especifica quais campos podem não estar no relatório para cada correspondência de regra. A coluna específica de DLP mostra quais campos existir como resultado do recurso DLP.


<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p><strong>Linha</strong> <strong>nome</strong></p></td>
<td><p><strong>Descrição</strong></p></td>
<td><p><strong>Formato</strong></p></td>
<td><p><strong>Campo opcional</strong></p></td>
<td><p><strong>DLP específico</strong></p></td>
</tr>
<tr class="even">
<td><p>Id da mensagem</p></td>
<td><p>ID da mensagem enviada original</p></td>
<td><p>Id da mensagem: O ID da mensagem</p></td>
<td><p>Obrigatório</p></td>
<td><p>Não</p></td>
</tr>
<tr class="odd">
<td><p>Sender</p></td>
<td><p>True remetente da mensagem original</p></td>
<td><p>Remetente: Endereço do remetente de Email</p></td>
<td><p>Obrigatório</p></td>
<td><p>Não</p></td>
</tr>
<tr class="even">
<td><p>Subject</p></td>
<td><p>Assunto da mensagem original</p></td>
<td><p>Assunto: cadeia de caracteres de assunto de entrada do usuário final</p></td>
<td><p>Obrigatório</p></td>
<td><p>Não</p></td>
</tr>
<tr class="odd">
<td><p>To</p></td>
<td><p>Destinatário ou destinatários da mensagem original</p>
<p>Cada um da linha conterá apenas um único destinatário e pode haver até 10 destinatários exibidos no relatório de incidente. Se houver destinatários adicionais, a próxima linha exibirá o número restante de destinatários.</p></td>
<td><p>Para: O endereço de Email do destinatário</p></td>
<td><p>Obrigatório</p></td>
<td><p>Não</p></td>
</tr>
<tr class="even">
<td><p>CC</p></td>
<td><p>Endereço de email CC da mensagem original; a linha é opcional</p>
<p>Cada linha CC conterá apenas um único endereço de email CC e só pode haver até 10 endereços de email CC que são exibidos no relatório de incidente. Se houver endereços adicionais de CC, a próxima linha CC exibirá o número restante de endereços de email CC.</p></td>
<td><p>CC: O endereço de Email do destinatário CC</p></td>
<td><p>Opcional</p></td>
<td><p>Não</p></td>
</tr>
<tr class="odd">
<td><p>CCO</p></td>
<td><p>Endereço de email Cco da mensagem original; a linha é opcional</p>
<p>Cada linha Cco conterá apenas um único endereço de email Cco e só pode haver até 10 endereços Cco que são exibidos no relatório de incidente. Se houver endereços de email adicionais Cco, a seguinte linha Cco exibirá o número restante de endereços de email Cco.</p></td>
<td><p>Cco: Endereço de Email do destinatário Cco</p></td>
<td><p>Opcional</p></td>
<td><p>Não</p></td>
</tr>
<tr class="even">
<td><p>Gravidade</p></td>
<td><p>Gravidade da regra de visitas; auditoria Exibe a gravidade mais alta se várias regras foram atingidas.</p></td>
<td><p>Gravidade: Baixa, média ou alta</p></td>
<td><p>Opcional</p></td>
<td><p>Não</p></td>
</tr>
<tr class="odd">
<td><p>Override</p></td>
<td><p>Exibe se uma substituição foi relatada para a mensagem e a justificação da substituição de caso seja fornecido.</p></td>
<td><p>Substituição: Sim, justificativa: cadeia de caracteres de justificativa de entrada do operador de informações</p></td>
<td><p>Opcional</p></td>
<td><p>Sim</p></td>
</tr>
<tr class="even">
<td><p>Falso positivo</p></td>
<td><p>Exibe se um falso positivo foi relatado para a mensagem.</p></td>
<td><p>Falso positivo: Sim</p></td>
<td><p>Opcional</p></td>
<td><p>Sim</p></td>
</tr>
<tr class="odd">
<td><p>Classificação de dados</p></td>
<td><p>Classificações de dados detectados encontradas na mensagem original; a linha é opcional.</p>
<p>Cada linha de classificação de dados conterá apenas um único detectada classificação junto com seu contagem, confiança e nível de confiança mínimo recomendado. Até 5 classificações detectadas será exibido no relatório de incidente. Se a classificação detectada foi uma afinidade, o valor de count não se aplica e não será mostrado.</p></td>
<td><p>Classificação de dados: tipo de informação confidencial, contagem: instâncias das informações confidenciais encontradas na mensagem, confiança: valor de porcentagem, confiança de mínimo recomendado: valor de porcentagem</p></td>
<td><p>Opcional</p></td>
<td><p>Sim</p></td>
</tr>
<tr class="even">
<td><p>Acerto de regra</p></td>
<td><p>Exibe todas as regras que chegam a mensagem original.</p>
<p>Inclui o nome da regra que foi atingido, a política de DLP (opcional) se a regra reside, as ações que foram feitas na mensagem devido a regra, classification(s) de dados na regra que causou a regra de visitas e a definição da regra.</p></td>
<td><p>Acerto de regra: o nome da regra, política de DLP: nome de política de DLP, se aplicável, ação: único de ação, a classificação de dados: tipo de informação confidencial, definição: definição de regra, se aplicável</p></td>
<td><p>Obrigatório</p></td>
<td><p>Não</p></td>
</tr>
<tr class="odd">
<td><p>ID de correspondência</p></td>
<td><p>Exibe a classificação de dados correspondentes, o conteúdo correspondente exato da mensagem e a evidência principal da correspondência de classificação de dados; a linha é opcional.</p></td>
<td><p>ID de correspondência: tipo de informação confidencial, valor: valor real dos dados confidenciais, contexto: texto ao redor dos dados confidenciais na mensagem</p></td>
<td><p>Opcional</p></td>
<td><p>Sim</p></td>
</tr>
</tbody>
</table>


## Para obter mais informações

[Exibir relatórios de detecção de política DLP](view-dlp-policy-detection-reports-exchange-2013-help.md)

[Prevenção de perda de dados](technical-overview-of-dlp-data-loss-prevention-in-exchange.md)

