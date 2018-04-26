---
title: Conjunto de integridade FIPS para solução de problemas
TOCTitle: Conjunto de integridade FIPS para solução de problemas
ms:assetid: 96e1b096-9cb5-426f-a84e-50d5599e4bbb
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/ms.exch.scom.fips(v=EXCHG.150)
ms:contentKeyID: 54652031
ms.date: 03/07/2017
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Conjunto de integridade FIPS para solução de problemas

 

_**Aplica-se a:**Exchange Server 2013, Project Server 2013_

_**Tópico modificado em:**2016-12-09_

O conjunto de integridade **FIPS** monitora a integridade geral das configurações padrões de processamento de informação Federal (FIPS) nos servidores Exchange. Para obter mais informações sobre FIPS 140, consulte [FIPS 140 validação](https://go.microsoft.com/fwlink/p/?linkid=521913).

Se você receber um alerta que indica que o conjunto de integridade **FIPS** não está íntegro, isso indica um problema que pode impedir que seu servidor Exchange usando os processos e componentes de 140 compatível com FIPS.

## Explicação

O serviço **FIPS** é monitorado usando as seguintes sondas e monitores.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Sonda</th>
<th>Conjunto de integridade</th>
<th>Monitores associados</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Nenhum (notificação ou seleção)</p></td>
<td><p>FIPS</p></td>
<td><p>CrashEvent.scanningprocess</p></td>
</tr>
<tr class="even">
<td><p>Nenhum (notificação ou seleção)</p></td>
<td><p>FIPS</p></td>
<td><p>MaintenanceFailureMonitor.FIPS</p></td>
</tr>
<tr class="odd">
<td><p>Nenhum (notificação ou seleção)</p></td>
<td><p>FIPS</p></td>
<td><p>MaintenanceTimeoutMonitor.FIPS</p></td>
</tr>
<tr class="even">
<td><p>Nenhum (notificação ou seleção)</p></td>
<td><p>FIPS</p></td>
<td><p>PrivateWorkingSetWarning.scanningprocess</p></td>
</tr>
<tr class="odd">
<td><p>Nenhum (notificação ou seleção)</p></td>
<td><p>FIPS</p></td>
<td><p>PrivateWorkingSetError.scanningprocess</p></td>
</tr>
<tr class="even">
<td><p>Nenhum (notificação ou seleção)</p></td>
<td><p>FIPS</p></td>
<td><p>ProcessProcessorTimeWarning.scanningprocess</p></td>
</tr>
<tr class="odd">
<td><p>Nenhum (notificação ou seleção)</p></td>
<td><p>FIPS</p></td>
<td><p>ProcessProcessorTimeError.scanningprocess</p></td>
</tr>
</tbody>
</table>


Para obter mais informações sobre sondas e monitores, consulte [Desempenho e a integridade do servidor](https://technet.microsoft.com/pt-br/library/jj150551\(v=exchg.150\)).

## Ação do usuário

É possível que o serviço recuperados após ele emitiu o alerta. Portanto, quando você recebe um alerta que especifica o conjunto de integridade **FIPS** não está íntegro, primeiro verificar se o problema ainda existe. Se o problema existir, execute as ações de recuperação apropriadas descritas na seção a seguir.

## Verificar se o problema

1.  Identifique o nome do conjunto de integridade e o nome do servidor que são fornecidas no alerta.

2.  Os detalhes de mensagem fornecem informações sobre a causa exata do alerta. Na maioria dos casos, os detalhes de mensagem fornecem informações de solução de problemas suficientes para ajudar a identificar a causa raiz. Se os detalhes da mensagem não criptografados, faça o seguinte:
    
    1.  Abra o Shell de Gerenciamento do Exchange e execute o seguinte comando para recuperar os detalhes do conjunto de integridade que emitiu o alerta:
        
            Get-ServerHealth <server name> | ?{$_.HealthSetName -eq "<health set name>"}
        
        Por exemplo, para recuperar o **FIPS** integridade definir detalhes sobre Server1. contoso.com, execute o seguinte comando:
        
            Get-ServerHealth server1.contoso.com | ?{$_.HealthSetName -eq "FIPS"}
    
    2.  Analise a saída para determinar o monitor que tenha reportado o erro do comando. O valor de **AlertValue** para o monitor que emitiu o alerta será **não íntegra**.

