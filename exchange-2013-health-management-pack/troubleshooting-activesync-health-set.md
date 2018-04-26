---
title: Solucionando problemas de integridade do ActiveSync definido
TOCTitle: Solucionando problemas de integridade do ActiveSync definido
ms:assetid: 8a0b8b26-b4ef-41b8-8f71-8271c1735a69
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/ms.exch.scom.activesync(v=EXCHG.150)
ms:contentKeyID: 53275623
ms.date: 03/07/2017
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Solucionando problemas de integridade do ActiveSync definido

 

_**Aplica-se a:**Exchange Server 2013_

_**Tópico modificado em:**2015-03-09_

O conjunto de integridade Exchange ActiveSync monitora a integridade geral do serviço ActiveSync para clientes móveis em sua organização. O conjunto de integridade ActiveSync está relacionado aos seguintes conjuntos de integridade:

[Solução de problemas de conjunto de integridade de ActiveSync.Protocol](troubleshooting-activesync-protocol-health-set.md)

[Solução de problemas de conjunto de integridade de ActiveSync.Proxy](troubleshooting-activesync-proxy-health-set.md)

Se você receber um alerta que indica que o conjunto de integridade ActiveSync não está íntegro, isso indica um problema que pode impedir que os usuários acessem suas caixas de correio usando ActiveSync.

## Explicação

O serviço ActiveSync é monitorado usando as seguintes sondas e monitores.


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
<td><p>ActiveSyncCTPProbe</p></td>
<td><p>ActiveSync</p></td>
<td><p>Active Directory</p>
<p>Autenticação</p>
<p>Autenticação de servidor de Caixa de Correio</p>
<p>Repositório de Informações</p>
<p>Alta Disponibilidade</p>
<p>Rede</p></td>
<td><p>ActiveSyncCTPMonitor (conjunto de integridade do ActiveSync)</p></td>
</tr>
<tr class="even">
<td><p>ActiveSyncProxyTestProbe</p></td>
<td><p>ActiveSync.Proxy</p></td>
<td><p>-</p></td>
<td><p>ActiveSyncProxyTestMonitor (ActiveSync.Proxy conjunto de integridade)</p></td>
</tr>
<tr class="odd">
<td><p>ActiveSyncDeepTestProbe</p></td>
<td><p>ActiveSync.Protocol</p></td>
<td><p>Active Directory</p>
<p>Autenticação</p>
<p>Repositório de Informações</p>
<p>Alta Disponibilidade</p></td>
<td><p>ActiveSyncDeepTestMonitor (conjunto de integridade do ActiveSync)</p></td>
</tr>
<tr class="even">
<td><p>ActiveSyncSelfTestProbe</p></td>
<td><p>ActiveSync.Protocol</p></td>
<td><p>Active Directory</p>
<p>Autenticação</p></td>
<td><p>ActiveSyncSelfTestMonitor (ActiveSync.Protocol conjunto de integridade)</p>
<p>RequestsQueuedGt500Monitor (conjunto de integridade do ActiveSync)</p></td>
</tr>
</tbody>
</table>


Para obter mais informações sobre sondas e monitores, consulte [Desempenho e a integridade do servidor](https://technet.microsoft.com/pt-br/library/jj150551\(v=exchg.150\)).

## Ação do usuário

É possível que o serviço recuperado depois que ele emitiu o alerta. Portanto, quando você recebe um alerta que especifica o conjunto de integridade ActiveSync não está íntegro, primeiro verificar se o problema ainda existe. Se o problema existir, execute as ações de recuperação apropriadas descritas nas seções a seguir.

## Verificar se o problema

1.  Identifique o nome do conjunto de integridade e o nome do servidor que são fornecidas no alerta.

2.  Os detalhes da mensagem fornecem informações sobre a causa exata do alerta. Na maioria dos casos, os detalhes da mensagem fornecem informações de solução de problemas suficientes para ajudar a identificar a causa raiz. Se os detalhes da mensagem não criptografados, faça o seguinte:
    
    1.  Abra o Shell de Gerenciamento do Exchange e execute o seguinte comando para recuperar os detalhes do conjunto de integridade que emitiu o alerta:
        
            Get-ServerHealth <server name> | ?{$_.HealthSetName -eq "<health set name>"}
        
        Por exemplo, para recuperar o ActiveSync integridade definir detalhes sobre Server1. contoso.com, execute o seguinte comando:
        
            Get-ServerHealth server1.contoso.com | ?{$_.HealthSetName -eq "ActiveSync"}
    
    2.  Analise a saída para determinar o monitor que tenha reportado o erro do comando. O valor de **AlertValue** para o monitor que emitiu o alerta será **não íntegra**.
    
    3.  Execute novamente a sonda associada do monitor que está em estado não íntegro. Consulte a tabela na seção Explanation para localizar a sondagem associada. Para fazer isso, execute o seguinte comando:
        
            Invoke-MonitoringProbe <health set name>\<probe name> -Server <server name> | Format-List
        
        Por exemplo, suponha que o monitor de falha é **ActiveSyncCTPMonitor**. A sonda associada a esse monitor é **ActiveSyncCTPProbe**. Para executar esse teste em Server1, execute o seguinte comando:
        
            Invoke-MonitoringProbe ActiveSync\ActiveSyncCTPProbe -Server server1.contoso.com | Format-List
    
    4.  Na saída do comando, examine a seção de "Resultados" da sonda. Se o valor for **teve êxito**, o problema foi um erro transitório, e ele não existe mais. Caso contrário, consulte as etapas de recuperação descritas nas seções a seguir.

## Ações de recuperação de ActiveSyncSelfTestMonitor e ActiveSyncDeepTestMonitor

Esse alerta monitor geralmente é emitida nos servidores de caixa de correio. Para executar as ações de recuperação, siga estas etapas:

1.  Inicie o Gerenciador do IIS e conecte-se ao servidor que está relatando o problema. Clique em **Pools de aplicativos** e recicle o pool de aplicativos do ActiveSync que nomeado **MSExchangeSyncAppPool**.

2.  Execute novamente a sonda associada conforme mostrado na etapa 2C na seção de Verificar se o problema .

3.  Se o problema ainda existir, recicle todo o serviço do IIS usando o utilitário IISReset.

4.  Execute novamente a sonda associada conforme mostrado na etapa 2C na seção de Verificar se o problema .

5.  Se o problema ainda existir, reinicie o servidor. Para fazer isso, o failover primeiro os bancos de dados hospedados no servidor usando o seguinte comando:
    
        Set-MailboxServer server1.contoso.com -DatabaseCopyActivationDisabledAndMoveNow $true
    
    Neste e em todos os exemplos de código subsequentes, substitua *server1.contoso.com* pelo nome real do servidor.

6.  Em seguida, verifique se todos os bancos de dados foram movidos desativa o servidor que está relatando o problema. Para fazer isso, execute o seguinte comando:
    
        Get-MailboxDatabaseCopyStatus -Server server1.contoso.com | Group Status

7.  Se a saída do comando na etapa 6 não mostrar nenhuma cópia ativa no servidor, reinicie o servidor. Se a saída mostrar cópias ativas, execute as etapas 5 e 6 novamente.

8.  Depois que o servidor for reiniciado, execute novamente a sonda associada conforme mostrado na etapa 2C na seção de Verificar se o problema .

9.  Se a investigação for bem sucedida, faça failover dos bancos de dados executando o seguinte comando:
    
        Set-MailboxServer server1.contoso.com -DatabaseCopyActivationDisabledAndMoveNow $false

10. Se a sonda ainda falhar, pode precisar de mais ajuda para resolver esse problema. Contate um profissional do Suporte Microsoft para resolver esse problema. Para entrar em contato com um profissional do Suporte Microsoft, visite o [Centro de Soluções do Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=180809). No painel de navegação, clique em **Recursos e opções de suporte** e use uma das opções listadas em **Obter suporte técnico** para entrar em contato com um profissional do Suporte Microsoft. Como a sua organização pode ter um procedimento específico para entrar em contato diretamente os Serviços de Suporte a Produtos Microsoft, tenha certeza de consultar primeiro as diretrizes da sua organização.

## Ações de recuperação de ActiveSyncCTPMonitor

Esse alerta do monitor normalmente é emitido em servidores de autoridade de certificação (CAS).

1.  Inicie o Gerenciador do IIS e conecte-se ao servidor que está relatando o problema. Clique em **Pools de aplicativos** e recicle o pool de aplicativos ActiveSync nomeado **MSExchangeSyncAppPool**.

2.  Execute novamente a sonda associada conforme mostrado na etapa 2C na seção de Verificar se o problema .

3.  Se o problema ainda existir, recicle todo o serviço do IIS usando o utilitário IISReset.

4.  Execute novamente a sonda associada conforme mostrado na etapa 2C na seção de Verificar se o problema .

5.  Se o problema persistir, você deve verificar o status de integridade no servidor de caixa de correio correspondente. O nome do servidor de caixa de correio é o valor de `_Mbx:` que é fornecido na mensagem de erro.
    
    1.  Execute o seguinte comando para o servidor de caixa de correio apropriado. Por exemplo, execute o comando a seguir um servidor de caixa de correio chamado mailbox1.contoso.com:
        
            Get-ServerHealth mailbox1.contoso.com | ?{$_.HealtSetName -like "ActiveSync*"}
    
    2.  Se qualquer um dos monitores que estão listados na saída do comando é relatado estar íntegro, você deve lidar com esses monitores pela primeira vez. Para fazer isso, siga as etapas de solução de problemas que são descritas na seção ActiveSyncDeepTestMonitor e ActiveSyncSelfTestMonitor ações de recuperação .

6.  Se todos os monitores no servidor de caixa de correio íntegras, reinicie o CAS.

7.  Depois que o servidor for reiniciado, execute novamente a sonda associada conforme mostrado na etapa 2C na seção de Verificar se o problema .

8.  Se a sonda continua a falhar, pode precisar de mais ajuda para resolver esse problema. Contate um profissional do Suporte Microsoft para resolver esse problema. Para entrar em contato com um profissional do Suporte Microsoft, visite o [Centro de Soluções do Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=180809). No painel de navegação, clique em **Recursos e opções de suporte** e use uma das opções listadas em **Obter suporte técnico** para entrar em contato com um profissional do Suporte Microsoft. Como a sua organização pode ter um procedimento específico para entrar em contato diretamente os Serviços de Suporte a Produtos Microsoft, tenha certeza de consultar primeiro as diretrizes da sua organização.

## Ações de recuperação RequestsQueuedGt500Monitor

Esse alerta monitor geralmente é emitida nos servidores de CA.

1.  Inicie o Gerenciador do IIS e conecte-se ao servidor que está relatando o problema. Clique em **Pools de aplicativos** e recicle o pool de aplicativos ActiveSync nomeado **MSExchangeSyncAppPool**.

2.  Aguarde 10 minutos para ver se o monitor permaneça íntegro. Após 10 minutos, execute o seguinte comando para o servidor apropriado. Por exemplo, execute o seguinte comando para Server1:
    
        Get-ServerHealth server1.contoso.com | ?{$_.HealthSetName -like "ActiveSync*"}

3.  Se o problema persistir, recicle todo o serviço do IIS usando o utilitário IISReset.

4.  Aguarde 10 minutos e execute o comando mostrado na etapa 2 novamente para ver se o monitor permaneça íntegro.

5.  Se o problema persistir, reinicie o servidor. Se o servidor for um CAS, basta reinicie o servidor. Se o servidor for um servidor de caixa de correio, faça o seguinte:
    
    1.  Faça o failover dos bancos de dados que estão hospedados no servidor. Para fazer isso, execute o seguinte comando:
        
            Set-MailboxServer server1.contoso.com -DatabaseCopyActivationDisabledAndMoveNow $true
        
        **Observação**   Neste exemplo de código e em todos os exemplos subsequentes, substitua *server1.contoso.com* pelo nome real do servidor.
    
    2.  Verifique se todos os bancos de dados foram removidos do servidor que está relatando o problema. Para fazer isso, execute o seguinte comando:
        
            Get-MailboxDatabaseCopyStatus -Server server1.contoso.com | Group Status
        
        Se a saída do comando não mostrar nenhuma cópia ativa no servidor, reinicie o servidor.

6.  Depois que o servidor for reiniciado, aguarde 10 minutos e execute o comando mostrado na etapa 2 novamente para determinar se o monitor permaneça íntegro.

7.  Se o monitor permanecer íntegro e se esse for um servidor de caixa de correio, o failover dos bancos de dados, executando o seguinte comando:
    
        Set-MailboxServer server1.contoso.com -DatabaseCopyActivationDisabledAndMoveNow $false

8.  Se a sonda continua a falhar, pode precisar de mais ajuda para resolver esse problema. Contate um profissional do Suporte Microsoft para resolver esse problema. Para entrar em contato com um profissional do Suporte Microsoft, visite o [Centro de Soluções do Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=180809). No painel de navegação, clique em **Recursos e opções de suporte** e use uma das opções listadas em **Obter suporte técnico** para entrar em contato com um profissional do Suporte Microsoft. Como a sua organização pode ter um procedimento específico para entrar em contato diretamente os Serviços de Suporte a Produtos Microsoft, tenha certeza de consultar primeiro as diretrizes da sua organização.

## Para Obter Mais Informações

[Exchange ActiveSync](https://technet.microsoft.com/pt-br/library/aa998357\(v=exchg.150\))

[Dispositivos móveis](https://technet.microsoft.com/pt-br/library/bb232129\(v=exchg.150\))

[Tarefas de gerenciamento de diretório virtual do Exchange ActiveSync](https://technet.microsoft.com/pt-br/library/bb125170\(v=exchg.150\))

