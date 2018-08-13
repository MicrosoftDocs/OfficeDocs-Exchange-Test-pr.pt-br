---
title: 'Pastas públicas: Exchange 2013 Help'
TOCTitle: Pastas públicas
ms:assetid: 94c4fb69-9234-4b34-8c1c-da2a0a11da65
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/JJ150538(v=EXCHG.150)
ms:contentKeyID: 50486223
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Pastas públicas

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2017-03-27_

As pastas públicas são feitas para acesso compartilhado e oferecem um jeito fácil e eficaz de coletar, organizar e compartilhar informações com outros pessoas no seu grupo de trabalho ou organização. Pastas públicas ajudam a organizar o conteúdo em uma hierarquia profunda fácil de navegar. Os usuários verão a hierarquia completa no Outlook, o que facilita a busca do conteúdo no qual eles estão interessados.


> [!TIP]
> Pastas públicas estão disponíveis nos seguintes clientes do Outlook: Outlook Web App para Exchange 2013, Outlook 2007, Outlook 2010, Outlook 2013 e Outlook for Mac.



Pastas públicas também podem ser usadas como um método de arquivamento para grupos de distribuição. Quando você habilitar uma pasta pública para email e adicioná-la como membro do grupo de distribuição, os emails enviados ao grupo serão automaticamente adicionados à pasta pública para referência futura.


> [!TIP]
> É necessário usar o Outlook 2007 ou posterior para acessar pastas públicas em servidores Exchange 2013.



As pastas públicas não foram projetadas para as seguintes finalidades:

  - **Arquivamento de dados**. Usuários com limites de caixa de correio muitas vezes usam pastas públicas em vez de caixas de correio para arquivar dados. Essa prática não é recomendada, pois afeta o armazenamento em pastas públicas e prejudica a meta de limites de caixa de correio. Em vez disso, recomendamos o uso do [Arquivamento In-loco do Exchange 2013](in-place-archiving-in-exchange-2013-exchange-2013-help.md) como solução de arquivamento.

  - **Colaboração e compartilhamento de documentos** Pastas públicas não oferecem Versionamento ou outro documento recursos de gerenciamento, controlada funcionalidade de check-in e check-out e notificações automáticas das alterações de conteúdo. Em vez disso, recomendamos que você use o [SharePoint](https://go.microsoft.com/fwlink/?linkid=282474) como sua solução de compartilhamento de documentação.

Para saber mais sobre pastas públicas e outros métodos de colaboração no Exchange 2013, consulte [Colaboração](collaboration-exchange-2013-help.md).

Para navegar por algumas perguntas frequentes sobre pastas públicas no Exchange 2013, consulte [Perguntas frequentes: Pastas públicas](faq-public-folders-exchange-2013-help.md).

Para obter mais informações sobre os limites e cotas de pastas públicas, consulte [Limites para pastas públicas](limits-for-public-folders-exchange-2013-help.md).

Para obter uma lista de tarefas de gerenciamento de pasta pública, consulte [Procedimentos de pasta pública](public-folder-procedures-exchange-2013-help.md).

Procurando a versão do Exchange Online deste tópico? Consulte [Pastas públicas no Office 365 e Exchange Online](https://technet.microsoft.com/pt-br/library/jj200758\(v=exchg.150\)).

**Sumário**

Public folder architecture

Migrar pastas públicas

Public folder moves

Public folder quotas

Disaster recovery

## Arquitetura de pastas públicas

No Exchange 2013, as pastas públicas foram reformuladas usando a infraestrutura de caixas de correio, a fim de tirar proveito das tecnologias existentes de armazenamento e alta disponibilidade do banco de dados de caixa de correio. A arquitetura de pastas públicas usa caixas de correio especialmente designadas para armazenar o conteúdo e a hierarquia de pastas públicas. Isso também significa que não há mais um banco de dados de pasta pública. A alta disponibilidade das caixas de correio de pasta pública é fornecida por um grupo de disponibilidade de banco de dados (DAG). Para saber mais sobre DAGs, consulte [Grupos de Disponibilidade do Banco de Dados (DAGs)](database-availability-groups-dags-exchange-2013-help.md).

Os principais componentes da arquitetura de pastas públicas são as caixas de correio, que podem residir em um ou mais bancos de dados de caixa de correio.

## Caixas de correio de pastas públicas

Há dois tipos de caixas de correio de pastas públicas: a *caixa de correio de hierarquia primária* e as *caixas de correio de hierarquia secundária*. Ambos os tipos de caixas de correio podem ter conteúdo:

  - **Caixa de correio de hierarquia primária** A caixa de correio de hierarquia primária é a cópia gravável única da hierarquia de pastas públicas. A hierarquia de pastas públicas é copiada para todas as outras caixas de correio de pastas públicas, mas estas serão cópias somente leitura.

  - **Caixas de correio de hierarquia secundária** As caixas de correio de hierarquia secundária também têm o conteúdo de pastas públicas e uma cópia somente leitura da hierarquia de pastas públicas.


> [!TIP]
> Não há suporte a políticas de retenção para caixas de correio de pastas públicas.



Há duas maneiras de gerenciar caixas de correio de pastas públicas:

  - No EAC (Centro de Administração do Exchange), navegue até **Pastas públicas** \> **Caixas de correio de pastas públicas**.

  - No Shell de Gerenciamento do Exchange, use o conjunto de cmdlets **\*-Mailbox**. Os seguintes parâmetros foram adicionados ao cmdlet [New-Mailbox](https://technet.microsoft.com/pt-br/library/aa997663\(v=exchg.150\)) para dar suporte a caixas de correio de pasta pública:
    
      - *PublicFolder*   Este parâmetro é usado com o cmdlet **New-Mailbox** para criar uma caixa de correio de pasta pública. Quando você cria uma caixa de correio de pasta pública, uma nova caixa de correio é criada com o tipo `PublicFolder`. Para obter mais informações, consulte [Criar uma caixa de correio de pasta pública](create-a-public-folder-mailbox-exchange-2013-help.md).
    
      - *HoldForMigration*   Este parâmetro é usado apenas se você está migrando pastas públicas de uma versão anterior para o Exchange 2013. Para obter mais informações, consulte Migrate Public folders from previous versions, posteriormente neste tópico.
    
      - *IsHierarchyReady*   Este parâmetro indica se a caixa de correio de pasta pública está pronta para atender à hierarquia de pasta pública para os usuários. Ela será definida como `$True` somente depois que toda a hierarquia tiver sido sincronizada com a caixa de correio de pasta pública. Se o parâmetro estiver definido como $False, os usuários não o usarão para acessar a hierarquia. Entretanto, se você definir a propriedade *DefaultPublicFolderMailbox* em uma caixa de correio de usuário para uma caixa de correio de pasta pública específica, o usuário ainda acessará a caixa de correio de pasta pública especificada, mesmo se o parâmetro *IsHierarchyReady* estiver definido como `$False`.
    
      - *IsExcludedFromServingHierarchy*   Este parâmetro evita que os usuários acessem a hierarquia de pasta pública na caixa de correio de pasta pública especificada. Para fins de balanceamento de carga, os usuários são distribuídos igualmente entre caixas de correio de pastas públicas, por padrão. Quando esse parâmetro é definido em uma caixa de correio de pasta pública, essa caixa de correio não é incluída nesse balanceamento de carga automático e não será acessada pelos usuários para recuperar a hierarquia de pasta pública. Entretanto, se você definir a propriedade *DefaultPublicFolderMailbox* em uma caixa de correio de usuário para uma caixa de correio de pasta pública específica, o usuário ainda acessará a caixa de correio de pasta pública especificada, mesmo se o parâmetro *IsExcludedFromServingHierarchy* estiver definido para essa caixa de correio de pasta pública.

Uma caixa de correio de hierarquia secundária só fornecerá informações de hierarquia de pasta pública para os usuários se essa condição estiver explicitamente especificada nas caixas de correio dos usuários por meio da propriedade *DefaultPublicFolderMailbox* ou se as seguintes condições forem atendidas:

  - A propriedade *IsHierarchyReady* na caixa de correio de pasta pública estiver definida como `$True`.

  - A propriedade *IsExcludedFromServingHierarchy* na caixa de correio de pasta pública estiver definida como `$False`.

## Hierarquia de pastas públicas

A hierarquia de pastas públicas contém propriedades das pastas e informações organizacionais, incluindo a estrutura de árvore. Cada caixa de correio de pastas públicas principal contém uma cópia da hierarquia de pastas públicas. Há apenas uma cópia gravável da hierarquia, que está na caixa de correio de pastas públicas primária. Para uma pasta específica, as informações hierárquicas são usadas para identificar o seguinte:

  - Permissões na pasta

  - A posição da pasta na árvore de pastas públicas, incluindo suas pastas pai e filho


> [!TIP]
> A hierarquia não armazena informações sobre endereços de email para pastas públicas habilitadas para email. Os endereços de email são armazenados no objeto de diretório no Active Directory.



## Sincronização de hierarquia

O processo de sincronização da hierarquia de pastas públicas utiliza a ICS (Sincronização Incremental de Alterações), que fornece um mecanismo de monitoramento e sincronização das alterações em um conteúdo ou em uma hierarquia de repositório do Exchange. As alterações incluem a criação, a modificação e a exclusão de pastas e mensagens. Quando os usuários estão conectados e usando caixas de correio de conteúdo, a sincronização ocorre a cada 15 minutos. Se nenhum usuário estiver conectado à caixa de correio de conteúdo, a sincronização será acionada com menos frequência (a cada 24 horas). Se uma operação de gravação, como a criação de uma pasta, for realizada na hierarquia primária, a sincronização será imediatamente disparada (de forma síncrona) para a caixa de correio de conteúdo.


> [!IMPORTANT]
> Como há apenas uma cópia gravável da hierarquia, a criação de pastas é encaminhada por proxy para a caixa de correio de hierarquia pela caixa de correio de conteúdo à qual os usuários estão conectados.



Em uma organização de grande porte, quando você cria uma nova caixa de correio de pasta pública, a hierarquia deve sincronizar com essa pasta pública antes de os usuários poderem se conectar a ela. Caso contrário, os usuários poderão ver uma estrutura de pasta pública incompleta ao se conectar com o Outlook. Para dar tempo para que essa sincronização ocorra sem que os usuários fiquem tentando se conectar à nova caixa de correio de pasta pública, defina o parâmetro *IsExcludedFromServingHierarchy* no cmdlet **New-Mailbox** ao criar a caixa de correio de pasta pública. Esse parâmetro evita que os usuários se conectem à caixa de correio de pasta pública recém-criada. Quando a sincronização estiver concluída, execute o cmdlet [Set-Mailbox](https://technet.microsoft.com/pt-br/library/bb123981\(v=exchg.150\)) com o parâmetro *IsExcludedFromServingHierarchy* definido como `false`, indicando que a caixa de correio de pasta pública está pronta para conexão. Você também pode usar o cmdlet [Get-PublicFolderMailboxDiagnostics](https://technet.microsoft.com/pt-br/library/jj218720\(v=exchg.150\)) para exibir o status da sincronização pelas propriedades *SyncInfo* e *AssistantInfo*.

Para obter mais informações, consulte [Criar uma pasta pública](create-a-public-folder-exchange-2013-help.md).

## Conteúdo de pastas públicas

O conteúdo de pastas públicas pode incluir mensagens de email, postagens, documentos e eForms. O conteúdo é armazenado na caixa de correio de pastas públicas, mas não é replicado em várias caixas de correio de pastas públicas. Todos os usuários acessam a mesma caixa de correio de pastas públicas para o mesmo conjunto de conteúdo. Embora uma pesquisa de texto completo de conteúdo de pastas públicas esteja disponível, o conteúdo de pasta pública não é pesquisável em pastas públicas, e o conteúdo não é indexado pela Pesquisa do Exchange.


> [!TIP]
> Há suporte para o Outlook Web App, mas com limitações. Você pode adicionar e remover pastas públicas favoritas e realizar operações em nível de item, como criar, editar, excluir postagens e responder a postagens. No entanto, você não pode criar nem excluir pastas públicas do Outlook Web App. Além disso, apenas as pastas públicas Email, Postagem, Calendário e Contatos podem ser adicionadas à lista de favoritos no Outlook Web App.



## Migrar pastas públicas

Você pode migrar suas pastas públicas a partir de versão anteriores do Exchange Server para o Exchange 2013 ou versões anteriores do Exchange Server para o Exchange Online. Também é possível migrar suas pastas públicas do Exchange 2013 para o Exchange Online.

Se você já tiver pastas públicas do Exchange 2010 SP3 ou Exchange 2007 SP3 RU10 em sua organização antes de instalar o Exchange 2013, você deve migrar as pastas públicas para o Exchange 2013. Para fazer isso, use os cmdlets de **PublicFolderMigrationRequst** . Para obter mais informações, consulte [Usar a migração de lote para migrar pastas públicas para o Exchange 2013 de versões anteriores](use-batch-migration-to-migrate-public-folders-to-exchange-2013-from-previous-versions-exchange-2013-help.md). Se sua organização está se movendo para o Exchange Online, você pode migrar suas pastas públicas para a nuvem e atualizá-los ao mesmo tempo. Para obter detalhes, consulte [Usar a migração de lotes para migrar as pastas públicas herdadas para o Office 365 e para o Exchange Online](use-batch-migration-to-migrate-legacy-public-folders-to-office-365-and-exchange-online-exchange-online-help.md) e [Usar a migração de lote para migrar pastas públicas do Exchange 2013 para o Exchange Online](use-batch-migration-to-migrate-exchange-2013-public-folders-to-exchange-online-exchange-online-help.md).

Devido às mudanças na maneira como as pastas públicas são armazenadas, as caixas de correio do Exchange herdadas não conseguem acessar a hierarquia de pasta pública em servidores Exchange 2013 ou no Exchange Online. Porém, caixas de correio de usuário em servidores Exchange 2013 ou no Exchange Online podem se conectar a pastas públicas herdadas. Pastas públicas do Exchange 2013 e pastas públicas herdadas não podem existir na sua organização do Exchange simultaneamente. Isso significa efetivamente que não há coexistência entre versões. A migração de pastas públicas para o Exchange Server 2013 ou Exchange Online é atualmente um processo de transferência realizado uma única vez.

Por esse motivo, recomenda-se que antes de migrar suas pastas públicas, você deve primeiro migrar suas caixas de correio herdadas com Exchange 2013 ou Exchange Online. Para obter mais informações sobre como migrar caixas de correio, consulte [Movimentações de caixa de correio no Exchange 2013](mailbox-moves-in-exchange-2013-exchange-2013-help.md), [executar uma migração de substituição de email para o Office 365](https://go.microsoft.com/fwlink/p/?linkid=536689)e [executar uma migração em estágios de email para o Office 365](https://go.microsoft.com/fwlink/p/?linkid=536687).

## Movimentações de pastas públicas

Você pode mover pastas públicas para outra caixa de correio de pasta pública e também mover caixas de correio de pasta pública para diferentes bancos de dados de caixa de correio. Para mover pastas públicas para diferentes caixas de correio de pasta pública, use o conjunto de cmdlets **PublicFolderMoveRequest**. Subpastas sob a pasta pública que estiver sendo movida não serão movidas por padrão. Se desejar mover uma ramificação das pastas públicas, use o script `Move-PublicFolderBranch.ps1` instalado por padrão com o Exchange 2013. Para obter mais informações, consulte [Mover uma pasta pública para uma caixa de correio de pasta pública diferentes](move-a-public-folder-to-a-different-public-folder-mailbox-exchange-2013-help.md).

Além de mover pastas públicas, você pode mover caixas de correio de pasta pública para diferentes bancos de dados de caixa de correio, usando o conjunto de cmdlets **MoveRequest**. Esse é o mesmo conjunto de cmdlets usados para mover caixas de correio normais. Para obter mais informações, consulte [Mover uma caixa de correio de pasta pública para um banco de dados de caixa de correio diferente](move-a-public-folder-mailbox-to-a-different-mailbox-database-exchange-2013-help.md).

Os cmdlets **PublicFolderMoveRequest** e **MoveRequest** usam o Serviço de Replicação de Caixa de Correio para mover pastas públicas de forma assíncrona. Isso significa que o cmdlet não faz o trabalho em si e, durante a maior parte da movimentação, a pasta pública e as caixas de correio de pasta pública ainda estarão disponíveis aos usuários. Como o Serviço de Replicação de Caixa de Correio executa movimentações de caixa de correio, solicitações de importação e exportação, e solicitações de movimentação de pasta pública, é importante considerar aspectos como limitação e gerenciamento de carga de trabalho.

## Cotas de pasta pública

Quando são criadas, as caixas de correio de pasta pública herdam automaticamente os limites de tamanho dos padrões do banco de dados de caixa de correio. Consequentemente, para avaliar com precisão o status da cota de armazenamento atual ao usar o cmdlet [Get-Mailbox](https://technet.microsoft.com/pt-br/library/bb123685\(v=exchg.150\)), é necessário examinar na propriedade *UseDatabaseQuotaDefaults*, além das propriedades *ProhibitSendQuota*, *ProhibitSendReceiveQuota* e *IssueWarningQuota*. Se a propriedade *UseDatabaseQuotaDefaults* estiver definida como `true`, as configurações por caixa de correio serão ignoradas e os limites do banco de dados de caixa de correio serão usados. Se essa propriedade estiver definida como `true` e as propriedades *ProhibitSendQuota*, *ProhibitSendReceiveQuota* e *IssueWarningQuota* estiverem definidas como `unlimited`, a caixa de correio não terá realmente tamanho ilimitado. Em vez disso, é necessário usar o cmdlet **Get-MailboxDatabase** e examinar os limites de armazenamento do banco de dados de caixa de correio para verificar quais são os limites para a caixa de correio. Se a propriedade *UseDatabaseQuotaDefaults* estiver definida como `false`, as configurações por caixa de correio serão usadas. No Exchange 2013, os limites de cota do banco de dados de caixa de correio padrão são os seguintes:

  - *Cota de aviso de problema*: 1,9 GB

  - *Cota de proibição de envio*: 2 GB

  - *Cota de proibição de recebimento*: 2,3 GB

Para encontrar as cotas do banco de dados da caixa de correio, execute o cmdlet [Get-MailboxDatabase](https://technet.microsoft.com/pt-br/library/bb124924\(v=exchg.150\)).

Para definir as cotas em uma caixa de correio de pasta pública, use o cmdlet [Set-OrganizationConfig](https://technet.microsoft.com/pt-br/library/aa997443\(v=exchg.150\)).

## Recuperação de desastres

As pastas públicas do Exchange 2013 são criadas sobre a infraestrutura de caixa de correio e usam os mesmos mecanismos para disponibilidade e redundância. Cada caixa de correio de pasta pública pode ter várias cópias redundantes com failover automático, assim como as caixas de correio normais. Para saber mais, consulte [Alta disponibilidade e resiliência de site](high-availability-and-site-resilience-exchange-2013-help.md).

Além do cenário geral de recuperação de desastre, você também pode restaurar pastas públicas nas seguintes situações:

  - **Restauração de pasta pública com exclusão reversível**   A pasta pública foi excluída, mas ainda está dentro do período de retenção.

  - **Restauração de caixa de correio de pasta pública com exclusão reversível**   A caixa de correio de pasta pública foi excluída e ainda está dentro do período de retenção de caixa de correio.

  - **Restauração de caixa de correio de pasta pública a partir de um banco de dados de recuperação**   Você poderá recuperar uma caixa de correio de pasta pública individual do backup quando o período de retenção de caixa de correio excluída tiver terminado. Em seguida, extraia dados da caixa de correio restaurada e copie-os para uma pasta de destino ou mescle-os com outra caixa de correio.

Em todas essas situações, a pasta pública ou a caixa de correio de pasta pública pode ser recuperada usando os cmdlets **MailboxRestoreRequest**.

Para obter mais informações, consulte [Restaurar pastas públicas e caixas de correio de pasta pública de movimentações com falha](restore-public-folders-and-public-folder-mailboxes-from-failed-moves-exchange-2013-help.md).

