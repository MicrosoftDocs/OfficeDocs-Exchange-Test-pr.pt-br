---
title: Solução de problemas de conjunto de integridade de POP
TOCTitle: Solução de problemas de conjunto de integridade de POP
ms:assetid: 6114e9fe-d037-4cb9-a643-933eb5fabc45
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/ms.exch.scom.pop(v=EXCHG.150)
ms:contentKeyID: 53275610
ms.date: 03/07/2017
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Solução de problemas de conjunto de integridade de POP

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2015-03-09_

O conjunto de integridade POP monitora a integridade e a disponibilidade geral do serviço POP3 do Microsoft Exchange e a conectividade de cliente POP3. O conjunto de integridade POP está intimamente relacionado com os seguintes conjuntos de integridade:

  - [Troubleshooting POP. Conjunto de integridade de protocolo](troubleshooting-pop-protocol-health-set.md)

  - [Troubleshooting POP. Conjunto de integridade de proxy](troubleshooting-pop-proxy-health-set.md)

Se você receber um alerta que especifica que o serviço POP não é íntegro, isso indica um problema que pode impedir que os usuários acessem suas caixas de correio usando POP3 no ambiente do Exchange.

## Explicação

O serviço POP é monitorado usando as seguintes sondagens e monitores.


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
<td><p>PopCTPProbe</p></td>
<td><p>POP</p></td>
<td><p>Active Directory</p>
<p>Autenticação</p>
<p>Autenticação de servidor de Caixa de Correio</p>
<p>Repositório de Informações</p>
<p>Alta Disponibilidade</p>
<p>Rede</p></td>
<td><p>PopCTPMonitor (conjunto de integridade POP)</p></td>
</tr>
<tr class="even">
<td><p>PopProxyTestProbe</p></td>
<td><p>POP.Proxy</p></td>
<td><p>Nenhum</p></td>
<td><p>PopProxyTestMonitor (conjunto de integridade POP.Proxy)</p></td>
</tr>
<tr class="odd">
<td><p>PopDeepTestProbe</p></td>
<td><p>POP.Protocol</p></td>
<td><p>Active Directory</p>
<p>Autenticação</p>
<p>Repositório de Informações</p>
<p>Alta Disponibilidade</p></td>
<td><p>PopDeepTestMonitor (conjunto de integridade POP.Protocol)</p></td>
</tr>
<tr class="even">
<td><p>PopSelfTestProbe</p></td>
<td><p>POP.Protocol</p></td>
<td><p>Nenhum</p></td>
<td><p>PopSelfTestMonitor (conjunto de integridade POP.Protocol)</p>
<p>AverageCommandProcessingTimeGt60sMonitor (conjunto de integridade POP)</p></td>
</tr>
</tbody>
</table>


## Ação do usuário

É possível que o serviço tenha se recuperado após a emissão do alerta. Portanto, quando você receber um alerta que especifica que o conjunto de integridade não está íntegro, primeiro verifique se o problema ainda existe. Se o problema existir, execute as ações de recuperação apropriadas descritas nas seções seguintes.

## Verificar se o problema ainda existe

1.  Identifique o nome do conjunto de integridade e o nome do servidor no alerta.

2.  Os detalhes da mensagem fornecem informações sobre a causa exata do alerta. Na maioria dos casos, os detalhes da mensagem fornecem informações sobre solução de problemas suficientes para identificar a causa raiz. Se os detalhes da mensagem não forem claros, faça o seguinte:
    
    1.  Abra o Shell de Gerenciamento do Exchange, e em seguida, execute o seguinte comando para recuperar os detalhes do conjunto de integridade que emitiu o alerta:
        
            Get-ServerHealth <server name> | ?{$_.HealthSetName -eq "<health set name>"}
        
        Por exemplo, para recuperar detalhes do conjunto de integridade POP sobre server1.contoso.com, execute o seguinte comando:
        
            Get-ServerHealth server1.contoso.com | ?{$_.HealthSetName -eq "POP"}
    
    2.  Verifique a saída do comando para determinar qual monitor relatou o erro. O valor **AlertValue** do monitor que emitiu o alerta será `Unhealthy`.
    
    3.  Execute novamente a sonda associada do monitor que está em estado não íntegro. Consulte a tabela na seção Explanation para localizar a sondagem associada. Para fazer isso, execute o seguinte comando:
        
            Invoke-MonitoringProbe <health set name>\<probe name> -Server <server name> | Format-List
        
        Por exemplo, suponha que o monitor com falha é **PopCTPMonitor**. A sondagem associada a esse monitor é **PopCTPProbe**. Para executar essa sonda em server1.contoso.com, execute o seguinte comando:
        
            Invoke-MonitoringProbe POP\PopCTPProbe -Server server1.contoso.com | Format-List
    
    4.  Na saída do comando, verifique o valor **Resultado** da sonda. Se o valor for **Êxito**, significa que o problema foi um erro transitório e não existe mais. Caso contrário, consulte as etapas de recuperação descritas nas seções seguintes.

## Ações de recuperação de PopTestDeepMonitor e PopSelfTestMonitor

Esse alerta do monitor normalmente é emitido em servidores de caixa de correio.

1.  Reinicie o serviço de back-end do POP3. Para obter mais informações, consulte [Iniciar e interromper os serviços POP3](https://technet.microsoft.com/pt-br/library/aa997475\(v=exchg.150\)).

2.  Execute novamente a sonda associada conforme mostrado na etapa 2c na seção Verifying the issue still exists.

3.  Se a sondagem ainda falhar, realize failover nos bancos de dados hospedados no servidor de caixa de correio usando o seguinte comando:
    
        Set-MailboxServer -Identity <ServerName> -DatabaseCopyActivationDisabledAndMoveNow $true

4.  Depois de todos os bancos de dados serem removidos do servidor de caixa de correio, você deve verificar se os bancos de dados foram movidos com êxito. Para fazer isso, execute o seguinte comando:
    
        Get-MailboxDatabaseCopyStatus -Server <ServerName> | group status

5.  Verifique se o servidor não hospeda nenhuma cópia ativa do banco de dados. Reinicie o servidor.

6.  Depois que o servidor tiver sido reiniciado com êxito, execute novamente a sondagem associada como mostrado na etapa 2c na seção Verifying the issue still exists.

7.  Se a investigação for bem sucedida, faça failover dos bancos de dados executando o seguinte comando:
    
        Set-MailboxServer -Identity <ServerName> -DatabaseCopyActivationDisabledAndMoveNow $false

8.  Se a sonda continuar a falhar, talvez você precise de ajuda para resolver esse problema. Contate um profissional do Suporte Microsoft para resolver esse problema. Para entrar em contato com um profissional do Suporte Microsoft, visite o [Centro de Soluções do Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=180809). No painel de navegação, clique em **Recursos e opções de suporte** e use uma das opções listadas em **Obter suporte técnico** para entrar em contato com um profissional do Suporte Microsoft. Como a sua organização pode ter um procedimento específico para entrar em contato diretamente os Serviços de Suporte a Produtos Microsoft, tenha certeza de consultar primeiro as diretrizes da sua organização.

## Ações de recuperação de POPCTPMonitor

Esse alerta do monitor normalmente é emitido em servidores de autoridade de certificação (CAS).

1.  Reinicie o serviço POP3 nos servidores que estão executando a função CAS. Para obter mais informações, consulte [Iniciar e interromper os serviços POP3](https://technet.microsoft.com/pt-br/library/aa997475\(v=exchg.150\)).

2.  Execute novamente a sonda associada conforme mostrado na etapa 2c na seção Verifying the issue still exists.

3.  Se o problema ainda existir, execute os seguintes comandos no PowerShell do Windows:
    
    1.  ``` 
        Set-PopSettings -server <CAS server name> -ProtocolLoggingEnabled $true
        ```
    
    2.  Reinicie o serviço POP3 nos servidores que estão executando a função CAS.
    
    3.  Execute novamente a sonda associada conforme mostrado na etapa 2c na seção Verifying the issue still exists.
    
    4.  Execute o seguinte comando e encontre o local do arquivo de log:
        
            Get-PopSettings -server <CAS server name>
    
    5.  Execute o seguinte comando para determinar qual caixa de correio está atendendo o comando comparando os carimbos de data/hora com a sondagem:
        
            Get-ServerHealth <mailbox server name> | ?{ $_.HealthSetName -like "POP*"}
    
    6.  Se qualquer um desses servidores forem relatados como não íntegros, siga as etapas listadas na seção PopTestDeepMonitor and PopSelfTestMonitor Recovery Actions.

4.  Se o servidor de caixa de correio for relatado como íntegro, reinicie o CAS.

5.  Após a reinicialização do servidor, execute novamente a sonda associada conforme descrito na etapa 2c da seção Verifying the issue still exists.

6.  Desative o log de protocolo executando o seguinte comando:
    
        Set-PopSettings -server <CAS server name> -ProtocolLoggingEnabled $false

7.  Reinicie o serviço POP3 nos servidores que estão executando a função CAS. Para obter mais informações, consulte [Iniciar e interromper os serviços POP3](https://technet.microsoft.com/pt-br/library/aa997475\(v=exchg.150\)).

8.  Se a sonda continuar a falhar, talvez você precise de ajuda para resolver esse problema. Contate um profissional do Suporte Microsoft para resolver esse problema. Para entrar em contato com um profissional do Suporte Microsoft, visite o [Centro de Soluções do Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=180809). No painel de navegação, clique em **Recursos e opções de suporte** e use uma das opções listadas em **Obter suporte técnico** para entrar em contato com um profissional do Suporte Microsoft. Como a sua organização pode ter um procedimento específico para entrar em contato diretamente os Serviços de Suporte a Produtos Microsoft, tenha certeza de consultar primeiro as diretrizes da sua organização.

## Ações de recuperação de PopProxyTestMonitor

1.  Reinicie o serviço POP3 nos servidores que estão executando a função CAS. Para obter mais informações, consulte [Iniciar e interromper os serviços POP3](https://technet.microsoft.com/pt-br/library/aa997475\(v=exchg.150\)).

2.  Execute novamente a sonda associada conforme mostrado na etapa 2c na seção Verifying the issue still exists.

3.  Se a sondagem continuar a falhar, reinicie o CAS.

4.  Após a reinicialização do servidor, execute novamente a sonda associada conforme descrito na etapa 2c da seção Verifying the issue still exists.

5.  Se a sonda continuar a falhar, talvez você precise de ajuda para resolver esse problema. Contate um profissional do Suporte Microsoft para resolver esse problema. Para entrar em contato com um profissional do Suporte Microsoft, visite o [Centro de Soluções do Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=180809). No painel de navegação, clique em **Recursos e opções de suporte** e use uma das opções listadas em **Obter suporte técnico** para entrar em contato com um profissional do Suporte Microsoft. Como a sua organização pode ter um procedimento específico para entrar em contato diretamente os Serviços de Suporte a Produtos Microsoft, tenha certeza de consultar primeiro as diretrizes da sua organização.

## Ações de recuperação de AverageCommandProcessingTimeGt60sMonitor

Esse alerta do monitor normalmente é emitido em servidores de caixa de correio ou CA.

1.  Reinicie o serviço POP3 nos servidores de caixa de correio ou CA. Para obter mais informações, consulte [Iniciar e interromper os serviços POP3](https://technet.microsoft.com/pt-br/library/aa997475\(v=exchg.150\)).

2.  Aguarde 10 minutos para ver se o monitor permanece íntegro. Após 10 minutos, execute o seguinte comando (o exemplo usa o server1.contoso.com).
    
        Get-ServerHealth server1.contoso.com | ?{$_.HealthSetName -like "POP*"}

3.  Se o problema ainda persistir, você precisará reiniciar o servidor. Se o servidor for um CAS, basta reiniciá-lo. Se o servidor for um servidor de caixa de correio, você deve realizar failover do banco de dados e verificar os resultados. Para fazer isso, siga estas etapas:
    
    1.  Realize failover nos bancos de dados hospedados no servidor usando o comando a seguir:
        
            Set-MailboxServer -Identity <ServerName> -DatabaseCopyActivationDisabledAndMoveNow $true
        
        **Observação**   Neste exemplo de código e em todos os exemplos subsequentes, substitua *server1.contoso.com* pelo nome real do servidor.
    
    2.  Verifique se todos os bancos de dados foram movidos do servidor que está relatando o problema. Para fazer isso, execute o seguinte comando:
        
            Get-MailboxDatabaseCopyStatus -Server <ServerName> | group status
        
        Se a saída do comando não mostrar nenhuma cópia ativa no servidor, reinicie o servidor.

4.  Após a reinicialização do servidor, aguarde 10 minutos e execute novamente o comando mostrado na etapa 2 para ver se o monitor permanece íntegro.

5.  Se o monitor é íntegro, e este é um servidor de caixa de correio, realize failover nos bancos de dados novamente para o servidor de caixa de correio executando o seguinte comando:
    
        Set-MailboxServer -Identity <ServerName> -DatabaseCopyActivationDisabledAndMoveNow $false

6.  Se a sonda continuar a falhar, talvez você precise de ajuda para resolver esse problema. Contate um profissional do Suporte Microsoft para resolver esse problema. Para entrar em contato com um profissional do Suporte Microsoft, visite o [Centro de Soluções do Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=180809). No painel de navegação, clique em **Recursos e opções de suporte** e use uma das opções listadas em **Obter suporte técnico** para entrar em contato com um profissional do Suporte Microsoft. Como a sua organização pode ter um procedimento específico para entrar em contato diretamente os Serviços de Suporte a Produtos Microsoft, tenha certeza de consultar primeiro as diretrizes da sua organização.

## Para obter mais informações

[Iniciar e interromper os serviços POP3](https://technet.microsoft.com/pt-br/library/aa997475\(v=exchg.150\))

[Test-PopConnectivity](https://technet.microsoft.com/pt-br/library/bb738143\(v=exchg.150\))

