---
title: Solucionando problemas de OWA. Conjunto de integridade de protocolo
TOCTitle: Solucionando problemas de OWA. Conjunto de integridade de protocolo
ms:assetid: fe172da8-65d3-43e0-ba62-d36a1b05fc11
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/ms.exch.scom.owa.protocol(v=EXCHG.150)
ms:contentKeyID: 53275638
ms.date: 03/07/2017
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Solucionando problemas de OWA. Conjunto de integridade de protocolo

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2015-03-09_

O OWA. Conjunto de integridade do protocolo monitora o protocolo Outlook Web App no servidor de caixa de correio.

Se você receber um alerta que especifica que OWA. Protocolo não está íntegro, que isso indica um problema que pode impedir que os usuários acessem suas caixas de correio usando Outlook Web App.

## Explicação

O serviço do OWA é monitorado usando as seguintes sondas e monitores.


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
<td><p>OwaSelfTestProbe</p></td>
<td><p>OWA.Protocol</p></td>
<td><p>Nenhum</p></td>
<td><p>OwaSelfTestMonitor</p></td>
</tr>
<tr class="even">
<td><p>OwaDeepTestProbe</p></td>
<td><p>OWA.Protocol</p></td>
<td><p>Active Directory</p>
<p>Repositório de Informações</p></td>
<td><p>OwaDeepTestMonitor</p></td>
</tr>
</tbody>
</table>


A sonda **OwaSelfTestProbe** envia uma única solicitação HTTP para o seguinte endereço: https://localhost:444/owa/exhealth.check. A sonda confirma que o pool de aplicativos está respondendo, retornando uma **200 OK** código de status. Essa sonda não tem nenhuma dependência de qualquer outro componente Exchange.

A sonda **OwaDeepTestProbe** é executada em cada banco de dados de caixa de correio usando cópias no servidor atual. A sonda determina que um logon completo pode ser feito em relação a esse servidor. Para fazer isso, ele simula o tipo de tráfego que é gerado por um servidor de acesso para cliente (CAS) contra um servidor específico. A sonda depende Active Directory serviços de domínio (AD DS) para autenticação e no repositório de caixa de correio para acesso de caixa de correio. Para obter mais informações sobre sondas e monitores, consulte [Desempenho e a integridade do servidor](https://technet.microsoft.com/pt-br/library/jj150551\(v=exchg.150\)).

## Problemas comuns

Essa sonda pode falhar por uma das seguintes razões:

  - O pool de aplicativos do OWA que é hospedado no CAS monitorado não responde ou o pool de aplicativos que está hospedado no servidor de caixa de correio não está respondendo.

  - O servidor de caixa de correio ou a autoridade de certificação está tendo problemas de rede e não puder se conectar ao outro servidor ou para um controlador de domínio.

  - As credenciais de conta de monitoramento não estão corretas.

  - Banco de dados do usuário não está montado ou o armazenamento de informações está inacessível para essa caixa de correio.

  - O armazenamento de informações não está respondendo.

  - Os controladores de domínio não estão respondendo.

## Ação do usuário

É possível que o serviço tenha se recuperado após a emissão do alerta. Portanto, quando você receber um alerta que especifica que o conjunto de integridade não está íntegro, primeiro verifique se o problema ainda existe. Se o problema existir, execute as ações de recuperação apropriadas descritas nas seções seguintes.

## Verificar se o problema ainda existe

1.  Identifique o nome do conjunto de integridade e o nome do servidor no alerta.

2.  Os detalhes da mensagem fornecem informações sobre a causa exata do alerta. Na maioria dos casos, os detalhes da mensagem fornecem informações sobre solução de problemas suficientes para identificar a causa raiz. Se os detalhes da mensagem não forem claros, faça o seguinte:
    
    1.  Abra o Shell de Gerenciamento do Exchange, e em seguida, execute o seguinte comando para recuperar os detalhes do conjunto de integridade que emitiu o alerta:
        
            Get-ServerHealth <server name> | ?{$_.HealthSetName -eq "<health set name>"}
        
        Por exemplo, para recuperar o OWA. O conjunto de integridade de protocolo detalhes sobre Server1. contoso.com, execute o seguinte comando:
        
            Get-ServerHealth server1.contoso.com | ?{$_.HealthSetName -eq "OWA.Protocol"}
    
    2.  Analise a saída para determinar o monitor que tenha reportado o erro do comando. O **AlertValue** para o monitor que emitiu o alerta será `Unhealthy`.
    
    3.  Execute novamente a sonda associada do monitor que está em estado não íntegro. Consulte a tabela na seção Explanation para localizar a sondagem associada. Para fazer isso, execute o seguinte comando:
        
            Invoke-MonitoringProbe <health set name>\<probe name> -Server <server name> | Format-List
        
        Por exemplo, suponha que o monitor está falhando foi **OwaSelfTestMonitor**. A sonda associada a esse monitor é **OwaSelfTestProbe**. Para executar essa sonda em Server1, execute o seguinte comando:
        
            Invoke-MonitoringProbe OWA.Protocol\OwaSelfTestProbe -Server server1.contoso.com | Format-List
    
    4.  Na saída do comando, verifique o valor **Resultado** da sonda. Se o valor for **Êxito**, significa que o problema foi um erro transitório e não existe mais. Caso contrário, consulte as etapas de recuperação descritas nas seções seguintes.

Quando você recebe um alerta de um conjunto de integridade, a mensagem de email contém as seguintes informações:

  - Nome do servidor que enviou o alerta

  - Tipo de sonda que falharam (autoteste ou DeepTest)

  - Hora e data em que o alerta ocorreu

  - Caminho para a pasta na qual você pode encontrar os rastreamentos de solicitação HTTP completos para a investigação
    
      
    Por padrão, os arquivos de rastreamento estão localizados nas seguintes pastas:
    
      - SelfTestProbe: \<*ExchangeServer*\>\\Logging\\Monitoring\\OWA\\ProtocolProbe
    
      - DeepTestProbe: \<*ExchangeServer*\>\\Logging\\Monitoring\\OWA\\MailboxProbe

  - Rastreamento de exceções completo do último erro, incluindo dados de diagnóstico e informações de cabeçalho HTTP específicas  
    
    **Observação**   Você pode usar as informações no rastreamento de exceções completo para ajudar a solucionar o problema. A exceção gerada pela sonda conter um motivo da falha que descreve por que o teste falhou. O motivo da falha pode ser qualquer um dos seguintes procedimentos:
    
      - **MissingKeyword**   Uma palavra-chave esperada não foi encontrada na resposta do servidor. Nesse caso, a exceção contém as palavras-chave esperadas.
    
      - **NameResolution**   A resolução DNS está falhando resolver o nome de um determinado servidor.
    
      - **NetworkConnection**   O teste está recebendo uma falha de conexão de rede quando ele tenta se conectar ao pool de aplicativos em CAFETERIAS OWA.
    
      - **UnexpectedHttpResponseCode**   A resposta continha um código HTTP inesperado. Por exemplo, o servidor retornou um código de **503** HTTP.
    
      - **RequestTimeout**   O servidor demorou muito para responder a uma solicitação de cliente.
    
      - **UnexpectedHttpResponseCode**   A resposta retornou um código HTTP inesperado. Por exemplo, o servidor retornou um código de **503** HTTP.
    
      - **ScenarioTimeout**   A sonda foi concluída com êxito, mas demorou mais de um minuto para fazê-lo. Isso geralmente indica um sistema que está sendo sobrecarregado.
    
      - **OwaErrorPage**   OWA retornados de uma página de erro. O nome do erro que causou a falha é normalmente disponível na mensagem de exceção.
    
      - **OwaMailboxErrorPage**   OWA retornados de uma página de erro que contém um erro de repositório de caixa de correio. Isso geralmente indica problemas, como o repositório de caixa de correio que está sendo pressionada ou caixas de correio que estão sendo desmontadas.
    
    O rastreamento de exceção contém um campo importante chamado **FailingComponent**, no qual a sonda torna um esforço para tentar determinar e categorizar a falha. Por exemplo, a sonda pode retornar qualquer um dos seguintes valores:
    
      - **Caixa de correio**   A sonda poderá encontrá-OWA, mas não puder se conectar ao repositório de caixa de correio. Nesse caso, o teste falhou ou a latência de acesso de caixa de correio causou a sonda falhar e gerar um erro de **ScenarioTimeout** . Quando esses tipos de falhas ocorrem, você deve verificar a integridade dos servidores de caixa de correio.
    
      - **Do Active Directory**   A sonda poderá encontrá-OWA, mas não puder se conectar ao AD DS. Nesse caso, o teste falhou ou as latências de chamada do AD DS podem causar a sonda atinja o tempo limite. Quando esses tipos de falhas ocorrem, você deve verificar a integridade dos controladores de domínio e também verificar as conexões de rede entre os servidores de CA e de caixa de correio e os controladores de domínio.
    
      - **OWA**   Normalmente, isso significa que ocorreu um erro dentro da camada do OWA. Quando esses tipos de falhas ocorrem, você deve verificar a integridade do processo de OWA no servidor de caixa de correio e de CA e também verificar as conexões de rede.
    
    A exceção também contém as informações mais recentes HTTP solicitação e a resposta que foi recebidas antes que o teste falhou.  
      
    o corpo de escalonamento contém o caminho para os logs de sonda que pode ser usado para verificar o completo web solicitações e respostas HTTP que foram enviadas quando o teste falhou. Esse arquivo contém dados apenas sondas com falha porque apenas tentativas fracassadas estão conectadas. Você pode usar essas informações para obter uma visão mais completa de por que o teste fracassou.

## Ações de recuperação de OwaSelfTestProbe

Como essa sonda tem dependências pouquíssimas, normalmente ocorrem falhas quando o processo do pool de aplicativo OWA não está respondendo.

Para resolver esse problema, siga estas etapas:

1.  Clique na URL de log de rastreamento de sonda no corpo da mensagem de email de alerta para verificar se estão ocorrendo falhas de novas.

2.  Crie uma conta de usuário de teste no mesmo servidor em que a caixa de correio está montada. Tente fazer logon para determinar se o problema pode ser reproduzido.

3.  Verifique se há alertas no conjunto de integridade do OWA que pode indicar um problema que afeta um servidor de caixa de correio específico. Para obter mais informações, consulte [Solução de problemas conjunto de integridade do OWA](troubleshooting-owa-health-set.md).

4.  Inicie o Gerenciador do IIS e conecte-se ao servidor que está relatando o problema para determinar se o pool de aplicativos **MSExchangeOwaAppPool** está sendo executado no CAS.

5.  No Gerenciador do IIS, verifique se que o site padrão está sendo executado.

6.  No Gerenciador do IIS, clique em **Pools de aplicativos** e recicle o pool de aplicativos **MSExchangeOWAAppPool** executando o comando a seguir a partir do Shell de Gerenciamento do Exchange:
    
        %SystemRoot%\System32\inetsrv\Appcmd recycle MSExchangeOWAAppPool

7.  Execute novamente a sonda associada conforme mostrado na etapa 2c na seção Verifying the issue still exists.

8.  Se o problema persistir, use o serviço do IIS com o utilitário IISReset ou executando o seguinte comando:
    
        Iisreset /noforce

9.  Execute novamente a sonda associada conforme mostrado na etapa 2c na seção Verifying the issue still exists.

10. Se o problema ainda existir, reinicie o servidor.

11. Depois que o servidor reiniciar, execute novamente a sondagem associada como mostrado na etapa 2c na seção Verifying the issue still exists.

12. Se a sonda continuar a falhar, talvez você precise de ajuda para resolver esse problema. Contate um profissional do Suporte Microsoft para resolver esse problema. Para entrar em contato com um profissional do Suporte Microsoft, visite o [Centro de Soluções do Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=180809). No painel de navegação, clique em **Recursos e opções de suporte** e use uma das opções listadas em **Obter suporte técnico** para entrar em contato com um profissional do Suporte Microsoft. Como a sua organização pode ter um procedimento específico para entrar em contato diretamente os Serviços de Suporte a Produtos Microsoft, tenha certeza de consultar primeiro as diretrizes da sua organização.

## Ações de recuperação de OwaDeepTestProbe

1.  Para determinar se o problema ainda existir, crie uma conta de usuário de teste no mesmo servidor em que a caixa de correio está montada e tente fazer logon no OWA. Por exemplo, tente fazer logon usando: https:// *\<servername\>*/owa.

2.  Verifique se há alertas no conjunto de integridade do OWA que pode indicar um problema que afeta um servidor de caixa de correio específico. Para obter mais informações, consulte [Solução de problemas conjunto de integridade do OWA](troubleshooting-owa-health-set.md).

3.  Inicie o Gerenciador do IIS e conecte-se ao servidor que está relatando o problema para determinar se o pool de aplicativos **MSExchangeOwaAppPool** está sendo executado no CAS.

4.  No Gerenciador do IIS, verifique se que o site padrão está sendo executado.

5.  Localize o banco de dados de caixa de correio para testes com falha e verificar que o banco de dados de caixa de correio está ativo no servidor de caixa de correio e que o repositório de caixa de correio está íntegro. Para localizar as informações de GUID de banco de dados com falha, abra as informações de rastreamento completo da exceção. Cada falha deve conter uma entrada semelhante ao seguinte:
    
    `Starting Owa probe with Target: https://localhost/owa/, Username:  HealthMailboxdf8b87828ab0427cb91e985bbdfcec62@yourdomain.com`

6.  Copie o GUID HealthMailbox e, em seguida, execute o seguinte comando no Shell:
    
        Get-Mailbox -Monitoring -Identity <username>
    
    Por exemplo, execute o seguinte comando:
    
        Get-Mailbox -Monitoring -Identity HealthMailboxdf8b87828ab0427cb91e985bbdfcec62@yourdomain.com
    
    No objeto retornado, você pode localizar o nome do banco de dados do usuário e você também pode determinar qual reside o banco de dados ativo no momento.

7.  No Gerenciador do IIS, clique em **Pools de aplicativos** e recicle o pool de aplicativos **MSExchangeOWAAppPool** executando o seguinte comando no Shell:
    
        %SystemRoot%\System32\inetsrv\Appcmd recycle MSExchangeOWAAppPool

8.  Execute novamente a sonda associada conforme mostrado na etapa 2c na seção Verifying the issue still exists.

9.  Se o problema persistir, use o serviço do IIS com o utilitário IISReset ou executando o seguinte comando:
    
        Iisreset /noforce

10. Execute novamente a sonda associada conforme mostrado na etapa 2c na seção Verifying the issue still exists.

11. Se o problema ainda existir, reinicie o servidor.

12. Depois que o servidor reiniciar, execute novamente a sondagem associada como mostrado na etapa 2c na seção Verifying the issue still exists.

13. Se a sonda continuar a falhar, talvez você precise de ajuda para resolver esse problema. Contate um profissional do Suporte Microsoft para resolver esse problema. Para entrar em contato com um profissional do Suporte Microsoft, visite o [Centro de Soluções do Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=180809). No painel de navegação, clique em **Recursos e opções de suporte** e use uma das opções listadas em **Obter suporte técnico** para entrar em contato com um profissional do Suporte Microsoft. Como a sua organização pode ter um procedimento específico para entrar em contato diretamente os Serviços de Suporte a Produtos Microsoft, tenha certeza de consultar primeiro as diretrizes da sua organização.

## Para obter mais informações

[Novidades do Exchange 2013](https://technet.microsoft.com/pt-br/library/jj150540\(v=exchg.150\))

[Cmdlets do Exchange 2013](https://technet.microsoft.com/pt-br/library/bb124413\(v=exchg.150\))

