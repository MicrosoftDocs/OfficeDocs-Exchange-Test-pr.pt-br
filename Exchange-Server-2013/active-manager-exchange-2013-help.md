---
title: 'Active Manager: Exchange 2013 Help'
TOCTitle: Active Manager
ms:assetid: f4be27b7-1d7c-47b4-87ac-bfdfcc046f00
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Dd776123(v=EXCHG.150)
ms:contentKeyID: 50487006
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Active Manager

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2015-04-07_

O Microsoft Exchange Server 2013 possui um componente chamado *Active Manager*, que gerencia a plataforma de alta disponibilidade que inclui o grupo de disponibilidade de banco de dados (DAG) e as cópias de banco de dados de caixa de correio. O Active Manager é executado dentro do Serviço de Replicação do Microsoft Exchange (MSExchangeRepl.exe) em todos os servidores de Caixa de Correio. Em servidores de Caixa de Correio que não são membros de um DAG, há uma única função do Active Manager: *Active Manager Autônomo*. Em servidores que são membros de um DAG, há duas funções do Active Manager: *Active Manager Principal* (PAM) e *Active Manager em Espera* (SAM). PAM é a função do Active Manager em um DAG que decide quais cópias serão ativas e passivas. O PAM é responsável por obter notificações de alteração de topologia e reagir a falhas do servidor. O membro do DAG que hospeda a função PAM é sempre o membro que atualmente possui o recurso de quorum do cluster (grupo de cluster padrão). Se o servidor que possui o recurso de quorum do cluster falhar, a função PAM automaticamente é movida para um servidor sobrevivente, que se apropria do recurso de quorum do cluster. Além disso, se for preciso desligar o servidor que hospeda o recurso de quorum do cluster para manutenção ou atualização, você deve primeiro mover o PAM para outro servidor do DAG. O PAM controla todos os movimentos das designações ativas entre uma cópia de banco de dados. (Somente uma cópia pode estar ativa em um horário especificado, e essa cópia pode estar montada ou desmontada.) O PAM também executa as funções da função SAM no sistema local (detectando o banco de dados local e falhas do Armazenamento de Informações).

O SAM fornece informações sobre qual servidor hospeda a cópia ativa de um banco de dados de caixa de correio para outros componentes do Exchange que estão executando um componente cliente do Active Manager (por exemplo, os serviços de Acesso para Cliente ou de Transporte). O SAM detecta falhas de bancos de dados locais e do Armazenamento de Informações local. Ele reage a falhas pedido ao PAM que inicie um failover (caso o banco de dados seja replicado). Um SAM não determina o destino de um failover, nem atualiza o estado da localização do banco de dados no PAM. Ele acessará o estado da localização da cópia do banco de dados ativa para responder consultas na cópia ativa do banco de dados que recebe.


> [!NOTE]
> O Exchange 2013 não é um aplicativo em cluster. Ao invés disso, usa as funções da biblioteca do cluster implementadas na clusapi.dll para cluster, rede de cluster (pulsação), gerenciamento de nó, registro de cluster e algumas funções de código de controle. Além disso, o Active Manager armazena informações do banco de dados de caixa de correio atual (por exemplo, dados ativos e passivos e dados montados) no banco de dados de cluster (também conhecido como o registro de cluster). Embora as informações sejam armazenadas diretamente no banco de dados de cluster, não são acessadas diretamente por qualquer outro componente.



No Exchange 2013, o serviço de Replicação do Microsoft Exchange monitora periodicamente a integridade de todos os bancos de dados montados. Além disso, ele também monitora o Mecanismo de Armazenamento Extensível (ESE) para detectar qualquer erro ou falha de E/S. Quando o serviço detecta uma falha, o Active Manager é notificado. O Active Manager então determina qual cópia de banco de dados deve ser montada e o que é necessário para montar o banco de dados. Além disso, controla a cópia ativa de um banco de dados de caixa de correio (com base na última cópia montada do banco de dados) e fornece informações dos resultados de rastreamento para o servidor de Acesso para Cliente ao qual o cliente está conectado.

## Seleção de melhor cópia

Quando ocorre uma falha que impede o acesso à cópia ativa de um banco de dados de caixa de correio replicado, o Active Manager executa várias etapas para recuperar-se da falha, selecionando a melhor cópia passiva possível do banco de dados para ativação. Esse processo era conhecido como seleção de melhor cópia (BCS) no Exchange 2010 e é agora conhecido como seleção de melhor cópia e servidor (BCSS) no Exchange 2013. O processo geral ocorre na seguinte ordem:

1.  A Disponibilidade Gerenciada ou o Active Manager detecta uma falha, ou um administrador inicia uma alternância sem destino.

2.  O PAM executa o algoritmo interno de BCSS.

3.  Ocorre um processo chamado *tentativa de cópia de últimos logs* (ACLL), que tenta copiar os arquivos de log ausentes do servidor que hospedava a cópia do banco de dados ativa antes da falha ou da alternância.

4.  Quando o processo ACLL tiver sido concluído, o valor de *AutoDatabaseMountDial* para os servidores de Caixa de Correio que hospedam cópias do banco de dados é comparado com o tamanho da fila de cópia sendo ativada. Nesse momento:
    
      - O número de arquivos de log faltando é menor ou igual ao valor do *AutoDatabaseMountDial*, caso em que a Etapa 5 ocorre.
    
      - O número dos arquivos de log faltando é maior que o valor de *AutoDatabaseMountDial*, situação em que o Active Manager tentará ativar a próxima melhor cópia disponível, se houver uma.

5.  O PAM emite uma solicitação de montagem para o Repositório de Informações do Microsoft Exchange por meio de RPC (chamada de procedimento remoto). Nesse momento:
    
      - O banco de dados é montado e disponibilizado para clientes.
    
      - O banco de dados não é montado e o PAM executa as etapas 3 e 4 na próxima melhor cópia (caso alguma esteja disponível).

Em Exchange 2010, o processo BCS avaliadas vários aspectos de cada cópia do banco de dados para determinar a melhor cópia para ativar. Essas incluídos:

  - Comprimento da fila de cópia

  - Comprimento da fila de repetição

  - Status do banco de dados

  - Status do índice de conteúdo

No Exchange 2013, o Active Manager executa as mesmas verificações e fases de BCS, mas agora inclui o uso de uma restrição em ordem decrescente de estados de integridade. Especificamente, BCSS inclui diversas verificações de integridade novas que fazem parte dos componentes integrados de disponibilidade gerenciada no Exchange 2013. Existem quatro novas verificações adicionais executadas pelo Active Manager (listadas na ordem em que são executadas):

1.  **Tudo Íntegro**   Verifica se há um servidor que hospeda uma cópia do banco de dados afetado que tenha todos os componentes de monitoramento em um estado íntegro.

2.  **Até Integridade Normal**   Verifica se há um servidor que hospeda uma cópia do banco de dados afetado que tenha todos os componentes de monitoramento com prioridade Normal em um estado íntegro.

3.  **Tudo Melhor que Fonte**   Verifica se há um servidor que hospeda uma cópia do banco de dados afetado que tenha componentes de monitoramento em um estado melhor que o servidor atual que hospeda a cópia afetada.

4.  **Mesmo que Fonte**   Verifica se há um servidor que hospeda uma cópia do banco de dados afetado que tenha componentes de monitoramento em um estado igual ao do servidor atual que hospeda a cópia afetada.

Se a BCSS for chamada como um resultado de um failover disparado por um componente de monitoramento (por exemplo, por meio de um respondente de Failover), uma restrição obrigatória adicional será aplicada onde a integridade de componentes do servidor de destino deve ser melhor que o servidor em que o failover ocorreu. Por exemplo, se uma falha do Microsoft Office Outlook Web App disparar um failover por meio de um respondente de Failover, a BCSS deverá selecionar um servidor que hospeda uma cópia do banco de dados afetado em que o Outlook Web App é integro.

## Processo de seleção de melhor cópia

Com relação às falhas de banco de dados (e não falhas de protocolo), o Active Manager no Exchange 2013 realiza as mesmas verificações que realizava no Exchange 2010. O Active Manager começa o processo de seleção de melhor cópia cirando uma lista de cópias do banco de dados que são possíveis candidatos para ativação. Cópias de banco de dados que estejam inacessíveis ou bloqueadas administrativamente contra ativação são ignoradas e não são usadas durante o processo de seleção. A ordem da lista depende do valor de *AutoDatabaseMountDial*:

  - Se o *AutoDatabaseMountDial* estiver configurado com qualquer valor que não seja `Lossless` em todos os servidores que hospedam uma cópia do banco de dados, o Active Manager classificará a lista resultante usando o comprimento da fila de cópia como chave primária. O cálculo é baseado em LastLogInspected (do ponto de vista da cópia), para que a lista de cópias possíveis seja classificada pelo valor mais alto para LastLogInspected (que será a cópia com o menor comprimento de fila de cópia). Se necessário, o Active Manager classifica a lista uma segunda vez, usando o valor da Preferência de Ativação como uma chave secundária para desvincular quaisquer condições em que duas ou mais cópias passivas têm o mesmo comprimento da fila de cópia. A cópia com o menor valor de Preferência de Ativação possui a mais alta prioridade na lista.

  - Se *AutoDatabaseMountDial* estiver configurado com um valor `Lossless` em todos os servidores que hospedam uma cópia do banco de dados, o Active Manager classificará a lista resultante em ordem crescente usando o valor de preferência de ativação como chave primária. Além disso, quando um administrador realiza uma alternância de servidor ou de banco de dados sem perdas sem especificar um destino, o Active Manager também classifica a lista resultante em ordem crescente usando o valor de Preferência de Ativação com chave primária.

Em seguida, o Active Manager tenta localizar na lista uma cópia do banco de dados de caixa de correio com status Healthy, DisconnectedAndHealthy, DisconnectedAndResynchronizing ou SeedingSource e avalia o potencial de ativação de cada uma das cópias na lista usando um conjunto ordenado de dez critérios. O Active Manager determina se qualquer dos candidatos para ativação atende ao primeiro conjunto de critérios:

  - Tem um índice de conteúdo com o status Íntegro (Healthy).

  - Tem um tamanho de fila de cópia inferior a 10 arquivos de log.

  - Tem um tamanho de fila de repetição inferior a 50 arquivos de log.

Caso nenhuma das cópias do banco de dados atenda ao primeiro conjunto de critérios, o Active Manager tenta localizar uma cópia do banco de dados que atenda ao segundo conjunto de critérios:

  - Tem um índice de conteúdo com o status Rastreando (Crawling).

  - Tem um tamanho de fila de cópia inferior a 10 arquivos de log.

  - Tem um tamanho de fila de repetição inferior a 50 arquivos de log.

Caso nenhuma das cópias do banco de dados atenda ao segundo conjunto de critérios, o Active Manager tenta localizar uma cópia do banco de dados que atenda ao terceiro conjunto de critérios:

  - Tem um índice de conteúdo com o status Íntegro (Healthy).

  - Tem um tamanho de fila de repetição inferior a 50 arquivos de log.

Caso nenhuma das cópias do banco de dados atenda ao terceiro conjunto de critérios, o Active Manager tenta localizar uma cópia do banco de dados que atenda ao quarto conjunto de critérios:

  - Tem um índice de conteúdo com o status Rastreando (Crawling).

  - Tem um tamanho de fila de repetição inferior a 50 arquivos de log.

Caso nenhuma das cópias do banco de dados atenda ao quarto conjunto de critérios, o Active Manager tenta localizar uma cópia do banco de dados que atenda ao quinto conjunto de critérios:

  - Tem um tamanho de fila de repetição inferior a 50 arquivos de log.

Caso nenhuma das cópias do banco de dados atenda ao quinto conjunto de critérios, o Active Manager tenta localizar uma cópia do banco de dados que atenda ao sexto conjunto de critérios:

  - Tem um índice de conteúdo com o status Íntegro (Healthy).

  - Tem um tamanho de fila de cópia inferior a 10 arquivos de log.

Caso nenhuma das cópias do banco de dados atenda ao sexto conjunto de critérios, o Active Manager tenta localizar uma cópia do banco de dados que atenda ao sétimo conjunto de critérios:

  - Tem um índice de conteúdo com o status Rastreando (Crawling).

  - Tem um tamanho de fila de cópia inferior a 10 arquivos de log.

Caso nenhuma das cópias do banco de dados atenda ao sétimo conjunto de critérios, o Active Manager tenta localizar uma cópia do banco de dados que atenda ao oitvao conjunto de critérios:

  - Tem um índice de conteúdo com o status Íntegro (Healthy).

Caso nenhuma das cópias do banco de dados atenda ao oitavo conjunto de critérios, o Active Manager tenta localizar uma cópia do banco de dados que atenda ao non conjunto de critérios:

  - Tem um índice de conteúdo com o status Rastreando (Crawling).

Caso nenhuma das cópias de banco de dados atenda ao nono conjunto de critérios, o Active Manager tenta ativar qualquer cópia de banco de dados com status Healthy, DisconnectedAndHealthy, DisconnectedAndResynchronizing ou SeedingSource (o décimo conjunto de critérios). Se nenhuma cópia de banco de dados que atenda ao décimo conjunto de critérios for encontrada, não será possível ativar automaticamente uma cópia do banco de dados.

Depois que uma ou mais cópias forem localizadas de acordo com um ou mais conjuntos de critérios, o processo ACLL é executado para copiar quaisquer arquivos de log da fonte original para a nova cópia ativa potencial. Depois que o processo ACLL é concluído, o PAM emite uma solicitação de montagem e o banco de dados é montado e disponibilizado para os clientes, ou o banco de dados não é montado e o PAM procura a próxima melhor cópia (caso haja uma disponível).

