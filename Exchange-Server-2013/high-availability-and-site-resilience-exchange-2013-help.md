---
title: 'Alta disponibilidade e resiliência de site: Exchange 2013 Help'
TOCTitle: Alta disponibilidade e resiliência de site
ms:assetid: 6628285e-d07c-443d-866b-be784ad1ed1e
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Dd638137(v=EXCHG.150)
ms:contentKeyID: 50485752
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Alta disponibilidade e resiliência de site

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2016-12-15_

No Microsoft Exchange Server 2013, você pode proteger bancos de dados de caixa de correio e seus dados configurando os bancos de dados de caixa de correio para alta disponibilidade e resiliência de site. O Exchange 2013 reduz o custo e a complexidade de implantar uma solução de mensagens resiliente e altamente disponível, enquanto fornece níveis mais altos de disponibilidade de serviço e dados e oferece suporte a grandes caixas de correio.

O Exchange 2013 permite que clientes de todos os tamanhos e em todos os segmentos implantem um serviço de continuidade de mensagens em sua organização de maneira econômica, valendo-se de recursos de replicação nativos e arquitetura de alta disponibilidade introduzidos no Exchange 2010. Para obter uma lista das alterações do Exchange 2010 e Exchange 2007, consulte [Alterações na alta disponibilidade e resilência de site em relação às versões anteriores](changes-to-high-availability-and-site-resilience-over-previous-versions-exchange-2013-help.md)

**Sumário**

Key terminology

Database availability groups

Mailbox database copies

Active Manager

Site resilience

Third-party replication API

High availability and site resilience documentation

## Terminologia principal

Os seguintes termos principais são importantes para entender a alta disponibilidade ou a resiliência de site:

  - *Active Manager*  
    Um componente interno do Exchange executado dentro do serviço de Replicação do Microsoft Exchange responsável pelo monitoramento de falhas e pela ação corretiva por meio de failover em um grupo de disponibilidade de banco de dados (DAG).

<!-- end list -->

  - *AutoDatabaseMountDial*  
    Uma configuração de propriedade de um servidor de Caixa de Correio que determina se uma cópia de banco de dados passiva será montada como a nova cópia ativa, com base no número de arquivos de log ausentes na cópia sendo montada.

<!-- end list -->

  - *Replicação contínua - modo de bloqueio*  
    No modo de bloqueio, cada atualização, ao ser gravada na buffer de log ativo da cópia ativa do banco de dados, também é enviada para um buffer de log em cada uma das cópias passivas da caixa de correio no modo de bloqueio. Quando o buffer de log estiver cheio, cada cópia do banco de dados desenvolve, inspeciona e cria o próximo arquivo de log na sequência de geração.

<!-- end list -->

  - *Replicação contínua - modo de arquivo*  
    No modo de arquivo, os arquivos de log de transações fechadas são enviados da cópia ativa do banco de dados para uma ou mais cópias passivas do bancos de dados.

<!-- end list -->

  - *Grupo de disponibilidade de banco de dados*  
    Um grupo de até 16 servidores de Caixa de Correio do Exchange 2013 que hospedam um conjunto de bancos de dados replicados.

<!-- end list -->

  - *Mobilidade de banco de dados*  
    A capacidade de um banco de dados de caixa de correio do Exchange 2013 ser replicado e montado e outros servidores de Caixa de Correio do Exchange 2013.

<!-- end list -->

  - *Data center*  
    Normalmente, isso se refere a um site do Active Directory; no entanto, pode também se referir a um local físico. No contexto desta documentação, datacenter é igual a site do Active Directory.

<!-- end list -->

  - *modo Coordenação de Ativação do Banco de Dados*  
    A propriedade da configuração do DAG que, quando habilitada, força o serviço de Replicação do Microsoft Exchange a adquirir permissão para montar bancos de dados na inicialização.

<!-- end list -->

  - *Recuperação de desastres*  
    Qualquer processo usado para se recuperar manualmente de uma falha. Pode ser uma falha que afeta um único item, ou uma falha que afeta toda uma localização física.

<!-- end list -->

  - *API de replicação de terceiros do Exchange*  
    Uma API fornecida pelo Exchange que permite o uso de replicação síncrona de terceiros para um DAG, ao invés de replicação contínua.

<!-- end list -->

  - *Alta disponibilidade*  
    Uma solução que fornece disponibilidade de serviço, de dados, e recuperação automática de falhas que afetam o serviço ou dados (como uma falha de rede, armazenamento ou servidor).

<!-- end list -->

  - *Implantação incremental*  
    A capacidade de implantar alta disponibilidade e resiliência de site depois da instalação do Exchange 2013.

<!-- end list -->

  - *Cópia de banco de dados de caixa de correio defasada*  
    Uma cópia de banco de dados passiva que tem um intervalo de repetição de log superior a zero.

<!-- end list -->

  - *Cópia de banco de dados de caixa de correio*  
    Um banco de dados de caixa de correio (arquivo .edb e logs), que é ativo ou passivo.

<!-- end list -->

  - *Resiliência de caixa de correio*  
    O nome de uma solução unificada de alta disponibilidade e resiliência de site no Exchange 2013.

<!-- end list -->

  - *Disponibilidade gerenciada*  
    Um conjunto de processos internos compostos por investigações, monitoramentos e respondentes que incorporam o monitoramento e a alta disponibilidade em todas as funções de servidor e em todos os protocolos.

<!-- end list -->

  - *\*over*(pronuncia-se "star over")  
    Abreviação para *switchovers* (alternâncias) e *failovers*. Uma alternância é uma ativação manual de uma ou mais cópias de bancos de dados. Um failover é uma ativação automática de uma ou mais cópias de bancos de dados após uma falha.

<!-- end list -->

  - *Rede de Segurança*  
    Anteriormente conhecido como o dumpster de transporte, este é um recurso do serviço de transporte que armazena uma cópia de todas as mensagens por *X* dias. A configuração padrão é de 2 dias.

<!-- end list -->

  - *Redundância de sombra*  
    Um recurso de servidor de transporte que fornece redundância para mensagens durante todo o tempo em que estão em trânsito.

<!-- end list -->

  - *Resiliência do site*  
    Uma configuração que estende a infraestrutura de mensagens para multiplicar os sites de Active Directory e fornecer continuidade operacional para o sistema de mensagens no caso de uma falha afetar um dos sites.

Voltar ao início

## Grupos de disponibilidade do banco de dados

Um DAG é o componente base da estrutura de alta disponibilidade e resiliência de site interna do Exchange 2013. Um DAG é um grupo de até 16 servidores de Caixa de Correio que hospeda um conjunto de bancos de dados e oferece recuperação automática no nível de banco de dados diante de falhas que afetem bancos de dados, redes ou servidores individuais. Qualquer servidor em um DAG pode hospedar uma cópia de um banco de dados de caixa de correio de qualquer outro servidor no DAG. Quando um servidor é adicionado a um DAG, funciona com outros servidores no DAG para oferecer recuperação automática de falhas que afetem bancos de dados de caixa de correio, como uma falha de disco ou uma falha do servidor. Para obter mais informações sobre DAGs, consulte [Grupos de Disponibilidade do Banco de Dados (DAGs)](database-availability-groups-dags-exchange-2013-help.md).

Voltar ao início

## Cópias de banco de dados de caixa de correio

Os recursos de alta disponibilidade e resiliência de site, introduzidos pela primeira vez no Exchange 2010, são usados no Exchange 2013 para criar e manter cópias de bancos de dados. O Exchange 2013 também aproveita o conceito de mobilidade de banco de dados, composto por failovers em nível de banco de dados gerenciados por Exchange.

A mobilidade de banco de dados desconecta bancos de dados dos servidores, adiciona suporte para até 16 cópias de um único banco de dados. Ele também oferece uma experiência nativa para a criação de cópias de um banco de dados.

Definir uma cópia de banco de dados como o banco de dados de caixa de correio ativo é conhecido como *alternância*. Quando uma falha que afeta um banco de dados ou o acesso a um banco de dados ocorre e um novo banco de dados torna-se a cópia ativa, esse processo é conhecido como *failover*. Este processo também refere-se a uma falha de servidor na qual um ou mais servidores colocam online o banco de dados que anteriormente estava online no servidor onde a falha aconteceu. Quando uma alternância ou failover ocorre, outros servidores Exchange 2013 tomam conhecimento da alternância quase imediatamente e redirecionam o tráfego de mensagens e os clientes para o novo banco de dados ativo.

Por exemplo, se um banco de dados ativo em um DAG falhar devido a uma falha do armazenamento subjacente, o Active Manager automaticamente se recupera, executando failover para uma cópia do banco de dados em outro servidor de Caixa de Correio no DAG. No Exchange 2013, a disponibilidade gerenciada adiciona novos comportamentos para recuperação a partir de perda de acesso de protocolo a um banco de dados, incluindo a reciclagem de pools de trabalhos de aplicativos, a reinicialização de serviços e servidores e a inicialização de failovers de banco de dados.

Para obter mais informações sobre cópias de banco de dados de caixa de correio, consulte [Cópias de banco de dados de caixa de correio](mailbox-database-copies-exchange-2013-help.md).

Voltar ao início

## Active Manager

O Exchange 2013 utiliza o componente do Active Manager apresentado no Exchange 2010 para gerenciar o banco de dados e a integridade de cópia do banco de dados, o status, a replicação contínua e outros aspectos de alta disponibilidade do servidor de Caixa de Correio. Para obter mais informações sobre o Active Manager, consulte [Active Manager](active-manager-exchange-2013-help.md).

Voltar ao início

## Resiliência do site

Embora o Exchange 2013 continue a usar os DAGs e o Cluster de Failover do Windows para alta disponibilidade da função de servidor de Caixa de Correio e resiliência de site, a resiliência de site não é a mesma no Exchange 2013. A resiliência de site é muito melhor no Exchange 2013 porque ela foi simplificada. As alterações de arquitetura subjacentes que foram feitas no Exchange 2013 têm impacto significativo nos aspectos de recuperação de uma configuração de resiliência de site.

No Exchange 2010, a recuperação de caixa de correio (DAG) e de acesso para cliente (matriz de servidor de Acesso para Cliente) era feita em conjunto. Se perdesse todos os seus servidores de Acesso para Cliente ou o VIP para a matriz ou perdesse uma parte significativa do seu DAG, você ficaria em uma situação em que precisava fazer uma alternância de data center. Esse é um processo bem-documentado e geralmente bem-compreendido, embora leve tempo para ser executado e exija intervenção humana para iniciar o processo.

No Exchange 2013, se perder sua matriz de servidor de Acesso para Cliente (por exemplo, o balanceador de carga falhar), você não precisará realizar uma alternância de data center. Com a configuração correta, o failover ocorre no nível de cliente, e os clientes são automaticamente redirecionados para um segundo data center que tem servidores de Acesso para Cliente operacionais, e esses servidores usam um proxy na comunicação de volta para o servidor de Caixa de Correio, que permanece não afetado pela interrupção (porque você não faz uma alternância). Em vez de trabalhar para recuperar o serviço, o serviço se autorrecupera e você pode se concentrar na correção do problema principal (por exemplo, substituir o balanceador de carga com falha).

Além do mais, com a simplificação de namespace, a consolidação de funções de servidor, a remoção dos requisitos de função de servidor do site do Active Directory, a separação da matriz do servidor de Acesso para Cliente e a recuperação do DAG, além das alterações de balanceamento de carga, há mudanças no Exchange 2013 que agora permitem que a recuperação do servidor de Acesso para Cliente e do DAG seja separada e automática nos sites, fornecendo dessa forma cenários de failover de datacenter, se você tiver três locais.

No Exchange 2010, era possível implantar um DAG entre dois data centers e hospedar o testemunha em um terceiro data center e habilitar o failover para a função de servidor de Caixa de Correio para um dos data centers. Mas, você não obtinha failover para a própria solução porque o namespace ainda precisava ser manualmente alterado para as funções de servidor que não são de Caixa de Correio.

No Exchange 2013, o namespace não precisa acompanhar o DAG. O Exchange utiliza a tolerância a falhas integrada ao namespace por meio de vários endereços IP, balanceamento de carga (e se necessário, a capacidade de colocar os servidores em operação e tirá-los de operação). Os clientes HTTP modernos funcionam com esta redundância automaticamente. A pilha HTTP pode aceitar vários endereços IP para um nome de domínio totalmente qualificado (FQDN), e se o primeiro endereço IP que ela tentar tiver falha grave (ou seja, não conseguir se conectar), ela tentará o próximo endereço IP na lista. Em uma falha de software (conexão perdida após estabelecimento da sessão, talvez devido a uma falha intermitente no serviço em que, por exemplo, um dispositivo está ignorando pacotes e precisa ser retirado de operação), pode ser que o usuário precise atualizar seu navegador.

Isso significa que o namespace não é mais um ponto único de falha, como era no Exchange 2010. No Exchange 2010, talvez o maior ponto único de falha no sistema de mensagens seja o FQDN que você fornece aos usuários porque ele informa o usuário aonde ir. No paradigma do Exchange 2010, mudar onde esse FQDN vai não é tão fácil porque você precisa alterar o DNS e lidar com a latência de DNS, o que em algumas partes do mundo é muito ruim. E você tem caches de nome nos navegadores que geralmente levam cerca de 30 minutos ou mais e com os quais é preciso lidar também.

Uma das mudanças no Exchange 2013 é permitir que os clientes tenham mais de um lugar para ir. Considerando que o cliente tem a capacidade de usar mais de um lugar para ir (quase todos os protocolos de acesso para cliente no Exchange 2013 são baseados em HTTP - exemplos incluem Outlook, Outlook em Qualquer Lugar, EAS, EWS, OWA e EAC - e todos os clientes HTTP com suporte têm a capacidade de usar vários endereços IP), proporcionando dessa forma failover no lado do cliente. Você pode configurar o DNS para lidar com vários endereços IP para um cliente durante uma resolução de nome. O cliente solicita mail.contoso.com e recebe de volta dois endereços IP ou quatro endereços IP, por exemplo. Contudo, vários endereços IP que o cliente recebe de volta serão usados de maneira confiável pelo cliente. Isso torna o cliente bem melhor porque se um dos endereços IP falhar, o cliente tem outros endereços IP para tentar se conectar. Se um cliente tentar um e ele falhar, ele aguardará cerca de 20 segundos e tentará o próximo na lista. Dessa forma, se você perder o VIP para a matriz de servidor de Acesso para Cliente, a recuperação dos clientes acontecerá automaticamente e em aproximadamente 21 segundos.

Os benefícios são os seguintes:

  - No Exchange 2010, se você perdesse o balanceador de carga no seu data center principal e não tivesse outro nesse site, era necessário fazer uma alternância de data center. No Exchange 2013, se perdesse o balanceador de carga no seu site principal, você simplesmente o desativava (ou talvez desativava o VIP) e o reparava ou substituía. Os clientes que ainda não estão usando o VIP no data center secundário farão automaticamente failover para o VIP secundário sem nenhuma alteração de namespace e sem nenhuma alteração no DNS. Isso não só significa que você não precisará mais realizar a alternância, mas também que todo o tempo normalmente associado a uma recuperação de alternância de data center não será gasto. No Exchange 2010, você precisava lidar com a latência de DNS (daí, a recomendação para definir a vida útil (TTL) como 5 minutos, e a introdução da URL de failback). No Exchange 2013, não é preciso fazer isso porque você obtém failover rápido (20 segundos) do namespace entre VIPs (data centers).

  - Como você pode realizar failover o namespace entre data centers, todas as opções que são necessárias para obter um failover de datacenter é um mecanismo para failover da função de servidor de caixa de correio em datacenters. Para obter failover automático para o DAG, simplesmente projetar uma solução que onde os DAG uniformemente é dividido entre dois datacenters e, em seguida, colocar o servidor testemunha em um local de terceiro para que ele possa ser arbitrários pelos membros do DAG em um datacenter, independentemente do estado da rede entre os centros de dados que contêm os membros do DAG. Se você tiver apenas dois data centers e um terceiro local físico não estiver disponível, você pode colocar o servidor testemunha em uma máquina virtual de Microsoft Azure. Consulte [Usando uma VM do Microsoft Azure como um servidor de testemunha do DAG](using-a-microsoft-azure-vm-as-a-dag-witness-server-exchange-2013-help.md) para obter mais informações.

  - Nesse cenário, os esforços do administrador são para simplesmente corrigir o problema e não para restaurar o serviço. Você simplesmente corrige a coisa que falhou; enquanto isso, o serviço está em operação, e a integridade dos dados foi mantida. O nível de urgência e estresse que você sente ao reparar um dispositivo quebrado não é nada como a urgência e o estresse que sente quando está trabalhando para restaurar o serviço. É melhor para o usuário e menos estressante para o administrador.

Você pode permitir que o failover ocorra sem precisar realizar switchbacks (às vezes mencionadas incorretamente como failbacks). Se perder os servidores de Acesso para Cliente no datacenter principal e isso resultar em uma interrupção de 20 segundos para os clientes, você não precisará se preocupar com o failback. Nesse ponto, sua preocupação principal seria corrigir o problema principal (por exemplo, substituir o balanceador de carga com falha). Quando isso estiver online novamente e funcionando, alguns clientes começarão a usá-lo, e outros poderão continuar operacional por meio do segundo data center.

O Exchange 2013 também fornece funcionalidade que permite aos administradores lidar com falhas intermitentes. Uma falha intermitente é quando, por exemplo, a conexão TCP inicial pode ser feita, mas nada acontece em seguida. Uma falha intermitente requer que um tipo de ação administrativa extra seja executada porque ela pode ser resultado de um dispositivo de substituição sendo colocado em operação. Enquanto este processo de reparo estiver ocorrendo, o dispositivo poderá ser ligado e aceitar algumas solicitações, mas não estará realmente pronto para atender os clientes até a execução das etapas de configuração necessárias. Nesse cenário, o administrador pode executar uma alternância de namespace simplesmente removendo o VIP do dispositivo sendo substituído a partir do DNS. Em seguida, durante esse período de serviço, nenhum cliente tentará se conectar a ele. Quando o processo de substituição tiver terminado, o administrador poderá adicionar o VIP de volta ao DNS, e os clientes finalmente começarão a utilizá-lo.

Para detalhes sobre planejamento e implantação de resiliência do site, consulte [Planejamento de alta disponibilidade e de resiliência do site](planning-for-high-availability-and-site-resilience-exchange-2013-help.md) e [Implantando a alta disponibilidade e resiliência do site](deploying-high-availability-and-site-resilience-exchange-2013-help.md).

Voltar ao início

## API de replicação de terceiros

O Exchange 2013 também inclui uma API de replicação de terceiros que permite que as organizações usem soluções de replicação síncronas de terceiros, ao invés do recurso de replicação contínua interno. A Microsoft oferece suporte a soluções de terceiros que usam essa API, desde que a solução ofereça as funcionalidades necessárias para substituir todas as funcionalidades nativas de replicação contínua que são desabilitadas como resultado do uso da API. As soluções têm suporte apenas quando a API é usada dentro de um DAG para gerenciar e ativar cópias do banco de dados de caixa de correio. Não há suporte ao uso da API fora desses limites. Além disso, a solução deve atender às especificações aplicáveis de suporte a hardware do Windows. (O teste de validação não é necessário para suporte.)

Ao implantar uma solução que usa a API de replicação de terceiros interna, lembre-se de que o fornecedor de solução é responsável pelo suporte principal da solução. A Microsoft oferece suporte a dados do Exchange para soluções não replicado e replicadas. Soluções que usam a replicação de dados devem cumprir a política de suporte da Microsoft para a replicação de dados, conforme descrito no artigo da Base de Conhecimento Microsoft 895847, [replicação de dados de multi-site de suporte para o Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=3052&kbid=895847). Além disso, soluções que utilizam o modelo de recurso de Cluster de Failover do Windows devem atender aos requisitos de suporte de cluster Windows conforme descrito no artigo da Base de Conhecimento Microsoft 943984, [a Microsoft suporte política para Windows Server 2008 ou Clusters de Failover do Windows Server 2008 R2](https://go.microsoft.com/fwlink/p/?linkid=3052&kbid=943984) ou [O Microsoft suporte política para Windows Server 2012 Failover Clusters](https://go.microsoft.com/fwlink/p/?linkid=3052&kbid=2775067).

A política de suporte para restaruação e backup da Microsoft para implantações que usam soluções baseadas em API de replicação de terceiros é a mesma que aquela para implantações nativas de replicação contínua.

Se você for um parceiro procurando informações sobre a API de replicação de terceiros, entre em contato com seu representante Microsoft.

Voltar ao início

## Documentação de resiliência de site e disponibilidade elevada

A tabela a seguir contém links para tópicos que irão ajudar você a aprender sobre e gerenciar DAGs, cópias de banco de dados de caixa de correio e backup e restauração para Exchange 2013.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Tópico</th>
<th>Descrição</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="database-availability-groups-dags-exchange-2013-help.md">Grupos de Disponibilidade do Banco de Dados (DAGs)</a></p></td>
<td><p>Saiba mais sobre DAGs, Active Manager, o modo Coordenação de Ativação de Datacenter (DAC) e cópias de banco de dados de caixa de correio.</p></td>
</tr>
<tr class="even">
<td><p><a href="planning-for-high-availability-and-site-resilience-exchange-2013-help.md">Planejamento de alta disponibilidade e de resiliência do site</a></p></td>
<td><p>Saiba mais sobre geral, hardware, rede, software, servidor testemunha e outros requisitos e práticas recomendadas para DAGs.</p></td>
</tr>
<tr class="odd">
<td><p><a href="deploying-high-availability-and-site-resilience-exchange-2013-help.md">Implantando a alta disponibilidade e resiliência do site</a></p></td>
<td><p>Explore um cenário de exemplo de implantação para implantar e configurar DAGs.</p></td>
</tr>
<tr class="even">
<td><p><a href="managing-high-availability-and-site-resilience-exchange-2013-help.md">Gerenciando a alta disponibilidade e resiliência do site</a></p></td>
<td><p>Saiba mais sobre as tarefas de gerenciamento de DAG, alternâncias e failovers e modo de manutenção.</p></td>
</tr>
<tr class="odd">
<td><p><a href="monitoring-database-availability-groups-exchange-2013-help.md">Grupos de disponibilidade de banco de dados de monitoramento</a></p></td>
<td><p>Saiba mais sobre os cmdlets e scripts incorporados para monitorar DAGs cópias de banco de dados.</p></td>
</tr>
<tr class="even">
<td><p><a href="backup-restore-and-disaster-recovery-exchange-2013-help.md">Backup, restauração e recuperação de desastres</a></p></td>
<td><p>Leia sobre backup e restauração de bancos de dados do Exchange, bancos de dados de recuperação e recuperação de servidor.</p></td>
</tr>
</tbody>
</table>


Voltar ao início

