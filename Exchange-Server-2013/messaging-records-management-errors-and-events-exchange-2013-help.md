---
title: 'Eventos e erros mensagens de gerenciamento de registros: Exchange 2013 Help'
TOCTitle: Eventos e erros mensagens de gerenciamento de registros
ms:assetid: 8bc3f5ae-403b-45af-86c1-b2fccab34e63
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Bb310783(v=EXCHG.150)
ms:contentKeyID: 51407888
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Eventos e erros mensagens de gerenciamento de registros

 

_**Aplica-se a:**Exchange Server 2013_

_**Tópico modificado em:**2015-03-09_

Gerenciamento de registros de mensagens (MRM) gera eventos que você pode exibir no Visualizador de eventos. Isso permite que você a solucionar problemas e verificar o desempenho do Assistente de pasta gerenciada. Visualizador de eventos rastreia os seguintes tipos de eventos na seguinte ordem, com base na prioridade:

1.  Eventos de erro

2.  Eventos de aviso

3.  Eventos informativos

## Eventos e erros MRM

As tabelas a seguir fornecem listas de eventos que você pode usar para solucionar problemas de MRM. Os tipos de log incluem o seguinte:

  - Eventos rotulados como **LogAlways** sempre são registrados individualmente.

  - Eventos rotulados como **LogPeriodic** são registrados somente uma vez em qualquer período de cinco minutos, não toda vez que ocorrem. Isso ajuda a impedir que as entradas de log excessivo.

### Eventos MRM na categoria de Assistente de pasta gerenciada

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
<th><strong>ID do Evento</strong></th>
<th><strong>Categoria</strong></th>
<th><strong>Tipo de evento</strong></th>
<th><strong>Log</strong></th>
<th><strong>Valor ou descrição</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>10003</p></td>
<td><p>Assistente de Pasta Gerenciada</p></td>
<td><p>Erro</p></td>
<td><p>LogPeriodic</p></td>
<td><p>Não pôde obter o servidor de objeto de configuração de Active Directory. &lt;<em>Exception details</em>&gt;. Verifique se há problemas de conectividade de rede de controlador de domínio ou configuração DNS incorreta.</p></td>
</tr>
<tr class="even">
<td><p>10004</p></td>
<td><p>Assistente de Pasta Gerenciada</p></td>
<td><p>Erro</p></td>
<td><p>LogAlways</p></td>
<td><p>A política de retenção para a pasta &lt;<em>folder</em>&gt; na caixa de correio &lt;<em>mailbox</em>&gt; não será aplicada. O Assistente de pasta gerenciada não é possível processar a configuração de conteúdo gerenciada &lt;<em>content setting</em>&gt; para a pasta gerenciada &lt;<em>managed folder</em>&gt;. O RetentionAction é MoveToFolder, mas uma pasta de destino não foi especificada. Especifique uma pasta de destino.</p></td>
</tr>
<tr class="odd">
<td><p>10005</p></td>
<td><p>Assistente de Pasta Gerenciada</p></td>
<td><p>Erro</p></td>
<td><p>LogAlways</p></td>
<td><p>Política de retenção não será aplicada à pasta &lt;<em>folder</em>&gt; na caixa de correio &lt;<em>mailbox</em>&gt;. Não é possível processar a configuração de conteúdo gerenciado &lt;<em>content setting</em>&gt; para a pasta gerenciada &lt;<em>managed folder</em>&gt;. O RetentionAction é MoveToFolder, mas a pasta de destino &lt;<em>folder</em>&gt; é o mesmo que a pasta de origem &lt;<em>folder</em>&gt;. Especifique uma pasta de destino é diferente da pasta de origem.</p></td>
</tr>
<tr class="even">
<td><p>10009</p></td>
<td><p>Assistente de Pasta Gerenciada</p></td>
<td><p>Erro</p></td>
<td><p>LogAlways</p></td>
<td><p>O Assistente de pasta gerenciada ignorados processamento de todos os bancos de dados no servidor local, pois ele não pôde ler os parâmetros do log de auditoria do Active Directory. Ele tentará novamente mais tarde na janela de agendamento. Banco de dados atual: &lt;<em>database</em>&gt;</p></td>
</tr>
<tr class="odd">
<td><p>10010</p></td>
<td><p>Assistente de Pasta Gerenciada</p></td>
<td><p>Erro</p></td>
<td><p>LogAlways</p></td>
<td><p>O Assistente de pasta gerenciada ignorados processamento de todos os bancos de dados no servidor local, pois o log de auditoria está habilitado, mas o caminho para o log de auditoria está ausente no Active Directory. Ele tentará novamente mais tarde na janela de agendamento. Banco de dados atual: &lt;<em>database</em>&gt;</p></td>
</tr>
<tr class="even">
<td><p>10011</p></td>
<td><p>Assistente de Pasta Gerenciada</p></td>
<td><p>Erro</p></td>
<td><p>LogAlways</p></td>
<td><p>O Assistente de pasta gerenciada não pôde configurar o log de auditoria. Ele irá parar o processamento de banco de dados atual: '%1'. Ele tentará novamente mais tarde na janela de agendamento. Detalhes da exceção: &lt;<em>details</em>&gt;</p></td>
</tr>
<tr class="odd">
<td><p>10012</p></td>
<td><p>Assistente de Pasta Gerenciada</p></td>
<td><p>Erro</p></td>
<td><p>LogAlways</p></td>
<td><p>O Assistente de pasta gerenciada não gravar no log de auditoria. Ele irá parar o processamento de banco de dados atual: &lt;<em>database</em>&gt;. Ele tentará gravar no log de auditoria novamente mais tarde na janela de agendamento. Detalhes da exceção: &lt;<em>details</em>&gt;</p></td>
</tr>
<tr class="even">
<td><p>10017</p></td>
<td><p>Assistente de Pasta Gerenciada</p></td>
<td><p>Erro</p></td>
<td><p>LogAlways</p></td>
<td><p>Ocorreu uma exceção no Assistente de pasta gerenciada enquanto ele estava processando a caixa de correio: &lt;<em>mailbox</em>&gt; pasta: nome: &lt;<em>folder name</em>&gt; Id: &lt;<em>folder ID</em>&gt; Item: Ids: &lt;<em>IDs</em>&gt;. Exceção: &lt;<em>exception</em>&gt;.</p></td>
</tr>
</tbody>
</table>


### Eventos MRM na categoria assistentes

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
<th><strong>ID do Evento</strong></th>
<th><strong>Categoria</strong></th>
<th><strong>Tipo de evento</strong></th>
<th><strong>Log</strong></th>
<th><strong>Valor ou descrição</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>9004</p></td>
<td><p>Assistentes</p></td>
<td><p>Aviso</p></td>
<td><p>LogAlways</p></td>
<td><p>Serviço &lt;<em>service</em>&gt;. &lt;<em>service</em>&gt; falhou ao processar a caixa de correio &lt;<em>mailbox</em>&gt;. A seguinte exceção causou a falha: &lt;<em>exception</em>&gt;</p></td>
</tr>
<tr class="even">
<td><p>9014</p></td>
<td><p>Assistentes</p></td>
<td><p>Aviso</p></td>
<td><p>LogAlways</p></td>
<td><p>Serviço &lt;<em>service</em>&gt;. Não é possível processar alterações na agenda. A seguinte exceção causou a falha: &lt;<em>exception</em>&gt;</p></td>
</tr>
<tr class="odd">
<td><p>9017</p></td>
<td><p>Assistentes</p></td>
<td><p>Informações</p></td>
<td><p>LogAlways</p></td>
<td><p>Serviço &lt;<em>service</em>&gt;. &lt;<em>service</em>&gt; para o banco de dados &lt;<em>database</em>&gt; está inserindo uma janela de horário agendado. Há &lt;<em>number</em>&gt; caixas de correio para processar.</p></td>
</tr>
<tr class="even">
<td><p>9018</p></td>
<td><p>Assistentes</p></td>
<td><p>Informações</p></td>
<td><p>LogAlways</p></td>
<td><p>Serviço &lt;<em>service</em>&gt;. &lt;<em>service</em>&gt; para o banco de dados &lt;<em>database</em>&gt; está deixando uma janela de horário agendado. &lt;<em>number</em>&gt; sem &lt;<em>number</em>&gt; caixas de correio foram processadas com êxito. &lt;<em>number</em>&gt; caixas de correio foram ignoradas devido a erros. &lt;<em>number</em>&gt; caixas de correio foram processadas separadamente. &lt;<em>number</em>&gt; caixas de correio não foram processadas devido ao tempo insuficiente.</p>

> [!TIP]
> Assistente de pasta gerenciada voltarão onde ela parou na próxima vez que ele é executado.


</td>
</tr>
<tr class="odd">
<td><p>9019</p></td>
<td><p>Assistentes</p></td>
<td><p>Aviso</p></td>
<td><p>LogPeriodic</p></td>
<td><p>Serviço &lt;<em>service</em>&gt;. Não é possível salvar o andamento para &lt;<em>service</em>&gt; no banco de dados &lt;<em>database</em>&gt;. (O assistente foi capaz de salvar onde ela parou de forma que poderia retomar lá quando ele for reiniciado.) A seguinte exceção causou a falha: &lt;<em>exception</em>&gt;</p></td>
</tr>
<tr class="even">
<td><p>9020</p></td>
<td><p>Assistentes</p></td>
<td><p>Aviso</p></td>
<td><p>LogAlways</p></td>
<td><p>Serviço &lt;<em>service</em>&gt;. &lt;<em>assistant name</em>&gt; falhou ao iniciar para o banco de dados &lt;<em>database</em>&gt;. A seguinte exceção causou a falha: &lt;<em>exception</em>&gt;</p></td>
</tr>
<tr class="odd">
<td><p>9021</p></td>
<td><p>Assistentes</p></td>
<td><p>Informações</p></td>
<td><p>LogAlways</p></td>
<td><p>Serviço &lt;<em>service</em>&gt;. &lt;<em>service</em>&gt; para o banco de dados &lt;<em>database</em>&gt; está processando uma solicitação sob demanda. Há &lt;<em>number</em>&gt; caixas de correio para processar.</p></td>
</tr>
<tr class="even">
<td><p>9022</p></td>
<td><p>Assistentes</p></td>
<td><p>Informações</p></td>
<td><p>LogAlways</p></td>
<td><p>Serviço &lt;<em>service</em>&gt;. &lt;<em>service</em>&gt; para o banco de dados &lt;<em>database</em>&gt; concluiu a uma solicitação de sob demanda. &lt;<em>number</em>&gt; sem &lt;<em>number</em>&gt; caixas de correio foram processadas com êxito. &lt;<em>number</em>&gt; caixas de correio foram ignoradas devido a erros.</p></td>
</tr>
<tr class="odd">
<td><p>9023</p></td>
<td><p>Assistentes</p></td>
<td><p>Aviso</p></td>
<td><p>LogAlways</p></td>
<td><p>Serviço &lt;<em>service</em>&gt;. &lt;<em>service</em>&gt; Falha ao iniciar o processamento da janela de tempo no banco de dados &lt;<em>database</em>&gt;. A seguinte exceção causou a falha: &lt;<em>exception</em>&gt;</p></td>
</tr>
<tr class="even">
<td><p>9025</p></td>
<td><p>Assistentes</p></td>
<td><p>Informações</p></td>
<td><p>LogAlways</p></td>
<td><p>Serviço &lt;<em>service</em>&gt;. &lt;<em>service</em>&gt; ignorados &lt;<em>number</em>&gt; caixas de correio no banco de dados &lt;<em>database</em>&gt;. Caixas de correio: &lt;<em>mailboxes</em>&gt;</p></td>
</tr>
<tr class="odd">
<td><p>9026</p></td>
<td><p>Assistentes</p></td>
<td><p>Aviso</p></td>
<td><p>LogAlways</p></td>
<td><p>Serviço &lt;<em>service</em>&gt;. &lt;<em>service</em>&gt; Falha ao iniciar o processamento no banco de dados &lt;<em>database</em>&gt; sob demanda. A seguinte exceção causou a falha: &lt;<em>exception</em>&gt;</p></td>
</tr>
<tr class="even">
<td><p>9027</p></td>
<td><p>Assistentes</p></td>
<td><p>Erro</p></td>
<td><p>LogAlways</p></td>
<td><p>Serviço &lt;<em>service</em>&gt;. &lt;<em>service</em>&gt; causado o processo encerrar os tempos de &lt;<em>number</em>&gt; enquanto o processamento da caixa de correio &lt;<em>mailbox</em>&gt; no banco de dados &lt;<em>database</em>&gt;. Esta caixa de correio não são mais será processada na janela de tempo solicitada ou solicitação sob demanda. A seguinte exceção causou a falha: &lt;<em>exception</em>&gt;</p></td>
</tr>
<tr class="odd">
<td><p>9028</p></td>
<td><p>Assistentes</p></td>
<td><p>Aviso</p></td>
<td><p>LogAlways</p></td>
<td><p>Serviço &lt;<em>service</em>&gt;. &lt;<em>service</em>&gt; causado o processo encerrar os tempos de &lt;<em>number</em>&gt; enquanto o processamento da caixa de correio &lt;<em>mailbox</em>&gt; no banco de dados &lt;<em>database</em>&gt;. A seguinte exceção causou a falha: &lt;<em>exception</em>&gt;</p></td>
</tr>
<tr class="even">
<td><p>9033</p></td>
<td><p>Assistentes</p></td>
<td><p>Aviso</p></td>
<td><p>LogAlways</p></td>
<td><p>Serviço &lt;<em>service</em>&gt;. &lt;<em>service</em>&gt; para o banco de dados &lt;<em>database</em>&gt; recebeu uma solicitação de sob demanda. No entanto, não há nenhuma caixa de correio para processar.</p></td>
</tr>
<tr class="odd">
<td><p>9034</p></td>
<td><p>Assistentes</p></td>
<td><p>Informações</p></td>
<td><p>LogAlways</p></td>
<td><p>O serviço &lt;<em>service</em>&gt; interrompido operações de tempo com base para o Assistente de pasta gerenciada no banco de dados &lt;<em>database</em>&gt;.</p></td>
</tr>
<tr class="even">
<td><p>9035</p></td>
<td><p>Assistentes</p></td>
<td><p>Aviso</p></td>
<td><p>LogAlways</p></td>
<td><p>Serviço &lt;<em>service</em>&gt;. &lt;<em>assistant name</em>&gt; não foi capaz de processar &lt;<em>number</em>&gt; caixas de correio porque tempo insuficiente.</p></td>
</tr>
<tr class="odd">
<td><p>9037</p></td>
<td><p>Assistentes</p></td>
<td><p>Erro</p></td>
<td><p>LogAlways</p></td>
<td><p>Serviço &lt;<em>service</em>&gt;. Uma exceção foi encontrada durante o processamento de uma RPC. Método: &lt;<em>method</em>&gt; exceção: &lt;<em>exception</em>&gt;</p></td>
</tr>
</tbody>
</table>

