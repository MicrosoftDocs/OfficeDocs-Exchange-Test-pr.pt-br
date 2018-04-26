---
title: Solucionando problemas de OWA. Conjunto de integridade de proxy
TOCTitle: Solucionando problemas de OWA. Conjunto de integridade de proxy
ms:assetid: 1eaa26ad-b489-402a-ad2d-bfae3b083f42
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/ms.exch.scom.owa.proxy(v=EXCHG.150)
ms:contentKeyID: 53275612
ms.date: 03/07/2017
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Solucionando problemas de OWA. Conjunto de integridade de proxy

 

_**Aplica-se a:**Exchange Server 2013_

_**Tópico modificado em:**2015-03-09_

O conjunto de integridade OWA.Proxy monitora a integridade geral do serviço Outlook Web App.

Se você receber um alerta especificando que o OWA.Proxy não está íntegro, isso indicará um problema que pode impedir os usuários de usarem o serviço Outlook Web App.

## Explicação

O serviço Outlook Web App é monitorado usando as seguintes sondas e monitores.


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
<td><p>OWAProxyTestProbe</p></td>
<td><p>OWA.Proxy</p></td>
<td><p>Active Directory</p></td>
<td><p>OWAProxyTestMonitor</p></td>
</tr>
<tr class="even">
<td><p>OWAanonymouscalendarProbe</p></td>
<td><p>OWA.Proxy</p></td>
<td><p>Active Directory</p></td>
<td><p>OWAProxyTestMonitor</p></td>
</tr>
</tbody>
</table>


Para obter mais informações sobre sondas e monitores, consulte [Desempenho e a integridade do servidor](https://technet.microsoft.com/pt-br/library/jj150551\(v=exchg.150\)).

## Problemas comuns

Essa sonda pode falhar por uma das seguintes razões:

  - O pool de aplicativos que está hospedado no servidor de Acesso para Cliente (CAS) monitorado não está funcionando corretamente.

  - As credenciais de conta de monitoramento não estão corretas.

  - Os controladores de domínio não estão respondendo.

## Ação do usuário

É possível que o serviço tenha se recuperado após a emissão do alerta. Portanto, quando você receber um alerta que especifica que o conjunto de integridade não está íntegro, primeiro verifique se o problema ainda existe. Se o problema existir, execute as ações de recuperação apropriadas descritas nas seções seguintes.

## Verificar se o problema ainda existe

1.  Identifique o nome do conjunto de integridade e o nome do servidor no alerta.

2.  Os detalhes da mensagem fornecem informações sobre a causa exata do alerta. Na maioria dos casos, os detalhes da mensagem fornecem informações sobre solução de problemas suficientes para identificar a causa raiz. Se os detalhes da mensagem não forem claros, faça o seguinte:
    
    1.  Abra o Shell de Gerenciamento do Exchange, e em seguida, execute o seguinte comando para recuperar os detalhes do conjunto de integridade que emitiu o alerta:
        
            Get-ServerHealth <server name> | ?{$_.HealthSetName -eq "<health set name>"}
        
        Por exemplo, para recuperar os detalhes do conjunto de integridade do OWA.Proxy sobre server1.contoso.com, execute o seguinte comando:
        
            Get-ServerHealth server1.contoso.com | ?{$_.HealthSetName -eq "OWA.Proxy"}
    
    2.  Verifique a saída do comando para determinar qual monitor relatou o erro. O valor **AlertValue** do monitor que emitiu o alerta será `Unhealthy`.
    
    3.  Execute novamente a sonda associada do monitor que está em estado não íntegro. Consulte a tabela na seção Explanation para encontrar a sonda associada. Para fazer isso, execute o seguinte comando:
        
            Invoke-MonitoringProbe <health set name>\<probe name> -Server <server name> | Format-List
        
        Por exemplo, vamos supor que o monitor com falha seja o **OWAProxyTestMonitor**. A sonda associada a esse monitor é **OWAProxyTestProbe**. Para executar essa sonda em server1.contoso.com, execute o seguinte comando:
        
            Invoke-MonitoringProbe OWA.Proxy\OWAProxyTestProbe -Server server1.contoso.com | Format-List
    
    4.  Na saída do comando, verifique o valor **Resultado** da sonda. Se o valor for **Êxito**, significa que o problema foi um erro transitório e não existe mais. Caso contrário, consulte as etapas de recuperação descritas nas seções seguintes.

## Ações de recuperação do OWAProxyTestMonitor

Quando você recebe um alerta de um conjunto de integridade, a mensagem de email contém as seguintes informações:

  - Nome do CAS que enviou o alerta

  - Rastreamento de exceções completo do último erro, incluindo dados de diagnóstico e informações de cabeçalho HTTP específicas  
    
    **Observação**   Você pode usar as informações no rastreamento de exceções completo para ajudar a solucionar o problema.

  - Date e hora em que o problema ocorreu

Para resolver esse problema, siga estas etapas:

1.  Revise os logs do protocolo nos servidores CA. Os logs de protocolo estão em *\<diretório de instalação do exchange server\>*\\Logging\\HttpProxy*\\\<protocol\>* no CAS.

2.  Crie uma conta de usuário de teste e, em seguida, faça logon no CAS usando essa conta. Por exemplo, faça logon usando: https:// *\<nomedoservidor\>*/owa.

3.  Inicie o Gerenciador do IIS e conecte-se ao servidor que está reportando o problema a fim de determinar se os pools de aplicativo **MSExchangeServicesAppPools** estão em execução no CAS.

4.  Clique em **Pools de Aplicativo** e recicle os pools de aplicativo **MSExchangeOWAAppPool** e **MSExchangeOWACalendarAppPool** executando o seguinte comando no Shell:
    
        %SystemRoot%\System32\inetsrv\Appcmd recycle APPPOOL MSExchangeOWAAppPool
    
        %SystemRoot%\System32\inetsrv\Appcmd recycle APPPOOL MSExchangeOWACalendarAppPool

5.  Execute novamente a sonda associada conforme mostrado na etapa 2c na seção Verifying the issue still exists.

6.  Se o problema ainda existir, recicle o serviço IIS usando o utilitário IISReset.

7.  Execute novamente a sonda associada conforme mostrado na etapa 2c na seção Verifying the issue still exists.

8.  Se o problema ainda existir, reinicie o servidor.

9.  Após a reinicialização do servidor, execute novamente a sonda associada, conforme exibido na etapa 2c, na seção Verifying the issue still exists.

10. Se a sonda continuar a falhar, talvez você precise de ajuda para resolver esse problema. Contate um profissional do Suporte Microsoft para resolver esse problema. Para entrar em contato com um profissional do Suporte Microsoft, visite o [Centro de Soluções do Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=180809). No painel de navegação, clique em **Recursos e opções de suporte** e use uma das opções listadas em **Obter suporte técnico** para entrar em contato com um profissional do Suporte Microsoft. Como a sua organização pode ter um procedimento específico para entrar em contato diretamente os Serviços de Suporte a Produtos Microsoft, tenha certeza de consultar primeiro as diretrizes da sua organização.

## Para obter mais informações

[Novidades do Exchange 2013](https://technet.microsoft.com/pt-br/library/jj150540\(v=exchg.150\))

[Cmdlets do Exchange 2013](https://technet.microsoft.com/pt-br/library/bb124413\(v=exchg.150\))

[Managing Outlook Web App](https://technet.microsoft.com/pt-br/3814b665-01e8-4881-9a44-163f14789ee4\(exchg.150\)#managing)

