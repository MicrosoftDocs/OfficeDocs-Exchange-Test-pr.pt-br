---
title: 'Gerenciando cópias de banco de dados de caixa de correio: Exchange 2013 Help'
TOCTitle: Gerenciando cópias de banco de dados de caixa de correio
ms:assetid: 28cedf1d-365a-4e36-b2ba-6bf81af8684f
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Dd335158(v=EXCHG.150)
ms:contentKeyID: 50485196
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Gerenciando cópias de banco de dados de caixa de correio

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2016-08-26_

Depois que o grupo de disponibilidade de banco de dados (DAG) tiver sido criado, configurado e preenchido com os membros do servidor de Caixa de Correio, você pode usar o Centro de Administração do Exchange (EAC) ou o Shell de gerenciamento do Exchange para adicionar cópias de bancos de dados de caixa de correio de maneira flexível e granular.

## Gerenciar cópias de banco de dados

Após a criação de várias cópias de um banco de dados, é possível usar o EMC e o Shell para monitorar a integridade e o status de cada cópia, além de realizar outras tarefas de gerenciamento associadas a cópias de banco de dados. Algumas das tarefas de gerenciamento que você talvez precise realizar incluem a suspensão ou a retomada de uma cópia de banco de dados, a propagação de uma cópia de banco de dados, o monitoramento de cópias de banco de dados, a configuração das definições da cópia de banco de dados e a remoção da cópia de banco de dados.

## Suspender e retomar cópias de banco de dados

Por várias razões, como realização de manutenção planejada, talvez seja necessário suspender e retomar a atividade de replicação contínua para uma cópia de banco de dados. Além disso, algumas tarefas administrativas, como a propagação, exigem que você primeiro suspenda a cópia do banco de dados. Recomendamos suspender toda a atividade de replicação quando o caminho do banco de dados ou dos arquivos de log estiver sendo alterado. É possível suspender e retomar a atividade de cópia de banco de dados usando o EAC ou executando os cmdlets **Suspend-MailboxDatabaseCopy** e **Resume-MailboxDatabaseCopy** no Shell. Para obter instruções detalhadas sobre como suspender ou retomar a atividade de replicação contínua para uma cópia do banco de dados, consulte [Suspender ou retomar uma cópia do banco de dados de caixa de correio](suspend-or-resume-a-mailbox-database-copy-exchange-2013-help.md).

## Propagar uma cópia do banco de dados

A *propagação*, também conhecida como *atualização*, é o processo no qual um banco de dados, seja um banco de dados vazio ou uma cópia do banco de dados de produção, é adicionado ao local da cópia de destino em outro servidor de Caixa de Correio no mesmo DAG do banco de dados ativo. Ele se torna o banco de dados de linha de base para a cópia mantida pelo servidor.

Dependendo da situação, a propagação pode ser um processo automático ou manual que você inicia. Quando uma cópia de banco de dados for adicionada, ela será propagada automaticamente, desde que o servidor de destino e o armazenamento sejam configurados corretamente. Se você quiser propagar manualmente uma cópia do banco de dados e não quiser que ocorra a propagação automática quando criar a cópia, você poderá usar o parâmetro *SeedingPostponed* ao executar o cmdlet [Add-MailboxDatabaseCopy](https://technet.microsoft.com/pt-br/library/dd298105\(v=exchg.150\)).

As cópias de banco de dados raramente precisam ser novamente propagadas após a propagação inicial. Mas, se uma nova propagação for necessária ou se você deseja propagar manualmente uma cópia do banco de dados em vez de o sistema propagá-la automaticamente, essas tarefas poderão ser realizadas usando o assistente de Atualização de Cópia de Banco de Dados de Caixa de Correio no EAC ou usando o cmdlet [Update-MailboxDatabaseCopy](https://technet.microsoft.com/pt-br/library/dd335201\(v=exchg.150\)) no Shell. Antes de propagar uma cópia de banco de dados, você deve primeiro suspender a cópia de banco de dados de caixa de correio. Para obter etapas detalhadas sobre como propagar a cópia de um banco de dados, consulte [Atualizar uma cópia de banco de dados de caixa de correio](update-a-mailbox-database-copy-exchange-2013-help.md).

Após a conclusão de uma operação de propagação manual, a replicação da cópia de banco de dados de caixa de correio propagada é retomada automaticamente. Se você não quiser que a replicação seja retomada automaticamente, será possível usar o parâmetro *ManualResume* durante a execução do cmdlet [Update-MailboxDatabaseCopy](https://technet.microsoft.com/pt-br/library/dd335201\(v=exchg.150\)).

## Escolher o que propagar

Ao realizar uma operação de propagação, você pode optar por propagar a cópia de banco de dados de caixa de correio, o catálogo de índice de conteúdo para a cópia do banco de dados de caixa de correio, ou a cópia do banco de dados e a cópia do catálogo de índice de conteúdo.

O comportamento padrão do Assistente de cópia de banco de dados de caixa de correio de atualização e o cmdlet [Update-MailboxDatabaseCopy](https://technet.microsoft.com/pt-br/library/dd335201\(v=exchg.150\)) é propagar a cópia do banco de dados de caixa de correio e da cópia do catálogo de índice de conteúdo. Para propagar apenas a cópia do banco de dados de caixa de correio sem propagar o catálogo de índice de conteúdo, use o parâmetro *DatabaseOnly* ao executar o cmdlet [Update-MailboxDatabaseCopy](https://technet.microsoft.com/pt-br/library/dd335201\(v=exchg.150\)) . Para propagar apenas a cópia do catálogo de índice de conteúdo, use o parâmetro *CatalogOnly* ao executar o cmdlet [Update-MailboxDatabaseCopy](https://technet.microsoft.com/pt-br/library/dd335201\(v=exchg.150\)) .

## Selecionar a fonte da propagação

Qualquer cópia de banco de dados íntegra pode ser usada como a origem de propagação de uma cópia adicional desse banco de dados. Isso é especialmente útil quando você tem um DAG estendido por vários locais físicos. Por exemplo, considere uma implantação do DAG com quatro membros, na qual dois membros (MBX1 e MBX2) estejam localizados em Portland, Oregon, e dois (MBX3 e MBX4) estejam em Nova York, Nova York. Um banco de dados de caixa de correio chamado DB1 está ativo em MBX1 e há cópias passivas de DB1 em MBX2 e MBX3. Ao adicionar uma cópia do DB1 para o MBX4, você tem a opção de usar a cópia no MBX3 como a origem da propagação. Fazendo isso, você evita propagar pelo link da rede de longa distância (WAN) entre Portland e Nova York.

Para usar uma cópia específica como a origem de propagação ao adicionar uma nova cópia de banco de dados, você faria o seguinte:

  - Use o parâmetro *SeedingPostponed* ao executar o cmdlet [Add-MailboxDatabaseCopy](https://technet.microsoft.com/pt-br/library/dd298105\(v=exchg.150\)) para adicionar a cópia de banco de dados. Se o parâmetro *SeedingPostponed* não for usado, a cópia de banco de dados será propagada explicitamente usando-se a cópia ativa do banco de dados como a fonte.

  - Você pode especificar o servidor de origem que deseja usar como parte do assistente de Atualização de Cópia do Banco de Dados de Caixa de Correio no EAC, ou você pode usar o parâmetro *SourceServer* ao executar o cmdlet [Update-MailboxDatabaseCopy](https://technet.microsoft.com/pt-br/library/dd335201\(v=exchg.150\)) para especificar o servidor de origem desejado para a propagação. No exemplo anterior, você especificaria MBX3 como o servidor de origem. Se o parâmetro *SourceServer* não for usado, a cópia de banco de dados será propagada explicitamente usando-se a cópia ativa do banco de dados.

## Propagação e redes

Além de selecionar um servidor de origem específico para propagar uma cópia de banco de dados de caixa de correio, você também pode usar o Shell para especificar quais redes do DAG usar e, opcionalmente, substituir as configurações de compactação e criptografia da rede do DAG durante a operação de propagação.


> [!NOTE]
> Propagar um catálogo de índice do contexto só é possível através de uma rede MAPI. Isso acontece, mesmo se você usar o parâmetro <CODE>-Network</CODE> no cmdlet Update-MailboxDatabaseCopy.



Para especificar as redes que você deseja usar para propagação, use o parâmetro *Network* ao executar o cmdlet [Update-MailboxDatabaseCopy](https://technet.microsoft.com/pt-br/library/dd335201\(v=exchg.150\)) e especifique as redes do DAG que você deseja usar. Se você não usar o parâmetro *Network*, o sistema usará o seguinte comportamento-padrão para selecionar uma rede a ser usada na operação de propagação:

  - Se o servidor de origem e o servidor de destino estiverem na mesma sub-rede e uma rede de replicação tiver sido configurada incluindo a sub-rede, a rede de replicação será usada.

  - Se o servidor de origem e o servidor de destino estiverem em sub-redes diferentes, mesmo que uma rede de replicação contendo essas sub-redes for configurada, a rede cliente (MAPI) será usada na propagação.

  - Se o servidor de origem e o servidor de destino estiverem em datacenters diferentes, a rede cliente (MAPI) será usada na propagação.

No nível do DAG, as redes do DAG são configuradas para criptografia e compactação. As configurações padrão são para usar a criptografia e a compactação apenas na comunicação em sub-redes diferentes. Se a origem e o destino estiverem em sub-redes diferentes e o DAG estiver configurado com os valores-padrão para *NetworkCompression* e *NetworkEncryption*, será possível substituir esses valores usando-se os parâmetros *NetworkCompressionOverride* e *NetworkEncryptionOverride*, respectivamente, durante a execução do cmdlet [Update-MailboxDatabaseCopy](https://technet.microsoft.com/pt-br/library/dd335201\(v=exchg.150\)).

## Processo de propagação

Quando você iniciar um processo de propagação usando os cmdlets [Add-MailboxDatabaseCopy](https://technet.microsoft.com/pt-br/library/dd298105\(v=exchg.150\)) ou [Update-MailboxDatabaseCopy](https://technet.microsoft.com/pt-br/library/dd335201\(v=exchg.150\)), as seguintes tarefas serão realizadas:

1.  As propriedades do banco de dados do Active Directory são lidas para validar o banco de dados especificado e os servidores, além de verificar se os servidores de origem e de destino estão executando o Exchange 2013, se eles são membros do mesmo DAG e se o banco de dados especificado não é um banco de dados de recuperação. Os caminhos do arquivo de banco de dados também são lidos.

2.  As preparações ocorrem para verificações novamente propagadas a partir do serviço de replicação do Microsoft Exchange no servidor de destino.

3.  O serviço de replicação do Microsoft Exchange no servidor de destino verifica a presença de arquivos do log de transação e do banco de dados nos diretórios de arquivos lidos pelas verificações do Active Directory na etapa 1.

4.  O serviço de replicação do Microsoft Exchange retorna as informações de status do servidor de destino para a interface administrativa onde o cmdlet foi executado.

5.  Se todas as verificações preliminares tiverem sido aprovadas, você será solicitado a confirmar a operação antes de continuar. Se você confirmar a operação, o processo continuará. Se um erro for encontrado durante as verificações preliminares, o erro será informado e haverá falha na operação.

6.  A operação de propagação é iniciada no serviço de replicação do Microsoft Exchange no servidor de destino.

7.  O serviço de replicação do Microsoft Exchange suspende a replicação do banco de dados para a cópia do banco de dados ativa.

8.  As informações de estado do banco de dados são atualizadas pelo serviço de replicação do Microsoft Exchange para refletir um status de Propagação.

9.  Se o servidor de destino ainda não tiver os diretórios para os arquivos do banco de dados de destino e do log, eles serão criados.

10. Uma solicitação para propagar o banco de dados é passada do serviço de replicação do Microsoft Exchange, no servidor de destino, para o serviço de replicação do Microsoft Exchange, no servidor de origem, usando TCP. Essa solicitação e a comunicação subsequente para a propagação do banco de dados ocorrem em uma rede do DAG configurada como uma rede de replicação.

11. O serviço de replicação do Microsoft Exchange no servidor de origem inicia um backup de streaming do Mecanismo de Armazenamento Extensível (ESE) por meio da interface de serviço de Armazenamento de Informações do Microsoft Exchange.

12. O serviço de Armazenamento de Informações do Microsoft Exchange transmite os dados do banco de dados para o serviço de replicação do Microsoft Exchange.

13. Os dados do banco de dados são movidos do serviço de replicação do Microsoft Exchange do servidor de origem para o serviço de replicação do Microsoft Exchange do servidor de destino.

14. O serviço de replicação do Microsoft Exchange no servidor de destino grava a cópia do banco de dados em um diretório temporário localizado no diretório de banco de dados principal chamado *temp-seeding*.

15. A operação de backup de streaming no servidor de origem termina quando se atinge o final do banco de dados.

16. A operação de gravação no servidor de destino é concluída e o banco de dados é movido do diretório temp-seeding para o local final. O diretório temp-seeding é excluído.

17. No servidor de destino, o serviço de replicação do Microsoft Exchange usa um proxy para uma solicitação ao serviço de pesquisa do Microsoft Exchange para montar o catálogo do índice de conteúdo, caso ele exista. Se houver arquivos de catálogo desatualizados existentes de uma instância anterior da cópia do banco de dados, haverá falha na operação da montagem, que dispara a necessidade de replicar o catálogo do servidor de origem. Da mesma forma, se o catálogo não existir em uma nova instância da cópia do banco de dados no servidor de destino, uma cópia do catálogo será obrigatória. O serviço de replicação do Microsoft Exchange orienta o serviço de pesquisa do Microsoft Exchange a suspender a indexação da cópia do banco de dados enquanto um novo catálogo é copiado da origem.

18. O serviço de replicação do Microsoft Exchange no servidor de destino envia uma solicitação de catálogo de propagação para o serviço de replicação do Microsoft Exchange no servidor de origem.

19. No servidor de origem, o serviço de replicação do Microsoft Exchange solicita as informações sobre o diretório do serviço de pesquisa do Microsoft Exchange e a suspensão dessa indexação.

20. O serviço de pesquisa do Microsoft Exchange no servidor de origem retorna as informações sobre o diretório do catálogo de pesquisa para o serviço de replicação do Microsoft Exchange.

21. O serviço de replicação do Microsoft Exchange no servidor de origem lê os arquivos de catálogo a partir do diretório.

22. O serviço de replicação do Microsoft Exchange no servidor de origem move os dados do catálogo para o serviço de replicação do Microsoft Exchange no servidor de destino, usando uma conexão na rede de replicação. Após a conclusão da leitura, o serviço de replicação do Microsoft Exchange envia uma solicitação para o serviço de pesquisa do Microsoft Exchange, para retomar a indexação do banco de dados de origem.

23. Se houver algum arquivo de catálogo existente no servidor de destino no diretório, o serviço de replicação do Microsoft Exchange no servidor de destino o excluirá.

24. O serviço de replicação do Microsoft Exchange no servidor de destino grava os dados do catálogo em um diretório temporário chamado *CiSeed.Temp* até a conclusão da transferência dos dados.

25. O serviço de replicação do Microsoft Exchange move todos os dados do catálogo para o local final.

26. O serviço de replicação do Microsoft Exchange no servidor de destino retoma a indexação de pesquisa no banco de dados de destino.

27. O serviço de replicação do Microsoft Exchange no servidor de destino retorna um status de conclusão.

28. O resultado final da operação é passado para a interface administrativa a partir da qual o cmdlet foi chamado.

## Configurar cópias de banco de dados

Após a criação de uma cópia de banco de dados, é possível exibir e modificar as definições de configuração quando necessário. É possível exibir algumas informações de configuração examinando a página **Propriedades** de uma cópia de banco de dados no EAC. Também é possível usar os cmdlets [Get-MailboxDatabase](https://technet.microsoft.com/pt-br/library/bb124924\(v=exchg.150\)) e [Set-MailboxDatabaseCopy](https://technet.microsoft.com/pt-br/library/dd298104\(v=exchg.150\)) no Shell para exibir e configurar as definições de cópia do banco de dados, como intervalo de repetição, intervalo de truncamento e ordem de preferência de ativação. Para instruções detalhadas sobre como visualizar e configurar as definições de cópia do banco de dados, consulte [Configurar propriedades de cópia de banco de dados de caixa de correio](configure-mailbox-database-copy-properties-exchange-2013-help.md).

## Usar opções de retardo de truncamento e de retardo de repetição

As cópias de banco de dados de caixa de correio dão suporte ao uso de um *tempo de retardo de repetição* e de um *tempo de retardo de truncamento*, ambos configurados em minutos. A configuração de um tempo de retardo de repetição permite restaurar uma cópia de backup de banco de dados para uma hora específica. A configuração de um tempo de retardo de truncamento permite usar os logs em uma cópia de banco de dados passiva para se recuperar da perda de arquivos de log na cópia de banco de dados ativa. Como esses recursos resultam na criação temporária de arquivos de log, o uso de um deles afetará o projeto de armazenamento.

## Tempo de retardo de repetição

Tempo de retardo de repetição é uma propriedade de uma cópia de banco de dados de caixa de correio que especifica o tempo, em minutos, de atraso para a repetição do log para a cópia de banco de dados. O cronômetro do tempo de retardo de repetição se inicia quando um arquivo de log é replicado para a cópia passiva e passa com êxito pela inspeção. Atrasando a repetição dos logs para a cópia de banco de dados, você tem a possibilidade de recuperar o banco de dados para um ponto específico anterior. Uma cópia de banco de dados de caixa de correio configurada com um tempo de retardo de repetição maior que 0 é conhecida como uma *cópia de banco de dados de caixa de correio com retardamento* ou simplesmente uma *cópia com retardamento*.

Uma estratégia que usa cópias de banco de dados e os recursos de retenção em litígio no Exchange 2013 podem fornecer proteção contra várias falhas que acabariam causando a perda de dados. No entanto, esses recursos não podem fornecer proteção contra a perda de dados em caso de dano lógico, que, embora raro, pode causar a perda de dados. As cópias com retardamento foram criadas para evitar a perda de dados em caso de dano lógico. Em geral, há dois tipos de dano lógico:

  - **Dano lógico ao banco de dados**   A soma de verificação das páginas de banco de dados corresponde, mas os dados nas páginas estão errados do ponto de vista lógico. Isso pode ocorrer quando o ESE tenta gravar em uma página de banco de dados e, mesmo que o sistema operacional retorne uma mensagem de êxito, os dados jamais são gravados no disco ou são gravados no lugar errado. Isso é conhecido como *liberação perdida*. Para evitar que liberações perdidas percam dados, o ESE inclui um mecanismo de detecção de liberação perdida no banco de dados com um recurso de aplicação de patch de página (restauração de página única).

  - **Dano lógico ao repositório**   Os dados são adicionados, excluídos ou manipulados de forma inesperada pelo usuário. Esses casos normalmente são causados por aplicativos de terceiros. Ele normalmente é apenas um dano no sentido em que o usuário o considera assim. O repositório do Exchange considera a transação que produziu o dano lógico uma série de operações MAPI válidas. O recurso de retenção de litígio no Exchange 2013 oferece proteção contra a corrupção lógica do repositório (pois ele evita que o conteúdo seja excluído permanentemente por um usuário ou aplicativo). Entretanto, pode haver cenários em que uma caixa de correio de usuário se torne tão corrompida que seria mais fácil restaurar o banco de dados até um ponto no tempo antes da corrupção e depois exportar a caixa de correio do usuário, para recuperar dados não corrompidos.

A combinação das cópias de banco de dados, da diretiva de guarda e da restauração de página única do ESE deixa apenas o caso de dano lógico raro, mas catastrófico, do repositório. A decisão de usar uma cópia de banco de dados com um tempo de retardo de repetição (uma cópia com retardamento) dependerá dos aplicativos de terceiros usados e do histórico da organização com dano lógico ao repositório.

Cópias com retardamento podem administrar a próprias no Exchange 2013 quando você chama a reprodução de log automática para descartar os arquivos de log em certos cenários:

  - Quando um limite de pouco espaço em disco é atingido

  - Quando a cópia com retardamento tem corrupção física e precisa passar por correção de página

  - Quando há menos de três cópias íntegras disponíveis (apenas ativa ou passiva; cópias de banco de dados com retardamento não são contadas) por mais de 24 horas

Página de aplicação de patch está disponível para cópias com retardamento através esse recurso de descarte automático. Se o sistema detectar que a correção de página é necessária para uma cópia com atraso, os logs são automaticamente reproduzidos na cópia com atraso para executar a correção de página. Cópias com retardamento também chamar esse recurso de repetição automática quando um limite de espaço em disco insuficiente tiver sido alcançado, e quando a cópia com atraso foi detectada como a cópia disponível apenas para um período de tempo específico.

O comportamento de descarte da cópia com retardamento está desabilitado por padrão e pode ser habilitado pela execução do seguinte comando.

```powershell
Set-DatabaseAvailabilityGroup <DAGName> -ReplayLagManagerEnabled $true
```

Uma vez habilitado, o descarte ocorrerá quando houver menos de três cópias. Você pode alterar o valor padrão de 3 modificando o seguinte valor do registro DWORD.

**HKLM\\Software\\Microsoft\\ExchangeServer\\v15\\Replay\\Parameters\\ReplayLagManagerNumAvailableCopies**

Para habilitar o descarte de limites de pouco espaço em disco, será preciso configurar a seguinte entrada do Registro.

**HKLM\\Software\\Microsoft\\ExchangeServer\\v15\\Replay\\Parameters\\ReplayLagLowSpacePlaydownThresholdInMB**

Após configurar essas configurações de Registro, reinicie o serviço de Gerenciamento do Microsoft Exchange DAG para fazer com que as alterações entrem em vigor.

Como um exemplo, considere um ambiente em que um dado banco de dados tenha 4 cópias ( 3 cópias com disponibilidade alta e 1 cópia com atraso) e a configuração padrão seja usada para ReplayLagManagerNumAvailableCopies. Se uma cópia sem atraso estiver fora de serviço por qualquer motivo (por exemplo, se estiver suspensa, etc) então uma cópia com atraso vai desprezar automaticamente os arquivos de log em 24 horas.

Se você optar por usar atraso cópias sem habilitar o parâmetro `ReplayLagManagerEnabled` , esteja ciente das seguintes implicações:

  - O tempo de retardo de repetição é um valor configurado por administrador e, por padrão, permanece desabilitado.

  - A configuração do tempo de retardo de repetição tem uma definição padrão de zero dia e uma definição máxima de 14 dias.

  - As cópias com retardamento não são consideradas cópias altamente disponíveis. Em vez disso, elas foram criadas para fins de recuperação de desastre, para proteger do dano lógico ao armazenamento.

  - Quanto maior for o tempo de retardo de repetição definido, mais longo será o processo de recuperação do banco de dados. Dependendo do número de arquivos de log que precisam ser repetidos durante a recuperação e da velocidade na qual o hardware pode repeti-los, talvez sejam necessárias várias horas para recuperar um banco de dados.

  - Recomendamos que você determine se as cópias com retardamento são críticas para a estratégia de recuperação de desastre geral. Se o uso deles for crítico à estratégia, recomendamos o uso de várias cópias com retardamento ou o uso de uma RAID (Redundant Array of Independent Disks) para proteger uma única cópia com retardamento, se você não tiver várias cópias com retardamento. Se perder um disco ou ocorrer um dano, você não perderá o ponto com retardamento.

  - As cópias com retardamento não podem receber o patch com o recurso de restauração de página única do ESE. Se uma cópia com retardamento encontrar um dano à página do banco de dados (por exemplo, um erro -1018), ela terá que ser novamente propagada (o que fará o aspecto com retardamento da cópia se perder).

A ativação e a recuperação de uma cópia de banco de dados de caixa de correio com retardamento formarão um processo simples, se você quiser que o banco de dados repita todos os arquivos de log e torne a cópia de banco de dados a atual. Se quiser repetir os arquivos de log até um ponto específico no tempo, essa será uma operação mais difícil porque você manipula os Utilitários do Banco de Dados do Exchange Server (Eseutil.exe).

Para instruções detalhadas sobre como ativar uma cópia do banco de dados de caixa de correio com retardamento, consulte [Ativar uma cópia do banco de dados de caixa de correio com atraso](activate-a-lagged-mailbox-database-copy-exchange-2013-help.md).

## Tempo de retardo de truncamento

Tempo de retardo de truncamento é uma propriedade de uma cópia de banco de dados de caixa de correio que especifica o tempo, em minutos, de atraso para a exclusão do log após a repetição do arquivo de log na cópia de banco de dados. O cronômetro do retardo de truncamento se inicia quando um arquivo de log é replicado para a cópia passiva e passa com êxito pela inspeção, além de ser repetido com êxito na cópia do banco de dados. Atrasando o truncamento dos logs da cópia de banco de dados, você tem a possibilidade de se recuperar de falhas que afetam os arquivos de log para a cópia ativa do banco de dados.

## Cópias de banco de dados e truncamento de log

Truncamento de log funciona da mesma em Exchange 2013 como no Exchange 2010. Comportamento de truncamento é determinado pelas repetição retardo truncamento e tempo de retardo tempo configurações para a cópia.

Os seguintes critérios deverão ser atendidos para que um arquivo de log do banco de dados seja truncado quando as configurações do retardo forem deixadas em valores-padrão iguais a zero (desabilitadas):

  - O backup do arquivo de log deve ser feito com êxito, ou o registro em log circular deve ser habilitado.

  - O arquivo de log deve estar abaixo do ponto de verificação (o arquivo de log mínimo obrigatório à recuperação) para o banco de dados.

  - Todas as outras cópias com retardamento devem ter inspecionado o arquivo de log.

  - Todas as outras cópias (sem retardamento) devem ter repetido o arquivo de log.

Os seguintes critérios devem ser atendidos para que ocorra o truncamento de uma cópia de banco de dados com retardamento:

  - O arquivo de log deve estar abaixo do ponto de verificação do banco de dados.

  - O arquivo de log deve ser anterior a ReplayLagTime + TruncationLagTime.

  - O arquivo de log deve ter sido truncado na cópia ativa.

No Exchange 2013, o truncamento de log não ocorre na cópia do banco de dados de caixa de correio ativo quando uma ou mais cópias passivas são suspensas. Se você tiver planejado atividades de manutenção que vão demorar muito (por exemplo, alguns dias), você pode ter um acúmulo considerável de arquivos de log. Para evitar que a unidade de log fiquei cheia de logs de transação, você pode remover a cópia do banco de dados passiva afetada, ao invés de suspendê-la. Quando a manutenção planejada estiver concluída, você pode readicionar a cópia do banco de dados passiva.

Exchange 2013 O Service Pack 1 (SP1) introduz um novo recurso denominado *truncamento flexível*, que, por padrão, vem desabilitado. Durante operações normais, cada cópia do banco de dados mantém logs que precisam ser enviados às outras cópias do banco de dados até que todas as cópias de um banco de dados confirmem ter reproduzido (cópias passivas) ou recebido (cópias atrasadas) os arquivos de log. Este é o comportamento padrão de truncamento de log. Se uma cópia do banco de dados ficar offline por algum motivo, os arquivos de log começam a se acumular nos discos usados pelas outras cópias do banco de dados. Se a cópia do banco de dados afetada continuar offline por um longo período, isto fará com que as demais cópias do banco de dados fiquem sem espaço em disco.

Quando o truncamento flexível estiver habilitado, o comportamento de truncamento será diferente. Cada cópia de banco de dados rastreia seu próprio espaço livre em disco e aplica o comportamento de truncamento flexível caso o espaço livre seja reduzido. Para a cópia ativa, a cópia isolada mais antiga (a cópia de banco de dados passiva que está mais longe da reprodução do log) é ignorada e o truncamento respeita as cópias passivas mais antigas restantes. A cópia do banco de dados ativa é onde o truncamento global é calculado. As cópias passivas tentarão respeitar a decisão de truncamento tomada na cópia ativa. Apesar da implicação do nome MinCopiesToProtect, o Exchange só ignorará a cópia isolada mais antiga conhecida no momento da execução do truncamento. Para uma cópia passiva, se o espaço ficar reduzido, ela truncará independentemente seus arquivos de log usando os parâmetros configurados descritos abaixo.

Quando o banco de dados offline ficar novamente online, estarão faltando arquivos de log que foram excluídos das outras cópias íntegras, e o status da cópia do banco de dados será FailedAndSuspended. Nesse caso, se o Autoreseed estiver configurado, a cópia afetada será automaticamente repropagada. Se o recurso Autoreseed não estiver configurado, a cópia do banco de dados precisará ser propagada manualmente por um administrador.

A quantidade necessária de cópias íntegras, o limite de espaço livre em disco e a quantidade de logs que deve ser mantida são parâmetros que podem ser configurados. Por padrão, o limite de espaço livre em disco é de 204800 MB (200 GB) e a quantidade de logs a manter é de 100.000 (100 GB) para cópias passivas e de 10.000 (10 GB) para cópias ativas.

A habilitação do truncamento flexível e a configuração dos parâmetros de truncamento flexível são obtidas pela edição do Registro do Windows em cada membro do DAG. Há três valores do registro que podem ser configurados que são armazenados em HKLM\\Software\\Microsoft\\ExchangeServer\\v15\\BackupInformation. Os seguintes valores DWORD da chave BackupInformation não existem por padrão e devem ser criados manualmente. Os valores do Registro DWORD em BackupInformation são descritos na tabela abaixo:


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Valor de Registro</th>
<th>Descrição</th>
<th>Valor padrão</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>LooseTruncation_MinCopiesToProtect</p></td>
<td><p>Esta chave é usada para habilitar o truncamento flexível. Ela representa a quantidade de cópias passivas a proteger do truncamento flexível na cópia ativa de um banco de dados. A definição do valor desta chave como 0 desativa o truncamento flexível.</p></td>
<td><p>0</p></td>
</tr>
<tr class="even">
<td><p>LooseTruncation_MinDiskFreeSpaceThresholdInMB</p></td>
<td><p>Limite disponível de espaço em disco (em MB) para o acionamento de truncamento flexível. Se o espaço livre em disco ficar abaixo desse valor, o truncamento flexível será acionado.</p></td>
<td><p>Se este valor do registro não estiver configurado, o valor padrão usado pelo truncamento flexível será 200 GB.</p></td>
</tr>
<tr class="odd">
<td><p>LooseTruncation_MinLogsToProtect</p></td>
<td><p>A quantidade mínima de arquivos de log a ser mantida em cópias íntegras cujos logs estejam sendo truncados. Se esse valor do registro estiver configurado, então o valor configurado se aplicará às cópias ativas e passivas.</p></td>
<td><p>Se esse valor do registro não estiver configurado, então os valores padrão de 100.000 para cópias de banco de dados passivas e de 10.000 para cópias de banco de dados ativas serão usados.</p></td>
</tr>
</tbody>
</table>


Ao usar o valor do registro LooseTruncation\_MinLogsToProtect, observe que o comportamento é diferente para cópias de banco de dados ativas e passivas. Na cópia de banco de dados ativa, essa é a quantidade de logs adicionais mantida antes daqueles exigidos pelas cópias passivas protegidas e o intervalo exigido da cópia ativa. Em uma cópia de banco de dados passiva, é a quantidade de logs mantida desde o log disponível mais recente. Um décimo desse número também é usado para manter logs antes do intervalo exigido dessa cópia passiva. Os dois limites existem para garantir que as cópias de banco de dados atrasadas não ocupem muito espaço, uma vez que o intervalo exigido por elas é normalmente muito grande.

## Política de ativação do banco de dados

Há cenários nos quais você talvez queira criar uma cópia de banco de dados de caixa de correio e impedir o sistema de ativar automaticamente essa cópia em caso de falha, por exemplo:

  - Se você implantar uma ou mais cópias de banco de dados de caixa de correio em um datacenter alternativo ou em espera.

  - Se você configurar uma cópia de banco de dados com retardo para fins de recuperação.

  - Se você estiver realizando uma manutenção ou atualização de um servidor.

Em cada um dos cenários anteriores, você tem cópias de banco de dados que não deseja que o sistema ative automaticamente. Para impedir que o sistema ative automaticamente uma cópia de banco de dados de caixa de correio, é possível configurar a cópia a ser bloqueada (suspensa) para ativação. Isso permite ao sistema manter a atualidade do banco de dados ao longo de todo o envio de logs e repetição, mas impede o sistema de ativar automaticamente e usar a cópia. As cópias bloqueadas para ativação devem ser ativadas manualmente por um administrador. Você pode configurar a política de ativação do banco de dados para um servidor inteiro, usando o cmdlet [Set-MailboxServer](https://technet.microsoft.com/pt-br/library/aa998651\(v=exchg.150\)) ou uma cópia individual do banco de dados, usando o cmdlet [Set-MailboxDatabaseCopy](https://technet.microsoft.com/pt-br/library/dd298104\(v=exchg.150\)) para definir o parâmetro *DatabaseCopyAutoActivationPolicy* para Bloqueado.

Para mais informações sobre como configurar a diretiva de ativação do banco de dados, consulte [Configurar a política de ativação para uma cópia do banco de dados de caixa de correio](configure-activation-policy-for-a-mailbox-database-copy-exchange-2013-help.md).

## Efeito das movimentações de caixa de correio sobre a replicação contínua

Em um banco de dados de caixa de correio com uma taxa alta de geração de log, há uma chance maior de perda de dados se a replicação das cópias de banco de dados passivas não conseguir acompanhar a geração do log. Um cenário que pode incluir uma alta taxa de geração de log é a movimentação de caixa de correio. inclui uma API de Garantia dos Dados que é usada para serviços como o serviço de Replicação de Caixa de Correio do Microsoft Exchange (MRS) para verificar a integridade da arquitetura de cópia do banco de dados com base no valor do parâmetro *DataMoveReplicationConstraint* que foi definido pelo sistema ou um administrador. Especificamente, a API de Garantia de Dados pode ser usada para:

  - **Verificar a integridade de replicação**   Confirma que o número de pré-requisito de cópias de banco de dados está disponível.

  - **Verificar despejo de replicação**   Confirma que os arquivos de log exigidos foram reproduzido em relação ao número de pré-requisito de cópias de banco de dados.

Quando executada, a API retorna as seguintes informações de status para o aplicativo fazendo a chamada:

  - **Tentar novamente**   Significa que há erros transitórios que evitam que uma condição seja verificada em relação ao banco de dados.

  - **Satisfeito**   Significa que o banco de dados atende às condições necessárias ou o banco de dados não foi replicado.

  - **NotSatisfied**   Significa que o banco de dados não atende às condições exigidas. Além disso, as informações são fornecidas ao aplicativo fazendo a chamada em relação a por que a resposta **NotSatisfied** foi retornada.

O valor do parâmetro *DataMoveReplicationConstraint* para o banco de dados de caixa de correio determina quantas cópias do banco de dados devem ser avaliadas como parte da solicitação. O parâmetro *DataMoveReplicationConstraint* tem os seguintes valores possíveis:

  - `None`   Quando você cria um banco de dados de caixa de correio, esse valor é definido por padrão. Quando esse valor é definido, as condições da API de Garantia de Dados são ignoradas. Essa configuração deve ser usada apenas para bancos de dados de caixa de correio que não são replicados.

  - `SecondCopy`   Esse é o valor padrão quando você adiciona a segunda cópia de um banco de dados de caixa de correio. Quando esse valor é definido, pelo menos uma cópia de banco de dados passiva deve atender às condições de API de Garantia de Dados.

  - `SecondDatacenter`   Quando esse valor é definido, pelo menos uma cópia de banco de dados passiva em outro site do Active Directory deve atender às condições de API de Garantia de Dados.

  - `AllDatacenters`   Quando esse valor é definido, pelo menos uma cópia de banco de dados passiva em cada site do Active Directory deve atender às condições de API de Garantia de Dados.

  - `AllCopies`   Quando esse valor é definido, todas as cópias do banco de dados passivas devem atender às condições de API de Garantia de Dados.

**Verificar a Integridade da Replicação**

Quando a API de Garantia de Dados é executada para avaliar a integridade da infraestrutura da cópia de banco de dados, vários itens são avaliados.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Se o parâmetro <em>DataMoveReplicationConstraint</em> for definido como...</th>
<th>Então, para um determinado banco de dados...</th>
<th>Condições</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code>SecondCopy</code></p></td>
<td><p>Pelo menos uma cópia de banco de dados passiva para um banco de dados replicado deve atender às condições na coluna seguinte.</p></td>
<td><p>A cópia passiva do banco de dados deve:</p>
<ul>
<li><p>Estar íntegra.</p></li>
<li><p>Ter uma fila de repetição dentro de 10 minutos do tempo de retardo de repetição.</p></li>
<li><p>Ter um comprimento de fila de cópia de menos de 10 logs.</p></li>
<li><p>Ter um comprimento média de fila de cópia de menos de 10 logs. O comprimento médio da fila de cópia é computado com base no número de vezes que o aplicativo consultou o status do banco de dados.</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p><code>SecondDatacenter</code></p></td>
<td><p>Pelo menos uma cópia de banco de dados passiva em outro site do Active Directory deve atender às condições na coluna seguinte.</p></td>
<td></td>
</tr>
<tr class="odd">
<td><p><code>AllDatacenters</code></p></td>
<td><p>A cópia ativa deve estar montada, e uma cópia passiva em cada site do Active Directory deve atender às condições na coluna seguinte.</p></td>
<td></td>
</tr>
<tr class="even">
<td><p><code>AllCopies</code></p></td>
<td><p>A cópia ativa deve estar montada, e todas as cópias passivas Directory devem atender às condições na coluna seguinte.</p></td>
<td></td>
</tr>
</tbody>
</table>


**Verificar Despejo de Replicação**

A API de Garantia de Dados também pode ser usada para validar que um número de pré-requisito de cópias de banco de dados tenham repetido os logs de transação requeridos. Isso é verificado comparando-se o carimbo de data/hora da última repetição de log com o carimbo de confirmação do serviço chamador (na maioria dos casos, esse é o carimbo de data/hora do último arquivo de log que contém os dados necessários) adicionado de cinco segundos, para lidar com desvios, atrasos ou adiantamentos do relógio do sistema). Se o carimbo de data/hora da repetição for maior do que o carimbo de data/hora da confirmação, então o parâmetro *DataMoveReplicationConstraint* terá sido atendido. Se o carimbo de data/hora da repetição for menor do que o carimbo de data/hora da confirmação, então o parâmetro *DataMoveReplicationConstraint* não terá sido atendido.

Antes de mover grandes números de caixas de correio para ou de bancos de dados de replicação dentro de um DAG, recomendamos que você configure o parâmetro *DataMoveReplicationConstraint* em cada banco de dados de caixa de correio, de acordo como seguinte:


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Se você estiver implantando...</th>
<th>Defina DataMoveReplicationConstraint para...</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Bancos de dados de caixa de correio que não tem nenhuma cópia de banco de dados</p></td>
<td><p><code>None</code></p></td>
</tr>
<tr class="even">
<td><p>Um DAG dentro de um único site do Active Directory</p></td>
<td><p><code>SecondCopy</code></p></td>
</tr>
<tr class="odd">
<td><p>Um DAG em vários datacenters usando um site do Active Directory alongado</p></td>
<td><p><code>SecondCopy</code></p></td>
</tr>
<tr class="even">
<td><p>Um DAG que abrange dois sites do Active Directory, e você terá cópias do banco de dados de disponibilidade alta em cada site</p></td>
<td><p><code>SecondDatacenter</code></p></td>
</tr>
<tr class="odd">
<td><p>Um DAG que abrange dois sites do Active Directory e você terá somente cópias do banco de dados com retardo no segundo site</p></td>
<td><p><code>SecondCopy</code></p>
<p>Isso é porque a API de Garantia de Dados não irá garantir os dados sendo comprometidos até que o arquivo de log seja reproduzido dentro da cópia do bando de dados e, devido à natureza da cópia do banco de dados sofrendo o retardo, essa restrição fará a solicitação de movimentação falhar, a menos que o valor de ReplayLagTime da cópia do banco de dados com retardo seja menor que 30 minutos.</p></td>
</tr>
<tr class="even">
<td><p>Um DAG que abranja três ou mais sites do Active Directory, e cada site irá conter cópias do banco de dados de alta disponibilidade</p></td>
<td><p><code>AllDatacenters</code></p></td>
</tr>
</tbody>
</table>


## Balancear cópias de banco de dados

Devido à natureza inerente dos DAGs, como resultado das alternâncias e dos failovers de banco de dados, as cópias de banco de dados de caixa de correio ativas alterarão hosts várias vezes durante toda a existência de um DAG. Como resultado, os DAGs podem se tornar desbalanceados em termos de distribuição de cópia de banco de dados de caixa de correio ativa. A tabela a seguir mostra um exemplo de DAG que tem quatro bancos de dados com quatro cópias de cada banco de dados (para um total de 16 bancos de dados em cada servidor) com uma distribuição irregular de cópias de banco de dados ativas.

### DAG com distribuição de cópia ativa desbalanceada

<table style="width:100%;">
<colgroup>
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
</colgroup>
<thead>
<tr class="header">
<th>Servidor</th>
<th>Número de bancos de dados ativos</th>
<th>Número de bancos de dados passivos</th>
<th>Número de bancos de dados montados</th>
<th>Número de bancos de dados desmontados</th>
<th>Lista de contagem de preferência</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>EX1</p></td>
<td><p>5</p></td>
<td><p>11</p></td>
<td><p>5</p></td>
<td><p>0</p></td>
<td><p>4, 4, 3, 5</p></td>
</tr>
<tr class="even">
<td><p>EX2</p></td>
<td><p>1</p></td>
<td><p>15</p></td>
<td><p>1</p></td>
<td><p>0</p></td>
<td><p>1, 8, 6, 1</p></td>
</tr>
<tr class="odd">
<td><p>EX3</p></td>
<td><p>12</p></td>
<td><p>4</p></td>
<td><p>12</p></td>
<td><p>0</p></td>
<td><p>13, 2, 1, 0</p></td>
</tr>
<tr class="even">
<td><p>EX4</p></td>
<td><p>1</p></td>
<td><p>15</p></td>
<td><p>1</p></td>
<td><p>0</p></td>
<td><p>1, 1, 5, 9</p></td>
</tr>
</tbody>
</table>


No exemplo anterior, há quatro cópias de cada banco de dados e, por isso, somente quatro valores possíveis para preferência de ativação (1, 2, 3 ou 4). A coluna **Lista de contagem de preferência** mostra a contagem do número de bancos de dados com cada um desses valores. Por exemplo, em EX3, há 13 cópias de bancos de dados com uma preferência de ativação de 1, duas cópias com uma preferência de ativação de 2, uma cópia com uma preferência de ativação de 3 e nenhuma cópia com uma preferência de ativação de 4.

Como é possível ver, esse DAG não é balanceado em termos do número de bancos de dados ativos hospedados por todos os membros do DAG, o número de bancos de dados passivos hospedados pelos membros do DAG ou a contagem de preferência de ativação dos bancos de dados hospedados.

Você pode usar o script RedistributeActiveDatabases.ps1 para equilibrar as cópias de banco de dados de caixas de correio ativas em um DAG. Esse script move bancos de dados entre suas cópias em uma tentativa de equilibrar o número de bancos de dados montados em cada servidor do DAG. Se necessário, o script também tentará equilibrar os bancos de dados ativos entre sites.

O script fornece duas opções para balancear cópias de banco de dados ativas em um DAG:

  - **BalanceDbsByActivationPreference**   Quando essa opção é especificada, o script tenta mover bancos de dados para a sua cópia mais preferida (com base na preferência de ativação) sem relação com o site do Active Directory.

  - **BalanceDbsBySiteAndActivationPreference**   Quando essa opção é especificada, o script tenta mover bancos de dados ativos para a sua cópia mais preferida, enquanto tenta também balancear os bancos de dados ativos em cada site do Active Directory.

Após executar o script com a primeira opção, o DAG anterior desbalanceado se tornará balanceado, como mostrado na seguinte tabela.

### DAG com distribuição de cópia ativa balanceada

<table style="width:100%;">
<colgroup>
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
</colgroup>
<thead>
<tr class="header">
<th>Servidor</th>
<th>Número de bancos de dados ativos</th>
<th>Número de bancos de dados passivos</th>
<th>Número de bancos de dados montados</th>
<th>Número de bancos de dados desmontados</th>
<th>Lista de contagem de preferência</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>EX1</p></td>
<td><p>4</p></td>
<td><p>12</p></td>
<td><p>4</p></td>
<td><p>0</p></td>
<td><p>4, 4, 4, 4</p></td>
</tr>
<tr class="even">
<td><p>EX2</p></td>
<td><p>4</p></td>
<td><p>12</p></td>
<td><p>4</p></td>
<td><p>0</p></td>
<td><p>4, 4, 4, 4</p></td>
</tr>
<tr class="odd">
<td><p>EX3</p></td>
<td><p>4</p></td>
<td><p>12</p></td>
<td><p>4</p></td>
<td><p>0</p></td>
<td><p>4, 4, 4, 4</p></td>
</tr>
<tr class="even">
<td><p>EX4</p></td>
<td><p>4</p></td>
<td><p>12</p></td>
<td><p>4</p></td>
<td><p>0</p></td>
<td><p>4, 4, 4, 4</p></td>
</tr>
</tbody>
</table>


Como mostrado na tabela anterior, esse DAG está agora balanceado em termos do número de bancos de dados ativos e passivos em cada servidor e preferência de ativação nos servidores.

A tabela a seguir lista os parâmetros disponíveis para o script RedistributeActiveDatabases.ps1.

### Parâmetros do script RedistributeActiveDatabases.ps1

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Parâmetro</th>
<th>Descrição</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>DagName</em></p></td>
<td><p>Especifica o nome do DAG que você deseja rebalancear. Se esse parâmetro for omitido, o DAG do qual o servidor local é um membro será usado.</p></td>
</tr>
<tr class="even">
<td><p><em>BalanceDbsByActivationPreference</em></p></td>
<td><p>Especifica se o script deve mover bancos de dados para a sua cópia mais preferida sem relação com o site do Active Directory.</p></td>
</tr>
<tr class="odd">
<td><p><em>BalanceDbsBySiteAndActivationPreference</em></p></td>
<td><p>Especifica que o script deve tentar mover bancos de dados ativos para a sua cópia mais preferida, enquanto tenta também balancear os bancos de dados ativos em cada site do Active Directory.</p></td>
</tr>
<tr class="even">
<td><p><em>ShowFinalDatabaseDistribution</em></p></td>
<td><p>Especifica que um relatório da distribuição de banco de dados atual deve ser exibido após a conclusão da redistribuição.</p></td>
</tr>
<tr class="odd">
<td><p><em>AllowedDeviationFromMeanPercentage</em></p></td>
<td><p>Especifica a variação permitida de bancos de dados ativos entre sites, expressa em porcentagem. O padrão é 20%. Por exemplo, se houver 99 bancos de dados distribuídos por 3 sites, a distribuição ideal será 33 bancos de dados em cada site. Se o desvio permitido for de 20%, o script tentará equilibrar a distribuição dos bancos de dados de forma que cada site não possua mais do que 10% a mais ou a menos desse número. 10% de 33 são 3,3, que são arredondados para 4. Portanto, o script tentará ter entre 29 e 37 bancos de dados em cada site.</p></td>
</tr>
<tr class="even">
<td><p><em>ShowDatabaseCurrentActives</em></p></td>
<td><p>Especifica se o script produz um relatório para cada banco de dados, detalhando como o banco de dados foi movido e se ele está agora ativo em sua cópia mais preferida.</p></td>
</tr>
<tr class="odd">
<td><p><em>ShowDatabaseDistributionByServer</em></p></td>
<td><p>Especifica que o script produz um relatório para cada servidor mostrando sua distribuição de banco de dados.</p></td>
</tr>
<tr class="even">
<td><p><em>RunOnlyOnPAM</em></p></td>
<td><p>Especifica que o script seja executado somente no membro do DAG que atualmente tem a função PAM. O script verifica se está sendo executado a partir do PAM. Se não estiver sendo executado a partir do PAM, o script será finalizado.</p></td>
</tr>
<tr class="odd">
<td><p><em>LogEvents</em></p></td>
<td><p>Especifica se o script gera logs de um evento (MsExchangeRepl evento 4115) contendo um resumo das ações.</p></td>
</tr>
<tr class="even">
<td><p><em>IncludeNonReplicatedDatabases</em></p></td>
<td><p>Especifica que o script deve incluir bancos de dados não replicados (bancos de dados sem cópias) ao determinar como redistribuir os bancos de dados ativos. Embora bancos de dados não replicados não possam ser movidos, eles podem afetar a distribuição dos bancos de dados replicados.</p></td>
</tr>
<tr class="odd">
<td><p><em>Confirm</em></p></td>
<td><p>A opção Confirm pode ser usada para suprimir o prompt de confirmação que aparece por padrão quando esse script é executado. Para suprimir o prompt de confirmação, use a sintaxe -Confirm:$False. Você deve incluir dois-pontos ( : ) na sintaxe.</p></td>
</tr>
</tbody>
</table>


## Exemplos de RedistributeActiveDatabases.ps1

Esse exemplo mostra a distribuição de banco de dados para um DAG, incluindo a lista de contagem de preferência.

```powershell
RedistributeActiveDatabases.ps1 -DagName DAG1 -ShowDatabaseDistributionByServer | Format-Table
```

Esse exemplo redistribui e balanceia as cópias de banco de dados de caixa de correio ativas em um DAG usando a preferência de ativação sem solicitar uma entrada.

```powershell
RedistributeActiveDatabases.ps1 -DagName DAG1 -BalanceDbsByActivationPreference -Confirm:$False
```

Esse exemplo redistribui e balanceia as cópias de banco de dados de caixa de correio ativas em um DAG usando a preferência de ativação e produz um resumo da distribuição.

```powershell
    RedistributeActiveDatabases.ps1 -DagName DAG1 -BalanceDbsByActivationPreference -ShowFinalDatabaseDistribution
```

## Monitorar cópias de banco de dados

Uma cópia de banco de dados será a primeira defesa se ocorrer uma falha que afete a cópia ativa de um banco de dados. Por isso, é importante monitorar a integridade e o status das cópias de bancos de dados para garantir a disponibilidade, quando necessário. Você pode exibir várias informações, incluindo o comprimento de filas de cópia, comprimento da fila de repetição, informações de estado de status e índice de conteúdo, examinando os detalhes de uma cópia de banco de dados no EAC. Também é possível usar o cmdlet **Get-MailboxDatabaseCopyStatus** no Shell para exibir várias informações de status de uma cópia de banco de dados.

Para mais informações sobre o monitoramento de cópias de bancos de dados, consulte [Grupos de disponibilidade de banco de dados de monitoramento](monitoring-database-availability-groups-exchange-2013-help.md).

## Remover uma cópia de banco de dados

Uma cópia de banco de dados pode ser removida a qualquer momento, usando-se o EAC ou o cmdlet **Remove-MailboxDatabaseCopy** no Shell. Após remover uma cópia de banco de dados, você precisará excluir manualmente todos os arquivos de log de transações e de banco de dados do servidor do qual a cópia de banco de dados está sendo removida. Para obter etapas detalhadas sobre como remover uma cópia de um banco de dados, consulte [Remover uma cópia do banco de dados de caixa de correio](remove-a-mailbox-database-copy-exchange-2013-help.md).

## Alternâncias de banco de dados

O servidor de Caixa de Correio que hospeda a cópia ativa de um banco de dados é conhecido como o banco de dados de caixa de correio mestre. O processo de ativação de uma cópia de banco de dados passiva altera o banco de dados de caixa de correio mestre do banco de dados e transforma a cópia passiva na nova cópia ativa. Esse processo é chamado de alternância de banco de dados. Em uma alternância de banco de dados, a cópia ativa de um banco de dados é desmontada em um servidor de Caixa de Correio e uma cópia passiva desse banco de dados é montada como o novo banco de dados de caixa de correio ativo em outro servidor de Caixa de Correio. Ao realizar uma alternância, também é possível substituir a configuração da discagem automática de montagem do banco de dados no novo banco de dados de caixa de correio mestre.

É possível identificar rapidamente que servidor de Caixa de Correio é o banco de dados de caixa de correio mestre atual revisando-se a coluna da direita na guia **Cópias de Banco de Dados** no EAC. É possível realizar uma alternância usando-se o link **Ativar** no EAC ou o cmdlet **Move-ActiveMailboxDatabase** no Shell.

Há várias verificações internas que serão realizadas antes da ativação de uma cópia passiva:

  - O status da cópia de banco de dados é verificado. Se a cópia de banco de dados estiver em um estado com falha, a alternância será bloqueada. É possível substituir esse comportamento e ignorar a verificação da integridade usando-se o parâmetro *SkipHealthChecks* do cmdlet **Move-ActiveMailboxDatabase**. Esse parâmetro permite mover a cópia ativa para uma cópia de banco de dados em um estado com falha.

  - A cópia do banco de dados ativo é verificada para saber se ela é uma fonte de propagação para quaisquer cópias passivas do banco de dados. Se a cópia ativa estiver sendo usada como uma fonte para a propagação, a alternância é bloqueada. É possível substituir esse comportamento e ignorar a verificação da fonte de propagação, usando-se o parâmetro *SkipActiveCopyChecks* do cmdlet **Move-ActiveMailboxDatabase**. Esse parâmetro permite que você mova uma cópia ativa que está sendo usada como uma fonte de propagação. Usar esse parâmetro irá fazer com que a operação de propagação seja cancelada e considerada falha.

  - Os comprimentos da fila de cópia e da fila de repetição para a cópia de banco de dados são verificados para assegurar-se de que os valores estejam dentro dos critérios configurados. Além disso, a cópia de banco de dados é verificada para assegurar-se de que ela não esteja em uso como uma origem para propagação. Se os valores dos comprimentos das filas estiverem fora dos critérios configurados ou se o banco de dados estiver sendo usado como uma origem para propagação, a alternância será bloqueada. É possível substituir esse comportamento e ignorar essas verificações usando-se o parâmetro *SkipLagChecks* do cmdlet **Move-ActiveMailboxDatabase**. Esse parâmetro permite a ativação de uma cópia com filas de repetição e cópia fora dos critérios configurados.

  - O estado do catálogo de pesquisa (índice do conteúdo) da cópia de banco de dados é verificado. Se o catálogo de pesquisa não estiver atualizado, estiver em um estado não íntegro ou estiver corrompido, a alternância será bloqueada. É possível substituir esse comportamento e ignorar a verificação do catálogo de pesquisa, usando-se o parâmetro *SkipClientExperienceChecks* do cmdlet **Move-ActiveMailboxDatabase**. Esse parâmetro faz essa pesquisa ignorar a verificação da integridade do catálogo. Se o catálogo de pesquisa da cópia de banco de dados que você estiver ativando estiver em um estado não íntegro ou inutilizável e você usar esse parâmetro para ignorar a verificação da integridade do catálogo, você precisará rastrear ou propagar o catálogo de pesquisa novamente.

Ao realizar uma alternância de banco de dados, você também tem a opção de substituir as definições da discagem automática de montagem configuradas do servidor que hospeda a cópia de banco de dados passiva sendo ativada. O uso do parâmetro *MountDialOverride* do cmdlet **Move-ActiveMailboxDatabase** instrui o servidor de destino a substituir as configurações da discagem automática de montagem especificadas pelo parâmetro *MountDialOverride*.

Para instruções detalhadas sobre como realizar uma alternância de uma cópia de banco de dados, consulte [Ativar uma cópia do banco de dados de caixa de correio](activate-a-mailbox-database-copy-exchange-2013-help.md).

