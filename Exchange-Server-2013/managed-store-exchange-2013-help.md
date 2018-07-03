---
title: 'Repositório Gerenciado: Exchange 2013 Help'
TOCTitle: Repositório Gerenciado
ms:assetid: efdaf80b-335c-491c-8eb5-1fafd297e8a2
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Dn792020(v=EXCHG.150)
ms:contentKeyID: 62607044
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Repositório Gerenciado

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2014-07-14_

Todas as versões anteriores do Exchange Server, do Exchange Server 4.0 para o Exchange Server 2010, oferecem suporte a execução de uma única instância do processo de armazenamento de informações (Store.exe) na função de servidor de caixa de correio. Essa única instância do repositório hospeda todos os bancos de dados no servidor: ativa, passivo com atraso e a recuperação. As arquiteturas anteriores do Exchange, não há pouca ou nenhuma, isolamento entre os diferentes bancos de dados hospedados em um servidor de caixa de correio. Um problema com um banco de dados de caixa de correio única tem o potencial de afetar negativamente todos os outros bancos de dados e falhas resultantes de uma corrupção de caixa de correio podem afetar o serviço para todos os usuários cujos bancos de dados são hospedados no servidor.

Outro desafio com uma única instância do repositório nas versões anteriores do Exchange é que o mecanismo de armazenamento extensível (ESE) dimensiona bem a 12 de 8 núcleos de processador, mas Além disso, os problemas de sincronização de comunicação e cache de entre processadores levam a escala negativa. Determinados hoje muito grandes servidores, com 16 + principais sistemas disponíveis, isso significa impor o desafio administrativo de gerenciar a afinidade de 12 de 8 núcleos para ESE e usar os outros núcleos para processos de não-Store (por exemplo, assistentes, Search Foundation, disponibilidade gerenciada, etc.). Além disso, a arquitetura anterior restrito dimensione para o processo de armazenamento.

Evolução consideravelmente o processo de Store.exe ao longo dos anos como o próprio evolução, Exchange Server, mas como um único processo, basicamente sua escalabilidade é limitada e representa um único ponto de falha. Devido a estes limites, Store.exe é ido no Exchange 2013 e substituída pela loja gerenciado.

## Repositório Gerenciado

O repositório gerenciado é o nome para o armazenamento de informações (também conhecido como o armazenamento) processa no Exchange Server 2013. O repositório gerenciado usa um modelo de processo do controlador/trabalhador que fornece failover de banco de dados mais rápido e de isolamento do processo de armazenamento. O repositório gerenciado também inclui um novo banco de dados estático cache mecanismo que substitui o algoritmo de buffer dinâmico nas versões anteriores do Exchange Server. No modelo de múltiplo processo usado pela loja gerenciado, há um processo de controlador de serviço de repositório único (no caso, Microsoft.Exchange.Store.Service.exe também conhecido como MSExchangeIS) e um processo de trabalho (no caso, Microsoft.Exchange.Store.Worker.exe) para cada banco de dados montado. Quando um banco de dados é montado, um novo processo de trabalho é instanciado que somente esse banco de dados de serviços. Quando um banco de dados é desmontado, o processo de trabalho ao banco de dados é encerrado.

Por exemplo, se você tiver 40 bancos de dados montados em um servidor, haverá 41 processos em execução para o repositório gerenciado, um para cada banco de dados e outro para o controlador de processo do serviço de repositório.

O controlador de processo do serviço de repositório é muito fina e muito confiável, mas se ele se tornar inativo ou é encerrado, todos os seus processos de trabalho die (eles detectará o processo do serviço controlador desapareceu e sair). O controlador do repositório de processo monitora a integridade de todos os processos de trabalho do repositório no servidor. Um encerramento em Gigabits e inesperado o Microsoft.Exchange.Store.Service.exe faz com que um failover imediato de todas as cópias de banco de dados ativo. O repositório gerenciado também integra-se com o serviço de replicação do Microsoft Exchange (MSExchangeRepl.exe) e o Gerenciador ativo. O processo controlador, processos de trabalho e o serviço de replicação funcionam juntas para oferecer maior disponibilidade e confiabilidade:

  - Processo do serviço de replicação do Microsoft Exchange (MSExchangeRepl.exe)
    
      - Responsável pela emissão montar e desmontar operações para o repositório
    
      - Inicia a ação de recuperação em falhas de banco de dados ou armazenamento relatado pelos respondentes loja, o mecanismo de armazenamento extensível (ESE) e disponibilidade gerenciada
    
      - Detecta falhas inesperadas de banco de dados
    
      - Fornece a interface administrativa para tarefas de gerenciamento

  - Processo do serviço de repositório/controlador (Microsoft.Exchange.Store.Service.exe)
    
      - Gerencia a cada tempo de vida do processo de trabalho com base nas operações de montagem e dismount recebidas do serviço de replicação
    
      - Trata solicitações de entrada do Gerenciador de controle de serviço do Windows
    
      - Os logs de itens de falha quando problemas do processo de trabalhador de repositório detectada (por exemplo, paralisar ou sair inesperada)
    
      - Finaliza o repositório de processos de trabalho no evento de failover de resposta

  - Processo de trabalho do repositório (Microsoft.Exchange.Store.Worker.exe)
    
      - Responsável pela execução de operações de RPC para caixas de correio em um banco de dados
    
      - Instância do ponto de extremidade RPC em processo de trabalho é o GUID do banco de dados
    
      - Fornece o cache de banco de dados para um banco de dados

## Algoritmo de cache de banco de dados estáticos

O algoritmo de cache de banco de dados conhecido como a alocação de buffer dinâmico que foi introduzido no Exchange Server 5.5 e também utilizado pelo armazenamento de informações no Exchange 2000 Server, o Exchange Server 2003, o Exchange Server 2007 e o Exchange Server 2010, desapareceu também do Exchange 2013. Exchange 2013 usa um algoritmo muito simple e objetivo para determinar o cache de banco de dados. O repositório gerenciado realocará não são mais dinamicamente cache entre bancos de dados quando ocorre failover, qual simplifica bastante o gerenciamento de cache interno. Em vez disso, a memória alocada para cada banco de dados cache (por exemplo, cada processo de trabalhador de armazenamento) é com base no número de cópias de banco de dados local e o valor de *MaximumActiveDatabases*, se configurado. Se o valor de *MaximumActiveDatabases* for maior que o número de cópias de banco de dados atual, o cálculo de cache se baseia no número de cópias de banco de dados.

O algoritmo de estático usado pelo Exchange 2013 aloca memória para o cache de ESE dos cada repositório de processo de trabalho com base na RAM física. Isso é conhecido como de um banco de dados *Cache de destino Max*. 25% da memória total do servidor que é alocada para o cache de ESE. Isso é conhecido como o *Tamanho do Cache de servidor de destino*.


> [!TIP]
> O servidor de destino de tamanho de Cache e, portanto, a quantidade de memória alocada para o repositório para o cache de ESE, podem ser substituídas usando o atributo <EM>msExchESEParamCacheSizeMax</EM> do objeto <EM>InformationStore</EM> no Active Directory (o valor configurado é o número de páginas de 32 KB alocar entre todos os processos de armazenamento).



Um estático este cache é alocado para cópias ativas e passivas. O processo de trabalho do repositório será o destino de Cache máximo alocado somente quando a manutenção de uma cópia do banco de dados ativo. Cópias passivas do banco de dados são alocadas 20% da máxima do Cache de destino. O restante é reservado pela loja e alocado para o processo de trabalho se o banco de dados faz a transição de passivos para ativo.

Destino de Cache máximo é calculado apenas durante a inicialização do repositório. Portanto, se você adicionar ou remove os bancos de dados ou cópias de banco de dados, você deve reiniciar o serviço do controlador de armazenamento (MSExchangeIS) para que o cache pode ser ajustado de acordo. Se o serviço não for reiniciado, então recém-criadas bancos de dados terá um destino de tamanho de cache menor que bancos de dados criado antes da inicialização do serviço. Nesse caso, a soma de destinos de tamanho de cache de banco de dados provavelmente exceder o servidor de destino de tamanho de Cache até que MSExchangeIS seja reiniciado.

## Cálculos do Cache de banco de dados de exemplo

A seguir é banco de dados de exemplo armazenamento em cache cálculos que se baseiam em configuração de memória e o banco de dados de um servidor caixa de correio.

**Exemplo 1**

Neste exemplo, o servidor de caixa de correio tem 48 GB de memória e ele hospeda dois bancos de dados ativos e dois bancos de dados passivos. Além disso, o parâmetro *MaximumActiveDatabases* não está configurado. Nesta configuração, a quantidade de cache de banco de dados é 3 GB para cada processo de trabalho de cópia de banco de dados ativos e 0,6 GB para cada processo de trabalho de cópia passiva do banco de dados. Aqui está como esses valores obtidos.

Para obter o servidor de destino de tamanho de Cache, multiplique a memória quantidade por 25%:

48 GB X 25% = 12 GB

Para obter o banco de dados de destino de Cache de Max, divida a meta de tamanho de Cache do servidor pelo número total de bancos de dados ativos e passivos:

12 GB / 4 bancos de dados = 3 GB

Para determinar a quantidade de memória usada para as cópias de banco de dados passiva, multiplique o banco de dados de destino de Cache de Max por 20%:

3 GB X 20% = 0,6 GB

Sem o 12 GB de memória atribuído para o servidor de destino de tamanho de Cache, 7,2 GB será sendo usado por processos de trabalho do banco de dados e 4,8 GB serão reservados pelo armazenamento de informações para as duas cópias do banco de dados passiva caso eles se tornam cópias ativas. Nesse caso, eles usarão seus destino de Cache máximo de 3 GB.

**Exemplo 2**

Neste exemplo, o servidor de caixa de correio também tem 48 GB de memória e hosts dois ativo bancos de dados e dois bancos de dados passivos; No entanto, o parâmetro *MaximumActiveDatabases* é configurado com um valor de 2. Nesta configuração, a quantidade de cache de banco de dados é 5 GB para cada processo de trabalho de cópia de banco de dados ativos e 0.2 GB para cada processo de trabalho de cópia passiva do banco de dados. Aqui está como esses valores obtidos.

Para obter o servidor de destino de tamanho de Cache, multiplique a memória quantidade por 25%:

48 GB X 25% = 12 GB

Para obter o banco de dados de destino de Cache de Max, divida o destino de tamanho de Cache do servidor pelo número total de banco de dados ativo, mais o número total de bancos de dados passivos multiplicado pelo 20%:

12 GB / (2A + (2 P X 20 %)) = 5 GB

Para determinar a quantidade de memória usada para as cópias de banco de dados passiva, multiplique o banco de dados de destino de Cache de Max por 20%:

5 GB X 20% = 1 GB

Sem o 12 GB de memória atribuído para o servidor de destino de tamanho de Cache, 12 GB será sendo usado por processos de trabalho do banco de dados e a memória não será reservada pelo armazenamento de informações para as duas cópias do banco de dados passiva porque elas não podem se tornar cópias ativas nessa configuração (porque *MaximumActiveDatabases* é configurado com um valor de 2 e já existem 2 cópias de banco de dados ativo no servidor).

