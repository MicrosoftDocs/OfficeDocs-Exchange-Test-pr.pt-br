---
title: 'Implantando a alta disponibilidade e resiliência do site: Exchange 2013 Help'
TOCTitle: Implantando a alta disponibilidade e resiliência do site
ms:assetid: 4c4e00a4-1f57-4fdb-b9b2-2779abf381a9
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Dd638129(v=EXCHG.150)
ms:contentKeyID: 50485550
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Implantando a alta disponibilidade e resiliência do site

 

_**Aplica-se a:**Exchange Server 2013_

_**Tópico modificado em:**2015-03-09_

O Microsoft Exchange Server 2013 usa o conceito conhecido como *implantação incremental* tanto para alta disponibilidade quanto para resiliência de site. Você simplesmente instala dois ou mais servidores de Caixa de Correio do Exchange 2013 como servidores independentes e os configura incrementalmente, junto com os bancos de dados de caixa de correio, para alta disponibilidade e resiliência de site, conforme a necessidade.

## Visão geral do processo de implantação

As etapas a serem seguidas em cada organização podem variar um pouco, mas o processo geral de implantação do Exchange 2013 em uma configuração de alta disponibilidade ou de resiliência de site geralmente é o mesmo. Depois de realizar as tarefas de planejamento e design para a criação e a implantação de um grupo de disponibilidade de banco de dados (DAG) e a criação de cópias de banco de dados de caixa de correio, você poderá:

1.  Criar um DAG. Para instruções detalhadas, consulte [Criar um grupo de disponibilidade do banco de dados](create-a-database-availability-group-exchange-2013-help.md).

2.  Se necessário, configure previamente o objeto de nome de cluster (CNO). A preparação prévia do CNO é necessária na implantação de um DAG com servidores de Caixa de Correio que executam o Windows Server 2012. Se você estiver implantando um DAG sem um ponto de acesso administrativo usando servidores de Caixa de Correio que executam o Windows Server 2012 R2, então não será necessário preparar previamente um CNO. Essa configuração prévia também é necessária em ambientes em que a criação da conta do computador é restrita ou em que as contas do computador são criadas em um contêiner que não seja o contêiner padrão do computador. Para obter etapas detalhadas, consulte [Preparar o objeto de nome de cluster de um grupo de disponibilidade do banco de dados](pre-stage-the-cluster-name-object-for-a-database-availability-group-exchange-2013-help.md).

3.  Adicionar dois ou mais servidores de caixa de correio ao DAG. Para instruções detalhadas, consulte [Gerenciar a associação de grupo de disponibilidade do banco de dados](manage-database-availability-group-membership-exchange-2013-help.md).

4.  Configurar as propriedades do DAG conforme a necessidade:
    
    1.  Uma opção é configurar a criptografia e a compactação do DAG, a porta de replicação, os endereços IP do DAG e outras propriedades do DAG. Para instruções detalhadas, consulte [Configurar as propriedades do grupo de disponibilidade do banco de dados](configure-database-availability-group-properties-exchange-2013-help.md).
    
    2.  Habilitar o modo Coordenação de Ativação de Datacenter (DAC) para o DAG. Isso protege o DAG de condições de dupla personalidade em nível de banco de dados durante um switchback para o data center principal após uma alternância de servidor ter sido executada e permite o uso de cmdlets de recuperação de DAG internos. Para mais informações, consulte [Modo coordenação de ativação de Datacenter](datacenter-activation-coordination-mode-exchange-2013-help.md).

5.  Adicionar cópias de banco de dados de caixa de correio entre servidores de caixa de correio no DAG. Para instruções detalhadas, consulte [Adicionar uma cópia do banco de dados de caixa de correio](add-a-mailbox-database-copy-exchange-2013-help.md).

## Exemplo de implantação: DAG de quatro membros em dois data centers

Este exemplo detalha como uma organização, como a Contoso Ltd., configura e implanta um DAG de quatro membros que se estenderá por dois locais físicos: Redmond, Washington e Portland, Oregon.

## Infraestrutura de base

Cada local contém os elementos de infraestrutura necessários à operação de uma infraestrutura de mensagens baseada no Exchange 2013, notadamente:

  - Serviços de diretório (Active Directory ou Serviços de Domínio do Active Directory Domain Services (AD DS))

  - Resolução de nomes DNS

  - Servidores de Acesso para Cliente do Exchange 2013

  - Vários servidores de Caixa de Correio do Exchange 2013

A figura a seguir ilustra a configuração da Contoso.

**O grupo de disponibilidade de banco de dados se estende por dois sites**

![Grupo de disponibilidade do banco de dados estendido para dois sites](images/Dd638129.1c326fd4-3c7b-4416-a63d-fbfdd0cc6b18(EXCHG.150).gif "Grupo de disponibilidade do banco de dados estendido para dois sites")

## Configuração da rede

Como mostra a figura anterior, a solução envolve o uso de várias redes e sub-redes. Cada servidor de Caixa de Correio no DAG tem dois adaptadores de rede em sub-redes separadas. Em cada servidor de caixa de correio, um adaptador de rede será usado para a rede MAPI (192.168.*x*.*x*) e um adaptador de rede será usado para a rede de Replicação (10.0.*x*.*x*). Apenas a rede MAPI oferece conectividade ao Active Directory, aos serviços de DNS e a outros servidores e clientes do Exchange. O adaptador usado para a rede de Replicação em cada membro oferece conectividade apenas para adaptadores de rede de Replicação em outros membros do DAG.

As configurações de cada adaptador de rede de cada nó são detalhadas na tabela a seguir.


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
<th>Endereço IPv4</th>
<th>Máscara de sub-rede</th>
<th>Gateway padrão</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>MBX1 (MAPI)</p></td>
<td><p>192.168.1.4</p></td>
<td><p>255.255.255.0</p></td>
<td><p>192.168.1.1</p></td>
</tr>
<tr class="even">
<td><p>MBX2 (MAPI)</p></td>
<td><p>192.168.1.5</p></td>
<td><p>255.255.255.0</p></td>
<td><p>192.168.1.1</p></td>
</tr>
<tr class="odd">
<td><p>MBX3 (MAPI)</p></td>
<td><p>192.168.2.4</p></td>
<td><p>255.255.255.0</p></td>
<td><p>192.168.2.1</p></td>
</tr>
<tr class="even">
<td><p>MBX4 (MAPI)</p></td>
<td><p>192.168.2.5</p></td>
<td><p>255.255.255.0</p></td>
<td><p>192.168.2.1</p></td>
</tr>
<tr class="odd">
<td><p>MBX1 (replicação)</p></td>
<td><p>10.0.1.4</p></td>
<td><p>255.255.0.0</p></td>
<td><p>Nenhum</p></td>
</tr>
<tr class="even">
<td><p>MBX2 (replicação)</p></td>
<td><p>10.0.1.5</p></td>
<td><p>255.255.0.0</p></td>
<td><p>Nenhum</p></td>
</tr>
<tr class="odd">
<td><p>MBX3 (replicação)</p></td>
<td><p>10.0.2.4</p></td>
<td><p>255.255.0.0</p></td>
<td><p>Nenhum</p></td>
</tr>
<tr class="even">
<td><p>MBX4 (replicação)</p></td>
<td><p>10.0.2.5</p></td>
<td><p>255.255.0.0</p></td>
<td><p>Nenhum</p></td>
</tr>
</tbody>
</table>


Como mostra a tabela anterior, os adaptadores usados para redes de Replicação não usam gateways-padrão. Para proporcionar conectividade de rede entre cada adaptador de rede de Replicação, a Contoso usa rotas estáticas persistentes, que eles configuram usando a ferramenta Netsh.exe.

Para configurar o roteamento para os adaptadores de rede de Replicação em MBX1 e MBX2, o comando a seguir foi executado em cada servidor.

    netsh interface ipv4 add route 10.0.2.0/24 <NetworkName> 10.0.1.254

Para configurar o roteamento para os adaptadores de rede de Replicação em MBX3 e MBX4, o comando a seguir foi executado em cada servidor.

    netsh interface ipv4 add route 10.0.1.0/24 <NetworkName> 10.0.2.254

As seguintes configurações de rede adicionais também foram configuradas:

  - A caixa de seleção **Registrar os endereços desta conexão no DNS** está marcada para cada adaptador de rede MAPI do membro do DAG e desmarcada para cada adaptador de rede de Replicação.

  - Ao menos um endereço de servidor DNS está configurado para cada adaptador de rede MAPI do membro do DAG, e nenhum está configurado para os adaptadores de rede de Replicação. Para redundância, a Contoso está usando vários endereços de servidores DNS para seus adaptadores de rede MAPI.

  - A Contoso não usa o Firewall do Windows e desativou-o em seus servidores.

Após a configuração dos adaptadores de rede, a Contoso está pronta para criar um DAG e adicionar servidores de caixa de correio ao DAG.

## Criação e configuração do grupo de disponibilidade de banco de dados

O administrador decidiu criar um script de interface de linha de comando do Windows PowerShell que realiza várias tarefas:

  - Ele usa o cmdlet [New-DatabaseAvailabilityGroup](https://technet.microsoft.com/pt-br/library/dd351107\(v=exchg.150\)) para criar o DAG. Como o REDMOND é considerado o data center principal, a Contoso optou por usar um servidor testemunha no mesmo datacenter, especificamente o CAS1.

  - Ele usa o cmdlet [Set-DatabaseAvailabilityGroup](https://technet.microsoft.com/pt-br/library/dd297934\(v=exchg.150\)) para pré-configurar um servidor testemunha alternativo e um diretório testemunha alternativo para o caso de uma alternância de datacenter ser necessária.

  - Ele usa o cmdlet [Add-DatabaseAvailabilityGroupServer](https://technet.microsoft.com/pt-br/library/dd298049\(v=exchg.150\)) para adicionar cada um dos quatro servidores de caixa de correio ao DAG.

  - Ele usa o cmdlet [Set-DatabaseAvailabilityGroup](https://technet.microsoft.com/pt-br/library/dd297934\(v=exchg.150\)) para configurar o DAG para modo DAC. Para mais informações sobre o modo DAC, consulte [Modo coordenação de ativação de Datacenter](datacenter-activation-coordination-mode-exchange-2013-help.md).

Os seguintes comandos são usados no script:

    New-DatabaseAvailabilityGroup -Name DAG1 -WitnessServer CAS1 -WitnessDirectory C:\DAGWitness\DAG1.contoso.com -DatabaseAvailabilityGroupIPAddresses 192.168.1.8,192.168.2.8

O comando anterior cria um DAG chamado DAG1, configura o CAS1 para agir como servidor testemunha, configura um diretório testemunha específico (C:\\DAGWitness\\DAG1.contoso.com) e configura dois endereços IP para o DAG (um para cada sub-rede na rede MAPI).

    Set-DatabaseAvailabilityGroup -Identity DAG1 -AlternateWitnessDirectory C:\DAGWitness\DAG1.contoso.com -AlternateWitnessServer CAS4

O comando anterior configura o DAG1 para usar um servidor testemunha alternativo CAS4 e um diretório testemunha alternativo no CAS4 que usa o mesmo caminho configurado no CAS1.


> [!TIP]
> Não é necessário usar o mesmo caminho; a Contoso optou por fazer isso para padronizar a configuração.



    Add-DatabaseAvailabilityGroupServer -Identity DAG1 -MailboxServer MBX1
    Add-DatabaseAvailabilityGroupServer -Identity DAG1 -MailboxServer MBX3
    Add-DatabaseAvailabilityGroupServer -Identity DAG1 -MailboxServer MBX2
    Add-DatabaseAvailabilityGroupServer -Identity DAG1 -MailboxServer MBX4

Os comandos anteriores adicionam cada um dos servidores de caixa de correio, um de cada vez, ao DAG. Os comandos também instalam o componente de Cluster de Failover do Windows em cada servidor de caixa de correio (caso ainda não esteja instalado), cria um cluster de failover e ingressa cada servidor de caixa de correio no cluster recém-criado.

    Set-DatabaseAvailabilityGroup -Identity DAG1 -DatacenterActivationMode DagOnly

O comando anterior habilita o modo DAC para o DAG.

## Bancos de dados de Caixas de Correio e cópias de bancos de dados de Caixas de Correio

Depois de criar o DAG e adicionar os servidores de Caixa de Correio ao DAG, a Contoso se prepara para criar bancos de dados de caixas de correio e cópias de bancos de dados de caixas de correio. Para atender ao critério de resistência a falhas, a Contoso pretende configurar cada banco de dados de caixa de correio com três cópias de banco de dados sem atraso e uma cópia de banco de dados com atraso. A cópia com atraso terá um atraso de repetição de log configurado para três dias.

Essa configuração proporciona um total de quatro cópias para cada banco de dados (uma ativa, duas passivas sem atraso e outra passiva com atraso). A Contoso pretende ter quatro bancos de dados ativos por servidor. Com quatro bancos de dados ativos por servidor e três cópias passivas de cada banco de dados, a solução da Contoso contém 16 cópias totais de banco de dados.

Como mostra a figura a seguir, a Contoso adotou uma abordagem equilibrada no layout de banco de dados.

**Layout da cópia do banco de dados para a Contoso, Ltd**

![Layout da Cópia do Banco de Dados para a Contoso, Ltd](images/Dd638129.41d0c78e-ccaf-4b67-8bab-6fb344668ead(EXCHG.150).gif "Layout da Cópia do Banco de Dados para a Contoso, Ltd")

Cada servidor de caixa de correio hospeda uma cópia de banco de dados de caixa de correio ativa, duas cópias de banco de dados passivas sem atraso e uma cópia de banco de dados passiva com atraso. A cópia com atraso de cada banco de dados de caixa de correio ativo é hospedada em um servidor de caixa de correio no outro site.

Para criar essa configuração, o administrador executa vários comandos.

No MBX1, execute os seguintes comandos.

    Add-MailboxDatabaseCopy -Identity DB1 -MailboxServer MBX2
    Add-MailboxDatabaseCopy -Identity DB1 -MailboxServer MBX4
    Add-MailboxDatabaseCopy -Identity DB1 -MailboxServer MBX3 -ReplayLagTime 3.00:00:00 -SeedingPostponed
    Suspend-MailboxDatabaseCopy -Identity DB1\MBX3 -SuspendComment "Seed from MBX4" -Confirm:$False
    Update-MailboxDatabaseCopy -Identity DB1\MBX3 -SourceServer MBX4
    Suspend-MailboxDatabaseCopy -Identity DB1\MBX3 -ActivationOnly

No MBX2, execute os seguintes comandos.

    Add-MailboxDatabaseCopy -Identity DB2 -MailboxServer MBX1
    Add-MailboxDatabaseCopy -Identity DB2 -MailboxServer MBX3
    Add-MailboxDatabaseCopy -Identity DB2 -MailboxServer MBX4 -ReplayLagTime 3.00:00:00 -SeedingPostponed
    Suspend-MailboxDatabaseCopy -Identity DB2\MBX4 -SuspendComment "Seed from MBX3" -Confirm:$False
    Update-MailboxDatabaseCopy -Identity DB2\MBX4 -SourceServer MBX3
    Suspend-MailboxDatabaseCopy -Identity DB2\MBX4 -ActivationOnly

No MBX3, execute os seguintes comandos.

    Add-MailboxDatabaseCopy -Identity DB3 -MailboxServer MBX4
    Add-MailboxDatabaseCopy -Identity DB3 -MailboxServer MBX2
    Add-MailboxDatabaseCopy -Identity DB3 -MailboxServer MBX1 -ReplayLagTime 3.00:00:00 -SeedingPostponed
    Suspend-MailboxDatabaseCopy -Identity DB3\MBX1 -SuspendComment "Seed from MBX2" -Confirm:$False
    Update-MailboxDatabaseCopy -Identity DB3\MBX1 -SourceServer MBX2
    Suspend-MailboxDatabaseCopy -Identity DB3\MBX1 -ActivationOnly

No MBX3, execute os seguintes comandos.

    Add-MailboxDatabaseCopy -Identity DB4 -MailboxServer MBX3
    Add-MailboxDatabaseCopy -Identity DB4 -MailboxServer MBX1
    Add-MailboxDatabaseCopy -Identity DB4 -MailboxServer MBX2 -ReplayLagTime 3.00:00:00 -SeedingPostponed
    Suspend-MailboxDatabaseCopy -Identity DB4\MBX2 -SuspendComment "Seed from MBX1" -Confirm:$False
    Update-MailboxDatabaseCopy -Identity DB4\MBX2 -SourceServer MBX1
    Suspend-MailboxDatabaseCopy -Identity DB4\MBX2 -ActivationOnly

Nos exemplos anteriores para o cmdlet **Add-MailboxDatabaseCopy**, o parâmetro *ActivationPreference* não foi especificado. A tarefa incrementa automaticamente o número de preferência de ativação a cada cópia adicionada. O banco de dados original sempre tem um número de preferência igual a 1. A primeira cópia adicionada com o cmdlet **Add-MailboxDatabaseCopy** recebe automaticamente um número de preferência igual a 2. Presumindo que nenhuma cópia seja removida, a próxima cópia adicionada recebe o número 3, e assim por diante. Logo, nos exemplos anteriores, a cópia passiva no mesmo datacenter da cópia ativa tem número de preferência de ativação 2; a cópia passiva sem atraso no datacenter remoto tem número de preferência de ativação 3, e a cópia passiva com atraso no datacenter remoto tem número de preferência de ativação 4.

Embora haja duas cópias de cada banco de dados ativo ao longo da WAN no outro local, a propagação pela WAN só foi realizada uma vez. Isso acontece porque a Contoso está potencializando a capacidade do Exchange 2013 para usar uma cópia passiva de um banco de dados como origem da propagação. O uso do cmdlet [Add-MailboxDatabaseCopy](https://technet.microsoft.com/pt-br/library/dd298105\(v=exchg.150\)) com o parâmetro *SeedingPostponed* impede que a tarefa propague automaticamente a nova cópia de banco de dados que está sendo criada. Assim, o administrador pode suspender a cópia não propagada e, usando o cmdlet [Update-MailboxDatabaseCopy](https://technet.microsoft.com/pt-br/library/dd335201\(v=exchg.150\)) com o parâmetro *SourceServer*, pode especificar a cópia local do banco de dados como origem da operação de propagação. Como resultado, a propagação da segunda cópia de banco de dados adicionada a cada localidade acontece localmente, e não através da WAN.


> [!TIP]
> No exemplo anterior, a cópia de banco de dados sem atraso é propagada através da WAN, e essa cópia é usada para propagar a cópia com atraso do banco de dados que está no mesmo datacenter que a cópia sem atraso.



A Contoso configurou uma das cópias passivas de cada banco de dados de caixa de correio como uma cópia de banco de dados com atraso para oferecer proteção contra o caso extremamente raro mas catastrófico de uma corrupção lógica de banco de dados. Como resultado, o administrador está configurando as cópias com atraso como bloqueadas para ativação usando o cmdlet [Suspend-MailboxDatabaseCopy](https://technet.microsoft.com/pt-br/library/dd351074\(v=exchg.150\)) com o parâmetro *ActivationOnly*. Isso garante que as cópias de banco de dados com atraso não serão ativadas se um failover de banco de dados ou servidor ocorrer.

## Validar a solução

Depois que a solução for implantada e configurada, o administrador realiza várias tarefas que validam a preparação da solução antes de mover caixas de correio de produção para os bancos de dados no DAG. A solução deve ser testada e inspecionada usando diversos métodos, incluindo simulações de falha. Para validar a solução, o administrador executa várias tarefas.

Para verificar a integridade geral do DAG, o administrador executa o cmdlet [Test-ReplicationHealth](https://technet.microsoft.com/pt-br/library/bb691314\(v=exchg.150\)). Esse cmdlet verifica vários aspectos do status de replicação e de repetição para oferecer informações sobre cada cópia de banco de dados e servidor de caixa de correio no DAG.

Para verificar a atividade de replicação e repetição, o administrador executa o cmdlet [Get-MailboxDatabaseCopyStatus](https://technet.microsoft.com/pt-br/library/dd298044\(v=exchg.150\)). Esse cmdlet pode oferecer informações de status em tempo real sobre uma cópia de banco de dados de caixa de correio específica ou sobre todas as cópias de banco de dados de caixa de correio em um servidor específico. Para mais informações sobre o monitoramento da integridade e do status de bancos de dados replicados em um DAG, consulte [Grupos de disponibilidade de banco de dados de monitoramento](monitoring-database-availability-groups-exchange-2013-help.md).

Para verificar se as alternâncias ocorrem conforme o esperado, o administrador usa o cmdlet [Move-ActiveMailboxDatabase](https://technet.microsoft.com/pt-br/library/dd298068\(v=exchg.150\)) para realizar uma série de alternâncias de bancos de dados e servidores. Quando essas tarefas forem concluídas com êxito, o administrador usa o mesmo cmdlet para mover as cópias de banco de dados ativas de volta aos seus locais originais.

Para verificar os comportamentos esperados em vários cenários de falha, o administrador realiza várias tarefas que simulam falhas ou que de fato causam as falhas. Por exemplo, o administrador pode:

  - Desconectar o cabo de alimentação no MBX1, disparando um failover de servidor. O administrador verifica se o DB1 se torna ativo em outro servidor (de preferência o MBX2, com base nos valores de preferência de ativação).

  - Desconectar o cabo de rede do adaptador de rede MAPI no MBX2, disparando um failover de servidor. O administrador verifica se o DB2 se torna ativo em outro servidor (de preferência o MBX1, com base nos valores de preferência de ativação).

  - Deixar offline o disco usado pela cópia ativa do DB3, disparando um failover de banco de dados. O administrador verifica se o DB3 se torna ativo em outro servidor (de preferência o MBX4, com base nos valores de preferência de ativação).

Podem haver outros cenários de falha testados por uma organização, tendo por base as necessidades de seus negócios. Depois de simular uma única falha (como desconectar a tomada) e verificar o comportamento de recuperação da solução, o administrador pode reverter a solução de volta à configuração original. Em alguns casos, a solução pode ser testada para várias falhas simultâneas. Em última análise, seu plano de testes de solução irá ditar se a solução será revertida de volta à configuração original após a conclusão de cada simulação de falha.

Além disso, o administrador pode optar por desconectar a conexão de rede entre os dois datacenters, simulando uma falha de site. A realização de uma alternância de datacenter é um processo muito mais complexo e coordenado; no entanto, recomendamos o processo se a solução que estiver sendo implantada tiver como objetivo proporcionar resiliência de site para os dados e serviços de mensagens.

## Fazendo a transição para operações

Depois que a solução for implantada, ela pode ser ampliada ainda mais, usando-se a implantação incremental. Nesse ponto, o gerenciamento da solução também faria a transição para processos de operação, com a realização das seguintes tarefas:

  - Monitorar a integridade e o status de DAGs e cópias de banco de dados de caixa de correio. Para mais informações, consulte [Grupos de disponibilidade de banco de dados de monitoramento](monitoring-database-availability-groups-exchange-2013-help.md).

  - Execute alternâncias de banco de dados conforme necessário. Para obter etapas detalhadas sobre como realizar um alternância de banco de dados, consulte [Ativar uma cópia do banco de dados de caixa de correio](activate-a-mailbox-database-copy-exchange-2013-help.md).

Para mais informações sobre o gerenciamento da solução, consulte [Gerenciando a alta disponibilidade e resiliência do site](managing-high-availability-and-site-resilience-exchange-2013-help.md).

