---
title: Solucionando problemas de integridade de descoberta automática definido
TOCTitle: Solucionando problemas de integridade de descoberta automática definido
ms:assetid: bc933621-df73-4d1d-bdef-825b98be8e09
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/ms.exch.scom.autodiscover(v=EXCHG.150)
ms:contentKeyID: 53275634
ms.date: 03/07/2017
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Solucionando problemas de integridade de descoberta automática definido

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2015-03-09_

O conjunto de integridade de descoberta automática monitora a integridade geral do serviço Descoberta automática para clientes.

Se você receber um alerta que especifica a descoberta automática não está íntegra, isso indica um problema que pode impedir que os usuários acessem suas caixas de correio usando o processo de descoberta automática.

## Explicação

O serviço Descoberta automática é monitorado usando as seguintes sondas e monitores.


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
<td><p>AutodiscoverCtpProbe</p></td>
<td><p>Descoberta Automática</p></td>
<td><p>Active Directory</p></td>
<td><p>AutodiscoverCtpMonitor</p></td>
</tr>
</tbody>
</table>


Para obter mais informações sobre sondas e monitores, consulte [Desempenho e a integridade do servidor](https://technet.microsoft.com/pt-br/library/jj150551\(v=exchg.150\)).

## Problemas comuns

Essa sonda pode falhar por um dos seguintes motivos:

  - O pool de aplicativos de descoberta automática (MSExchangeAutodiscoverAppPool) que está hospedado no servidor de acesso para cliente monitorado (CAS) não está respondendo. Ou então, o pool de aplicativos de descoberta automática que está hospedado em um ou mais servidores de caixa de correio não está respondendo.

  - O CAS está com problemas de rede e não consegue se conectar ao servidor de caixa de correio ou controlador de domínio.

  - As credenciais de conta de monitoramento não estão corretas.

  - Os controladores de domínio não estão respondendo.

## Ação do usuário

É possível que o serviço recuperado depois que ele emitiu o alerta. Portanto, quando você recebe um alerta que especifica o conjunto de integridade não está íntegro, primeiro verificar se o problema ainda existe. Se o problema existir, execute as ações de recuperação apropriadas descritas nas seções a seguir.

## Verificar se o problema ainda existe

1.  Identifique o nome do conjunto de integridade e o nome do servidor no alerta.

2.  Os detalhes da mensagem fornecem informações sobre a causa exata do alerta. Na maioria dos casos, os detalhes da mensagem fornecem informações sobre solução de problemas suficientes para identificar a causa raiz. Se os detalhes da mensagem não forem claros, faça o seguinte:
    
    1.  Abra o Shell de Gerenciamento do Exchange e execute o seguinte comando para recuperar os detalhes do conjunto de integridade que emitiu o alerta:
        
            Get-ServerHealth <server name> | ?{$_.HealthSetName -eq "<health set name>"}
        
        Por exemplo, para recuperar a descoberta automática integridade definir detalhes sobre Server1. contoso.com, execute o seguinte comando:
        
            Get-ServerHealth server1.contoso.com | ?{$_.HealthSetName -eq "Autodiscover"}
    
    2.  Analise a saída para determinar o monitor que tenha reportado o erro do comando. O valor de **AlertValue** para o monitor que emitiu o alerta é `Unhealthy`.
    
    3.  Execute novamente a sonda associada do monitor que está em estado não íntegro. Consulte a tabela na seção Explanation para localizar a sondagem associada. Para fazer isso, execute o seguinte comando:
        
            Invoke-MonitoringProbe <health set name>\<probe name> -Server <server name> | Format-List
        
        Por exemplo, suponha que o monitor de falha é **AutodiscoverCtpMonitor**. A sonda associada a esse monitor é **AutodiscoverCtpProbe**. Para executar essa sonda em Server1, execute o seguinte comando:
        
            Invoke-MonitoringProbe Autodiscover\AutodiscoverCtpProbe -Server server1.contoso.com | Format-List
    
    4.  Na saída do comando, verifique o valor **Resultado** da sonda. Se o valor for **Êxito**, significa que o problema foi um erro transitório e não existe mais. Caso contrário, consulte as etapas de recuperação descritas nas seções seguintes.

## Ações de recuperação de AutodiscoverCtpMonitor

Quando você recebe um alerta de um conjunto de integridade, a mensagem de email contém as seguintes informações:

  - Nome do servidor que enviou o alerta

  - Nome do servidor de caixa de correio que foi a sonda de monitoramento

  - Hora e data em que o alerta ocorreu

  - Mecanismo de autenticação usado e informações de credenciais

  - Rastreamento de exceções completo do último erro, incluindo dados de diagnóstico e informações de cabeçalho HTTP específicas

Você pode usar as informações no rastreamento de exceções completo para ajudar a solucionar o problema. A exceção gerada pela sonda contém um motivo da falha que descreve por que o teste falhou. Por exemplo, o motivo da falha pode ser um destes procedimentos:

  - **X-FEServer**   Indica em qual CAS a sonda foi executada

  - **X-CalculatedBETarget**   Indica o servidor de caixa de correio para o qual a solicitação é roteada

  - **X-DiagInfo**   Indica o servidor de caixa de correio que recebeu a solicitação

Para resolver esse problema, siga estas etapas:

1.  Examine os logs de protocolo nos servidores de CA e de caixa de correio. Por padrão, os logs de protocolo NAS CAS estão localizados na pasta ***\<exchange server installation directory\>*\\Logging\\HttpProxy\\Autodiscover** . Por padrão, os arquivos de log do protocolo no servidor de caixa de correio estão localizados na pasta ***\<exchange server installation directory\>*\\Logging\\Autodiscover** .

2.  Crie uma conta de usuário de teste e, em seguida, faça logon no CAS usando a conta de usuário de teste. Por exemplo, faça logon usando: https://*\<servername\>*/autodiscover/autodiscover.xml.
    
    Se os passos de nome de conta de usuário de teste, um problema podem afetar o servidor de caixa de correio que está hospedando a caixa de correio monitorada.
    
    Tente repetir as etapas anteriores, usando uma conta de teste no servidor de caixa de correio. Se essa tentativa falhar, tente executar o teste contra um CAS diferente para verificar se o problema está ocorrendo em um CAS específico e não no servidor caixa de correio.

3.  Verificar a conectividade de rede entre os servidores de CA e de caixa de correio. Use o ping.exe para verificar se cada servidor está respondendo.

4.  Verifique se há alertas no Conjunto de Integridade Autodiscover.Proxy que podem indicar um problema que afeta um servidor de Caixa de Correio específico. Para obter mais informações, consulte [Solução de problemas de conjunto de integridade de Autodiscover.Proxy](troubleshooting-autodiscover-proxy-health-set.md).

5.  Verifique se há alertas no Autodiscover.Protocol conjunto de integridade que pode indicar um problema que afeta os servidores de caixa de correio específicas. Para obter mais informações, consulte [Solução de problemas de conjunto de integridade de Autodiscover.Protocol](troubleshooting-autodiscover-protocol-health-set.md).

6.  Inicie o Gerenciador do IIS e conecte-se ao servidor que está relatando o problema. Verifique se que o pool de aplicativos **MSExchangeAutodiscoverAppPool** esteja em execução nos servidores de CA e de caixa de correio.

7.  No Gerenciador do IIS, clique em **Pools de Aplicativos** e recicle o pool de aplicativos **MSExchangeAutodiscoverAppPool** executando o seguinte comando a partir do Shell:
    
        %SystemRoot%\System32\inetsrv\Appcmd recycle MSExchangeAutodiscoverAppPool

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

