---
title: 'Contadores de desempenho do Exchange 2013: Exchange 2013 Help'
TOCTitle: Contadores de desempenho do Exchange 2013
ms:assetid: 9143dd77-7c30-4769-8de1-28c717cfa9e9
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Dn904093(v=EXCHG.150)
ms:contentKeyID: 63915392
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Contadores de desempenho do Exchange 2013

 

_**Aplica-se a:**Exchange Server 2013_

_**Tópico modificado em:**2017-02-06_

## Contadores de desempenho do Exchange 2013

As seções a seguir listam os contadores de desempenho úteis que você pode utilizar ao solucionar problemas de desempenho do Exchange 2013.

## Contadores de conectividade do controlador de domínio do Exchange

As tabelas a seguir exibe informações sobre contadores de conectividade do controlador de domínio do Exchange e limites aceitáveis.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Contador</th>
<th>Descrição</th>
<th>Limite</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Tempo de leitura \LDAP do MSExchange ADAccess domínio controladores (*)</p></td>
<td><p>Mostra o tempo em milissegundos (ms) para enviar um LDAP leia a solicitação para o controlador de domínio especificado e recebe uma resposta.</p></td>
<td><p>Deve estar abaixo de 50 ms em média. Os picos (valores máximos) não devem ser mais que 100 ms.</p></td>
</tr>
<tr class="even">
<td><p>Tempo de pesquisa do MSExchange ADAccess domínio controladores (*) \LDAP</p></td>
<td><p>Mostra o tempo (em ms) para enviar uma solicitação de pesquisa LDAP e recebe uma resposta.</p></td>
<td><p>Deve estar abaixo de 50 ms em média. Os picos (valores máximos) não devem ser mais que 100 ms.</p></td>
</tr>
<tr class="odd">
<td><p>Tempo de leitura \LDAP (*) de processos do MSExchange ADAccess</p></td>
<td><p>Mostra o tempo (em ms) para enviar a que solicitação para o controlador de domínio especificado de leitura de um LDAP e recebe uma resposta.</p></td>
<td><p>Deve estar abaixo de 50 ms em média. Os picos (valores máximos) não devem ser mais que 100 ms.</p></td>
</tr>
<tr class="even">
<td><p>Tempo de pesquisa (*) \LDAP de processos do MSExchange ADAccess</p></td>
<td><p>Mostra o tempo (em ms) para enviar uma solicitação de pesquisa LDAP e recebe uma resposta.</p></td>
<td><p>Deve estar abaixo de 50 ms em média. Os picos (valores máximos) não devem ser mais que 100 ms.</p></td>
</tr>
</tbody>
</table>


## Processador e contadores de processo

As tabelas a seguir exibe informações sobre contadores de processo e processadores e limites aceitáveis.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Contador</th>
<th>Descrição</th>
<th>Limite</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Processador ( total) \ % tempo do processador</p></td>
<td><p>Mostra a porcentagem de tempo que o processador está executando o aplicativo ou processos do sistema operacional. Isso é quando o processador não está ocioso.</p></td>
<td><p>Deve ser menor que 75% em média.</p></td>
</tr>
<tr class="even">
<td><p>Processador ( total) \ % tempo de usuário</p></td>
<td><p>Mostra a porcentagem de tempo de processador gasto no modo de usuário. Modo de usuário é um modo de processamento restrito projetado para aplicativos, subsistemas de ambiente e subsistemas integrais.</p></td>
<td><p>Deve ser menor que 75% em média.</p></td>
</tr>
<tr class="odd">
<td><p>Processador ( total) \ % tempo privilegiado</p></td>
<td><p>Mostra a porcentagem de tempo de processador gasto no modo privilegiado. Modo privilegiado é um modo de processamento projetado para componentes do sistema operacional e drivers de manipulação de hardware. Permite acesso direto ao hardware e toda a memória.</p></td>
<td><p>Deve ser menor que 75% em média.</p></td>
</tr>
<tr class="even">
<td><p>Sistema\comprimento da fila (todas as instâncias)</p></td>
<td><p>Indica o número de threads que está atendendo a cada processador. Comprimento da fila de processador pode ser usado para identificar se contenção de processador ou alta utilização da CPU é causada pela capacidade do processador que está sendo insuficiente para lidar com cargas de trabalho atribuídas a ele. Comprimento da fila de processador mostra o número de segmentos que estão atrasadas na fila pronto do processador e estão aguardando para ser agendado para execução. O valor listado é o último valor observado no momento que a medida foi feita.</p></td>
<td><p>Não deve ser maior que 5 por processador.</p></td>
</tr>
<tr class="odd">
<td><p>Processo (*) \ % tempo do processador</p></td>
<td><p>Pode ser usado para identificar o consumo de CPU de processos específicos.</p></td>
<td><p>Não aplicável</p></td>
</tr>
</tbody>
</table>


## Contadores de memória

As tabelas a seguir exibe informações sobre contadores de memória e limites aceitáveis.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Contador</p></td>
<td><p>Descrição</p></td>
<td><p>Limite</p></td>
</tr>
<tr class="even">
<td><p>Memória \ Mbytes disponíveis</p></td>
<td><p>Mostra a quantidade de memória física, em megabytes (MB), imediatamente disponíveis para alocação para um processo ou para uso do sistema. É igual a soma de memória atribuído para o standby (em cache), livre, e listas de zero página. Para obter uma explicação completa o Gerenciador de memória, consulte Microsoft Developer Network (MSDN) ou &quot;System Performance and Troubleshooting Guide&quot; no Windows Server 2003 Resource Kit.</p></td>
<td><p>Deve permanecer acima de 5% do total de RAM.</p></td>
</tr>
<tr class="odd">
<td><p>Memory\% confirmadas Bytes em uso</p></td>
<td><p>Mostra a taxa de Bytes Memory\Committed ao limite Memory\Commit. Memória confirmada é a memória física em uso para o qual o espaço reservado no arquivo de paginação deve ele precisarão ser gravadas no disco. O limite de confirmação é determinado pelo tamanho do arquivo de paginação. Se o arquivo de paginação é ampliado, o limite de confirmação aumenta e a proporção é reduzida. Esse contador exibe o valor de porcentagem atual apenas; não é uma média.</p></td>
<td><p>Se esse valor for mais de 80%, é uma indicação de que o sistema é provável sob tensão para fornecer mais memória.</p></td>
</tr>
</tbody>
</table>


## Contadores do .NET framework

As tabelas a seguir exibe informações sobre contadores do .NET Framework e limites aceitáveis.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Contador</p></td>
<td><p>Descrição</p></td>
<td><p>Limite</p></td>
</tr>
<tr class="even">
<td><p>Memória do .NET CLR (*) \ % tempo gasto em CL</p></td>
<td><p>Mostra quando a coleta de lixo ocorreu. Quando o contador excede o limite, ele indica que o CPU é limpando e não está sendo usada com eficiência de carga. Adicionando memória ao servidor aumentaria essa situação.</p></td>
<td><p>Deve estar abaixo de 10% em média.</p></td>
</tr>
<tr class="odd">
<td><p>Exceções do .NET CLR (*) \ n º de Excepts iniciadas / s</p></td>
<td><p>Exibe o número de exceções iniciadas por segundo. Eles incluem as exceções do .NET Framework e as exceções não gerenciadas que são convertidas em exceções do .NET Framework. Por exemplo, a exceção de referência do ponteiro nulo em código não gerenciado seria obter lançada novamente em código gerenciado estão Framework. Este contador inclui exceções manipuladas e não tratadas.</p></td>
<td><p>Deve ser menor que 5% do total de solicitações por segundo (RPS) (servidor Web ( total) \Connection. tentativas de s *.05).</p></td>
</tr>
<tr class="even">
<td><p>Memória .NET CLR (*) \ n º de Bytes em todas as pilhas</p></td>
<td><p>Mostra a soma dos quatro outros contadores: tamanho do Heap Ger 0, tamanho do Heap Ger 1, tamanho do Heap Ger 2 e tamanho de Heap de objeto grande. Esse contador indica a memória atual alocada em bytes no GC pilhas.</p></td>
<td><p>Não aplicável</p></td>
</tr>
</tbody>
</table>


## Contadores de rede

As tabelas a seguir exibe informações sobre contadores de rede comuns e limites aceitáveis.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Contador</p></td>
<td><p>Descrição</p></td>
<td><p>Limite</p></td>
</tr>
<tr class="even">
<td><p>Interface de Rede(*)\Erros de Saída dos Pacotes</p></td>
<td><p>Indica o número de pacotes de saída que não puderam ser transmitidos devido a erros.</p></td>
<td><p>Deve ser sempre 0.</p></td>
</tr>
<tr class="odd">
<td><p>TCPv6\Falhas de Conexão</p></td>
<td><p>Mostra o número de conexões TCP para o qual o estado atual é estabelecido ou CLOSE-WAIT. O número de conexões TCP que podem ser estabelecidas é restrito pelo tamanho do pool não paginado. Quando o pool não paginado é esvaziado, novas conexões não pode ser estabelecido.</p></td>
<td><p>Não aplicável</p></td>
</tr>
<tr class="even">
<td><p>TCPv4\Redefinição de Conexões</p></td>
<td><p>Mostra o número de vezes que conexões TCP fizeram uma transação direta do estado ESTABLISHED ou CLOSE-WAIT para o estado CLOSED.</p></td>
<td><p>Um número crescente de redefinições ou uma taxa consistentemente aumento de redefinições de pode indicar uma escassez de largura de banda.</p></td>
</tr>
<tr class="odd">
<td><p>TCPv6\Redefinição de Conexões</p></td>
<td><p>Mostra o número de vezes que conexões TCP fizeram uma transação direta do estado ESTABLISHED ou CLOSE-WAIT para o estado CLOSED.</p></td>
<td><p>Um número crescente de redefinições ou uma taxa consistentemente aumento de redefinições pode indicar uma falta de largura de banda.</p></td>
</tr>
</tbody>
</table>


## Contadores de logon de rede

As tabelas a seguir exibe informações sobre comuns contadores para monitorar os problemas de autenticação NTLM e MaxConcurrentAPI e limites aceitáveis. Consulte o Microsoft Knowledge Base artigo 2688798 [como fazer o ajuste de desempenho para a autenticação NTLM usando a configuração de MaxConcurrentAPI](https://go.microsoft.com/fwlink/p/?linkid=389728) , para obter mais informações.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Contador</p></td>
<td><p>Descrição</p></td>
<td><p>Limite</p></td>
</tr>
<tr class="even">
<td><p>\Netlogon\Semaphore waiters</p></td>
<td><p>O número do thread que está aguardando para obter o semáforo.</p></td>
<td><p>Consulte o artigo da Base de Conhecimento Microsoft 2688798 <a href="https://go.microsoft.com/fwlink/p/?linkid=389728">como fazer o ajuste de desempenho para a autenticação NTLM, usando a configuração MaxConcurrentAPI</a></p></td>
</tr>
<tr class="odd">
<td><p>Proprietários de \Netlogon\Semaphore</p></td>
<td><p>O número do thread que está mantendo o semáforo.</p></td>
<td><p>Não aplicável</p></td>
</tr>
<tr class="even">
<td><p>Adquire \Netlogon\Semaphore</p></td>
<td><p>O número total de vezes que o semáforo tenha sido obtido no decorrer da conexão do canal de segurança, ou desde a inicialização do sistema para total.</p></td>
<td><p>Não aplicável</p></td>
</tr>
<tr class="odd">
<td><p>Tempos limite de \Netlogon\Semaphore</p></td>
<td><p>O número total de vezes que um segmento esgotou enquanto ele aguardou para o sinal no decorrer da conexão do canal de segurança, ou desde a inicialização do sistema para total.</p></td>
<td><p>Não aplicável</p></td>
</tr>
<tr class="even">
<td><p>Tempo de espera do semáforo \Netlogon\Average</p></td>
<td><p>O tempo médio (em segundos) que o semáforo é mantido sobre a última amostra.</p></td>
<td><p>Não aplicável</p></td>
</tr>
</tbody>
</table>


## Contadores do Banco de Dados

A tabela a seguir mostra os contadores de requisitos de latência de e/s log ativo e seus limites aceitáveis. Quando os limites são excedidos, cai a experiência do cliente. Por exemplo, os usuários podem enfrentar atrasos de entrega de mensagem ou lento o desempenho do sistema.


> [!TIP]
> Orientação de latência de armazenamento normal no Exchange 2013 é muito semelhante para acessar as diretrizes do Exchange 2010. Contadores de bancos de dados adicionais podem ser encontrados no <A href="https://go.microsoft.com/fwlink/p/?linkid=525622">Contadores de servidor de caixa de correio</A>.




<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Contador</p></td>
<td><p>Descrição</p></td>
<td><p>Limite</p></td>
</tr>
<tr class="even">
<td><p>Banco de dados do MSExchange = = &gt; banco de dados \I/O de instâncias (*) lê a latência média (anexada)</p></td>
<td><p>Mostra a duração média de tempo, em milissegundos (ms) por operação de leitura do banco de dados.</p></td>
<td><p>Deve ser menor que 20 ms em média.</p></td>
</tr>
<tr class="odd">
<td><p>Banco de dados do MSExchange = = &gt; banco de dados \I/O de instâncias (*) grava latência média (anexada)</p></td>
<td><p>Indica o intervalo de tempo médio, em ms, por operação de gravação de banco de dados.</p></td>
<td><p>Deve ser menor que 50 ms em média.</p></td>
</tr>
<tr class="even">
<td><p>Banco de dados do MSExchange = = &gt; instâncias (*) latência média de gravações do Log de \I/O</p></td>
<td><p>Mostra a duração média de tempo, em ms, por operação de gravação de Log.</p></td>
<td><p>Deve ser menor do que 10 ms em média.</p></td>
</tr>
<tr class="odd">
<td><p>Banco de dados do MSExchange = = &gt; banco de dados \I/O de instâncias (*) lê a latência média (recuperação)</p></td>
<td><p>Mostra a duração média de tempo, em ms, por banco de dados passivo operação de leitura.</p></td>
<td><p>Deve ser menor que 200 ms em média.</p></td>
</tr>
<tr class="even">
<td><p>Banco de dados do MSExchange = = &gt; banco de dados \I/O de instâncias (*) grava a latência média (recuperação)</p></td>
<td><p>Mostra a duração média de tempo, em ms, por operação de gravação do banco de dados passiva.</p></td>
<td><p>Deve menos que a latência de leitura para a mesma instância, medido pelo banco de dados do MSExchange ser = = &gt; instâncias (*) \I/O banco de dados lê (recuperação) contador da latência média.</p></td>
</tr>
<tr class="odd">
<td><p>Banco de dados do MSExchange = = &gt; instâncias (*) \I/O banco de dados leituras (anexadas) / s</p></td>
<td><p>Mostra a quantidade de operações por segundo para cada instância de banco de dados anexado de leitura do banco de dados.</p></td>
<td><p>Não aplicável</p></td>
</tr>
<tr class="even">
<td><p>Banco de dados do MSExchange = = &gt; instâncias (*) \I/O gravações banco de dados (anexadas) / s</p></td>
<td><p>Mostra a quantidade de operações de gravação do banco de dados por segundo para cada instância de banco de dados anexado.</p></td>
<td><p>Não aplicável</p></td>
</tr>
<tr class="odd">
<td><p>Banco de dados do MSExchange = = &gt; instâncias (*) \I/O Log gravações/s</p></td>
<td><p>Mostra o número de log gravações por segundo para cada instância de banco de dados.</p></td>
<td><p>Não aplicável</p></td>
</tr>
<tr class="even">
<td><p>Montado do MSExchange Active Manager ( total) \Database</p></td>
<td><p>Mostra o número de cópias de banco de dados ativos no servidor.</p></td>
<td><p>Não aplicável</p></td>
</tr>
</tbody>
</table>


## ASP.NET

As tabelas a seguir exibe informações sobre contadores do ASP.NET e limites aceitáveis.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Contador</p></td>
<td><p>Descrição</p></td>
<td><p>Limite</p></td>
</tr>
<tr class="even">
<td><p>Reinicializações de ASP.NET\Application</p></td>
<td><p>Mostra a quantidade de vezes que o aplicativo foi reiniciado durante o tempo de vida do servidor Web.</p></td>
<td><p>Deve ser sempre 0.</p></td>
</tr>
<tr class="odd">
<td><p>Reinicializações de processo de ASP.NET\Worker</p></td>
<td><p>Mostra a quantidade de vezes que um processo de trabalho foi reiniciado no computador.</p></td>
<td><p>Deve ser sempre 0.</p></td>
</tr>
<tr class="even">
<td><p>Tempo de espera de ASP.NET\Request</p></td>
<td><p>Mostra a quantidade de ms que a solicitação mais recente aguardou na fila.</p></td>
<td><p>Deve ser sempre 0.</p></td>
</tr>
<tr class="odd">
<td><p>ASP.NET aplicativos (*) \Requests na fila de aplicativos</p></td>
<td><p>Mostra o número de solicitações na fila de solicitação de aplicativo.</p></td>
<td><p>Deve ser sempre 0.</p></td>
</tr>
<tr class="even">
<td><p>Execução do ASP.NET aplicativos (*) \Requests</p></td>
<td><p>Mostra o número de solicitações em execução no momento.</p></td>
<td><p>Não aplicável</p></td>
</tr>
<tr class="odd">
<td><p>ASP.NET aplicativos (*) \Requests/Sec</p></td>
<td><p>Mostra o número de solicitações executadas por segundo.</p></td>
<td><p>Não aplicável</p></td>
</tr>
</tbody>
</table>


## Contadores de acesso de cliente RPC

As tabelas a seguir exibe informações sobre contadores de acesso para cliente RPC e limites aceitáveis.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Contador</p></td>
<td><p>Descrição</p></td>
<td><p>Limite</p></td>
</tr>
<tr class="even">
<td><p>Latência média do MSExchange RpcClientAccess\RPC</p></td>
<td><p>Mostra a latência, em milissegundos (ms), uma média dos últimos 1.024 pacotes.</p></td>
<td><p>Deve estar abaixo 250 ms.</p></td>
</tr>
<tr class="odd">
<td><p>Solicitações de RpcClientAccess\RPC do MSExchange</p></td>
<td><p>Mostra o número de solicitações de cliente sendo processado pelo serviço de acesso para cliente RPC.</p></td>
<td><p>Não deve ser a mais de 40.</p></td>
</tr>
<tr class="even">
<td><p>Contagem de usuários do MSExchange RpcClientAccess\Active</p></td>
<td><p>Mostra o número de usuários exclusivos que mostraram alguma atividade nos últimos 2 minutos.</p></td>
<td><p>Não aplicável</p></td>
</tr>
<tr class="odd">
<td><p>Do MSExchange RpcClientAccess\Connection contagem</p></td>
<td><p>Mostra o número total de cliente conexões mantidas.</p></td>
<td><p>Não aplicável</p></td>
</tr>
<tr class="even">
<td><p>Operações do MSExchange RpcClientAccess\RPC/seg.</p></td>
<td><p>Mostra a tarifa na qual RPC operações ocorrem, por segundo.</p></td>
<td><p>Não aplicável</p></td>
</tr>
<tr class="odd">
<td><p>Contagem de RpcClientAccess\User do MSExchange</p></td>
<td><p>Mostra a quantidade de usuários conectados ao serviço.</p></td>
<td><p>Não aplicável</p></td>
</tr>
</tbody>
</table>


## Contadores de Proxy HTTP

As tabelas a seguir exibe informações sobre contadores de HTTP Proxy.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Contador</p></td>
<td><p>Descrição</p></td>
</tr>
<tr class="even">
<td><p>Latência média de \MailboxServerLocator MSExchange HttpProxy (*)</p></td>
<td><p>Mostra a latência média (ms) das chamadas de serviço web MailboxServerLocator.</p></td>
</tr>
<tr class="odd">
<td><p>Latência de autenticação \Average MSExchange HttpProxy (*)</p></td>
<td><p>Mostra o tempo médio gasto na autenticação de solicitações de CAS sobre as últimas 200 amostras.</p></td>
</tr>
<tr class="even">
<td><p>Latência de processamento do servidor do MSExchange HttpProxy (*) \Average ClientAccess</p></td>
<td><p>Mostra a latência média (ms) de tempo de processamento de CAS (não inclui o tempo gasto proxy) sobre as últimas 200 solicitações.</p></td>
</tr>
<tr class="odd">
<td><p>Taxa de falha do MSExchange HttpProxy (*) \Mailbox servidor Proxy</p></td>
<td><p>Mostra a porcentagem de conectividade relacionadas falhas entre o servidor acesso para cliente e servidores MBX sobre as últimas 200 amostras.</p></td>
</tr>
<tr class="even">
<td><p>Solicitações de Proxy de \Outsanding MSExchange HttpProxy (*)</p></td>
<td><p>Mostra o número de solicitações simultâneas proxy pendentes.</p></td>
</tr>
<tr class="odd">
<td><p>MSExchange HttpProxy (*) \Proxy solicitações/s</p></td>
<td><p>Mostra o número de solicitações de proxy processadas a cada segundo.</p></td>
</tr>
<tr class="even">
<td><p>\Requests/Sec MSExchange HttpProxy (*)</p></td>
<td><p>Mostra o número de solicitações processadas a cada segundo.</p></td>
</tr>
</tbody>
</table>


## Contadores de armazenamento de informações

As tabelas a seguir exibe informações sobre contadores de armazenamento de informações e limites aceitáveis.


> [!TIP]
> Orientação de latência normal de armazenamento no Exchange 2013 é muito semelhante para acessar as diretrizes do Exchange 2010. Contadores de armazenamento de informações adicionais podem ser encontrados no <A href="https://go.microsoft.com/fwlink/p/?linkid=525622">Contadores de servidor de caixa de correio</A>.




<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Contador</p></td>
<td><p>Descrição</p></td>
<td><p>Limite</p></td>
</tr>
<tr class="even">
<td><p>Solicitações \RPC de armazenamento do MSExchange (*)</p></td>
<td><p>Indica as solicitações gerais de RPC executadas atualmente no processo do repositório de informações.</p></td>
<td><p>Deve ser sempre inferior a 70.</p></td>
</tr>
<tr class="odd">
<td><p>Latência média do \RPC MSExchangeIS cliente tipo (*)</p></td>
<td><p>Indica a latência média de RPC de um servidor, em ms, dos últimos 1.024 pacotes, para um determinado protocolo do cliente.</p></td>
<td><p>Deve ser inferior a 50 ms em média para cada cliente.</p></td>
</tr>
<tr class="even">
<td><p>Latência média de \RPC de armazenamento do MSExchange (*)</p></td>
<td><p>Média de latência de RPC (MS) é a latência média em milissegundos de solicitações RPC por banco de dados. Média é calculada sobre todos os RPCs desde que o exrpc32 foi carregado.</p></td>
<td><p>Deve ser menor que 50 ms em todos os momentos, com os picos 100ms menores.</p></td>
</tr>
<tr class="odd">
<td><p>Operações do armazenamento do MSExchange (*) \RPC/seg.</p></td>
<td><p>Mostra a quantidade de operações RPC por segundo para cada instância de banco de dados.</p></td>
<td><p>Não aplicável</p></td>
</tr>
<tr class="even">
<td><p>Cliente MSExchangeIS tipo (*) \RPC operações/s</p></td>
<td><p>Mostra a quantidade de operações RPC por segundo para cada conexão de tipo de cliente.</p></td>
<td><p>Não aplicável</p></td>
</tr>
</tbody>
</table>


## Contadores de servidor de acesso do cliente

As tabelas a seguir exibe informações sobre contadores de conexão do cliente e os contadores de serviços de informações da Internet (IIS).


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Contador</p></td>
<td><p>Descrição</p></td>
</tr>
<tr class="even">
<td><p>MSExchange ActiveSync\Requests/seg.</p></td>
<td><p>Mostra o número de solicitações HTTP recebidas do cliente via ASP.NET por segundo. Determina a taxa de solicitação Exchange ActiveSync atual. Usado somente para determinar a carga do usuário atual.</p></td>
</tr>
<tr class="odd">
<td><p>Do MSExchange ActiveSync\Ping comandos pendente</p></td>
<td><p>Mostra o número de ping comandos atualmente pendentes na fila.</p></td>
</tr>
<tr class="even">
<td><p>Comandos do MSExchange ActiveSync\Sync/seg.</p></td>
<td><p>Mostra o número de comandos sync processados por segundo. Clientes usam esse comando para sincronizar itens dentro de uma pasta.</p></td>
</tr>
<tr class="odd">
<td><p>Solicitações de Service\Availability MSExchange disponibilidade (s)</p></td>
<td><p>Mostra o número de solicitações atendidas por segundo. A solicitação pode ser apenas para as informações de livres / ocupadas ou incluir sugestões. Uma solicitação pode conter várias caixas de correio. Determina a taxa em que ocorrem as solicitações de serviço de disponibilidade.</p></td>
</tr>
<tr class="even">
<td><p>Usuários de MSExchange OWA\Current únicos</p></td>
<td><p>Mostra o número de usuários exclusivos atualmente conectado ao Outlook Web App. Esse valor monitora o número de sessões de usuários ativos exclusivos, para que os usuários sejam removidos este contador apenas depois que fizerem logoff ou suas sessões expire. Determina a carga do usuário atual.</p></td>
</tr>
<tr class="odd">
<td><p>MSExchange OWA\Requests/seg.</p></td>
<td><p>Mostra o número de solicitações manipuladas pelo Outlook Web App por segundo. Determina a carga do usuário atual.</p></td>
</tr>
<tr class="even">
<td><p>MSExchangeAutodiscover\Requests/sec</p></td>
<td><p>Mostra o número de solicitações de serviço de descoberta automática processadas a cada segundo. Determina a carga do usuário atual.</p></td>
</tr>
<tr class="odd">
<td><p>MSExchangeWS\Requests/sec</p></td>
<td><p>Mostra o número de solicitações processadas por segundo. Determina a carga do usuário atual.</p></td>
</tr>
<tr class="even">
<td><p>Conexões de \Current do Web Service ( total)</p></td>
<td><p>Mostra a quantidade atual de conexões estabelecidas com o serviço Web. Determina a carga do usuário atual.</p></td>
</tr>
<tr class="odd">
<td><p>Conexões de \Current do Web Service (Site padrão)</p></td>
<td><p>Mostra a quantidade atual de conexões estabelecidas ao site padrão que corresponde ao número de conexões visitando a função de servidor CAS de Front End. Determina a carga do usuário atual.</p></td>
</tr>
<tr class="even">
<td><p>Tentativas de \Connection. WebService ( total) / seg.</p></td>
<td><p>Mostra a taxa que conexões ao serviço da Web estão sendo tentadas. Determina a carga do usuário atual.</p></td>
</tr>
<tr class="odd">
<td><p>Web Service ( total) \Other solicitação de métodos/s</p></td>
<td><p>Mostra a taxa HTTP são feitas solicitações que não use as opções, obter, cabeça, postar, colocar, excluir, os métodos de rastreamento, MOVE, COPY, MKCOL, PROPFIND, PROPPATCH, pesquisa, bloquear ou desbloquear. Determina a carga do usuário atual.</p></td>
</tr>
</tbody>
</table>


## Contadores de gerenciamento de carga de trabalho

As tabelas a seguir exibe informações sobre contadores de gerenciamento de carga de trabalho do Exchange. Esses contadores são importantes para monitorar porque o gerenciamento de carga de trabalho pode executar tarefas em segundo plano horários de pico.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Contador</p></td>
<td><p>Descrição</p></td>
</tr>
<tr class="even">
<td><p>MSExchange WorkloadManagement cargas de trabalho (*) \ActiveTasks</p></td>
<td><p>Mostra a quantidade de tarefas ativas atualmente em execução em segundo plano para gerenciamento de carga de trabalho.</p></td>
</tr>
<tr class="odd">
<td><p>MSExchange WorkloadManagement cargas de trabalho (*) \CompletedTasks</p></td>
<td><p>Mostra a quantidade de carga de trabalho com tarefas de gerenciamento que tenham sido concluídas.</p></td>
</tr>
<tr class="even">
<td><p>Do MSExchange WorkloadManagement cargas de trabalho (*) \QueuedTasks</p></td>
<td><p>Mostra a quantidade de carga de trabalho com tarefas de gerenciamento que estão atualmente enfileiradas aguardando processamento.</p></td>
</tr>
</tbody>
</table>

