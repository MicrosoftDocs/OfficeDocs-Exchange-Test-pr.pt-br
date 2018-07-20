---
title: 'Gerenciar movimentações de local: Exchange 2013 Help'
TOCTitle: Gerenciar movimentações de local
ms:assetid: 1691b658-f5af-49c6-9170-5c3cb66c7306
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/JJ150487(v=EXCHG.150)
ms:contentKeyID: 50485014
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Gerenciar movimentações de local

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2013-02-25_

Uma solicitação de movimentação é o processo de mover uma caixa de correio de um banco de dados de caixa de correio para outro. Uma solicitação de movimentação local é uma movimentação de caixa de correio que ocorre dentro de uma única floresta. No Microsoft Exchange Server 2013, as caixas de correio e as caixas de correio de arquivo morto pessoais podem residir em bancos de dados separados. Usando a funcionalidade de solicitação de movimentação, é possível mover a caixa de correio principal e o respectivo arquivo morto para o mesmo banco de dados ou para bancos de dados separados. Os procedimentos neste tópico irão ajudá-lo com movimentos de caixa de correio local.

Use os procedimentos a seguir para mover caixas de correio em sua organização no local. Estes procedimentos usam o Shell de Gerenciamento do Exchange e o Centro do Exchange (EAC).

Quando você usa a solicitação de movimentação para mover caixas de correio, as solicitações são processadas pelos dois serviços a seguir:

  - Serviço de Replicação de Caixa de Correio do Microsoft Exchange

  - Serviço de Replicação de Caixa de Correio do Microsoft Exchange

Para obter mais informações sobre o servidor de replicação e proxy de Caixa de Correio, consulte [Saiba mais sobre o Proxy MRS](https://technet.microsoft.com/pt-br/library/jj156451\(v=exchg.150\)).

Para obter mais informações sobre movimentos de caixas de correio, consulte [Movimentações de caixa de correio no Exchange 2013](mailbox-moves-in-exchange-2013-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para concluir cada procedimento: 20 minutos

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Permissões de movimentação e migração da caixa de correio" em [Permissões de destinatários](recipients-permissions-exchange-2013-help.md).

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>.



## O que você deseja fazer?

## Testar se uma caixa de correio está pronta para movimentação

Esse exemplo usa a opção *WhatIf* para testar se a caixa de correio de Tony Smith está pronta para ser movimentada para o novo banco de dados DB01 e se há algum erro com o comando. Ao usar a opção *WhatIf*, o sistema executa verificações na caixa de correio. Se a caixa de correio não estiver pronta para a movimentação, você receberá um erro.

    New-MoveRequest -Identity 'tony@alpineskihouse.com' -TargetDatabase DB01 -WhatIf

Para obter informações detalhadas sobre sintaxe e parâmetros, consulte [New-MigrationBatch](https://technet.microsoft.com/pt-br/library/jj219166\(v=exchg.150\)) e [New-MoveRequest](https://technet.microsoft.com/pt-br/library/dd351123\(v=exchg.150\)).

## Criar uma solicitação de movimentação local

## Usar o EAC para criar uma solicitação de movimentação local

Para criar uma solicitação de movimentação local, faça logon no EAC e execute as seguintes etapas:

1.  No EAC, navegue até **Destinatários** \> **Migração** e clique em **Adicionar**![Ícone Adicionar](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Ícone Adicionar").

2.  No assistente **Nova movimentação local de caixa de correio**, selecione o usuário que deseja mover, clique em **OK** e em **Avançar**.

3.  Na página **Configuração da movimentação**, especifique um nome para o novo lote. Selecione que opções deseja para a caixa de correio de arquivo e a localização do banco de dados da caixa de correio e clique em **Nova**.

## Usar o Shell para criar uma solicitação de movimentação local

Para ver um exemplo de como criar uma solicitação de movimentação local, consulte o Exemplo 2 em [New-MoveRequest](https://technet.microsoft.com/pt-br/library/dd351123\(v=exchg.150\)).

## Como saber se funcionou?

Para verificar se você concluiu com êxito a migração, faça o seguinte:

  - Na EAC, navegue até **Destinatários** \> **Migração**.

  - Verifique se a movimentação teve êxito no EAC clicando em **Status de todos os lotes**.

  - No Shell, execute o comando a seguir para recuperar as informações de movimentação de caixa de correio.
    
        Get-MigrationUserStatistics -Identity BatchName -Status | Format-List

Para mais informações, consulte [Get-MigrationUserStatistics](https://technet.microsoft.com/pt-br/library/jj218695\(v=exchg.150\)).

## Criar uma solicitação de movimento em lote

## Usar o EAC para criar uma solicitação de movimentação em lote

Faça logon no EAC e execute as seguintes etapas:

1.  No EAC, navegue até **Destinatários** \> **Migração** e clique em **Adicionar**![Ícone Adicionar](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Ícone Adicionar").

2.  No assistente **Nova movimentação local de caixa de correio**, selecione os usuários que deseja mover, clique em **OK** e em **Avançar**.

3.  Na página **Configuração da movimentação**, especifique um nome para o novo lote. Selecione que opções deseja para a caixa de correio de arquivo e a localização do banco de dados da caixa de correio e clique em **Nova**.


> [!WARNING]
> Não configure o Limite de itens incorretos para mais de 50 itens. Se o fizer, a movimentação poderá falhar. Se você quiser definir o Limite de item incorreto acima de 50 itens, será necessário usar o Shell de Gerenciamento do Exchange e definir o parâmetro –<EM>AcceptLargeDataLoss</EM> como true.



## Usar o Shell para criar uma solicitação de movimentação em lote

Este exemplo cria um lote de migração para uma movimentação local, em que as caixas de correio no arquivo .csv especificado são movidas para um banco de dados de caixa de correio diferente. Esse arquivo .csv contém uma única coluna, que inclui o endereço de e-mail de cada uma das caixas de correio que serão movidas. O cabeçalho desta coluna deve ser nomeado **EmailAddress**. O lote de migração neste exemplo deve ser iniciado manualmente usando o cmdlet **Start-MigrationBatch** ou o Centro de Administração do Exchange (EAC). De forma alternativa, você pode usar o parâmetro *AutoStart* para iniciar o lote de migração automaticamente.

```
    New-MigrationBatch -Local -Name LocalMove1 -CSVData ([System.IO.File]::ReadAllBytes("C:\Users\Administrator\Desktop\LocalMove1.csv")) -TargetDatabases MBXDB2 -TimeZone "Pacific Standard Time"
```
```
    Start-MigrationBatch -Identity LocalMove1
```

Para obter informações detalhadas sobre sintaxe e parâmetros, consulte [New-MigrationBatch](https://technet.microsoft.com/pt-br/library/jj219166\(v=exchg.150\)) e [Start-MigrationBatch](https://technet.microsoft.com/pt-br/library/jj219165\(v=exchg.150\)).

## Como saber se funcionou?

Para verificar se você concluiu com êxito a migração, faça o seguinte:

  - Verifique se a movimentação teve êxito no EAC clicando em **Status de todos os lotes**.

  - No Shell, execute o comando a seguir para recuperar as informações de movimentação de caixa de correio.
    
        Get-MigrationUserStatistics -Identity BatchName -Status | Format-List

Para mais informações, consulte [Get-MigrationUserStatistics](https://technet.microsoft.com/pt-br/library/jj218695\(v=exchg.150\)).

## Exibir lotes de migração

Para ver um exemplo de como usar o Shell para exibir um lote de migração, consulte o Exemplo 2 em [Get-MigrationBatch](https://technet.microsoft.com/pt-br/library/jj219164\(v=exchg.150\)).

## Mover somente a caixa de correio principal do usuário

## Usar o EAC para mover somente a caixa de correio principal de um usuário

1.  No EAC, navegue até **Destinatários** \> **Migração** e clique em **Adicionar**![Ícone Adicionar](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Ícone Adicionar").

2.  No assistente **Nova movimentação local de caixa de correio**, selecione o usuário cuja caixa de correio principal deseja mover, clique em **OK** e em **Avançar**.

3.  Na página **Configuração da movimentação**, especifique um nome para o novo lote. Selecione **Mover somente caixa de correio principal**, selecione quais opções deseja para a localização do banco de dados da caixa de correio e clique em **Nova**.

## Usar o Shell para mover somente a caixa de correio principal de um usuário

Este exemplo move somente a caixa de correio principal Tony Smith para DB01. O arquivamento não é movido.

    New-MoveRequest -Identity 'tony@alpineskihouse.com' -PrimaryOnly -TargetDatabase "DB01"

Para informações detalhadas de sintaxes e de parâmetros, consulte [New-MoveRequest](https://technet.microsoft.com/pt-br/library/dd351123\(v=exchg.150\)).

## Como saber se funcionou?

Para verificar se você concluiu com êxito a migração, faça o seguinte:

  - Na EAC, clique em **Status de todos os lotes**.

  - No Shell, execute o comando a seguir para recuperar as informações de movimentação de caixa de correio.
    
        Get-MigrationUserStatistics -Identity BatchName -Status | Format-List

Para mais informações, consulte [Get-MigrationUserStatistics](https://technet.microsoft.com/pt-br/library/jj218695\(v=exchg.150\)).

## Criar uma movimentação entre florestas usando um arquivo de lote .csv

Este exemplo configura o ponto de extremidade da migração e cria uma movimentação em lote entre florestas, da floresta de origem para a floresta de destino, usando um arquivo .csv.

```
New-MigrationEndpoint -Name Fabrikam -ExchangeRemote -Autodiscover -EmailAddress tonysmith@fabrikam.com -Credentials (Get-Credential fabrikam\tonysmith) 
```
```    
    $csvData=[System.IO.File]::ReadAllBytes("C:\Users\Administrator\Desktop\batch.csv")
    New-MigrationBatch -CSVData $csvData -Timezone "Pacific Standard Time" -Name FabrikamMerger -SourceEndpoint Fabrikam -TargetDeliveryDomain "mail.contoso.com"
```

Para obter mais informações sobre como preparar a sua floresta para movimentações entre florestas, consulte os seguintes tópicos:

  - [Preparar a caixas de correio para solicitações de movimentação entre florestas](prepare-mailboxes-for-cross-forest-move-requests-exchange-2013-help.md)

  - [Preparar a caixas de correio para movimentações entre florestas usando código de exemplo](prepare-mailboxes-for-cross-forest-moves-using-sample-code-exchange-2013-help.md)

  - [Prepare a caixas de correio para movimentações entre florestas usando o script de preparação-MoveRequest.ps1 no Shell](prepare-mailboxes-for-cross-forest-moves-using-the-prepare-moverequest-ps1-script-in-the-shell-exchange-2013-help.md)

Para obter informações detalhadas sobre sintaxe e parâmetros, consulte [New-MigrationBatch](https://technet.microsoft.com/pt-br/library/jj219166\(v=exchg.150\)) e [New-MoveRequest](https://technet.microsoft.com/pt-br/library/dd351123\(v=exchg.150\)).

## Como saber se funcionou?

Para verificar se você concluiu com êxito a migração, faça o seguinte:

  - No Shell, execute o comando a seguir para recuperar as informações de movimentação de caixa de correio.
    
        Get-MigrationUserStatistics -Identity BatchName -Status | Format-List

Para mais informações, consulte [Get-MigrationUserStatistics](https://technet.microsoft.com/pt-br/library/jj218695\(v=exchg.150\)).

## Mover somente uma caixa de correio de arquivo morto

## Usar o EAC para mover somente uma caixa de correio de arquivo

1.  No EAC, navegue até **Destinatários** \> **Migração** e clique em **Adicionar**![Ícone Adicionar](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Ícone Adicionar").

2.  No assistente **Nova movimentação local de caixa de correio**, selecione o usuário cuja caixa de correio de arquivo deseja mover, clique em **OK** e em **Avançar**.

3.  Na página **Configuração da movimentação**, especifique um nome para o novo lote. Selecione **Mover somente caixa de correio de arquivo**, selecione quais opções deseja para a localização do banco de dados da caixa de correio e clique em **Nova**.

## Usar o Shell para mover somente uma caixa de correio de arquivo

Este exemplo move somente a caixa de correio de arquivo Tony Smith para DB03. A caixa de correio principal não é movida.

    New-MoveRequest -Identity 'tony@alpineskihouse.com' -ArchiveOnly -ArchiveTargetDatabase "DB03"

Para obter informações detalhadas sobre sintaxe e parâmetros, consulte [New-MigrationBatch](https://technet.microsoft.com/pt-br/library/jj219166\(v=exchg.150\)) e [New-MoveRequest](https://technet.microsoft.com/pt-br/library/dd351123\(v=exchg.150\)).

## Como saber se funcionou?

Para verificar se você concluiu com êxito a migração, faça o seguinte:

  - No Shell, execute o comando a seguir para recuperar as informações de movimentação de caixa de correio.
    
        Get-MigrationUserStatistics -Identity BatchName -Status | Format-List

Para mais informações, consulte [Get-MigrationUserStatistics](https://technet.microsoft.com/pt-br/library/jj218695\(v=exchg.150\)).

## Mover a caixa de correio principal e a caixa de correio de arquivo morto de um usuário para bancos de dados separados

Este exemplo move a caixa de correio principal e a caixa de correio de arquivo morto de Ayla para bancos de dados separados. O banco de dados principal é movido para DB01 e o arquivo é movido para DB03.

    New-MoveRequest -Identity 'ayla@humongousinsurance.com' -TargetDatabase DB01 -ArchiveTargetDatabase -DB03

Para obter informações detalhadas sobre sintaxe e parâmetros, consulte [New-MigrationBatch](https://technet.microsoft.com/pt-br/library/jj219166\(v=exchg.150\)) e [New-MoveRequest](https://technet.microsoft.com/pt-br/library/dd351123\(v=exchg.150\)).

## Como saber se funcionou?

Para verificar se você concluiu com êxito a migração, faça o seguinte:

  - No Shell, execute o comando a seguir para recuperar as informações de movimentação de caixa de correio.
    
        Get-MigrationUserStatistics -Identity BatchName -Status | Format-List

Para mais informações, consulte [Get-MigrationUserStatistics](https://technet.microsoft.com/pt-br/library/jj218695\(v=exchg.150\)).

## Mover a caixa de correio principal de um usuário com um limite amplo para itens inválidos

## Usar o EAC para mover a caixa de correio principal de um usuário e permitir um limite amplo para itens inválidos

1.  No EAC, navegue até **Destinatários** \> **Migração** e clique em **Adicionar**![Ícone Adicionar](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Ícone Adicionar").

2.  No assistente **Nova movimentação local de caixa de correio**, selecione o usuário cuja caixa de correio principal deseja mover, clique em **OK** e em **Avançar**.

3.  Na página **Configuração da movimentação**, especifique um nome para o novo lote. Selecione **Mover somente caixa de correio principal** e selecione quais opções deseja para a localização do banco de dados da caixa de correio.

4.  Em **Mais opções**![Ícone Mais opções](images/JJ150550.5381819e-3b21-4873-8714-e9b956290b28(EXCHG.150).gif "Ícone Mais opções"), digite o limite para itens inválidos e clique em **OK**.

## Usar o Shell para mover a caixa de correio principal de um usuário e permitir um limite amplo para itens inválidos

Este exemplo move a caixa de correio principal de Lisa para o banco de dados de caixa de correio DB01 e define o limite para itens inválidos como `100`. Para definir um limite amplo para itens inválidos, é necessário usar o parâmetro *AcceptLargeDataLoss*.

    New-MoveRequest -Identity 'Lisa' -PrimaryOnly -TargetDatabase "DB01" -BadItemLimit 100 -AcceptLargeDataLoss

Para obter informações detalhadas sobre sintaxe e parâmetros, consulte [New-MigrationBatch](https://technet.microsoft.com/pt-br/library/jj219166\(v=exchg.150\)) e [New-MoveRequest](https://technet.microsoft.com/pt-br/library/dd351123\(v=exchg.150\)).

## Como saber se funcionou?

Para verificar se você concluiu com êxito a migração, faça o seguinte:

  - No Shell, execute o comando a seguir para recuperar as informações de movimentação de caixa de correio.
    
        Get-MigrationUserStatistics -Identity BatchName -Status | Format-List

Para mais informações, consulte [Get-MigrationUserStatistics](https://technet.microsoft.com/pt-br/library/jj218695\(v=exchg.150\)).

