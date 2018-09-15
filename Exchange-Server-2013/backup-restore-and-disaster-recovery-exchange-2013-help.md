---
title: 'Backup, restauração e recuperação de desastres: Exchange 2013 Help'
TOCTitle: Backup, restauração e recuperação de desastres
ms:assetid: 394fc4ed-fa02-41fa-9159-cc2754ff8875
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Dd876874(v=EXCHG.150)
ms:contentKeyID: 50485387
ms.date: 01/10/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Backup, restauração e recuperação de desastres

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2016-12-09_

Como parte do planejamento para proteção de dados, é importante compreender as formas nas quais os dados podem ser protegidos e determinar qual o método que melhor atende às necessidades da organização. O planejamento para proteção de dados é um processo complexo que depende de várias decisões tomadas durante a fase de planejamento da implantação.

Os backups têm sido usados, tradicionalmente, para os seguintes cenários:

  - **Recuperação de desastres**   Em caso de falha de hardware ou software, várias cópias de banco de dados em um DAG possibilitam alta disponibilidade com failover rápido e pouca, ou nenhuma, perda de dados. Isso elimina o tempo de inatividade e a perda de produtividade resultante, um custo significativo de recuperação de um backup pontual anterior em disco ou em fita. Os DAGs podem ser ampliados para vários sites e podem fornecer resiliência diante de falhas no disco, no servidor, na rede e no datacenter.

  - **Recuperação de itens excluídos acidentalmente**   Historicamente, em uma situação na qual um usuário excluiu itens que posteriormente precisarão ser recuperados, isso envolvia a localização da mídia de backup na qual os dados que precisavam ser recuperados foram armazenados e, de alguma forma, a obtenção e fornecimento dos itens desejados ao usuário. Com a nova pasta Itens Recuperáveis no Exchange 2013 e a Política de Retenção que pode ser aplicada a ela, é possível reter todos os dados excluídos e modificados durante um período especificado, para que a recuperação desses itens seja mais fácil e rápida. Isso reduz a carga sobre os administradores do Exchange e a assistência técnica de TI, permitindo aos usuários finais recuperarem itens excluídos acidentalmente por eles próprios, o que reduz a complexidade e os custos administrativos associados à recuperação de um único item. Para obter mais informações, consulte [Conformidade e política de sistema de mensagens](messaging-policy-and-compliance-exchange-2013-help.md) e [Prevenção de perda de dados](https://docs.microsoft.com/pt-br/exchange/security-and-compliance/data-loss-prevention/data-loss-prevention).

  - **Armazenamento de dados a longo prazo**   Os backups também têm sido usados como um arquivo morto, e a fita costuma ser usada para preservar instantâneos pontuais de dados por longos períodos, segundo os requisitos de conformidade. Os novos recursos de arquivamento, de pesquisa em várias caixas de correio e de retenção de mensagens do Exchange 2013 fornecem um mecanismo para preservar dados de maneira acessível ao usuário final com eficiência durante longos períodos. Isso elimina restaurações onerosas a partir de fita e aumenta a produtividade. Para obter mais informações, consulte [Arquivamento In-loco do Exchange 2013](in-place-archiving-in-exchange-2013-exchange-2013-help.md), [Descoberta Eletrônica In-loco](https://docs.microsoft.com/pt-br/exchange/security-and-compliance/in-place-ediscovery/in-place-ediscovery) e [Retenção local e Retenção de litígio](https://docs.microsoft.com/pt-br/exchange/security-and-compliance/in-place-and-litigation-holds).

  - **Instantâneo de banco de dados pontual**   Se uma cópia pontual anterior dos dados de caixa de correio for um requisito para a sua organização, o Exchange garantirá a possibilidade de criação de uma cópia do banco de dados com retardamento em um ambiente do DAG. Isso pode ser útil no caso raro de um dano lógico no armazenamento se replicar pelas várias cópias de bancos de dados no DAG, o que resulta na necessidade de retornar a um momento anterior. Isso também poderá ser útil se um administrador excluir acidentalmente caixas de correio ou dados do usuário. A recuperação a partir de uma cópia com retardamento pode ser mais rápida do que a restauração a partir de um backup porque as cópias com retardamento não exigem um processo de cópia demorado do servidor de backup para o servidor do Exchange. Isso pode reduzir significativamente o custo total de propriedade, reduzindo o tempo de inatividade.

Porque há recursos nativos do Exchange 2013 que atendem a cada um desses cenários de maneira eficiente e econômica, você poderá reduzir ou eliminar o uso de backups tradicionais em seu ambiente.

Proteção de Dados Nativa do Exchange

Tecnologias de backup compatíveis

Gravador VSS do Exchange 2013

Recuperação do Exchange Server

Recuperação de repositório unificado de contatos

Banco de Dados de Recuperação

Portabilidade do banco de dados

Portabilidade de sinal de linha

## Proteção de Dados Nativa do Exchange

A [arquitetura preferida](https://blogs.technet.com/b/exchange/archive/2014/04/21/the-preferred-architecture.aspx) da Microsoft para o Exchange Server 2013 utiliza um conceito conhecido como Proteção de Dados Nativa do Exchange. A Proteção de Dados Nativa do Exchange baseia-se nos recursos internos do Exchange para proteger os dados de caixa de correio, sem o uso de backups (mesmo que você ainda possa usar esses recursos e fazer backups). O Exchange 2013 contém vários novos recursos e alterações centrais que, quando implantadas e configuradas corretamente, podem fornecer proteção de dados nativa, eliminando a necessidade de fazer backups tradicionais dos dados. O uso dos recursos de alta disponibilidade se integram ao Exchange 2013 para minimizar o tempo de inatividade e a perda de dados caso haja um desastre também podem reduzir o custo total de propriedade do sistema de mensagens. Ao combinar esses recursos a outros recursos internos, como à Retenção de litígio, você pode reduzir ou eliminar o uso de backups pontuais tradicionais e reduzir os custos associados.

Além de determinar se o Exchange 2013 permitirá a você abandonar os backups pontuais tradicionais, também recomendamos que você avalie os custos de sua infraestrutura de backup atual. Considere os custos de perda de dados e tempo de inatividade de usuário final ao tentar se recuperar de um desastre usando sua infraestrutura de backup existente. Inclua também os custos com hardware, instalação e licenças, além do custo de gerenciamento associado à recuperação de dados e à manutenção de backups. Dependendo dos requisitos de sua organização, é bem provável que um ambiente puro do Exchange 2013 com pelo menos três cópias de banco de dados de caixa de correio ofereça um custo total de propriedade menor do que um com backups.

Existem vários problemas a serem considerados antes do uso dos recursos integrados ao Exchange 2013 em substituição a backups tradicionais. Também pode haver considerações exclusivas para sua organização. Considere as seguintes questões e note que isto não é uma lista exaustiva:

  - Você deve determinar quantas cópias do banco de dados precisam ser implantadas. É altamente recomendável implantar pelo menos três cópias (sem atraso) de um banco de dados de caixa de correio antes de eliminar formas tradicionais de proteção do banco de dados, como backups RAID ou tradicionais baseados em VSS.

  - As metas para tempo e ponto de recuperação devem ser definidas claramente e você deve estabelecer que o uso de um conjunto combinado de recursos internos em lugar dos backups tradicionais permite atingir essas metas.

  - Você deve determinar quantas cópias de cada banco de dados são necessárias para cobrir os vários cenários de falha diante dos quais o sistema foi projetado para se proteger.

  - É necessário determinar se a eliminação do uso de um DAG ou de algum de seus membros garante custos suficientes para suportar uma solução de backup tradicional. Se a resposta for sim, você deverá determinar se essa solução irá melhorar os SLAs (contratos de nível de serviço) por objetivo de tempo ou de ponto de recuperação.

  - Você deve determinar se pode se dar ao luxo de perder uma cópia pontual se o membro DAG que hospeda a cópia apresentar uma falha que afete a cópia ou a integridade da cópia.

  - O Exchange 2013 permite que você implante caixas de correio muito maiores, como um tamanho máximo recomendado para banco de dados de caixa de correio igual a 2 terabytes (quando duas ou mais cópias de banco de dados de caixa de correio de alta disponibilidade estão sendo usadas). Com base nas caixa de correio maiores que a maioria das organizações tende a implantar, é necessário determinar o objetivo quanto ao ponto de recuperação se você precisar repetir um grande número de arquivos de log ao ativar uma cópia de banco de dados ou uma cópia de banco de dados com atraso.

  - É preciso determinar como você irá detectar e evitar o dano lógico em uma cópia de banco de dados ativa decorrente da replicação para as cópias passivas do banco de dados. Isso inclui determinar o plano de recuperação para essa situação e o quão frequentemente esse cenário ocorreu no passado. Se o dano lógico ocorrer com frequência na organização, será recomendável levar esse cenário em conta no projeto usando-se uma ou mais cópias com retardamento, com uma janela de intervalo de repetição suficiente para permitir a detecção e a ação diante do dano lógico quando ele ocorrer, mas antes desse dano ser replicado para outras cópias de banco de dados.

Uma das funções realizadas ao final de um backup completo ou incremental com êxito é o truncamento dos arquivos de log da transação que não são mais necessários à recuperação do banco de dados. Se não estiverem sendo realizados backups, não ocorrerá truncamento de log. Para evitar um acúmulo de arquivos de log, você habilita o registro em log circular para os bancos de dados replicados. Ao integrar o registro em log circular à replicação contínua, você tem um novo tipo de registro em log circular chamado de CRCL (registro em log circular de replicação contínua), diferente do registro em log circular ESE (Mecanismo de Armazenamento Extensível). Enquanto o log circular ESE é executado e gerenciado pelo serviço Repositório de Informações do Microsoft Exchange, o CRCL é executado e gerenciado pelo serviço de Replicação do Microsoft Exchange. Quando ativado, o log circular ESE não gera arquivos de log adicionais; em vez disso, ele substitui o arquivo de log atual, quando necessário. Contudo, em um ambiente de replicação contínua, os arquivos de log são necessários para envio e repetição. O resultado é que, ao ativar o CRCL, o arquivo de log atual não é substituído e são gerados arquivos de log fechados para o processo de envio e repetição de log.

Especificamente, o Serviço de Replicação do Microsoft Exchange gerencia o CRCL para que a continuidade dos logs seja mantida e os logs não sejam excluídos se ainda forem necessários para replicação. O Serviço de Replicação do Microsoft Exchange e o serviço Repositório de Informações do Microsoft Exchange se comunicam usando chamadas de procedimento remoto (RPCs) em relação a quais arquivos de log podem ser excluídos.

Para que ocorra truncamento em cópias de banco de dados de caixa de correio altamente disponíveis (sem atraso), os itens a seguir devem ser verdadeiros:

  - Foi realizado o backup do arquivo de log, ou o CRCL está habilitado.

  - O arquivo de log está abaixo do ponto de verificação.

  - As outras cópias sem atraso do banco de dados estão de acordo com exclusão.

  - O arquivo de log foi inspecionado por todas as cópias com atraso de banco de dados.

Para que ocorra truncamento em cópias de banco de dados de caixa com atraso, os itens a seguir devem ser verdadeiros:

  - O arquivo de log está abaixo do ponto de verificação.

  - O arquivo de log é mais antigo que ReplayLagTime + TruncationLagTime.

  - O arquivo de log foi excluído na cópia ativa do banco de dados.

Proteção de Dados Nativa do Exchange

## Tecnologias de backup compatíveis

O Exchange 2013 é compatível apenas com backups que reconhecem o Exchange e são baseados no VSS. O Exchange 2013 inclui um plugin para Backup do Windows Server que permite fazer e restaurar backups de dados do Exchange baseados em VSS. Para fazer backup e restaurar o Exchange 2013, você deve usar um aplicativo que reconheça o Exchange e que seja compatível com o gravador VSS para Exchange 2013, como o Backup do Windows Server (com o plug-in VSS), o Microsoft System Center 2012 - Data Protection Manager ou um aplicativo de terceiros baseado em VSS que reconheça o Exchange.

Para instruções detalhadas sobre backup e restauração de dados do Exchange usando o Backup do Windows Server, consulte [Usar o Backup do Windows Server para fazer backup e restaurar dados do Exchange](using-windows-server-backup-to-back-up-and-restore-exchange-data-exchange-2013-help.md).

Proteção de Dados Nativa do Exchange

## Gravador VSS do Exchange 2013

O Exchange 2013 apresenta uma mudança expressiva da arquitetura do gravador VSS usado no Exchange 2010 e no Exchange 2007. Essas versões anteriores do Exchange incluíam dois gravadores VSS: um dentro do serviço Repositório de Informações do Microsoft Exchange (store.exe) e outro dentro do serviço de Replicação do Microsoft Exchange. No Exchange, a funcionalidade do gravador VSS encontrada anteriormente no serviço Repositório de Informações do Microsoft Exchange foi movida para o serviço de Replicação do Microsoft Exchange. O novo gravador, chamado de Gravador do Microsoft Exchange, agora é usado por aplicativos baseados em VSS que reconhecem o Exchange para fazer backup de cópias ativas e passivas de banco de dados e para restaurar cópias de bancos de dados a partir de seus backups. Embora o novo gravador seja executado no serviço de Replicação do Microsoft Exchange, ele exige que o serviço Repositório de Informações do Microsoft Exchange esteja em execução para que o gravador seja anunciado. Com isso, ambos os serviços são necessários para o backup ou a restauração de bancos de dados do Exchange.

Proteção de Dados Nativa do Exchange

## Recuperação do Exchange Server

Quase todas as configurações dos servidores de Caia de Correio e Acesso para Cliente são armazenadas no Active Directory. Assim como acontecia com versões anteriores do Exchange, o Exchange 2013 inclui um parâmetro de Instalação para recuperação de servidores perdidos. Esse parâmetro, */m:RecoverServer*, é usado para recompilar e recriar um servidor perdido, usando-se as definições e as informações de configuração armazenadas no Active Directory. Entretanto, lembre-se que há várias configurações que não são restauradas, como alterações no arquivo local web.config e em outros arquivos de configuração. Além disso, as entradas de registro personalizadas não serão restauradas. Recomendamos o uso de um processo de gerenciamento de alterações confiável para rastrear e recriar estas mudanças.

Para obter etapas detalhadas sobre a realização da recuperação de um servidor perdido do Exchange 2013, consulte [Recuperar um Exchange Server](recover-an-exchange-server-exchange-2013-help.md). Para obter etapas detalhadas sobre a recuperação de um servidor perdido que seja membro de um grupo de disponibilidade do banco de dados (DAG), consulte [Recuperar um servidor membro de grupo de disponibilidade de banco de dados](recover-a-database-availability-group-member-server-exchange-2013-help.md).

Proteção de Dados Nativa do Exchange

## Recuperação de repositório unificado de contatos

Quando o Microsoft Lync Server 2013 é usado em um ambiente do Exchange 2013, as informações de contato do Lync do usuário são armazenadas em uma pasta especial de contatos na caixa de correio do usuário. Isto é referido como o repositório unificado de contatos (UCS). Se você restaurar uma caixa de correio migrada do UCS, a lista de contatos de mensagens instantâneas do usuário de destino pode ser afetada. Se o usuário foi migrado após o último backup, a restauração da caixa de correio resultará em uma perda completa da lista de contatos do usuário. Em casos menos graves, as modificações na lista de contatos feitas pelo usuário desde o último backup serão perdidas. Para migrar essa possível perda de dados, certifique-se de que o usuário seja migrado de volta para o servidor de mensagens instantâneas antes da restauração da caixa de correio.

Proteção de Dados Nativa do Exchange

## Banco de Dados de Recuperação

Banco de dados de recuperação é um tipo especial de banco de dados de caixa de correio que permite montar um banco de dados de caixa de correio restaurado e extrair dados do banco de dados restaurado como parte de uma operação de recuperação. É possível usar o cmdlet [New-MailboxRestoreRequest](https://technet.microsoft.com/pt-br/library/ff829875\(v=exchg.150\)) para extrair dados de um banco de dados de recuperação. Após a extração, os dados podem ser exportados para uma pasta ou mesclados em uma caixa de correio existente. Os bancos de dados de recuperação permitem recuperar dados de um backup ou da cópia de um banco de dados sem atrapalhar o acesso do usuário a dados atuais.

Não há suporte ao uso de um banco de dados de recuperação para um banco de dados de caixa de correio de versões anteriores do Exchange. Além disso, a caixa de correio de destino usada em mesclagens de dados e extrações deve estar na mesma floresta do Active Directory do banco de dados montado no banco de dados de recuperação.

Para mais informações, consulte [Bancos de dados de recuperação](recovery-databases-exchange-2013-help.md). Para instruções detalhadas sobre como criar um banco de dados de recuperação, consulte [Criar um banco de dados de recuperação](create-a-recovery-database-exchange-2013-help.md). Para instruções detalhadas sobre como usar um banco de dados de recuperação, consulte [Restaurar dados usando um banco de dados de recuperação](restore-data-using-a-recovery-database-exchange-2013-help.md).

Proteção de Dados Nativa do Exchange

## Portabilidade do banco de dados

A portabilidade do banco de dados é um recurso que permite que um banco de dados de caixa de correio do Exchange 2013 seja movido para, e montado em, qualquer outro servidor de caixa de correio do Exchange 2013 na mesma organização. Usando a portabilidade de banco de dados, a confiabilidade é aprimorada pela remoção de diversas etapas manuais suscetíveis a erros dos processos de recuperação. Além disso, essa portabilidade reduz os tempos de recuperação gerais de vários cenários de falha.

Para obter mais informações, consulte [Portabilidade do banco de dados](database-portability-exchange-2013-help.md). Para obter instruções detalhadas sobre portabilidade de banco de dados, consulte [Mover um banco de dados de caixa de correio usando a portabilidade de banco de dados](move-a-mailbox-database-using-database-portability-exchange-2013-help.md).

Proteção de Dados Nativa do Exchange

## Portabilidade de sinal de linha

A portabilidade de sinal de linha é um recurso que fornece uma solução de continuidade comercial limitada para falhas que afetem um banco de dados de caixa de correio, um servidor ou um site inteiro. A portabilidade de sinal de linha permite que um usuário tenha uma caixa de correio temporária para envio e recebimento de emails enquanto a caixa de correio original está sendo restaurada ou reparada. A caixa de correio temporária pode estar no mesmo servidor de Caixa de Correio do Exchange 2013 ou em qualquer outro servidor de Caixa de Correio do Exchange 2013 em sua organização. Isso permite que um servidor alternativo hospede as caixas de correio de usuários que estavam antes em um servidor que não está mais disponível. Clientes que oferecem suporte à Descoberta Automática, como o Microsoft Outlook, são automaticamente redirecionados para o novo servidor, sem a necessidade de atualização manual do perfil da área de trabalho do usuário. Após os dados da caixa de correio original do usuário serem restaurados, um administrador pode mesclar a caixa de correio recuperada e a caixa de correio com sinal de linha de um usuário em uma caixa de correio única e atualizada.

O processo para o uso da portabilidade de sinal de linha é denominado uma *recuperação de sinal de linha*. Uma recuperação de sinal de linha envolve a criação de um banco de dados vazio em um servidor de Caixa de Correio para substituir o banco de dados com falha. Esse banco de dados vazio, conhecido como *banco de dados de sinal de linha*, permite que os usuários enviem e recebam emails enquanto o banco de dados em falha está sendo recuperado. Após a recuperação do banco de dados em falha, o banco de dados de sinal de linha e o banco de dados recuperado são trocados e, em seguida, os dados do banco de dados de sinal de linha são mesclados ao banco de dados recuperado.

Para obter mais informações, consulte [Portabilidade de tom de discagem](dial-tone-portability-exchange-2013-help.md). Para obter instruções detalhadas sobre a realização de uma recuperação de sinal de linha, consulte [Executar uma recuperação de sinal de linha](perform-a-dial-tone-recovery-exchange-2013-help.md).

Proteção de Dados Nativa do Exchange

