---
title: 'Disponibilidade Gerenciada: Exchange 2013 Help'
TOCTitle: Disponibilidade Gerenciada
ms:assetid: ceb99e6f-6dca-446d-abfb-3e6fc6a72704
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Dn482056(v=EXCHG.150)
ms:contentKeyID: 59890402
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Disponibilidade Gerenciada

 

_**Aplica-se a:** Exchange Online, Exchange Server 2013 SP1_

_**Tópico modificado em:** 2017-03-29_

A garantia de que os usuários tenham uma boa experiência com emails sempre foi o principal objetivo dos administradores de sistemas de mensagens. Para ajudar a assegurar a disponibilidade e a confiabilidade da sua organização Exchange Server 2013, todos os aspectos do sistema devem ser ativamente monitorados, e qualquer problema detectado deve ser rapidamente resolvido. Em versões anteriores do Exchange, o monitoramento de componentes críticos do sistema geralmente envolvia o uso de um aplicativo externo, como o Microsoft System Center 2012 Operations Manager, para coletar dados e fornecer a ação de recuperação para os problemas detectados como resultado da análise dos dados coletados. O Exchange 2010 e versões anteriores incluíam manifestos de integridade e mecanismos de correlação na forma de pacotes de gerenciamento. Esses componentes habilitavam o Operations Manager a determinar se um determinado componentes está íntegro ou não. Além disso, o Operations Manager também usava a infraestrutura de cmdlet de diagnóstico, interna ao Exchange 2010, para executar transações sintéticas baseadas em vários aspectos do sistema.

O Exchange 2013 traz uma nova abordagem ao monitoramento e à preservação da experiência do usuário final, usando nativamente um recurso chamado *Disponibilidade Gerenciada*, que fornece monitoramento interno e ações de recuperação.

## Disponibilidade Gerenciada

A disponibilidade gerenciada, também conhecida como *Monitoramento Ativo* ou *Monitoramento Ativo Local*, é a integração do monitoramento interno e das ações de recuperação com a plataforma de alta disponibilidade do Exchange. O recurso foi projetado para detectar e se recuperar de problemas assim que eles ocorrem e são descobertos pelo sistema. Diferentemente das soluções e técnicas anteriores de monitoramento externo do Exchange, a disponibilidade gerenciada não tenta identificar ou comunicar a causa raiz de um problema. Em vez disso, ela se concentra nos aspectos de recuperação que tratam das três principais áreas da experiência do usuário.

  - **Disponibilidade**   Os usuários podem acessar o serviço?

  - **Latência**   Como é a experiência para os usuários?

  - **Erros**   Os usuários podem obter aquilo que querem?

Essa consolidação de função de servidor e outras alterações de arquitetura do Exchange 2013 exigem uma nova abordagem para as metodologias de monitoramento e para o modelo de integridade de versões anteriores do Exchange. A disponibilidade gerenciada foi projetada para cuidar dessas alterações fornecendo uma solução nativa de monitoramento de integridade e recuperação. Ela abandona o monitoramento de fatias separadas individuais do sistema e adota o monitoramento da experiência completa do usuário, protegendo a experiência do usuário final por meio de ações orientadas à recuperação.

A disponibilidade gerenciada é um processo interno executado em cada servidor do Exchange 2013. Ela examina e analisa centenas de métricas de integridade a cada segundo. Se algo errado for detectado, isso será, na maior parte das vezes, corrigido automaticamente. Mas sempre haverá problemas que a disponibilidade gerenciada, por si só, não poderá resolver. Nesses casos, a disponibilidade gerenciada encaminhará o problema para um administrador, usando o log de eventos.

A disponibilidade gerenciada é implementada na forma de dois serviços:

  - **Serviço de Gerenciamento de Integridade do Exchange (MSExchangeHMHost.exe)**   É um processo controlador, usado para gerenciar processos de trabalho. É usado para compilar, executar e iniciar e parar o processo de trabalho, conforme o necessário. Também é usado para recuperar o processo de trabalho em caso de falha, para evitar que o processo de trabalho se torne um único ponto de falha.

  - **Processo de trabalho do Gerenciador de integridade do Exchange (MSExchangeHMWorker.exe)**   Este é o processo de trabalho responsável pela execução de tarefas de tempo de execução dentro da estrutura de disponibilidade gerenciada.

A disponibilidade gerenciada usa o armazenamento persistente para executar suas funções:

  - Os arquivos XML da pasta \\bin\\Monitoring\\config são usados para armazenar definições de configuração para alguns dos itens de trabalho da sonda e do monitor.

  - Active Directory é usado para armazenar substituições globais.

  - O Registro do Windows é usado para armazenar dados de tempo de execução, como indicadores, e substituições locais (específicas de servidor).

  - A infraestrutura de log de evento do canal carmesim do Windows é usada para armazenar resultados de itens de trabalho.

  - As caixas de correio de integridade são usadas para atividades de investigação. Várias caixas de correio de integridade serão criadas em cada banco de dados de caixa de correio existente no servidor.

Como ilustrado no desenho a seguir, a disponibilidade gerenciada inclui três componentes assíncronos principais, que estão constantemente trabalhando.

**Componentes de disponibilidade gerenciada**

![Disponibilidade gerenciada no Exchange Server 2013](images/Dn482056.7a54dcb5-1e28-4bd4-87e6-0d496b4ab796(EXCHG.150).gif "Disponibilidade gerenciada no Exchange Server 2013")

O primeiro componente é chamado de um *teste*. Sondas são responsáveis por colocar medidas no servidor e a coleta de dados. Os resultados de tais medidas fluem para o segundo componente, o *Monitor*. O monitor contém toda a lógica de negócios usada pelo sistema com base no que é considerado Íntegro sobre os dados coletados. Semelhante a um mecanismo de reconhecimento padrão, o monitor procura os vários diferentes padrões em todas as medições coletados e, em seguida, decida se algo é considerado íntegro. Finalmente, há *respondentes*, que são responsáveis por ações de escalonamento e a recuperação. Quando algo não está íntegro, a primeira ação é para tentar recuperar esse componente. Isso pode incluir as ações de recuperação de várias fases; Por exemplo, a primeira tentativa pode ser reiniciar o pool de aplicativos, o segundo pode ser para reiniciar o serviço, a tentativa de terceira pode estar reiniciar o servidor e a tentativa subsequente pode ser colocar o servidor offline para que ele aceite o tráfego não é mais. Se as ações de recuperação bem sucedidas, o sistema escalona o problema para um humano por meio de notificações de log de eventos.

Existem três categorias principais de sondas: sondas recorrentes, notificações e verificações. Sondas recorrentes são transações sintéticas realizadas pelo sistema para testar a experiência do usuário de ponta a ponta. As verificações são a infraestrutura que executar a coleta de dados de desempenho, incluindo o tráfego de usuário, e medem os dados coletados em relação a limites definidos para determinar os picos de falhas de usuário. Isso permite que a infraestrutura de verificações fique ciente quando os usuários estão enfrentando problemas. Finalmente, a lógica de notificação permite que o sistema deverá executar uma ação que imediatamente com base em um evento crítico, sem precisar aguardar os resultados dos dados coletados por uma sonda. Normalmente são exceções ou as condições que podem ser detectadas e reconhecidas sem um conjunto de grandes de amostras.

Sondas recorrentes execute cada alguns minutos e verifique se algum aspecto de integridade do serviço. Esses testes podem transmitir um email por meio do Exchange ActiveSync para uma caixa de correio de monitoramento, eles podem ser conectar a um ponto de extremidade RPC ou eles podem verificar a conectividade do cliente Access-para-Mailbox.

Todos os testes são definidos na inicialização do serviço do Gerenciador de integridade no canal crimson de Microsoft.Exchange.ActiveMonitoring\\ProbeDefinition. Cada definições de sonda tem várias propriedades, mas as propriedades mais relevantes são:

  - **Nome** O nome da sonda, que começa com um *SampleMask* Monitor de teste.

  - **TypeName** O tipo de objeto de código da sonda que contém a lógica da sonda.

  - **ServiceName** O nome do conjunto de integridade que contém essa sonda.

  - **TargetResource** O objeto a sonda está validando. Isso é anexado ao nome da sonda quando ele é executado para se tornar um resultado de sonda *ResultName*

  - **RecurrenceIntervalSeconds** Com que frequência a sonda executa.

  - **TimeoutSeconds** Quanto tempo a sonda esperará antes de falhar.

Há centenas de sondas recorrentes. Muitas dessas investigações são por banco de dados, assim como o número de aumenta de bancos de dados, aumenta o número de testes. Maioria dos testes são definidos no código e, portanto, não são diretamente detectáveis.

Noções básicas sobre uma sonda recorrente é os seguintes: iniciar cada *RecurrenceIntervalSeconds* e verificar (ou investigue) alguns aspectos de integridade. Se o componente está íntegro, a sonda passa e grava um evento informativo o canal de Microsoft.Exchange.ActiveMonitoring\\ProbeResult com um *ResultType* de 3. Se a verificação falha ou expire, o teste falhará e grava um evento de erro ao mesmo canal. Um *ResultType* de 4 significa que a verificação de falha e um *ResultType* 1 significa que ele se esgotou. Muitos testes serão executado novamente se eles tempo de espera, até o valor da propriedade *MaxRetryAttempts* .


> [!TIP]
> <STRONG>Observação</STRONG> A ProbeResult canal crimson pode fazer muito ocupado com centenas de sondas executando cada alguns minutos e registrar um evento, portanto, pode haver um impacto real sobre o desempenho do seu servidor Exchange, caso você tente consultas caras contra os logs de eventos em um ambiente de produção.



As notificações são sondas que não são executadas pela estrutura de Gerenciador de integridade, mas, por algum outro serviço no servidor. Esses serviços realizar suas próprias monitoramento e, em seguida, feed seus dados o Framework de disponibilidade gerenciada escrevendo diretamente resultados de sonda. Você não verá estes testes no canal ProbeDefinition, como esse canal apenas descreve os testes que serão executados pela estrutura de disponibilidade gerenciada. Por exemplo, o Monitor de ServerOneCopyMonitor é disparado por escrito pelo serviço MSExchangeDAGMgmt resultados da sonda. Esse serviço executa seu próprio monitoring, determina se há um problema e os logs de um resultado de teste. A maioria dos testes de notificação possuem a capacidade de registrar um evento vermelho que ativa o monitor não íntegros e um evento verde que torna íntegro o monitor novamente.

As verificações são sondas que apenas log de eventos quando um contador de desempenho passa acima ou abaixo de um limite definido. Eles são realmente um caso especial de sondas de notificação, pois não há um serviço os contadores de desempenho no servidor de monitoramento e log de eventos para o canal de ProbeResult quando o limite configurado for atingido.

Para localizar o contador e o limite que é considerado não íntegro, você pode examinar o monitor para essa verificação. Monitores do tipo *Microsoft.Office.Datacenter.ActiveMonitoring.OverallConsecutiveSampleValueAboveThresholdMonitor* ou *Microsoft.Office.Datacenter.ActiveMonitoring.OverallConsecutiveSampleValueBelowThresholdMonitor* significam que a sonda Assista a é um teste de verificação

Os monitores consultam os dados coletados pelas sondas para determinar se a ação deve ser realizada com base em um conjunto predefinido de regras. Dependendo da regra ou da natureza do problema, um monitor poderá iniciar um respondente ou encaminhar o problema para alguém por meio de uma entrada no log de eventos. Além disso, os monitores definem o período pós-falha em que um respondente será executado, como também o fluxo de trabalho da ação de recuperação. Monitores têm vários estados. Na perspectiva de estado do sistema, os monitores têm dois estados:

  - **Íntegro**   O monitor está funcionando adequadamente e todas as métricas coletadas cumprem os parâmetros operacionais normais.

  - **Não Íntegro**   O monitor não está íntegro e iniciou uma recuperação por meio de um respondente ou notificou o administrador via escalonamento.

Na perspectiva administrativa, os monitores têm mais dois estados, que aparecem no Shell:

  - **Degradado**   Quando um monitor apresenta um estado de não integridade durante 0 a 60 segundos, ele é considerado degradado. Se o monitor apresentar um estado de não integridade por mais de 60 segundos, ele será considerado Não Íntegro.

  - **Desabilitado**   O monitor foi explicitamente desabilitado por um administrador.

  - **Não Disponível**   O serviço de integridade do Microsoft Exchange consulta periodicamente cada monitor para detectar seu estado. Se o serviço não conseguir uma resposta para a consulta, o estado do monitor se tornará Não Disponível.

  - **Reparando**   Um administrador define o estado Reparando para indicar ao sistema que a ação corretiva está sendo realizada por alguém, o que permite ao sistema e à pessoa diferenciar as falhas que podem ocorrer simultaneamente à ação corretiva (por exemplo, falha na operação de cópia de banco de dados).

Cada monitor tem uma propriedade *SampleMask* em sua definição. À medida que o monitor é executado, ele procura os eventos do canal de ProbeResult que têm um *ResultName* correspondente *SampleMask* do monitor. Esses eventos poderia ser de sondas recorrentes, notificações ou verificações. Se os limites do monitor são atingidos, ele se torna não íntegra. Da perspectiva do monitor, todos os tipos de sonda três são os mesmos quando eles cada se conectam ao canal ProbeResult.

É importante observar que uma falha de sonda único não necessariamente indica que há algo errado com o servidor. É o design de monitores para identificar corretamente quando há algum problema real que precisa ser corrigido. Isso é por isso que muitos monitores têm limites de múltiplas falhas de sonda antes de se tornar não íntegra. Mesmo assim, muitos desses problemas podem ser corrigidos automaticamente pelo respondentes, portanto, o melhor local para procurar problemas que exigem intervenção manual é no canal crimson de Microsoft.Exchange.ManagedAvailability\\Monitoring. Isso incluirá o erro mais recente da sonda.

Tal como indica o nome deles, os respondentes executam algum tipo de resposta a um alerta gerado por um monitor. Os respondentes realizam várias ações de recuperação; por exemplo, reiniciam um pool de trabalhos de aplicativo para reinicializar um servidor. Há vários tipos de respondentes:

  - **Respondente Reiniciar** Finaliza e reinicia um serviço

  - **Respondente Reiniciar Pool de Aplicativos** Interrompe e reinicia um pool de aplicativos no IIS (Serviços de Informações da Internet).

  - **Respondente de Failover** Inicia um failover de banco de dados ou de servidor

  - **Respondente de Verificação de Erro** Inicia uma verificação de erro do servidor, causando assim uma reinicialização do servidor

  - **Respondente Offline** Usa um protocolo em um servidor fora de serviço (rejeita solicitações de clientes)

  - **Respondente Online** Aplica um protocolo em um servidor que voltou ao modo de produção (aceita solicitações de clientes)

  - **Respondente de Escalonamento** Encaminha o problema para um administrador por meio do log de eventos

Além dos respondentes listados acima, alguns componentes também têm respondentes especializados e exclusivos do componente.

Todos os respondentes incluem o comportamento de limitação, que fornece um mecanismo de sequenciamento interno para controlar as ações do respondente. O comportamento de limitação foi projetado para garantir que o sistema não será comprometido ou prejudicado como resultado das ações de recuperação do respondente. Todos os respondentes são limitados de alguma forma. Quando ocorre uma limitação, a ação de recuperação do respondente pode ser ignorada ou atrasada, dependendo da ação. Por exemplo, quando o respondente de verificação de erro é limitado, sua ação é ignorada, em vez de atrasada.

## Conjuntos de integridade

Na perspectiva de relatórios, a disponibilidade gerenciada tem dois modos de exibição de integridade, um interno e outro externo. O modo de exibição interno usa *conjuntos de integridade*. Cada componentes do Exchange 2013 (por exemplo, o Outlook Web App, o Exchange ActiveSync, o serviço Armazenamento de Informações, a indexação de conteúdo, os serviços de transporte etc.) é monitorado pela disponibilidade gerenciado usando sondas, monitores e respondentes. Um grupo de sondas, monitores e respondentes de um determinado componente é chamado de *conjunto de integridade*. Um conjunto de integridade é um grupo de sondas, monitores e respondentes, que determina se o componente é íntegro. O estado atual de um conjunto de integridade (ou seja, se está íntegro ou não) é determinado pelo estado dos monitores do conjunto de integridade. Se todos os monitores de um conjunto de integridade forem íntegros, então o conjunto de integridade terá um estado íntegro. Se qualquer monitor não tiver um estado íntegro, então o estado do conjunto de integridade será determinado pelo monitor menos íntegro.

Para obter etapas detalhadas para exibir a integridade de servidor ou o estado de conjuntos de integridade, veja [Gerenciar conjuntos de integridade e a integridade do servidor](manage-health-sets-and-server-health-exchange-2013-help.md).

## Grupos de integridade

O modo de exibição externo da disponibilidade gerenciada é composto pelos *grupos de integridade*. Os grupos de integridade são expostos no System Center Operations Manager 2007 R2 e no System Center Operations Manager 2012.

Há quatro grupos principais de integridade:

  - **Pontos de toque do cliente** Componentes que afetam as interações do usuário em tempo real; por exemplo, protocolos ou o Armazenamento de Informações

  - **Componentes de serviço** Componentes sem interação direta e em tempo real do usuário; por exemplo, o serviço Replicação de Caixa de Correio do Microsoft Exchange ou o OABGen (processo de geração do catálogo de endereços offline)

  - **Componentes de servidor** Os recursos físicos do servidor; por exemplo, espaço em disco, memória e rede

  - **Disponibilidade de dependência** A capacidade do servidor de acessar as dependências necessárias; por exemplo, Active Directory, DNS etc.

Quando o pacote de gerenciamento do Exchange está instalado, o System Center Operations Manager (SCOM) atua como um portal de integridade para exibir informações relacionadas ao ambiente Exchange. O painel de controle do SCOM inclui três modos de exibição de integridade do servidor de Exchange:

  - **Alertas Ativos** Os respondentes de escalonamento gravam eventos no log de eventos do Windows, os quais são consumidor pelo monitor no SCOM. São exibidos como alertas no modo de exibição Alertas Ativos.

  - **Integridade da organização** Um resumo de rollup da integridade global da integridade da organização Exchange é mostrada nesse modo de exibição. Esses rollups incluem a exibição da integridade de cada grupo de disponibilidade de banco de dados, além da integridade em sites Active Directory específicos.

  - **Integridade de servidor** Os conjuntos de integridade relacionados são combinados em grupos de integridade e resumidos nesse modo de exibição.

## Substituições

As substituições capacitam o administrador a configurar alguns aspectos de sondas, monitores e respondentes da disponibilidade gerenciada. As substituições podem ser usadas para ajustar alguns dos limites utilizados pela disponibilidade gerenciada. Elas também podem ser usadas para habilitar ações emergenciais para eventos inesperados, o que pode exigir definições de configuração diferentes dos padrões predefinidos.

Substituições podem ser criadas e aplicadas em um único servidor (o que se conhece como *substituição de servidor*) ou podem ser aplicadas a um grupo de servidores (mais conhecida como *substituição global*). Os dados de configuração da substituição de servidor são armazenados no Registro do Windows, no servidor em que a substituição foi aplicada. Os dados de configuração da substituição global são armazenados em Active Directory.

As substituições podem ser configuradas com duração infinita ou com uma duração específica. Além disso, as substituições globais podem ser configuradas para aplicação em todos os servidores ou apenas nos servidores que executam uma determinada versão do Exchange.

Quando configura cria uma substituição, ela não tem efeito imediato. O serviço Gerenciador de Integridade do Microsoft Exchange verifica se há dados de configuração atualizados, a cada 10 minutos. Além disso, as substituições globais são dependentes da latência de replicação do Active Directory.

Para obter as etapas detalhadas para exibir ou configurar substituições de servidor ou globais, veja [Configurar substituições de disponibilidade gerenciada](configure-managed-availability-overrides-exchange-2013-help.md).

## Cmdlets e tarefas de gerenciamento

Há três tarefas operacionais principais que, em geral, os administradores executam na disponibilidade gerenciada:

  - Extração ou exibição da integridade do sistema

  - Exibição de conjuntos de integridade e detalhes sobre sondas, monitores e respondentes

  - Gerenciamento de substituições

As duas principais ferramentas de gerenciamento da disponibilidade gerenciada são Logo de Eventos do Windows e o Shell. A disponibilidade gerenciada registra uma grande quantidade de informações nos logs de eventos do canal carmesim ActiveMonitoring e ManagedAvailability do Exchange; por exemplo:

  - Definições de sonda, monitor e respondente que registrou os respectivos logs de eventos \*Definição.

  - Resultados de sonda, monitor e respondente que registrou os respectivos logs de eventos \*Resultados.

  - Detalhes sobre as ações de recuperação do respondente, incluindo quando a ação de recuperação foi iniciada e quando foi considerada concluída (se bem-sucedida ou não), o que é registrado no log de evento RecoveryActionResults.

Há 12 cmdlets usados para disponibilidade gerenciada, os quais estão descritos na tabela a seguir.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Cmdlet</th>
<th>Descrição</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="https://technet.microsoft.com/pt-br/library/jj218703(v=exchg.150)">Get-ServerHealth</a></p></td>
<td><p>Usado para obter informações brutas de integridade do servidor; por exemplo, conjuntos de integridade e respectivos estados vigentes (íntegro ou não íntegro), monitores de conjuntos de integridade, componentes de servidor, recursos de destino para sondas e carimbos de data/hora relacionados à hora de início ou de término da sonda ou do monitor e às horas de transição de estado.</p></td>
</tr>
<tr class="even">
<td><p><a href="https://technet.microsoft.com/pt-br/library/jj218724(v=exchg.150)">Get-HealthReport</a></p></td>
<td><p>Usado para obter um modo de exibição de resumo da integridade, que inclui conjuntos de integridade e respectivos estados vigentes.</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://technet.microsoft.com/pt-br/library/jj218668(v=exchg.150)">Get-MonitoringItemIdentity</a></p></td>
<td><p>Usado para exibir sondas, monitores e respondentes associados a um conjunto específico de integridade.</p></td>
</tr>
<tr class="even">
<td><p><a href="https://technet.microsoft.com/pt-br/library/jj218642(v=exchg.150)">Get-MonitoringItemHelp</a></p></td>
<td><p>Usado para exibir descrições sobre algumas das propriedades de sondas, monitores e respondentes.</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://technet.microsoft.com/pt-br/library/jj218628(v=exchg.150)">Add-ServerMonitoringOverride</a></p></td>
<td><p>Usado para criar uma substituição local, específica do servidor de sonda, monitor ou respondente.</p></td>
</tr>
<tr class="even">
<td><p><a href="https://technet.microsoft.com/pt-br/library/jj218664(v=exchg.150)">Get-ServerMonitoringOverride</a></p></td>
<td><p>Usado para exibir uma lista de substituições locais no servidor especificado.</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://technet.microsoft.com/pt-br/library/dn482411(v=exchg.150)">Remove-ServerMonitoringOverride</a></p></td>
<td><p>Usado para remover uma substituição local de um servidor específico.</p></td>
</tr>
<tr class="even">
<td><p><a href="https://technet.microsoft.com/pt-br/library/jj218683(v=exchg.150)">Add-GlobalMonitoringOverride</a></p></td>
<td><p>Usado para criar uma substituição global para um grupo de servidores.</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://technet.microsoft.com/pt-br/library/jj218627(v=exchg.150)">Get-GlobalMonitoringOverride</a></p></td>
<td><p>Usado para exibir uma lista de substituições globais configuradas na organização.</p></td>
</tr>
<tr class="even">
<td><p><a href="https://technet.microsoft.com/pt-br/library/jj218675(v=exchg.150)">Remove-GlobalMonitoringOverride</a></p></td>
<td><p>Usado para remover uma substituição global.</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://technet.microsoft.com/pt-br/library/jj218699(v=exchg.150)">Set-ServerComponentState</a></p></td>
<td><p>Usado para configurar o estado de um ou mais componentes de servidor.</p></td>
</tr>
<tr class="even">
<td><p><a href="https://technet.microsoft.com/pt-br/library/jj218713(v=exchg.150)">Get-ServerComponentState</a></p></td>
<td><p>Usado para exibir o estado de um ou mais componentes de servidor.</p></td>
</tr>
</tbody>
</table>

