---
title: Solução de problemas conjunto de integridade do ECP
TOCTitle: Solução de problemas conjunto de integridade do ECP
ms:assetid: 0a1cfcd5-585c-4a0a-9d3c-28dc49e16a6c
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/ms.exch.scom.ecp(v=EXCHG.150)
ms:contentKeyID: 53275609
ms.date: 03/07/2017
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Solução de problemas conjunto de integridade do ECP

 

_**Aplica-se a:**Exchange Server 2013, Project Server 2013_

_**Tópico modificado em:**2015-03-09_

O conjunto de integridade do Painel de Controle do Exchange (ECP) monitora a integridade geral do Centro de Administração do Exchange e do serviço de configuração do usuário do Outlook Web App (OWA). O conjunto de integridade do ECP tem uma relação bem próxima com o seguinte conjunto de integridade:

[Solucionando problemas de ECP. Conjunto de integridade de proxy](troubleshooting-ecp-proxy-health-set.md)

Se você receber um alerta que especifica que o conjunto de integridade do ECP não está íntegro, que isso indica um problema que pode impedir que os usuários acessem o EAC.

## Explicação

O serviço EAC é monitorado usando as seguintes sondas e monitores.


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
<td><p>EacSelfTestProbe</p></td>
<td><p>ECP</p></td>
<td><p>Active Directory</p></td>
<td><p>EacSelfTestMonitor</p></td>
</tr>
<tr class="even">
<td><p>EacDeepTestProbe</p></td>
<td><p>ECP</p></td>
<td><p>Active Directory</p></td>
<td><p>EacDeepTestMonitor</p></td>
</tr>
</tbody>
</table>


Para obter mais informações sobre sondas e monitores, consulte [Desempenho e a integridade do servidor](https://technet.microsoft.com/pt-br/library/jj150551\(v=exchg.150\)).

## Ação do usuário

Quando você recebe um alerta de um conjunto de integridade, a mensagem de email contém as seguintes informações:

  - Nome do servidor que enviou o alerta

  - Hora e data em que o alerta ocorreu

  - Informações de autenticação e credenciais

  - Rastreamento de exceções completo do último erro, incluindo dados de diagnóstico e informações de cabeçalho HTTP específicas
    
    **Observação**   Você pode usar as informações no rastreamento de exceções completo para ajudar a solucionar o problema.

É possível que o serviço tenha se recuperado após a emissão do alerta. Portanto, quando você receber um alerta que especifica que o conjunto de integridade não está íntegro, primeiro verifique se o problema ainda existe. Se o problema existir, execute as ações de recuperação apropriadas descritas nas seções seguintes.

## Verificar se o problema ainda existe

1.  Identifique o nome do conjunto de integridade e o nome do servidor no alerta.

2.  Os detalhes da mensagem fornecem informações sobre a causa exata do alerta. Na maioria dos casos, os detalhes da mensagem fornecem informações sobre solução de problemas suficientes para identificar a causa raiz. Se os detalhes da mensagem não estiverem claros, execute estas etapas:
    
    1.  Abra o Shell de Gerenciamento do Exchange, e em seguida, execute o seguinte comando para recuperar os detalhes do conjunto de integridade que emitiu o alerta:
        
            Get-ServerHealth -Identity <ServerName> -HealthSet <HealthSetName>
        
        Por exemplo, para recuperar o ECP integridade definir detalhes sobre Server1. contoso.com, execute o seguinte comando:
        
            Get-ServerHealth -Identity server1.contoso.com -HealthSetName ECP
    
    2.  Verifique a saída do comando para determinar qual monitor relatou o erro. O valor **AlertValue** do monitor que emitiu o alerta será `Unhealthy`.
    
    3.  Execute novamente a sonda associada do monitor que está em estado não íntegro. Consulte a tabela na seção Explanation para encontrar a sonda associada. Para fazer isso, execute o seguinte comando:
        
            Invoke-MonitoringProbe <HealthSetName>\<ProbeName> -Server <ServerName> | Format-List
        
        Por exemplo, vamos supor que o monitor com falha seja o **EacSelfTestMonitor**. A sonda associada a esse monitor é **EacSelfTestProbe**. Para executar essa sonda em server1.contoso.com, execute o seguinte comando:
        
            Invoke-MonitoringProbe ECP\EacSelfTestProbe -Server server1.contoso.com | Format-List
    
    4.  Na saída do comando, verifique o valor **Resultado** da sonda. Se o valor for **Êxito**, significa que o problema foi um erro transitório e não existe mais. Caso contrário, consulte as etapas de recuperação descritas nas seções seguintes.

## Ações de recuperação para EacSelfTestMonitor e EacDeepTestMonitor

1.  Inicie o Gerenciador do IIS e conecte-se ao servidor que está relatando o problema. Clique em **Pools de aplicativos** e recicle o pool de aplicativos do ECP chamado **MSExchangeECPAppPool**.

2.  Execute novamente a sonda associada conforme mostrado na etapa 2c na seção Verifying the issue still exists.

3.  Se o problema ainda existir, recicle todo o serviço do IIS usando o utilitário IISReset.

4.  Execute novamente a sonda associada conforme mostrado na etapa 2c na seção Verifying the issue still exists.

5.  Se a sonda falhar, reinicie o servidor.

6.  Após a reinicialização do servidor, execute novamente a sonda associada, conforme exibido na etapa 2c, na seção Verifying the issue still exists.

7.  Se a sonda continuar a falhar, talvez você precise de ajuda para resolver esse problema. Contate um profissional do Suporte Microsoft para resolver esse problema. Para entrar em contato com um profissional do Suporte Microsoft, visite o [Centro de Soluções do Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=180809). No painel de navegação, clique em **Recursos e opções de suporte** e use uma das opções listadas em **Obter suporte técnico** para entrar em contato com um profissional do Suporte Microsoft. Como a sua organização pode ter um procedimento específico para entrar em contato diretamente os Serviços de Suporte a Produtos Microsoft, tenha certeza de consultar primeiro as diretrizes da sua organização.

## Para obter mais informações

[Novidades do Exchange 2013](https://technet.microsoft.com/pt-br/library/jj150540\(v=exchg.150\))

[Cmdlets do Exchange 2013](https://technet.microsoft.com/pt-br/library/bb124413\(v=exchg.150\))

[Centro de administração do Exchange no Exchange 2013](https://technet.microsoft.com/pt-br/library/jj150562\(v=exchg.150\))

