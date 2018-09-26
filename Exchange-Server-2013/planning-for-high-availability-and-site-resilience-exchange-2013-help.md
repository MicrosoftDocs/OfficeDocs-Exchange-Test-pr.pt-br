---
title: 'Planejamento de alta disponibilidade e resiliência de site: Exchange 2013 Help'
TOCTitle: Planejamento de alta disponibilidade e de resiliência do site
ms:assetid: 29bb0358-fc8e-4437-8feb-d2959ed0f102
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Dd638104(v=EXCHG.150)
ms:contentKeyID: 50485221
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Planejamento de alta disponibilidade e de resiliência do site

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2016-12-09_

Durante a fase de planejamento, os arquitetos de sistema, os administradores e os outros participantes principais devem identificar os requisitos de negócios e de arquitetura da implantação, em especial os requisitos de alta disponibilidade e de resiliência do site.

Existem requisitos gerais que devem ser atendidos para a implantação desses recursos, bem como requisitos de hardware, software e rede que também devem ser atendidos.

**Sumário**

General requirements

Hardware requirements

Storage requirements

Software requirements

Network requirements

Witness server requirements

Planning for site resilience

## Requisitos gerais

Antes de implantar um grupo de disponibilidade de banco de dados (DAG)e criar cópias de banco de dados de caixa de correio, certifique-se de que as recomendações de sistema a seguir foram atendidas:

  - O DNS (Sistema de Nomes de Domínio) deve estar em execução. O ideal é que o servidor DNS aceite atualizações dinâmicas. Se o servidor DNS não aceitar atualizações dinâmicas, você deverá criar um registro de host DNS (A) para cada servidor do Exchange. Caso contrário, o Exchange não funcionará corretamente.

  - Cada servidor de caixa de correio em um DAG deve ser um servidor membro no mesmo domínio.

  - Não há suporte para a adição de um servidor de Caixa de Correio do Exchange 2013 que também seja um servidor de diretório para um DAG.

  - O nome atribuído ao DAG deve ser um nome de computador válido, disponível e exclusivo com 15 caracteres ou menos.

Voltar ao início

## Requisitos de hardware

Em geral, não há nenhum requisito de hardware especial que seja específico de DAGs ou cópias de banco de dados de caixa de correio. Os servidores usados devem atender a todos os requisitos determinados nos tópicos para o [Pré-requisitos do Exchange 2013](exchange-2013-prerequisites-exchange-2013-help.md) e o [Requisitos de sistema do Exchange 2013](exchange-2013-system-requirements-exchange-2013-help.md).

Voltar ao início

## Requisitos de armazenamento

Em geral, não há nenhum requisito de armazenamento especial que seja específico de DAGs ou cópias de banco de dados de caixa de correio. Os DAGs não solicitam ou usam armazenamento compartilhado gerenciado por cluster. O armazenamento compartilhado gerenciado por cluster tem suporte para uso em um DAG somente quando o DAG é configurado para usar uma solução que aproveita a API de Replicação de Terceiros integrada ao Exchange 2013.

Voltar ao início

## Requisitos de software

OS DAGs estão disponíveis no Exchange 2013 Standard e no Exchange 2013 Enterprise. Além disso, um DAG pode conter uma combinação de servidores com o Exchange 2013 Standard e o Exchange 2013 Enterprise.

Cada membro do DAG também deve ter o mesmo sistema operacional em execução. O Exchange 2013 é suportado nos sistemas operacionais Windows Server 2008 R2, Windows Server 2012 e Windows Server 2012 R2. Todos os membros de um determinado DAG devem executar o mesmo sistema operacional. O Windows Server 2012 R2 só tem suporte para membros do DAG que executem o Service Pack 1 ou posterior do Exchange 2013.

Além de atender aos pré-requisitos de instalação do Exchange 2013, existem requisitos do sistema operacional que devem ser atendidos. Os DAGs usam a tecnologia de Cluster de Failover do Windows e, como resultado, eles exigem a versão Enterprise ou Datacenter do Windows Server 2008 R2 ou a versão Standard ou Datacenter dos sistemas operacionais Windows Server 2012 ou Windows Server 2012 R2.

Voltar ao início

## Requisitos de rede

Existem requisitos de rede específicos que devem ser atendidos para cada DAG e cada membro do DAG. Cada DAG deve ter uma única *rede MAPI*, que será usada por um membro do DAG para se comunicar com outros servidores (por exemplo, outros servidores do Exchange 2013 ou servidores de diretório), e zero ou mais *redes de Replicação*, que são redes dedicadas a registrar em log o envio e a propagação.

Nas versões anteriores do Exchange, é recomendável pelo menos duas redes (uma rede MAPI e uma rede de replicação) para DAGs. No Exchange 2013, várias redes são suportadas, mas nossa recomendação depende de sua topologia de rede física. Se você tiver várias redes físicas entre os membros do DAG fisicamente separados um do outro, em seguida, usando uma rede MAPI e replicação separada fornece redundância adicional. Se você tiver várias redes que são parcialmente fisicamente separados, mas convergem em uma única rede física (por exemplo, um único link WAN), em seguida, usando uma única rede (preferencialmente 10 gigabit Ethernet) para tráfego de replicação e MAPI é recomendável. Isso oferece simplicidade para a rede e o caminho de rede.

Considere o seguinte ao criar a infraestrutura de rede para o DAG:

  - Cada membro do DAG deve ter pelo menos um adaptador de rede que seja capaz de se comunicar com todos os outros membros do DAG. Se você estiver usando um caminho de rede único, recomendamos que você use um mínimo de Ethernet de 1 gigabit, mas preferencialmente 10 gigabit Ethernet. Além disso, ao usar um único adaptador de rede em cada membro DAG, recomendamos que você crie a solução global com o único adaptador de rede e o caminho em mente.

  - O uso de dois adaptadores de rede em cada membro DAG fornece uma rede MAPI e uma rede de replicação, com redundância da rede de replicação e os seguintes comportamentos de recuperação:
    
      - Se uma falha afetar a rede MAPI, ocorrerá um failover de servidor (pressupondo que haja cópias de banco de dados de caixa de correio íntegras que possam ser ativadas).
    
      - Em caso de uma falha afetar a rede de replicação, se a rede MAPI não for afetada pela falha, as operações de registro em log do envio e da propagação serão revertidas para usar a rede MAPI, mesmo se a rede MAPI tiver sua propriedade *ReplicationEnabled* definida como False. Quando a rede de replicação com falha for restaurada com integridade e estiver pronta para continuar as operações de registro em log do remessa e propagação, você deve alternar manualmente para a rede de replicação. Para alterar a replicação de uma rede MAPI para uma rede de Replicação recuperada, você pode suspender e retomar a replicação contínua utilizando os cmdlets **Suspend-MailboxDatabaseCopy** e **Resume-MailboxDatabaseCopy**, ou reiniciar o serviço de replicação do Microsoft Exchange. Recomendamos utilizar as operações suspender e retomar, para evitar a breve interrupção causada ao se reiniciar o serviço de Replicação do Microsoft Exchange.

  - Cada membro do DAG deve ter o mesmo número de redes. Por exemplo, se você pretende usar um único adaptador de rede em um membro do DAG, todos os membros do DAG também devem usar um único adaptador de rede.

  - Cada DAG deve ter mais de uma rede MAPI. A rede MAPI deve fornecer conectividade a outros servidores do Exchange e outros serviços, como Active Directory e DNS.

  - Redes de replicação adicionais podem ser adicionadas conforme necessário. Também é possível impedir um adaptador de rede individual de ser um único ponto de falha, usando uma equipe de adaptadores de rede ou tecnologia semelhante. No entanto, mesmo usando a equipe, isso não impede a rede de ser, ela própria, um único ponto de falha. Além disso, a equipe acrescenta complexidade desnecessária ao DAG.

  - Cada rede em cada servidor membro do DAG deve estar em sua própria sub-rede da rede. Cada servidor no DAG pode estar em uma sub-rede diferente, mas as redes MAPI e de replicação devem ser roteáveis e fornecer conectividade, como esta:
    
      - Cada rede em cada servidor membro do DAG está em sua própria sub-rede da rede separada da sub-rede usada por todas as outras redes no servidor.
    
      - A rede MAPI de cada servidor membro do DAG pode se comunicar com a rede MAPI de todos os outros membros do DAG.
    
      - A rede de replicação de cada servidor membro do DAG pode se comunicar com a rede de replicação de todos os outros membros do DAG.
    
      - Não há nenhum roteamento direto que permita o tráfego de pulsação da rede de replicação em um servidor membro do DAG para a rede MAPI em outro servidor membro DAG, ou vice-versa, ou entre várias redes de replicação no DAG.

  - Independentemente do local geográfico relativo a outros membros do DAG, cada membro do DAG não deve ter uma latência de rede de viagem de ida e volta maior que 500 milissegundos entre cada membro. Conforme a latência de ida e volta entre dois servidores de Caixa de Correio hospedando cópias de um banco de dados aumenta, o potencial para que a replicação não esteja atualizada também aumenta. Seja qual for a latência da solução, os clientes devem validar que as redes entre todos os membros do DAG sejam capazes de atingir os objetivos de proteção de dados e disponibilidade da implantação. Configurações com valores de latência mais altos podem exigir um ajuste especial de parâmetros do DAG, de replicação e de rede, como o aumento do número de bancos de dados ou a diminuição do número de caixas de correio por banco de dados, para que se atinjam os objetivos desejados.

  - Os requisitos de latência da viagem de ida e volta talvez não sejam os requisitos mais restritos de latência e de largura de banda da rede para uma configuração de vários datacenters. Avalie a carga de rede total, que inclui acesso para cliente, Active Directory, transporte, replicação contínua e outros tráfegos de aplicativo, para determinar os requisitos de rede necessários para o ambiente.

  - As redes do DAG dão suporte ao Protocolo TCP/IP versão 4 (IPv4) e IPv6. Só há suporte ao IPv6 quando o IPv4 também é usado; não há suporte a um ambiente de IPv6 puro. Só há suporte ao uso de endereços IPv6 e intervalos de endereços IP quando IPv6 e IPv4 estão habilitados nesse computador e a rede dá suporte a ambas as versões do endereço IP. Se o Exchange 2013 for implantado nessa configuração, todas as funções de servidor poderão enviar e receber dados de dispositivos, servidores e clientes que usem endereços IPv6.

  - O endereçamento APIPA (Automatic Private IP Addressing) é um recurso do Windows que atribui automaticamente endereços IP quando não há nenhum servidor de protocolo DHCP (Dynamic Host Configuration Protocol) disponível na rede. Não há suporte a endereços APIPA (inclusive endereços atribuídos manualmente do intervalo de endereços APIPA) a serem usados por DAGs ou pelo Exchange 2013.

## Requisitos de endereço IP e nome do DAG

Durante a criação, cada DAG recebe um nome exclusivo e um ou mais endereços IP estáticos, ou configurados para usarem DHCP. Independentemente de usar endereços atribuídos estática ou dinamicamente, qualquer endereço IP atribuído ao DAG deve estar na rede MAPI.

Cada DAG em execução no Windows Server 2008 R2 ou Windows Server 2012 exige um mínimo de um endereço IP na rede MAPI. Um DAG exige endereços IP adicionais quando a rede MAPI é estendida em várias sub-redes. DAGs em execução no Windows Server 2012 R2 criados com um ponto de acesso administrativo de cluster não exigem um endereço IP.

A figura a seguir ilustra um DAG em que todos os nós do DAG têm a rede MAPI na mesma sub-rede.

**DAG com rede MAPI na mesma sub-rede**

![DAG em uma única sub-rede](images/Dd638104.bcb7ef68-6d18-4516-a736-b936991c82cb(EXCHG.150).gif "DAG em uma única sub-rede")

Neste exemplo, a rede MAPI em cada membro do DAG está na sub-rede 172.19.18.*x*. Dessa forma, o DAG exige um único endereço IP nessa sub-rede.

A próxima figura ilustra um DAG com uma rede MAPI que se estende por duas sub-redes: 172.19.18.*x* e 172.19.19.*x*.

**DAG com rede MAPI em várias sub-redes**

![DAG estendido em diversas sub-redes](images/Dd638104.ffb57c64-3cb1-435c-8148-1b7154d1575c(EXCHG.150).gif "DAG estendido em diversas sub-redes")

Neste exemplo, a rede MAPI em cada membro do DAG está em uma sub-rede separada. Dessa forma, o DAG exige dois endereços IP: um para cada sub-rede na rede MAPI.

Sempre que a rede MAPI do DAG for estendida até uma sub-rede adicional, um endereço IP adicional para essa sub-rede deverá ser configurado para o DAG. Todos os endereços IP configurados para o DAG são atribuídos a e usados pelo cluster de failover subjacente do DAG. O nome do DAG também é usado como o nome do cluster de failover subjacente.

A qualquer momento específico, o cluster do DAG só usará um dos endereços IP atribuídos. O Cluster de Failover do Windows registra esse endereço IP no DNS quando o endereço IP do cluster e os recursos de nome da rede estão online. Além de usar um endereço IP e um nome da rede, um CNO (objeto de rede de cluster) é criado no Active Directory. O nome, o endereço IP e o CNO do cluster são usados internamente pelo sistema para proteger o DAG e para fins de comunicação interna. Os administradores e os usuários finais não precisam ter interface com ou se conectar ao nome do DAG ou ao endereço IP.


> [!NOTE]
> Muito embora o endereço IP do cluster e o nome da rede sejam usados internamente pelo sistema, não há nenhuma dependência difícil no Exchange 2013&nbsp;para que esses recursos estejam disponíveis. Mesmo se o ponto de acesso administrativo do cluster subjacente (por exemplo, seus recursos de endereço IP e Nome da Rede) estiver offline, a comunicação interna ainda ocorrerá no DAG por meio do uso de nomes de servidores membros do DAG. No entanto, recomendamos monitorar periodicamente a disponibilidade desses recursos para ter certeza de que eles não permaneçam offline por mais de 30 dias. Se o cluster subjacente permanecer offline por mais de 30 dias, a conta CNO do cluster poderá ser invalidada pelo mecanismo de coleta de lixo no Active Directory.



## Configuração do adaptador de rede para DAGs

Cada adaptador de rede deve ser configurado adequadamente, com base em seu uso pretendido. Um adaptador de rede que é usado para uma rede MAPI está configurado de forma diferente de um adaptador de rede que é usado para uma rede de replicação. Além de definir cada adaptador de rede corretamente, você também deve configurar a ordem de conexão de rede em Windows para que a rede MAPI está na parte superior da ordem de conexão. Para obter instruções detalhadas sobre como modificar a ordem de conexão de rede, consulte [modificar as vinculações de protocolo e a ordem dos provedores de rede](https://go.microsoft.com/fwlink/p/?linkid=179138).

## Configuração do adaptador de rede MAPI

Um adaptador de rede a ser usado por uma rede MAPI deve ser configurado conforme a descrição na tabela a seguir.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Recursos de rede</th>
<th>Configurações</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Cliente para redes Microsoft</p></td>
<td><p>Habilitado</p></td>
</tr>
<tr class="even">
<td><p>Agendador de pacotes QoS</p></td>
<td><p>Opcionalmente habilitado</p></td>
</tr>
<tr class="odd">
<td><p>Compartilhamento de arquivos e impressoras para redes Microsoft</p></td>
<td><p>Habilitado</p></td>
</tr>
<tr class="even">
<td><p>Protocolo TCP/IP versão 6 (TCP/IP v6)</p></td>
<td><p>Habilitado</p></td>
</tr>
<tr class="odd">
<td><p>Protocolo TCP/IP versão 4 (TCP/IP v4)</p></td>
<td><p>Habilitado</p></td>
</tr>
<tr class="even">
<td><p>Driver de E/S do mapeador da descoberta de topologia da camada de link</p></td>
<td><p>Habilitado</p></td>
</tr>
<tr class="odd">
<td><p>Respondente da descoberta de topologia da camada de link</p></td>
<td><p>Habilitado</p></td>
</tr>
</tbody>
</table>


As propriedades do TCP/IP v4 para um adaptador de rede MAPI são configuradas da seguinte forma:

  - O endereço IP da rede MAPI do membro do DAG pode ser atribuído manualmente ou configurado para usar DHCP. Se o DHCP for usado, recomendamos o uso de reservas persistentes para o endereço IP do servidor.

  - A rede MAPI normalmente usa um gateway padrão, embora ele não seja obrigatório.

  - Pelo menos um endereço de servidor DNS deve ser configurado. É recomendável o uso de vários servidores DNS para redundância.

  - A caixa de seleção **Registrar endereços desta conexão no DNS** deve ser marcada.

## Configuração do adaptador de rede de replicação

Um adaptador de rede a ser usado por uma rede de replicação deve ser configurado conforme a descrição na tabela a seguir.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Recursos de rede</th>
<th>Configurações</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Cliente para redes Microsoft</p></td>
<td><p>Desabilitado</p></td>
</tr>
<tr class="even">
<td><p>Agendador de pacotes QoS</p></td>
<td><p>Opcionalmente habilitado</p></td>
</tr>
<tr class="odd">
<td><p>Compartilhamento de arquivos e impressoras para redes Microsoft</p></td>
<td><p>Desabilitado</p></td>
</tr>
<tr class="even">
<td><p>Protocolo TCP/IP versão 6 (TCP/IP v6)</p></td>
<td><p>Habilitado</p></td>
</tr>
<tr class="odd">
<td><p>Protocolo TCP/IP versão 4 (TCP/IP v4)</p></td>
<td><p>Habilitado</p></td>
</tr>
<tr class="even">
<td><p>Driver de E/S do mapeador da descoberta de topologia da camada de link</p></td>
<td><p>Habilitado</p></td>
</tr>
<tr class="odd">
<td><p>Respondente da descoberta de topologia da camada de link</p></td>
<td><p>Habilitado</p></td>
</tr>
</tbody>
</table>


As propriedades do TCP/IP v4 para um adaptador de rede de replicação são configuradas da seguinte forma:

  - O endereço IP da rede de Replicação do membro do DAG pode ser atribuído manualmente ou configurado para usar DHCP. Se o DHCP for usado, recomendamos o uso de reservas persistentes para o endereço IP do servidor.

  - As redes de replicação normalmente não têm gateways padrão e, se a rede MAPI tiver um, nenhuma outra rede deverá ter. O roteamento do tráfego de rede em uma rede de replicação pode ser configurado usando-se rotas persistentes e estáticas para a rede correspondente em outros membros do DAG que usam endereços de gateway com a possibilidade de rotear entre as redes de replicação. Todo o outro tráfego correspondente a essa rota será tratado pelo gateway padrão configurado no adaptador da rede MAPI.

  - Os endereços de servidor DNS não devem ser configurados.

  - A caixa de seleção **Registrar endereços desta conexão no DNS** não deve ser marcada.

Voltar ao início

## Requisitos de servidor testemunha

*Servidor testemunha* é um servidor fora de um DAG usado para atingir e manter um quorum quando o DAG tiver um número par de membros. Os DAGs com um número ímpar de membros não usam um servidor testemunha. Todos os DAGs com um número par de membros devem usar um servidor testemunha. O servidor testemunha pode ser qualquer computador com o Windows Server em execução. Não há nenhum requisito para que a versão do sistema operacional Windows Server do servidor testemunha corresponda ao sistema operacional usado por membros do DAG.

O quorum é mantido no nível do cluster, abaixo do DAG. Um DAG tem quorum quando a maioria de seus membros estão online e podem se comunicar com os outros membros online do DAG. Essa noção de quorum é um aspecto do conceito de quorum no failover de cluster do Windows. Um aspecto relacionado e necessário ao quorum em clusters de failover é o *recurso de quorum*. O recurso de quorum é um recurso dentro de um cluster de failover que fornece um meio de arbitragem que leva a um estado de cluster e decisões de associação. O recurso de quorum também fornece armazenamento persistente para armazenar informações de configuração. Um complemento ao recurso de quorum é o *log de quorum*, que é um banco de dados de configuração do cluster. O log de quorum contém informações como quais servidores são membros do cluster, quais recursos são instalados no cluster e o estado desses recursos (por exemplo, online ou offline).

É essencial que cada membro do DAG tenha uma exibição consistente de como o cluster subjacente do DAG está configurado. O quorum funciona como o repositório definitivo de todas as informações de configuração relacionadas ao cluster. O quorum também é usado como um desempate para evitar a síndrome do *cérebro dividido*. A síndrome do cérebro dividido é uma condição que ocorre quando os membros do DAG não conseguem se comunicar entre si, embora estejam operantes. A síndrome da divisão é evitada exigindo-se sempre a disponibilidade e a interação da maioria dos membros do DAG (e, no caso dos DAGs com um número par de membros, o servidor testemunha do DAG) para que o DAG esteja operacional.

Voltar ao início

## Planejar a resiliência do site

Diariamente, mais empresas reconhecem que o acesso a um sistema de mensagens confiável e disponível é fundamental para seu sucesso. Para muitas organizações, o sistema de mensagens faz parte dos planos de continuidade dos negócios, e a implantação do serviço de mensagens foi projetada tendo a resiliência do site em mente. Fundamentalmente, muitas soluções resilientes do site envolvem a implantação de hardware em um segundo datacenter.

Em último caso, o design geral de um DAG, inclusive o número de membros do DAG e o número de cópias de banco de dados de caixa de correio, dependerá dos SLAs (contratos de nível de serviço) de recuperação de cada organização que cobrem vários cenários de falha. Durante o estágio de planejamento, os arquitetos das soluções e os administradores identificam os requisitos de implantação, inclusive os requisitos da resiliência do site em especial. Eles identificam os locais a serem usados e os alvos de SLA de recuperação obrigatórios. O SLA identificará dois elementos específicos que devem ser a base do design de uma solução que fornece alta disponibilidade e resiliência do site: o objetivo de tempo de recuperação e o objetivo de ponto de recuperação. Esses valores são medidos em minutos. O objetivo de tempo de recuperação é o tempo necessário para a restauração do serviço. O objetivo de ponto de recuperação se refere à atualização dos dados após a conclusão da operação de recuperação. Um SLA também pode ser definido para restaurar o serviço completo do datacenter principal após a correção de seus problemas.

Os arquitetos das soluções e os administradores também identificarão qual conjunto de usuários exige proteção de resiliência do site e determinarão se a solução multissite terá a configuração ativa/passiva ou ativa/ativa. Em uma configuração ativa/passiva, nenhum usuário costuma ser hospedado em um datacenter em espera. Em uma configuração ativa/ativa, os usuários são hospedados em ambos os locais, e parte da porcentagem do número total de bancos de dados dentro da solução tem um local ativo preferencial em um segundo datacenter. Quando há falha no serviço para os usuários de um datacenter, esses usuários são ativados no outro datacenter.

A criação dos SLAs apropriados normalmente exige respostas para as seguintes perguntas básicas:

  - Que nível de serviço é exigido após a falha do data center principal?

  - Os usuários precisam de seus dados ou apenas de serviços de mensagens?

  - Com que rapidez os dados são exigidos?

  - Quantos usuários devem ter suporte?

  - Como os usuários acessarão seus dados?

  - O que é a ativação do Data Center em espera SLA?

  - Como o serviço é movido novamente para o datacenter principal?

  - Os recursos são dedicados para a solução de resiliência do site?

Respondendo essas perguntas, você começa a formar um design resiliente do site para a solução de mensagens. Um requisito básico da recuperação de falha do site é criar uma solução que leve os dados necessários para o datacenter em espera que hospeda o serviço de mensagens em espera.

## Planejamento de certificado

Não há nenhuma consideração exclusiva ou especial quanto ao design de certificados durante a implantação de um DAG em um único datacenter. No entanto, durante a extensão de um DAG por vários datacenters em uma configuração resiliente do site, existem algumas considerações específicas em relação aos certificados. Em geral, o design do certificado dependerá do uso dos clientes, bem como dos requisitos de certificado de outros aplicativos que usam certificados. Mas há algumas recomendações específicas e práticas recomendadas que você deve seguir com relação ao tipo e ao número de certificados.

Como uma prática recomendada, minimize o número de certificados que você usa para seus servidores Exchange e servidores de proxy reverso. Recomendamos o uso de um único certificado para todas esses pontos de extremidade de serviço em cada datacenter. Essa abordagem minimiza o número de certificados necessários, o que reduz o custo e a complexidade da solução.

Para clientes do Outlook Anywhere, recomendamos que você use um único certificado SAN (Nome Alternativo do Requerente) para cada datacenter e inclua vários nomes de host no certificado. Para assegurar a conectividade do Outlook Anywhere após a alternância de um banco de dados, servidor ou datacenter, você deve usar o mesmo Nome Principal do Certificado em cada certificado e configurar o objeto de Configuração do Provedor do Outlook no Active Directory com o mesmo Nome Principal na Forma Padrão Microsoft (msstd). Por exemplo, se usar um Nome Principal do Certificado de mail.contoso.com, você configuraria o atributo da seguinte forma:

```powershell
Set-OutlookProvider EXPR -CertPrincipalName "msstd:mail.contoso.com"
```

Alguns aplicativos que se integram ao Exchange têm requisitos de certificado específicos que podem exigir o uso de certificados adicionais. O Exchange 2013 pode coexistir com o OCS (Office Communications Server). O OCS exige certificados com 1024 bits ou certificados maiores que usam o nome de servidor do OCS para o Nome Principal do Certificado. Como o uso de um nome de servidor do OCS para o Nome Principal do Certificado impediria o Outlook Anywhere de funcionar corretamente, você precisaria usar um certificado adicional e à parte para o ambiente do OCS.

## Planejamento de rede

Além dos requisitos específicos de rede que devem ser atendidos para cada DAG, bem como para cada servidor membro de um DAG, existem alguns requisitos e recomendações específicos de configurações de resiliência do site. Assim como acontece com todos os DAGs, independentemente de os membros do DAG serem implantados em um único site ou em vários sites, a latência de rede de retorno da viagem de ida e volta entre os membros do DAG não deve ser maior que 500 ms. Além disso, há definições de configuração específicas recomendáveis para os DAGs que se estendem por vários sites:

  - **Redes MAPI devem ser isoladas das redes de Replicação**   As políticas de rede do Windows, as políticas de firewall do Windows ou as ACLs (listas de controle de acesso) devem ser usadas para bloquear o tráfego entre a rede MAPI e as redes de Replicação. Essa configuração é necessária para impedir o crosstalk de pulsação da rede.

  - **Registros DNS voltados para o cliente devem ter uma TTL (vida útil) de cinco minutos**   O tempo de inatividade enfrentado pelo cliente depende não apenas da velocidade com que pode ocorrer a alternância, mas também da velocidade com que ocorre a replicação do DNS e da velocidade com que os clientes consultam informações atualizadas do DNS. Os registros de DNS de todos os serviços de cliente do Exchange, incluindo Microsoft Office Outlook Web App, Microsoft Exchange ActiveSync, serviços Web do Exchange, Outlook Anywhere, SMTP, POP3 e IMAP4 nos servidores DNS internos e externos devem ser definidos com uma TTL de cinco minutos.

  - **Usar rotas estáticas para configurar a conectividade em redes de replicação** Para fornecer a conectividade de rede entre cada um dos adaptadores de rede de replicação, use rotas estáticas persistentes. Essa é uma configuração rápida e única realizada em todos os membros do DAG durante o uso de endereços IP estáticos. Se você estiver usando o DHCP para obter endereços IP para redes de replicação, também será possível usá-lo para atribuir rotas estáticas para a replicação, o que simplifica o processo de configuração.

## Planejamento de resiliência do site geral

Além dos requisitos listados acima para alta disponibilidade, existem outras recomendações para implantar o Exchange 2013 em uma configuração resiliente do site (por exemplo, a extensão de um DAG até vários datacenters). O que você faz durante a fase de planejamento afetará diretamente o êxito da solução de resiliência do site. Por exemplo, um design de namespace ruim pode causar dificuldades com certificados, e uma configuração de certificado incorreta pode impedir usuários de acessar serviços.

Para minimizar o tempo necessário à ativação de um segundo datacenter e permitir ao segundo datacenter hospedar os pontos de extremidade de serviço de um datacenter com falha, o planejamento apropriado deve ser concluído. Eis alguns exemplos:

  - As metas de SLA para a solução de resiliência do site devem estar bem compreendidas e documentadas.

  - Os servidores no segundo datacenter devem ter capacidade suficiente para hospedar a população de usuários combinada de ambos os datacenters.

  - O segundo datacenter deve ter todos os serviços habilitados fornecidos no datacenter principal (a menos que o serviço não esteja incluído como parte do SLA de resiliência do site). Isso inclui o Active Directory, a infraestrutura de rede (por exemplo, DNS, TCP/IP etc.), os serviços de telefonia (se a Unificação de Mensagens estiver sendo usada) e a infraestrutura do site (energia ou refrigeração).

  - Para que alguns serviços possam atender a usuários do datacenter com falha, eles devem ter os certificados de servidor configurados corretamente. Alguns serviços não permitem a instanciação (por exemplo, POP3 e IMAP4) e só permitem o uso de um único certificado. Nesses casos, o certificado deve ser um certificado SAN que inclua vários nomes, ou os vários nomes devem ser semelhantes o suficiente para que um certificado curinga possa ser usado (pressupondo que as políticas de segurança da organização permitam o uso de certificados curinga).

  - Os serviços necessários devem ser definidos no segundo datacenter. Por exemplo, se o primeiro datacenter tiver três URLs SMTP diferentes em servidores de transporte diferentes, a configuração apropriada deverá ser definida no segundo datacenter para habilitar pelo menos um (se não todos os três) servidor de transporte para hospedar a carga de trabalho.

  - A configuração de rede necessária deve estar in-loco para dar suporte à alternância de datacenter. Isso pode significar a verificação de que as configurações de balanceamento de carga estejam in-loco, de que o DNS global esteja configurado e de que a conexão da Internet esteja habilitada com o roteamento apropriado configurado.

  - A estratégia de habilitação das alterações de DNS necessárias a uma alternância de datacenter deve ser compreendida. As alterações de DNS específicas, inclusive suas configurações de TTL, devem ser definidas e documentadas para dar suporte ao SLA em vigor.

  - A estratégia de teste da solução também deve ser estabelecida e considerada no SLA. A validação periódica da implantação é a única forma de garantir que a qualidade e a viabilidade da implantação não sejam degradadas com o passar do tempo. Após a validação da implantação, recomendamos que a parte da configuração que afeta diretamente o êxito da solução seja documentada explicitamente. Além disso, recomendamos que você aperfeiçoe os processos de gerenciamento de alterações quanto a esses segmentos da implantação.

Voltar ao início

