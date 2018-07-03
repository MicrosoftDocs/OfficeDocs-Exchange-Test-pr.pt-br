---
title: RPS da solução de problemas. Conjunto de integridade de proxy
TOCTitle: RPS da solução de problemas. Conjunto de integridade de proxy
ms:assetid: a5058323-5d86-438a-ad4a-fa4292310e98
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/ms.exch.scom.rps.proxy(v=EXCHG.150)
ms:contentKeyID: 53275622
ms.date: 03/07/2017
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# RPS da solução de problemas. Conjunto de integridade de proxy

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2015-03-09_

O número de RPS. Conjunto de integridade do proxy monitora a integridade geral do serviço do PowerShell remoto.

Se você receber um alerta especificando que o RPS. Proxy não está íntegro, que isso indica um problema que pode impedir que você usando o PowerShell remoto para acessar Exchange.

## Explicação

O serviço RPS é monitorado usando as seguintes sondas e monitores:


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
<td><p>RPSProxyTestProbe</p></td>
<td><p>RPS.Proxy</p></td>
<td><p>Active Directory</p></td>
<td><p>RPSProxyTestMonitor</p></td>
</tr>
</tbody>
</table>


Para obter mais informações sobre sondas e monitores, consulte [Desempenho e a integridade do servidor](https://technet.microsoft.com/pt-br/library/jj150551\(v=exchg.150\)).

## Problemas comuns

Quando esse teste falha pode haver vários motivos para que o problema. Alguns dos problemas mais comuns incluem o seguinte:

  - O pool de aplicativos que está hospedado no servidor CAS monitorado não está funcionando corretamente.

  - As credenciais de conta de monitoramento não estão corretas.

  - Os controladores de domínio não estão respondendo.

## Ação do usuário

É possível que o serviço foi capaz de recuperar após emitir um alerta. Portanto, quando você recebe um alerta que especifica o conjunto de integridade não está íntegro, a primeira coisa que você deve fazer é verificar se o problema ainda existe. Se contiver, em seguida, execute as ações de recuperação apropriadas descritas nas seções a seguir.

## Verificar se o problema ainda existe

1.  Identifique o nome do conjunto de integridade e o nome do servidor no alerta.

2.  Os detalhes da mensagem fornecem informações sobre o que causou exatamente o alerta a ser gerado. Na maioria dos casos, os detalhes da mensagem seriam fornecem informações de solução de problemas suficientes para identificar a causa raiz. Se os detalhes da mensagem não criptografados, faça o seguinte:
    
    1.  Abra o Shell de gerenciamento do Exchange e execute o seguinte comando para recuperar os detalhes do conjunto de integridade que emitiu o alerta:
        
            Get-ServerHealth <server name> | ?{$_.HealthSetName -eq "<health set name>"}
        
        Por exemplo, para recuperar o RPS. Detalhes do conjunto de integridade de proxy em Server1, execute o seguinte comando:
        
            Get-ServerHealth server1.contoso.com | ?{$_.HealthSetName -eq "RPS.Proxy"}
    
    2.  Analise a saída do comando e determinar o monitor que tenha reportado o erro. O **AlertValue** para o monitor que emitiu o alerta lerá `Unhealthy`.
    
    3.  Execute novamente a sonda associada para o monitor que está no estado íntegro. Consulte a tabela na seção explicação para encontrar a sonda associada. Para fazer isso, execute o seguinte comando:
        
            Invoke-MonitoringProbe <health set name>\<probe name> -Server <server name> | Format-List
        
        Por exemplo, vamos supor que o monitor está falhando foi **RPSProxyTestMonitor**. A sonda associada a esse monitor é **RPSProxyTestProbe**. Para executar essa sonda no servidor Server1, execute o seguinte comando:
        
            Invoke-MonitoringProbe RPS.Proxy\RPSProxyTestProbe -Server server1.contoso.com | Format-List
    
    4.  Na saída do comando, revise o **resultado** da sonda. Se o valor for **teve êxito**, o problema foi um erro transitório e não existe mais. Caso contrário, consulte as etapas de recuperação descritas nas seções a seguir.

## Ações de recuperação de RPSProxyTestMonitor

Ao receber um alerta de um conjunto de integridade, o email conterá as informações a seguir:

  - O nome do servidor CAS que enviou o alerta.

  - Rastreamento de exceções completo incluindo eroor mensagens, dados de diagnóstico e informações de cabeçalho HTTP específicas. As informações no rastreamento completo da exceção podem ser usadas para ajudar a solucionar o problema.

  - A hora e data que o problema ocorreu.

Para ajudar a solucionar esse problema, execute o seguinte procedimento:

1.  Examine os logs de protocolo em servidores CAS. Logs de protocolo estão localizados na pasta *\<exchange server installation directory\>*\\Logging\\HttpProxy*\\\<protocol\>* o servidor CAS.

2.  Criar uma conta de usuário de teste e, em seguida, logon para o servidor CAS usando a conta de usuário de teste, por exemplo o https:// *\<servername\>*/owa

3.  Inicie o Gerenciador do IIS e conecte-se ao servidor que está relatando o problema e verifique se o MSExchangePowerShellFrontEndAppPool está em execução no servidor CAS.

4.  Clique em **Pools de aplicativos** e recicle o pool de aplicativos **MSExchangePowerShellFrontEndAppPool** executando o seguinte comando do Shell de gerenciamento do Exchange:
    
        %SystemRoot%\System32\inetsrv\Appcmd recycle MSExchangePowerShellFrontEndAppPool

5.  Execute novamente a sonda associada conforme mostrado na etapa 2.c. na seção Verifying o problema ainda existir .

6.  Se o problema ainda existir, recicle o serviço do IIS usando o utilitário IISReset.

7.  Execute novamente a sonda associada conforme mostrado na etapa 2.c. na seção Verifying o problema ainda existir .

8.  Se o problema ainda existir, reinicie o servidor.

9.  Depois que o servidor for reiniciado, execute novamente a sonda associada conforme mostrado na etapa 2.c. na seção Verifying o problema ainda existir .

10. Se a sonda continua a falhar, talvez você precise de ajuda para resolver esse problema. Contate um profissional do Suporte Microsoft para resolver esse problema. Para entrar em contato com um profissional do Suporte Microsoft, visite o [Centro de Soluções do Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=180809). No painel de navegação, clique em **Recursos e opções de suporte** e use uma das opções listadas em **Obter suporte técnico** para entrar em contato com um profissional do Suporte Microsoft. Como a sua organização pode ter um procedimento específico para entrar em contato diretamente os Serviços de Suporte a Produtos Microsoft, tenha certeza de consultar primeiro as diretrizes da sua organização.

## Para obter mais informações

[Novidades do Exchange 2013](https://technet.microsoft.com/pt-br/library/jj150540\(v=exchg.150\))

[Cmdlets do Exchange 2013](https://technet.microsoft.com/pt-br/library/bb124413\(v=exchg.150\))

