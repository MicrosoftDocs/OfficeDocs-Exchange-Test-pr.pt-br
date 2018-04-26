---
title: Como usar o Exchange Server 2013 Management Pack para a Solução de Problemas
TOCTitle: Como usar o Exchange Server 2013 Management Pack para a Solução de Problemas
ms:assetid: c9672dad-1e67-4f07-bad9-539a67f2ac70
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Dn195913(v=EXCHG.150)
ms:contentKeyID: 53275646
ms.date: 08/29/2014
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Como usar o Exchange Server 2013 Management Pack para a Solução de Problemas

 

_**Tópico modificado em:** 2013-04-09_

O [Introdução ao Pacote de Gerenciamento do Exchange Server 2013](getting-started-with-exchange-server-2013-management-pack.md) fornece uma visão geral do painel do pacote de gerenciamento. Este tópico fornece as orientações sobre como ele pode te ajudar a solucionar um problema. Ilustra-se o processo melhor por meio de um exemplo. Considere o seguinte cenário:

Sérgio Oliveira é um administrador do Exchange na Contoso. Ele abre um Console SCOM e clica na **Integridade do servidor** no painel do Exchange Server 2013 para verificar o status dos servidores Exchange. Ele percebe o estado crítico dos **Componentes de serviço** em um de seus servidores CAS.

![Servidor CAS com falha](images/Dn195913.32a265d9-68e0-4d8c-9f83-1d10cdda1f84(EXCHG.150).png "Servidor CAS com falha")

O Sérgio clica duas vezes no servidor que abre a janela **Gerenciador de Integridade**. Nesta janela, ele pode ver que a componente de serviço que está em um estado não íntegro é o conjunto de integridade OWA.Proxy. Ele clique nele para ver as informações relevantes deste conjunto de saúde.

![Detalhes de healthset do servidor CAS com falha](images/Dn195913.8e4d05a6-9128-40d8-b262-e60e9affc973(EXCHG.150).png "Detalhes de healthset do servidor CAS com falha")

O link fornecido Recursos de Conhecimento Externos leva Sérgio para o tópico [Solução de problemas do conjunto de integridade OWA.Proxy](https://technet.microsoft.com/pt-br/library/jj737712\(v=exchg.150\)). Neste artigo, Sérgio vê que a primeira coisa a fazer é verificar se o problema ainda existe. Seguindo as instruções, ele executa o seguinte comando para verificar o estado atual do conjunto de integridade do OWA.Proxy definido no Shell:

    Get-ServerHealth Server1.contoso.com | ?{$_.HealthSetName -eq "OWA.Proxy"}

Executar esse comando lhe dá a seguinte saída:

    Server          State           Name                 TargetResource       HealthSetName   AlertValue ServerComp
                                                                                                         onent
    ------          -----           ----                 --------------       -------------   ---------- ----------
    Server1         Online          OWAProxyTestMonitor  MSExchangeOWAAppPool OWA.Proxy       Unhealthy  OwaProxy
    Server1         Online          OWAProxyTestMonitor  MSExchangeOWACale... OWA.Proxy       Healthy    OwaProxy

Sérgio vê que o problema está no pool de aplicativos OWA. A próxima etapa é executar novamente a sonda associada do monitor que está em estado não íntegro. Usando a tabela no tópico "Solução de problemas do Conjunto de Integridade do OWA.Proxy", ele determina que a sonda que precisa ser executada novamente é OWAProxyTestProbe. Ele executa o seguinte comando:

    Invoke-MonitoringProbe OWA.Proxy\OWAProxyTestProbe -Server Server1.contoso.com | Format-List

Ele verifica a saída do valor ResultType e vê que a sonda falhou:

    ResultType : Failed

Ele procede para a seção “Ações de recuperação de OWAProxyTestMonitor” do artigo. Ele se conecta ao Server1 usando o Gerenciador do IIS para ver se o MSExchangeOWAAppPool está sendo executado no Servidor do IIS. Depois de verificar se ele está funcionando, a próxima etapa diz para Sérgio reciclar o MSExchangeOWAAppPool:

    C:\Windows\System32\Inetsrv\Appcmd recycle APPPOOL MSExchangeOWAAppPool

Depois de ver que o MSExchangeOWAAppPool foi reciclado com êxito, ele continua verificando se o problema ainda existe executando novamente a sonda usando o cmdlet Invoke-MonitoringProbe e dessa vez ele vê que o resultado teve êxito. Então ele executa o seguinte comando para verificar se o conjunto de integridade está relatando o status **Íntegro** novamente:

    Get-ServerHealth Server1.contoso.com | ?{$_.HealthSetName -eq "OWA.Proxy"}

Dessa vez ele vê que o problema foi resolvido.

    Server          State           Name                 TargetResource       HealthSetName   AlertValue ServerComp
                                                                                                         onent
    ------          -----           ----                 --------------       -------------   ---------- ----------
    Server1         Online          OWAProxyTestMonitor  MSExchangeOWAAppPool OWA.Proxy       Healthy    OwaProxy
    Server1         Online          OWAProxyTestMonitor  MSExchangeOWACale... OWA.Proxy       Healthy    OwaProxy

Ele volta ao console SCOM e verifica se o problema foi resolvido.

![Integridade do Servidor](images/Dn195908.c863be83-fc4b-4daf-a18b-27b1aae15b1d(EXCHG.150).png "Integridade do Servidor")

A situação abordada acima é uma simples demonstração do fluxo de trabalho de solução de problemas, quando você vê um alerta no console SCOM. Mesmo que os detalhes possam variar, normalmente se segue um fluxo de trabalho de solução de problemas semelhante para cada problema relatado no console.

