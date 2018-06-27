---
title: 'Perguntas frequentes: Pastas públicas: Exchange 2013 Help'
TOCTitle: 'Perguntas frequentes: Pastas públicas'
ms:assetid: 1cdcdcb7-f11b-45ca-ad23-7c38f640208c
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/JJ552408(v=EXCHG.150)
ms:contentKeyID: 50485071
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Perguntas frequentes: Pastas públicas

 

_**Aplica-se a:**Exchange Server 2013_

_**Tópico modificado em:**2017-03-27_

Este tópico oferece a você uma lista de perguntas frequentes sobre pastas públicas do Exchange Server 2013. Para saber mais sobre pastas públicas, consulte [Pastas públicas](public-folders-exchange-2013-help.md).

Tem dúvidas sobre pastas públicas que não foram respondidas aqui? Envie um email para nós, em [Ex2013HelpFeedback@microsoft.com](mailto:ex2013helpfeedback@microsoft.com).

## Perguntas frequentes sobre migração de pasta pública

Esta seção contém perguntas frequentes sobre migração de pasta pública. Para obter mais informações, consulte [Usar a migração de lote para migrar pastas públicas para o Exchange 2013 de versões anteriores](use-batch-migration-to-migrate-public-folders-to-exchange-2013-from-previous-versions-exchange-2013-help.md), [Usar a migração de lotes para migrar as pastas públicas herdadas para o Office 365 e para o Exchange Online](use-batch-migration-to-migrate-legacy-public-folders-to-office-365-and-exchange-online-exchange-online-help.md)ou [Usar a migração de lote para migrar pastas públicas do Exchange 2013 para o Exchange Online](use-batch-migration-to-migrate-exchange-2013-public-folders-to-exchange-online-exchange-online-help.md).

## Quais são os cenários de migração suportados pasta pública?

A lista a seguir detalha as opções disponíveis para migração de pastas públicas para Exchange 2013 ou Exchange Online.

  - Pastas públicas do Exchange 2007 (RU15 SP3 ou posterior) podem ser migrados para Exchange 2013 ou Exchange Online.

  - Pastas públicas do Exchange 2010 (RU8 SP3 ou posterior) podem ser migrados com Exchange 2013 ou Exchange Online.

  - Pastas públicas do Exchange 2013 (CU15 ou posterior) podem ser migrados para o Exchange Online.

Há suporte para migrações no momento, somente para Exchange 2013 na mesma floresta do Active Directory. Migrações entre florestas serão suportadas no futuro.

## Depois da migração, o que acontece com a hierarquia, nos servidores de origem do Exchange 2010?

Durante o estágio de finalização da migração, é feito um bloqueio no servidor de origem, para deixá-lo inacessível para o usuário. Esse bloqueio permanece em vigor, para evitar que os usuários acessem as pastas públicas de origem após a finalização da migração. Embora seja possível liberar esse bloqueio, isso não é recomendado, pois as alterações não poderão ser sincronizadas para o Exchange 2013.

## Quando você migra pastas públicas, o que acontece com as regras de pasta pública existentes?

As regras de pasta pública são migradas junto com os dados e são mantidas como regras de pasta pública. Elas não são convertidas para regras de caixa de correio.

## O que acontece se as alterações de hierarquia forem executadas na origem, depois de o arquivo .csv inicial ser gerado? Como essas alterações refletem sobre o destino?

O arquivo .csv é usado para determinar o mapeamento entre a hierarquia de origem e a caixa de correio de destino. Ele contém somente as pastas de nível superior. As pastas filho sob as pastas de nível superior são migradas automaticamente. Então, se uma nova pasta filho for adicionada, ela será migrada durante o processo. Se uma nova pasta de nível superior for criada, ela será criada na caixa de correio que contém a cópia gravável da hierarquia.

## Durante a migração para pastas públicas do Exchange 2013, se houver uma janela de tempo longa entre a suspensão e a finalização, como posso forçar uma sincronização delta, de modo que os usuários possam acessar pastas públicas durante a sincronização final?

Você pode forçar que uma sincronização delta ocorra antes da inicialização, antes de bloquear a origem), executando o seguinte comando do Shell:

    Resume-PublicFolderMigrationRequest \PublicFolderMigration

Para informações detalhadas de sintaxes e de parâmetros, consulte [Resume-PublicFolderMigrationRequest](https://technet.microsoft.com/pt-br/library/jj218689\(v=exchg.150\)).

## Para a migração de uma hierarquia geodistribuída, como posso garantir que as pastas públicas sejam criadas no local mais próximo dos usuários de destino?

Como parte do processo de migração, um arquivo .csv é gerado (usando o script `publicfoldertomailboxmapgenerator.ps1`). Esse arquivo contém o mapeamento de pasta para caixa de correio para a nova hierarquia. Você poderá usar esse arquivo .csv para criar caixas de correio de pasta pública no local geográfico adequado e modificar o arquivo para colocar as pastas necessárias na caixa de correio apropriada, de modo que elas fiquem perto dos usuários de destino.

O arquivo .csv de entrada pode ser gerado executando-se o script `AggregatePFData.ps1`, localizado no diretório \<*Diretório de Instalação do Exchange*\>\\V15\\Scripts. Execute o script desta forma:

    .\AggregatePFData.ps1 | Select-Object -property @{Name="FolderName"; Expression = {$_.Identity}}, @{Name="FolderSize"; Expression = {$_.TotalItemSize.Value.ToBytes()}} | Export-CSV -Path <Path followed by the name of the CSV>

## As permissões de pasta pública existentes são migradas?

Sim, as permissões são migradas automaticamente no nível da pasta com os dados. Você não tem que executar essa etapa separadamente.

## As pastas públicas estão indo embora?

Não. As pastas públicas são ótimas para integração com o Outlook, cenários simples de compartilhamento e para permitir que várias pessoas acessem os mesmos dados.

## Quais clientes suportam pastas públicas?

Os usuários do Outlook 2007, Outlook 2010, Outlook 2013 e Outlook para Mac podem acessar pastas públicas. No entanto, usuários cujas caixas de correio estão nos servidores do Exchange 2013 não conseguirão se conectar às pastas públicas do Exchange 2007 ou do Exchange 2010 de clientes que usam os Serviços Web do Exchange (EWS), como Outlook para Mac. Recomendamos migrar pastas públicas herdadas do Exchange 2013 para manter o acesso desses usuários.

## Existem limitações nos clientes?

Há suporte para o Outlook Web App, mas com algumas limitações. Você pode adicionar e remover pastas públicas favoritas (se forem Post, email, calendário e contatos de pastas públicas) e executar operações de nível de item, como criando, editando, excluindo postagens e responder às postagens. Porém, você não pode fazer o seguinte no Outlook Web App:

  - Criar ou excluir pastas públicas

  - Arrastar e soltar conteúdo

  - Acessar pastas públicas localizadas em servidores que executam versões anteriores do Exchange


> [!TIP]
> Você só pode criar regras de pasta pública que contenham o elemento <STRONG>responder usando um modelo específico</STRONG> em pastas públicas habilitadas para email. É possível que pré-existente regras contendo <STRONG>responder usando um modelo específico</STRONG> continuarão a trabalhar em pastas públicas habilitadas para email, mas essas pastas que você não pode criar novas regras com esse elemento do modelo ou editar as regras existentes com esse elemento.



Em um cenário híbrido, Outlook na web e Outlook 2011 para Mac não são suportados para as pastas públicas entre locais. Os usuários devem estar no mesmo local em que as pastas públicas para acessá-los com o Outlook 2011 para Mac ou Outlook na web. Usuários de 2016 do Outlook para Mac podem acessar pastas públicas em um cenário híbrido, se os procedimentos em [procedimentos de implantação híbrida](https://technet.microsoft.com/en-us/library/jj200788\(v=exchg.150\).aspx) são seguidos, e a atualização de abril de 2016 para 2016 do Outlook para Mac foi instalada em todos os clientes.

## Como posso armazenar uma hierarquia muito grande em uma caixa de correio de pasta pública?

Para obter mais informações sobre limites de armazenamento de pastas públicas, consulte [Limites para pastas públicas](limits-for-public-folders-exchange-2013-help.md).

## Como posso ver a caixa de correio de pasta pública de hierarquia?

Execute o seguinte comando:

    Get-OrganizationConfig | Format-List RootPublicFolderMailbox

Para informações detalhadas sobre sintaxe e parâmetro, consulte [Get-OrganizationConfig](https://technet.microsoft.com/pt-br/library/aa997571\(v=exchg.150\)).

## Como posso criar caixas de correio de conteúdo para pastas públicas, usando cmdlets do Shell de Gerenciamento do Exchange?

Execute o comando a seguir, para criar a primeira caixa de correio de pasta pública de hierarquia mestre e as caixas de correio de hierarquia secundárias.

    New-Mailbox -PublicFolder -Name <name of public folder>

Para saber mais detalhes, consulte [Criar uma pasta pública](create-a-public-folder-exchange-2013-help.md).

## Nas versões anteriores do Exchange, para cada banco de dados de caixa de correio, havia uma opção para especificar o banco de dados de pasta pública. Como isso irá funcionar no Exchange 2013?

O Exchange 2013 não tem nenhuma configuração no nível do banco de dados. Ele tem, no nível da caixa de correio, a capacidade de especificar a caixa de correio da pasta pública, mas, por padrão, calcula automaticamente a caixa de correio da hierarquia por usuário.

## Como estão sendo usadas ferramentas métricas de pasta pública no Exchange 2013?

No Exchange 2013, você pode usar os cmdlets [Get-PublicFolderStatistics](https://technet.microsoft.com/pt-br/library/aa998663\(v=exchg.150\)) e [Get-PublicFolderItemStatistics](https://technet.microsoft.com/pt-br/library/ee332344\(v=exchg.150\)) para obter dados de métricas de pasta pública. Essa é a mesma solução que tínhamos no Exchange 2010, de forma que nada mudou, aqui. As pastas públicas não exigem complementos de relatório adicionais.

## As pastas públicas podem diferenciar entre acesso interno e acesso de terceiros às pastas públicas?

No Exchange 2013, as permissões de pasta pública são gerenciadas por meio do Controle de Acesso Baseado em Função (RBAC). As listas de controle de acesso (ACL) não são usadas no Exchange 2013. Utilize os cmdlets [Get-PublicFolderStatistics](https://technet.microsoft.com/pt-br/library/aa998663\(v=exchg.150\)) e [Get-PublicFolderItemStatistics](https://technet.microsoft.com/pt-br/library/ee332344\(v=exchg.150\)) para acompanhar as contas que estão realizando tarefas administrativas e, depois, faça a auditoria do acesso correspondente. Para saber mais sobre RBAC, consulte [Controle de acesso baseado em função de compreensão](understanding-role-based-access-control-exchange-2013-help.md).

## O log de auditoria de caixa de correio funciona com as pastas públicas?

Não. Não neste momento.

## Quais são os limites das pastas públicas? Quais são as recomendações?

Para obter mais informações sobre limites de pastas públicas, consulte [Limites para pastas públicas](limits-for-public-folders-exchange-2013-help.md).

## Quais são as recomendações para dividir as caixas de correio de pasta pública? Eles devem ficar no mesmo banco de dados?

Nas versões anteriores do Exchange, você podia dividir as pastas públicas nos bancos de dados da pasta pública. Você pode decidir se deseja dividir o conteúdo de uma caixa de correio de pasta pública para uma caixa de correio no mesmo banco de dados de caixa de correio ou em um banco de dados diferente. Normalmente, recomenda-se que uma divisão esteja em um banco de dados separado, porque você deseja balancear armazenamento e E/S.

## Você pode definir as políticas de retenção em pastas públicas?

Assim como nas versões anteriores do Exchange, você pode definir limites de retenção em itens. Para obter detalhes, consulte [Limites para pastas públicas](limits-for-public-folders-exchange-2013-help.md).

## É possível especificar quais usuários podem usar uma caixa de correio de pasta pública específica?

No Exchange 2007 e no Exchange 2010, era possível especificar quais usuários tinham acesso às pastas públicas específicas. No Exchange 2013, você pode definir a caixa de correio de pasta pública por usuário. Para fazer isso, execute o cmdlet [Set-Mailbox](https://technet.microsoft.com/pt-br/library/bb123981\(v=exchg.150\)) com o parâmetro *DefaultPublicFolderMailbox*.

    Set-Mailbox -Identity kweku@contoso.com -DefaultPublicFolderMailbox "PF_Administration"

## Se a hierarquia mestre cair, qual será o impacto no usuário?

Se a caixa de correio de pasta pública da hierarquia mestre cair, os usuários poderão visualizar, mas não gravar nas pastas públicas. Para ajudar a evitar que a hierarquia caia, recomendamos que suas pastas públicas sejam incluídas em um grupo de disponibilidade de banco de dados (DAG). Para saber mais sobre DAGs, consulte [Grupos de Disponibilidade do Banco de Dados (DAGs)](database-availability-groups-dags-exchange-2013-help.md).

## É possível alterar qual caixa de correio de pasta pública é a caixa de correio da hierarquia mestre?

Não. Se você tentar alterar a caixa de correio da hierarquia mestre, você receberá um erro.

## As pastas públicas possuem recursos de pesquisa de texto completo?

Sim, a pesquisa de texto completo está disponível para pastas públicas no Exchange 2013. Você não pode, porém, pesquisar em várias pastas públicas.

