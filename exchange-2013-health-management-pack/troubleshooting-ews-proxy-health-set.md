---
title: Solucionando problemas de EWS. Conjunto de integridade de proxy
TOCTitle: Solucionando problemas de EWS. Conjunto de integridade de proxy
ms:assetid: 5bfbf7e9-d52d-4a3d-91ac-72427c6cb37d
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/ms.exch.scom.ews.proxy(v=EXCHG.150)
ms:contentKeyID: 53275628
ms.date: 03/07/2017
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Solucionando problemas de EWS. Conjunto de integridade de proxy

 

_**Aplica-se a:**Exchange Server 2013_

_**Tópico modificado em:**2015-03-09_

O conjunto de integridade do EWS.Proxy monitora a disponibilidade da infraestrutura de proxy dos Serviços Web do Exchange (EWS) no servidor de Acesso para Cliente (CAS). O conjunto de integridade do EWS.Proxy está intimamente relacionado com o seguinte conjunto de integridade:

[Solucionando problemas de conjunto de integridade de ClientAccess.Proxy](troubleshooting-clientaccess-proxy-health-set.md)

Se você receber um alerta que especifica que o EWS.Proxy não é íntegro, isso indica um problema que pode impedir que os usuários acessem o serviço EWS.

## Explicação

O serviço EWS é monitorado usando as seguintes sondagens e monitoramentos.


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
<td><p>EWSProxyTestProbe</p></td>
<td><p>EWS.Proxy</p></td>
<td><p>Active Directory</p></td>
<td><p>EWSProxyTestMonitor</p></td>
</tr>
</tbody>
</table>


Para obter mais informações sobre sondas e monitores, consulte [Desempenho e a integridade do servidor](https://technet.microsoft.com/pt-br/library/jj150551\(v=exchg.150\)).

## Problemas comuns

Essa sonda pode falhar por um dos seguintes motivos:

  - O pool de aplicativos hospedado no CAS monitorado não está funcionando corretamente.

  - As credenciais de conta de monitoramento não estão corretas.

  - Os controladores de domínio não estão respondendo.

## Ação do usuário

É possível que o serviço tenha se recuperado após a emissão do alerta. Portanto, quando você receber um alerta que especifica que o conjunto de integridade não está íntegro, primeiro verifique se o problema ainda existe. Se o problema existir, execute as ações de recuperação apropriadas descritas nas seções seguintes.

## Verificar se o problema ainda existe

1.  Identifique o nome do conjunto de integridade e o nome do servidor no alerta.

2.  Os detalhes da mensagem fornecem informações sobre a causa exata do alerta. Na maioria dos casos, os detalhes da mensagem fornecem informações sobre solução de problemas suficientes para identificar a causa raiz. Se os detalhes da mensagem não forem claros, faça o seguinte:
    
    1.  Abra o Shell de Gerenciamento do Exchange, e em seguida, execute o seguinte comando para recuperar os detalhes do conjunto de integridade que emitiu o alerta:
        
            Get-ServerHealth <server name> | ?{$_.HealthSetName -eq "<health set name>"}
        
        Por exemplo, para recuperar os detalhes do conjunto de integridade do EWS.Proxy sobre server1.contoso.com, execute o seguinte comando:
        
            Get-ServerHealth server1.contoso.com | ?{$_.HealthSetName -eq "EWS.Proxy"}
    
    2.  Verifique a saída do comando para determinar qual monitor relatou o erro. O valor **AlertValue** do monitor que emitiu o alerta será `Unhealthy`.
    
    3.  Execute novamente a sonda associada do monitor que está em estado não íntegro. Consulte a tabela na seção Verifying the issue still exists para localizar a sondagem associada. Para fazer isso, execute o seguinte comando:
        
            Invoke-MonitoringProbe <health set name>\<probe name> -Server <server name> | Format-List
        
        Por exemplo, suponha que o monitor com falha é **EWSProxyTestMonitor**. A sondagem associada a esse monitor é **EWSProxyTestProbe**. Para executar essa sonda em server1.contoso.com, execute o seguinte comando:
        
            Invoke-MonitoringProbe EWS.Proxy\EWSProxyTestProbe -Server server1.contoso.com | Format-List
    
    4.  Na saída do comando, verifique o valor **Resultado** da sonda. Se o valor for **Êxito**, significa que o problema foi um erro transitório e não existe mais. Caso contrário, consulte as etapas de recuperação descritas nas seções seguintes.

## Ações de recuperação de EWSProxyTestMonitor

Quando você receber um alerta de um conjunto de integridade, a mensagem de email irá conter as seguintes informações:

  - Nome do CAS que enviou o alerta

  - Rastreamento de exceções completo do último erro, incluindo dados de diagnóstico e informações de cabeçalho HTTP específicas
    
    Você pode usar as informações no rastreamento de exceções completo para ajudar a solucionar o problema.

  - Date e hora em que o problema ocorreu

Para resolver esse problema, siga estas etapas:

1.  Examine os logs de protocolo nos servidores de CA. Os logs de protocolo estão em *\<diretório de instalação do exchange server\>*\\Logging\\HttpProxy*\\\<protocol\>* no CAS.

2.  Crie uma conta de usuário de teste e, em seguida, faça logon no CAS usando essa conta. Por exemplo, use o seguinte endereço de logon: https:// *\<nome\_do\_servidor\>*/owa

3.  Inicie o Gerenciador do IIS e conecte-se ao servidor que está relatando o problema para determinar se o pool de aplicativos **MSExchangeServicesAppPool** está sendo executado no CAS.

4.  Clique em **Pools de Aplicativos** e recicle o pool de aplicativos **MSExchangeServicesAppPool** executando o seguinte comando a partir do Shell:
    
        %SystemRoot%\System32\inetsrv\Appcmd recycle MSExchangeServicesAppPool

5.  Execute novamente a sonda associada conforme mostrado na etapa 2c na seção Verifying the issue still exists.

6.  Se o problema ainda existir, recicle o serviço IIS usando o utilitário IISReset.

7.  Execute novamente a sonda associada conforme mostrado na etapa 2c na seção Verifying the issue still exists.

8.  Se o problema ainda existir, reinicie o servidor.

9.  Depois que o servidor reiniciar, execute novamente a sondagem associada como mostrado na etapa 2c na seção Verifying the issue still exists.

10. Se a sonda continuar a falhar, talvez você precise de ajuda para resolver esse problema. Contate um profissional do Suporte Microsoft para resolver esse problema. Para entrar em contato com um profissional do Suporte Microsoft, visite o [Centro de Soluções do Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=180809). No painel de navegação, clique em **Recursos e opções de suporte** e use uma das opções listadas em **Obter suporte técnico** para entrar em contato com um profissional do Suporte Microsoft. Como a sua organização pode ter um procedimento específico para entrar em contato diretamente os Serviços de Suporte a Produtos Microsoft, tenha certeza de consultar primeiro as diretrizes da sua organização.

## Para obter mais informações

[Novidades do Exchange 2013](https://technet.microsoft.com/pt-br/library/jj150540\(v=exchg.150\))

[Cmdlets do Exchange 2013](https://technet.microsoft.com/pt-br/library/bb124413\(v=exchg.150\))

