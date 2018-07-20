---
title: 'Grupos de Disponibilidade do Banco de Dados (DAGs): Exchange 2013 Help'
TOCTitle: Grupos de Disponibilidade do Banco de Dados (DAGs)
ms:assetid: ab9b88ce-2f44-4334-96ad-a666b95888a0
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Dd979799(v=EXCHG.150)
ms:contentKeyID: 50486346
ms.date: 01/10/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Grupos de Disponibilidade do Banco de Dados (DAGs)

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2015-06-04_

Saiba mais sobre o Exchange DAG no Exchange Server 2013. Este artigo discute o ciclo de vida do grupo de disponibilidade de banco de dados (DAG), além de usar um DAG para alta disponibilidade e para resiliência do site.

Um grupo de disponibilidade de banco de dados (DAG) é o componente básico da estrutura do servidor de Caixa de Correio de alta disponibilidade e de resiliência de site integrada do Microsoft Exchange Server 2013. Um DAG é um grupo de até 16 servidores de Caixa de Correio que hospeda um conjunto de bancos de dados e oferece recuperação automática no nível de banco de dados diante de falhas que afetem servidores ou bancos de dados individuais.

Um DAG é um limite para a replicação de banco de dados de caixa de correio, alternâncias e failovers de banco de dados e servidores e um componente interno chamado *Active Manager*. O Active Manager, que é executado em todos os servidores de caixa de correio, gerencia as alternâncias e os failovers dentro dos DAGs. Para mais informações sobre o Gerenciador Ativo, consulte [Active Manager](active-manager-exchange-2013-help.md).

Qualquer servidor em um DAG pode hospedar uma cópia de um banco de dados de caixa de correio de qualquer outro servidor no DAG. Quando um servidor é adicionado a um DAG, funciona com outros servidores no DAG para oferecer recuperação automática de falhas que afetem bancos de dados de caixas de correio, como falhas de disco, servidor ou rede.

**Sumário**

Ciclo de vida do grupo de disponibilidade de banco de dados (DAG)

Usando um grupo de disponibilidade de banco de dados (DAG) para alta disponibilidade

Usando um grupo de disponibilidade de banco de dados (DAG) para resiliência de site

## Ciclo de vida do grupo de disponibilidade de banco de dados (DAG)

Os DAGs utilizam o conceito de *implantação incremental*, que é a capacidade de implantar disponibilidade de dados e serviços para todos os servidores de Caixa de Correio e bancos de dados depois da instalação do Exchange. Depois de implantar os servidores de Caixa de Correio do Exchange 2013, você poderá criar um DAG, adicionar servidores de Caixa de Correio a ele e replicar bancos de dados de caixa de correio entre os membros do DAG.


> [!TIP]
> Há suporte para criar um DAG que contém uma combinação de servidores de Caixa de Correio físicos e virtualizados, desde que os servidores e a solução estejam em conformidade com os <A href="exchange-2013-system-requirements-exchange-2013-help.md">Requisitos de sistema do Exchange 2013</A> e os requisitos estabelecidos em <A href="exchange-2013-virtualization-exchange-2013-help.md">Virtualização do Exchange 2013</A>. Como em todas as configurações de alta disponibilidade do Exchange, você deve garantir que todos os servidores de Caixa de Correio no DAG sejam corretamente dimensionados para lidar com a carga de trabalho necessária durante as interrupções agendadas ou não agendadas.



Um DAG é criado usando o cmdlet [New-DatabaseAvailabilityGroup](https://technet.microsoft.com/pt-br/library/dd351107\(v=exchg.150\)). Um DAG é criado inicialmente como um objeto vazio no Active Directory. Esse objeto de diretório é usado para armazenar informações relevantes sobre o DAG, como informações de associação do servidor e algumas definições de configuração do DAG. Quando você adiciona o primeiro servidor a um DAG, um cluster de failover é criado automaticamente para o DAG. Esse cluster de failover é usado exclusivamente pelo DAG e deve ser dedicado ao DAG. O uso do cluster para qualquer outra finalidade não tem suporte.

Além de um cluster de failover ser criado, a infraestrutura que monitora os servidores em busca de falhas de rede ou servidor é iniciado. Em seguida, o mecanismo de pulsação do cluster de failover e o banco de dados do cluster são usados para acompanhar e gerenciar informações sobre o DAG que podem ser alteradas rapidamente, como o status de montagem do banco de dados, o status da replicação e o local da última montagem.

Durante a criação, o DAG recebe um nome exclusivo e um ou mais endereços IP estáticos, é configurado para usar o protocolo DHCP ou é criado sem um ponto de acesso administrativo do cluster. DAGs sem um ponto de acesso administrativo do cluster só podem ser criados em servidores com o Exchange 2013 Service Pack 1 ou versão superior no Windows Server 2012 R2 Standard ou Datacenter Edition. Os DAGs sem o ponto de acesso administrativo do cluster apresentam as seguintes características:

  - Não há um endereço IP atribuído ao cluster/DAG e, portanto, nenhum Recurso de Endereço IP no grupo de recursos principais do cluster.

  - Não há um nome de rede atribuído ao cluster e, portanto, nenhum Recurso de Nome de Rede no grupo de recursos principais do cluster.

  - O nome do cluster/DAG não é registrado no DNS e não pode ser resolvido na rede.

  - Um objeto de nome do cluster (CNO) é criado no Active Directory.

  - O cluster não pode ser gerenciado com a ferramenta de Gerenciamento de Cluster de Failover. O gerenciamento deve ser feito com o Windows PowerShell e os cmdlets do PowerShell devem ser executados em membros individuais do cluster.

Este exemplo mostra como usar o Shell para criar um DAG com um ponto de acesso administrativo do cluster que terá três servidores. Dois servidores (EX1 e EX2) estão na mesma sub-rede (10.0.0.0), e o terceiro servidor (EX3) está em uma sub-rede diferente (192.168.0.0).

    New-DatabaseAvailabilityGroup -Name DAG1 -WitnessServer EX4 -DatabaseAvailabilityGroupIPAddresses 10.0.0.5,192.168.0.5
    Add-DatabaseAvailabilityGroupServer -Identity DAG1 -MailboxServer EX1
    Add-DatabaseAvailabilityGroupServer -Identity DAG1 -MailboxServer EX2
    Add-DatabaseAvailabilityGroupServer -Identity DAG1 -MailboxServer EX3

Os comandos usados para criar um DAG sem um ponto de acesso administrativo do cluster são muito semelhantes:

    New-DatabaseAvailabilityGroup -Name DAG1 -WitnessServer EX4 -DatabaseAvailabilityGroupIPAddresses ([System.Net.IPAddress])::None
    Add-DatabaseAvailabilityGroupServer -Identity DAG1 -MailboxServer EX1
    Add-DatabaseAvailabilityGroupServer -Identity DAG1 -MailboxServer EX2
    Add-DatabaseAvailabilityGroupServer -Identity DAG1 -MailboxServer EX3

O cluster de DAG1 é criado quando EX1 é adicionado ao DAG. Durante a criação de cluster, o cmdlet **Add-DatabaseAvailabilityGroupServer** recupera os endereços IP configurados para o DAG e ignora os que não correspondem a nenhuma das sub-redes encontradas em EX1. No primeiro exemplo acima, o cluster do DAG1 é criado com um endereço IP 10.0.0.5 e 192.168.0.5 é ignorado. No segundo exemplo acima, o valor do parâmetro *DatabaseAvailabilityGroupIPAddresses* instrui a tarefa a criar um cluster de failover para o DAG que não tem um ponto de acesso administrativo do cluster. Assim, o cluster é criado com um recurso de endereço de IP ou de nome de recurso no grupo de recursos principais do cluster.

Em seguida, EX2 é adicionado, e o cmdlet **Add-DatabaseAvailabilityGroupServer** recupera novamente os endereços IP configurados para o DAG. Não são feitas alterações nos endereços IP do cluster, pois EX2 está na mesma sub-rede de EX1.

Em seguida, EX3 é adicionado, e o cmdlet **Add-DatabaseAvailabilityGroupServer** recupera novamente os endereços IP configurados para o DAG. Como uma sub-rede correspondente a 192.168.0.5 está presente em EX3, o endereço 192.168.0.5 é adicionado como um recurso de endereço IP no grupo do cluster. Além disso, uma dependência **OR** para o recurso de Nome de Rede de cada recurso de endereço IP é configurada automaticamente. O endereço 192.168.0.5 será usado pelo cluster quando o grupo de recursos principais do cluster for movido para EX3.

Para os DAGs com pontos de acesso administrativo do cluster, o cluster de failover do Windows registra os endereços IP do cluster no DNS (sistema de nomes de domínio) quando o recurso de Nome de Rede é colocado online. Além disso, quando EX1 é adicionado ao cluster, um objeto de nome do cluster (CNO) é criado no Active Directory. O nome de rede, os endereços IP e o CNO para o cluster não são usados para fins de função do DAG. Os administradores e os usuários finais não precisam interagir com ou se conectar ao nome do cluster/DAG ou ao endereço IP por motivo algum. Alguns aplicativos de terceiros se conectam ao ponto de acesso administrativo do cluster para realizar tarefas de gerenciamento, como backup ou monitoramento. Se você não usa aplicativos de terceiros que exigem um ponto de acesso administrativo do cluster e seu DAG estiver executando o Exchange 2013 SP1 ou superior no Windows Server 2012 R2, recomendamos criar um DAG sem um ponto de acesso administrativo. Isso simplifica a configuração do DAG, elimina a necessidade de ter um ou mais endereços IP e reduz a superfície de ataque do DAG.

O DAG também é configurado para usar um servidor testemunha e um diretório testemunha. O servidor testemunha e o diretório testemunha são configurados automaticamente pelo sistema ou podem ser especificados manualmente pelo administrador. No exemplo acima, EX4 (um servidor que não é, nem será, membro do DAG) está sendo configurado manualmente como o servidor testemunha do DAG.

Por padrão, um DAG é projetado para utilizar o recurso interno de replicação contínua para replicar bancos de dados de caixa de correio entre servidores no DAG. Se você estiver usando uma replicação de dados de terceiros com suporte à API de Replicação de Terceiros no Exchange 2013, o DAG deve ser criado em modo de replicação de terceiros usando o cmdlet [New-DatabaseAvailabilityGroup](https://technet.microsoft.com/pt-br/library/dd351107\(v=exchg.150\)) com o parâmetro *ThirdPartyReplication*. Depois de habilitado, este modo não pode ser desabilitado.

Depois que o DAG é criado, os servidores de Caixa de Correio podem ser adicionados ao DAG. Quando o primeiro servidor é adicionado ao DAG, um cluster é formado para utilização pelo DAG. Os DAGs fazem uso de tecnologias de cluster de failover do Windows, como a pulsação de cluster, as redes de cluster e o banco de dados de cluster (para armazenar dados que mudam, como alterações no estado do banco de dados de ativo para passivo e vice-versa, ou de montado para desmontado e vice-versa). Conforme cada servidor subsequente é adicionado ao DAG, ele entra no cluster subjacente, o modelo de quorum do cluster é ajustado automaticamente pelo Exchange, e o servidor é adicionado ao objeto DAG no Active Directory.

Depois que servidores de Caixa de Correio são adicionados a um DAG, várias propriedades do DAG podem ser configuradas, como o uso de criptografia de rede ou compactação de rede para replicação de banco de dados no DAG. Você pode também configurar redes de DAG e criar redes de DAG adicionais.

Depois de adicionar membros a um DAG e configurar o DAG, os bancos de dados de caixa de correio ativos em cada servidor podem ser replicados para os outros membros do DAG. Depois de criar cópias de banco de dados de caixa de correio, você pode monitorar a integridade e o status das cópias usando diversas ferramentas de monitoramento internas. Além disso, é possível realizar alternâncias de banco de dados e servidor.

Para mais informações sobre a criação de DAGs, o gerenciamento de associações do DAG, a configuração de propriedades do DAG, a criação e o monitoramento de cópias de banco de dados de caixa de correio e a realização de alternâncias, consulte [Gerenciando a alta disponibilidade e resiliência do site](managing-high-availability-and-site-resilience-exchange-2013-help.md).

## Modelos de quórum do grupo de disponibilidade de banco de dados (DAG)

Sob cada DAG há um cluster de failover do Windows. Clusters de failover usam o conceito de quorum, que utiliza um consenso de votantes para garantir que apenas um subconjunto dos membros do cluster (o que pode significar todos os membros ou uma maioria dos membros) esteja funcionando ao mesmo tempo. O quorum não é um conceito novo no Exchange 2013. Servidores de Caixa de Correio amplamente disponíveis em versões anteriores do Exchange também usam o cluster de failover e seu conceito de quorum. O quorum representa uma visão compartilhada de membros e recursos, e o termo "quorum" também é usado para descrever os dados físicos que representam a configuração dentro do cluster que está sendo compartilhada entre todos os membros do cluster. Como resultado, todos os DAGs exigem que seu cluster de failover subjacentes tenham quorum. Se o cluster perder quorum, todas as operações do DAG se encerram, e todos os bancos de dados montados, hospedados no DAG, serão desmontados. Nesse caso, a intervenção do administrador será necessária para corrigir o problema de quorum e restaurar as operações do DAG.

O quorum é importante para garantir a consistência, para agir como desempate para evitar o particionamento e para garantir uma boa resposta do cluster:

  - **Garantindo a consistência** Um requisito primário para um cluster de failover do Windows é que cada membro sempre tenha uma visualização do cluster consistente com a dos outros membros. O grupo de quorum funciona como o repositório definitivo de todas as informações de configuração relacionadas ao cluster. Se o grupo de cluster não puder ser carregado localmente em um membro do DAG, o serviço Cluster não inicia, porque não pode garantir que o membro atenda ao requisito de ter uma visualização do cluster consistente com a de outros membros.

  - **Agindo como um desempate** Um recurso de testemunha de quorum é usado em DAGs com um número par de membros para evitar cenários de síndrome do cérebro dividido, e para garantir que apenas uma coleção dos membros do DAG seja considerada oficial. Quando o servidor testemunha é necessário para o quorum, qualquer membro do DAG que possa se comunicar com o servidor testemunha pode pôr um bloqueio de protocolo SMB no arquivo witness.log do servidor testemunha. O membro do DAG que bloqueia o servidor testemunha (chamado de *nó de bloqueio*) mantém um voto adicional para fins de quorum. Os membros do DAG em contato com o nó de bloqueio estão em maioria e mantêm quorum. Quaisquer membros do DAG que não possam contatar o nó de bloqueio estão em minoria e portanto perdem quorum.

  - **Garantindo uma boa capacidade de resposta** Para garantir uma boa capacidade de resposta, o modelo de quorum se certifica de que, sempre que o cluster estiver em execução, membros suficientes do sistema distribuído estejam operacionais e comunicativos, e que pelo menos uma réplica do estado atual do cluster possa ser garantida. Não é necessário tempo adicional para fazer os membros se comunicarem ou para determinar se uma réplica específica é garantida.

DAGs com um número par de membros usam modo de quorum Maioria dos Nós e Compartilhamento de Arquivo do cluster de failover, que emprega um servidor testemunha externo que age para desempatar. Nesse modo de quórum, cada membro do DAG conta com um voto. Além disso, o servidor testemunha é usado para fornecer um membro do DAG com uma votação ponderada (por exemplo, conta dois votos em vez de um). Os dados de quorum do cluster são armazenados por padrão no disco do sistema de cada membro do DAG e é mantido consistente nesses discos. Entretanto, uma cópia dos dados do quorum não será armazenada no servidor testemunha. Um arquivo no servidor testemunha é usado para manter o controle de qual membro tem a cópia mais atualizada dos dados, mas o servidor testemunha não tem uma cópia dos dados de quorum do cluster. Neste modo, a maioria dos votantes (os membros do DAG somados ao servidor testemunha) deve estar operacional e ser capaz de se comunicar entre si para manter o quorum. Se a maioria dos votantes não puder se comunicar com os outros, o cluster subjacente do DAG perde quorum e o DAG exigirá intervenção administrativa para tornar-se novamente operacional.

Os DAGs com número ímpar de membros usam o modo de quorum Maioria dos Nós do cluster de failover. Neste modo, cada membro tem um voto e o disco de sistema local de cada membro é usado para armazenar os dados de quorum do cluster. Se a configuração do DAG for alterada, essa alteração é refletida nos diferentes discos. A alteração só é considerada como confirmada e realizada de forma persistente se for feita nos discos de metade dos membros (arredondando para baixo) mais um. Por exemplo, em um DAG de cinco membros, a alteração deve ser feita em dois membros mais um, ou três membros no total.

O quorum exige que a maioria dos votantes seja capaz de se comunicar entre si. Considere um DAG com quatro membros. Como este DAG tem um número par de membros, um servidor testemunha externo é usado para fornecer a um dos membros do cluster um quinto voto, para desempate. Para manter uma maioria de votantes (e com isso o quorum), pelo menos três votantes devem ser capazes de se comunicar entre si. A qualquer momento, um máximo de dois votantes podem estar offline sem interromper o serviço e o acesso aos dados. Se três ou mais votantes estiverem offline, o DAG perde quorum e o acesso aos dados e ao serviço é interrompido até o problema ser resolvido.

Voltar ao início

## Usando um grupo de disponibilidade de banco de dados (DAG) para alta disponibilidade

Para ilustrar como um DAG pode oferecer alta disponibilidade aos seus bancos de dados de caixa de correio, considere o exemplo a seguir, que usa um DAG com cinco membros. Esse DAG é ilustrado na figura a seguir.

**DAG com cinco membros**

![Grupo de Disponibilidade de Banco de Dados (DAG)](images/Dd979799.21fcbf7b-cb10-49c0-8e32-bdf3c03f825d(EXCHG.150).gif "Grupo de Disponibilidade de Banco de Dados (DAG)")

Na figura anterior, os bancos de dados verdes são cópias ativas de banco de dados de caixa de correio e os bancos de dados azuis são cópias passivas de banco de dados de caixa de correio. Neste exemplo, as cópias de banco de dados não são espelhadas em cada servidor, mas sim distribuídas em vários servidores. Isso garante que dois servidores do DAG não terão o mesmo conjunto de cópias de banco de dados, dando ao DAG uma maior resiliência a falhas, incluindo as que ocorrem enquanto outros componentes não estão disponíveis como resultado de manutenção regular.

Considere o seguinte cenário, usando o DAG do exemplo anterior, que ilustra resiliências a múltiplas falhas de banco de dados e servidor.

Inicialmente, todos os bancos de dados e servidores têm integridade. É necessário instalar algumas atualizações de sistema operacional no EX2 para que você coloque o servidor no modo de manutenção. Isso resulta em uma alternância de servidor, que ativa a cópia de DB4 em outro servidor de Caixa de Correio. Uma alternância de servidor move todas as cópias de banco de dados de caixa de correio ativas de seu servidor atual para um ou mais servidores de caixa de correio no DAG em preparação para uma interrupção agendada do servidor atual. Neste exemplo, há apenas um banco de dados de caixa de correio ativa no EX2 (DB4), portanto apenas uma cópia de caixa de correio ativa é movida.

**DAG com um servidor offline para manutenção**

![Grupo de Disponibilidade de Banco de Dados (DAG) com um Servidor Offline](images/Dd979799.f48f0e77-80e1-4f14-8c36-112393895bdc(EXCHG.150).gif "Grupo de Disponibilidade de Banco de Dados (DAG) com um Servidor Offline")

Enquanto você realiza a manutenção em EX2, EX3 passa por uma falha de hardware catastrófica e fica offline. Antes de ficar offline, EX3 hospedava a cópia ativa de DB2. Para se recuperar da falha, o sistema ativa automaticamente a cópia de DB2 hospedada em EX1 em 30 segundos. Isso é ilustrado na figura a seguir.

**DAG com um servidor offline para manutenção e um servidor com falha**

![DAG com um servidor offline e um servidor com falha](images/Dd979799.9bbfd9e7-3881-4957-ae8d-32318cbc208b(EXCHG.150).gif "DAG com um servidor offline e um servidor com falha")

Depois que a manutenção agendada é concluída para EX2, você coloca o servidor online e o retira do modo de manutenção. Assim que EX2 fica disponível, os outros membros do DAG são notificados, e as cópias de DB1, DB4 e DB5 hospedadas em EX2 são sincronizadas automaticamente com a cópia ativa de cada banco de dados. Isso é ilustrado na figura a seguir.

**DAG com servidor restaurado sincronizando suas cópias de bancos de dados**

![DAG com servidor restaurado ressincronizando bancos de dados](images/Dd979799.58601531-e078-41d3-9287-e8e470ef7f41(EXCHG.150).gif "DAG com servidor restaurado ressincronizando bancos de dados")

Depois que o componente de hardware com falha de EX3 é substituído por um novo componente, EX3 é posto online. Depois que EX3 fica disponível, os outros membros do DAG são notificados, e as cópias de DB2, DB3 e DB4 hospedadas em EX3 são sincronizadas automaticamente com a cópia ativa de cada banco de dados. Isso é ilustrado na figura a seguir.

**DAG com servidor reparado sincronizando suas cópias de bancos de dados**

![DAG com Membro Ressincronizando Cópias de Bancos de Dados](images/Dd979799.56259671-e840-4cf0-9ea2-3657dc36c035(EXCHG.150).gif "DAG com Membro Ressincronizando Cópias de Bancos de Dados")

Voltar ao início

## Usando um grupo de disponibilidade de banco de dados (DAG) para resiliência de site

Além de oferecer alta disponibilidade em um data center, um DAG também pode ser ampliado para um ou mais datacenters, em uma configuração que oferece resiliência de site para um ou vários datacenters. Nas figuras do exemplo anterior, o DAG está localizado em um único datacenter e em um único site do Active Directory. A implantação incremental pode ser usada para ampliar esse DAG para um segundo datacenter (e um segundo site do Active Directory) por meio da implantação de um servidor de Caixa de Correio e dos recursos de suporte necessários (um ou mais servidores do Active Directory e serviços de DNS. O servidor de Caixa de Correio é então adicionado ao DAG, como é ilustrado na figura a seguir.

**DAG estendido a dois sites do Active Directory**

![DAG estendido entre dois sites do Active Directory](images/Dd979799.28e96e9d-d7d6-451a-b7b8-c06122c81dc9(EXCHG.150).gif "DAG estendido entre dois sites do Active Directory")

Neste exemplo, uma cópia passiva de cada banco de dados ativo no datacenter Redmond é configurada em EX6 no datacenter Dublin. Entretanto, há muitos outros exemplos de configurações de DAG que oferecem resiliência de site. Por exemplo:

  - Em vez de hospedar apenas cópias passivas de banco de dados, o EX6 poderia hospedar todas as cópias ativas, ou poderia hospedar um misto de cópias ativas e passivas.

  - Além do EX6, vários membros do DAG poderiam ser implantados no datacenter Dublin, oferecendo proteção contra falhas adicionais. A configuração também oferece capacidade adicional, de modo que se o datacenter Redmond falhar, o datacenter Dublin possa suportar uma população muito maior.

## Usando vários grupos de disponibilidade de banco de dados (DAGs) para resiliência de site

No exemplo anterior, um único DAG se estende por vários datacenters, oferecendo resiliência de site para um dos ou ambos os datacenters. Ao usar um único DAG para oferecer resiliência de site em um ambiente no qual cada datacenter para o qual você estende o DAG tem uma população ativa de usuários, há um único ponto de falha na conexão WAN. Isso acontece porque o quorum exige que a maioria dos votantes seja ativa e capaz de se comunicar entre si.

No exemplo anterior, a maioria dos votantes está localizada no datacenter Redmond. Se o datacenter Dublin hospedar bancos de dados de caixa de correio ativos e tiver uma população local de usuários, uma interrupção na WAN resultaria em uma interrupção no serviço de mensagens para os usuários de Dublin. Quando a conectividade WAN é interrompida, apenas os membros do DAG no datacenter Redmond mantêm quorum e continuam oferecendo o serviço de mensagens.

Para eliminar o WAN como ponto único de falha quando precisar oferecer resiliência de site para vários datacenters, cada um com uma população ativa de usuários, é necessário implantar vários DAGs, onde cada DAG tem uma maioria de votantes em um datacenter separado. Quando ocorre uma interrupção de WAN, a replicação é bloqueada até que a conectividade seja restaurada. Os usuários terão o serviço de mensagens, porque cada DAG continua servindo sua população local de usuários.

Voltar ao início

