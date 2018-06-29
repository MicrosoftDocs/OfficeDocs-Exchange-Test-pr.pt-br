---
title: 'Criar uma pesquisa de Descoberta Eletrônica In-loco: Exchange 2013 Help'
TOCTitle: Criar uma pesquisa de Descoberta Eletrônica In-loco
ms:assetid: feedc0c9-4a44-4bb2-8520-cc29d66d4fc3
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Dd353189(v=EXCHG.150)
ms:contentKeyID: 50487088
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Criar uma pesquisa de Descoberta Eletrônica In-loco

 

_**Aplica-se a:**Exchange Online, Exchange Server 2013_

_**Tópico modificado em:**2017-01-17_


> [!TIP]
> Adiamos o prazo de 1º de julho de 2017 para criar novas pesquisas de Descoberta eletrônica In-loco no Exchange Online (em planos autônomos do Office 365 e do Exchange Online). No entanto, mais para o fim deste ano ou no início do próximo ano, não será possível criar novas pesquisas no Exchange Online. Para criar pesquisas de Descoberta Eletrônica, use a <A href="https://go.microsoft.com/fwlink/?linkid=847843">Pesquisa de Conteúdo</A> no Centro de Conformidade e Segurança doOffice 365. Após desativarmos as novas pesquisas de Descoberta Eletrônica In-loco, você ainda conseguirá modificar as pesquisas existentes. Além disso, a criação de novas pesquisas de Descoberta Eletrônica In-loco no Exchange Server 2013 e as implantações híbridas do Exchange continuam com suporte.



Use [Descoberta Eletrônica In-loco](in-place-ediscovery-exchange-2013-help.md) para pesquisar em todo o conteúdo de caixa de correio, incluindo itens excluídos e versões originais de itens modificados para usuários que estão em [Retenção local e Retenção de litígio](in-place-hold-and-litigation-hold-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: 5 minutos

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Descoberta" no tópico [Permissões de política e conformidade de mensagens](messaging-policy-and-compliance-permissions-exchange-2013-help.md).

  - Para criar pesquisas de descoberta eletrônica, você precisa ter um endereço SMTP da organização que você está criando as pesquisas no. Isso no Exchange Online, você deve ter uma caixa de correio Exchange Online (plano 2) licenciada para criar pesquisas de descoberta eletrônica. Em uma organização do Exchange híbrido, sua caixa de correio do Exchange local deve ter uma conta de usuário de email correspondente na sua organização Office 365 para que você pode pesquisar Exchange Online caixas de correio. Ou, se você entrar com uma conta que existe apenas na Office 365, como a conta de administrador de locatário, essa conta deve ser atribuída uma licença do Exchange Online (plano 2).

  - A Instalação do Exchange 2013 cria uma caixa de correio de Descoberta chamada **Caixa de Correio de Pesquisa de Descoberta** para copiar os resultados da pesquisa. A Caixa de Correio de Pesquisa de Descoberta também é criada por padrão no Exchange Online. Você pode criar caixas de correio de Descoberta adicionais. Para detalhes, consulte [Criar uma caixa de correio de descoberta](create-a-discovery-mailbox-exchange-2013-help.md).

  - Quando você cria uma pesquisa de Descoberta eletrônica in-loco, as mensagens retornadas nos resultados da pesquisa não são copiadas automaticamente para uma caixa de correio de descoberta. Após criar a pesquisa, você pode usar o Centro de Administração do Exchange (EAC) para fazer uma estimativa, visualizar ou copiar os resultados da pesquisa em uma caixa de correio de descoberta. Para ver detalhes, consulte:
    
      - Estimate or preview search results (posteriormente neste tópico)
    
      - [Copiar os resultados de pesquisa de descoberta eletrônica para uma caixa de correio de descoberta](copy-ediscovery-search-results-to-a-discovery-mailbox-exchange-2013-help.md)

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>.



## Usar o EAC para criar uma pesquisa de Descoberta Eletrônica In-loco

Conforme explicado anteriormente, para criar pesquisas de Descoberta eletrônica, você precisa entrar com uma conta de usuário que tenha um endereço SMTP em sua organização.

1.  Vá até **Gerenciamento de conformidade** \> **Bloqueio e Descoberta Eletrônica In-loco**.

2.  Clique em **Novo**![Ícone Adicionar](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Ícone Adicionar").

3.  Em **Bloqueio e Descoberta Eletrônica In-loco**, na página **Nome e descrição**, digite um nome para a pesquisa, adicione uma descrição opcional e clique em **Avançar**.

4.  Na página **caixas de correio**, marque as caixas de correio a ser pesquisado. Você pode pesquisar em todas as caixas de correio ou selecionar aqueles específicos a ser pesquisado. Em Exchange Online, você também pode selecionar os grupos de Office 365 como uma fonte de conteúdo para a pesquisa.
    

    > [!IMPORTANT]
    > Não é possível usar a opção <STRONG>Pesquisar em todas as caixas de correio</STRONG> para bloqueat todas as caixas de correio. Para Retenção In-loco, você deve selecionar <STRONG>Especificar caixas de correio a pesquisar</STRONG>. Para mais detalhes, consulte <A href="create-or-remove-an-in-place-hold-exchange-2013-help.md">Criar ou remover um bloqueio In-loco</A>.



5.  Na página **Consulta de pesquisa**, preencha os seguintes campos:
    
      - **Incluir todo o conteúdo da caixa de correio do usuário**   Selecione esta opção para reter todo o conteúdo das caixas de correio selecionadas. Se você selecionar essa opção, não poderá especificar critérios de pesquisa adicionais.
    
      - **Filtrar baseado em critérios**   Selecione esta opção para especificar os critérios de pesquisa, incluindo palavras-chave, datas de início e término, endereços do remetente e do destinatário e tipos de mensagens.
        
        ![Configure a Consulta de Pesquisa de Descoberta Eletrônica](images/Dd298021.a3626569-8700-421e-8b4e-7ec520b28272(EXCHG.150).png "Configure a Consulta de Pesquisa de Descoberta Eletrônica")  
    

    > [!TIP]
    > O <STRONG>do:</STRONG> e <STRONG>para/Cc/Cco:</STRONG> campos são conectados por um operador <STRONG>ou</STRONG> na consulta de pesquisa que é criado quando você executar a pesquisa. Isso significa que qualquer mensagem enviado ou recebido por qualquer um dos usuários especificado (e os outros critérios de pesquisa de correspondências) está incluída nos resultados da pesquisa.<BR>As datas são conectadas por um operador <STRONG>e</STRONG>.



6.  Na página **Configurações de retenção local**, marque a caixa de seleção **Colocar em retenção o conteúdo que corresponda à consulta de pesquisa nas caixas de correio selecionadas** e selecione uma das seguintes opções para colocar itens na retenção local:
    
      - **Reter indefinidamente**   Selecione esta opção para colocar os itens retornados em uma retenção indefinida. Itens retidos serão preservados até que você remova a caixa de correio da pesquisa ou remova a pesquisa.
    
      - **Especificar número de dias para reter itens relativos para a data de recebimento** Use esta opção para reter itens por um período específico. Por exemplo, você pode usar essa opção se sua organização exigir que todas as mensagens sejam retidas por pelo menos sete anos. Você pode usar uma Retenção Local *com base no tempo* juntamente com uma política de retenção para garantir que itens sejam excluídos em sete anos.
        

        > [!IMPORTANT]
        > Ao Reter In-Loco caixas de correio ou itens por motivos jurídicos, geralmente, recomenda-se reter itens indefinidamente e remover a retenção quando o caso ou a investigação for concluído.



7.  Clique em **Concluir** para salvar a pesquisa e retornar uma estimativa do tamanho total e da quantidade itens que serão retornados pela pesquisa com base nos critérios que você especificou. As estimativas são exibidas no painel de detalhes. Clique em **Atualizar**![Ícone Atualizar](images/Dd353189.85f271ca-32a4-426c-842a-d2172567099d(EXCHG.150).gif "Ícone Atualizar") para atualizar as informações exibidas no painel de detalhes.

Voltar ao início

## Usar o Shell para criar uma pesquisa de Descoberta Eletrônica In-loco

Este exemplo cria a pesquisa de descoberta eletrônica In-loco chamada descoberta Discovery-CaseId012 que procura itens que contêm as palavras-chave Contoso e ProjectA e que também atendem aos seguintes critérios:

  - Data de início: 1/1/2009

  - Data de término: 12/31/2011

  - Caixa de correio de origem: DG-Finance

  - Caixa de correio de destino: Caixa de Correio de Pesquisa de Descoberta

  - Tipos de mensagens: Email

  - Inclui itens não pesquisáveis nas estatísticas da pesquisa

  - Nível de log: Inteiro


> [!IMPORTANT]
> Se você não especificar parâmetros de pesquisa adicionais ao realizar uma pesquisa de Descoberta Eletrônica In-loco, todos os itens nas caixas de correio de origem especificadas serão retornados nos resultados. Se você não especificar caixas de correio para a pesquisa, todas as caixas de correio em sua organização do Exchange ou do Exchange Online serão pesquisadas.



    New-MailboxSearch "Discovery-CaseId012" -StartDate "01/01/2009" -EndDate "12/31/2011" -SourceMailboxes "DG-Finance" -TargetMailbox "Discovery Search Mailbox" -SearchQuery '"Contoso" AND "Project A"' -MessageTypes Email -IncludeUnsearchableItems -LogLevel Full


> [!TIP]
> Ao usar os parâmetros <EM>StartDate</EM> e <EM>EndDate</EM>, você precisa usar o formato de data mm/dd/aaaa, mesmo se as configurações de seu computador local forem diferentes, como dd/mm/aaaa. Por exemplo, para pesquisar mensagens enviadas entre 1º de abril de 2013 e 1º de julho de 2013, use <STRONG>04/01/2013</STRONG> e <STRONG>07/01/2013</STRONG> como as datas de início e de término.



Este exemplo cria uma pesquisa de descoberta eletrônica In-loco denominada HRCase090116 que pesquisa para mensagens de email enviadas pelo Alex Darrow para Sara Davis 2015.

    New-MailboxSearch "HRCase090116" -StartDate "01/01/2015" -EndDate "12/31/2015" -SourceMailboxes  alexd,sarad -SearchQuery 'From:alexd@contoso.com AND To:sarad@contoso.com' -MessageTypes Email -TargetMailbox "Discovery Search Mailbox" -IncludeUnsearchableItems -LogLevel Full

Depois de usar o Shell para criar a pesquisa de Descoberta eletrônica in-loco, é necessário iniciar a pesquisa usando o cmdlet **Start-MailboxSearch** para copiar mensagens para a caixa de correio de descoberta especificada no parâmetro *TargetMailbox*. Para obter detalhes, consulte [Copiar os resultados de pesquisa de descoberta eletrônica para uma caixa de correio de descoberta](copy-ediscovery-search-results-to-a-discovery-mailbox-exchange-2013-help.md).

Para informações detalhadas de sintaxes e de parâmetros, consulte [New-MailboxSearch](https://technet.microsoft.com/pt-br/library/dd298064\(v=exchg.150\)).

Voltar ao início

## Usar o EAC para obter uma estimativa ou visualizar os resultados da pesquisa

Depois de criar uma pesquisa de Descoberta eletrônica in-loco, é possível usar o EAC para obter uma estimativa e uma visualização dos resultados da pesquisa. Se você criou uma nova pesquisa usando o cmdlet **New-MailboxSearch**, poderá usar o Shell para iniciar a pesquisa e obter uma estimativa dos resultados da pesquisa. Você não pode usar o Shell para visualizar mensagens retornadas nos resultados da pesquisa.

1.  Navegue até **Gerenciamento de conformidade** \> **Retenção e Descoberta Eletrônica Locais**.

2.  Na exibição de lista, selecione a pesquisa de descoberta eletrônica In-loco e siga um destes procedimentos:
    
      - Clique em **pesquisa**![Ícone Pesquisar](images/Dn750895.773574d0-9b92-4cab-9f6b-81532c7418b9(EXCHG.150).gif "Ícone Pesquisar") \> **Estimate resultados de pesquisa** para retornar uma estimativa do tamanho total e o número de itens que serão retornados pela pesquisa com base em critérios especificados. Esta opção reinicia a pesquisa e realiza uma estimativa.
        
        As Estimativas de Pesquisa são exibidas no painel de detalhes. Clique em **Atualizar**![Ícone Atualizar](images/Dd353189.85f271ca-32a4-426c-842a-d2172567099d(EXCHG.150).gif "Ícone Atualizar") para atualizar as informações exibidas no painel de detalhes.
    
      - No painel de detalhes para visualizar os resultados de uma vez concluída a estimativa de pesquisa, clique em **resultados da pesquisa de visualização** . Selecionar essa opção abre a janela de **visualização da pesquisa de descoberta eletrônica**. Todas as mensagens retornadas das caixas de correio que foram pesquisadas são exibidas.
        

        > [!TIP]
        > As caixas de correio pesquisadas são listadas no painel à direita na janela <STRONG>Visualização da pesquisa de descoberta eletrônica</STRONG>. Para cada caixa de correio, a quantidade de itens retornada e o tamanho total desses itens também são exibidos. Todos os itens retornados pela pesquisa são listados no painel à direita e podem ser classificados de acordo com a data mais recente ou a mais antiga. Os itens de cada caixa de correio não podem ser exibidos no painel à direita clicando em uma caixa de correio no painel à esquerda. Para exibir os itens retornados de uma caixa de correio específica, você pode copiar os resultados da pesquisa e exibir os itens na caixa de correio de descoberta.

    
    ![Estimativa ou visualização dos resultados da pesquisa](images/Dd353189.57e0fc2d-71bf-42aa-aa4b-4a77148f2b43(EXCHG.150).gif "Estimativa ou visualização dos resultados da pesquisa")  

Voltar ao início

## Usar o Shell para realizar uma estimativa dos resultados da pesquisa

Você pode usar a chave *EstimateOnly* para retornar apenas uma estimativa dos resultados da pesquisa e não copiar os resultados em uma caixa de correio de descoberta. É necessário iniciar uma pesquisa apenas para obtenção da estimativa com o cmdlet **Start-MailboxSearch**. Em seguida, você pode recuperar os resultados da pesquisa estimados usando o cmdlet **Get-MailboxSearch**.

Por exemplo, execute os seguintes comandos para criar uma nova pesquisa de Descoberta eletrônica e exibir uma estimativa dos resultados da pesquisa:

    New-MailboxSearch "FY13 Q2 Financial Results" -StartDate "04/01/2013" -EndDate "06/30/2013" -SourceMailboxes "DG-Finance" -SearchQuery '"Financial" AND "Fabrikam"' -EstimateOnly -IncludeKeywordStatistics

    Start-MailboxSearch "FY13 Q2 Financial Results"

    Get-MailboxSearch "FY13 Q2 Financial Results"

Para exibir informações específicas sobre os resultados de pesquisa estimados do exemplo anterior, você pode executar o seguinte comando:

    Get-MailboxSearch "FY13 Q2 Financial Results" | FL Name,Status,LastRunBy,LastStartTime,LastEndTime,Sources,SearchQuery,ResultSizeEstimate,ResultNumberEstimate,Errors,KeywordHits

Voltar ao início

## Mais informações sobre as pesquisas de descoberta eletrônica

  - Depois de criar uma nova pesquisa de descoberta eletrônica, você pode copiar os resultados da pesquisa na caixa de correio de descoberta e exportar esses resultados de pesquisa para um arquivo PST. Para obter mais informações, consulte:
    
      - [Copiar os resultados de pesquisa de descoberta eletrônica para uma caixa de correio de descoberta](copy-ediscovery-search-results-to-a-discovery-mailbox-exchange-2013-help.md)
    
      - [Exportar resultados de pesquisa de Descoberta Eletrônica para um arquivo PST](export-ediscovery-search-results-to-a-pst-file-exchange-2013-help.md)

  - Depois de executar uma estimativa de pesquisa de descoberta eletrônica (que inclui as palavras-chave nos critérios de pesquisa), você pode exibir as estatísticas de palavra-chave, clicando em **Exibir estatísticas de palavra-chave** no painel de detalhes para a pesquisa selecionado. Essas estatísticas mostram detalhes sobre o número de itens retornados para cada palavra-chave usado na consulta de pesquisa. No entanto, se mais de 100 caixas de correio de origem estão incluídas na pesquisa, um erro será retornado se você tentar exibir as estatísticas de palavra-chave. Para exibir estatísticas de palavra-chave, não mais de 100 caixas de correio de origem podem ser incluídas na pesquisa.

  - Se você usar **Get-MailboxSearch** em Exchange Online para recuperar informações sobre uma pesquisa de descoberta eletrônica, você precisa especificar o nome de uma pesquisa para retornar uma lista completa das propriedades de pesquisa; Por exemplo, `Get-MailboxSearch "Contoso Legal Case"`. Se você executar o cmdlet **Get-MailboxSearch** sem usar quaisquer parâmetros, as propriedades a seguir não são retornadas:
    
      - SourceMailboxes
    
      - Sources
    
      - SearchQuery
    
      - ResultsLink
    
      - PreviewResultsLink
    
      - Errors
    
    O motivo é que ele requer muitos recursos para retornar essas propriedades para todas as pesquisas de descoberta eletrônica em sua organização.

Voltar ao início

