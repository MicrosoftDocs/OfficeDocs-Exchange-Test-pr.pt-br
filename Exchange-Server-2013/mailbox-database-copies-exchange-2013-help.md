---
title: 'Cópias de banco de dados de caixa de correio: Exchange 2013 Help'
TOCTitle: Cópias de banco de dados de caixa de correio
ms:assetid: ce748bca-3e24-493b-b9e6-153157bffd6a
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Dd979802(v=EXCHG.150)
ms:contentKeyID: 50486684
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Cópias de banco de dados de caixa de correio

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2015-04-07_

Microsoft Exchange Server 2013 aproveita o conceito de mobilidade de banco de dados, que é Exchange-gerenciados failovers de nível de banco de dados. Mobilidade de banco de dados desconecta bancos de dados de servidores, adiciona suporte a até 16 cópias de um único banco de dados e oferece uma experiência nativa para adição de cópias de banco de dados para um banco de dados.

## Características principais

As principais características de cópias de banco de dados de caixa de correio são:

  - Até 16 cópias de um Exchange 2013 de banco de dados de caixa de correio pode ser criado em vários servidores de caixa de correio, fornecidos que os servidores são agrupados em um grupo de disponibilidade do banco de dados (DAG), que é um limite para replicação contínua. bancos de dados de caixa de correio Exchange 2013 podem ser replicados somente a outros servidores de caixa de correio Exchange 2013 dentro de um DAG. Você não pode replicar um banco de dados fora de um DAG, nem pode replicar um banco de dados de caixa de correio de Exchange 2013 para uma execução de servidor Exchange 2010 ou anterior. Para obter informações detalhadas sobre DAGs, consulte [Grupos de Disponibilidade do Banco de Dados (DAGs)](database-availability-groups-dags-exchange-2013-help.md).

  - Todos os servidores de caixa de correio em um DAG devem estar no mesmo domínio Active Directory.

  - Os conceitos do tempo de retardo de repetição e tempo de retardo de truncamento suportam a cópias de banco de dados de caixa de correio. Planejamento apropriados deve ser executada antes de habilitar esses recursos.

  - Todas as cópias de banco de dados podem ser feitas usando um Exchange-ciente, com base em VSS do serviço de cópias de sombra de Volume de aplicativo de backup.

  - Cópias de banco de dados podem ser criadas somente em servidores de caixa de correio que não hospedam a cópia ativa do banco de dados. É possível criar duas cópias do mesmo banco de dados no mesmo servidor.

  - Todas as cópias de um banco de dados usam o mesmo caminho em cada servidor que contém uma cópia. Os caminhos de arquivo de banco de dados e log para obter uma cópia do banco de dados em cada servidor de caixa de correio não devem entrar em conflito com quaisquer outros caminhos de banco de dados.

  - Cópias de banco de dados podem ser criadas nos sites do mesmo ou diferente Active Directory e, no mesmo ou diferente subredes.

  - Cópias de banco de dados não são suportadas entre os servidores de caixa de correio com latência de rede de ida e volta maior do que 500 milissegundos (ms).

## Cópias de banco de dados de caixa de correio

Você pode criar uma cópia do banco de dados de caixa de correio a qualquer momento. Cópias de banco de dados de caixa de correio podem ser distribuídas em servidores de caixa de correio de uma forma flexível e granular.

Você pode criar uma cópia de banco de dados de caixa de correio usando o Assistente de **cópia de banco de dados de caixa de correio de adicionar** na Exchange Administração Central ou usando o cmdlet **Add-MailboxDatabaseCopy** em Exchange Management Shell.

Ao criar uma cópia do banco de dados de caixa de correio, especifique os seguintes parâmetros:

  - *Identity*   Este parâmetro especifica o nome do banco de dados que está sendo copiado. Nomes de banco de dados devem ser exclusivos dentro da organização Exchange.

  - *MailboxServer*   Este parâmetro especifica o nome do servidor de caixa de correio que irá hospedar a cópia do banco de dados. Esse servidor deve ser um membro do mesmo DAG e não deve hospedar uma cópia do banco de dados.

Opcionalmente, você também pode especificar:

  - *ActivationPreference*    Este parâmetro especifica o número de preferência de ativação, que é usado como parte do processo de seleção de melhor cópia do Gerenciador ativo. Ele também é usado para redistribuir bancos de dados de caixa de correio ativas em todo o DAG ao usar o script Redistributeactivedatabases ps1. O valor para a preferência de ativação é um número igual ou maior do que um, onde uma é na parte superior da ordem de preferência. O número da posição não pode ser maior que o número de cópias de banco de dados de caixa de correio.

  - *ReplayLagTime *  Este parâmetro especifica a quantidade de tempo que o Microsoft Exchange serviço de replicação deve aguardar antes de repetir arquivos de log são copiados para a cópia do banco de dados. O formato para esse parâmetro é (dias). A configuração padrão para este valor é 0 segundos. A configuração máxima permitida para esse valor é 14 dias. A configuração mínima permitida é 0 segundo. Definindo o valor para o tempo de retardo de repetição para 0 desativa o atraso de repetição de log.

  - *TruncationLagTime*   Este parâmetro especifica a quantidade de tempo que o Microsoft Exchange serviço de replicação deve aguardar antes de truncar arquivos de log que têm repetidos em uma cópia do banco de dados. O período de tempo começa depois que o log foi repetido com êxito na cópia do banco de dados. O formato para esse parâmetro é (dias). A configuração padrão para este valor é 0 segundos. A configuração máxima permitida para esse valor é 14 dias. A configuração mínima permitida é 0 segundo. Definindo o valor de tempo de retardo de truncamento como 0 desativa o atraso de truncamento de log.

  - *SeedingPostponed*    Este parâmetro especifica que a tarefa não deve propagar automaticamente a cópia do banco de dados no servidor de caixa de correio especificada. Essa opção é normalmente usada quando você pretende propagar uma nova cópia do banco de dados de caixa de correio usando uma cópia passiva existente do banco de dados (por exemplo, adicionando uma segunda cópia de um banco de dados específico para um local remoto). Quando você usa esse parâmetro, você deve propagar manualmente a cópia do banco de dados usando o cmdlet [Update-MailboxDatabaseCopy](https://technet.microsoft.com/pt-br/library/dd335201\(v=exchg.150\)) .

Para obter mais informações sobre como criar, usando e gerenciando cópias de banco de dados de caixa de correio, consulte [Gerenciando cópias de banco de dados de caixa de correio](managing-mailbox-database-copies-exchange-2013-help.md).

