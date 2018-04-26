---
title: Solucionando problemas de EWS. Conjunto de integridade de protocolo
TOCTitle: Solucionando problemas de EWS. Conjunto de integridade de protocolo
ms:assetid: 826b2d5b-adbb-4bf5-94b6-0a8de2e3aac0
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/ms.exch.scom.ews.protocol(v=EXCHG.150)
ms:contentKeyID: 53275614
ms.date: 03/07/2017
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Solucionando problemas de EWS. Conjunto de integridade de protocolo

 

_**Aplica-se a:**Exchange Server 2013, Project Server 2013_

_**Tópico modificado em:**2015-03-09_

O EWS. Conjunto de integridade do protocolo monitora Exchange protocolo de comunicação de serviços da Web (EWS) no servidor de caixa de correio. O EWS. Conjunto de integridade do protocolo está relacionado aos seguintes conjuntos de integridade:

[Solução de problemas do conjunto de integridade EWS](troubleshooting-ews-health-set.md)

[Solucionando problemas de EWS. Conjunto de integridade de proxy](troubleshooting-ews-proxy-health-set.md)

Se você receber um alerta que especifica que o EWS. Protocolo não está íntegro, que isso indica um problema que pode impedir que os usuários acessem Exchange.

## Explicação

O EWS. Conjunto de integridade do protocolo é composto os testes a seguintes:

1.  EwsSelfTestProbe

2.  EwsDeepTestProbe

O EwsSelfTestProbe não depende do armazenamento de informações. No entanto, a sonda EwsDeepTestProbe depende do armazenamento de informações. Ambas estes testes realizar operações de EWS no servidor de caixa de correio e usarem o mesmo método de autenticação como um servidor de acesso para cliente (CAS). EwsSeftTestProbe chama o método **ConvertId** e EwsDeepTestProbe chama o método **GetFolder** .


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
<td><p>EwsSelfTestProbe</p></td>
<td><p>EWS.Protocol</p></td>
<td><p>Active Directory</p></td>
<td><p>EWSSelfTestMonitor</p></td>
</tr>
<tr class="even">
<td><p>EwsDeepTestProbe</p></td>
<td><p>EWS.Protocol</p></td>
<td><p>Repositório de Informações</p></td>
<td><p>EWSDeepTestMonitor</p></td>
</tr>
</tbody>
</table>


Para obter mais informações sobre sondas e monitores, consulte [Desempenho e a integridade do servidor](https://technet.microsoft.com/pt-br/library/jj150551\(v=exchg.150\)).

Quando você recebe um alerta deste HealthSet, a mensagem de email contém as seguintes informações:

1.  Nome do servidor de caixa de correio no qual origem do alerta

2.  Rastreamento de exceções completo do último erro, incluindo dados de diagnóstico e informações específicas de cabeçalhos HTTP

3.  Hora em que o incidente ocorreu

## Problemas comuns

Essa sonda pode falhar por um dos seguintes motivos:

  - O pool de aplicativos do EWS no servidor de caixa de correio monitorado não está funcionando corretamente.

  - Os controladores de domínio não estão respondendo ou eles não podem se comunicar com o servidor de caixa de correio.

  - O banco de dados do usuário não está montado ou o Repositório de Informações está indisponível para uma caixa de correio específica.

## Ação do usuário

É possível que o serviço tenha se recuperado após a emissão do alerta. Portanto, quando você receber um alerta que especifica que o conjunto de integridade não está íntegro, primeiro verifique se o problema ainda existe. Se o problema existir, execute as ações de recuperação apropriadas descritas nas seções seguintes.

## Verificar se o problema ainda existe

1.  Identifique o nome do conjunto de integridade e o nome do servidor no alerta.

2.  Os detalhes da mensagem fornecem informações sobre a causa exata do alerta. Na maioria dos casos, os detalhes da mensagem fornecem informações sobre solução de problemas suficientes para identificar a causa raiz. Se os detalhes da mensagem não forem claros, faça o seguinte:
    
    1.  Abra o Shell de Gerenciamento do Exchange, e em seguida, execute o seguinte comando para recuperar os detalhes do conjunto de integridade que emitiu o alerta:
        
            Get-ServerHealth <server name> | ?{$_.HealthSetName -eq "<health set name>"}
        
        Por exemplo, para recuperar o EWS. O conjunto de integridade de protocolo detalhes sobre Server1. contoso.com, execute o seguinte comando:
        
            Get-ServerHealth server1.contoso.com | ?{$_.HealthSetName -eq "EWS.Protocol"}
    
    2.  Verifique a saída do comando para determinar qual monitor relatou o erro. O valor **AlertValue** do monitor que emitiu o alerta será `Unhealthy`.
    
    3.  Execute novamente a sonda associada do monitor que está em estado não íntegro. Consulte a tabela na seção Explanation para localizar a sonda associada. Para fazer isso, execute o seguinte comando:
        
            Invoke-MonitoringProbe <health set name>\<probe name> -Server <server name> | Format-List
        
        Por exemplo, suponha que o monitor de falha é **EWSSelfTestMonitor**. A sonda associada a esse monitor é **EWSSelfTestProbe**. Para executar essa sonda em Server1, execute o seguinte comando:
        
            Invoke-MonitoringProbe EWS.Protocol\EWSSelfTestProbe -Server server1.contoso.com | Format-List
    
    4.  Na saída do comando, verifique o valor **Resultado** da sonda. Se o valor for **Êxito**, significa que o problema foi um erro transitório e não existe mais. Caso contrário, consulte as etapas de recuperação descritas nas seções seguintes.

## Ações de recuperação de EWSDeepTestMonitor e EWSSelfTestMonitor

Esse alerta monitor geralmente é emitida para servidores de caixa de correio.

1.  Inicie o Gerenciador do IIS e conecte-se ao servidor que está relatando o problema para determinar se o MSExchangeServicesAppPool está sendo executado em servidores de CA e de caixa de correio.

2.  Localize o MailboxDatabase para os testes com falha e, em seguida, verifique se que o MailboxDatabase está ativo para o MailboxServer e que o repositório de informações está íntegro.

3.  Clique em **Pools de Aplicativos** e recicle o pool de aplicativos **MSExchangeServicesAppPool** executando o seguinte comando a partir do Shell:
    
        %SystemRoot%\System32\inetsrv\Appcmd recycle MSExchangeServicesAppPool

4.  Execute novamente a sonda associada conforme mostrado na etapa 2c na seção Verifying the issue still exists.

5.  Se o problema ainda existir, reinicie o serviço do IIS usando o utilitário IISReset.

6.  Execute novamente a sonda associada conforme mostrado na etapa 2c na seção Verifying the issue still exists.

7.  Se o problema ainda for encerrado, revise os arquivos de log do protocolo no servidor de caixa de correio. No servidor de caixa de correio, os logs residem na pasta \\Logging\\Ews *\<exchange server installation directory\>*.

8.  Criar uma conta de usuário de teste e faça logon usando a conta de usuário de teste com base no servidor de caixa de correio determinado na porta 444 https://*\<servername\>*: 444/ews/exchange.asmx. Se o teste for bem-sucedido, um problema pode afetar o banco de dados de caixa de correio específica ou o servidor de caixa de correio no qual a caixa de correio de monitoramento está localizada. Tente Repita essa etapa usando uma conta de teste no banco de dados.

9.  Verifique qualquer alerta no EWS. Protocolo de integridade definido que possa indicar um problema que afeta o servidor de caixa de correio específico.

10. Se o problema ainda existir, reinicie o servidor. Para fazer isso, o failover primeiro os bancos de dados hospedados no servidor usando o seguinte comando:
    
        Set-MailboxServer server1.contoso.com -DatabaseCopyActivationDisabledAndMoveNow $true
    
    Neste e em todos os exemplos de código subsequentes, substitua *server1.contoso.com* pelo nome real do servidor.

11. Verifique se todos os bancos de dados foram removidos do servidor que está relatando o problema. Para fazer isso, execute o seguinte comando:
    
        Get-MailboxDatabaseCopyStatus -Server server1.contoso.com | Group Status
    
    Se a saída do comando não mostrar nenhuma cópia ativa no servidor, o servidor é salvar a reinicialização. Reinicie o servidor.

12. Depois que o servidor reiniciar, execute novamente a sondagem associada como mostrado na etapa 2c na seção Verifying the issue still exists.

13. Se a investigação for bem sucedida, faça failover dos bancos de dados executando o seguinte comando:
    
        Set-MailboxServer server1.contoso.com -DatabaseCopyActivationDisabledAndMoveNow $false

14. Se a sonda continuar falhando, você pode precisar de ajuda para solucionar o problema. Contate um profissional do Suporte Microsoft para resolver esse problema. Para entrar em contato com um profissional do Suporte Microsoft, visite o [Centro de Soluções do Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=180809). No painel de navegação, clique em **Recursos e opções de suporte** e use uma das opções listadas em **Obter suporte técnico** para entrar em contato com um profissional do Suporte Microsoft. Como a sua organização pode ter um procedimento específico para entrar em contato diretamente os Serviços de Suporte a Produtos Microsoft, tenha certeza de consultar primeiro as diretrizes da sua organização.

## Para obter mais informações

[Novidades do Exchange 2013](https://technet.microsoft.com/pt-br/library/jj150540\(v=exchg.150\))

