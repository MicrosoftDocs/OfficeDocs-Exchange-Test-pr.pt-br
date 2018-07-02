---
title: 'Virtualização do Exchange 2013: Exchange 2013 Help'
TOCTitle: Virtualização do Exchange 2013
ms:assetid: 36184b2f-4cd9-48f8-b100-867fe4c6b579
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/JJ619301(v=EXCHG.150)
ms:contentKeyID: 50485326
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Virtualização do Exchange 2013

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2017-08-08_

Você pode implantar o Microsoft Exchange Server 2013 em um ambiente virtualizado. Este tópico fornece uma visão geral dos cenários que são suportados para implantar o Exchange 2013 em software de virtualização de hardware.

**Sumário**

Requirements for hardware virtualization

Host machine storage requirements

Exchange storage requirements

Exchange memory requirements and recommendations

Host-based failover clustering and migration for Exchange

Os termos a seguir são usados nesta discussão sobre a virtualização do Exchange:

  - **Inicialização a frio**   Ao retomar o sistema de um estado de desligamento para uma inicialização limpa do sistema operacional, a ação é uma *inicialização a frio*. Nenhum estado de sistema operacional persiste nesse caso.

  - **Estado salvo**   Quando uma maquina virtual é desligada, normalmente os hipervisores tem a capacidade de salvar o estado da máquina virtual, então, quando a máquina é ligada novamente, ele retorna ao *estado salvo* em vez de uma inicialização a frio.

  - **Migração planejada**   Quando um administrador do sistema inicia o movimentação de uma máquina virtual a partir de um hipervisor host para outro, a ação é uma *migração planejada*. A ação poderia ser uma migração única ou o administrador de sistema pode configurar a automação para mover a máquina virtual de forma programada. Uma migração planejada também poderia ser o resultado de algum outro evento que ocorre no sistema, diferente de falha de hardware ou software. O ponto-chave é a máquina virtual do Exchange que está operando normalmente e necessita ser realocada por algum motivo. Essa realocação pode ser feita através de tecnologia, como o Live Migration ou VMotion. No entanto, se a máquina virtual do Exchange ou o host do hipervisor em que a máquina virtual está localizada passa por algum tipo de condição de falha, o resultado não se caracteriza como uma migração planejada.

## Requisitos para virtualização de hardware

A Microsoft aceitará o Exchange 2013 em produção no software de virtualização de hardware apenas quando todas as seguintes condições forem verdadeiras:

  - O software de virtualização de hardware está executando um dos seguintes procedimentos:
    
      - Qualquer versão do Windows Server com tecnologia Hyper-V ou Microsoft Hyper-V Server
    
      - Qualquer hipervisor de terceiros que tenha sido validado sob o [Programa de validação de virtualização do Windows Server](https://go.microsoft.com/fwlink/p/?linkid=125375).
    

    > [!TIP]
    > Implantação do Exchange 2013 em provedores de infra-estrutura-como um serviço (IaaS) é suportada se todos os requisitos de suporte são atendidos. No caso de provedores que são provisionamento de máquinas virtuais, esses requisitos incluem garantindo que o hipervisor que está sendo usado para máquinas virtuais do Exchange é totalmente suportado e que atenda a infraestrutura a ser utilizado por Exchange o requisitos de desempenho que foram determinados durante o processo de dimensionamento. Implantação de máquinas virtuais do Microsoft Azure é suportada se todos os volumes de armazenamento usado para bancos de dados do Exchange e logs de transações do banco de dados (incluindo bancos de dados de transporte) estão configurados para o armazenamento do Azure Premium.



  - A máquina virtual convidada com o Exchange tem as seguintes condições:
    
      - Está executando o Exchange 2013.
    
      - Está implantada no Windows Server 2008 R2 SP1 (ou versões posteriores), ou no Windows Server 2012, ou no Windows Server 2012 R2.

Para implantações do Exchange 2013:

  - Todas as funções de servidor do Exchange 2013 têm suporte em uma máquina virtual.

  - As máquinas virtuais do servidor do (incluindo as máquinas virtuais de Caixa de Correio do Exchange que são parte de um grupo de disponibilidade de banco de dados ou DAG), podem ser combinadas com cluster de failover baseado em host e tecnologia de migração, desde que as máquinas virtuais sejam configuradas de modo que não salvem e restaurem estado no disco quando alteradas ou desligadas. Toda atividade de failover que ocorra no nível do hipervisor deve resultar em uma inicialização a frio quando a máquina virtual estiver ativada no nó alvo. Toda migração planejada deve resultar em desligamento ou inicialização a frio, e uma migração online que faça uso de uma tecnologia como a migração Live Hyper-V. A migração hipervisor de máquinas virtuais é suportada pelo vendedor hipervisor. Desse modo, verifique se o vendedor hipervisor testou e suporta a migração das máquinas virtuais do Exchange. A Microsoft oferece suporte á migração Live Hyper-V dessas máquinas virtuais.

  - Somente um software de gerenciamento (por exemplo, software antivírus, software de backup ou software de gerenciamento de máquina virtual) poderá ser implantado na máquina host física. Nenhum outro aplicativo baseado em servidor (por exemplo, Exchange, SQL Server, Active Directory ou SAP) deverá ser instalado na máquina host. A máquina host deve ser dedicada para executar máquinas virtuais de convidados.

  - Alguns hipervisores incluem recursos para obtenção de instantâneos de máquinas virtuais. Os instantâneos de máquina virtual capturam o estado de uma máquina virtual durante a sua execução. Esse recurso permite obter vários instantâneos de uma máquina virtual e reverter a máquina virtual para qualquer um dos estados anteriores aplicando um instantâneo à máquina virtual. Entretanto, os instantâneos da máquina virtual não são sensíveis a aplicativos, e utilizá-los pode trazer consequências inesperadas e não intencionais para um aplicativo do servidor que mantenha dados de estado, como o Exchange. Como resultado, não é possível obter instantâneos de máquina virtual de uma máquina virtual de convidado do Exchange.

  - Muitos produtos de virtualização de hardware permitem que você especifique o número de processadores virtuais que deve ser alocada para cada máquina virtual convidada. Os processadores virtuais localizados na máquina virtual convidada compartilharem um número fixo de núcleos de processador físico no sistema físico. Exchange oferece suporte a uma taxa de núcleo de processador virtual do processador-para-físico não maior que 2:1, embora seja recomendável uma taxa de 1:1. Por exemplo, um sistema de processador dual usando processadores de núcleo quádruplo contém um total de 8 núcleos de processador físico no sistema host. Em um sistema com essa configuração, não aloca mais do que um total de 16 processadores virtuais para todas as máquinas virtuais de convidado combinadas.

  - Ao calcular o número total de processadores virtuais necessários pela máquina host, você deverá levar em conta também os requisitos do sistema operacional e de E/S. Na maioria dos casos, o número equivalente de processadores virtuais exigido no sistema operacional host para um sistema que hospeda máquinas virtuais do Exchange é 2. Esse valor deve ser usado como uma linha de base para o processador virtual do sistema operacional host ao se calcular a taxa global de núcleos físicos para processadores virtuais. Se o monitoramento de desempenho do sistema operacional host indicar que você está consumindo mais recursos de processador do que o equivalente a 2 processadores, será preciso reduzir a contagem de processadores virtuais designados às máquinas virtuais de convidado conforme o necessário e verificar se a taxa global de processador virtual para núcleo físico não é superior a 2:1.

  - O sistema operacional de uma máquina de convidado do Exchange deve usar um disco que tenha um tamanho mínimo de 15 GB mais o tamanho da memória virtual que está alocada na máquina de convidado. Esse requisito é necessário para atender aos requisitos de disco do sistema operacional e do arquivo de paginação. Por exemplo, se a máquina de convidado tiver alocado 16 GB de memória, o espaço em disco mínimo necessário para o disco do sistema operacional será de 31 GB.
    
    Além disso, é possível que as máquinas virtuais de convidado possam ser impedidas de se comunicar diretamente com o Fibre Channel ou com HBAs (adaptadores de barramento de host) SCSI instalados na máquina host. Nesse caso, você deve configurar os adaptadores no sistema operacional da máquina host e apresentar os LUNs (números de unidades lógicas) às máquinas virtuais de convidado como um disco virtual ou um disco de passagem.

  - A única maneira com suporte para enviar emails a domínios externos do Azure recursos de computação é por meio de uma retransmissão de SMTP (também conhecida como um host inteligente de SMTP). O recurso do Azure compute envia o email para a retransmissão de SMTP e, em seguida, o provedor de retransmissão de SMTP oferece o email para o domínio externo. Microsoft Exchange Online Protection for um provedor de uma retransmissão de SMTP, mas há um número de provedores de terceiros também. Para obter mais informações, consulte a postagem [Envio de email do recurso do Windows Azure Compute a domínios externos](https://go.microsoft.com/fwlink/p/?linkid=799723)do Blog da equipe de suporte do Microsoft Azure.

Voltar ao início

## Requisitos de armazenamento da máquina host

Os requisitos de espaço mínimo em disco para cada máquina host são os seguintes:

  - Máquinas de host em alguns aplicativos de virtualização de hardware podem exigir o espaço de armazenamento para um sistema operacional e seus componentes. Por exemplo, quando executando Windows Server 2008 R2 com Hyper-V, você precisará de um mínimo de 10 GB para cumprir os requisitos para Windows Server 2008. Para obter mais detalhes, consulte [Requisitos de sistema do Windows Server 2008 R2](https://go.microsoft.com/fwlink/p/?linkid=125378). Espaço de armazenamento adicional também é necessária para suportar o arquivo de paginação do sistema operacional, software de gerenciamento e travar arquivos de recuperação (dump).

  - Alguns hipervisores mantêm arquivos na máquina host que são exclusivos para cada máquina virtual de convidado. Por exemplo, em um ambiente do Hyper-V, um arquivo de armazenamento de memória temporário (arquivo BIN) é criado e mantido para cada máquina de convidado. O tamanho de cada arquivo BIN é igual à quantidade de memória alocada para a máquina de convidado. Além disso, outros arquivos também podem ser criados e mantidos na máquina host para cada máquina de convidado.

  - Se sua máquina host esteja executando Windows Server 2012 Hyper-V ou 2012 Hyper-V e você estiver configurando um cluster de failover baseado em host que irá hospedar servidores de caixa de correio Exchange em um grupo de disponibilidade do banco de dados, é recomendável seguir as orientações documentadas artigo da Base de Conhecimento Microsoft, [2872325, Cluster de convidado nós no Hyper-V podem não ser capazes de criar ou ingressar em](https://support.microsoft.com/kb/2872325).

Voltar ao início

## Requisitos de armazenamento do Exchange

Os requisitos de armazenamento conectado ao servidor do Exchange virtualizado são:

  - A cada máquina de convidado do Exchange, deve ser alocado espaço de armazenamento suficiente na máquina host para o disco fixo que contém o sistema operacional de convidado, todos os arquivos de armazenamento de memória temporários em uso e os arquivos da máquina virtual relacionados que estão hospedados na máquina host. Além disso, para cada máquina de convidado do Exchange, você deve alocar também armazenamento suficiente para as filas de mensagens e armazenamento suficiente para os bancos de dados e os arquivos de log nos servidores de Caixa de Correio.

  - O armazenamento usado por máquina convidada Exchange para armazenamento de dados de Exchange (por exemplo, bancos de dados de caixa de correio e filas de transporte) pode ser armazenamento virtual de tamanho fixo (por exemplo, discos rígidos virtuais fixos (VHD ou VHDX) em um ambiente Hyper-V), armazenamento virtual dinâmico ao usar arquivos VHDX com Hyper-V, armazenamento de passagem SCSI ou armazenamento de Internet SCSI (iSCSI). Armazenamento de passagem é armazenamento que tiver configurado no nível do host e dedicado à máquina um convidado. Todo o armazenamento usado por uma máquina de convidado Exchange para armazenamento de dados de Exchange deve ser blocos de armazenamento porque Exchange 2013 não é compatível com o uso de volumes de armazenamento (NAS Network) conectado à rede, que não seja no cenário SMB 3.0 descritos posteriormente nesta tópico. Além disso, armazenamento NAS apresentada para o convidado como não há suporte para armazenamento de blocos via o hipervisor.

  - Discos virtuais fixos ou dinâmicos podem ser armazenados em arquivos SMB 3.0 que contam com o armazenamento de blocos se a máquina convidada está sendo executado no Windows Server 2012 Hyper-V (ou uma versão posterior do Hyper-V). Os únicos suporte para uso do 3.0 SMB compartilhamentos de arquivos é para armazenamento de discos virtuais fixos ou dinâmicos. Esses compartilhamentos de arquivos não podem ser usados para o armazenamento de dados de Exchange diretamente. Ao usar os compartilhamentos de arquivos SMB 3.0 para armazenar discos virtuais fixos ou dinâmicos, o armazenamento fazendo o compartilhamento de arquivo deve ser configurado para alta disponibilidade garantir a melhor disponibilidade possível do serviço do Exchange.

  - O armazenamento usado pelo Exchange deve ser hospedado em eixos de disco separados do armazenamento que está hospedando o sistema operacional da máquina virtual de convidado.

  - Há suporte para a configuração do armazenamento iSCSI para uso de um iniciador iSCSI dentro de uma máquina virtual de convidado do Exchange. Entretanto, haverá um desempenho reduzido nessa configuração se a pilha de rede dentro de uma máquina virtual não tiver recursos completos (por exemplo, nem todas as pilhas de rede virtual aceitam quadros jumbo).

Voltar ao início

## Requisitos e recomendações de memória do Exchange

Alguns hipervisores podem superestimar ou ajustar dinamicamente a quantidade de memória disponível para uma máquina convidada específica com base no uso percebido de memória na máquina convidada em comparação às necessidades de outras máquinas convidadas gerenciadas pelo mesmo hipervisor. Essa tecnologia faz sentido para cargas de trabalho nas quais a memória seja necessária por breves períodos de tempo e depois possa ser liberada para outros usos. Porém, isso não faz sentido para cargas de trabalho projetadas para usar memória de forma contínua. , como muitos aplicativos para servidores com otimizações de desempenho que envolvem o cache de dados na memória, é suscetível a um desempenho ruim do sistema e a uma experiência de cliente inaceitável caso não tenha controle total sobre a memória alocada à máquina física ou virtual na qual está sendo executado. Como consequência, não há suporte para a utilização de recursos de memória dinâmica para o Exchange.

Voltar ao início

## Cluster de failover baseado em host e migração para o Exchange

A seguir, estão as respostas para algumas das perguntas frequentes sobre cluster de failover baseado em host e tecnologia de migração com DAGs do Exchange 2013:

  - **A Microsoft oferece suporte à tecnologia de migração de terceiros?**
    
    A Microsoft não pode fazer instruções de suporte para a integração de produtos hipervisores de terceiros usando essas tecnologias com o Exchange, pois essas tecnologias não fazem parte do Programa de Validação de Virtualização de Servidores (SVVP). O SVVP abrange outros aspectos do suporte da Microsoft para hipervisores de terceiros. É necessário se assegurar que seu fornecedor de hipervisor suporta a combinação de sua tecnologia de migração e cluster com o Exchange. Se o seu fornecedor de hipervisor suporta sua tecnologia de migração com o Exchange, então a Microsoft suportará o Exchange com sua tecnologia de migração.

  - **Como a Microsoft define o cluster de failover baseado em host?**
    
    Cluster de failover baseado em host se refere a qualquer tecnologia que fornece a capacidade automática de reagir a falhas no nível do host e iniciar as máquinas virtuais afetadas em servidores alternativos. O uso desta tecnologia é suportada uma vez que, em um cenário de falha, a máquina virtual está chegando de uma inicialização a frio de um host alternativo. Essa tecnologia ajuda a garantir que a máquina virtual nunca opere a partir de um estado salvo que persiste no disco porque ele vai ser obsoleto em relação ao resto dos membros do DAG.

  - **O que a Microsoft quer dizer com suporte à migração?**
    
    Tecnologia de migração se refere qualquer tecnologia que permite uma movimentação planejada de uma máquina virtual a partir de uma máquina host para outra máquina host. Essa movimentação também poderia ser um movimento automatizado que ocorre como parte recurso de balanceamento de carga, mas ela não está relacionada com uma falha no sistema. Migrações são suportados desde que as máquinas virtuais nunca operem a partir de um estado salvo que persiste no disco. Isso significa que a tecnologia que move uma máquina virtual, transportando o estado e memória da máquina virtual através da rede sem tempo de inatividade percebido é suportado para utilização com o Exchange. Um fornecedor de hipervisor de terceiros deve fornecer suporte para a tecnologia de migração, enquanto a Microsoft fornecerá suporte para o Exchange quando usado nessa configuração.

Voltar ao início

