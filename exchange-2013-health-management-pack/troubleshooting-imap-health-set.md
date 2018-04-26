---
title: Conjunto de integridade IMAP para solução de problemas
TOCTitle: Conjunto de integridade IMAP para solução de problemas
ms:assetid: 2a06e671-4cc2-4ce5-bf53-6243ea140f20
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/ms.exch.scom.imap(v=EXCHG.150)
ms:contentKeyID: 53275617
ms.date: 03/07/2017
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Conjunto de integridade IMAP para solução de problemas

 

_**Aplica-se a:**Exchange Server 2013_

_**Tópico modificado em:**2015-03-09_

O conjunto de integridade IMAP monitora a disponibilidade da infraestrutura proxy IMAP4 no servidor de Acesso para Cliente (CAS). O conjunto de integridade do IMAP tem uma relação bem próxima com os seguintes conjuntos de integridade:

[Solucionando problemas de IMAP. Conjunto de integridade de protocolo](troubleshooting-imap-protocol-health-set.md)

[Solucionando problemas de IMAP. Conjunto de integridade de proxy](troubleshooting-imap-proxy-health-set.md)

Se você receber um alerta especificando que o IMAP não está íntegro, isso indicará um problema que pode impedir seus usuários de acessar suas caixas de correio usando IMAP.

## Explicação

O serviço IMAP4 é monitorado usando as seguintes sondas e monitores.


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
<td><p>ImapCTPProbe</p></td>
<td><p>IMAP</p></td>
<td><p>Active Directory</p>
<p>Autenticação</p>
<p>Autenticação de servidor de Caixa de Correio</p>
<p>Alta Disponibilidade</p>
<p>Sistema de rede</p></td>
<td><p>ImapCTPMonitor (conjunto de integridade IMAP)</p></td>
</tr>
<tr class="even">
<td><p>ImapProxyTestProbe</p></td>
<td><p>IMAP.Proxy</p></td>
<td><p>Active Directory</p>
<p>Autenticação</p></td>
<td><p>ImapProxyTestMonitor (conjunto de integridade IMAP.Proxy)</p></td>
</tr>
<tr class="odd">
<td><p>ImapDeepTestProbe</p></td>
<td><p>IMAP.Protocol</p></td>
<td><p>Active Directory</p>
<p>Autenticação</p>
<p>Repositório de Informações</p>
<p>Alta Disponibilidade</p></td>
<td><p>IMAP.Protocol (conjunto de integridade IMAP.Protocol)</p></td>
</tr>
<tr class="even">
<td><p>ImapSelfTestProbe</p></td>
<td><p>IMAP.Protocol</p></td>
<td><p>Active Directory</p>
<p>Autenticação</p></td>
<td><p>IMAP.Protocol (conjunto de integridade IMAP.Protocol)</p>
<p>AverageCommandProcessingTimeGt60sMonitor (conjunto de integridade IMAP)</p></td>
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
        
        Por exemplo, para recuperar os detalhes do conjunto de integridade do IMAP sobre server1.contoso.com, execute o seguinte comando:
        
            Get-ServerHealth server1.contoso.com | ?{$_.HealthSetName -like "IMAP*"}
    
    2.  Verifique a saída do comando para determinar qual monitor relatou o erro. O valor **AlertValue** do monitor que emitiu o alerta será `Unhealthy`.
    
    3.  Execute novamente a sonda associada do monitor que está em estado não íntegro. Consulte a tabela na seção Explanation para encontrar a sonda associada. Para fazer isso, execute o seguinte comando:
        
            Invoke-MonitoringProbe <health set name>\<probe name> -Server <server name> | Format-List
        
        Por exemplo, vamos supor que o monitor com falha seja o **ImapCTPMonitor**. A sonda associada a esse monitor é **ImapCTPProbe**. Para executar essa sonda em server1.contoso.com, execute o seguinte comando:
        
            Invoke-MonitoringProbe IMAP\ImapCTPProbe -Server server1.contoso.com | Format-List
    
    4.  Na saída do comando, verifique o valor **Resultado** da sonda. Se o valor for **Êxito**, significa que o problema foi um erro transitório e não existe mais. Caso contrário, consulte as etapas de recuperação descritas nas seções seguintes.

## Ações de recuperação do ImapTestDeepMonitor e do ImapSelfTestMonitor

1.  Reinicie o serviço IMAP4 do Exchange no servidor back-end. Para obter mais informações sobre como parar e iniciar o serviço IMAP4, consulte [Iniciar e interromper os serviços de IMAP4](https://technet.microsoft.com/pt-br/library/bb124022\(v=exchg.150\)).

2.  Execute novamente a sonda associada conforme mostrado na etapa 2c na seção Verifying the issue still exists.

3.  Se o problema ainda existir, execute o failover nos bancos de dados hospedados no servidor de caixa de correio usando o seguinte comando:
    
        Set-MailboxServer -Identity <ServerName> -DatabaseCopyActivationDisabledAndMoveNow $true

4.  Verifique se todos os bancos de dados foram retirados do servidor que está reportando o problema. Para fazer isso, execute o seguinte comando:
    
        Get-MailboxDatabaseCopyStatus -Server server1.contoso.com | Group Status
    
    Se a saída do comando não mostrar nenhuma cópia ativa no servidor, reinicie o servidor.

5.  Execute novamente a sonda associada conforme mostrado na etapa 2c na seção Verifying the issue still exists.

6.  Se a investigação for bem sucedida, faça failover dos bancos de dados executando o seguinte comando:
    
        Set-MailboxServer server1.contoso.com -DatabaseCopyActivationDisabledAndMoveNow $false

7.  Se a sonda continuar a falhar, talvez você precise de ajuda para resolver esse problema. Contate um profissional do Suporte Microsoft para resolver esse problema. Para entrar em contato com um profissional do Suporte Microsoft, visite o [Centro de Soluções do Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=180809). No painel de navegação, clique em **Recursos e opções de suporte** e use uma das opções listadas em **Obter suporte técnico** para entrar em contato com um profissional do Suporte Microsoft. Como a sua organização pode ter um procedimento específico para entrar em contato diretamente os Serviços de Suporte a Produtos Microsoft, tenha certeza de consultar primeiro as diretrizes da sua organização.

## Ações de recuperação do ImapCTPMonitor

Este alerta do monitor é normalmente emitido em servidores CAS.

1.  Reinicie o serviço IMAP4 do Exchange no servidor back-end. Para obter mais informações sobre como parar e iniciar o serviço IMAP4, consulte [Iniciar e interromper os serviços de IMAP4](https://technet.microsoft.com/pt-br/library/bb124022\(v=exchg.150\)).

2.  Execute novamente a sonda associada, conforme exibido na etapa 2.c., na seção Verifying the issue still exists.

3.  Se o problema ainda existir, será necessário ativar o registro em log do protocolo IMAP para ajudar a resolver o problema. Para fazer isso, siga estas etapas:
    
    1.  No Windows PowerShell, execute o seguinte comando:
        
            Set-ImapSettings -server <CAS server name> -ProtocolLoggingEnabled $true
    
    2.  Reinicie o serviço IMAP4 do Exchange no servidor back-end. Para obter mais informações sobre como parar e iniciar o serviço IMAP4, consulte [Iniciar e interromper os serviços de IMAP4](https://technet.microsoft.com/pt-br/library/bb124022\(v=exchg.150\))
    
    3.  Execute novamente a sonda associada conforme mostrado na etapa 2c na seção Verifying the issue still exists.
    
    4.  Execute o seguinte comando e determine o local do arquivo de log. Para fazer isso, execute o seguinte comando:
        
            Get-ImapSettings -server <CAS server name>
    
    5.  Determine a caixa de correio que está atendendo a esse comando. O nome do servidor de caixa de correio é o valor para o valor `_Mbx:` na mensagem de erro.
    
    6.  Execute o seguinte comando:
        
            Get-ServerHealth mailbox1.contoso.com | ?{$_.HealtSetName -like "IMAP*"}
        
        **Observação**   Neste comando, substitua *mailbox1.contoso.com* pelo nome do servidor real de Caixa de Correio.
    
    7.  Se qualquer um dos monitores listados na saída do comando for reportado com não íntegro, será necessário resolver esses monitores primeiro. Execute as etapas de solução de problema descritas na seção ImapTestDeepMonitor and ImapSelfTestMonitor Recovery Actions.

4.  Se o servidor de Caixa de Correio for reportado como não íntegro, reinicie o CAS.

5.  Após a reinicialização do servidor, execute novamente a sonda associada conforme mostrado na etapa 2c da seção Verifying the issue still exists.

6.  Desative o registro em log do protocolo. Para fazer isso, execute o seguinte comando do Windows PowerShell:
    
        Set-ImapSettings -server <CAS server name> -ProtocolLoggingEnabled $false

7.  Reinicie o serviço IMAP4.

8.  Se a sonda continuar a falhar, talvez você precise de ajuda para resolver esse problema. Contate um profissional do Suporte Microsoft para resolver esse problema. Para entrar em contato com um profissional do Suporte Microsoft, visite o [Centro de Soluções do Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=180809). No painel de navegação, clique em **Recursos e opções de suporte** e use uma das opções listadas em **Obter suporte técnico** para entrar em contato com um profissional do Suporte Microsoft. Como a sua organização pode ter um procedimento específico para entrar em contato diretamente os Serviços de Suporte a Produtos Microsoft, tenha certeza de consultar primeiro as diretrizes da sua organização.

## Ações de recuperação do ImapProxyTestMonitor

1.  Reinicie o serviço IMAP4.

2.  Execute novamente a sonda associada conforme mostrado na etapa 2c na seção Verifying the issue still exists.

3.  Se a sonda ainda falhar, reinicie o CAS.

4.  Após a reinicialização do servidor, execute novamente a sonda associada conforme mostrado na etapa 2c da seção Verifying the issue still exists.

5.  Se a sonda continuar a falhar, talvez você precise de ajuda para resolver esse problema. Contate um profissional do Suporte Microsoft para resolver esse problema. Para entrar em contato com um profissional do Suporte Microsoft, visite o [Centro de Soluções do Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=180809). No painel de navegação, clique em **Recursos e opções de suporte** e use uma das opções listadas em **Obter suporte técnico** para entrar em contato com um profissional do Suporte Microsoft. Como a sua organização pode ter um procedimento específico para entrar em contato diretamente os Serviços de Suporte a Produtos Microsoft, tenha certeza de consultar primeiro as diretrizes da sua organização.

## Ações de recuperação de AverageCommandProcessingTimeGt60sMonitor RequestsQueuedGt500Monitor

Este alerta do monitor é normalmente emitido em servidores CAS e de Caixa de Correio.

1.  Reinicie o serviço IMAP4 do Exchange no servidor back-end ou CAS. Para obter mais informações sobre como parar e iniciar o serviço IMAP4, consulte [Iniciar e interromper os serviços de IMAP4](https://technet.microsoft.com/pt-br/library/bb124022\(v=exchg.150\))

2.  Aguarde 10 minutos para ver se o monitor permanece íntegro. Após 10 minutos, execute o seguinte comando:
    
        Get-ServerHealth server1.contoso.com | ?{$_.HealthSetName -like "IMAP*"}
    
    **Observação**   Neste comando, substitua *server1.contoso.com* pelo nome do servidor real.

3.  Aguarde 10 minutos e execute o comando exibido na etapa 2 novamente para ver se o monitor permanece íntegro.

4.  Se o problema ainda existir, será necessário reiniciar o servidor. Se o servidor for um CAS, basta reiniciá-lo. Se o servidor for de Caixa de Correio, faça o seguinte:
    
    1.  Faça o failover dos bancos de dados que estão hospedados no servidor. Para fazer isso, execute o seguinte comando:
        
            Set-MailboxServer server1.contoso.com -DatabaseCopyActivationDisabledAndMoveNow $true
        
        **Observação**   Neste e em todos os exemplos de código subsequentes, substitua *server1.contoso.com* pelo nome do servidor real.
    
    2.  Verifique se todos os bancos de dados foram retirados do servidor que está reportando o problema. Para fazer isso, execute o seguinte comando:
        
            Get-MailboxDatabaseCopyStatus -Server server1.contoso.com | Group Status
        
        Se a saída do comando não mostrar nenhuma cópia ativa no servidor, reinicie o servidor.

5.  Após a reinicialização do servidor, aguarde 10 minutos e execute novamente o comando mostrado na etapa 2 para ver se o monitor permanece íntegro.

6.  Se o monitor permanecer íntegro e for um servidor de Caixa de Correio, aplique o failover nos bancos de dados executando o seguinte comando:
    
        Set-MailboxServer server1.contoso.com -DatabaseCopyActivationDisabledAndMoveNow $false

7.  Se a sonda continuar a falhar, talvez você precise de ajuda para resolver esse problema. Contate um profissional do Suporte Microsoft para resolver esse problema. Para entrar em contato com um profissional do Suporte Microsoft, visite o [Centro de Soluções do Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=180809). No painel de navegação, clique em **Recursos e opções de suporte** e use uma das opções listadas em **Obter suporte técnico** para entrar em contato com um profissional do Suporte Microsoft. Como a sua organização pode ter um procedimento específico para entrar em contato diretamente os Serviços de Suporte a Produtos Microsoft, tenha certeza de consultar primeiro as diretrizes da sua organização.

## Para obter mais informações

[POP3 e IMAP4 no Exchange Server 2013](https://technet.microsoft.com/pt-br/library/jj657728\(v=exchg.150\))

[Habilitar IMAP4 no Exchange 2013](https://technet.microsoft.com/pt-br/library/bb124489\(v=exchg.150\))

[Test-ImapConnectivity](https://technet.microsoft.com/pt-br/library/bb738126\(v=exchg.150\))

