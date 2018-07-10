---
title: Solucionando problemas de integridade SiteMailbox definido
TOCTitle: Solucionando problemas de integridade SiteMailbox definido
ms:assetid: ac00985c-c9a5-44bf-b152-4b99d8ae24ed
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/ms.exch.scom.sitemailbox(v=EXCHG.150)
ms:contentKeyID: 53275629
ms.date: 03/07/2017
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Solucionando problemas de integridade SiteMailbox definido

 

_**Aplica-se a:** Exchange Server 2013, Project Server 2013_

_**Tópico modificado em:** 2013-02-11_

O conjunto de integridade SiteMailbox monitora a integridade geral e a acessibilidade as caixas de correio de site em sua organização.

Se você receber um alerta que especifica a SiteMailbox não está íntegro, isto indica que o conteúdo da caixa de correio de um usuário não está em um estado sincronizado.

## Explicação

O sistema de monitoramento de SiteMailbox recebe resultados passiva de sincronização do serviço de sincronização de plano de fundo. Este sistema não usa qualquer investigações. Os resultados de sincronização passivos são gravados o SiteMailbox sistema de monitoramento após cada tentativa de sincronização. Sincronizações também são acionadas quando os seguintes eventos ocorrer:

  - Os usuários acessar suas caixas de correio de site usando Outlook ou Outlook Web App

  - Executar o comando **Update-SiteMailbox**

  - Abra a janela de opções Outlook Web App e clique no botão **Iniciar sincronização** na página **Status de sincronização** para a caixa de correio de site selecionado

Para obter mais informações sobre o cmdlet Update-SiteMailbox, consulte: [Update-SiteMailbox](https://technet.microsoft.com/pt-br/library/jj218690\(v=exchg.150\))

Para obter mais informações sobre sondas e monitores, consulte [Desempenho e a integridade do servidor](https://technet.microsoft.com/pt-br/library/jj150551\(v=exchg.150\)).

## Problemas comuns

O serviço de monitoramento de sincronização geralmente dispara um alerta quando ocorrerem problemas de sincronização de todo o site de difusão. Um alerta não será enviado quando uma caixa de correio de site único falha sincronizar. Para determinar a causa de um acima do limite de alerta para uma caixa de correio de site único, recomendamos que você examine os arquivos de log de sincronização de caixa de correio do site.

## Ação do usuário

É possível que o serviço tenha se recuperado após a emissão do alerta. Portanto, quando você receber um alerta que especifica que o conjunto de integridade não está íntegro, primeiro verifique se o problema ainda existe. Se o problema existir, execute as ações de recuperação apropriadas descritas nas seções seguintes.

## Verificar se o problema ainda existe

1.  Identifique o nome do conjunto de integridade e o nome do servidor no alerta.

2.  Os detalhes da mensagem fornecem informações sobre a causa exata do alerta. Na maioria dos casos, os detalhes da mensagem fornecem informações sobre solução de problemas suficientes para identificar a causa raiz. Se os detalhes da mensagem não forem claros, faça o seguinte:
    
    1.  Abra o Shell de Gerenciamento do Exchange, e em seguida, execute o seguinte comando para recuperar os detalhes do conjunto de integridade que emitiu o alerta:
        
            Get-ServerHealth <server name> | ?{$_.HealthSetName -eq "<health set name>"}
        
        Por exemplo, para recuperar o SiteMailbox integridade definir detalhes sobre Server1. contoso.com, execute o seguinte comando:
        
            Get-ServerHealth server1.contoso.com | ?{$_.HealthSetName -eq "SiteMailbox"}
    
    2.  Verifique a saída do comando para determinar qual monitor relatou o erro. O valor **AlertValue** do monitor que emitiu o alerta será `Unhealthy`.

## Etapas para a solução de problemas

Quando você recebe um alerta de um conjunto de integridade, a mensagem de email contém as seguintes informações:

  - Nome do servidor que enviou o alerta

  - Hora e data em que o alerta ocorreu

  - Mecanismo de autenticação usado e informações de credenciais

  - Rastreamento de exceções completo do último erro, incluindo dados de diagnóstico e informações de cabeçalho HTTP específicas  
    
    **Observação**   Você pode usar as informações no rastreamento de exceções completo para ajudar a solucionar o problema. A exceção gerada pela sonda contém um Motivo da Falha que descreve por que a sonda falhou.

**Erros de sincronização do plano de fundo**

Quando o processo de sincronização do plano de fundo falha, você pode receber um alerta que é semelhante ao seguinte:

A sincronização de plano de fundo da caixa de correio de Site está falhando pelo menos 25%: 41 falhas sem 87 tentativas. Resultado da sincronização de amostra:

\[Mensagem: O servidor remoto retornou um erro: (401) não autorizado.\] \[Type:System.Net.WebException\]

Esse alerta é acionado quando uma porcentagem consistentemente alta de falhas ocorreram durante o horário de quatro anterior de sincronização. Para evitar falsos negativos, um alerta será enviado apenas quando as seguintes condições são atendidas em uma janela de 15 minutos durante o horário de quatro anterior:

  - Ocorrem falhas de pelo menos 20 em uma janela de 15 minutos.

  - A porcentagem de falhas em comparação ao total de tentativas de exceder 25% em uma janela de 15 minutos.

Cada caixa de correio de site no Exchange é vinculada a um site SharePoint. Para cada uma das caixas de correio de site em um servidor determinado Exchange que está hospedando a função caixa de correio, o servidor sincroniza informações relacionadas a caixa de correio de site de SharePoint.

Dois tipos de sincronizações ocorrem durante esse processo: sincronização de associação e sincronização do documento. Os metadados para esses processos de sincronização originam de serviços web diferentes. Além disso, um servidor de determinado Exchange pode conter caixas de correio de site que são vinculadas a várias SharePoint servidores ou farms. Portanto, o alerta pode se originar de vários servidores de caixa de correio, dependendo das condições a seguintes:

1.  Como caixas de correio de site usado ativamente na organização são distribuídas

2.  Os servidores de SharePoint vinculadas ao qual as caixas de correio de site usado ativamente

3.  Se o servidor de caixa de correio tem o volume de sincronização suficientes para atender aos limites de alerta

Para ajudar a resolver esse problema, o resultado da sincronização de amostra no alerta pode ajudar a determinar o motivo da falha. Detalhes sobre o sucesso ou falha de cada tentativa de sincronização é gravada na pasta Logging\\TeamMailbox *\<exExchangeSvrNoVersion installation directory\>*. Revise os arquivos Microsoft.Exchange.ServiceHost\_TeamMailboxSyncLog\* mais recentes para falhas pesquisando no termo **falhou**. Você também pode usar os cmdlets **Test-OAuthConnectivity**, **Test-SiteMailbox**e **Get-SiteMailboxDiagnostics** para solucionar ainda mais.

**O serviço MSExchangeServiceHost não está em execução**

Se o serviço MSExchangeServiceHost não estiver funcionando, você recebe um alerta semelhante ao seguinte:

O serviço 'MSExchangeServiceHost' não está executando após a recuperação tentativas. O serviço pode ser desativado ou em travar loop.

Para resolver esse problema, verifique se que o serviço de MSExchangeServiceHost está sendo executado no servidor que enviou o alerta. Se estiver executando o serviço, examine os logs de eventos Windows para indicações de por que o serviço pode não estar sendo executado anteriormente, como controle de serviço manual ou repetidas falhas do serviço.

**O serviço MSExchangeServiceHost tiver falhado**

Se o serviço MSExchangeServiceHost travar, você recebe um alerta semelhante ao seguinte:

O processo de MSExchangeServiceHost tiver travado pelo menos 3 vezes na últimos 60 minutos.  
Mensagem Watson:

\<*Message*\>

Para resolver esse problema, examine o log de eventos do aplicativo Windows no servidor que enviou o alerta para eventos **4999** relativas ao serviço MSExchangeServiceHost. O texto de detalhe pode fornecer informações sobre a causa do problema.

## Para obter mais informações

[Novidades do Exchange 2013](https://technet.microsoft.com/pt-br/library/jj150540\(v=exchg.150\))

[Cmdlets do Exchange 2013](https://technet.microsoft.com/pt-br/library/bb124413\(v=exchg.150\))

