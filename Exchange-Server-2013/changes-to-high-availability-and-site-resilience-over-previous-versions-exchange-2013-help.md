---
title: 'Alterações na alta disp. e resilência de site em relação a versões anteriores'
TOCTitle: Alterações na alta disponibilidade e resilência de site em relação às versões anteriores
ms:assetid: de53c00b-091c-4a31-aacc-1bd40c756ce2
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Dn789066(v=EXCHG.150)
ms:contentKeyID: 62519766
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Alterações na alta disponibilidade e resilência de site em relação às versões anteriores

 

_**Aplica-se a:** Exchange Server 2013 SP1_

_**Tópico modificado em:** 2015-04-07_

O Exchange 2013 usa DAGs e cópias de banco de dados de caixa de correio, além de outros recursos, como recuperação de itens únicos, políticas de retenção e cópias de banco de dados com atraso, para fornecer alta disponibilidade, resiliência de site e proteção de dados nativos do Exchange. A plataforma de alta disponibilidade, o Repositório de Informações do Exchange e o Mecanismo de Armazenamento Extensível (ESE) foram aprimorados para oferecer maior disponibilidade, gerenciamento mais fácil e reduzir custos. Esses aprimoramentos incluem:

  - **Redução de IOPS em relação ao Exchange 2010**   Permite utilizar discos maiores em termos de capacidade e IOPS da forma mais eficiente possível.

  - **Disponibilidade gerenciada**   Com a disponibilidade gerenciada, o monitoramento interno e os recursos orientados à recuperação estão totalmente integrados para ajudar a impedir falhas, restaurar serviços proativamente e iniciar failovers de servidor automaticamente ou alertar administradores para tomarem uma providência. O foco está no monitoramento e no gerenciamento da experiência do usuário final em vez de apenas no servidor e no tempo de operação de componentes, para ajudar a manter o serviço continuamente disponível.

  - **Repositório Gerenciado**   Repositório Gerenciado é o nome dos processos de Repositório de Informações reescritos recentemente no Exchange 2013. O novo Repositório Gerenciado é escrito em C\# e possui alta integração com o serviço de Replicação do Microsoft Exchange (MSExchangeRepl.exe) para oferecer disponibilidade maior por meio de resiliência aprimorada.

  - **Suporte para vários bancos de dados por disco**   O Exchange 2013 inclui aprimoramentos que possibilitam o suporte para vários bancos de dados (combinações de cópias ativas e passivas) no mesmo disco, utilizando, assim, discos maiores em termos de capacidade e IOPS da forma mais eficiente possível.

  - **Nova propagação automática**   A habilidade de nova propagação automática permite que você restaure rapidamente a redundância de banco de dados após uma falha de disco. Se um disco falhar, a cópia de banco de dados armazenada nesse disco será copiada da cópia de banco de dados ativa para um disco reserva no mesmo servidor. Se várias cópias de banco de dados forem armazenadas no disco com falha, todas elas poderão ser automaticamente repropagadas em um disco reserva. Isso permite propagações mais rápidas, visto que os bancos de dados ativos provavelmente estão em vários servidores, e os dados são copiados em paralelo.

  - **Recuperação automática de falhas de armazenamento**   Este recurso dá continuidade à inovação introduzida no Exchange 2010 para permitir que o sistema se recupere de falhas que afetam a resiliência ou a redundância. Além dos comportamentos de verificação de bugs do Exchange 2010, o Exchange 2013 inclui comportamentos de recuperação adicionais para tempos de E/S longos e consumo de memória excessivo pelo MSExchangeRepl.exe. Nos casos severos em que o sistema está em um estado inválido, threads não podem ser agendados.

  - **Aprimoramentos de cópias com retardamento**   As cópias com retardamento podem agora administrar a si próprias até um determinado limite, desprezando o log automaticamente. As cópias com retardamento desprezarão automaticamente os arquivos de log em uma variedade de situações, como cenários de correção de páginas e pouco espaço em disco. Se o sistema detectar que a correção de páginas é necessária para uma cópia com retardamento, os logs serão automaticamente reproduzidos na cópia com retardamento para a correção das páginas. As cópias com retardamento chamarão esse recurso de reprodução automática quando um limite de pouco espaço em disco for atingido e quando a cópia com retardamento tiver sido detectada como a única disponível para um período específico. Além disso, as cópias com retardamento podem utilizar a Rede de Segurança, tornando a recuperação ou a ativação mais fácil.

  - **Aprimoramentos no alerta de cópia única**   O alerta de cópia única introduzido no Exchange 2010 não é mais um script agendado separado. Ele está agora integrado aos componentes de disponibilidade gerenciados no sistema e é uma função nativa no Exchange.

  - **Configuração automática da rede do DAG**   As redes do DAG podem ser automaticamente configuradas pelo sistema com base nas definições de configuração. Além das opções de configuração manual, os DAGs podem também fazer a distinção entre as redes MAPI e de replicação e configurar as redes do DAG automaticamente.

## Redução de IOPS em relação ao Exchange 2010

No Exchange 2010, as cópias de banco de dados passivas têm uma profundidade de ponto de verificação muito baixa, o que é necessário para failover mais rápido. Além disso, a cópia passiva realiza uma pré-leitura agressiva de dados para acompanhar a profundidade de ponto de verificação de 5 MB. Como resultado do uso de uma profundidade de ponto de verificação baixa e realizando essas operações de pré-leitura agressivas, o IOPS de uma cópia de banco de dados passiva foi igual ao IOPS de uma cópia ativa no Exchange 2010.

No Exchange 2013, o sistema consegue fornecer failover rápido ao usar uma profundidade de ponto de verificação alta na cópia passiva (100 MB). Como as cópias passivas têm uma profundidade de ponto de verificação de 100 MB, elas foram desajustadas para não serem mais agressivas. Como resultado do aumento da profundidade de ponto de verificação e do desajuste das pré-leituras agressivas, o IOPS de uma cópia passiva é de aproximadamente 50% do IOPS da cópia ativa no Exchange 2013.

Ter uma profundidade de ponto de verificação mais alta na cópia passiva também resulta em outras alterações. No failover no Exchange 2010, o cache de banco de dados é liberado conforme o banco de dados é convertido de uma cópia passiva para uma ativa. No Exchange 2013, o registro em log de ESE foi reescrito para que o cache seja persistido através da transição de passivo para ativo. Como ESE não precisa liberar o cache, você obtém failover rápido.

Uma outra alteração foi feita para o processo de manutenção de banco de dados em segundo plano (BDM). A BDM agora processa cerca de 1 a 2 MB por segundo por cópia.

Devido a essas alterações, o Exchange 2013 fornece uma redução significante no IOPS em relação ao Exchange 2010.

## Disponibilidade gerenciada

A disponibilidade gerenciada é a integração de monitoramento ativo incorporado e da plataforma de alta disponibilidade do Exchange 2013. Com disponibilidade gerenciada, o sistema pode determinar quando fazer o failover de um banco de dados com base na integridade do serviço. A disponibilidade gerenciada é uma infraestrutura interna implantada nas funções de servidor de Acesso para Cliente e de Caixa de Correio no Exchange 2013. A disponibilidade gerenciada inclui três componentes assíncronos principais que estão constantemente fazendo o trabalho. O primeiro componente é o mecanismo de sondagem, responsável por realizar medições no servidor e coletar os dados. Os resultados dessas medições vão para o segundo componente, chamado de monitoramento. O monitoramento contém toda a lógica de negócios usada pelo sistema com base no que é considerado íntegro nos dados coletados. Similar ao mecanismo de reconhecimento de padrão, o monitoramento procura os vários padrões diferentes em todas as medições coletadas e pode decidir se algo é considerado íntegro ou não. Finalmente, há o mecanismo de respondente, que é responsável pelas ações de recuperação. Quando algo não é íntegro, a primeira ação é tentar recuperar esse componente. Essas ações podem ser de recuperação em vários estágios; por exemplo, a primeira tentativa pode ser reiniciar o pool de aplicativos, a segunda pode ser reiniciar o serviço, e a terceira, reiniciar o servidor, e a tentativa seguinte, colocar o servidor offline para que não aceite mais tráfego. Se as ações de recuperação não tiverem êxito, o sistema escalará o problema a uma pessoa por meio de notificações de log de eventos.

A disponibilidade gerenciada é implementada na forma de dois serviços:

  - **Serviço de Gerenciador de Integridade do Exchange (MSExchangeHMHost.exe)**   Este é um processo de controlador usado para gerenciar processos de trabalho. É usado para criar, executar, iniciar e interromper o processo de trabalho, conforme necessário. É também usado para recuperar o processo de trabalho caso o processo falhe, para impedir que o processo de trabalho seja um ponto de falha único

  - **Processo Trabalho do Gerenciador de Integridade do Exchange (MSExchangeHMHost.exe)**   Este é um processo de trabalho responsável por executar as tarefas de tempo de execução.

A disponibilidade gerenciada usa armazenamento persistente para desempenhar suas funções:

  - Os arquivos de configuração XML são usados para inicializar as definições de item de trabalho durante a inicialização do processo de trabalho.

  - O Registro é usado para armazenar dados de tempo de execução, como indicadores.

  - A infraestrutura do log de eventos do canal crimson é usada para armazenar os resultados de item de trabalho.

Para obter mais informações sobre disponibilidade gerenciada, consulte [Disponibilidade Gerenciada](managed-availability-exchange-2013-help.md).

## Repositório Gerenciado

Todas as versões anteriores do Exchange Server, do Exchange Server 4.0 para o Exchange Server 2010, oferecem suporte a execução de uma única instância do processo de armazenamento de informações (Store.exe) na função de servidor de caixa de correio. Essa única instância do repositório hospeda todos os bancos de dados no servidor: ativa, passivo com atraso e a recuperação. As arquiteturas anteriores do Exchange, não há pouca ou nenhuma, isolamento entre os diferentes bancos de dados hospedados em um servidor de caixa de correio. Um problema com um banco de dados de caixa de correio única tem o potencial de afetar negativamente todos os outros bancos de dados e falhas resultantes de uma corrupção de caixa de correio podem afetar o serviço para todos os usuários cujos bancos de dados são hospedados no servidor.

Outro desafio com uma única instância do repositório nas versões anteriores do Exchange é que o mecanismo de armazenamento extensível (ESE) dimensiona bem a 12 de 8 núcleos de processador, mas Além disso, os problemas de sincronização de comunicação e cache de entre processadores implicar negativo escala. Dado servidores muito maiores de hoje, com 16 + principais sistemas disponíveis, isso significaria impor o desafio administrativo de gerenciar a afinidade de 12 de 8 núcleos para ESE e usar os outros núcleos para processos de não-Store (por exemplo, assistentes, Search Foundation, Disponibilidade gerenciada, etc.). Além disso, a arquitetura anterior restrito dimensione para o processo de armazenamento.

Evolução consideravelmente o processo de Store.exe ao longo dos anos como o próprio evolução, Exchange Server, mas como um único processo, basicamente sua escalabilidade é limitada e representa um único ponto de falha. Devido a estes limites, Store.exe é ido no Exchange 2013 e substituída pela loja gerenciado.

Para obter mais informações, consulte [Repositório Gerenciado](managed-store-exchange-2013-help.md).

## Vários bancos de dados por volume

Embora os aprimoramentos de armazenamento no Exchange 2013 sejam projetados principalmente para configurações de apenas um grupo de discos (JBOD), eles estão disponíveis para uso por todas as configurações de armazenamento suportadas. Um recurso é a disponibilidade de hospedar vários bancos de dados no mesmo volume. Esse recurso é sobre a otimização do Exchange para discos grandes. Essas otimizações resultam em um uso muito mais eficiente de discos grandes em termos de capacidade, IOPS e tempos de nova propagação e devem resolver os desafios associados à execução em uma configuração de armazenamento JBOD:

  - Os tamanhos de banco de dados devem ser gerenciáveis.

  - As operações de nova propagação devem ser rápidas e confiáveis.

  - Embora a capacidade de armazenamento esteja aumentando, o IOPS não aumenta.

  - As cópias de banco de dados passivas de hospedagem de discos estão subutilizadas em termos de IOPS.

  - Cópias com retardamento têm requisitos de armazenamento assimétrico.

  - Existe agilidade limitada para se recuperar de condições de pouco espaço em disco.

A tendência de aumento da capacidade de armazenamento continua, com unidades de 8 TB que devem estar disponíveis em breve. Usando unidades de 8 TB em conjunto com as diretrizes de práticas recomendadas de tamanho máximo de banco de dados do Exchange (2 TB), você gastaria mais de 5 TB de espaço em disco. Uma solução seria simplesmente aumentar os bancos de dados, mas isso inibe a capacidade de gerenciamento porque apresenta tempos de nova propagação muito grandes, incluindo, em alguns casos, tempos de nova propagação operacionalmente não gerenciáveis, e a capacidade de cópia dessa quantidade de dados pela rede fica comprometida.

Além disso, no modelo Exchange 2010, o disco que armazena uma cópia passiva fica subutilizado em termos de IOPS. No caso de cópia passiva com retardamento, o disco fica não só subutilizado em termos de IOPS, mas também assimétrico em termos de seu tamanho, em relação aos discos usados para armazenar as cópias ativas e passivas sem retardamento.

Dando continuidade a uma prática de longa data, o Exchange 2013 foi otimizado para que ele possa usar discos grandes (8 TB) em uma configuração JBOD de modo mais eficiente. No Exchange 2013, com vários bancos de dados por disco, você pode ter discos com o mesmo tamanho armazenando várias cópias de banco de dados incluindo cópias com retardamento. A meta é realizar a distribuição de usuários em um número de volumes existentes, oferecendo um design simétrico em que, durante as operações normais, cada membro do DAG hospeda uma combinação de cópias com retardamento ativas, passivas e opcionais nos mesmos volumes.

Um exemplo de uma configuração que utiliza vários bancos de dados por volume está ilustrada abaixo.

**Configuração que usa vários bancos de dados por volume**

![Vários bancos de dados por volume](images/Dn789066.c5e7d6c8-3e77-4f72-a873-5e9aaded9aa3(EXCHG.150).gif "Vários bancos de dados por volume")

A configuração acima fornece um design simétrico. Os quatro servidores têm os mesmos quatro bancos de dados hospedados em um único disco por servidor. A questão aqui é que o número de cópias de cada banco de dados que você tem deve ser igual ao número de cópias de banco de dados por disco. No exemplo acima, existem quatro cópias de cada banco de dados: uma cópia ativa, duas cópias passivas e uma cópia com retardamento. Como há quatro cópias de cada banco de dados, a configuração correta é a que tem quatro cópias por volume. Além disso, a preferência de ativação é configurada para que seja balanceada no DAG e em cada servidor. Por exemplo, a cópia ativa terá um valor de preferência de ativação de 1, a primeira cópia passiva terá um valor de preferência de ativação de 2, a segunda cópia passiva terá um valor de preferência de ativação de 3 e a cópia com retardamento terá um valor de preferência de ativação de 4.

Além de ter uma distribuição melhor de usuários nos volumes existentes, outro benefício de usar vários bancos de dados por disco é que isso reduz o tempo necessário para restaurar a proteção de dados no caso de uma falha que necessite de uma nova propagação (por exemplo, falha de disco).

À medida que um banco de dados cresce, a nova propagação do banco de dados leva cada vez mais tempo. Por exemplo, um banco de dados de 2 TB poderá levar 23 horas para uma nova propagação, ao passo que um banco de dados de 8 TB, até 93 horas (quase 4 dias). Ambas as propagações ocorreriam em cerca de 20 MB por segundo. Isso geralmente significa que um banco de dados muito grande não pode ser propagado dentro de um prazo operacionalmente razoável.

No caso de um cenário de cópia por disco de banco de dados único, a operação de propagação é efetivamente vinculada à fonte, porque ela está sempre propagando o disco a partir de uma única fonte. Dividindo o volume em várias cópias de banco de dados e armazenando a cópia ativa dos bancos de dados passivos de um determinado volume em membros separados do DAG, o sistema não será mais vinculado à fonte no contexto de nova propagação do disco. Quando um disco com falha é substituído, ele pode ser propagado novamente a partir de várias fontes. Isso permite que o sistema propague novamente e restaure a proteção de dados para esses bancos de dados em um tempo muito menor.

Ao usar vários bancos de dados por volume, recomendamos aderir às seguintes boas práticas e requisitos:

  - Uma única partição de disco lógico por disco físico deve ser usada. Não crie várias partições no disco. Cada cópia de banco de dados e seus arquivos complementares (como logs de transação e índice de conteúdo) devem ser hospedados em um único diretório na partição única.

  - O número de cópias de banco de dados configuradas por volume deverá ser igual ao número de cópias de cada banco de dados. Por exemplo, se você tiver quatro cópias de seus bancos de dados, você deverá usar quatro cópias por volume.

  - Cópias de banco de dados devem ter os mesmos vizinhos. (Por exemplo, todas elas devem compartilhar o mesmo disco em cada servidor.)

  - Equilibre a preferência de ativação no DAG, de forma que cada cópia de banco de dados em um determinado disco tenha um valor de preferência de ativação exclusivo.

## AutoReseed

A nova propagação automática, ou simplesmente AutoReseed, é um recurso que funciona como substituição do que é normalmente uma ação voltada para a administração em resposta a uma falha de disco, um evento de corrupção de banco de dados ou outro problema que necessite de uma nova propagação de uma cópia de banco de dados. A AutoReseed foi projetada para restaurar automaticamente a redundância de banco de dados após uma falha de disco usando discos sobressalentes provisionados no sistema.

Para obter mais informações, consulte [AutoReseed](autoreseed-exchange-2013-help.md). Para obter etapas detalhadas sobre como configurar o AutoReseed, consulte [Configurar o AutoReseed para um grupo de disponibilidade do banco de dados](configure-autoreseed-for-a-database-availability-group-exchange-2013-help.md).

## Recuperação automática de falhas de armazenamento

A recuperação automática de falhas de armazenamento dá continuidade à inovação introduzida no Exchange 2010 para permitir que o sistema se recupere de falhas que afetam a resiliência ou a redundância. Além dos comportamentos de verificação de bugs do Exchange 2010, o Exchange 2013 inclui comportamentos de recuperação adicionais para tempos de E/S longos e consumo de memória excessivo pelo serviço de Replicação do Microsoft Exchange (MSExchangeRepl.exe). Nos casos severos, threads não podem ser agendados.

Mesmo em ambientes JBOD, os controladores de matriz de armazenamento podem ter problemas, como falhas ou travamentos. O Exchange 2010 incluiu os recursos de detecção e recuperação de E/S parada, os quais proporcionaram maior resiliência. Esses recursos estão relacionadas na tabela a seguir.


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Nome</th>
<th>Verificar</th>
<th>Ação</th>
<th>Limite</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Detecção de ES de travamento de banco de dados de ESE</p></td>
<td><p>ESE verifica se há E/Ss pendentes</p></td>
<td><p>Gera um item de falha no canal crimson para reiniciar o servidor</p></td>
<td><p>240 segundos</p></td>
</tr>
<tr class="even">
<td><p>Pulsação de canal de item de falha</p></td>
<td><p>Verifica se os itens de falha podem ser gravados no canal crimson e lidos dele</p></td>
<td><p>Canal crimson de pulsações do serviço de replicação e servidor de reinicialização em falhas</p></td>
<td><p>30 segundos</p></td>
</tr>
<tr class="odd">
<td><p>Pulsação de disco do sistema</p></td>
<td><p>Verifica o estado de disco do sistema do servidor</p></td>
<td><p>Envia periodicamente E/S sem buffer ao disco do sistema; reinicia o servidor no limite de pulsações</p></td>
<td><p>120 segundos</p></td>
</tr>
</tbody>
</table>


O Exchange 2013 aprimora a resiliência de servidor e armazenamento incluindo novos comportamentos para outras condições sérias. Essas condições e esses comportamentos são descritos na tabela a seguir.


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Nome</th>
<th>Verificar</th>
<th>Ação</th>
<th>Limite</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Estado inválido do sistema</p></td>
<td><p>Nenhum thread, incluindo threads não gerenciados, pode ser agendado</p></td>
<td><p>Reiniciar o servidor</p></td>
<td><p>302 segundos</p></td>
</tr>
<tr class="even">
<td><p>Tempos de I/O longos</p></td>
<td><p>Medições de latência de operação de E/S</p></td>
<td><p>Reiniciar o servidor</p></td>
<td><p>41 segundos</p></td>
</tr>
<tr class="odd">
<td><p>Uso de memória do serviço de replicação</p></td>
<td><p>Medir o conjunto de trabalho de MSExchangeRepl.exe</p></td>
<td><ol>
<li><p>Gerar log de evento 4395 no canal crimson com uma solicitação de cancelamento do serviço</p></li>
<li><p>Iniciar encerramento de MSExchangeRepl.exe</p></li>
<li><p>Se o encerramento do serviço falhar, reinicie o servidor</p></li>
</ol></td>
<td><p>4 gigabytes (GB)</p></td>
</tr>
<tr class="even">
<td><p>System Event 129 (Reiniciar barramento)</p></td>
<td><p>Verifique o Event 129 no log de eventos do Sistema.</p></td>
<td><p>Reiniciar o servidor</p></td>
<td><p>Quando ocorrer o evento</p></td>
</tr>
<tr class="odd">
<td><p>O banco de dados do cluster trava</p></td>
<td><p>As atualizações do Gerenciador de Atualização Globais estão bloqueadas</p></td>
<td><p>Reiniciar o servidor</p></td>
<td><p>Quando ocorrer o evento</p></td>
</tr>
</tbody>
</table>


## Aprimoramentos de cópias com retardamento

Os aprimoramentos de cópias com retardamento incluem integração com Rede Segura e desprezo automático de arquivos de log em determinados cenários. Rede Segura é um recurso de transporte que substitui o recurso do Exchange 2010 conhecido como dumpster de transporte. Rede Segura é similar a dumpster de transporte, por ser uma fila de entrega associada ao serviço de Transporte em um servidor de Caixa de Correio. Essa fila armazena cópias de mensagens entregues com êxito ao banco de dados de caixa de correio ativo no servidor de Caixa de Correio. Cada banco de dados de caixa de correio ativo no servidor de Caixa de Correio tem sua própria fila que armazena cópias das mensagens entregues. Você pode especificar por quanto tempo a Rede Segura deve armazenar cópias das mensagens entregues com êxito antes que elas expirem e sejam excluídas automaticamente.

A Rede Segura assume alguma responsabilidade pela redundância de sombra em ambientes do DAG. Nos ambientes do DAG, a redundância de sombra não precisa manter outra cópia da mensagem entregue em uma fila de sombra enquanto aguarda a mensagem entregue ser replicada nas cópias passivas dos bancos de dados de caixa de correio nos outros servidores de Caixa de Correio no DAG. A cópia da mensagem entregue já está armazenada na Rede Segura, portanto, a redundância de sombra pode entregar novamente a mensagem a partir da Rede Segura se necessário.

Com a introdução da Rede Segura , a ativação de uma cópia de banco de dados com retardamento se torna bem mais fácil. Por exemplo, considere que você tenha uma cópia com retardamento que tem um retardo de repetição de dois dias. Nesse caso, você configuraria a Rede Segura para um período de dois dias. Se encontrar uma situação em que precisa usar sua cópia com retardamento, você poderá suspender a replicação para ela e copiá-la duas vezes (para preservar a natureza de retardamento do banco de dados e criar uma cópia extra caso você precise dela). Em seguida, faça uma cópia e descarte todos os arquivos de log, exceto aqueles no intervalo necessário. Monte a cópia, que dispara uma solicitação automática para a Rede Segura entregar novamente os últimos dois dias de email. Com a Rede Segura, não é preciso mais realizar nenhuma busca a partir de onde o ponto de corrupção foi introduzido. Você receberá os últimos dois dias de email, exceto os dados normalmente perdidos em um failover com perdas.

As cópias com retardamento podem agora administrar a si próprias chamando a reprodução de log automática para descartar os arquivos de log em certos cenários:

  - Quando um limite de pouco espaço em disco é atingido

  - Quando a cópia com retardamento tem corrupção física e precisa passar por correção de página

  - Quando há menos de três cópias íntegras disponíveis (apenas ativa ou passiva; cópias de banco de dados com retardamento não são contadas) por mais de 24 horas

No Exchange 2010, a correção de página não estava disponível para cópias com retardamento. No Exchange 2013, a correção de página está disponível para cópias com retardamento por meio desse recurso de descarte automático. Se o sistema detectar que a correção de páginas é necessária para uma cópia com retardamento, os logs serão automaticamente reproduzidos na cópia com retardamento para a correção das páginas. As cópias com retardamento também chamarão esse recurso de reprodução automática quando um limite de pouco espaço em disco for atingido e quando a cópia com retardamento tiver sido detectada como a única disponível para um período específico.

O comportamento de descarte da cópia com retardamento está desabilitado por padrão e pode ser habilitado pela execução do seguinte comando.

```powershell
Set-DatabaseAvailabilityGroup <DAGName> -ReplayLagManagerEnabled $true
```

Uma vez habilitado, o descarte ocorrerá quando houver menos de três cópias. Você pode alterar o valor padrão de 3 modificando o seguinte valor do registro DWORD.

**HKLM\\Software\\Microsoft\\ExchangeServer\\v15\\Replay\\Parameters\\ReplayLagManagerNumAvailableCopies**

Para habilitar o descarte de limites de pouco espaço em disco, será preciso configurar a seguinte entrada do Registro.

**HKLM\\Software\\Microsoft\\ExchangeServer\\v15\\Replay\\Parameters\\ReplayLagLowSpacePlaydownThresholdInMB**

Após configurar essas configurações de Registro, reinicie o serviço de Gerenciamento do Microsoft Exchange DAG para fazer com que as alterações entrem em vigor.

Como um exemplo, considere um ambiente em que um dado banco de dados tenha 4 cópias ( 3 cópias com disponibilidade alta e 1 cópia com atraso) e a configuração padrão seja usada para *ReplayLagManagerNumAvailableCopies*. Se uma cópia sem atraso estiver fora de serviço por qualquer motivo (por exemplo, se estiver suspensa, etc) então uma cópia com atraso vai desprezar automaticamente os arquivos de log em 24 horas.

## Aprimoramentos de alerta de cópia único

Garantir que seus servidores estejam operando confiavelmente e que suas cópias de bancos de dados de caixa de correio sejam íntegras são os principais objetivos das operações diárias de mensagens do Exchange 2013. É necessário monitorar ativamente o hardware, o sistema operacional Windows e os serviços do Exchange. Mas, ao executar em um ambiente de resiliência de caixa de correio do Exchange 2013, é importante monitorar a integridade e o status do DAG e suas cópias de banco de dados de caixa de correio. É especialmente vital executar o gerenciamento de riscos de redundância de dados e monitorar os períodos em que um banco de dados replicado fica reduzido a apenas uma única cópia. Isso é particularmente crucial em ambientes que não usam RAID e, em vez disso, implantam configurações de JBOD. Em um ambiente RAID, uma única falha de disco não afeta uma cópia de banco de dados de caixa de correio ativa. Entretanto, em um ambiente JBOD, uma única falha de disco disparará um failover de banco de dados.

No Exchange 2010, o script chamado CheckDatabaseRedundancy.ps1 foi introduzido. Como seu nome sugere, a finalidade do script é monitorar a redundância de bancos de dados de caixa de correio replicados, confirmando que há pelo menos duas cópias configuradas, íntegras e atualizadas, e alertar um administrador por meio de geração de log de eventos quando houver somente uma cópia íntegra de um banco de dados replicado. Nesse caso, tanto cópias ativas como passivas são contadas ao determinar a redundância.

As condições de cópia única incluem, sem limitações:

  - Falha de uma cópia ativa para replicar para qualquer cópia passiva.

  - Falha de todas as cópias passivas, que inclui os estados FailedAndSuspended e Falha, além de estados íntegros em que a cópia está atrás na reprodução ou na cópia de log. Observe que as cópias com retardamento não serão consideradas como estando atrás se elas estiverem dentro dos dez minutos na reprodução de seus logs para seu período de retardamento.

  - Falha do sistema em precisamente conhecer a geração de log atual da cópia ativa.

Como é importante para os administradores saberem quando estão com apenas uma cópia íntegra de um banco de dados, o script CheckDatabaseRedundancy.ps1 foi substituído por uma funcionalidade integrada e nativa que faz parte do Conjunto de Integridade DataProtection da disponibilidade gerenciada.

A funcionalidade nativa ainda alerta os administradores por meio de notificações de log de eventos e para distinguir os alertas de Exchange 2013 de Exchange 2010, Exchange 2013 usa as seguintes IDs de evento:

  - Evento 4138 (alerta vermelho)

  - Evento 4139 (alerta verde)

No Exchange 2013, a funcionalidade nativa foi aprimorada para reduzir o nível de ruído de alerta que pode ocorrer quando vários bancos de dados no mesmo servidor entram em uma condição de cópia única. No Exchange 2010, foram gerados alertas de cópia única, por banco de dados. Como resultado, quando ocorrer um problema no lado do servidor que afete vários bancos de dados e várias cópias de banco de dados, poderão ocorrer tempestades de alertas. Como várias falhas, como problemas de controlador ou memória, ocorrem no lado do servidor, há uma probabilidade moderadamente maior de tal tempestade de alerta ocorrer para cada incidente de servidor. No Exchange 2013, os alertas são agora gerados por servidor. Quando uma interrupção afeta todo um servidor, e a redundância de dados se torna um risco para várias cópias de banco de dados, um alerta único por servidor é gerado agora.

## Autoconfiguração de rede do DAG

Uma rede do DAG é uma coleção de uma ou mais sub-redes usadas para tráfego de replicação ou tráfego MAPI. Cada DAG contém um máximo de uma rede MAPI e zero ou mais redes de replicação. No Exchange 2010, as redes DAG iniciais (por exemplo, DAGNetwork01 e DAGNetwork02) criadas pelo sistema têm como base as sub-redes enumeradas pelo serviço de Cluster. Nos ambientes em que várias redes são usadas, e as interfaces de uma determinada rede (por exemplo, a rede MAPI) estavam na mesma sub-rede, havia pouca configuração adicional que um administrador precisava executar. Entretanto, nos ambientes em que as interfaces de uma determinada rede estavam em várias sub-redes, o administrador precisava executar uma tarefa conhecida como recolhimento de redes do DAG.

Em Exchange 2013, o recolhimento das redes DAG não é mais necessário. O Exchange 2013 ainda usa os mesmos mecanismos de detenção para distinguir entre as redes MAPI e de Replicação, mas agora as redes do DAG são recolhidas automaticamente, conforme apropriado.

Além disso, por padrão, as redes do DAG são agora automaticamente gerenciadas pelo sistema. Para exibir as propriedades da rede do DAG usando o Centro de Administração do Exchange (EAC), você deverá configurar o DAG para controle de rede manual modificando as propriedades do DAG usando o EAC, ou utilizando o cmdlet **Set-DatabaseAvailabilityGroup** para definir o parâmetro *ManualDagNetworkConfiguration* como `True`.

## Mudanças para seleção de melhor cópia

A seleção de melhor cópia (BCS) é um processo de algoritmo interno para localizar a melhor cópia de um banco de dados individual a ser ativado, dada uma lista de cópias potenciais para ativação e sua integridade e seu status. O Active Manager seleciona a melhor cópia disponível (e desbloqueada) para se tornar a nova cópia de banco de dados ativa quando a cópia de banco de dados ativa existente falhar ou um administrador executar uma alternância sem destino. No Exchange 2010, o processo de BCS avaliava vários aspectos de cada cópia de banco de dados para determinar a melhor cópia a ser ativada. Isso incluía:

  - Comprimento da fila de cópia

  - Comprimento da fila de repetição

  - Status do banco de dados

  - Status do índice de conteúdo

No Exchange 2013, o Active Manager executa as mesmas verificações e fases de BCS para determinar a integridade da replicação, mas agora inclui o uso de uma restrição em ordem decrescente de estados de integridade. Devido a essas mudanças, a BCS é agora chamada de seleção de melhor cópia e servidor (BCSS).

A BCSS inclui diversas verificações de integridade novas que fazem parte dos componentes integrados de disponibilidade gerenciada no Exchange 2013. Existem quatro novas verificações adicionais executadas pelo Active Manager (listadas na ordem em que são executadas):

1.  **Tudo Íntegro**   Verifica se há um servidor que hospeda uma cópia do banco de dados afetado que tenha todos os componentes de monitoramento em um estado íntegro.

2.  **Até Integridade Normal**   Verifica se há um servidor que hospeda uma cópia do banco de dados afetado que tenha todos os componentes de monitoramento com prioridade Normal em um estado íntegro.

3.  **Tudo Melhor que Fonte**   Verifica se há um servidor que hospeda uma cópia do banco de dados afetado que tenha componentes de monitoramento em um estado melhor que o servidor atual que hospeda a cópia afetada.

4.  **Mesmo que Fonte**   Verifica se há um servidor que hospeda uma cópia do banco de dados afetado que tenha componentes de monitoramento em um estado igual ao do servidor atual que hospeda a cópia afetada.

Se a BCSS for chamada como um resultado de um failover disparado por um componente de monitoramento de disponibilidade gerenciada (por exemplo, por meio de um respondente de Failover), uma restrição obrigatória adicional será aplicada onde a integridade de componentes do servidor de destino deve ser melhor que o servidor em que o failover ocorreu. Por exemplo, se uma falha do Microsoft Office Outlook Web App disparar um failover de disponibilidade gerenciada por meio de um respondente de Failover, a BCSS deverá selecionar um servidor que hospeda uma cópia do banco de dados afetado em que o Outlook Web App é integro.

## Serviço de gerenciamento de DAG

Atualização cumulativa 2 (CU2) para a versão Release to Manufacturing (RTM) do Exchange 2013 contém um novo serviço em servidores de caixa de correio que são membros de um DAG. Este serviço é chamado de Microsoft Exchange DAG Management Service (MSExchangeDAGMgmt). Este novo serviço contém funcionalidade de monitoramento DAG interna que anteriormente era executada dentro do serviço de Replicação do Microsoft Exchange (MSExchangeRepl).

## DAGs sem um ponto de acesso administrativo de cluster

Todos os DAGs em execução no Windows Server 2008 R2 ou no Windows Server 2012 exigem pelo menos um endereço IP em todas as sub-redes incluídas na rede MAPI. Os endereços IP atribuídos ao DAG são usados pelo cluster do DAG com o ponto de acesso administrativo do cluster (também conhecido como o nome de rede do cluster) para habilitar a resolução de nomes e a conectividade para o cluster (ou, mais precisamente, a conectividade com o membro do cluster que atualmente é proprietário do grupo de recursos principal do cluster) usando o nome do cluster. O Windows Server 2012 R2 permite que você crie um cluster de failover sem um ponto de acesso administrativo. Os clusters de failover do Windows sem pontos de acesso administrativos têm as seguintes características:

  - Não há endereço IP atribuído ao cluster e, portanto, nenhum Recurso de Endereço IP no grupo de recursos principais do cluster.

  - Não há um nome de rede atribuído ao cluster e, portanto, nenhum Recurso de Nome de Rede no grupo de recursos principais do cluster.

  - O nome do cluster não é registrado no DNS e não pode ser resolvido na rede.

  - Um objeto de nome do cluster (CNO) é criado no Active Directory.

  - O cluster de failover do Windows não pode ser gerenciado usando a ferramenta Gerenciamento de Cluster de Failover. O gerenciamento deve ser feito com o Windows PowerShell e os cmdlets do PowerShell devem ser executados em membros individuais do cluster.

Ao executar no Windows Server 2012 R2 ou posterior, o Service Pack 1 (SP1) para Exchange 2013 e posterior permite que você crie um DAG sem um ponto de acesso administrativo de cluster. Você pode criar um DAG sem um ponto de acesso administrativo usando o Centro de Administração do Exchange ou usando o Shell. Para obter mais informações, consulte [Creating DAGs](managing-database-availability-groups-exchange-2013-help.md) e [Criar um grupo de disponibilidade do banco de dados](create-a-database-availability-group-exchange-2013-help.md).

