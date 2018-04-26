---
title: Solução de problemas de conjunto de integridade de Autodiscover.Protocol
TOCTitle: Solução de problemas de conjunto de integridade de Autodiscover.Protocol
ms:assetid: 06afdcc8-7920-4e88-b85a-98e67a19d221
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/ms.exch.scom.autodiscover.protocol(v=EXCHG.150)
ms:contentKeyID: 53275608
ms.date: 03/07/2017
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Solução de problemas de conjunto de integridade de Autodiscover.Protocol

 

_**Aplica-se a:**Exchange Server 2013_

_**Tópico modificado em:**2015-03-09_

O conjunto de integridade Autodiscover.Protocol monitora o protocolo de comunicações de Descoberta Automática no servidor de Caixa de Correio.

Se você receber um alerta especificando que Autodiscover.Protocol não está íntegro, isso indicará um problema que pode impedir os usuários de acessarem suas caixas de correio.

## Explicação

O serviço Autodiscover.Protocol é monitorado usando as seguintes sondas e monitores.


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
<td><p>AutodiscoverSelfTestProbe</p></td>
<td><p>Autodiscover.Protocol</p></td>
<td><p>Active Directory</p></td>
<td><p>AutodiscoverSelfTestMonitor</p></td>
</tr>
</tbody>
</table>


Para obter mais informações sobre sondas e monitores, consulte [Desempenho e a integridade do servidor](https://technet.microsoft.com/pt-br/library/jj150551\(v=exchg.150\)).

## Problemas comuns

Essa sonda pode falhar por um dos seguintes motivos:

  - O pool de aplicativos de Descoberta Automática (MSExchangeAutodiscoverAppPool) hospedado no servidor CAS (Acesso para Cliente monitorado) não está respondendo. Ou, o pool de aplicativos de Descoberta Automática hospedado em um ou mais servidores de Caixa de Correio não está respondendo.

  - Os controladores de domínio não estão respondendo.

## Ação do usuário

É possível que o serviço tenha se recuperado após a emissão do alerta. Portanto, quando você receber um alerta que especifica que o conjunto de integridade não está íntegro, primeiro verifique se o problema ainda existe. Se o problema existir, execute as ações de recuperação apropriadas descritas nas seções seguintes.

## Verificar se o problema ainda existe

1.  Identifique o nome do conjunto de integridade e o nome do servidor no alerta.

2.  Os detalhes da mensagem fornecem informações sobre a causa exata do alerta. Na maioria dos casos, os detalhes da mensagem fornecem informações sobre solução de problemas suficientes para identificar a causa raiz. Se os detalhes da mensagem não forem claros, faça o seguinte:
    
    1.  Abra o Shell de Gerenciamento do Exchange, e em seguida, execute o seguinte comando para recuperar os detalhes do conjunto de integridade que emitiu o alerta:
        
            Get-ServerHealth <server name> | ?{$_.HealthSetName -eq "<health set name>"}
        
        Por exemplo, para recuperar os detalhes do conjunto de integridade do Autodiscover.Protocol sobre server1.contoso.com, execute o seguinte comando:
        
            Get-ServerHealth server1.contoso.com | ?{$_.HealthSetName -eq "Autodiscover.Protocol"}
    
    2.  Verifique a saída do comando para determinar qual monitor relatou o erro. O valor **AlertValue** do monitor que emitiu o alerta será `Unhealthy`.
    
    3.  Execute novamente a sonda associada do monitor que está em estado não íntegro. Consulte a tabela na seção Explanation para encontrar a sonda associada. Para fazer isso, execute o seguinte comando:
        
            Invoke-MonitoringProbe <health set name>\<probe name> -Server <server name> | Format-List
        
        Por exemplo, suponha que o monitor com falha seja **AutodiscoverSelfTestMonitor**. A sonda associada a esse monitor é **AutodiscoverSelfTestProbe**. Para executar essa sonda em server1.contoso.com, execute o seguinte comando:
        
            Invoke-MonitoringProbe Autodiscover.Protocol\AutodiscoverSelfTestProbe -Server server1.contoso.com | Format-List
    
    4.  Na saída do comando, verifique o valor **Resultado** da sonda. Se o valor for **Êxito**, significa que o problema foi um erro transitório e não existe mais. Caso contrário, consulte as etapas de recuperação descritas nas seções seguintes.

## Ações de recuperação do AutodiscoverSelfTestProbe

Quando você recebe um alerta de um conjunto de integridade, a mensagem de email contém as seguintes informações:

  - Nome do servidor de Caixa de Correio que enviou o alerta

  - Nome do servidor de Caixa de Correio que está sendo monitorado

  - Hora e data em que o alerta ocorreu

  - Mecanismo de autenticação usado e informações de credenciais

  - Rastreamento de exceções completo do último erro, incluindo dados de diagnóstico e informações de cabeçalho HTTP específicas

Você pode usar as informações no rastreamento de exceções completo para ajudar a solucionar o problema. A exceção gerada pela sonda contém um Motivo da Falha que descreve por que a sonda falhou.

Para resolver esse problema, siga estas etapas:

1.  Revise os logs do protocolo nos servidores de Caixa de Correio. Por padrão, os arquivos de log de protocolo no servidor de Caixa de Correio estão localizados na pasta **\\Logging\\Autodiscover do *\<diretório de instalação do exchange server\>***.

2.  Crie uma conta de usuário de teste e faça logon no servidor de Caixa de Correio usando a conta de usuário de teste no endereço. Por exemplo, faça logon usando: https://*\<servername\>*:444/autodiscover/autodiscover.xml.
    
    Se o nome da conta de usuário de teste passar, um problema poderá afetar o servidor de caixa de correio que está hospedando a caixa de correio monitorada.

3.  Tente repetir as etapas anteriores usando uma conta de teste no servidor de Caixa de Correio.

4.  Verifique se há alertas no Conjunto de Integridade Autodiscover.Proxy que podem indicar um problema que afeta um servidor de Caixa de Correio específico. Para obter mais informações, consulte [Solução de problemas de conjunto de integridade de Autodiscover.Proxy](troubleshooting-autodiscover-proxy-health-set.md).

5.  Verifique a existência de alertas no Conjunto de integridade de Descoberta Automática que possam indicar um problema em servidores de Caixa de Correio específicos. Para obter mais informações, consulte [Solucionando problemas de integridade de descoberta automática definido](troubleshooting-autodiscover-health-set.md).

6.  Inicie o Gerenciador do IIS e conecte-se ao servidor de Caixa de Correio que está informando o problema. Verifique se o pool de aplicativos **MSExchangeAutodiscoverAppPool** está em execução no servidor de Caixa de Correio.

7.  No Gerenciador do IIS, clique em **Pools de Aplicativos** e recicle o pool de aplicativos **MSExchangeAutodiscoverAppPool** executando o seguinte comando a partir do Shell:
    
        %SystemRoot%\System32\inetsrv\Appcmd recycle MSExchangeAutodiscoverAppPool

8.  Execute novamente a sonda associada conforme mostrado na etapa 2c na seção Verifying the issue still exists.

9.  Se o problema ainda existir, recicle o serviço IIS usando o utilitário IISReset ou executando o seguinte comando:
    
        Iisreset /noforce

10. Execute novamente a sonda associada conforme mostrado na etapa 2c na seção Verifying the issue still exists.

11. Se o problema ainda existir, reinicie o servidor.

12. Após a reinicialização do servidor, execute novamente a sonda associada, conforme exibido na etapa 2c, na seção Verifying the issue still exists.

13. Se a sonda continuar a falhar, talvez você precise de ajuda para resolver esse problema. Contate um profissional do Suporte Microsoft para resolver esse problema. Para entrar em contato com um profissional do Suporte Microsoft, visite o [Centro de Soluções do Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=180809). No painel de navegação, clique em **Recursos e opções de suporte** e use uma das opções listadas em **Obter suporte técnico** para entrar em contato com um profissional do Suporte Microsoft. Como a sua organização pode ter um procedimento específico para entrar em contato diretamente os Serviços de Suporte a Produtos Microsoft, tenha certeza de consultar primeiro as diretrizes da sua organização.

## Para obter mais informações

[Novidades do Exchange 2013](https://technet.microsoft.com/pt-br/library/jj150540\(v=exchg.150\))

[Cmdlets do Exchange 2013](https://technet.microsoft.com/pt-br/library/bb124413\(v=exchg.150\))

