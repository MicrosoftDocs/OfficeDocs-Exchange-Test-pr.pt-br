---
title: 'Log de auditoria de administrador: Exchange 2013 Help'
TOCTitle: Log de auditoria de administrador
ms:assetid: 22b17eb8-d8ee-4599-b202-d6a7928c20d9
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Dd335144(v=EXCHG.150)
ms:contentKeyID: 50556166
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Log de auditoria de administrador

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2018-03-05_

Você pode usar o registro em log de auditoria do administrador no Microsoft Exchange Server 2013 para registrar em log quando um usuário ou administrador faz uma alteração em sua organização. Mantendo um log das alterações, você pode rastrear quem fez cada alteração, aumentar seus logs de alterações com registros detalhados da alteração quando ela foi implementada, atender aos requisitos regulamentares e às solicitações para descoberta e mais.

Por padrão, o log de auditoria está habilitado em novas instalações do Exchange 2013.

**Sumário**

What gets audited

Audit logging configuration

Audit logs

Manual audit log entries

Active Directory replication

Admin Audit Log agent

## O que é auditado

Cmdlets que são executados diretamente no Shell de Gerenciamento do Exchange são auditados. Além disso, as operações realizadas usando o Centro de administração do Exchange (EAC) também são registradas porque elas executam cmdlets no plano de fundo.

Cmdlets, independentemente de onde são executados, sejam auditados se um cmdlet estiver no cmdlet auditoria lista e um ou mais parâmetros nesse cmdlet estão na lista de auditoria de parâmetro. Log de auditoria é destinado para mostrar as ações que foram tomadas para modificar objetos em uma organização Exchange em vez de quais objetos tem sido exibidos.


> [!IMPORTANT]
> Um cmdlet poderá não ser registrado em log se ocorrer um erro antes de o cmdlet chamar o agente de extensão de cmdlet Log de Auditoria de Admin. Se ocorrer um erro depois que o agente de Log de Auditoria de Admin for chamado, o cmdlet será registrado em log com o erro associado. Para obter mais informações, consulte a seção Admin Audit Log Agent mais adiante neste tópico.<BR>As alterações feitas usando ferramentas de gerenciamento do Microsoft Exchange Server 2010 são registradas; no entanto, as alterações usando ferramentas de gerenciamento do Microsoft Exchange Server 2007 não são registradas.<BR>As alterações feitas na configuração do log de auditoria são atualizadas a cada 60 minutos em computadores que têm o Shell aberto no momento em que é feita uma alteração na configuração. Se você quiser aplicar as alterações imediatamente, feche e reabra o Shell em cada computador.<BR>Um comando pode demorar até 15 minutos após sua execução para aparecer nos resultados de pesquisa do log de auditoria. Isso ocorre porque as entradas do log de auditoria precisam ser indexadas antes de serem pesquisáveis. Se um comando não aparecer no log de auditoria do administrador, aguarde alguns minutos e execute a pesquisa novamente.



## Configuração de log de auditoria

Por padrão, se o log de auditoria está habilitado, uma entrada de log é criada sempre que qualquer cmdlet é executado. Se você não quiser auditar todos os cmdlets que é executado, você pode configurar o log de auditoria de auditoria somente os cmdlets e os parâmetros que você está interessado em. Configurar o log de auditoria com o cmdlet **Set-AdminAuditLogConfig** . Os parâmetros referenciados nas seções a seguir são usados com este cmdlet.


> [!IMPORTANT]
> As alterações feitas na configuração do log de auditoria do administrador são sempre registradas em log, independentemente de o cmdlet <STRONG>Set-AdministratorAuditLog</STRONG> estar incluído na lista de cmdlets que estão sendo auditados ou de o registro em log de auditoria estar habilitado ou desabilitado.



Quando um comando é executado, o Exchange inspeciona o cmdlet usado. Se o cmdlet executado corresponder a qualquer dos cmdlets fornecidos com o parâmetro *AdminAuditLogConfigCmdlets*, o Exchange irá verificar os parâmetros especificados no parâmetro *AdminAuditLogConfigParameters*. Se ao menos um parâmetro na lista de parâmetros tiver correspondência, o Exchange registrará em log o cmdlet executado na caixa de correio especificada, usando o parâmetro *AdminAuditLogMailbox*. As seções a seguir contêm mais informações sobre cada aspecto da configuração do log de auditoria.

Para mais informações sobre o gerenciamento de configuração de registro em log de auditoria, consulte [Gerenciar o administrador do log de auditoria](manage-administrator-audit-logging-exchange-2013-help.md).

Voltar ao início

## Cmdlets

É possível controlar quais cmdlets serão auditados fornecendo uma lista de cmdlets e dos parâmetros que deseja registrar. Ao configurar o log de auditoria, você pode especificar a auditoria de todos os cmdlets ou especificar os cmdlets que você deseja auditar usando o parâmetro *AdminAuditLogConfigCmdlets*. Você pode especificar nomes completos de cmdlets, como **New-Mailbox**, ou especificar nomes parciais de cmdlets e colocar esses nomes entre caracteres curinga, como um asterisco (`*`). Por exemplo, se quiser um registro em log quando qualquer cmdlet que contenha a cadeia de caracteres `Transport` for executado, você poderá especificar um valor de `*Transport*`. É possível misturar nomes completos e nomes parciais de cmdlet para adequar o log de auditoria às suas necessidades.

## Parâmetros

Além de especificar quais cmdlets deseja registrar em log, você também pode indicar que os cmdlets só sejam registrados se certos parâmetros deles forem usados. Use o parâmetro *AdminAuditLogConfigParameters* para especificar os parâmetros a serem registrados em log. Assim como faz com os cmdlets, você pode especificar nomes completos de parâmetros, como `Database`, ou nomes parciais de parâmetros entre caracteres curinga (`*`), como `*Address*`, ou uma combinação de ambos.

## Limite de idade do log de auditoria

Por padrão, o registro em log de auditoria é configurado para armazenar entradas de log de auditoria por 90 dias. Após 90 dias, a entrada de log de auditoria é excluída. É possível alterar o limite de idade do log de auditoria usando o parâmetro *AdminAuditLogAgeLimit*. É possível especificar o número de dias, horas, minutos e segundos que as entradas de log de auditoria devem ser mantidas. Para especificar um valor, utilize o formato `dd.hh:mm:ss` em que o seguinte se aplica:

  - **dd**   O número de dias que a entrada do log de auditoria será mantida.

  - **hh**   O número de horas que a entrada do log de auditoria será mantida.

  - **mm**   O número de minutos que a entrada do log de auditoria será mantida.

  - **ss**   O número de segundos que a entrada do log de auditoria será mantida.

Você deve especificar anos múltiplos usando o campo `dd`. Por exemplo, 365 dias é igual a um ano; 730 dias é igual a dois anos; 913 dias é igual a dois anos e seis meses. Por exemplo, para definir o limite de idade do log de auditoria como dois anos e seis meses, use a sintaxe `913.00:00:00`.


> [!CAUTION]
> Você pode definir para o limite de idade do log de auditoria um valor menor do que o limite de idade atual. Se isso for feito, todas as entradas do log de auditoria com idade que exceda o novo limite de idade serão excluídas.<BR>Se você definir o limite de idade para 0, o Exchange&nbsp;exclui todas as entradas no log de auditoria.<BR>Recomendamos que você conceda permissões de configuração do limite de idade do log de auditoria somente a usuários extremamente confiáveis.



## Log detalhado

Por padrão, o log de auditoria do administrador registra apenas o nome do cmdlet, os parâmetros do cmdlet (e valores especificados), o objeto que foi modificado, quem executou o cmdlet, quando o cmdlet foi executado e em qual servidor o cmdlet foi executado. O log de auditoria do administrador não registra quais propriedades foram modificadas no objeto. Se deseja que o log de auditoria também inclua as propriedades do objeto que foram modificadas, você pode habilitar o log detalhado definindo o parâmetro *LogLevel* como `Verbose`. Ao habilitar o log detalhado, além das informações registradas por padrão, as propriedades modificadas em um objeto, incluindo seus valores antigos e novos, serão incluídas no log de auditoria.

## Cmdlets de teste

Os cmdlets que começam com o verbo **Test** não são registrados em log por padrão. Você pode indicar que cmdlets **Test** devem ser registrados em log configurando o parâmetro *TestCmdletLoggingEnabled* como `$true`. Embora seja possível habilitar o registro em log de cmdlets de teste, recomendamos que você o faça somente por curtos períodos de tempo, pois os cmdlets podem produzir uma grande quantidade de informações.

## Logs de auditoria

Toda vez que um cmdlet é registrado em log, uma entrada de log de auditoria é criada. Os logs de auditoria estão armazenados em uma caixa de correio de arbitragem dedicada e oculta que pode ser acessada somente por meio do EAC ou do cmdlet **Search-AdminAuditLog** ou **New-AdminAuditLogSearch**. Não pode ser aberta com o Microsoft Outlook Web App ou o Microsoft Outlook. As seções a seguir contém informações sobre o seguinte:

  - O que está incluído nos logs

  - Relatórios disponíveis na página de **auditoria** do EAC

  - Cmdlets de pesquisa de log de auditoria

## Conteúdo do log de auditoria

Cada entrada de log de auditoria contém as informações descritas na tabela a seguir. O log de auditoria contém uma ou mais entradas de log de auditoria. O número de entradas de log de auditoria é controlado pelo limite de idade do log de auditoria especificado pelo cmdlet **Set-AdminAuditLogConfig**. Todas as entradas de log de auditoria que excederem o limite de idade serão excluídas.

### Campos de entrada de log de auditoria

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Campo</th>
<th>Descrição</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code>RunspaceId</code></p></td>
<td><p>Esse campo é usado internamente pelo Exchange.</p></td>
</tr>
<tr class="even">
<td><p><code>ObjectModified</code></p></td>
<td><p>Este campo contém o objeto que foi modificado pelo cmdlet especificado no campo <code>CmdletName</code>.</p></td>
</tr>
<tr class="odd">
<td><p><code>CmdletName</code></p></td>
<td><p>Este campo contém o nome do cmdlet que foi executado pelo usuário no campo <code>Caller</code>.</p></td>
</tr>
<tr class="even">
<td><p><code>CmdletParameters</code></p></td>
<td><p>Este campo contém os parâmetros que foram especificados quando o cmdlet no campo <code>CmdletName</code> foi executado. O valor especificado com o parâmetro, se houver, também é armazenado nesse campo, mas não é visível na saída-padrão. Para obter mais informações sobre como acessar as informações adicionais nesse campo, consulte <a href="search-the-role-group-changes-or-administrator-audit-logs-exchange-2013-help.md">Pesquisar as alterações do grupo de funções ou logs de auditoria do administrador</a>.</p></td>
</tr>
<tr class="odd">
<td><p><code>ModifiedProperties</code></p></td>
<td><p>Este campo contém as propriedades que foram modificadas no objeto do campo <code>ObjectModified</code>. O valor antigo da propriedade e o novo valor que foi armazenado também é armazenado nesse campo, mas não é visível na saída-padrão. Para obter mais informações sobre como acessar as informações adicionais nesse campo, consulte <a href="search-the-role-group-changes-or-administrator-audit-logs-exchange-2013-help.md">Pesquisar as alterações do grupo de funções ou logs de auditoria do administrador</a>.</p>

> [!IMPORTANT]
> Esse campo só é preenchido se o parâmetro <EM>LogLevel</EM> no cmdlet <STRONG>Set-AdminAuditLogConfig</STRONG> for definido como <CODE>Verbose</CODE>.


</td>
</tr>
<tr class="even">
<td><p><code>Caller</code></p></td>
<td><p>Este campo contém a conta do usuário que executou o cmdlet no campo <code>CmdletName</code>.</p></td>
</tr>
<tr class="odd">
<td><p><code>Succeeded</code></p></td>
<td><p>Este campo especifica se o cmdlet no campo <code>CmdletName</code> foi executado com êxito. O valor é <code>True</code> ou <code>False</code>.</p></td>
</tr>
<tr class="even">
<td><p><code>Error</code></p></td>
<td><p>Este campo contém a mensagem de erro gerada por causa da falha de conclusão do cmdlet no campo <code>CmdletName</code>.</p></td>
</tr>
<tr class="odd">
<td><p><code>RunDate</code></p></td>
<td><p>Este campo contém a data e a hora da execução do cmdlet no campo <code>CmdletName</code>. A data e a hora são armazenadas em formato UTC (Tempo Universal Coordenado).</p></td>
</tr>
<tr class="even">
<td><p><code>OriginatingServer</code></p></td>
<td><p>Esse campo indica o servidor em que o cmdlet especificado no campo <code>CmdletName</code> foi executado.</p></td>
</tr>
<tr class="odd">
<td><p><code>Identity</code></p></td>
<td><p>Esse campo é usado internamente pelo Exchange.</p></td>
</tr>
<tr class="even">
<td><p><code>IsValid</code></p></td>
<td><p>Esse campo é usado internamente pelo Exchange.</p></td>
</tr>
<tr class="odd">
<td><p><code>ObjectState</code></p></td>
<td><p>Esse campo é usado internamente pelo Exchange.</p></td>
</tr>
</tbody>
</table>


Voltar ao início

## Relatórios de auditoria de EAC

A página de **auditoria** no EAC possui diversos relatórios que fornecem informações sobre vários tipos de alterações de configuração administrativa e de conformidade. Os relatórios a seguir fornecem informações sobre alterações nas configurações em sua organização:

  - **Relatório de grupo de funções de Administrador**   Este relatório permite que você pesquise alterações nos grupos de função de gerenciamento que você especifica dentro de um período de tempo especificado. Os resultados retornados incluem os grupos de função que foram alterados, quem os alterou e quando, além de quais alterações foram feitas. Um valor máximo de 3.000 entradas pode ser retornado. Se sua pesquisa retornar mais de 3.000 entradas, use o relatório de **Log de auditoria de administrador** ou o cmdlet **Search-AdminAuditLog**.

  - **Log de auditoria de administrador**   Este relatório permite que você exporte as entradas de log de auditoria gravadas dentro de um período de tempo especificado para um arquivo XML e depois envie o arquivo por email para um destinatário especificado por você. Para mais informações sobre o conteúdo do arquivo XML, consulte [Estrutura de log de auditoria do administrador](administrator-audit-log-structure-exchange-2013-help.md).

Para mais informações sobre como usar esses relatórios, consulte [Pesquisar as alterações do grupo de funções ou logs de auditoria do administrador](search-the-role-group-changes-or-administrator-audit-logs-exchange-2013-help.md).

Para obter informações sobre outros relatórios incluídos na página de **auditoria**, consulte [Relatórios de auditoria do Exchange](exchange-auditing-reports-exchange-2013-help.md).

## Cmdlet Search-AdminAuditLog

Quando o cmdlet **Search-AdminAuditLog** é executado, todas as entradas de log de auditoria que correspondem aos critérios de pesquisa que você especificou são retornados. Você pode especificar os seguintes critérios de pesquisa:

  - **Cmdlets**   Especifica os cmdlets que você quer pesquisar no log de auditoria do administrador.

  - **Parâmetros**   Especifica os parâmetros, separados por vírgula, que você quer pesquisar no log de auditoria do administrador. Você pode pesquisar parâmetros somente se você especificar um cmdlet a ser pesquisado.

  - **Data final**   Direciona os resultados do log de auditoria do administrador para as entradas de log que ocorreram na data especificada ou antes.

  - **Data inicial**   Direciona os resultados do log de auditoria do administrador para as entradas de log que ocorreram na data especificada ou depois.

  - **IDs de objeto**   Especifica que somente as entradas de log de auditoria de administrador que contenham os objetos alterados especificados devem ser retornadas

  - **IDs de usuário**   Especifica que somente as entradas de log de auditoria de administrador que contenham as IDs especificadas do usuário que executou o cmdlet devem ser retornadas.

  - **Conclusão bem-sucedida**   Especifica que somente as entradas de log de auditoria de administrador que indicaram sucesso ou falha podem ser retornadas.

Cada entrada de log de auditoria retornada contém as informações descritas na tabela de Audit Log Contents. Por padrão, somente as 1.000 primeiras entradas de log que correspondam aos critérios que você especifica são retornadas. Contudo, é possível substituir esse padrão e retornar mais ou menos entradas usando o parâmetro *ResultSize*. É possível especificar um valor de `Unlimited` com o parâmetro *ResultSize* para retornar todas as entradas de log que correspondam aos critérios especificados.

Para obter informações sobre como usar o cmdlet **Search-AdminAuditLog**, consulte [Pesquisar as alterações do grupo de funções ou logs de auditoria do administrador](search-the-role-group-changes-or-administrator-audit-logs-exchange-2013-help.md).

## Cmdlet New-AdminAuditLogSearch

O cmdlet **New-AdminAuditLogSearch** pesquisa o log de auditoria da mesma maneira que o cmdlet **Search-AdminAuditLog**. Contudo, em vez de exibir os resultados da pesquisa do log de auditoria no Shell, o cmdlet **New-AdminAuditLogSearch** executa a pesquisa e depois envia por email os resultados da pesquisa para um destinatário especificado. Os resultados são incluídos como um anexo XML à mensagem de email.

É possível usar os mesmos critérios de pesquisa com o cmdlet **New-AdminAuditLogSearch** que é usado no cmdlet **Search-AdminAuditLog**. Para obter uma lista com critérios de pesquisa, consulte Search-AdminAuditLog Cmdlet.

Após a execução do cmdlet **New-AdminAuditLogSearch**, o Exchange pode levar até 15 minutos para entregar o relatório ao destinatário especificado. O relatório com o arquivo XML anexado pode ser de, no máximo, 10 megabytes (MB). O arquivo XML contém as mesmas informações descritas na tabela de Audit Log Contents. Para mais informações sobre a estrutura do arquivo XML, consulte [Estrutura de log de auditoria do administrador](administrator-audit-log-structure-exchange-2013-help.md).


> [!NOTE]
> O Outlook Web App não permite que você abra anexos XML por padrão. O Exchange pode ser configurado para permitir que os anexos XML sejam visualizados usando o Outlook Web App, ou você pode usar outro cliente de email, como o Microsoft Outlook, para exibir o anexo. Para saber mais sobre como configurar o Outlook Web App para permitir a exibição de um anexo XML, confira <A href="view-or-configure-outlook-web-app-virtual-directories-exchange-2013-help.md">Exibir ou configurar diretórios virtuais do Outlook Web App</A>.



Para informações sobre como usar o cmdlet **New-AdminAuditLogSearch**, consulte [Pesquisar as alterações do grupo de funções ou logs de auditoria do administrador](search-the-role-group-changes-or-administrator-audit-logs-exchange-2013-help.md).

Voltar ao início

## Entradas manuais de log de auditoria

Além de os cmdlets do Exchange serem registrados em log quando são executados, o Exchange 2013 permite que você grave manualmente entradas de log no log de auditoria. O Exchange 2013 suporta isso usando o cmdlet **Write-AdminAuditLog** . As situações nas quais você pode querer adicionar uma entrada manual de log são as seguintes:

  - Entrada e saída de script personalizado

  - Informações de controle de alterações

  - Horário de início e término de manutenção

Com o cmdlet **Write-AdminAuditLog** , você especifica uma cadeia de textos a ser incluída no log de auditoria usando o parâmetro *Comment*. O parâmetro *Comment* aceita uma cadeia alfanumérica de até 500 caracteres. Na entrada do log de auditoria manual, junto com a cadeia de caracteres de comentários, estão as mesmas informações capturadas quando um cmdlet do Exchange for registrado em log. Para uma descrição de cada campo incluído no log de auditoria, consulte a tabela em Audit Log Contents.

É possível recuperar as entradas manuais de log de auditoria da mesma maneira que qualquer outra entrada de log, usando a página de **auditoria** do EAC ou usando os cmdlets **Search-AdminAuditLog** ou **New-AdminAuditLogSearch**.

Para exibir o conteúdo do parâmetro *Comment* no cmdlet **Write-AdminAuditLog** em uma entrada manual de log de auditoria, consulte [Pesquisar as alterações do grupo de funções ou logs de auditoria do administrador](search-the-role-group-changes-or-administrator-audit-logs-exchange-2013-help.md).

## Replicação do Active Directory

Auditoria do administrador log depende de replicação de Active Directory para replicar as definições de configuração que você especificar para os controladores de domínio em sua organização. Dependendo das suas configurações de replicação, as alterações feitas podem não ser imediatamente aplicadas a todos os servidores executando o Exchange 2013 ou Exchange 2010 em sua organização.

## Agente de Log de Auditoria de Admin

O agente de extensão de cmdlet integrado de Log de Auditoria de Admin realiza o registro em log de auditoria de administrador de operações do cmdlet no Exchange 2013. Esse agente lê a configuração do log de auditoria e realiza uma avaliação de cada cmdlet executado em sua organização. Se os critérios especificados na configuração do log de auditoria corresponderem ao cmdlet que está sendo executado, o agente gerará um log de auditoria.

O agente de Log de Auditoria de Admin vem habilitado por padrão, e isso é necessário para que o log de auditoria funcione. Ele não pode ser desabilitado e sua prioridade não pode ser alterada. Para mais informações sobre agentes de extensão de cmdlet, consulte [Agentes de extensão de cmdlet](cmdlet-extension-agents-exchange-2013-help.md).

