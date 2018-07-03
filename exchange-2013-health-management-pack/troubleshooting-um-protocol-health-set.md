---
title: Solucionando problemas de Unificação de mensagens. Conjunto de integridade de protocolo
TOCTitle: Solucionando problemas de Unificação de mensagens. Conjunto de integridade de protocolo
ms:assetid: 8dd9a16f-77a1-4a8d-aea4-5e96ab922dd4
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/ms.exch.scom.um.protocol(v=EXCHG.150)
ms:contentKeyID: 53275620
ms.date: 03/07/2017
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Solucionando problemas de Unificação de mensagens. Conjunto de integridade de protocolo

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2015-03-09_

A Unificação de mensagens. Conjunto de integridade do protocolo monitora o protocolo de Unificação de mensagens (UM) no servidor de caixa de correio.

Se você receber um alerta que especifica que a Unificação de mensagens. Protocolo não está íntegro, que isso indica um problema que pode impedir que usuários usando o serviço de Unificação de mensagens em sua organização. A Unificação de mensagens. Conjunto de integridade do protocolo está relacionado aos seguintes conjuntos de integridade:

[Solucionando problemas de UM conjunto de integridade](troubleshooting-um-health-set.md)

[Solucionando problemas de Unificação de mensagens. Conjunto de integridade CallRouter](troubleshooting-um-callrouter-health-set.md)

## Explicação

A Unificação de mensagens. Serviço de protocolo é monitorado usando as seguintes sondas e monitores.


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Sonda</th>
<th>Conjunto de integridade</th>
<th>Dependências</th>
<th>Monitores associados</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>UMSelfTestProbe</p></td>
<td><p>UM.Protocol</p></td>
<td><p>Serviços de Domínio Active Directory (AD DS)</p></td>
<td><p>UMSelfTestMonitor</p></td>
</tr>
</tbody>
</table>


Para obter mais informações sobre sondas e monitores, consulte [Desempenho e a integridade do servidor](https://technet.microsoft.com/pt-br/library/jj150551\(v=exchg.150\)).

## Ação do usuário

É possível que o serviço tenha se recuperado após a emissão do alerta. Portanto, quando você receber um alerta que especifica que o conjunto de integridade não está íntegro, primeiro verifique se o problema ainda existe. Se o problema existir, execute as ações de recuperação apropriadas descritas nas seções seguintes.

## Verificar se o problema ainda existe

1.  Identifique o nome do conjunto de integridade e o nome do servidor no alerta.

2.  Os detalhes da mensagem fornecem informações sobre a causa exata do alerta. Na maioria dos casos, os detalhes da mensagem fornecem informações sobre solução de problemas suficientes para identificar a causa raiz. Se os detalhes da mensagem não forem claros, faça o seguinte:
    
    1.  Abra o Shell de Gerenciamento do Exchange, e em seguida, execute o seguinte comando para recuperar os detalhes do conjunto de integridade que emitiu o alerta:
        
            Get-ServerHealth <server name> | ?{$_.HealthSetName -eq "<health set name>"}
        
        Por exemplo, para recuperar a Unificação de mensagens. O conjunto de integridade de protocolo detalhes sobre Server1. contoso.com, execute o seguinte comando:
        
            Get-ServerHealth server1.contoso.com | ?{$_.HealthSetName -eq "UM.Protocol"}
    
    2.  Verifique a saída do comando para determinar qual monitor relatou o erro. O valor **AlertValue** do monitor que emitiu o alerta será `Unhealthy`.
    
    3.  Execute novamente a sonda associada do monitor que está em estado não íntegro. Consulte a tabela na seção Explanation para localizar a sondagem associada. Para fazer isso, execute o seguinte comando:
        
            Invoke-MonitoringProbe <health set name>\<probe name> -Server <server name> | Format-List
        
        Por exemplo, suponha que o monitor de falha é **UMSelfTestMonitor**. A sonda associada a esse monitor é **UMSelfTestProbe**. Para executar essa sonda em Server1, execute o seguinte comando:
        
            Invoke-MonitoringProbe UM.Protocol\UMSelfTestMonitor -Server server1.contoso.com | Format-List
    
    4.  Na saída do comando, verifique o valor **Resultado** da sonda. Se o valor for **Êxito**, significa que o problema foi um erro transitório e não existe mais. Caso contrário, consulte as etapas de recuperação descritas nas seções seguintes.

## Etapas para a solução de problemas

Quando você recebe um alerta de um conjunto de integridade, a mensagem de email contém as seguintes informações:

  - Nome do servidor que enviou o alerta

  - Hora e data em que o alerta ocorreu

  - Mecanismo de autenticação usado e informações de credenciais

  - Rastreamento de exceções completo do último erro, incluindo dados de diagnóstico e informações de cabeçalho HTTP específicas
    
    **Observação**   Você pode usar as informações no rastreamento de exceções completo para ajudar a solucionar o problema. A exceção gerada pela sonda contém um Motivo da Falha que descreve por que a sonda falhou.

Para obter mais informações sobre como solucionar problemas de mensagens de alerta de UJM, consulte [Solucionando problemas de UM conjunto de integridade](troubleshooting-um-health-set.md)

## Para obter mais informações

[Novidades do Exchange 2013](https://technet.microsoft.com/pt-br/library/jj150540\(v=exchg.150\))

[Cmdlets do Exchange 2013](https://technet.microsoft.com/pt-br/library/bb124413\(v=exchg.150\))

