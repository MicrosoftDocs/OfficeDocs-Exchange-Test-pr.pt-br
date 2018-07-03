---
title: Solucionando problemas de integridade HubTransport definido
TOCTitle: Solucionando problemas de integridade HubTransport definido
ms:assetid: e3932ce3-836c-4230-9f64-63af1b704d79
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/ms.exch.scom.hubtransport(v=EXCHG.150)
ms:contentKeyID: 54652041
ms.date: 03/07/2017
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Solucionando problemas de integridade HubTransport definido

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2015-03-09_

O conjunto de integridade **HubTransport** monitora a integridade geral do pipeline de transporte nos servidores de caixa de correio que é responsável pelo roteamento de mensagens em sua organização. Para obter mais informações, consulte [Fluxo de mensagens](https://technet.microsoft.com/pt-br/library/aa996349\(v=exchg.150\)).

Se você receber um alerta que indica que o conjunto de integridade **HubTransport** não está íntegro, isso indica um problema que pode impedir que os emails de sendo roteadas e entregues.

## Explicação

O serviço **HubTransport** é monitorado usando as seguintes sondas e monitores.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Sonda</th>
<th>Conjunto de integridade</th>
<th>Monitores associados</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>ActiveQueueDrainFailureProbe</p></td>
<td><p>HubTransport</p></td>
<td><p>ActiveQueueDrainFailureMonitor</p></td>
</tr>
<tr class="even">
<td><p>DiagnosticsAggregationLocalSnapshotProbe</p></td>
<td><p>HubTransport</p></td>
<td><p>DiagnosticsAggregationLocalSnapshotMonitor</p></td>
</tr>
<tr class="odd">
<td><p>DiagnosticsAggregationWebServiceProbe</p></td>
<td><p>HubTransport</p></td>
<td><p>DiagnosticsAggregationWebServiceMonitor</p></td>
</tr>
<tr class="even">
<td><p>HubAvailabilityProbe</p></td>
<td><p>HubTransport</p></td>
<td><p>HubAvailabilityMonitor</p></td>
</tr>
<tr class="odd">
<td><p>HubTransportServiceRunning</p></td>
<td><p>HubTransport</p></td>
<td><p>HubTransportServiceRunningMonitor</p></td>
</tr>
<tr class="even">
<td><p>ShadowQueueDiscardDrainFailureProbe</p></td>
<td><p>HubTransport</p></td>
<td><p>ShadowQueueDiscardDrainFailureMonitor</p></td>
</tr>
<tr class="odd">
<td><p>ThrottlingServiceRunning</p></td>
<td><p>HubTransport</p></td>
<td><p>ThrottlingServiceRunningMonitor</p></td>
</tr>
<tr class="even">
<td><p>TransportEdgeSync.Service.Probe</p></td>
<td><p>HubTransport</p></td>
<td><p>TransportEdgeSync.Service.Monitor</p></td>
</tr>
<tr class="odd">
<td><p>TransportLogSearchRunningProbe</p></td>
<td><p>HubTransport</p></td>
<td><p>TransportLogSearchRunningMonitor</p></td>
</tr>
<tr class="even">
<td><p>Nenhum (notificação ou seleção)</p></td>
<td><p>HubTransport</p></td>
<td><p>BootloaderOutstandingItemsTriggerMonitor</p></td>
</tr>
<tr class="odd">
<td><p>Nenhum (notificação ou seleção)</p></td>
<td><p>HubTransport</p></td>
<td><p>CrashEvent.edgetransport</p></td>
</tr>
<tr class="even">
<td><p>Nenhum (notificação ou seleção)</p></td>
<td><p>HubTransport</p></td>
<td><p>CrashEvent.msexchangethrottling</p></td>
</tr>
<tr class="odd">
<td><p>Nenhum (notificação ou seleção)</p></td>
<td><p>HubTransport</p></td>
<td><p>CrashEvent.msexchangetransport</p></td>
</tr>
<tr class="even">
<td><p>Nenhum (notificação ou seleção)</p></td>
<td><p>HubTransport</p></td>
<td><p>CrashEvent.msexchangetransportlogsearch</p></td>
</tr>
<tr class="odd">
<td><p>Nenhum (notificação ou seleção)</p></td>
<td><p>HubTransport</p></td>
<td><p>EdgeTransportBackpressureSustainedTimeMonitor</p></td>
</tr>
<tr class="even">
<td><p>Nenhum (notificação ou seleção)</p></td>
<td><p>HubTransport</p></td>
<td><p>FederatedDecryptionAgentFailedToXDecryptMonitor</p></td>
</tr>
<tr class="odd">
<td><p>Nenhum (notificação ou seleção)</p></td>
<td><p>HubTransport</p></td>
<td><p>HubTransport.ServiceInconsistentState.Monitor</p></td>
</tr>
<tr class="even">
<td><p>Nenhum (notificação ou seleção)</p></td>
<td><p>HubTransport</p></td>
<td><p>IsMemberOfResolverExpandedGroupsCacheSizeMonitor</p></td>
</tr>
<tr class="odd">
<td><p>Nenhum (notificação ou seleção)</p></td>
<td><p>HubTransport</p></td>
<td><p>IsMemberOfResolverResolvedGroupsCacheSizeMonitor</p></td>
</tr>
<tr class="even">
<td><p>Nenhum (notificação ou seleção)</p></td>
<td><p>HubTransport</p></td>
<td><p>Messages.failed.to.be.made.redundant.Monitor</p></td>
</tr>
<tr class="odd">
<td><p>Nenhum (notificação ou seleção)</p></td>
<td><p>HubTransport</p></td>
<td><p>MessagesDeferredDuringCategorizationMonitor</p></td>
</tr>
<tr class="even">
<td><p>Nenhum (notificação ou seleção)</p></td>
<td><p>HubTransport</p></td>
<td><p>MessageTrackingLogsDirQuotaMonitor</p></td>
</tr>
<tr class="odd">
<td><p>Nenhum (notificação ou seleção)</p></td>
<td><p>HubTransport</p></td>
<td><p>PrivateWorkingSetError.edgetransport</p></td>
</tr>
<tr class="even">
<td><p>Nenhum (notificação ou seleção)</p></td>
<td><p>HubTransport</p></td>
<td><p>PrivateWorkingSetError.msexchahangetransportlogsearch</p></td>
</tr>
<tr class="odd">
<td><p>Nenhum (notificação ou seleção)</p></td>
<td><p>HubTransport</p></td>
<td><p>PrivateWorkingSetError.msexchangethrottling</p></td>
</tr>
<tr class="even">
<td><p>Nenhum (notificação ou seleção)</p></td>
<td><p>HubTransport</p></td>
<td><p>PrivateWorkingSetError.msexchangetransport</p></td>
</tr>
<tr class="odd">
<td><p>Nenhum (notificação ou seleção)</p></td>
<td><p>HubTransport</p></td>
<td><p>PrivateWorkingSetWarning.edgetransport</p></td>
</tr>
<tr class="even">
<td><p>Nenhum (notificação ou seleção)</p></td>
<td><p>HubTransport</p></td>
<td><p>PrivateWorkingSetWarning.msexchangethrottling</p></td>
</tr>
<tr class="odd">
<td><p>Nenhum (notificação ou seleção)</p></td>
<td><p>HubTransport</p></td>
<td><p>PrivateWorkingSetWarning.msexchangetransport</p></td>
</tr>
<tr class="even">
<td><p>Nenhum (notificação ou seleção)</p></td>
<td><p>HubTransport</p></td>
<td><p>PrivateWorkingSetWarning.msexchangetransportlogsearch</p></td>
</tr>
<tr class="odd">
<td><p>Nenhum (notificação ou seleção)</p></td>
<td><p>HubTransport</p></td>
<td><p>ProcessProcessorTimeError.edgetransport</p></td>
</tr>
<tr class="even">
<td><p>Nenhum (notificação ou seleção)</p></td>
<td><p>HubTransport</p></td>
<td><p>ProcessProcessorTimeError.msexchangethrottling</p></td>
</tr>
<tr class="odd">
<td><p>Nenhum (notificação ou seleção)</p></td>
<td><p>HubTransport</p></td>
<td><p>ProcessProcessorTimeError.msexchangetransport</p></td>
</tr>
<tr class="even">
<td><p>Nenhum (notificação ou seleção)</p></td>
<td><p>HubTransport</p></td>
<td><p>ProcessProcessorTimeError.msexchangetransportlogsearch</p></td>
</tr>
<tr class="odd">
<td><p>Nenhum (notificação ou seleção)</p></td>
<td><p>HubTransport</p></td>
<td><p>ProcessProcessorTimeWarning.edgetransport</p></td>
</tr>
<tr class="even">
<td><p>Nenhum (notificação ou seleção)</p></td>
<td><p>HubTransport</p></td>
<td><p>ProcessProcessorTimeWarning.msexchangethrottling</p></td>
</tr>
<tr class="odd">
<td><p>Nenhum (notificação ou seleção)</p></td>
<td><p>HubTransport</p></td>
<td><p>ProcessProcessorTimeWarning.msexchangetransport</p></td>
</tr>
<tr class="even">
<td><p>Nenhum (notificação ou seleção)</p></td>
<td><p>HubTransport</p></td>
<td><p>ProcessProcessorTimeWarning.msexchangetransportlogsearch</p></td>
</tr>
<tr class="odd">
<td><p>Nenhum (notificação ou seleção)</p></td>
<td><p>HubTransport</p></td>
<td><p>QueueExternalAggregateMonitor</p></td>
</tr>
<tr class="even">
<td><p>Nenhum (notificação ou seleção)</p></td>
<td><p>HubTransport</p></td>
<td><p>QueueInternalAggregateMonitor</p></td>
</tr>
<tr class="odd">
<td><p>Nenhum (notificação ou seleção)</p></td>
<td><p>HubTransport</p></td>
<td><p>QueueInternalAggregateNormalPriorityMonitor</p></td>
</tr>
<tr class="even">
<td><p>Nenhum (notificação ou seleção)</p></td>
<td><p>HubTransport</p></td>
<td><p>QueueInternalHubRetryMonitor</p></td>
</tr>
<tr class="odd">
<td><p>Nenhum (notificação ou seleção)</p></td>
<td><p>HubTransport</p></td>
<td><p>QueueInternalHubRetryNormalPriorityMonitor</p></td>
</tr>
<tr class="even">
<td><p>Nenhum (notificação ou seleção)</p></td>
<td><p>HubTransport</p></td>
<td><p>QueueMailboxRetryMonitor</p></td>
</tr>
<tr class="odd">
<td><p>Nenhum (notificação ou seleção)</p></td>
<td><p>HubTransport</p></td>
<td><p>QueueNonSMTPRetryMonitor</p></td>
</tr>
<tr class="even">
<td><p>Nenhum (notificação ou seleção)</p></td>
<td><p>HubTransport</p></td>
<td><p>RuleEvaluationFailureEventLogMonitor</p></td>
</tr>
<tr class="odd">
<td><p>Nenhum (notificação ou seleção)</p></td>
<td><p>HubTransport</p></td>
<td><p>RuleEvaluationIgnoredFailureEventLogMonitor</p></td>
</tr>
<tr class="even">
<td><p>Nenhum (notificação ou seleção)</p></td>
<td><p>HubTransport</p></td>
<td><p>RuleEvaluationIgnoredFipsFailureEventLogMonitor</p></td>
</tr>
<tr class="odd">
<td><p>Nenhum (notificação ou seleção)</p></td>
<td><p>HubTransport</p></td>
<td><p>RuleEvaluationSmallScaleFailureEventLogMonitor</p></td>
</tr>
<tr class="even">
<td><p>Nenhum (notificação ou seleção)</p></td>
<td><p>HubTransport</p></td>
<td><p>RuleEvaluationSmallScaleFipsFailureEventLogMonitor</p></td>
</tr>
<tr class="odd">
<td><p>Nenhum (notificação ou seleção)</p></td>
<td><p>HubTransport</p></td>
<td><p>RuleExcessiveForkingEventLogMonitor</p></td>
</tr>
<tr class="even">
<td><p>Nenhum (notificação ou seleção)</p></td>
<td><p>HubTransport</p></td>
<td><p>RuleLoadFailureEventLogMonitor</p></td>
</tr>
<tr class="odd">
<td><p>Nenhum (notificação ou seleção)</p></td>
<td><p>HubTransport</p></td>
<td><p>RuleLoadSmallScaleFailureEventLogMonitor</p></td>
</tr>
<tr class="even">
<td><p>Nenhum (notificação ou seleção)</p></td>
<td><p>HubTransport</p></td>
<td><p>SmtpProxyEhloOptionsDoNotMatchContinueProxyingMonitor</p></td>
</tr>
<tr class="odd">
<td><p>Nenhum (notificação ou seleção)</p></td>
<td><p>HubTransport</p></td>
<td><p>SubmissionQueueMonitor</p></td>
</tr>
<tr class="even">
<td><p>Nenhum (notificação ou seleção)</p></td>
<td><p>HubTransport</p></td>
<td><p>TlsDomainClientCertificateSubjectMismatchMonitor</p></td>
</tr>
<tr class="odd">
<td><p>Nenhum (notificação ou seleção)</p></td>
<td><p>HubTransport</p></td>
<td><p>Total.Shadow.Queue.Length.Above.Threshold.Monitor</p></td>
</tr>
<tr class="even">
<td><p>Nenhum (notificação ou seleção)</p></td>
<td><p>HubTransport</p></td>
<td><p>TotalE2ELatencyHighForMSExchangeTransportMonitor</p></td>
</tr>
<tr class="odd">
<td><p>Nenhum (notificação ou seleção)</p></td>
<td><p>HubTransport</p></td>
<td><p>TotalE2ELatencyLowForMSExchangeTransportMonitor</p></td>
</tr>
<tr class="even">
<td><p>Nenhum (notificação ou seleção)</p></td>
<td><p>HubTransport</p></td>
<td><p>TotalE2ELatencyNormalForMSExchangeTransportMonitor</p></td>
</tr>
<tr class="odd">
<td><p>Nenhum (notificação ou seleção)</p></td>
<td><p>HubTransport</p></td>
<td><p>Transport.CatExpiry.Monitor</p></td>
</tr>
<tr class="even">
<td><p>Nenhum (notificação ou seleção)</p></td>
<td><p>HubTransport</p></td>
<td><p>Transport.Critical.Storage.Recovery.Failed.Monitor</p></td>
</tr>
<tr class="odd">
<td><p>Nenhum (notificação ou seleção)</p></td>
<td><p>HubTransport</p></td>
<td><p>Transport.DatabaseMoved.Monitor</p></td>
</tr>
<tr class="even">
<td><p>Nenhum (notificação ou seleção)</p></td>
<td><p>HubTransport</p></td>
<td><p>Transport.DomainSecureCert.Monitor</p></td>
</tr>
<tr class="odd">
<td><p>Nenhum (notificação ou seleção)</p></td>
<td><p>HubTransport</p></td>
<td><p>Transport.DomainSecureCertAuth.Monitor</p></td>
</tr>
<tr class="even">
<td><p>Nenhum (notificação ou seleção)</p></td>
<td><p>HubTransport</p></td>
<td><p>Transport.DomainSecureServerCertFailed.Monitor</p></td>
</tr>
<tr class="odd">
<td><p>Nenhum (notificação ou seleção)</p></td>
<td><p>HubTransport</p></td>
<td><p>Transport.DomainSecureServerDomainCertFailed.Monitor</p></td>
</tr>
<tr class="even">
<td><p>Nenhum (notificação ou seleção)</p></td>
<td><p>HubTransport</p></td>
<td><p>Transport.FailedToCreatePickupDirectory.Monitor</p></td>
</tr>
<tr class="odd">
<td><p>Nenhum (notificação ou seleção)</p></td>
<td><p>HubTransport</p></td>
<td><p>Transport.InvalidAcceptedDomain.Monitor</p></td>
</tr>
<tr class="even">
<td><p>Nenhum (notificação ou seleção)</p></td>
<td><p>HubTransport</p></td>
<td><p>Transport.LowDiskSpace.Monitor</p></td>
</tr>
<tr class="odd">
<td><p>Nenhum (notificação ou seleção)</p></td>
<td><p>HubTransport</p></td>
<td><p>Transport.Messages.Completing.Categorization.Monitor</p></td>
</tr>
<tr class="even">
<td><p>Nenhum (notificação ou seleção)</p></td>
<td><p>HubTransport</p></td>
<td><p>Transport.NDRForUnrestrictedLargeDL.Monitor</p></td>
</tr>
<tr class="odd">
<td><p>Nenhum (notificação ou seleção)</p></td>
<td><p>HubTransport</p></td>
<td><p>Transport.PickupDelete.Monitor</p></td>
</tr>
<tr class="even">
<td><p>Nenhum (notificação ou seleção)</p></td>
<td><p>HubTransport</p></td>
<td><p>Transport.PickupIsBadmailingFile.Monitor</p></td>
</tr>
<tr class="odd">
<td><p>Nenhum (notificação ou seleção)</p></td>
<td><p>HubTransport</p></td>
<td><p>Transport.SendConn.AuthKerb.Monitor</p></td>
</tr>
<tr class="even">
<td><p>Nenhum (notificação ou seleção)</p></td>
<td><p>HubTransport</p></td>
<td><p>Transport.SendConnAuth.Monitor</p></td>
</tr>
<tr class="odd">
<td><p>Nenhum (notificação ou seleção)</p></td>
<td><p>HubTransport</p></td>
<td><p>Transport.SendConnTLS.Monitor</p></td>
</tr>
<tr class="even">
<td><p>Nenhum (notificação ou seleção)</p></td>
<td><p>HubTransport</p></td>
<td><p>Transport.ServerCertExpireSoon.Monitor</p></td>
</tr>
<tr class="odd">
<td><p>Nenhum (notificação ou seleção)</p></td>
<td><p>HubTransport</p></td>
<td><p>Transport.ServerCertMismatch.Monitor</p></td>
</tr>
<tr class="even">
<td><p>Nenhum (notificação ou seleção)</p></td>
<td><p>HubTransport</p></td>
<td><p>Transport.ServiceStartError.Monitor</p></td>
</tr>
<tr class="odd">
<td><p>Nenhum (notificação ou seleção)</p></td>
<td><p>HubTransport</p></td>
<td><p>Transport.SmtpSendDirectTrustFailed.Monitor</p></td>
</tr>
<tr class="even">
<td><p>Nenhum (notificação ou seleção)</p></td>
<td><p>HubTransport</p></td>
<td><p>Transport.TemplateDoesNotExist.Monitor</p></td>
</tr>
<tr class="odd">
<td><p>Nenhum (notificação ou seleção)</p></td>
<td><p>HubTransport</p></td>
<td><p>Transport.TLSValidate.Monitor</p></td>
</tr>
<tr class="even">
<td><p>Nenhum (notificação ou seleção)</p></td>
<td><p>HubTransport</p></td>
<td><p>Transport.UnknownTemplateInPublishingLicense.Monitor</p></td>
</tr>
<tr class="odd">
<td><p>Nenhum (notificação ou seleção)</p></td>
<td><p>HubTransport</p></td>
<td><p>TransportCategorizerJobAvailabilityMonitor</p></td>
</tr>
<tr class="even">
<td><p>Nenhum (notificação ou seleção)</p></td>
<td><p>HubTransport</p></td>
<td><p>TransportDatabaseCorruptMonitor</p></td>
</tr>
<tr class="odd">
<td><p>Nenhum (notificação ou seleção)</p></td>
<td><p>HubTransport</p></td>
<td><p>TransportDeliveryFailures544Monitor</p></td>
</tr>
<tr class="even">
<td><p>Nenhum (notificação ou seleção)</p></td>
<td><p>HubTransport</p></td>
<td><p>TransportDeliveryFailuresDeliveryStoreDriver520Monitor</p></td>
</tr>
<tr class="odd">
<td><p>Nenhum (notificação ou seleção)</p></td>
<td><p>HubTransport</p></td>
<td><p>TransportLogGenerationCheckpointDepthMonitor</p></td>
</tr>
<tr class="even">
<td><p>Nenhum (notificação ou seleção)</p></td>
<td><p>HubTransport</p></td>
<td><p>TransportLogSearchLogPathInvalidMonitor</p></td>
</tr>
<tr class="odd">
<td><p>Nenhum (notificação ou seleção)</p></td>
<td><p>HubTransport</p></td>
<td><p>TransportMaxLocalLoopCountMonitor</p></td>
</tr>
<tr class="even">
<td><p>Nenhum (notificação ou seleção)</p></td>
<td><p>HubTransport</p></td>
<td><p>TransportPickupReadMonitor</p></td>
</tr>
<tr class="odd">
<td><p>Nenhum (notificação ou seleção)</p></td>
<td><p>HubTransport</p></td>
<td><p>TransportPoisonMessageMonitor</p></td>
</tr>
<tr class="even">
<td><p>Nenhum (notificação ou seleção)</p></td>
<td><p>HubTransport</p></td>
<td><p>TransportRejectingMessageSubmissionsMonitor</p></td>
</tr>
<tr class="odd">
<td><p>Nenhum (notificação ou seleção)</p></td>
<td><p>HubTransport</p></td>
<td><p>TransportServerCertPersonalStoreMonitor</p></td>
</tr>
<tr class="even">
<td><p>Nenhum (notificação ou seleção)</p></td>
<td><p>HubTransport</p></td>
<td><p>UnreachableQueueMonitor</p></td>
</tr>
<tr class="odd">
<td><p>Nenhum (notificação ou seleção)</p></td>
<td><p>HubTransport</p></td>
<td><p>XProxyToTransientInvalidArgumentsMonitor</p></td>
</tr>
</tbody>
</table>


Para obter mais informações sobre sondas e monitores, consulte [Desempenho e a integridade do servidor](https://technet.microsoft.com/pt-br/library/jj150551\(v=exchg.150\)).

## Ação do usuário

É possível que o serviço recuperado depois que ele emitiu o alerta. Portanto, quando você recebe um alerta que especifica o conjunto de integridade **HubTransport** não está íntegro, primeiro verificar se o problema ainda existe. Se o problema existir, execute as ações de recuperação apropriadas descritas na seção a seguir.

## Verificar se o problema

1.  Identifique o nome do conjunto de integridade e o nome do servidor que são fornecidas no alerta.

2.  Os detalhes da mensagem fornecem informações sobre a causa exata do alerta. Na maioria dos casos, os detalhes da mensagem fornecem informações de solução de problemas suficientes para ajudar a identificar a causa raiz. Se os detalhes da mensagem não criptografados, faça o seguinte:
    
    1.  Abra o Shell de Gerenciamento do Exchange e execute o seguinte comando para recuperar os detalhes do conjunto de integridade que emitiu o alerta:
        
            Get-ServerHealth <server name> | ?{$_.HealthSetName -eq "<health set name>"}
        
        Por exemplo, para recuperar o **HubTransport** integridade definir detalhes sobre mailbox1.contoso.com, execute o seguinte comando:
        
            Get-ServerHealth mailbox1.contoso.com | ?{$_.HealthSetName -eq "HubTransport"}
    
    2.  Analise a saída para determinar o monitor que tenha reportado o erro do comando. O valor de **AlertValue** para o monitor que emitiu o alerta será **não íntegra**.
    
    3.  Execute novamente a sonda associada do monitor que está em estado não íntegro. Consulte a tabela na seção [Explanation](troubleshooting-activesync-health-set.md) para localizar a sondagem associada. Para fazer isso, execute o seguinte comando:
        
            Invoke-MonitoringProbe <health set name>\<probe name> -Server <server name> | Format-List
        
        Por exemplo, suponha que o monitor de falha é **ActiveQueueDrainFailureMonitor**. A sonda associada a esse monitor é **ActiveQueueDrainFailureProbe**. Para executar esse teste em mailbox1.contoso.com, execute o seguinte comando:
        
            Invoke-MonitoringProbe HubTransport\ActiveQueueDrainFailureProbe -Server mailbox1.contoso.com | Format-List
    
    4.  Na saída do comando, examine a seção de "Resultados" da sonda. Se o valor for **teve êxito**, o problema foi um erro transitório, e ele não existe mais.

