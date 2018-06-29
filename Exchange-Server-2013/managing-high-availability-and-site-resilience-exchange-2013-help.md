---
title: 'Gerenciando a alta disponibilidade e resiliência do site: Exchange 2013 Help'
TOCTitle: Gerenciando a alta disponibilidade e resiliência do site
ms:assetid: f9677392-88d2-457f-a488-245771a8c1f2
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Dd638215(v=EXCHG.150)
ms:contentKeyID: 50487033
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Gerenciando a alta disponibilidade e resiliência do site

 

_**Aplica-se a:**Exchange Server 2013_

_**Tópico modificado em:**2012-11-05_

Depois de criar, validar e implantar uma alta disponibilidade do Microsoft Exchange Server 2013 ou uma solução de resiliência do site, as transições de solução da fase de implantação para a fase operacional do ciclo de vida de solução geral. A fase operacional consiste em várias tarefas, e todas as tarefas relacionadas a uma das seguintes áreas: grupos de disponibilidade (DAGs), cópias de banco de dados de caixa de correio, executando o monitoramento proativo e gerenciando alternâncias e failovers de banco de dados.

**Sumário**

Gerenciamento de grupo de disponibilidade do banco de dados

Gerenciamento de cópia de banco de dados de caixa de correio

Monitoramento proativo

Alternâncias e failovers

## Gerenciamento de grupo de disponibilidade do banco de dados

As tarefas de gerenciamento operacional associadas DAGs incluem:

  - **Criando DAGs um ou mais**   A criação de um DAG é geralmente um procedimento de uma única vez executado durante a fase de implantação do ciclo de vida de solução. No entanto, pode haver razões para a criação de DAGs que ocorrem durante a fase operacional, por exemplo:
    
      - DAG está configurado para o modo de replicação de terceiros e você quiser reverter para usando a replicação contínua. Você não pode converter um DAG para replicação contínua; Você precisa criar um DAG.
    
      - Você tem servidores em vários domínios. Todos os membros do mesmo DAG também devem ser membros do mesmo domínio.

  - **Associação ao DAG Gerenciando**   Gerenciar membros do DAG é uma tarefa não frequentes normalmente executada durante a fase de implantação do ciclo de vida de solução. No entanto, devido a flexibilidade oferecida pela implantação incremental, gerenciar a associação ao DAG pode também ser executada durante todo o ciclo de solução.

  - **Propriedades do DAG Configurando**   Cada DAG tem várias propriedades que podem ser configuradas conforme necessário. Essas propriedades incluem:
    
      - **Servidor testemunha e um diretório testemunha**   O servidor testemunha é um servidor fora do DAG que atua como um eleitor quorum quando o DAG contém um número par de membros. O diretório testemunha é um diretório criado e compartilhado no servidor testemunha para uso pelo sistema em manter um quorum.
    
      - **Endereços IP**   Cada DAG terão um ou mais endereços IPv4 e, opcionalmente, um ou mais endereços IPv6. Os endereços IP atribuídos ao DAG são usados pelo cluster subjacente do DAG. O número de endereços IPv4 atribuídos ao DAG é igual ao número de sub-redes que compõem a rede MAPI usada pelo DAG. Você pode configurar o DAG usar endereços IP estáticos ou obter endereços automaticamente usando o Dynamic Host Configuration Protocol (DHCP).
    
      - **Modo coordenação de ativação de Datacenter**   Modo coordenação de ativação de Datacenter é uma configuração de propriedade em um DAG que foi desenvolvido para evitar condições Split-Brain no nível do banco de dados, em um cenário no qual você está restaurando serviço para um data center principal após uma alternância de datacenter foi realizada . Para obter mais informações sobre o modo coordenação de ativação de Datacenter, consulte [Modo coordenação de ativação de Datacenter](datacenter-activation-coordination-mode-exchange-2013-help.md).
    
      - **Servidor testemunha alternativo e diretório testemunha alternativo**   O servidor testemunha alternativo e o diretório testemunha alternativo são valores que você pode predefinir como parte do processo de planejamento para uma alternância de datacenter. Essas referir-se ao servidor de testemunha e um diretório testemunha que será usado quando uma alternância de datacenter foi realizada.
    
      - **Porta de replicação**   Por padrão, DAGs todos usam a porta TCP 64327 para replicação contínua. Você pode modificar o DAG para usar uma porta TCP diferente para replicação usando o parâmetro *ReplicationPort* do cmdlet [Set-DatabaseAvailabilityGroup](https://technet.microsoft.com/pt-br/library/dd297934\(v=exchg.150\)) .
    
      - **Descoberta de rede**   Você pode forçar o DAG para detectar novamente redes e interfaces de rede. Essa operação é usada quando você adicionar ou remove redes ou introduzir novas sub-redes. Nova descoberta de todas as redes do DAG pode ser forçada usando o parâmetro *DiscoverNetworks* do cmdlet [Set-DatabaseAvailabilityGroup](https://technet.microsoft.com/pt-br/library/dd297934\(v=exchg.150\)) .
    
      - **Compactação de rede**   Por padrão, DAGs usam a compactação apenas entre redes do DAG em diferentes sub-redes. Você pode habilitar a compactação de todas as redes do DAG ou para propagação somente operações ou é possível desabilitar a compactação de todas as redes do DAG.
    
      - **Criptografia de rede**   Por padrão, DAGs usam criptografia apenas entre redes do DAG em diferentes sub-redes. É possível habilitar a criptografia de todas as redes do DAG ou para propagação somente operações ou você pode desabilitar a criptografia de todas as redes do DAG.

  - **Desligado membros DAG**   A solução de alta disponibilidade Exchange 2013 é integrada com o processo de encerramento Windows. Se um administrador ou aplicativo inicia um desligamento de um servidor Windows em um DAG que tenha um banco de dados montado que é replicado para um ou mais membros do DAG, o sistema tentará ativar outra cópia dos bancos de dados montados antes de permitir o desligamento processo seja concluído. No entanto, esse novo comportamento não garante que todos os bancos de dados no servidor que está sendo desligado experimentará uma ativação sem perdas. Como resultado, é uma prática recomendada para realizar uma alternância de servidor antes de encerrar um servidor que seja membro de um DAG.

Para obter instruções detalhadas sobre como criar um DAG, consulte [Criar um grupo de disponibilidade do banco de dados](create-a-database-availability-group-exchange-2013-help.md). Para obter etapas detalhadas sobre como configurar DAGs e DAG propriedades, consulte [Configurar as propriedades do grupo de disponibilidade do banco de dados](configure-database-availability-group-properties-exchange-2013-help.md). Para obter mais informações sobre cada uma das tarefas de gerenciamento de anterior e sobre como gerenciar DAGs em geral, consulte [Gerenciando grupos de disponibilidade de banco de dados](managing-database-availability-groups-exchange-2013-help.md).

Voltar ao início

## Gerenciamento de cópia de banco de dados de caixa de correio

As tarefas de gerenciamento operacional associadas a cópias de banco de dados de caixa de correio incluem:

  - **Adicionando cópias de banco de dados de caixa de correio**   Quando você adiciona uma cópia de um banco de dados de caixa de correio, a replicação contínua é ativada automaticamente entre a cópia do banco de dados e o banco de dados existente.

  - **Configurando propriedades de cópia de banco de dados de caixa de correio**   Você pode configurar uma variedade de propriedades, como a política de ativação do banco de dados, a quantidade de tempo, se houver, para a preferência de ativação para a cópia do banco de dados e de retardo de truncamento e de retardo de repetição.

  - **Suspending ou retomar uma cópia do banco de dados de caixa de correio**   É possível suspender uma cópia do banco de dados de caixa de correio em preparação para a propagação ou outras formas de manutenção. Também é possível suspender uma cópia de banco de dados de caixa de correio para ativação apenas. Essa configuração impede que o sistema ativando automaticamente a cópia como resultado de uma falha, mas ela ainda permite que o sistema manter a cópia do banco de dados atualizado com envio de log e repetição.

  - **Atualizando uma cópia do banco de dados de caixa de correio**   Atualizando, também conhecido como *propagação*, é o processo no qual uma cópia de um banco de dados de caixa de correio é adicionada para outro servidor de caixa de correio. Isso se torna o banco de dados de linha de base para a cópia. Após o término da propagação primeiro inicial do banco de dados da linha de base copia, somente em circunstâncias raras o banco de dados precisará ser propagado novamente.

  - **Ativando uma cópia do banco de dados de caixa de correio**   Ativação é o processo de designar uma cópia passiva específica como a nova cópia ativa de um banco de dados de caixa de correio. Esse processo é conhecido como uma *alternância*. Para obter mais informações, consulte "Alternâncias e Failovers" mais adiante neste tópico.

  - **Removendo uma cópia do banco de dados de caixa de correio**   Você pode remover uma cópia do banco de dados de caixa de correio a qualquer momento. Ocasionalmente, talvez seja necessário remover uma cópia do banco de dados de caixa de correio. Por exemplo, é possível remover um servidor de caixa de correio de um DAG até que todas as cópias de banco de dados de caixa de correio são removidas do servidor. Além disso, você deve remover todas as cópias de um banco de dados de caixa de correio antes de alterar o caminho para um banco de dados de caixa de correio.

Para obter instruções detalhadas sobre como adicionar uma cópia do banco de dados de caixa de correio, consulte [Adicionar uma cópia do banco de dados de caixa de correio](add-a-mailbox-database-copy-exchange-2013-help.md). Para obter instruções detalhadas sobre como configurar cópias de banco de dados de caixa de correio, consulte [Configurar propriedades de cópia de banco de dados de caixa de correio](configure-mailbox-database-copy-properties-exchange-2013-help.md). Para obter mais informações sobre cada uma das tarefas de gerenciamento de anterior e sobre como gerenciar cópias do banco de dados de caixa de correio em geral, consulte [Gerenciando cópias de banco de dados de caixa de correio](managing-mailbox-database-copies-exchange-2013-help.md). Para obter instruções detalhadas sobre como remover uma cópia do banco de dados de caixa de correio, consulte [Remover uma cópia do banco de dados de caixa de correio](remove-a-mailbox-database-copy-exchange-2013-help.md).

Voltar ao início

## Monitoramento proativo

Certificando-se de que os servidores estão funcionando confiável e que suas cópias de banco de dados são íntegras é os objetivos principais para operações diárias de mensagens. Exchange 2013 inclui vários recursos que podem ser usados para executar uma variedade de tarefas de monitoramento de integridade para DAGs e cópias de banco de dados de caixa de correio, incluindo:

  - [Get-MailboxDatabaseCopyStatus](https://technet.microsoft.com/pt-br/library/dd298044\(v=exchg.150\))

  - [Test-ReplicationHealth](https://technet.microsoft.com/pt-br/library/bb691314\(v=exchg.150\))

  - Log de eventos do canal Crimson

Além de monitorar a integridade e o status, também é essencial para o monitoramento de situações em que podem comprometer a disponibilidade. Por exemplo, é recomendável monitorar a redundância de seus bancos de dados replicados. É essencial para evitar situações em que você esteja para baixo até uma única cópia de um banco de dados. Este cenário deve ser tratado com prioridade máxima e resolvido assim que possível.

Para obter informações mais detalhadas sobre como monitorar a integridade e o status de DAGs e cópias de banco de dados de caixa de correio, consulte [Grupos de disponibilidade de banco de dados de monitoramento](monitoring-database-availability-groups-exchange-2013-help.md).

Voltar ao início

## Alternâncias e failovers

Uma *alternância* é um processo manual no qual um administrador ativa manualmente uma ou mais cópias de banco de dados de caixa de correio. Alternâncias, que podem ocorrer no nível do banco de dados ou servidor, geralmente são executadas como parte da preparação para atividades de manutenção. Gerenciamento de alternância envolve a realização de alternâncias de banco de dados ou servidor conforme necessário. Por exemplo, se você precisar executar manutenção em um servidor de caixa de correio em um DAG, você deve executar primeiro uma alternância de servidor para que o servidor não hospedar qualquer cópias de banco de dados de caixa de correio ativas. Para obter instruções detalhadas sobre como realizar uma alternância de banco de dados, consulte [Ativar uma cópia do banco de dados de caixa de correio](activate-a-mailbox-database-copy-exchange-2013-help.md). Alternâncias também podem ser executadas no nível do datacenter.

Um *failover* é a ativação automática pelo sistema de uma ou mais cópias de banco de dados em reação a uma falha. Por exemplo, a perda de uma unidade de disco em um ambiente sem RAID irá disparar um failover de banco de dados. Perda de rede MAPI ou uma falha de energia irá disparar um failover de servidor.

Voltar ao início

