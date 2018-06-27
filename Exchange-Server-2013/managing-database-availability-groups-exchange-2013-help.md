---
title: 'Gerenciando grupos de disponibilidade de banco de dados: Exchange 2013 Help'
TOCTitle: Gerenciando grupos de disponibilidade de banco de dados
ms:assetid: 74be3f97-ec0f-4d2a-b5d8-7770cc489919
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Dd298065(v=EXCHG.150)
ms:contentKeyID: 50485937
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Gerenciando grupos de disponibilidade de banco de dados

 

_**Aplica-se a:**Exchange Server 2013_

_**Tópico modificado em:**2017-10-04_

DAG (grupo de disponibilidade do banco de dados) é um conjunto de até 16 servidores de caixa de correio do Microsoft Exchange Server 2013 que fornece recuperação automática no nível de banco de dados, diante de uma falha no banco de dados, no servidor ou na rede. Os DAGs utilizam replicação contínua e uma sub-rede de tecnologias de cluster de failover do Windows para fornecer alta disponibilidade e resiliência de site. Servidores de caixa de correio em um DAG monitoram-se por falhas. Ao ser adicionado a um DAG, um servidor de Caixa de Correio funciona com outros servidores no DAG para fornecer recuperação automática em nível de banco de dados a partir de falhas de banco de dados.

Quando criado, um DAG está vazio. Quando você adiciona o primeiro servidor a um DAG, um cluster de failover é criado automaticamente para o DAG. Além disso, é iniciada a infraestrutura que monitora os servidores em busca de falhas de rede ou servidor. Em seguida, o mecanismo de pulsação do cluster de failover e o banco de dados do cluster são usados para acompanhar e gerenciar informações sobre o DAG que podem ser alteradas rapidamente, como o status de montagem do banco de dados, o status da replicação e o local da última montagem.

**Sumário**

Creating DAGs

DAG membership

Configuring DAG properties

DAG networks

Configuring DAG members

Performing maintenance on DAG members

Shutting down DAG members

Installing updates on DAG members

## Criando DAGs

Um DAG pode ser criado usando-se o assistente de Novo Grupo de Disponibilidade de Banco de Dados, no Centro de Administração do Exchange (EAC) ou executando-se o cmdlet **New-DatabaseAvailabilityGroup**, no Shell de Gerenciamento do Exchange. Ao criar um DAG, você fornece um nome para o DAG, um servidor testemunha opcional e as configurações do diretório testemunha. Além disso, atribua um ou mais endereços IP ao DAG, usando endereços IP estáticos ou permitindo que os endereços IP necessários sejam atribuídos automaticamente ao DAG, usando o protocolo DHCP. É possível atribuir endereços IP manualmente ao DAG usando-se o parâmetro *DatabaseAvailabilityGroupIpAddresses*. Se você omitir esse parâmetro, o DAG tentará obter um endereço IP usando um servidor DHCP na rede.

Se estiver criando um DAG que conterá servidores de Caixa de Correio que estejam executando o Windows Server 2012 R2, você também terá a opção de criar um DAG sem um ponto de acesso administrativo de cluster. Nesse caso, o cluster não terá um objeto de nome do cluster (CNO) no Active Directory e o grupo de recursos principais do cluster não conterá um recurso de nome de rede ou um recurso de endereço IP.

Para instruções detalhadas sobre como criar um DAG, consulte [Criar um grupo de disponibilidade do banco de dados](create-a-database-availability-group-exchange-2013-help.md).

Quando você cria um DAG, um objeto vazio representando o DAG com o nome especificado e uma classe de objeto **msExchMDBAvailabilityGroup** é criada no Active Directory.

DAGs usam um subconjunto das tecnologia de cluster de failover do Windows, como a pulsação do cluster, redes de cluster e o banco de dados de cluster (para armazenar dados que mudam ou podem mudar rapidamente, como mudanças de estado de banco de dados de ativo para passivo ou vice-versa ou de montado para desmontado e vice-versa). Como os DAGs dependem do cluster de failover do Windows, eles só podem ser criados em servidores de caixa de correio do Exchange 2013 que executem o sistema operacional Windows Server 2008 R2 Enterprise ou Datacenter, sistema operacional Windows Server 2012 Standard ou Datacenter ou o sistema operacional Windows Server 2012 R2 Standard ou Datacenter.


> [!TIP]
> O cluster de failover criado e usado pelo DAG deve ser dedicado ao DAG. O cluster não pode ser usado por nenhuma outra solução de alta disponibilidade ou para qualquer outra finalidade. Por exemplo, o cluster de failover não pode ser usado para armazenar em cluster outros aplicativos ou serviços. O uso do cluster de failover subjacente do DAG para finalidades que não sejam o DAG não tem suporte.



## Servidor testemunha do DAG e diretório testemunha

Ao criar um DAG, você precisa especificar um nome para o DAG que não seja maior que 15 caracteres, exclusivo dentro da floresta do Active Directory. Além disso, cada DAG é configurado com um servidor testemunha e um diretório testemunha. O servidor testemunha e seu diretório só são usados quando houver um número par de membros no DAG, e mesmo assim apenas para fins de quorum. Você não precisa criar o diretório testemunha com antecedência. O Exchange cria e protege automaticamente o diretório para você no servidor testemunha. O diretório não deve ser usado para qualquer outro fim que não seja do servidor testemunha do DAG.

Os requisitos do servidor de testemunha são os seguintes:

  - O servidor testemunha não pode ser um membro do DAG.

  - O servidor testemunha deve estar na mesma floresta do Active Directory do DAG.

  - O servidor testemunha deve estar executando uma versão compatível do Windows Server. Para obter mais informações, consulte [Requisitos de sistema do Exchange 2013](exchange-2013-system-requirements-exchange-2013-help.md).

  - Um único servidor pode funcionar como testemunha para vários DAGs. Entretanto, cada DAG requer seu próprio diretório testemunha.

Independentemente de qual servidor é usado como o testemunha, se o firewall do Windows estiver habilitado no servidor testemunha pretendido, você deverá habilitar a exceção de firewall do Windows para compartilhamento de arquivo e impressora.


> [!IMPORTANT]
> Se o servidor testemunha que você especificar não for um servidor Exchange 2013 ou Exchange 2010, você deve adicionar o grupo de segurança universal de subsistema confiável de Exchange (USG) ao grupo Administradores local no servidor testemunha antes de criar o DAG. Essas permissões de segurança são necessárias para garantir que Exchange pode criar um diretório e compartilhar no servidor testemunha, conforme necessário.<BR>O servidor testemunha usa a porta SMB 445.



Nem o servidor testemunha nem o diretório testemunha precisa ser tolerante a falhas ou usar uma forma de redundância ou de alta disponibilidade. Não há nenhuma necessidade de usar um servidor de arquivo em cluster para o servidor testemunha ou empregar qualquer outra forma de resiliência para o servidor testemunha. Há várias razões para isso. Com DAGs maiores (por exemplo, seis membros ou mais), várias falhas são necessárias para que haja a necessidade do servidor testemunha. Como um DAG com seis membros podem tolerar até duas falhas de votante sem perder quorum, seriam necessários até três votantes com falha para que o servidor testemunha fosse exigido a fim de manter um quórum. Além disso, se houver uma falha que afete o servidor testemunha atual (por exemplo, você perde o servidor testemunha por conta de uma falha de hardware), será possível usar o cmdlet [Set-DatabaseAvailabilityGroup](https://technet.microsoft.com/pt-br/library/dd297934\(v=exchg.150\)) para configurar um novo servidor testemunha e um diretório testemunha (desde que você tenha um quórum).


> [!TIP]
> Também será possível usar o cmdlet <STRONG>Set-DatabaseAvailabilityGroup</STRONG> para configurar o servidor testemunha e o diretório testemunha no local original, se o servidor testemunha tiver perdido seu armazenamento ou se alguém tiver alterado o diretório testemunha ou as permissões de compartilhamento.



## Considerações colocação servidor testemunha

O posicionamento do servidor de testemunha do DAG um dependerá de suas necessidades de negócios e as opções disponíveis para sua organização. Exchange 2013 inclui suporte para novas opções de configuração do DAG que não são recomendados ou não é possível nas versões anteriores do Exchange. Essas opções incluem o uso de um terceiro local, como um terceiro datacenter, uma filial ou uma rede virtual do Microsoft Azure.

A tabela a seguir lista recomendações de posicionamento de servidor testemunha gerais para diferentes cenários de implantação.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Cenário de implantação</th>
<th>Recomendações</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Único DAG implantado em um único datacenter</p></td>
<td><p>Localize servidor testemunha no mesmo datacenter como membros do DAG</p></td>
</tr>
<tr class="even">
<td><p>Único DAG implantado em dois datacenters; há locais adicionais disponíveis</p></td>
<td><p>Localize servidor testemunha em uma rede virtual do Microsoft Azure para habilitar o failover automático do datacenter, ou</p>
<p>Localizar o servidor testemunha no datacenter primário</p></td>
</tr>
<tr class="odd">
<td><p>Vários DAGs implantado em um único datacenter</p></td>
<td><p>Localize servidor testemunha no mesmo datacenter como membros do DAG. As opções adicionais incluem:</p>
<ul>
<li><p>Usando o mesmo servidor testemunha para vários DAGs</p></li>
<li><p>Usando um membro do DAG para agir como um servidor de testemunha para um DAG diferente</p></li>
</ul>
<p></p></td>
</tr>
<tr class="even">
<td><p>Vários DAGs implantado em dois datacenters</p></td>
<td><p>Localize servidor testemunha em uma rede virtual do Microsoft Azure para habilitar o failover automático do datacenter, ou</p>
<p>Localizar o servidor testemunha no datacenter, que é considerada primária para cada DAG. As opções adicionais incluem:</p>
<ul>
<li><p>Usando o mesmo servidor testemunha para vários DAGs</p></li>
<li><p>Usando um membro do DAG para agir como um servidor de testemunha para um DAG diferente</p>
<p></p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>DAGs única ou múltipla implantado em mais de dois datacenters</p></td>
<td><p>Nesta configuração, o servidor testemunha deve estar localizado no datacenter onde deseja que a maioria dos votos de quorum de existir.</p></td>
</tr>
</tbody>
</table>


Quando um DAG tiver sido implantado em dois datacenters, uma nova opção de configuração no Exchange 2013 é usar um terceiro local para hospedar o servidor testemunha. Se sua organização tem um terceiro local com uma infra-estrutura de rede é isolado de falhas de rede que afetam os dois datacenters nos quais o DAG estiver implantado, você pode implantar o servidor de testemunha do DAG nesta localização terceira, assim como configurar seu DAG com a capacidade automaticamente failover bancos de dados para o datacenter outro em resposta a um evento de falha de nível de datacenter. Se sua organização tiver apenas dois locais físicos, você pode usar uma rede virtual do Microsoft Azure como um local de terceiro para colocar o servidor testemunha.

## Especificar um servidor testemunha e um diretório testemunha durante a criação do DAG

Ao criar um DAG, você deve fornecer um nome para ele. Também é possível especificar um servidor e um diretório testemunha.

Durante a criação de um DAG, as seguintes combinações de opções e comportamentos estão disponíveis:

  - É possível especificar apenas um nome para o DAG e deixar os campos **Servidor testemunha** e **Diretório testemunha** em branco. Nesse cenário, o assistente pesquisa o site Active Directory local para um servidor Acesso para Cliente que não tenha o servidor de caixas de correio instalado, e isso cria automaticamente o diretório padrão (%SystemDrive%:\\DAGFileShareWitnesses\\\<*DAGFQDN*\>) e o compartilhamento padrão (\<*DAGFQDN*\>) nesse servidor e usa esse servidor Acesso para Cliente como o servidor testemunha. Por exemplo, considere o CAS3 servidor testemunha em que o sistema operacional foi instalado na unidade C. A DAG chamado DAG1 no domínio contoso.com usaria um diretório testemunha padrão de C:\\DAGFileShareWitnesses\\DAG1.contoso.com, o que ser compartilhada como \\\\CAS3\\DAG1.contoso.com.

  - É possível especificar um nome para o DAG, o servidor testemunha que você deseja usar e o diretório que você deseja criar e compartilhar no servidor testemunha.

  - É possível especificar um nome para o DAG e o servidor testemunha que deseja usar, além de deixar o campo **Diretório testemunha** em branco. Nesse cenário, o assistente cria o diretório padrão no servidor testemunha especificado.

  - É possível especificar um nome para o DAG e deixar o campo **Servidor testemunha** em branco, além de especificar o diretório que você deseja criar e compartilhar no servidor testemunha. Nesse cenário, o assistente procura um servidor de Acesso para Cliente que não tenha o servidor de Caixa de Correio instalado e cria automaticamente o DAG especificado nesse servidor, compartilha o diretório e usa o servidor de Acesso para Cliente como o servidor testemunha.

Quando um DAG for formado, ele usará inicialmente o modelo de quórum Maioria dos Nós. Quando o segundo servidor de Caixa de Correio for adicionado ao DAG, o quorum será alterado automaticamente para um modelo de quorum Maioria dos Nós e Compartilhamentos de Arquivos. Quando essa alteração ocorrer, o cluster do DAG começará a usar o servidor testemunha para manter quorum. Se o diretório testemunha não existir, ele será automaticamente criado e compartilhado pelo Exchange, que fornecerá o compartilhamento com permissões de controle total para a conta de computador do CNO do DAG.


> [!TIP]
> Não é possível usar compartilhamento de arquivos que seja parte de um namespace do sistema de arquivos distribuído.



Se o firewall do Windows estiver habilitado no servidor testemunha antes de o DAG ser criado, ele poderá bloquear a criação do DAG. O Exchange usa a Instrumentação de Gerenciamento do Windows (WMI) para criar o diretório e o compartilhamento de arquivo no servidor testemunha. Se o firewall do Windows estiver habilitado no servidor testemunha e não houver nenhuma exceção de firewall configurada para a WMI, o cmdlet **New-DatabaseAvailabilityGroup** falhará com um erro. Caso especifique um servidor testemunha, mas não um diretório testemunha, será exibida a seguinte mensagem de erro.


<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>A tarefa não pôde criar o diretório testemunha padrão no servidor &lt;<em>Nome de Servidor</em>&gt;. Especifique um diretório testemunha manualmente.</p></td>
</tr>
</tbody>
</table>


Caso especifique um servidor testemunha e um diretório testemunha, será exibida a seguinte mensagem de erro:


<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Não é possível acessar compartilhamentos de arquivos no servidor testemunha '<em>Nome do servidor</em>'. Até o problema ser corrigido, o grupo de disponibilidade pode ficar mais vulnerável a falhas. Você pode usar o cmdlet Set-DatabaseAvailabilityGroup para tentar a operação novamente. Erro: O caminho da rede não foi encontrado.</p></td>
</tr>
</tbody>
</table>


Se o firewall do Windows estiver habilitado no servidor testemunha após a criação do DAG, mas antes de os servidores serem adicionados, ele poderá bloquear a adição ou remoção de membros do DAG. Se o firewall do Windows estiver habilitado no servidor testemunha e não houver nenhuma exceção de firewall configurada para a WMI, o cmdlet **Add-DatabaseAvailabilityGroupServer** exibirá a seguinte mensagem de aviso.


<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Falha ao criar o diretório testemunha de compartilhamento de arquivo 'C:\DAGFileShareWitnesses\DAG_FQDN' no servidor testemunha <em>'Nome do servidor'</em>. Até o problema ser corrigido, o grupo de disponibilidade pode ficar mais vunerável a falhas. Você pode usar o cmdlet Set-DatabaseAvailabilityGroup para tentar a operação novamente. Erro: Ocorreu uma exceção de WMI no servidor <em>'Nome do servidor'</em>: O servidor RPC não está disponível. (Exceção de HRESULT: 0x800706BA)</p></td>
</tr>
</tbody>
</table>


Para resolver o erro e os avisos anteriores, execute um destes procedimentos:

  - Crie manualmente o diretório testemunha e compartilhe o servidor testemunha e atribua ao CNO do DAG total controle para o diretório e o compartilhamento.

  - Habilite a exceção WMI no firewall do Windows.

  - Desabilite o firewall do Windows.

Voltar ao início

## Associação ao DAG

Depois da criação de um DAG, é possível adicionar servidores ao DAG ou removê-los do DAG, usando o assistente para Gerenciar Grupo de Disponibilidade de Banco de Dados no EAC ou usando os cmdlets **Add-DatabaseAvailabilityGroupServer** ou **Remove-DatabaseAvailabilityGroupServer** no Shell. Para instruções detalhadas sobre como gerenciar a associação ao DAG, consulte [Gerenciar a associação de grupo de disponibilidade do banco de dados](manage-database-availability-group-membership-exchange-2013-help.md).


> [!TIP]
> Cada servidor de Caixa de Correio membro de um DAG também é um nó no cluster subjacente usado pelo DAG. Dessa forma, a qualquer momento, um servidor de Caixa de Correio pode ser membro de apenas um único DAG.



Se o servidor de Caixa de Correio adicionado a um DAG não tiver o componente de cluster de failover instalado, o método usado para adicionar o servidor (por exemplo, o cmdlet **Add-DatabaseAvailabilityGroupServer** ou o assistente para Gerenciar Grupo de Disponibilidade de Banco de Dados) instalará o recurso de clustering de failover.

Quando o primeiro servidor de Caixa de Correio for adicionado a um DAG, ocorrerá o seguinte:

  - O componente de clustering de failover do Windows será instalado, se ainda não estiver.

  - Um cluster de failover é criado usando-se o nome do DAG. Esse cluster de failover é usado exclusivamente pelo DAG e deve ser dedicado ao DAG. O uso do cluster para qualquer outra finalidade não tem suporte.

  - Um CNO é criado no contêiner de computadores padrão.

  - O nome e o endereço IP do DAG é registrado como um Host (A) no DNS.

  - O servidor é adicionado ao objeto do DAG no Active Directory.

  - O banco de dados clusterizado é atualizado com informações sobre os bancos de dados montados no servidor adicionado.

Em um ambiente grande ou com vários locais, especialmente aqueles em que o DAG é estendido a vários locais de Active Directory, é preciso aguardar a replicação de Active Directory do objeto do DAG que contém o primeiro membro do DAG a ser concluído. Se esse objeto do Active Directory não for replicado em todo o ambiente, a adição do segundo servidor poderá causar a criação de um novo cluster (e novo CNO) para o DAG. Isso ocorre porque o objeto do DAG aparentará estar vazio a partir da perspectiva do segundo membro sendo adicionado, dessa forma fazendo com que o cmdlet **Add-DatabaseAvailabilityGroupServer** crie um novo cluster e CNO para o DAG, embora esses objetos já existam. Para verificar se o objeto do DAG que tem o primeiro servidor do DAG foi replicado, use o cmdlet **Get-DatabaseAvailabilityGroup** no segundo servidor sendo adicionado para verificar se o primeiro servidor adicionado está listado como membro do DAG.

Quando o segundo e os servidores subsequentes forem adicionados ao DAG, ocorrerá o seguinte:

  - O servidor é adicionado ao cluster de failover do Windows para o DAG.

  - O modelo de quorum é ajustado automaticamente:
    
      - Um modelo de quorum Maioria dos Nós é usado para DAGs com um número ímpar de membros.
    
      - Um modelo de quorum Maioria dos Nós e Compartilhamentos de Arquivos é usado para DAGs com um número par de membros.

  - O diretório testemunha e o compartilhamento são criados automaticamente pelo Exchange quando necessário.

  - O servidor é adicionado ao objeto do DAG no Active Directory.

  - O banco de dados clusterizado é atualizado com informações sobre bancos de dados montados.


> [!TIP]
> A alteração feita no modelo de quorum deve acontecer automaticamente. No entanto, se o modelo de quorum não for alterado automaticamente para o modelo apropriado, será possível executar o cmdlet <STRONG>Set-DatabaseAvailabilityGroup</STRONG> com apenas o parâmetro <EM>Identity</EM> para corrigir as configurações de quorum do DAG.



## Pré-preparo do objeto nome do cluster para um DAG

O CNO é uma conta de computador criada no Active Directory e associada ao recurso de nome do cluster. Esse recurso está vinculado ao CNO, que é um objeto habilitado para Kerberos que atua como a identidade do cluster e fornece o contexto de segurança do cluster. A formação do cluster subjacente do DAG e do CNO para esse cluster é feita quando o primeiro membro é adicionado ao DAG. Quando o primeiro servidor for adicionado ao DAG, o Powershell remoto entra em contato com o Serviço de Replicação do Microsoft Exchange no servidor de Caixa de Correio sendo adicionado. O serviço de Replicação do Microsoft Exchange instala o recurso cluster de failover (se ele ainda não estiver instalado) e inicia o processo de criação do cluster. O Serviço de Replicação do Microsoft Exchange é executado no contexto de segurança de LOCAL SYSTEM e está sob esse contexto em que a criação do cluster é feita.


> [!WARNING]
> Caso os membros do DAG estejam executando o Windows Server 2012, você deverá preparar o CNO antes de adicionar o primeiro servidor ao DAG. Se os seus membros do DAG estiverem executando o Windows Server 2012 R2 e você criar um DAG sem um ponto de acesso administrativo de cluster, não será criado um CNO e você não precisará criar um CNO para o DAG.



Nos ambientes em que a criação de conta de computador é restrita ou as contas de computador são criadas em um contêiner que não seja o de computadores padrão, você pode preparar e fornecer o CNO. Crie e desabilite uma conta de computador para o CNO e:

  - Atribua controle total da conta do computador à conta do computador do primeiro servidor de Caixa de Correio sendo adicionado ao DAG.

  - Atribua controle total da conta do computador ao USG do Subsistema Confiável do Exchange.

Atribuir controle total da conta do computador à conta do computador do primeiro servidor de Caixa de Correio sendo adicionado ao DAG assegura que o contexto de segurança de LOCAL SYSTEM possa gerenciar a conta de computador preparada. A atribuição de controle total da conta de computador ao USG do Subsistema Confiável do Exchange pode ser usada porque o USG do Subsistema Confiável do Exchange tem as contas de máquina de todos os servidores Exchange do domínio.

Para obter as etapas detalhadas sobre como preparar e fornecer o CNO de um DAG, consulte [Preparar o objeto de nome de cluster de um grupo de disponibilidade do banco de dados](pre-stage-the-cluster-name-object-for-a-database-availability-group-exchange-2013-help.md).

## Remover servidores de um DAG

Os servidores de caixa de correio podem ser removidos de um DAG usando-se o assistente para Gerenciar Grupo de Disponibilidade de Banco de Dados no EAC ou o cmdlet **Remove-DatabaseAvailabilityGroupServer** no Shell. Para que um servidor de Caixa de Correio possa ser removido de um DAG, todos os bancos de dados de caixa de correio replicados devem ser primeiramente removidos do servidor. Se você tentar remover um servidor de Caixa de Correio com bancos de dados de caixa de correio de um DAG, haverá falha na tarefa.

Há cenários nos quais você deve remover um servidor de Caixa de Correio de um DAG antes de realizar determinadas operações. Esses cenários incluem:

  - **Realizar uma operação de recuperação de servidor**   Se um servidor de Caixa de Correio membro de um DAG for perdido ou houver uma falha e ele não puder ser recuperado e precisar de substituição, será possível realizar uma operação de recuperação de servidor usando a opção **Setup /m:RecoverServer**. No entanto, antes de conseguir realizar a operação de recuperação, você deve primeiro remover o servidor do DAG usando o cmdlet [Remove-DatabaseAvailabilityGroupServer](https://technet.microsoft.com/pt-br/library/dd297956\(v=exchg.150\)) com o parâmetro *ConfigurationOnly*.

  - **Remover o grupo de disponibilidade do banco de dados**   Talvez haja situações nas quais você precise remover um DAG (por exemplo, ao desabilitar o modo de replicação de terceiros). Se precisar remover um DAG, você deverá remover primeiro todos os servidores do DAG. Se você tentar remover um DAG que contenha algum membro, haverá falha na tarefa.

Voltar ao início

## Configurar propriedades do DAG

Depois que os servidores forem adicionados ao DAG, será possível usar o EAC ou o Shell para configurar as propriedades de um DAG, inclusive o servidor testemunha e o diretório testemunha usados pelo DAG, além dos endereços IP atribuídos ao DAG.

As propriedades configuráveis incluem:

  - **Servidor testemunha**   O nome do servidor em que você deseja hospedar o compartilhamento de arquivos para a testemunha de compartilhamento de arquivos. Recomendamos que você especifique um servidor de Acesso para Cliente como o servidor testemunha. Isso permite que o sistema configure, proteja e use automaticamente o compartilhamento conforme necessário, e que o administrador de mensagens saiba da disponibilidade do servidor testemunha.

  - **Diretório testemunha**   O nome de um diretório que será usado para armazenar dados de testemunha de compartilhamento de arquivos. Esse diretório será criado automaticamente pelo sistema no servidor testemunha especificado.

  - **Endereços IP do Grupo de Disponibilidade do Banco de Dados**   Devem ser atribuídos ao DAG um ou mais endereços IP, a não ser que os membros do DAG estejam executando o Windows Server 2012 R2 e você esteja criando um DAG sem endereço IP. Caso contrário, os endereços IP do DAG podem ser configurados com endereços IP estáticos atribuídos manualmente ou podem ser atribuídos automaticamente ao DAG com um servidor DHCP na organização.

O Shell permite configurar as propriedades do DAG que não estão disponíveis no EAC, como os endereços IP do DAG, a criptografia de rede e as configurações de compactação, a descoberta de rede, a porta TCP usada para replicação e o servidor testemunha alternativo e as configurações do diretório testemunha, além de habilitar o modo de Coordenação de Ativação do Data Center.

Para obter etapas detalhadas sobre como configurar as propriedades do DAG, consulte [Configurar as propriedades do grupo de disponibilidade do banco de dados](configure-database-availability-group-properties-exchange-2013-help.md).

## Criptografia de rede do DAG

DAGs suporte ao uso de criptografia, aproveitando os recursos de criptografia do sistema operacional Windows Server. DAGs usam a autenticação Kerberos entre servidores Exchange. Microsoft Kerberos segurança suporte provider (SSP) EncryptMessage e APIs de DecryptMessage alça de criptografia de tráfego de rede do DAG. SSP do Kerberos Microsoft oferece suporte a vários algoritmos de criptografia. (Para uma lista completa, consulte a seção 3.1.5.2, "Tipos de criptografia" de [Extensões do protocolo Kerberos](https://go.microsoft.com/fwlink/p/?linkid=179131)). O handshake de autenticação Kerberos seleciona o protocolo de criptografia mais forte com suporte na lista: normalmente avançadas criptografia AES (padrão) 256 bits, potencialmente com um Hash SHA-based mensagem Authentication Code (HMAC) para manter a integridade do dados. Para obter detalhes, consulte [HMAC](https://en.wikipedia.org/wiki/hmac).

A criptografia de rede é uma propriedade do DAG e não de uma rede do DAG. É possível configurar a criptografia de rede do DAG usando o cmdlet **Set-DatabaseAvailabilityGroup** no Shell. As configurações de criptografia possíveis para a comunicação de rede do DAG são mostradas na tabela a seguir.

### Configurações de criptografia da comunicação de rede do DAG

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Configuração</th>
<th>Descrição</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Desabilitado</p></td>
<td><p>A criptografia de rede não é usada.</p></td>
</tr>
<tr class="even">
<td><p>Habilitado</p></td>
<td><p>A criptografia de rede é usada em todas as redes do DAG para replicação e propagação.</p></td>
</tr>
<tr class="odd">
<td><p>InterSubnetOnly</p></td>
<td><p>A criptografia de rede é usada em redes do DAG durante a replicação em sub-redes diferentes. Esta é a configuração padrão.</p></td>
</tr>
<tr class="even">
<td><p>SeedOnly</p></td>
<td><p>A criptografia de rede é usada em todas as redes do DAG apenas para propagação.</p></td>
</tr>
</tbody>
</table>


## Compactação de rede do DAG

DAGs suportam a compactação interna. Quando a compactação estiver ativada, comunicação de rede de DAG usa XPRESS, que é a implementação da Microsoft do algoritmo LZ77. Para obter detalhes, consulte seção 3.1.4.11.1.2.1 e [Uma explicação do algoritmo Deflate](http://www.zlib.net/feldspar.html) "Algoritmo de compactação LZ77" da [Especificação do protocolo de formato de transmissão](https://go.microsoft.com/fwlink/p/?linkid=179133). Este é o mesmo tipo de compactação usada em vários protocolos da Microsoft, em particular, compactação de MAPI RPC entre Microsoft Outlook e Exchange.

Assim como acontece com a criptografia de rede, a compactação de rede também é uma propriedade do DAG, e não de uma rede do DAG. Você configura a compactação de rede do DAG usando o cmdlet [Set-DatabaseAvailabilityGroup](https://technet.microsoft.com/pt-br/library/dd297934\(v=exchg.150\)) no Shell. As configurações de compactação possíveis para a comunicação de rede do DAG são mostradas na tabela a seguir.

### Configurações de compactação da comunicação de rede do DAG

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Configuração</th>
<th>Descrição</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Desabilitado</p></td>
<td><p>A compactação de rede não é usada.</p></td>
</tr>
<tr class="even">
<td><p>Enabled</p></td>
<td><p>A compactação de rede é usada em todas as redes do DAG para replicação e propagação.</p></td>
</tr>
<tr class="odd">
<td><p>InterSubnetOnly</p></td>
<td><p>A compactação de rede é usada em redes do DAG durante a replicação em sub-redes diferentes. Esta é a configuração padrão.</p></td>
</tr>
<tr class="even">
<td><p>SeedOnly</p></td>
<td><p>A compactação de rede é usada em todas as redes do DAG apenas para propagação.</p></td>
</tr>
</tbody>
</table>


Voltar ao início

## Redes do DAG

Uma rede de DAG é uma coleção de uma ou mais sub-redes usado para tráfego de replicação ou o tráfego MAPI. Cada DAG contém um máximo de uma rede MAPI e zero ou mais redes de replicação.

## Configurações do adaptador de rede único

Nas configurações do adaptador de rede único, a mesma rede é usada para tráfego de replicação e de MAPI. Para reduzir a complexidade, um único adaptador de rede é a configuração recomendada para servidores de Exchange, isso significa que Okey ter o tráfego de replicação e MAPI na mesma rede.

## Configurações do adaptador de rede dual

Normalmente, você só precisará usar o adaptadores de rede dual onde o tráfego de rede maior tem o potencial saturem um único adaptador de rede.

Em configurações do adaptador de rede dual, uma rede geralmente é dedicada para o tráfego de replicação e a outra rede é usada principalmente para tráfego MAPI. Você também pode adicionar adaptadores de rede para cada membro DAG e configurar redes do DAG adicionais como redes de replicação.


> [!TIP]
> Ao usar várias redes de replicação, não há qualquer maneira de especificar uma ordem de precedência para o uso das redes. O Exchange seleciona aleatoriamente uma rede de replicação, no grupo de redes de replicação, para usá-la para envio de logs.



No Exchange 2010, a configuração manual de redes DAG era necessária em muitos casos. Por padrão no Exchange 2013, as redes DAG são configuradas automaticamente pelo sistema. Antes de criar ou modificar redes DAG, você deve primeiro habilitar o controle manual de redes DAG executando este comando:

    Set-DatabaseAvailabilityGroup <DAGName> -ManualDagNetworkConfiguration $true

Depois de habilitar a configuração manual de redes DAG, você poderá usar o cmdlet **New-DatabaseAvailabilityGroupNetwork** no Shell para criar uma rede do DAG. Para instruções detalhadas sobre como criar uma rede DAG, consulte [Criar uma rede de grupo de disponibilidade do banco de dados](create-a-database-availability-group-network-exchange-2013-help.md).

É possível usar o cmdlet **Set-DatabaseAvailabilityGroupNetwork** no Shell para configurar as propriedades de redes DAG. Para obter etapas detalhadas sobre como configurar as propriedades de rede do DAG, consulte [Configurar propriedades de rede do grupo de disponibilidade de banco de dados](configure-database-availability-group-network-properties-exchange-2013-help.md). Cada rede do DAG exigiu parâmetros opcionais a serem configurados:

  - **Nome da rede**   Um nome exclusivo para a rede do DAG, com até 128 caracteres.

  - **Descrição da rede**   Uma descrição opcional para a rede do DAG, com até 256 caracteres.

  - **Sub-redes da rede**   Uma ou mais sub-redes inseridas usando-se um formato de *IPAddress/Bitmask* (por exemplo, 192.168.1.0/24 para sub-redes IPv4; 2001:DB8:0:C000::/64 para sub-redes IPv6).

  - **Habilitar replicação**   No EAC, marque a caixa de seleção para dedicar a rede do DAG ao tráfego de replicação e bloquear o tráfego MAPI. Desmarque a caixa de seleção para evitar a replicação do uso da rede do DAG e habilitar o tráfego MAPI. No Shell, use o parâmetro *ReplicationEnabled* no cmdlet [Set-DatabaseAvailabilityGroupNetwork](https://technet.microsoft.com/pt-br/library/dd298008\(v=exchg.150\)) para habilitar e desabilitar a replicação.


> [!TIP]
> Desabilitar a replicação na rede MAPI não garante que o sistema não usará essa rede na replicação. Quando todas as redes de replicação configuradas estiverem offline, tiverem falhado ou estiverem indisponíveis de qualquer outra forma e somente a rede MAPI continuar ativa (o que é configurado como desabilitado para replicação), o sistema usará a rede MAPI para replicação.



As redes DAG iniciais (por exemplo, MapiDagNetwork e ReplicationDagNetwork01) criadas pelo sistema têm como base as sub-redes enumeradas pelo serviço de Cluster. Cada membro do DAG deve ter o mesmo número de adaptadores de rede, e cada adaptador de rede deve ter um endereço IPv4 (e opcionalmente, um endereço IPv6 também) em uma sub-rede exclusiva. Vários membros do DAG podem ter endereços IPv4 na mesma sub-rede, mas cada adaptador de rede e par de endereço IP em um membro do DAG específico deve estar em uma sub-rede exclusiva. Além disso, somente o adaptador usado para a rede MAPI deve ser configurado com um gateway padrão. As redes de replicação não devem ser configuradas com um gateway padrão.

Por exemplo, considere o DAG1, um DAG de dois membros em que cada membro tem dois adaptadores de rede (um dedicado para a rede MAPI e outro para uma rede de replicação). As configurações de definição de endereço IP de exemplo são mostradas na tabela a seguir.

### Exemplo de configurações do adaptador de rede

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Adaptador de servidor-rede</th>
<th>Endereço IP/máscara de sub-rede</th>
<th>Gateway padrão</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>EX1-MAPI</p></td>
<td><p>192.168.1.15/24</p></td>
<td><p>192.168.1.1</p></td>
</tr>
<tr class="even">
<td><p>EX1-Replicação</p></td>
<td><p>10.0.0.15/24</p></td>
<td><p>Não aplicável</p></td>
</tr>
<tr class="odd">
<td><p>EX2-MAPI</p></td>
<td><p>192.168.1.16</p></td>
<td><p>192.168.1.1</p></td>
</tr>
<tr class="even">
<td><p>EX2-Replicação</p></td>
<td><p>10.0.0.16</p></td>
<td><p>Não se aplica</p></td>
</tr>
</tbody>
</table>


Na configuração a seguir, há duas sub-redes configuradas no DAG: 192.168.1.0 e 10.0.0.0. Quando EX1 e EX2 são adicionados ao DAG, duas sub-redes serão enumeradas e duas redes de DAG serão criadas: MapiDagNetwork (192.168.1.0) e ReplicationDagNetwork01 (10.0.0.0). Essas redes serão configuradas como mostrado na tabela a seguir.

### Configurações de rede de DAG enumeradas para um DAG de sub-rede única

<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>Nome</th>
<th>Sub-redes</th>
<th>Interfaces</th>
<th>Acesso MAPI habilitado</th>
<th>Replicação habilitada</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>MapiDagNetwork</p></td>
<td><p>192.168.1.0/24</p></td>
<td><p>EX1 (192.168.1.15)</p>
<p>EX2 (192.168.1.16)</p></td>
<td><p>Verdadeiro</p></td>
<td><p>Verdadeiro</p></td>
</tr>
<tr class="even">
<td><p>ReplicationDagNetwork01</p></td>
<td><p>10.0.0.0/24</p></td>
<td><p>EX1 (10.0.0.15)</p>
<p>EX2 (10.0.0.16)</p></td>
<td><p>Falso</p></td>
<td><p>Verdadeiro</p></td>
</tr>
</tbody>
</table>


Para concluir a configuração do ReplicationDagNetwork01 como a rede de replicação dedicada, desabilite a replicação para MapiDagNetwork executando o seguinte comando.

    Set-DatabaseAvailabilityGroupNetwork -Identity DAG1\MapiDagNetwork -ReplicationEnabled:$false

Depois que a replicação é desabilitada para MapiDagNetwork, o serviço de replicação do Microsoft Exchange usa ReplicationDagNetwork01 para replicação contínua. Se ReplicationDagNetwork01 falhar, o serviço de replicação do Microsoft Exchange volta a usar MapiDagNetwork para replicação contínua. Isso é feito intencionalmente pelo sistema para manter alta disponibilidade.

## Redes DAG e várias implantações de sub-rede

No exemplo anterior, embora existam duas sub-redes diferentes em uso pelo DAG (192.168.1.0 e 10.0.0.0), o DAG é considerado uma sub-rede única porque cada membro usa a mesma sub-rede para formar a redes MAPI. Quando os membros do DAG usam sub-redes diferentes para a rede MAPI, o DAG é mencionado como um *DAG com várias sub-redes*. Em um DAG com várias sub-redes, as sub-redes adequadas são associadas automaticamente a cada rede DAG.

Por exemplo, considere o DAG2, um DAG de dois membros em que cada membro tem dois adaptadores de rede (um dedicado para a rede MAPI e outro para uma rede de replicação), e cada membro do DAG está localizado em um site do Active Directory separado, com sua rede MAPI em uma sub-rede diferente. As configurações de definição de endereço IP de exemplo são mostradas na tabela a seguir.

### Exemplo de configurações de adaptador de rede para um DAG com várias sub-redes

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Adaptador de servidor-rede</th>
<th>Endereço IP/máscara de sub-rede</th>
<th>Gateway padrão</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>EX1-MAPI</p></td>
<td><p>192.168.0.15/24</p></td>
<td><p>192.168.0.1</p></td>
</tr>
<tr class="even">
<td><p>EX1-Replicação</p></td>
<td><p>10.0.0.15/24</p></td>
<td><p>Não aplicável</p></td>
</tr>
<tr class="odd">
<td><p>EX2-MAPI</p></td>
<td><p>192.168.1.15</p></td>
<td><p>192.168.1.1</p></td>
</tr>
<tr class="even">
<td><p>EX2-Replicação</p></td>
<td><p>10.0.1.15</p></td>
<td><p>Não se aplica</p></td>
</tr>
</tbody>
</table>


Na configuração a seguir, há quatro sub-redes configuradas no DAG: 192.168.0.0, 192.168.1.0, 10.0.0.0 e 10.0.1.0. Quando EX1 e EX2 são adicionados ao DAG, quatro sub-redes serão enumeradas, mas apenas duas redes DAG serão criadas: MapiDagNetwork (192.168.0.0, 192.168.1.0) e ReplicationDagNetwork01 (10.0.0.0, 10.0.1.0). Essas redes serão configuradas como mostrado na tabela a seguir.

### Configurações de rede de DAG enumeradas para um DAG de várias sub-redes

<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>Nome</th>
<th>Sub-redes</th>
<th>Interfaces</th>
<th>Acesso MAPI habilitado</th>
<th>Replicação habilitada</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>MapiDagNetwork</p></td>
<td><p>192.168.0.0/24</p>
<p>192.168.1.0/24</p></td>
<td><p>EX1 (192.168.0.15)</p>
<p>EX2 (192.168.1.15)</p></td>
<td><p>Verdadeiro</p></td>
<td><p>Verdadeiro</p></td>
</tr>
<tr class="even">
<td><p>ReplicationDagNetwork01</p></td>
<td><p>10.0.0.0/24</p>
<p>10.0.1.0/24</p></td>
<td><p>EX1 (10.0.0.15)</p>
<p>EX2 (10.0.1.15)</p></td>
<td><p>Falso</p></td>
<td><p>Verdadeiro</p></td>
</tr>
</tbody>
</table>


## Redes DAG e redes iSCSI

Por padrão, os DAGs realizam a descoberta de todas as redes detectadas e configuradas para uso pelo cluster subjacente. Isso inclui todas as redes iSCSI (Internet SCSI) em uso como resultado do uso do armazenamento iSCSI para um ou mais membros do DAG. Como prática recomendada, o armazenamento iSCSI deve usar redes dedicadas e adaptadores de rede. Essas redes não devem ser gerenciadas pelo DAG ou pelo cluster, ou usadas como redes DAG (MAPI ou replicação). Em vez disso, essas redes devem ser desabilitadas manualmente do uso pelo DAG, para que possam ser dedicadas ao tráfego de armazenamento iSCSI. Para impedir que redes iSCSI sejam detectadas e usadas como redes DAG, configure o DAG para ignorar quaisquer redes iSCSI detectadas no momento usando o cmdlet [Set-DatabaseAvailabilityGroupNetwork](https://technet.microsoft.com/pt-br/library/dd298008\(v=exchg.150\)), como neste exemplo:

    Set-DatabaseAvailabilityGroupNetwork -Identity DAG2\DAGNetwork02 -ReplicationEnabled:$false -IgnoreNetwork:$true

Este comando também irá desativar a rede para uso pelo cluster. Embora as redes iSCSI continuem aparecendo como redes do DAG, elas não serão usadas para MAPI ou tráfego de replicação após a execução do comando acima.

Voltar ao início

## Configurar membros do DAG

Os servidores de caixa de correio que são membros de um DAG têm algumas propriedades específicas de alta disponibilidade que devem ser configuradas como descrito nas seguintes seções:

  - Automatic database mount dial

  - Database copy automatic activation policy

  - Maximum active databases

## Discagem de montagem automática de banco de dados

O parâmetro *AutoDatabaseMountDial* especifica o comportamento de montagem de banco de dados automático após o failover de um banco de dados. É possível usar o cmdlet [Set-MailboxServer](https://technet.microsoft.com/pt-br/library/aa998651\(v=exchg.150\)) para configurar o parâmetro *AutoDatabaseMountDial* com qualquer um dos seguintes valores:

  - `BestAvailability`   Se você especificar esse valor, o banco de dados será montado automaticamente depois de um failover se o tamanho da fila de cópia for menor que ou igual a 12. O tamanho da fila de cópia é o número de logs reconhecidos pela cópia passiva que precisa ser replicada. Se o tamanho da fila de cópia for maior que 12, o banco de dados não será montado automaticamente. Quando o tamanho da fila de cópia é inferior ou igual a 12, o Exchange tenta replicar os logs restantes para a cópia passiva e monta o banco de dados.

  - `GoodAvailability`   Se você especificar esse valor, o banco de dados será montado automaticamente logo depois de um failover se o tamanho da fila de cópia for menor que ou igual a seis. O tamanho da fila de cópia é o número de logs reconhecidos pela cópia passiva que precisa ser replicada. Se o tamanho da fila de cópia for maior que seis, o banco de dados não será montado automaticamente. Quando o tamanho da fila de cópia é inferior ou igual a seis, o Exchange tenta replicar os logs restantes para a cópia passiva e monta o banco de dados.

  - `Lossless`   Se você especificar esse valor, o banco de dados não será montado automaticamente até que todos os logs que foram gerados na cópia ativa tenham sido copiados para a cópia passiva. Essa configuração faz também com que o Gerenciador Ativo selecione a melhor cópia de algoritmo para classificar candidatos potenciais para ativação com base no valor de preferência de ativação da cópia de banco de dados e não na extensão da fila de cópia.

O valor padrão é `GoodAvailability`. Se você especificar `BestAvailability` ou `GoodAvailability` e nenhum log da cópia ativa puder ser replicado para a cópia passiva sendo ativada, você poderá perder alguns dados da caixa de correio. No entanto, o recurso de Rede Segura (que é habilitado por padrão) ajuda a proteger contra a perda da maior parte dos dados, reenviando as mensagens que estão na fila de Rede Segura.

## Exemplo: configurar discagem de montagem automática de banco de dados

O exemplo a seguir configura um servidor de Caixa de Correio com uma configuração *AutoDatabaseMountDial* de `GoodAvailability`.

    Set-MailboxServer -Identity EX1 -AutoDatabaseMountDial GoodAvailability

## Política de ativação automática de cópia do banco de dados

O parâmetro *DatabaseCopyAutoActivationPolicy* especifica o tipo de ativação automática disponível para cópias de banco de dados da caixa de correio nos servidores Caixa de Correio selecionados. É possível usar o cmdlet [Set-MailboxServer](https://technet.microsoft.com/pt-br/library/aa998651\(v=exchg.150\)) para configurar o parâmetro *DatabaseCopyAutoActivationPolicy* com qualquer um dos seguintes valores:

  - `Blocked`   Se você especificar esse valor, os bancos de dados não poderão ser ativados automaticamente nos servidores de Caixa de Correio selecionados.

  - `IntrasiteOnly`   Se você especificar esse valor, a cópia de banco de dados poderá ser ativada nos servidores no mesmo site do Active Directory. Isso impede o failover ou a ativação entre sites. Essa propriedade se destina a cópias de banco de dados de caixa de correio (por exemplo, uma cópia passiva transformada em uma cópia ativa). Os bancos de dados não podem ser ativados nesse servidor de Caixa de Correio para cópias de banco de dados ativos em outro site do Active Directory.

  - `Unrestricted`   Se você especificar esse valor, não haverá nenhuma restrição especial na ativação de cópias de banco de dados de caixa de correio nos servidores de Caixa de Correio.

## Exemplo: configurar política de ativação automática de cópia do banco de dados

O exemplo a seguir configura um servidor de Caixa de Correio com uma configuração *DatabaseCopyAutoActivationPolicy* de `Blocked`.

    Set-MailboxServer -Identity EX1 -DatabaseCopyAutoActivationPolicy Blocked

## Máximo de bancos de dados ativos

O parâmetro *MaximumActiveDatabases* (também usado com o cmdlet [Set-MailboxServer](https://technet.microsoft.com/pt-br/library/aa998651\(v=exchg.150\))) especifica o número de bancos de dados que pode ser montado em um servidor de Caixa de Correio. Você pode configurar servidores de Caixa de Correio para atender aos seus requisitos de implantação assegurando que um servidor de Caixa de Correio individual não fique sobrecarregado.

O parâmetro *MaximumActiveDatabases* é configurado com um valor numérico de número inteiro. Quando o número máximo for atingido, as cópias de banco de dados no servidor não poderão ser ativadas se houver failover ou alternância. Se as cópias já estiverem ativas em um servidor, ele não permitirá a montagem de bancos de dados.

## Exemplo: configurar máximo de bancos de dados ativos

O exemplo a seguir configura um servidor de Caixa de Correio para suporte a um máximo de 20 bancos de dados ativos.

    Set-MailboxServer -Identity EX1 -MaximumActiveDatabases 20

Voltar ao início

## Executar a manutenção em membros do DAG

Antes de realizar qualquer tipo de manutenção de software ou hardware em um membro do DAG, você deve primeiro colocar o membro do DAG em modo de manutenção. Isso envolve a transferência de todos os bancos de dados ativos fora do servidor e bloqueando bancos de dados ativos de se mudar para o servidor. Ele também garante que todas as funcionalidades de apoio DAG crítico que pode estar no servidor (por exemplo, o papel do Gerente de atividade primária (PAM)) é movido para outro servidor e impedido de mudar de volta para o servidor. Especificamente, você deve realizar as seguintes tarefas:

1.  Para iniciar o processo de drenagem filas dos transportes, executado `Set-ServerComponentState <ServerName> -Component HubTransport -State Draining -Requester Maintenance`

2.  Para iniciar a drenagem das filas dos transportes, execute `Restart-Service MSExchangeTransport`

3.  Para iniciar o processo de drenagem de todas as chamadas de Unificação de Mensagens, execute `Set-ServerComponentState <ServerName> -Component UMCallRouter -State Draining -Requester Maintenance`

4.  Para redirecionar mensagens pendentes de entrega nas filas locais para o servidor de caixa de correio especificado pelo parâmetro de destino, execute `Redirect-Message -Server <ServerName> -Target <MailboxServerFQDN>`

5.  Para fazer uma pausa no nó do cluster, o que impede o nó de ser e tornar-se o PAM, execute `Suspend-ClusterNode <ServerName>`

6.  Para mover todos os bancos de dados ativos atualmente hospedados no membro DAG para os outros membros do DAG, execute `Set-MailboxServer <ServerName> -DatabaseCopyActivationDisabledAndMoveNow $True`

7.  Para evitar que o servidor de hospedagem de cópias do banco de dados ativos, execute `Set-MailboxServer <ServerName> -DatabaseCopyAutoActivationPolicy Blocked`

8.  Para colocar o servidor no modo de manutenção, execute `Set-ServerComponentState <ServerName> -Component ServerWideOffline -State Inactive -Requester Maintenance`

Para verificar se um servidor está pronto para manutenção, realizar as seguintes tarefas:

1.  Para verificar se o servidor foi colocado no modo de manutenção, execute `Get-ServerComponentState <ServerName> | ft Component,State -Autosize`

2.  Para verificar se o servidor não está hospedando qualquer cópia do banco de dados ativos, execute `Get-MailboxServer <ServerName> | ft DatabaseCopy* -Autosize`

3.  Para verificar se o nó está em pausa, execute `Get-ClusterNode <ServerName> | fl`

4.  Para verificar se todas as filas de transporte foram drenados, execute `Get-Queue`

Após a manutenção estiver completa eo membro DAG está pronto para voltar ao serviço, você pode levar o membro do DAG do modo de manutenção e colocá-lo de volta à produção, executando as seguintes tarefas:

  - Para designar que o servidor está fora do modo de manutenção, execute `Set-ServerComponentState <ServerName> -Component ServerWideOffline -State Active -Requester Maintenance`

  - Para permitir que o servidor para aceitar chamadas de Unificação de Mensagens, execute `Set-ServerComponentState <ServerName> -Component UMCallRouter -State Active -Requester Maintenance`

  - Para retomar o nó do cluster e permitir a funcionalidade do cluster completo para o servidor, execute `Resume-ClusterNode <ServerName>`

  - Para permitir que os bancos de dados para tornar-se ativo no servidor, execute `Set-MailboxServer <ServerName> -DatabaseCopyActivationDisabledAndMoveNow $False`

  - Para remover os blocos de ativação automática, execute `Set-MailboxServer <ServerName> -DatabaseCopyAutoActivationPolicy Unrestricted`

  - Para habilitar as filas dos transportes e permitir que o servidor aceite e processe mensagens, execute `Set-ServerComponentState <ServerName> -Component HubTransport -State Active -Requester Maintenance`

  - Para retomar a atividade de transporte, execute `Restart-Service MSExchangeTransport`

Para verificar se um servidor está pronto para o uso na produção, execute as seguintes tarefas:

1.  Verifique se o servidor não está no modo de manutenção, executando `Get-ServerComponentState <ServerName> | ft Component,State -Autosize`

Se você estiver instalando uma atualização do Exchange e processo falhar, alguns componentes do servidor poderão ficar em estado inativo, como será mostrado no relatório do cmdlet Get-ServerComponentState acima. Para solucionar isso, execute os seguintes comandos:

  - `Set-ServerComponentState <ServerName> -Component ServerWideOffline -State Active -Requester Functional`

  - `Set-ServerComponentState <ServerName> -Component Monitoring -State Active -Requester Functional`

  - `Set-ServerComponentState <ServerName> -Component RecoveryActionsEnabled -State Active -Requester Functional`

Voltar ao início

## Desativar os membros do DAG

A solução de alta disponibilidade do Exchange 2013 é integrada ao processo de desligamento do Windows. Se um administrador ou aplicativo iniciar um desligamento de um servidor do Windows em um DAG com um banco de dados montado replicado para um ou mais membros do DAG, o sistema tentará ativar outra cópia do banco de dados montado, antes de permitir a conclusão do processo de desligamento.

No entanto, esse novo comportamento não assegura que todos os bancos de dados no servidor desligados enfrentarão uma ativação `lossless`. Dessa forma, é uma prática recomendável realizar uma alternância de servidor antes de desligar um servidor membro de um DAG.

Voltar ao início

## Instalar atualizações sobre membros do DAG

Instalando o Microsoft Exchange Server 2013 atualizações em um servidor que é membro de um DAG é um processo relativamente simples. Quando você instalar uma atualização em um servidor que é membro de um DAG, vários serviços são interrompidos durante a instalação, incluindo todos os Exchange serviços eo serviço de cluster. O processo geral para a aplicação de alterações de um membro do DAG é como se segue:

1.  Use as etapas descritas acima para colocar o membro do DAG em modo de manutenção.

2.  Instale a atualização.

3.  Use os passos descritos acima para dar o membro do DAG do modo de manutenção e colocá-lo novamente em produção.

4.  Opcionalmente, use o script RedistributeActiveDatabases.ps1 para reequilibrar as cópias do banco de dados ativos em todo o DAG.

Você pode baixar a atualização mais recente para o Exchange 2013 do [Microsoft Download Center](http://www.microsoft.com/downloads) .

Voltar ao início

