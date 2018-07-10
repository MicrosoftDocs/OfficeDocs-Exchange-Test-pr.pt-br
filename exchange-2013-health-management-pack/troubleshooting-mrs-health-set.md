---
title: Conjunto de integridade do MRS de solução de problemas
TOCTitle: Conjunto de integridade do MRS de solução de problemas
ms:assetid: 21947ed6-1584-4db9-9cd6-f6c1de22e352
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/ms.exch.scom.mrs(v=EXCHG.150)
ms:contentKeyID: 53275616
ms.date: 03/07/2017
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Conjunto de integridade do MRS de solução de problemas

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2015-03-09_

O conjunto de integridade Serviço de Replicação de Caixa de Correio (MRS) monitora a integridade geral do serviço MRS.

## Explicação

O serviço MRS é monitorado usando as seguintes sondas e monitores.


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
<td><p>MRSServiceCrashingProbe</p></td>
<td><p>MRS</p></td>
<td><p>Repositório de Informações</p></td>
<td><p>MRSServiceCrashingMonitor</p></td>
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
        
        Por exemplo, para recuperar os detalhes do conjunto de integridade do MRSsobre server1.contoso.com, execute o seguinte comando:
        
            Get-ServerHealth server1.contoso.com | ?{$_.HealthSetName -eq "MRS"}
    
    2.  Verifique a saída do comando para determinar qual monitor relatou o erro. O valor **AlertValue** do monitor que emitiu o alerta será `Unhealthy`.
    
    3.  Execute novamente a sonda associada do monitor que está em estado não íntegro. Consulte a tabela na seção Explanation para encontrar a sonda associada. Para fazer isso, execute o seguinte comando:
        
            Invoke-MonitoringProbe <health set name>\<probe name> -Server <server name> | Format-List
        
        Por exemplo, vamos supor que o monitor com falha seja o **MRSServiceCrashingMonitor**. A sonda associada a esse monitor é **MRSServiceCrashingProbe**. Para executar essa sonda em server1.contoso.com, execute o seguinte comando:
        
            Invoke-MonitoringProbe MRS\MRSServiceCrashingProbe -Server server1.contoso.com | Format-List
    
    4.  Na saída do comando, verifique o valor **Resultado** da sonda. Se o valor for **Êxito**, significa que o problema foi um erro transitório e não existe mais. Caso contrário, consulte as etapas de recuperação descritas nas seções seguintes.

## Problemas comuns

Quando você recebe um alerta de um conjunto de integridade, a mensagem de email contém as seguintes informações:

  - Nome do servidor que enviou o alerta

  - Hora e data em que o alerta ocorreu

  - Mecanismo de autenticação usado e informações de credenciais

  - Rastreamento de exceções completo do último erro, incluindo dados de diagnóstico e informações de cabeçalho HTTP específicas
    
    Você pode usar as informações no rastreamento de exceções completo para ajudar a solucionar o problema. A exceção gerada pela sonda contém um Motivo da Falha que descreve por que a sonda falhou.

**Caixa de correio bloqueada**

Quando uma Caixa de Correio está bloqueada, você pode receber um alerta que lembra o seguinte:

*MailboxIdentity: namprd03.prod.outlook.com/Microsoft Exchange Hosted Organizations/example.com/User6 MailboxGuid: Primary (00000000-abcd-01234-5678-1234567890ab) RequestFlags: IntraOrg, Pull, Protected Database: exampledb-db089 Exception: MapiExceptionADUnavailable: Unable to prepopulate the cache for user …*

Isso indica que uma caixa de correio está bloqueada. Para desbloquear a caixa de correio, execute o seguinte comando:

    New-MailboxRepairRequest -CorruptionType LockedMoveTarget -Identity <mailboxIdentity> [-Archive]

**Observação**   Neste comando, substitua \<*mailboxIdentity*\> pelo nome da caixa de correio fornecida na mensagem de email como **MailboxIdentity**. Se a caixa de correio estiver em uma caixa de correio de arquivo morto, será necessário incluir o sinalizador **–Archive**. É possível determinar se uma caixa de correio é uma caixa de correio primária ou de arquivo morto vendo o campo **MailboxGuid** no alerta.

**Trabalho de migração corrompido**

Quando ocorre um trabalho de migração corrompido, você pode receber um alerta parecido com o seguinte:

*Notification thrown by MailboxMigration at 9/7/2012 9:08:32 PM. Detalhes: Diagnostic Information: ProcessCacheEntry: First Organization :: /o=ExchangeLabs/ou=Exchange Administrative Group (FYDIBOHF23SPDLT)/cn=Recipients/cn=e80fc128879e452ebc882f6bca7007fa-Migration.8*

A corrupção ocorre quando os metadados de migração encontram problemas. Ao ocorrer a corrupção, a Microsoft recebe um relatório Watson que será investigado. Para se recuperar desse problema, é necessário remover o lote de migração e recriá-lo. Para fazer isso, siga estas etapas:

1.  Para remover o lote corrompido, execute o seguinte comando:
    
        Remove-MigrationBatch -Identity

2.  Para recriar o lote, execute o seguinte comando:
    
        New-MigrationBatch -Local -Name

Para mais informações, consulte [Cmdlets do Exchange 2013](https://technet.microsoft.com/pt-br/library/bb124413\(v=exchg.150\))

**Alerta do MailboxMigration: CriticalError**

Quando ocorre um erro crítico durante a migração de emails, você pode receber um alerta parecido com o seguinte:

*Notification thrown by MailboxMigration at 9/7/2012 9:08:32 PM. Detalhes: Diagnostic Information: ProcessCacheEntry: First Organization :: /o=ExchangeLabs/ou=Exchange Administrative Group (FYDIBOHF23SPDLT)/cn=Recipients/cn=e80fc128879e452ebc882f6bca7007fa-Migration.8*

Para resolver esse problema, você precisa tentar novamente a migração. Para fazer isso, execute o seguinte comando ou pressione o botão **Iniciar** no Centro de administração do Exchange (EAC).

    Call start-migrationbatch -Identity batchName

Quando esse problema ocorre, uma mensagem do Dr. Watson é enviada para a Microsoft para investigação.

**O Serviço de Replicação de Migração do Exchange não está em execução**

Quando esse motivo de erro for exibido, você poderá confirmar a integridade do serviço executando o seguinte comando:

    Test-MRSHealth <servername> -MonitoringContext:$true

Também pode tentar iniciar o serviço executando o seguinte comando:

    Start-Service msexchangemailboxreplication

**Falha no Ping RCP MSExchangeMailboxReplication**

Quando esse motivo de erro é exibido, você pode receber um alerta parecido com o seguinte:

*An issue with MRS was detected at 6/26/2012 6:08:47 AM. Details: MRS RPC Ping check for server \<ServerName\> failed with the following error: O ponto de extremidade de RPC para o Serviço de Replicação do Microsoft Exchange não respondeu:*

Quando esse problema ocorrer, você poderá confirmar a integridade do serviço executando o seguinte comando:

    Test-MRSHealth <servername> -MonitoringContext:$true

Também pode tentar reiniciar o serviço executando o seguinte comando:

    Restart-Service msexchangemailboxreplication

**O serviço MSExchangeMailboxReplication falha repetidamente**

Quando o serviço MSExchangeMailboxReplication falha ou para de responder, você pode receber um alerta que lembra o seguinte:

*The MRS process has crashed at least 3 times in last 01:00:00. \<b\>Watson Message:\</b\> Watson report about to be sent for process id: 41432, with parameters: E12, \<ServerName\>, 15.00.0516.024, MSExchangeMailboxReplication, M.Exchange.MailboxReplicationService, M.E.M.BaseJob.BeginJob, System.ApplicationException, 7ec9, 15.00.0516.024. ErrorReportingEnabled: True.*

Quando esse problema ocorrer, você poderá confirmar a integridade do serviço executando o seguinte comando:

    Test-MRSHealth <servername> -MonitoringContext:$true

Também pode tentar reiniciar o serviço executando o seguinte comando:

    Restart-Service msexchangemailboxreplication

**MSExchangeMailboxReplication não está examinando as filas de MDB**

Quando o serviço MSExchangeMailboxReplication fnão examina filas, você pode receber um alerta que lembra o seguinte:

*An issue with MRS was detected at 6/12/2012 6:20:44 PM. Detalhes: MRS queue scan check for server \<servername\> failed with the following error: O Serviço de Replicação de Caixa de Correio do Microsoft Exchange não está examinando filas de banco de dados de caixa de correio para os trabalhos. Idade do último exame: 04:38:02.1959439..*

Quando esse problema ocorrer, você poderá confirmar a integridade do serviço executando o seguinte comando:

    Test-MRSHealth <servername> -MonitoringContext:$true

Também pode tentar reiniciar o serviço executando o seguinte comando:

    Restart-Service msexchangemailboxreplication

**Etapas adicionais de solução de problemas**

1.  Inicie o Gerenciador de IIS e conecte-se ao servidor que está reportando o problema para verificar se o pool de aplicativos **MSExchangeServicesAppPool** está em execução.

2.  No Gerenciador de IIS, clique em **Pools de Aplicativo** e recicle o pool de aplicativos **MSExchangeServicesAppPool** executando o seguinte comando a partir do Shell:
    
        %SystemRoot%\System32\inetsrv\Appcmd recycle MSExchangeServicesAppPool

3.  Execute novamente a sonda associada conforme mostrado na etapa 2c na seção Verifying the issue still exists.

4.  Se o problema ainda existir, recicle o serviço IIS usando o utilitário IISReset ou executando o seguinte comando:
    
        Iisreset /noforce

5.  Execute novamente a sonda associada conforme mostrado na etapa 2c na seção Verifying the issue still exists.

6.  Se o problema ainda existir, reinicie o servidor.

7.  Após a reinicialização do servidor, execute novamente a sonda associada, conforme exibido na etapa 2c, na seção Verifying the issue still exists.

8.  Se a sonda continuar a falhar, talvez você precise de ajuda para resolver esse problema. Contate um profissional do Suporte Microsoft para resolver esse problema. Para entrar em contato com um profissional do Suporte Microsoft, visite o [Centro de Soluções do Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=180809). No painel de navegação, clique em **Recursos e opções de suporte** e use uma das opções listadas em **Obter suporte técnico** para entrar em contato com um profissional do Suporte Microsoft. Como a sua organização pode ter um procedimento específico para entrar em contato diretamente os Serviços de Suporte a Produtos Microsoft, tenha certeza de consultar primeiro as diretrizes da sua organização.

## Para obter mais informações

[Novidades do Exchange 2013](https://technet.microsoft.com/pt-br/library/jj150540\(v=exchg.150\))

[Cmdlets do Exchange 2013](https://technet.microsoft.com/pt-br/library/bb124413\(v=exchg.150\))

