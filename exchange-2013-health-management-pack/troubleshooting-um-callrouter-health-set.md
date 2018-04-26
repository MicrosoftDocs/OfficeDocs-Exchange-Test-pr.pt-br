---
title: Solucionando problemas de Unificação de mensagens. Conjunto de integridade CallRouter
TOCTitle: Solucionando problemas de Unificação de mensagens. Conjunto de integridade CallRouter
ms:assetid: 444a9038-0952-4823-98fb-99fa59f4a378
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/ms.exch.scom.um.callrouter(v=EXCHG.150)
ms:contentKeyID: 53275624
ms.date: 03/07/2017
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Solucionando problemas de Unificação de mensagens. Conjunto de integridade CallRouter

 

_**Aplica-se a:**Exchange Server 2013_

_**Tópico modificado em:**2015-03-09_

O conjunto de integridade Roteador de Chamadas da Unificação de Mensagens (UM) do Microsoft Exchange monitora a integridade geral do serviço Roteador de Chamadas da UM.

Se você receber um alerta que especifique que a UM não esteja íntegra, isso indicará um problema que pode impedir os usuários de usar o serviço da UM na organização. O conjunto de integridade da UM está intimamente relacionado aos seguintes conjuntos de integridade:

[Solucionando problemas de UM conjunto de integridade](troubleshooting-um-health-set.md)

[Solucionando problemas de Unificação de mensagens. Conjunto de integridade de protocolo](troubleshooting-um-protocol-health-set.md)

## Explicação

O serviço UM.Protocol é monitorado usando as sondas e monitores a seguir


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
<td><p>UMCallRouterTestProbe</p></td>
<td><p>UM.CallRouter</p></td>
<td><p>Serviços de Domínio Active Directory (AD DS)</p></td>
<td><p>UMCallRouterTestMonitor</p></td>
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
        
        Por exemplo, para recuperar detalhes do conjunto de integridade UM.CallRouter sobre o server1.contoso.com, execute o seguinte comando:
        
            Get-ServerHealth server1.contoso.com | ?{$_.HealthSetName -eq "UM.CallRouter"}
    
    2.  Verifique a saída do comando para determinar qual monitor relatou o erro. O valor **AlertValue** do monitor que emitiu o alerta será `Unhealthy`.
    
    3.  Execute novamente a sonda associada do monitor que está em estado não íntegro. Consulte a tabela na seção Explanation para localizar a sonda associada. Para fazer isso, execute o seguinte comando:
        
            Invoke-MonitoringProbe <health set name>\<probe name> -Server <server name> | Format-List
        
        Por exemplo, suponha que o monitor com falha seja **UMCallRouterTestMonitor**. A sonda associada a esse monitor é **UMCallRouterTestProbe**. Para executar essa sonda em server1.contoso.com, execute o seguinte comando:
        
            Invoke-MonitoringProbe UM.CallRouter\UMCallRouterTestMonitor -Server server1.contoso.com | Format-List
    
    4.  Na saída do comando, verifique o valor **Resultado** da sonda. Se o valor for **Êxito**, significa que o problema foi um erro transitório e não existe mais. Caso contrário, consulte as etapas de recuperação descritas nas seções seguintes.

## Etapas para a solução de problemas

Quando você recebe um alerta de um conjunto de integridade, a mensagem de email contém as seguintes informações:

  - Nome do servidor que enviou o alerta

  - Hora e data em que o alerta ocorreu

  - Mecanismo de autenticação usado e informações de credenciais

  - Rastreamento de exceções completo do último erro, incluindo dados de diagnóstico e informações de cabeçalho HTTP específicas
    
    **Observação**   Você pode usar as informações no rastreamento de exceções completo para ajudar a solucionar o problema. A exceção gerada pela sonda contém um Motivo da Falha que descreve por que a sonda falhou.

**Opções Sip para serviço Roteador de Chamadas da UM falharam**

Determine se o serviço Roteador de Chamadas da UM está desabilitado. Se o serviço Roteador de Chamadas da UM não estiver iniciado ou se estiver desabilitado, reinicie o serviço da UM.

**Mias de 50% de chamadas de entrada foram rejeitadas pelo serviço Roteador de Chamadas da UM na última hora**

Examine os logs de eventos no servidor Acesso para Cliente (CAS) para determinar se os objetos da UM, como **umipgateway** e **umhuntgroup**, estão configurados corretamente.

Se os logs de eventos não contiverem informações suficientes, talvez seja necessário habilitar logs de eventos da UM no nível Especialista e então examinar os arquivos do log de rastreamento da UM.

**Mais de {0}% de Proxy de Notificação de Chamada Perdida falharam no Roteador de Chamada da UM na última hora**

Examine os logs de eventos no CAS para determinar se os objetos da UM, como **umipgateway** e **umhuntgroup**, estão configurados corretamente.

Se os logs de eventos não contiverem informações suficientes, talvez seja necessário habilitar logs de eventos da UM no nível Especialista e então examinar os arquivos do log de rastreamento da UM.

**O certificado do Roteador de Chamadas da Unificação de Mensagens do Microsoft Exchange está chegando à data de expiração**

Renove o certificado de serviço do Roteador de Chamadas da UM no CAS.

**Etapas de solução de problemas adicionais:**

1.  Inicie o Gerenciador do IIS e então conecte-se ao servidor que está relatando o problema para determinar se o pool de aplicativos **MSExchangeServicesAppPool** está em execução.

2.  No Gerenciador do IIS, clique em **Pools de Aplicativos** e então recicle o pool de aplicativos **MSExchangeServicesAppPool** ao executar o seguinte comando do Shell:
    
        %SystemRoot%\System32\inetsrv\Appcmd recycle MSExchangeServicesAppPool

3.  Execute novamente a sonda associada conforme mostrado na etapa 2c na seção Verifying the issue still exists.

4.  Se o problema persistir, use o serviço do IIS com o utilitário IISReset ou executando o seguinte comando:
    
        Iisreset /noforce

5.  Execute novamente a sonda associada conforme mostrado na etapa 2c na seção Verifying the issue still exists.

6.  Se o problema ainda existir, reinicie o servidor.

7.  Após o reinício do servidor, execute novamente a sonda associada como mostrado na etapa 2c da seção Verifying the issue still exists.

8.  Se a sonda continuar a falhar, talvez você precise de ajuda para resolver esse problema. Contate um profissional do Suporte Microsoft para resolver esse problema. Para entrar em contato com um profissional do Suporte Microsoft, visite o [Centro de Soluções do Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=180809). No painel de navegação, clique em **Recursos e opções de suporte** e use uma das opções listadas em **Obter suporte técnico** para entrar em contato com um profissional do Suporte Microsoft. Como a sua organização pode ter um procedimento específico para entrar em contato diretamente os Serviços de Suporte a Produtos Microsoft, tenha certeza de consultar primeiro as diretrizes da sua organização.

## Para obter mais informações

[Novidades do Exchange 2013](https://technet.microsoft.com/pt-br/library/jj150540\(v=exchg.150\))

[Cmdlets do Exchange 2013](https://technet.microsoft.com/pt-br/library/bb124413\(v=exchg.150\))

