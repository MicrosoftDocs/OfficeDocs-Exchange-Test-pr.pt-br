---
title: 'Estrutura de log de auditoria do administrador: Exchange 2013 Help'
TOCTitle: Estrutura de log de auditoria do administrador
ms:assetid: 87e259c9-c884-4d53-bd78-d13f2300d73e
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Ff459251(v=EXCHG.150)
ms:contentKeyID: 50556237
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Estrutura de log de auditoria do administrador

 

_**Aplica-se a:**Exchange Server 2013_

_**Tópico modificado em:**2015-03-09_

Logs de auditoria do administrador contém um registro de todos os cmdlets e os parâmetros que foram executados em Exchange Shell de gerenciamento e por Exchange Centro de administração (EAC). Eles são criados sob demanda quando você executa o administrador do relatório do log de auditoria no EAC, ou quando você executa o cmdlet **New-AdminAuditLogSearch** no Shell. Para obter mais informações sobre logs de auditoria, consulte [Log de auditoria de administrador](administrator-audit-logging-exchange-2013-help.md).

Os logs de auditoria são arquivos XML e podem conter várias entradas de log de auditoria. A tabela a seguir descreve cada marca XML e seus atributos associados.

Procurando tarefas de gerenciamento relacionadas aos logs de auditoria do administrador? Consulte [Gerenciar o administrador do log de auditoria](manage-administrator-audit-logging-exchange-2013-help.md).

### Os atributos e as marcas XML de log de auditoria

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Elemento</th>
<th>Atributo</th>
<th>Descrição</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code>&lt;?xml version=&quot;1.0&quot; encoding=&quot;utf-8&quot;?&gt;</code></p>
<p></p></td>
<td><p><code>N/A</code></p></td>
<td><p>Esta é a marca de declaração de documento XML. Ele está incluído em cada arquivo de XML de log de auditoria e contém o número de versão XML e o valor de codificação de caracteres.</p></td>
</tr>
<tr class="even">
<td><p><code>SearchResults</code></p></td>
<td><p><code>N/A</code></p></td>
<td><p>Nesta marca contém todas as entradas de log de auditoria no arquivo XML. A marca de <code>Event</code> é um filho da marca.</p>
<p>Há apenas uma marca de <code>SearchResults</code> por um arquivo XML.</p></td>
</tr>
<tr class="odd">
<td><p><code>Event</code></p></td>
<td><p><code> </code></p></td>
<td><p>Nesta marca contém a entrada de log de auditoria para um cmdlet individual. Nesta marca contém o <code>Caller</code>, <code>Cmdlet</code>, <code>ObjectModified</code>, <code>RunDate</code>, <code>Succeeded</code>, <code>Error</code>e <code>OriginatingServer</code> atributos. As marcas de <code>CmdletParameters</code> e <code>ModifiedProperties</code> são filhos da marca.</p>
<p>Não há uma marca de <code>Event</code> por entrada do log de auditoria.</p></td>
</tr>
<tr class="even">
<td><p><code> </code></p></td>
<td><p><code>Caller</code></p></td>
<td><p>Este atributo contém a conta de usuário do usuário que executou o cmdlet no atributo <code>Cmdlet</code> .</p></td>
</tr>
<tr class="odd">
<td><p><code> </code></p></td>
<td><p><code>Cmdlet</code></p></td>
<td><p>Este atributo contém o nome do cmdlet que foi executado pelo usuário no atributo <code>Caller</code> .</p></td>
</tr>
<tr class="even">
<td><p><code> </code></p></td>
<td><p><code>ObjectModified</code></p></td>
<td><p>Este atributo contém o objeto que foi modificado pelo cmdlet especificado no atributo <code>Cmdlet</code> . A marca <code>ModifiedProperties</code> mostra quais propriedades foram modificadas neste objeto.</p></td>
</tr>
<tr class="odd">
<td><p><code> </code></p></td>
<td><p><code>RunDate</code></p></td>
<td><p>Este atributo contém a data e hora de quando o cmdlet no atributo <code>Cmdlet</code> foi executado.</p></td>
</tr>
<tr class="even">
<td><p><code> </code></p></td>
<td><p><code>Succeeded</code></p></td>
<td><p>Este atributo especifica se o cmdlet no atributo <code>Cmdlet</code> foi executada com êxito. O valor é <code>True</code> ou <code>False</code>.</p></td>
</tr>
<tr class="odd">
<td><p><code> </code></p></td>
<td><p><code>Error</code></p></td>
<td><p>Este atributo contém a mensagem de erro gerada se o cmdlet no atributo <code>Cmdlet</code> com falha para concluir com êxito. Se nenhum erro for encontrado, o valor é definido como <code>None</code>.</p></td>
</tr>
<tr class="even">
<td><p><code> </code></p></td>
<td><p><code>OriginatingServer</code></p></td>
<td><p>Este atributo contém o servidor no qual o cmdlet especificado no atributo <code>Cmdlet</code> foi executado.</p></td>
</tr>
<tr class="odd">
<td><p><code>CmdletParameters</code></p></td>
<td><p><code>N/A</code></p></td>
<td><p>Nesta marca contém todos os parâmetros especificados quando o cmdlet foi executado. A marca de <code>Parameter</code> é um filho da marca.</p>
<p>Não há uma marca de <code>CmdletParameters</code> por marca <code>Event</code> .</p></td>
</tr>
<tr class="even">
<td><p><code>Parameter</code></p></td>
<td><p><code> </code></p></td>
<td><p>Nesta marca contém um parâmetro individual que foi especificado quando o cmdlet foi executado. Nesta marca contém os atributos <code>Name</code> e <code>Value</code> .</p>
<p>Pode haver várias marcas <code>Parameter</code> por marca <code>CmdletParameters</code> .</p></td>
</tr>
<tr class="odd">
<td><p><code> </code></p></td>
<td><p><code>Name</code></p></td>
<td><p>Este atributo contém o nome do parâmetro que foi especificado no cmdlet que foi executado.</p></td>
</tr>
<tr class="even">
<td><p><code> </code></p></td>
<td><p><code>Value</code></p></td>
<td><p>Este atributo contém o valor que foi fornecido no parâmetro especificado no atributo <code>Name</code> .</p></td>
</tr>
<tr class="odd">
<td><p><code>ModifiedProperties</code></p></td>
<td><p><code>N/A</code></p></td>
<td><p>Nesta marca contém todas as propriedades que foram modificadas pelo cmdlet que foi executado. A marca de <code>Property</code> é um filho da marca.</p>
<p>Não há uma marca de <code>ModifiedProperties</code> por marca <code>Event</code> .</p>

> [!IMPORTANT]
> Esta marca é preenchida somente se o parâmetro <EM>LogLevel</EM> no cmdlet <STRONG>Set-AdminAuditLogConfig</STRONG> estiver definido como <CODE>Verbose</CODE>.


</td>
</tr>
<tr class="even">
<td><p><code>Property</code></p></td>
<td><p><code> </code></p></td>
<td><p>Nesta marca contém uma propriedade individual que foi especificada quando o cmdlet foi executado. Nesta marca contém os atributos <code>Name</code>, <code>OldValue</code>e <code>NewValue</code> .</p>
<p>Pode haver várias marcas <code>Property</code> por marca <code>ModifiedProperties</code> .</p></td>
</tr>
<tr class="odd">
<td><p><code> </code></p></td>
<td><p><code>Name</code></p></td>
<td><p>Este atributo contém o nome da propriedade que foi modificado quando o cmdlet foi executado.</p></td>
</tr>
<tr class="even">
<td><p><code> </code></p></td>
<td><p><code>OldValue</code></p></td>
<td><p>Este atributo contém o valor que foi contido na propriedade especificada no atributo <code>Name</code> antes que ela foi alterada.</p></td>
</tr>
<tr class="odd">
<td><p><code> </code></p></td>
<td><p><code>NewValue</code></p></td>
<td><p>Este atributo contém o valor que a propriedade no atributo <code>Name</code> foi alterada para.</p></td>
</tr>
</tbody>
</table>


## Entrada de log de auditoria de exemplo

O exemplo a seguir é um exemplo de uma entrada de log de auditoria típica. Com base nas informações da entrada de log, nós sabemos que ocorreu o seguinte:

  - Em 18/10/2012 às 15:48. horário de verão do Pacífico (UTC-7), o usuário `Administrator` executou o cmdlet **Set-Mailbox**.

  - Os dois parâmetros a seguir foram fornecidos quando o cmdlet **Set-Mailbox** foi executado:
    
      - *Identity* com um valor de `david`
    
      - *ProhibitSendReceiveQuota* com um valor de `10GB`

  - As duas propriedades a seguir sobre o objeto `david` foram modificadas:
    

    > [!TIP]
    > As propriedades modificadas são salvas no log de auditoria, porque o parâmetro <EM>LogLevel</EM> no cmdlet <CODE>Set-AdminAuditLogConfig</CODE> foi definido para <CODE>Verbose</CODE> neste exemplo.

    
      - *ProhibitSendReceiveQuota* com um novo valor de `10GB`, que substituiu o valor antigo do `35GB`

  - Operação concluída com êxito sem erros.

<!-- end list -->

    <?xml version="1.0" encoding="utf-8"?>
    <SearchResults>
    
      <Event Caller="corp.e15a.contoso.com/Users/Administrator" Cmdlet="Set-Mailbox" ObjectModified="corp.e15a.contoso.com/Users/david" RunDate="2012-10-18T15:48:15-07:00" Succeeded="true" Error="None" OriginatingServer="WIN8MBX (15.00.0516.032)">
        <CmdletParameters>
          <Parameter Name="Identity" Value="david" />
          <Parameter Name="ProhibitSendReceiveQuota" Value="10 GB (10,737,418,240 bytes)" />
        </CmdletParameters>
        <ModifiedProperties>
          <Property Name="ProhibitSendReceiveQuota" OldValue="35 GB (37,580,963,840 bytes)" NewValue="10 GB (10,737,418,240 bytes)" />
        </ModifiedProperties>
      </Event>
    </SearchResults>

