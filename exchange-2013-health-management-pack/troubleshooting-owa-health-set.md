---
title: Solução de problemas conjunto de integridade do OWA
TOCTitle: Solução de problemas conjunto de integridade do OWA
ms:assetid: eae9dbd7-2ce6-43ce-b9a1-b114fd0c3ab4
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/ms.exch.scom.owa(v=EXCHG.150)
ms:contentKeyID: 53275635
ms.date: 03/07/2017
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Solução de problemas conjunto de integridade do OWA

 

_**Aplica-se a:**Exchange Server 2013_

_**Tópico modificado em:**2015-03-09_

O conjunto de integridade Outlook Web App (OWA) monitora a integridade geral do serviço Outlook Web App.

Se você receber um alerta que especifica que não está íntegro, que isso indica um problema que pode impedir que os usuários acessem suas caixas de correio usando Outlook Web AppOutlook Web App.

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
<td><p>OwaCtpProbe</p></td>
<td><p>Outlook Web App</p></td>
<td><p>Active Directory</p>
<p>Repositório de Informações</p></td>
<td><p>OwaCtpMonitor</p></td>
</tr>
</tbody>
</table>


Para obter mais informações sobre sondas e monitores, consulte [Desempenho e a integridade do servidor](https://technet.microsoft.com/pt-br/library/jj150551\(v=exchg.150\)).

## Problemas comuns

Essa sonda pode falhar por vários motivos. Estes são alguns dos motivos mais comuns:

  - O pool de aplicativos Outlook Web App que está hospedado no servidor de acesso para cliente monitorado (CAS) não está respondendo ou o pool de aplicativos que está hospedado no servidor de caixa de correio não está respondendo.

  - O CAS está com problemas de rede e não puder se conectar ao servidor caixa de correio ou o controlador de domínio.

  - As credenciais de conta de monitoramento não estão corretas.

  - Banco de dados do usuário não está montado ou o armazenamento de informações está inacessível para essa caixa de correio.

  - O armazenamento de informações não está respondendo.

  - Os controladores de domínio não estão respondendo.

## Ação do usuário

É possível que o serviço tenha se recuperado após a emissão do alerta. Portanto, quando você receber um alerta que especifica que o conjunto de integridade não está íntegro, primeiro verifique se o problema ainda existe. Se o problema existir, execute as ações de recuperação apropriadas descritas nas seções seguintes.

## Verificar se o problema ainda existe

1.  Identifique o nome do conjunto de integridade e o nome do servidor no alerta.

2.  Os detalhes da mensagem fornecem informações sobre a causa exata do alerta. Na maioria dos casos, os detalhes da mensagem fornecem informações sobre solução de problemas suficientes para identificar a causa raiz. Se os detalhes da mensagem não forem claros, faça o seguinte:
    
    1.  Abra Shell de Gerenciamento do Exchange e, em seguida, execute o seguinte comando para recuperar os detalhes do conjunto de integridade que gerou o alerta:
        
            Get-ServerHealth <server name> | ?{$_.HealthSetName -eq "<health set name>"}
        
        o conjunto de integridade de Outlook Web App detalhes sobre Server1. contoso.com, execute o seguinte comando:
        
            Get-ServerHealth server1.contoso.com | ?{$_.HealthSetName -eq "OWA"}
    
    2.  Analise a saída para determinar o monitor que tenha reportado o erro do comando. O valor de **AlertValue** para o monitor que emitiu o alerta é `Unhealthy`.
    
    3.  Execute novamente a sonda associada do monitor que está em estado não íntegro. Consulte a tabela na seção Explanation para localizar a sondagem associada. Para fazer isso, execute o seguinte comando:
        
            Invoke-MonitoringProbe <health set name>\<probe name> -Server <server name> | Format-List
        
        Por exemplo, para criar um Exchange ActiveSync monitoring sonda em *server1.contoso.com*, execute o seguinte comando:
        
            Invoke-MonitoringProbe -Identity ActiveSync.Protocol\ActiveSyncSelfTestProbe -Server server1.contoso.com
    
    4.  Na saída do comando, verifique o valor **Resultado** da sonda. Se o valor for **Êxito**, significa que o problema foi um erro transitório e não existe mais. Caso contrário, consulte as etapas de recuperação descritas nas seções seguintes.

## Ações de recuperação de OwaCtpMonitor

Um alerta de email a partir de um conjunto de integridade contém as seguintes informações:

  - Nome do servidor que enviou o alerta

  - Rastreamento de exceções completo do último erro, incluindo dados de diagnóstico e informações de cabeçalho HTTP específicas  
    
    **Observação**   Você pode usar as informações no rastreamento de exceções completo para ajudar a solucionar o problema. A exceção gerada pela sonda contém um motivo da falha que descreve por que o teste falhou. Por exemplo, a exceção contém o seguinte:
    
      - **MissingKeyword**   Uma palavra-chave esperada não foi encontrada na resposta do servidor. Nesse caso, a exceção contém as palavras-chave esperadas.
    
      - **NameResolution**   Resolução DNS está falhando resolver o nome de um determinado servidor.
    
      - **NetworkConnection**   O teste está recebendo uma falha de conexão de rede quando ele tenta se conectar ao pool de aplicativo OWA em CAFETERIAS.
    
      - **UnexpectedHttpResponseCode**   Resposta tinha um código HTTP inesperado. Por exemplo, o servidor retornou um código de **503** HTTP.
    
      - **RequestTimeout**   O servidor demorou muito para responder a uma solicitação de cliente.
    
      - **ScenarioTimeout**   A sonda foi concluída com êxito, mas demorou mais de um minuto para fazer isso. Isso geralmente indica um sistema que está sendo sobrecarregado.
    
      - **OwaErrorPage** Outlook Web App retornados de uma página de erro. O nome do erro que causou a falha é geralmente disponível na mensagem de exceção.   
    
      - **OwaMailboxErrorPage** Outlook Web App retornados de uma página de erro que contém um erro de repositório de caixa de correio. Normalmente, isso indica que o repositório de caixa de correio está inoperante ou que caixas de correio estão sendo desmontadas.   
    
    O rastreamento de exceção contém um campo importante chamado **FailingComponent**. A sonda tenta determinar a falha, como no exemplo a seguir:
    
      - **Caixa de correio**   A sonda pode alcançar Outlook Web App, mas não puder se conectar ao repositório de caixa de correio. Nesse caso, o teste falhou ou a latência de acesso de caixa de correio causou a sonda falhar e gerar um erro de **ScenarioTimeout** . Quando esses tipos de falhas ocorrem, você deve verificar a integridade dos servidores de caixa de correio.
    
      - **Active Directory**    A sonda pode alcançar Outlook Web App, mas não puder se conectar ao Active Directory. Nesse caso, o teste falhou ou as latências de chamada Active Directory podem ter causado o tempo limite da sonda. Quando esses tipos de falhas ocorrem, você deve verificar a integridade dos controladores de domínio e também verificar as conexões de rede entre os servidores de CA e de caixa de correio e controladores de domínio.
    
      - **OWA**   Normalmente, isso significa que ocorreu um erro dentro da camada de Outlook Web App. Quando esses tipos de falhas ocorrem, você deve verificar a integridade do processo de Outlook Web App nos servidores de CA e de caixa de correio e também verificar as conexões de rede.
    
    A exceção também contém as informações mais recentes HTTP solicitação e a resposta que foi recebidas antes que o teste falhou. O corpo de escalonamento contém o caminho para investigue logs. Você pode usar essas informações para determinar o completo web solicitações e respostas HTTP que foram enviadas quando o teste falhou. Esse arquivo contém dados apenas sondas com falha porque apenas tentativas fracassadas estão conectadas. Você pode usar essas informações para obter uma visão mais completa de por que o teste fracassou.

  - Como baixo na métrica de disponibilidade capitular (x %).

  - O caminho completo para a pasta que contém os rastreamentos de solicitação HTTP completos para o teste. Por padrão, essa informação está localizada na pasta \\Logging\\Monitoring\\OWA\\ClientAccessProbe *\<ExchangeServer\>*.

  - A hora e data quando o alerta ocorreu.

Para resolver esse problema, siga estas etapas:

1.  Crie uma conta de usuário de teste e, em seguida, faça logon no CAS usando a conta de usuário de teste. Por exemplo, faça logon usando https:// *\<servername\>*/owa.
    
    Se isso falhar, o teste usando um servidor diferente da autoridade de certificação para verificar se o problema está ocorrendo em um CAS específico e não no servidor caixa de correio.

2.  Verifique a conectividade de rede entre os servidores de CA e de caixa de correio. Use o ping.exe para verificar se cada servidor está respondendo.

3.  Verifique se há alertas no OWA. Conjunto de integridade de protocolo que pode indicar um problema que afeta um servidor de caixa de correio específico. Para obter mais informações, consulte [Solucionando problemas de OWA. Conjunto de integridade de protocolo](troubleshooting-owa-protocol-health-set.md).

4.  Inicie o Gerenciador do IIS e conecte-se ao servidor que está relatando o problema para verificar se o pool de aplicativos MSExchangeOwaAppPool está sendo executado no CAS.

5.  No Gerenciador do IIS, verifique se que o site padrão está sendo executado.

6.  Localize o banco de dados de caixa de correio para testes com falha e verificar se o banco de dados de caixa de correio é ativo em um servidor de caixa de correio e que o repositório de caixa de correio está íntegro. Para localizar as informações de GUID de banco de dados com falha, abra as informações de rastreamento completo da exceção. Cada falha deve conter uma entrada que se parece com o exemplo a seguir:
    
    Iniciando o Owa sonda com destino: https://localhost/owa/, Username: *HealthMailboxdf8b87828ab0427cb91e985bbdfcec62@yourdomain.com*

7.  Copie o GUID HealthMailbox e, em seguida, execute o seguinte comando no Shell:
    
        Get-Mailbox -Monitoring -Identity <username>
    
    Por exemplo, execute o seguinte comando:
    
        Get-Mailbox -Monitoring -Identity HealthMailboxdf8b87828ab0427cb91e985bbdfcec62@yourdomain.com
    
    No objeto retornado, você pode localizar o nome do banco de dados do usuário e você também pode determinar qual reside o banco de dados ativo no momento.

8.  Se você tiver configurado o redirecionamento entre sites, talvez você veja sondas falhando e gerar um erro de MissingKeyword. Isso ocorre porque, por padrão, sondas de autoridade de certificação são realizadas em contas para qualquer local e também porque a sonda não tenta testar um CAS em um site diferente quando ele usa o redirecionamento. Para resolver esse problema, certifique-se de que os servidores em cada site estão contidos em MonitoringGroups. Teste de servidores de CA em um determinado grupo monitoramento somente em conjunto com os servidores de caixa de correio no mesmo grupo.
    
    Para determinar os grupos de monitoramento para seus servidores, execute o seguinte comando:
    
        Get-ExchangeServer | ft MonitoringGroup
    
    Para modificar o grupo monitoramento em um servidor, use o parâmetro *MonitoringGroup* em conjunto com o cmdlet **Set-ExchangeServer** . Por exemplo, use o seguinte:
    
        Set-ExchangeServer -Identity "ServerName" -MonitoringGroup "Primary"

9.  No Gerenciador do IIS, clique em **Pools de aplicativos** e recicle o pool de aplicativos **MSExchangeOWAAppPool** executando o comando a seguir a partir do Shell de Gerenciamento do Exchange:
    
        %SystemRoot%\System32\inetsrv\Appcmd recycle MSExchangeOWAAppPool

10. Execute novamente a sonda associada, conforme mostrado na etapa 2C na seção Verifying o problema ainda existir .

11. Se o problema persistir, use o serviço do IIS com o utilitário IISReset ou executando o seguinte comando:
    
        Iisreset /noforce

12. Execute novamente a sonda associada, conforme mostrado na etapa 2C na seção Verifying o problema ainda existir .

13. Se o problema ainda existir, reinicie o servidor.

14. Depois que o servidor for reiniciado, execute novamente a sonda associada, conforme mostrado na etapa 2C na seção Verifying o problema ainda existir .

15. Se a sonda continua a falhar, você pode precisar de assistência para resolver esse problema. Contate um profissional do Suporte Microsoft para resolver esse problema. Para entrar em contato com um profissional do Suporte Microsoft, visite o [Centro de Soluções do Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=180809). No painel de navegação, clique em **Recursos e opções de suporte** e use uma das opções listadas em **Obter suporte técnico** para entrar em contato com um profissional do Suporte Microsoft. Como a sua organização pode ter um procedimento específico para entrar em contato diretamente os Serviços de Suporte a Produtos Microsoft, tenha certeza de consultar primeiro as diretrizes da sua organização.

## Para obter mais informações

[Novidades do Exchange 2013](https://technet.microsoft.com/pt-br/library/jj150540\(v=exchg.150\))

[Cmdlets do Exchange 2013](https://technet.microsoft.com/pt-br/library/bb124413\(v=exchg.150\))

