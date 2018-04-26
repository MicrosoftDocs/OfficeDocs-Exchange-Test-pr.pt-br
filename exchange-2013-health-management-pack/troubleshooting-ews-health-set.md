---
title: Solução de problemas do conjunto de integridade EWS
TOCTitle: Solução de problemas do conjunto de integridade EWS
ms:assetid: f5aaacdd-7f4a-4d63-8440-1c564e644dfc
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/ms.exch.scom.ews(v=EXCHG.150)
ms:contentKeyID: 53275633
ms.date: 03/07/2017
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Solução de problemas do conjunto de integridade EWS

 

_**Aplica-se a:**Exchange Server 2013, Project Server 2013_

_**Tópico modificado em:**2015-03-09_

O conjunto de integridade dos Serviços Web do Exchange (EWS) monitora a integridade geral do serviço do EWS. O conjunto de integridade do EWS está profundamente relacionado aos seguintes conjuntos de integridade:

[Solucionando problemas de EWS. Conjunto de integridade de protocolo](troubleshooting-ews-protocol-health-set.md)

[Solucionando problemas de EWS. Conjunto de integridade de proxy](troubleshooting-ews-proxy-health-set.md)

Se você receber um alerta que especifica que o EWS não está saudável, isso indica um problema que pode impedir que os usuários se comuniquem com o servidor do Exchange.

## Explicação

O EWS é monitorado usando as seguintes sondas e monitores.


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
<td><p>EwsCtpProbe</p></td>
<td><p>EWS</p></td>
<td><p>Repositório de Informações</p>
<p>Serviços de Domínio Active Directory (AD DS)</p></td>
<td><p>EwsCtpMonitor (conjunto de integridade do EWS)</p></td>
</tr>
<tr class="even">
<td><p>EwsSelfTestProbe</p></td>
<td><p>EWS.Protocol</p></td>
<td><p>Serviços de Domínio Active Directory (AD DS)</p></td>
<td><p>EWSSelfTestMonitor</p></td>
</tr>
<tr class="odd">
<td><p>EwsDeepTestProbe</p></td>
<td><p>EWS.Protocol</p></td>
<td><p>Repositório de Informações</p></td>
<td><p>EWSDeepTestMonitor</p></td>
</tr>
</tbody>
</table>


Esta sonda realiza um logon completo no EWS do servidor de Acesso para Cliente (CAS) em um servidor de Caixa de Correio usando uma conta de monitoramento. Esta sonda chama o método **GetFolder** no EWS. Para obter mais informações sobre sondas e monitores, consulte [Desempenho e a integridade do servidor](https://technet.microsoft.com/pt-br/library/jj150551\(v=exchg.150\)).

## Problemas comuns

Essa sonda pode falhar por um dos seguintes motivos:

  - Há uma falha de correspondência entre o mecanismo de autenticação usado pela sonda e o mecanismo de autenticação usado no diretório virtual do CAS.

  - O pool de aplicativos do EWS no CAS que está sendo monitorado não responde.

  - O CAS está com problemas de rede ao se conectar ao servidor de Caixa de Correio.

  - O CAS está com problemas na comunicação com os Controladores de Domínio.

  - Os controladores de domínio não estão respondendo.

  - O pool de aplicativos do EWS que reside em um ou mais servidores de Caixa de Correio não responde.

  - O banco de dados do usuário não está montado ou o Repositório de Informações está indisponível para uma caixa de correio específica.

  - O serviço do Repositório de Informações em um ou mais servidores de Caixa de Correio está com problemas.

## Ação do usuário

É possível que o serviço tenha se recuperado após a emissão do alerta. Portanto, quando você receber um alerta que especifica que o conjunto de integridade não está íntegro, primeiro verifique se o problema ainda existe. Se o problema existir, execute as ações de recuperação apropriadas descritas nas seções seguintes.

## Verificar se o problema ainda existe

1.  Identifique o nome do conjunto de integridade e o nome do servidor no alerta.
    
    Quando você recebe um alerta deste HealthSet, a mensagem de email contém as seguintes informações:
    
    1.  Nome do CAS de origem do alerta
    
    2.  Nome do servidor de Caixa de Correio que a sonda estava monitorando como recurso de destino
    
    3.  Rastreamento de exceções completo do último erro, incluindo dados de diagnóstico e informações de cabeçalho HTTP específicas
    
    4.  Hora em que o incidente ocorreu
    
    5.  Mecanismo de autenticação usado e informações de credenciais
    
    As informações do rastreamento da exceção fornecem as dicas mais importantes do motivo de falha da sonda. A mensagem de escalonamento também contém os seguintes cabeçalhos HTTP:
    
    1.  **X-FEServer**   Indica em qual CAS a sonda foi executada
    
    2.  **X-TargetBEServer**   Indica para qual servidor MBX a solicitação foi direcionada
    
    3.  **X-DiagInfo**   Indica o servidor MBX que recebeu a solicitação

2.  Os detalhes da mensagem fornecem informações sobre a causa exata do alerta. Na maioria dos casos, os detalhes da mensagem fornecem informações sobre solução de problemas suficientes para identificar a causa raiz. Se os detalhes da mensagem não forem claros, faça o seguinte:
    
    1.  Abra o Shell de Gerenciamento do Exchange, e em seguida, execute o seguinte comando para recuperar os detalhes do conjunto de integridade que emitiu o alerta:
        
            Get-ServerHealth <server name> | ?{$_.HealthSetName -eq "<health set name>"}
        
        Por exemplo, para recuperar os detalhes do conjunto de integridade do EWS sobre server1.contoso.com, execute o seguinte comando:
        
            Get-ServerHealth server1.contoso.com | ?{$_.HealthSetName -eq "EWS"}
    
    2.  Verifique a saída do comando para determinar qual monitor relatou o erro. O valor **AlertValue** do monitor que emitiu o alerta será `Unhealthy`.
    
    3.  Execute novamente a sonda associada ao monitor que está com estado não saudável. Consulte a tabela na seção Explanation para encontrar a sonda associada. Para fazer isso, execute o seguinte comando:
        
            Invoke-MonitoringProbe <health set name>\<probe name> -Server <server name> | Format-List
        
        Para o conjunto de integridade do EWS, suponha que o monitor em falha é **EWSCtpMonitor**. A sonda associada àquele monitor é **EWSCtpProbe**. Para executar essa sonda em server1.contoso.com, execute o seguinte comando:
        
            Invoke-MonitoringProbe EWS\EWSCtpProbe -Server server1.contoso.com | Format-List
    
    4.  Na saída do comando, verifique o valor **Resultado** da sonda. Se o valor for **Êxito**, significa que o problema foi um erro transitório e não existe mais. Caso contrário, consulte as etapas de recuperação descritas nas seções seguintes.

## Ações de recuperação de EwsCtpMonitor

1.  Inicie o Gerenciador do IIS e conecte-se ao servidor que está relatando o problema para determinar se o pool de aplicativos **MSExchangeServicesAppPool** está sendo executado nos servidores de CA e de Caixa de Correio.

2.  Localize as sondas em falha do MailboxDatabase. Depois, verifique se o banco de dados de Caixa de Correio está ativo no servidor de Caixa de Correio, e se o Repositório de Informações está saudável.

3.  Clique em **Pools de Aplicativos** e recicle o pool de aplicativos **MSExchangeServicesAppPool** executando o seguinte comando a partir do Shell:
    
        %SystemRoot%\System32\inetsrv\Appcmd recycle MSExchangeServicesAppPool

4.  Execute novamente a sonda associada conforme mostrado na etapa 2c na seção Verifying the issue still exists.

5.  Se o problema ainda existir, recicle todo o serviço do IIS usando o utilitário IISReset.

6.  Execute novamente a sonda associada conforme mostrado na etapa 2c na seção Verifying the issue still exists.

7.  Se o problema continuar, revise os arquivos de log do protocolo nos servidores de CA e de Caixa de Correio. Os logs de protocolo do CAS estão na pasta *\<diretório de instalação do servidor do Exchange\>\\Logging\\HttpProxy\\Ews*. No servidor de Caixa de Correio, os logs estão na pasta *\<diretório de instalação do servidor do Exchange\>\\Logging\\Ews*.

8.  Crie uma conta de usuário de teste e entre usando essa conta no CAS fornecido. Por exemplo, faça logon usando: https://\<nomeservidor\>/ews/exchange.asmx. Se o problema continuar, tente um CAS diferente para determinar se o problema está relacionado àquele CAS e não ao servidor de Caixa de Correio. Se o nome de usuário de teste for bem sucedido, um problema pode afetar o banco de dados ou servidor de Caixa de Correio específico em que a caixa de correio de monitoramento está localizada. Tente repetir esta etapa usando uma conta de teste do banco de dados de Caixa de Correio.

9.  Verifique a conexão de rede entre os servidores de CA e de Caixa de Correio.

10. Verifique qualquer alerta no Conjunto de Integridade EWS.Proxy que possa indicar um problema que afeta um CAS específico.

11. Verifique qualquer alerta no Conjunto de Integridade EWS.Protocol que possa indicar um problema que afeta um servidor de Caixa de Correio específico.

12. Se o problema ainda existir, reinicie o servidor. Para tanto, faça primeiro o failover dos bancos de dados que estão hospedados no servidor. Para fazer isso, execute o seguinte comando:
    
        Set-MailboxServer server1.contoso.com -DatabaseCopyActivationDisabledAndMoveNow $true
    
    **Observação**   Neste exemplo de código e em todos os exemplos subsequentes, substitua *server1.contoso.com* pelo nome real do servidor.

13. Verifique se todos os bancos de dados foram removidos do servidor que está relatando o problema. Para fazer isso, execute o seguinte comando:
    
        Get-MailboxDatabaseCopyStatus -Server server1.contoso.com | Group Status
    
    Se a saída do comando não mostrar nenhuma cópia ativa no servidor, reinicie o servidor.

14. Após a reinicialização do servidor, execute novamente a sonda associada conforme mostrado na etapa 2c da seção Verifying the issue still exists.

15. Se a sonda for bem sucedida, faça o failover dos bancos de dados de volta para o servidor de Caixa de Correio executando o seguinte comando:
    
        Set-MailboxServer server1.contoso.com -DatabaseCopyActivationDisabledAndMoveNow $false

16. Se a sonda continuar falhando, você pode precisar de ajuda para solucionar o problema. Contate um profissional do Suporte Microsoft para resolver esse problema. Para entrar em contato com um profissional do Suporte Microsoft, visite o [Centro de Soluções do Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=180809). No painel de navegação, clique em **Recursos e opções de suporte** e use uma das opções listadas em **Obter suporte técnico** para entrar em contato com um profissional do Suporte Microsoft. Como a sua organização pode ter um procedimento específico para entrar em contato diretamente os Serviços de Suporte a Produtos Microsoft, tenha certeza de consultar primeiro as diretrizes da sua organização.

## Para obter mais informações

[Cmdlets do Exchange 2013](https://technet.microsoft.com/pt-br/library/bb124413\(v=exchg.150\))

[Novidades do Exchange 2013](https://technet.microsoft.com/pt-br/library/jj150540\(v=exchg.150\))

