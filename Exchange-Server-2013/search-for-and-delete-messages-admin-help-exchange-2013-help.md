---
title: 'Pesquisar e excluir mensagens - ajuda de Admin: Exchange 2013 Help'
TOCTitle: Pesquisar e excluir mensagens - ajuda de Admin
ms:assetid: 8c36bb03-e716-4fdd-9958-4aa7a2a1db42
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Ff459253(v=EXCHG.150)
ms:contentKeyID: 52058463
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Pesquisar e excluir mensagens - ajuda de Admin

 

_**Aplica-se a:** Exchange Online, Exchange Server 2013_

_**Tópico modificado em:** 2017-12-20_

Os administradores podem usar o cmdlet **Search-Mailbox** para pesquisar caixas de correio do usuário e, em seguida, excluir mensagens de uma caixa de correio.

Para pesquisar e excluir mensagens em uma etapa, execute o cmdlet **Search-Mailbox** com a opção *DeleteContent*. Entretanto, quando você faz isso, não consegue visualizar os resultados da pesquisa ou gerar um log de mensagens que será retornado pela pesquisa, podendo excluir mensagens inadvertidamente. Para visualizar um log das mensagens encontradas na pesquisa antes de elas serem excluídas, execute o cmdlet **Search-Mailbox** com a opção *LogOnly*.

Como garantia adicional, você pode primeiro copiar as mensagens para outra caixa de correio usando os parâmetros *TargetMailbox* e *TargetFolder*. Fazendo isso, você mantém uma cópia das mensagens excluídas, caso precise acessá-las novamente.

## O que eu preciso saber antes de começar?

  - Tempo estimado para conclusão: 10 minutos. O tempo real pode variar dependendo do tamanho da caixa de correio e da consulta de pesquisa.

  - Você não pode usar o Centro de Administração do Exchange (EAC) para executar esses procedimentos. É necessário usar o Shell.

  - Você precisa ser atribuído ambas as seguintes funções de gerenciamento para procurar e excluir mensagens nas caixas de correio dos usuários:
    
      - **Pesquisa de Caixa de Correio**   Essa função permite procurar mensagens em várias caixas de correio da sua organização. Os administradores não têm essa função atribuída por padrão. Para atribuir a si mesmo esta função para que você possa pesquisar caixas de correio, adicione a si mesmo como um membro do grupo de funções do Gerenciamento de Descoberta. Consulte [Atribuir permissões de descoberta eletrônica no Exchange](https://docs.microsoft.com/pt-br/exchange/security-and-compliance/in-place-ediscovery/assign-ediscovery-permissions).
    
      - **Caixa de correio importar e exportar**   Essa função permite que você excluir mensagens da caixa de correio do usuário. Por padrão, essa função não é atribuída a qualquer grupo de funções. Para excluir mensagens de caixas de correio dos usuários, você pode adicionar a função caixa de correio importar e exportar para o grupo de funções de gerenciamento da organização. Para obter mais informações, consulte a seção "Adicionar uma função a um grupo de funções" no [Gerenciar grupos de função](manage-role-groups-exchange-2013-help.md) .

  - Se a caixa de correio a partir do qual você deseja excluir mensagens tiver a recuperação de item único habilitada, primeiro será necessário desabilitar o recurso. Para obter mais informações, consulte [Habilitar ou desabilitar a recuperação de item único para uma caixa de correio](https://docs.microsoft.com/pt-br/exchange/recipients-in-exchange-online/manage-user-mailboxes/enable-or-disable-single-item-recovery).

  - Se a caixa de correio a partir do qual você deseja excluir mensagens for colocada em espera, recomendamos que você verifique com o gerenciamento de registros ou o departamento jurídico antes de remover a retenção e excluam o conteúdo de caixa de correio. Depois de obter aprovação, siga as etapas listadas no tópico [Limpar a pasta itens recuperáveis](clean-up-the-recoverable-items-folder-exchange-2013-help.md).

  - Você pode pesquisar um máximo de 10.000 caixas de correio usando o cmdlet **Search-Mailbox** . Caso você seja uma organização Exchange Online e têm mais de 10.000 caixas de correio, você pode usar o recurso de pesquisa de conformidade (ou o cmdlet **New-ComplianceSearch** correspondente) para um número ilimitado de caixas de correio de pesquisa. Em seguida, você pode usar o cmdlet **New-ComplianceSearchAction** para excluir as mensagens retornadas por uma pesquisa de conformidade. Para obter mais informações, consulte [Procurar e excluir mensagens de email da sua organização do Office 365](https://go.microsoft.com/fwlink/p/?linkid=786856).

  - Se você incluir uma consulta de pesquisa (usando o parâmetro *SearchQuery* ), o cmdlet **Search-Mailbox** retornará um máximo de 10.000 itens nos resultados da pesquisa. Portanto, se você incluir uma consulta de pesquisa, você pode precisar executar o comando **Search-Mailbox** várias vezes para excluir mais de 10.000 itens.

  - Caixa de correio de arquivo morto do usuário também devem ser pesquisada quando você executa o cmdlet **Search-Mailbox** . Da mesma forma, os itens na caixa de correio de arquivo morto principal serão excluídos quando você usa o cmdlet **Search-Mailbox** com a opção *DeleteContent* . Para impedir isso, você pode incluir a opção *DoNotIncludeArchive* . Além disso, é recomendável que você não usar a opção *DeleteContent* para excluir mensagens nas caixas de correio Exchange Online que têm a expansão automática arquivamento habilitado, pois pode ocorrer a perda de dados inesperada.

## Pesquisar mensagens e registrar os resultados da pesquisa em log

Este exemplo pesquisa na caixa de correio de Isabel Martins mensagens que contenham a frase "Seu extrato bancário" no campo Assunto e registra em log os resultados da pesquisa na pasta SearchAndDeleteLog da caixa de correio do administrador. As mensagens não são copiadas para a caixa de correio de destino ou excluídas dela.

    Search-Mailbox -Identity "April Stewart" -SearchQuery 'Subject:"Your bank statement"' -TargetMailbox administrator -TargetFolder "SearchAndDeleteLog" -LogOnly -LogLevel Full

Este exemplo procura todas as caixas de correio na organização para mensagens que têm qualquer tipo de arquivo anexado que contém a palavra "Troia" no nome de arquivo e envia uma mensagem de log para a caixa de correio do administrador.

    Get-Mailbox -ResultSize unlimited | Search-Mailbox -SearchQuery attachment:trojan* -TargetMailbox administrator -TargetFolder "SearchAndDeleteLog" -LogOnly -LogLevel Full

Para obter informações detalhadas sobre sintaxes e parâmetros, confira [Search-Mailbox](https://technet.microsoft.com/pt-br/library/dd298173\(v=exchg.150\)).

Voltar ao início

## Pesquisar e excluir mensagens

Este exemplo pesquisa na caixa de correio de Isabel Martins mensagens que contenham a frase "Seu extrato bancário" no campo Assunto e exclui as mensagens da caixa de correio de origem sem copiar os resultados da pesquisa para outra pasta. Como explicado anteriormente, você precisa ter a função de gerenciamento de Importação e Exportação de Caixas de Correio para excluir mensagens da caixa de correio de um usuário.


> [!IMPORTANT]
> Quando você usar o cmdlet <STRONG>Search-Mailbox</STRONG> com a opção <EM>DeleteContent</EM>, as mensagens serão excluídas permanentemente da caixa de correio de origem. Antes de excluir permanentemente as mensagens, recomendamos usar a opção <EM>LogOnly</EM> para gerar um log das mensagens encontradas na pesquisa antes de serem excluídas ou copiar as mensagens para outra caixa de correio antes de excluí-las da caixa de correio de origem.



    Search-Mailbox -Identity "April Stewart" -SearchQuery 'Subject:"Your bank statement"' -DeleteContent

Este exemplo pesquisa na caixa de correio de Isabel Martins mensagens que contenham a frase "Seu extrato bancário" no campo Assunto, copia os resultados da pesquisa para a pasta AprilStewart-DeletedMessages na caixa de correio BackupMailbox e exclui as mensagens da caixa de correio de Isabel.

    Search-Mailbox -Identity "April Stewart" -SearchQuery 'Subject:"Your bank statement"' -TargetMailbox "BackupMailbox" -TargetFolder "AprilStewart-DeletedMessages" -LogLevel Full -DeleteContent

Este exemplo procura todas as caixas de correio na organização para mensagens com a linha de assunto "Download esse arquivo" e, em seguida, exclui-los permanentemente.

    Get-Mailbox -ResultSize unlimited | Search-Mailbox -SearchQuery 'Subject:"Download this file"' -DeleteContent

Para obter informações detalhadas sobre sintaxes e parâmetros, confira [Search-Mailbox](https://technet.microsoft.com/pt-br/library/dd298173\(v=exchg.150\)).

Voltar ao início

## Usando o parâmetro - LogLevel completo

Em alguns dos exemplos anteriores, o parâmetro *LogLevel* , com o `Full` valor é usado para registrar informações detalhadas sobre os resultados retornados pelo cmdlet **Search-Mailbox** . Quando você tiver incluído neste parâmetro, uma mensagem de email é criada e enviada à caixa de correio especificada pelo parâmetro *TargetMailbox* . O arquivo de log (que é um arquivo de formato CSV chamado pesquisa Results.csv) é anexado a esta mensagem de email e estará localizado na pasta especificada pelo parâmetro *TargetFolder* . O arquivo de log contém uma linha para cada mensagem que está incluída nos resultados da pesquisa quando você executa o cmdlet **Search-Mailbox** .

