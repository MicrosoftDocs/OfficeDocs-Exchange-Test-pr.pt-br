---
title: 'Propagar novamente o catálogo de pesquisa: Exchange 2013 Help'
TOCTitle: Propagar novamente o catálogo de pesquisa
ms:assetid: 9d873bd4-0422-4975-b5e2-82a347479115
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Ee633475(v=EXCHG.150)
ms:contentKeyID: 52058862
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Propagar novamente o catálogo de pesquisa

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2015-03-09_

Se o catálogo do índice de conteúdo de uma cópia de banco de dados de caixa de correio for corrompido, talvez seja necessário propagar novamente o catálogo. Os índices de conteúdo corrompidos são indicados no log de eventos do aplicativo pelo evento a seguir.


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>ID do Evento</th>
<th>Nível</th>
<th>Origem</th>
<th>Detalhes</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>123</p></td>
<td><p>Erro</p></td>
<td><p>ExchangeStoreDB</p></td>
<td><p>Em &lt;<em>carimbo de data/hora</em>&gt;, a cópia de &lt;<em>identidade</em>&gt; do Banco de Dados de Repositório de Informações do Microsoft Exchange neste servidor apresentou um catálogo de pesquisa corrompido. Consulte o log de eventos no servidor em busca de outros eventos &quot;ExchangeStoreDb&quot; e &quot;Indexador de Pesquisa do MSExchange&quot; para obter informações mais específicas sobre a falha. É recomendável realizar uma nova propagação do catálogo usando a tarefa 'Update-MailboxDatabaseCopy'.</p></td>
</tr>
</tbody>
</table>


Se a cópia do banco de dados da caixa de correio estiver localizada em um servidor que é parte de um grupo de disponibilidade do banco de dados (DAG), você pode realizar uma nova propagação do catálogo de índice de conteúdo a partir de outro membro do DAG.

Se a cópia do banco de dados de caixa de correio for a única, você deverá criar manualmente um novo catálogo de índice de conteúdo.

Para outras tarefas de gerenciamento relacionadas à Pesquisa do Exchange, consulte [Procedimentos de pesquisa do Exchange](exchange-search-procedures-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: 2 minutos. O tempo real para a nova propagação pode variar dependendo do tamanho do catálogo do índice de conteúdo que estiver sendo propagado novamente.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Pesquisa do Exchange" no tópico [Permissões de destinatários](recipients-permissions-exchange-2013-help.md).

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), ou [Proteção do Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=285351).

## Propagar novamente o catálogo de índice de conteúdo se o banco de dados de caixa de correio for parte de um DAG

Use um dos seguintes procedimentos se o banco de dados da caixa de correio estiver localizado em um servidor que faz parte de um DAG.

## Propagar novamente o catálogo do índice de conteúdo a partir de qualquer origem

Este exemplo propaga novamente o catálogo do índice de conteúdo da cópia do banco de dados DB1 no servidor de Caixa de Correio MBX1 a partir de qualquer servidor de origem no DAG que tenha uma cópia do banco de dados.

```powershell
Update-MailboxDatabaseCopy -Identity DB1\MBX1 -CatalogOnly
```

Para obter informações detalhadas de sintaxes e parâmetros, consulte [Update-MailboxDatabaseCopy](https://technet.microsoft.com/pt-br/library/dd335201\(v=exchg.150\)).

## Propagar novamente o catálogo do índice de conteúdo a partir de uma origem específica

Este exemplo propaga novamente o catálogo do índice de conteúdo da cópia do banco de dados DB1 no servidor de Caixa de Correio MBX1 a partir do servidor de Caixa de Correio MBX2, que também tem uma cópia do banco de dados.

```powershell
Update-MailboxDatabaseCopy -Identity DB1\MBX1 -SourceServer MBX2 -CatalogOnly
```

Para obter informações detalhadas de sintaxes e parâmetros, consulte [Update-MailboxDatabaseCopy](https://technet.microsoft.com/pt-br/library/dd335201\(v=exchg.150\)).

## Propagar novamente o catálogo de índice de conteúdo se houver apenas uma cópia do banco de dados da caixa de correio

Se a cópia do banco de dados de caixa de correio for a única, é preciso propagar novamente e de forma manual o catálogo de pesquisa recriando o catálogo de índice de conteúdo.

1.  Execute os seguintes comandos para interromper os serviços da Pesquisa do Microsoft Exchange e do Controlador de Host de Pesquisa do Microsoft Exchange.
    
    
    ```powershell
    Stop-Service MSExchangeFastSearch
    ```
    
    ```powershell
    Stop-Service HostControllerService
    ```

2.  Excluir, mover ou renomear a pasta que contém o catálogo de índice de conteúdo do Exchange. Esta pasta é denominada `%ExchangeInstallPath\Mailbox\<name of mailbox database>_Catalog\<GUID>12.1.Single`. Por exemplo, você pode renomear a pasta `C:\Program Files\Microsoft\Exchange Server\V15\Mailbox\Mailbox Database 0657134726_Catalog\F0627A72-9F1D-494A-839A-D7C915C279DB12.1.Single_OLD`.
    

    > [!NOTE]
    > A exclusão dessa pasta disponibilizará mais espaço em disco. Como alternativa, você pode renomear ou mover a pasta para mantê-la para fins de solução de problemas.



3.  Execute os seguintes comandos para reiniciar os serviços da Pesquisa do Microsoft Exchange e do Controlador de Host de Pesquisa do Microsoft Exchange.
    

    ```powershell
    Start-Service MSExchangeFastSearch
    ```

    ```powershell
    Start-Service HostControllerService
    ```
 
 Após reiniciar esses serviços, a Pesquisa do Exchange recriará o catálogo de índice de conteúdo.

## Como saber se funcionou?

Pode demorar um pouco para a Pesquisa do Exchange propagar novamente o catálogo do índice de conteúdo. Execute o seguinte comando para exibir o status do processo de propagação.

```powershell
    Get-MailboxDatabaseCopyStatus | FL Name,*Index*
```
Quando a nova propagação do catálogo de pesquisa estiver em andamento, o valor da propriedade *ContentIndexState* será **Crawling** (Rastreando). Quando a nova propagação estiver concluída, esse valor será alterado para **Healthy** (Adequado).

