---
title: 'Grupos de disponibilidade de banco de dados de monitoramento: Exchange 2013 Help'
TOCTitle: Grupos de disponibilidade de banco de dados de monitoramento
ms:assetid: f5bdfd6e-e93c-4d96-8bc2-548750d51930
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Dd351258(v=EXCHG.150)
ms:contentKeyID: 50487026
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Grupos de disponibilidade de banco de dados de monitoramento

 

_**Aplica-se a:**Exchange Server 2013_

_**Tópico modificado em:**2015-03-09_

Você pode usar os detalhes neste tópico para monitorar a integridade e o status de cópias de banco de dados de caixa de correio para grupos de disponibilidade de banco de dados (DAGs), para reunir informações de diagnósticos e para configurar o espaço em disco insuficiente limite de monitoramento.

## Cmdlet Get-MailboxDatabaseCopyStatus

Você pode usar o cmdlet [Get-MailboxDatabaseCopyStatus](https://technet.microsoft.com/pt-br/library/dd298044\(v=exchg.150\)) para visualizar informações de status sobre cópias de bancos de dados de caixa de correio. Este cmdlet permite que você visualize informações sobre todas as cópias de um banco de dados em particular, informações sobre uma cópia específica de um banco de dados em um servidor específico, ou informações sobre todas as cópias de bancos de dados em um servidor. A tabela a seguir descreve os valores possíveis para o status de cópia de uma cópia de banco de dados de caixa de correio.

### Status da cópia do banco de dados

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Status da cópia do banco de dados</th>
<th>Descrição</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Falha</p></td>
<td><p>A cópia do banco de dados de caixa de correio está no estado de Falha porque não está suspensa, e ainda não pode copiar ou reproduzir arquivos de log. Enquanto estiver no estado de Falha e não estiver suspensa, o sistema verificará periodicamente se o problema que causou a alteração do status da cópia para Falha foi resolvido. Depois de o sistema detectar que o problema está resolvido, e de não encontrar outros problemas, o status da cópia automaticamente será alterado para Íntegra.</p></td>
</tr>
<tr class="even">
<td><p>Propagação</p></td>
<td><p>A cópia do banco de dados de caixa de correio está sendo propagada, o índice de conteúdo para a cópia do banco de dados de caixa de correio está sendo propagado, ou ambos estão sendo propagados. Depois da conclusão bem-sucedida da propagação, o status de cópia deve mudar para Inicializando.</p></td>
</tr>
<tr class="odd">
<td><p>SeedingSource</p></td>
<td><p>A cópia do banco de dados de caixa do correio está sendo usada como uma fonte de uma operação de propagação de cópia de banco de dados.</p></td>
</tr>
<tr class="even">
<td><p>Suspensa</p></td>
<td><p>A cópia do banco de dados de caixa de correio está no estado Suspensa como resultado de um administrador ter suspendido manualmente a cópia do banco de dados, executando o cmdlet <strong>Suspend-MailboxDatabaseCopy</strong>.</p></td>
</tr>
<tr class="odd">
<td><p>Íntegra</p></td>
<td><p>A cópia do banco de dados de caixa de correio está copiando e reproduzindo arquivos de log com sucesso, ou copiou e reproduziu com sucesso todos os arquivos de log disponíveis.</p></td>
</tr>
<tr class="even">
<td><p>ServiceDown</p></td>
<td><p>O serviço de Replicação do Microsoft Exchange está indisponível ou está sendo executado no servidor que hospeda a cópia do banco de dados de caixa de correio.</p></td>
</tr>
<tr class="odd">
<td><p>Inicializando</p></td>
<td><p>A cópia do banco de dados de caixa de correio estará no estado Inicializando quando uma cópia de banco de dados for criada, quando o serviço de Replicação do Microsoft Exchange estiver iniciando ou tiver iniciado recentemente e durante as transições de Suspensa, ServiceDown, Falha, Propagação ou SinglePageRestore para outro estado. Neste estado, o sistema está verificando se o banco de dados e o fluxo de log estão em um estado consistente. Na maioria dos casos, o status da cópia permanecerá no estado Inicializando por aproximadamente 15 segundos, mas em todos os casos geralmente não deve ficar neste estado por mais de 30 segundos.</p></td>
</tr>
<tr class="even">
<td><p>Ressincronizando</p></td>
<td><p>A cópia do banco de dados de caixa de correio e seus arquivos de log estão sendo comparados com a cópia ativa do banco de dados para verificar se há divergência entre as duas cópias. O status da cópia permanecerá neste estado até que alguma divergência seja detectada e resolvida.</p></td>
</tr>
<tr class="odd">
<td><p>Montada</p></td>
<td><p>A cópia ativa está online e aceitando conexões de clientes. Apenas a cópia ativa da cópia do banco de dados de caixa de correio pode ter o status de cópia Montada.</p></td>
</tr>
<tr class="even">
<td><p>Desmontada</p></td>
<td><p>A cópia ativa está offline e não aceita conexões de clientes. Apenas a cópia ativa da cópia do banco de dados de caixa de correio pode ter o status de cópia Desmontada.</p></td>
</tr>
<tr class="odd">
<td><p>Montando</p></td>
<td><p>A cópia ativa está sendo colocada online e ainda não aceita conexões de clientes. Apenas a cópia ativa da cópia do banco de dados de caixa de correio pode ter o status de cópia Montando.</p></td>
</tr>
<tr class="even">
<td><p>Desmontando</p></td>
<td><p>A cópia ativa está sendo colocada offline e está encerrando as conexões de clientes. Apenas a cópia ativa da cópia do banco de dados de caixa de correio pode ter o status de cópia Desmontando.</p></td>
</tr>
<tr class="odd">
<td><p>DisconnectedAndHealthy</p></td>
<td><p>A cópia do banco de dados de caixa de correio não está mais conectada à cópia ativa do banco de dados e estava no estado Íntegra quando a perda da conexão aconteceu. Este estado representa a cópia do banco de dados em relação à conectividade com sua cópia de banco de dados de origem. Pode ser informado durante falhas de rede do DAG entre a cópia de origem e a cópia de banco de dados de destino.</p></td>
</tr>
<tr class="even">
<td><p>DisconnectedAndResynchronizing</p></td>
<td><p>A cópia do banco de dados de caixa de correio não está mais conectada à cópia ativa do banco de dados e estava no estado Ressincronizando quando a perda da conexão aconteceu. Este estado representa a cópia do banco de dados em relação à conectividade com sua cópia de banco de dados de origem. Pode ser informado durante falhas de rede do DAG entre a cópia de origem e a cópia de banco de dados de destino.</p></td>
</tr>
<tr class="odd">
<td><p>FailedAndSuspended</p></td>
<td><p>Os estados Falha e Suspensa foram definidos simultaneamente pelo sistema porque uma falha foi detectada, e porque a resolução da falha explicitamente exige a intervenção do administrador. Um exemplo é se o sistema detectar divergências irreversíveis entre o banco de dados de caixa de correio ativo e a cópia do banco de dados. Diferente do estado Falha, o sistema não verificará periodicamente se o problema foi resolvido e não recuperará automaticamente. Ao invés disso, um administrador deve intervir para resolver a causa da falha subjacente antes que a cópia do banco de dados possa passar para um estado de integridade.</p></td>
</tr>
<tr class="even">
<td><p>SinglePageRestore</p></td>
<td><p>Este estado indica que uma operação de restauração de página única está ocorrendo na cópia do banco de dados de caixa de correio.</p></td>
</tr>
</tbody>
</table>


O cmdlet **Get-MailboxDatabaseCopyStatus** também retorna detalhes sobre as redes de replicação em uso, incluindo o *IncomingLogCopyingNetwork*, que é retornado para cópias do banco de dados passivas, incluindo *OutgoingConnections*, que é retornado para bancos de dados ativos que possuem mais que uma cópia, bem como qualquer cópia de banco de dados sendo usada como fonte para uma operação de propagação de banco de dados. As informações de conexão de saída são fornecidas para cópias de banco de dados que estão em replicação de modo de arquivo. As informações de conexão de saída não são fornecidas para cópias de banco de dados que estão em replicação de modo de bloco.

## Exemplos de Get-MailboxDatabaseCopyStatus

Os exemplos seguintes usam o cmdlet **Get-MailboxDatabaseCopyStatus**. Cada exemplo redireciona os resultados para o cmdlet **Format-List** para exibir a saída em formato de lista.

Este exemplo retorna informações de status para todas as cópias do banco de dados DB2.

    Get-MailboxDatabaseCopyStatus -Identity DB2 | Format-List

Este exemplo retorna o status para todas as cópias de banco de dados no servidor de Caixa de Correio MBX2.

    Get-MailboxDatabaseCopyStatus -Server MBX2 | Format-List

Este exemplo retorna o status para todas as cópias de banco de dados no servidor de Caixa de Correio local.

    Get-MailboxDatabaseCopyStatus -Local | Format-List

Para mais informações sobre o uso do cmdlet **Get-MailboxDatabaseCopyStatus**, consulte [Get-MailboxDatabaseCopyStatus](https://technet.microsoft.com/pt-br/library/dd298044\(v=exchg.150\)).

## Cmdlet Test-ReplicationHealth

Você pode usar o cmdlet [Test-ReplicationHealth](https://technet.microsoft.com/pt-br/library/bb691314\(v=exchg.150\)) para visualizar informações de status da replicação contínua sobre cópias de bancos de dados de caixa de correio. Este cmdlet pode ser usado para verificar todos os aspectos do status da replicação e da reprodução para fornecer uma visão geral completa de um servidor de Caixa de Correio em um DAG.

O cmdlet **Test-ReplicationHealth** é projetado para o monitoramento proativo da replicação contínua e do pipeline de replicação contínua, da disponibilidade do Active Manager e da integridade e status do serviço de cluster, quorum e componentes de rede subjacentes. Pode ser executado local ou remotamente em qualquer servidor de Caixa de Correio em um DAG. O cmdlet **Test-ReplicationHealth** executa os testes descritos na tabela a seguir.

### Testes do cmdlet Test-ReplicationHealth

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Nome do teste</th>
<th>Descrição</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>ClusterService</p></td>
<td><p>Verifica se o serviço de Cluster está em execução e acessível no membro do DAG especificado ou, se nenhum membro do DAG estiver especificado, no servidor local.</p></td>
</tr>
<tr class="even">
<td><p>ReplayService</p></td>
<td><p>Verifica se o serviço de Replicação do Microsoft Exchange está em execução e acessível no membro do DAG especificado ou, se nenhum membro do DAG estiver especificado, no servidor local.</p></td>
</tr>
<tr class="odd">
<td><p>ActiveManager</p></td>
<td><p>Verifica se a instância do Active Manager em execução no membro especificado do DAG (ou, se nenhum membro do DAG estiver especificado, no servidor local) está em uma função válida (primária, secundária ou autônoma).</p></td>
</tr>
<tr class="even">
<td><p>TasksRpcListener</p></td>
<td><p>Verifica se o servidor de tarefas de chamada de procedimento remoto (RPC) está em execução e acessível no membro do DAG especificado ou, se nenhum membro do DAG estiver especificado, no servidor local.</p></td>
</tr>
<tr class="odd">
<td><p>TcpListener</p></td>
<td><p>Verifica se o ouvinte da cópia do log do TCP está em execução e acessível no membro do DAG especificado ou, se nenhum membro do DAG estiver especificado, no servidor local.</p></td>
</tr>
<tr class="even">
<td><p>ServerLocatorService</p></td>
<td><p>Verifica os processos do cliente/servidor do Active Manager em membros DAG e no Servidor de Acesso para Cliente que realizam pesquisas no Active Directory e no Active Manager para determinar onde o banco de dados de caixa de correio de um usuário está ativo.</p></td>
</tr>
<tr class="odd">
<td><p>DagMembersUp</p></td>
<td><p>Verifica se todos os membros do DAG estão disponíveis, em execução e acessíveis.</p></td>
</tr>
<tr class="even">
<td><p>ClusterNetwork</p></td>
<td><p>Verifica se todas as redes gerenciadas por cluster no membro do DAG especificado (ou, se nenhum membro do DAG estiver especificado, no servidor local) estão disponíveis.</p></td>
</tr>
<tr class="odd">
<td><p>QuorumGroup</p></td>
<td><p>Verifica se o grupo de cluster padrão (grupo de quorum) está em um estado íntegro e online.</p></td>
</tr>
<tr class="even">
<td><p>FileShareQuorum</p></td>
<td><p>Verifica se o servidor testemunha e o diretório testemunha e o compartilhamento configurado para DAG estão acessíveis.</p></td>
</tr>
<tr class="odd">
<td><p>DatabaseRedundancy</p></td>
<td><p>Verifica se há pelo menos uma cópia íntegra disponível dos bancos de dados no membro do DAG especificado ou, se nenhum membro do DAG estiver especificado, no servidor local.</p></td>
</tr>
<tr class="even">
<td><p>DatabaseAvailability</p></td>
<td><p>Verifica se os bancos de dados têm disponibilidade suficiente no membro do DAG especificado ou, se nenhum membro do DAG estiver especificado, no servidor local.</p></td>
</tr>
<tr class="odd">
<td><p>DBCopySuspended</p></td>
<td><p>Verifica se alguma cópia de banco de dados de caixa de correio está no estado Suspensa no membro do DAG especificado ou, se nenhum membro do DAG estiver especificado, no servidor local.</p></td>
</tr>
<tr class="even">
<td><p>DBCopyFailed</p></td>
<td><p>Verifica se alguma cópia de banco de dados de caixa de correio está no estado Falha no membro do DAG especificado ou, se nenhum membro do DAG estiver especificado, no servidor local.</p></td>
</tr>
<tr class="odd">
<td><p>DBInitializing</p></td>
<td><p>Verifica se alguma cópia de banco de dados de caixa de correio está no estado Inicializando no membro do DAG especificado ou, se nenhum membro do DAG estiver especificado, no servidor local.</p></td>
</tr>
<tr class="even">
<td><p>DBDisconnected</p></td>
<td><p>Verifica se alguma cópia de banco de dados de caixa de correio está no estado Desconectada no membro do DAG especificado ou, se nenhum membro do DAG estiver especificado, no servidor local.</p></td>
</tr>
<tr class="odd">
<td><p>DBLogCopyKeepingUp</p></td>
<td><p>Verifica se a cópia e inspeção de log pelas cópias passivas de bancos de dados no membro do DAG especificado (ou, se nenhum membro do DAG estiver especificado, no servidor local) estão aptas para prosseguir com a atividade de geração de log na cópia ativa.</p></td>
</tr>
<tr class="even">
<td><p>DBLogReplayKeepingUp</p></td>
<td><p>Verifica se a atividade de repetição para as cópias passivas de bancos de dados no membro do DAG especificado (ou, se nenhum membro do DAG estiver especificado, no servidor local) está apta para prosseguir com a atividade de cópia e inspeção de log.</p></td>
</tr>
</tbody>
</table>


## Exemplo de Test-ReplicationHealth

Este exemplo usa o cmdlet **Test-ReplicationHealth** para testar a integridade da replicação para o servidor de Caixa de Correio MBX1.

    Test-ReplicationHealth -Identity MBX1

## Log de eventos do canal Crimson

O Windows inclui duas categorias de logs de eventos: Logs do Windows e logs de Aplicativos e Serviços. A categoria de logs do Windows inclui os logs de eventos disponíveis nas versões anteriores do Windows: Logs de eventos de Aplicativo, Segurança e Sistema. Também inclui dois novos logs: o log de Instalação e log ForwardedEvents. Os logs Windows têm por objetivo armazenar eventos de aplicativos e eventos herdados que se aplicam a todo o sistema.

Logs de Aplicativos e Serviços são uma categoria nova de logs de eventos. Estes logs armazenam eventos de um único aplicativo ou componente, ao invés de eventos que possam ter impacto em todo o sistema. Esta nova categoria de logs de eventos é referenciada como um canal crimson do aplicativo.

A categoria de logs de Aplicativos e Serviços inclui quatro subtipos: Logs Admin, Operacional, Analítico e Depuração. Os eventos nos logs Admin são de particular interesse se você usa os registros do log de eventos para solucionar problemas. Os eventos no log Admin devem fornecer orientação sobre como responder aos eventos. Os eventos no log Operacional também são úteis, mas podem exigir mais interpretação. Os logs Admin e Depuração não são tão amigáveis. Os logs Analíticos (que por padrão estão ocultos e desabilitados) armazenam eventos que rastreiam um problema, e geralmente um alto volume de eventos é registrada. Logs de Depuração são usados por desenvolvedores quando depuram aplicativos.

O Exchange 2013 registra eventos no canal crimson na área de logs de Aplicativos e Serviços. Você pode exibir esses canais executando estas etapas:

1.  Abra o Visualizador de Eventos.

2.  Na árvore do console, navegue até **Logs de Aplicativos e Serviços** \> **Microsoft** \> **Exchange**.

3.  Em **Exchange**, selecione um canal crimson, como **HighAvailability** ou **MailboxDatabaseFailureItems** para ver o eventos relacionados a cópia do DAG e o banco de dados, ou **ActiveMontoring** ou **ManagedAvailability** para ver os eventos relacionado à disponibilidade gerenciada.

O canal HighAvailability contém eventos relacionados à inicialização e desligamento do serviço de Replicação do Microsoft Exchange, e os vários componentes executados dentro do serviço de Replicação do Microsoft Exchange, como o Active Manager, a API da replicação síncrona de terceiros, o servidor de tarefas RPC, o ouvinte de TCP e o gravador do Serviço de Cópias de Sombra de Volume (VSS). O canal HighAvailability também é usado pelo Active Manager para registrar eventos relacionados ao monitoramento de funções do Active Manager e eventos de ação de banco de dados, como uma operação de montagem de banco de dados e truncamento de log, e para registrar eventos relacionados ao cluster subjacente do DAG.

O canal MailboxDatabaseFailureItems é usado para registrar eventos associados a qualquer falha que afete um banco de dados de caixa de correio replicado.

O canal de ActiveMonitoring contém eventos de resultado e definição para disponibilidade gerenciada sondas, monitores e respondentes.

O canal de ManagedAvailability contém os logs de ação de recuperação e os resultados e eventos relacionados.

## Monitor de espaço em disco insuficiente

Exchange 2013 Gerenciados centenas de métricas de sistema e componentes de monitores de disponibilidade a cada minuto, incluindo a quantidade de espaço livre em disco em volumes usado pela função de servidor de caixa de correio. Antes de Exchange 2013 Service Pack 1 (SP1), o Exchange monitora o espaço disponível em todos os volumes locais, incluindo os volumes que não contêm quaisquer bancos de dados ou arquivos de log. No SP1 e posterior, somente os volumes que contêm bancos de dados do Exchange e arquivos de log são monitorados. No SP1, o limite padrão para o monitor de espaço de baixo volume será 200 GB. No Exchange 2013 atualização cumulativa 6 e posterior, o limite padrão é de 180 GB. No SP1 e posterior, você pode configurar o limite, adicionando o seguinte valor de Registro DWORD (em MB) em cada servidor de caixa de correio que você deseja personalizar:

Caminho: **HKEY\_LOCAL\_MACHINE\\Software\\Microsoft\\ExchangeServer\\v15\\Replay\\Parameters**

Valor: *SpaceMonitorLowSpaceThresholdInMB*

Por exemplo definir o limite de 100 GB, você configuraria o seguinte valor de registro:

**186a0 REG\_DWORD (100000)**

Após configurar ou modificar o valor de registro acima, você deve reiniciar o serviço de gerenciamento do Microsoft Exchange DAG para que a alteração entre em vigor.

## Script CollectOverMetrics.ps1

O Exchange 2013 inclui um script chamado CollectOverMetrics.ps1, que pode ser encontrado na pasta Scripts. CollectOverMetrics.ps1 lê logs de eventos de membros do DAG para reunir informações sobre operações de banco de dados  (como montagens, movimentações e failovers de banco de dados) abrangendo um período de tempo específico. Para cada operação, o script retorna as seguintes informações:

  - Identidade do banco de dados

  - Hora de início e término da operação

  - Servidores em que o banco de dados estava montado no início e no término da operação

  - Motivo para a operação

  - Se a operação foi bem-sucedida, incluindo os detalhes de erros no caso de falha da operação

O script grava essas informações em arquivos .csv com uma operação por fila. Ele grava um arquivo .csv separado para cada DAG.

O script suporta parâmetros que permitem personalizar seu comportamento e sua saída. Por exemplo, os resultados podem ser restritos a um subconjunto especificado usando os parâmetros *Database* ou *ReportFilter*. Somente as operações que correspondem a esses filtros serão incluídas no relatório HTML do resumo. Os parâmetros disponíveis estão listados na tabela a seguir.

### Parâmetros do script CollectOverMetrics.ps1

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Parâmetro</th>
<th>Descrição</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>DatabaseAvailabilityGroup</em></p></td>
<td><p>Especifica o nome do DAG do qual você deseja coletar métricas. Se este parâmetro for omitido, o DAG do qual o servidor local é membro será usado. Caracteres curinga podem ser usados para coletar informações e gerar relatórios sobre vários DAGs.</p></td>
</tr>
<tr class="even">
<td><p><em>Database</em></p></td>
<td><p>Fornece uma lista de bancos de dados para os quais o relatório precisa ser gerado. Há suporte para caracteres curinga, por exemplo, <code>-Database:&quot;DB1&quot;,&quot;DB2&quot;</code> ou <code>-Database:&quot;DB*&quot;</code>.</p></td>
</tr>
<tr class="odd">
<td><p><em>StartTime</em></p></td>
<td><p>Especifica a duração do período de tempo a relatar. O script coleta somente os eventos registrados durante esse período. Como resultado, o script pode capturar registros parciais da operação (por exemplo, apenas o final de uma operação no início do período ou vice-versa). Se nem <em>StartTime</em> nem <em>EndTime</em> forem especificados, o script adotará como padrão as últimas 24 horas. Se apenas um parâmetro for especificado, o período será de 24 horas, começando ou terminando no horário especificado.</p></td>
</tr>
<tr class="even">
<td><p><em>EndTime</em></p></td>
<td><p>Especifica a duração do período de tempo a relatar. O script coleta somente os eventos registrados durante esse período. Como resultado, o script pode capturar registros parciais da operação (por exemplo, apenas o final de uma operação no início do período ou vice-versa). Se nem <em>StartTime</em> nem <em>EndTime</em> forem especificados, o script o script adotará como padrão as últimas 24 horas. Se apenas um parâmetro for especificado, o período será de 24 horas, começando ou terminando no horário especificado.</p></td>
</tr>
<tr class="odd">
<td><p><em>ReportPath</em></p></td>
<td><p>Especifica a pasta usada para armazenar os resultados do processamento de eventos. Se este parâmetro for omitido, a pasta Scripts será usada. Quando especificado, o script usa uma lista de arquivos .csv gerados por ele como dados de origem para gerar um relatório HTML resumido. O relatório é o mesmo que é gerado com a opção -GenerateHtmlReport. Os arquivos podem ser gerados abrangendo vários DAGs em muitos períodos de tempo diferentes, ou mesmo com horários sobrepostos. O script mescla todos esses dados.</p></td>
</tr>
<tr class="even">
<td><p><em>GenerateHtmlReport</em></p></td>
<td><p>Especifica que o script colete todas as informações que gravou, agrupe os dados pelo tipo de operação e gere um arquivo HTML que inclua estatísticas para cada um desses grupos. O relatório inclui o número total de operações em cada grupo, o número de operações que falharam e estatísticas sobre o tempo gasto em cada grupo. O relatório também detalha os tipos de erros que resultaram em falha nas operações.</p></td>
</tr>
<tr class="odd">
<td><p><em>ShowHtmlReport</em></p></td>
<td><p>Especifica se o relatório gerado em HTML deve ser exibido em um navegador Web depois da sua geração.</p></td>
</tr>
<tr class="even">
<td><p><em>SummariseCsvFiles</em></p></td>
<td><p>Especifica que o script leia os dados de arquivos .csv existentes que foram gerados anteriormente por ele. Em seguida, esses dados são usados para gerar um relatório resumido semelhante ao relatório gerado pelo parâmetro <em>GenerateHtmlReport</em>.</p></td>
</tr>
<tr class="odd">
<td><p><em>ActionType</em></p></td>
<td><p>Especifica o tipo de ações operacionais que o script deve coletar. Os valores válidos para esse parâmetro são <code>Move</code>, <code>Mount</code>, <code>Dismount</code> e <code>Remount</code>. O valor <code>Move</code> refere-se a qualquer horário em que o banco de dados altera seu servidor ativo, seja por movimentos controlado ou por failovers. Os valores <code>Mount</code>, <code>Dismount</code> e <code>Remount</code> referem-se aos horários em que o banco de dados altera seu status de montagem sem ser movido para outro computador.</p></td>
</tr>
<tr class="even">
<td><p><em>ActionTrigger</em></p></td>
<td><p>Especifica quais operações administrativas devem ser coletadas pelo script. Os valores válidos para esse parâmetro são <code>Admin</code> ou <code>Automatic</code>. Ações automáticas são aquelas executadas automaticamente pelo sistema (por exemplo, um failover quando um servidor fica offline). Ações administrativas são ações que foram executadas por um administrador usando o Shell de Gerenciamento do Exchange ou o Centro de Administração do Exchange.</p></td>
</tr>
<tr class="odd">
<td><p><em>RawOutput</em></p></td>
<td><p>Especifica que o script grave os resultados que teriam sido gravados em arquivos .csv diretamente no fluxo de saída, como aconteceria com write-output. Essas informações podem ser canalizadas para outros comandos.</p></td>
</tr>
<tr class="even">
<td><p><em>IncludedExtendedEvents</em></p></td>
<td><p>Especifica que o script colete os eventos que fornecem detalhes de diagnóstico do tempo gasto montando bancos de dados. Esse pode ser um estágio demorado se o log de eventos de Aplicativo nos servidores for grande.</p></td>
</tr>
<tr class="odd">
<td><p><em>MergeCSVFiles</em></p></td>
<td><p>Especifica que o script mescle todos os arquivos .csv contendo dados sobre cada operação em um único arquivo .csv.</p></td>
</tr>
<tr class="even">
<td><p><em>ReportFilter</em></p></td>
<td><p>Especifica que um filtro deve ser aplicado às operações, usando os campos que aparecem nos arquivos .csv. Esse parâmetro usa o mesmo formato de uma operação <code>Where</code>, com cada elemento definido como <code>$_</code> e retornando um valor booleano. Por exemplo: <code>{$_DatabaseName -notlike &quot;Mailbox Database*&quot;}</code> pode ser usado para excluir os bancos de dados padrão do relatório.</p></td>
</tr>
</tbody>
</table>


## Exemplos de CollectOverMetrics.ps1

Este exemplo coleta métricas para todos os bancos de dados que correspondem a DB\* (o que inclui um caractere curinga) no DAG DAG1. Depois da coleta das métricas, um relatório HTML é gerado e exibido.

    CollectOverMetrics.ps1 -DatabaseAvailabilityGroup DAG1 -Database:"DB*" -GenerateHTMLReport -ShowHTMLReport

Os seguintes exemplos demonstram maneiras de filtrar o relatório HTML resumido. O primeiro usa o parâmetro *Database*, que recebe uma lista de nomes de bancos de dados. O relatório resumido resultante conterá dados apenas sobre esses bancos de dados. Os dois próximos exemplos usam a opção *ReportFilter*. O último exemplo filtra todos os bancos de dados padrão.

    CollectOverMetrics.ps1 -SummariseCsvFiles (dir *.csv) -Database MailboxDatabase123,MailboxDatabase456
    CollectOverMetrics.ps1 -SummariseCsvFiles (dir *.csv) -ReportFilter { $_.DatabaseName -notlike "Mailbox Database*" }
    CollectOverMetrics.ps1 -SummariseCsvFiles (dir *.csv) -ReportFilter { ($_.ActiveOnStart -like "ServerXYZ*") -and ($_.ActiveOnEnd -notlike "ServerXYZ*") }

## Script CollectReplicationMetrics.ps1

CollectReplicationMetrics.ps1 é outro script de métrica de integridade incluído no Exchange 2013. Esse script fornece uma forma ativa de monitoramento, porque coleta métricas em tempo real, enquanto o script é executado. CollectReplicationMetrics.ps1 coleta dados de contadores de desempenho relacionados à replicação de banco de dados. O script reúne dados de contador de vários servidores de Caixa de Correio, grava os dados de cada servidor em um arquivo .csv e então relata diferentes estatísticas abrangendo todos esses dados (por exemplo, por quanto tempo cada cópia falhou ou foi suspensa, o comprimento médio da fila de cópia ou de repetição ou quanto tempo as cópias permaneceram fora de seus critérios de failover).

Você pode especificar os servidores individualmente ou DAGs inteiros. Você pode ou executar o script para coletar primeiro os dados e depois gerar o relatório, ou pode executá-lo apenas para coletar os dados ou para apenas para gerar um relatório sobre os dados que já foram coletados. É possível especificar a frequência de amostragem dos dados e a duração total da coleta de dados.

Os dados coletados de cada servidor são gravados em um arquivo chamado **CounterData.\<ServerName\>.\<TimeStamp\>.csv**. O relatório de resumo será gravado em um arquivo chamado **HaReplPerfReport.\<NomeDoDAG\>.\<CarimbodeDataeHora\>.csv**, ou **HaReplPerfReport.\<CarimbodeDataeHora\>.csv** caso o script não tenha sido executado com o parâmetro *DagName*.

O script inicia trabalhos do Windows PowerShell para coletar os dados de cada servidor. Esses trabalhos são executados durante todo o período em que os dados estão sendo coletados. Se você especificar um grande número de servidores, esse processo pode usar uma quantidade considerável de memória. O estágio final do processo, quando os dados são processados em um relatório resumido, também pode ser bastante demorado para grandes quantidades de dados. É possível executar o estágio de coleta em um computador e depois copiar os dados para outro local para processamento.

O script CollectReplicationMetrics.ps1 suporta parâmetros que permitem personalizar seu comportamento e sua saída. Os parâmetros disponíveis estão listados na tabela a seguir.

### Parâmetros do script CollectReplicationMetrics

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Parâmetro</th>
<th>Descrição</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>DagName</em></p></td>
<td><p>Especifica o nome do DAG do qual você deseja coletar métricas. Se esse parâmetro for omitido, o DAG do qual o servidor local é membro será usado.</p></td>
</tr>
<tr class="even">
<td><p><em>DatabaseNames</em></p></td>
<td><p>Fornece uma lista de bancos de dados para os quais o relatório precisa ser gerado. Há suporte para caracteres curinga, por exemplo, <code>-DatabaseNames:&quot;DB1&quot;,&quot;DB2&quot;</code> ou <code>-DatabaseNames:&quot;DB*&quot;</code>.</p></td>
</tr>
<tr class="odd">
<td><p><em>ReportPath</em></p></td>
<td><p>Especifica a pasta usada para armazenar os resultados do processamento de eventos. Se esse parâmetro for omitido, a pasta Scripts será usada.</p></td>
</tr>
<tr class="even">
<td><p><em>Duration</em></p></td>
<td><p>Especifica a quantidade de tempo em que o processo de coleta deve ser executado. Os valores típicos seriam de uma a três horas. Durações maiores devem ser usadas somente com longos intervalos entre cada amostra ou como uma série de trabalhos mais curtos executados por tarefas agendadas.</p></td>
</tr>
<tr class="odd">
<td><p><em>Frequency</em></p></td>
<td><p>Especifica a freqüência na qual as métricas de dados são coletadas. Os valores típicos seriam de 30 segundos, um minuto ou cinco minutos. Sob circunstâncias normais, intervalos mais curtos que esses não mostrarão mudanças significativas entre cada amostra.</p></td>
</tr>
<tr class="even">
<td><p><em>Servers</em></p></td>
<td><p>Especifica a identidade dos servidores dos quais serão coletadas estatísticas. É possível especificar qualquer valor, incluindo caracteres curinga ou GUIDs.</p></td>
</tr>
<tr class="odd">
<td><p><em>SummariseFiles</em></p></td>
<td><p>Especifica uma lista de arquivos .csv para gerar um relatório resumido. Esses são os arquivos chamados <strong>CounterData.&lt;CounterData&gt;*</strong> gerados pelo script CollectReplicationMetrics.ps1.</p></td>
</tr>
<tr class="even">
<td><p><em>Mode</em></p></td>
<td><p>Especifica os estágios de processamento que o script executa. É possível usar os seguintes valores:</p>
<ul>
<li><p><code>CollectAndReport</code>   Esse é o valor padrão. Esse valor significa que o script deve coletar os dados dos servidores e depois processá-los para produzir o relatório resumido.</p></li>
<li><p><code>CollectOnly</code>   Esse valor significa que o script deve apenas coletar os dados e não produzir o relatório.</p></li>
<li><p><code>ProcessOnly</code>   Esse valor significa que o script deve importar os dados de um conjunto de arquivos .csv e processá-los para produzir o relatório resumido. O parâmetro <em>SummariseFiles</em> é usado para fornecer ao script a lista de arquivos para serem processados.</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p><em>MoveFilestoArchive</em></p></td>
<td><p>Especifica que o script deve mover os arquivos para uma pasta compactada após o processamento.</p></td>
</tr>
<tr class="even">
<td><p><em>LoadExchangeSnapin</em></p></td>
<td><p>Especifica que o script deve carregar os comandos de Shell. Esse parâmetro é útil quando o script precisa ser executado de fora do Shell, como em uma tarefa agendada.</p></td>
</tr>
</tbody>
</table>


## Exemplo de CollectReplicationMetrics.ps1

O seguinte exemplo coleta dados correspondentes a uma hora de todos os servidores no DAG DAG1, amostrados em intervalos de um minuto, e gera um relatório resumido. Além disso, o parâmetro *ReportPath* é usado, o que faz com que o script coloque todos os arquivos no diretório atual.

    CollectReplicationMetrics.ps1 -DagName DAG1 -Duration "01:00:00" -Frequency "00:01:00" -ReportPath

O seguinte exemplo lê os dados de todos os arquivos que correspondem a CounterData\* e gera um relatório resumido.

    CollectReplicationMetrics.ps1 -SummariseFiles (dir CounterData*) -Mode ProcessOnly -ReportPath

