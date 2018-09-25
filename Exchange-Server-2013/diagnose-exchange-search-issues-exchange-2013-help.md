---
title: 'Diagnosticar problemas de Pesquisa do Exchange: Exchange 2013 Help'
TOCTitle: Diagnosticar problemas de Pesquisa do Exchange
ms:assetid: 8cfa26f4-ccf0-42dd-8570-67018188b4e8
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Bb123701(v=EXCHG.150)
ms:contentKeyID: 52058839
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Diagnosticar problemas de Pesquisa do Exchange

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2016-12-09_

Exchange Pesquisa indexa caixas de correio e suportado anexos em caixas de correio Exchange. Com o aumento de volumes de email, aumentando tamanhos e cotas de armazenamento, provisionamento de caixas de correio de arquivamento para usuários e In-Place eDiscovery para a realização de pesquisas de descoberta, Exchange pesquisa é um componente essencial dos servidores de caixa de correio em sua organização do Microsoft Exchange Server 2013. Problemas com Exchange pesquisa podem afetar a produtividade do usuário e afetar a funcionalidade de descoberta eletrônica In-loco.

Para saber mais sobre a Pesquisa do Exchange, consulte [Pesquisa do Exchange](exchange-search-exchange-2013-help.md).

Procurando tarefas de gerenciamento relacionadas à Pesquisa do Exchange? Consulte [Procedimentos de pesquisa do Exchange](exchange-search-procedures-exchange-2013-help.md).

## Usando o cmdlet Test-ExchangeSearch

A Etapa 5 do procedimento neste tópico descreve a execução do cmdlet **Test-ExchangeSearch** para ajudar a diagnosticar os problemas da Pesquisa do Exchange. Você pode usar o cmdlet **Test-ExchangeSearch** para testar a funcionalidade de Pesquisa do Exchange para um servidor de Caixa de correio, um banco de dados de caixa de correio ou uma caixa de correio específica. O cmdlet envia uma mensagem de teste à caixa de correio especificada (ou a uma caixa de correio de sistema do banco de dados, se uma caixa de correio não for especificada) e, em seguida, executa uma pesquisa para determinar se a mensagem foi indexada, incluindo o tempo para indexá-la. Sob condições normais, a Pesquisa do Exchange indexa uma mensagem em até 10 segundos após a mensagem ser criada ou enviada a uma caixa de correio. A mensagem de teste é excluída automaticamente após o teste.

Para informações detalhadas sobre sintaxes e parâmetros, consulte [Test-ExchangeSearch](https://technet.microsoft.com/pt-br/library/bb124733\(v=exchg.150\)).

## Recuperando itens não pesquisáveis

Você pode usar o cmdlet [Get-FailedContentIndexDocuments](https://technet.microsoft.com/pt-br/library/dd351154\(v=exchg.150\)) para recuperar uma lista de itens não pesquisáveis de caixa de correio que não puderam ser indexados com êxito por Exchange pesquisa. Você pode executar o cmdlet contra um servidor de caixa de correio, um banco de dados de caixa de correio ou uma caixa de correio específica. O cmdlet retorna detalhes sobre cada item que não puderam ser pesquisados. Há vários motivos por que um item de caixa de correio não pode ser pesquisado; Por exemplo, uma mensagem de email pode conter um tipo de arquivo de anexo que não pode ser indexado para pesquisa ou porque um filtro de pesquisa não está instalado ou está desabilitado. Se um filtro de pesquisa para esse tipo de arquivo estiver disponível, você pode instalá-lo em seus servidores Exchange.


> [!IMPORTANT]
> Os filtros de pesquisa fornecidos pela Microsoft são testados e compatíveis com a Microsoft. Recomendamos que você teste quaisquer filtros de pesquisa de terceiros em um ambiente de teste antes de instalá-los nos servidores do Exchange em um ambiente de produção.



Para obter mais informações sobre itens não pesquisáveis, consulte:

  - [Formatos de arquivo indexados pela pesquisa do Exchange](file-formats-indexed-by-exchange-search-exchange-2013-help.md)

  - [Itens não pesquisáveis na descoberta eletrônica do Exchange](unsearchable-items-in-exchange-ediscovery-exchange-2013-help.md)

## Diagnosticar problemas de Pesquisa do Exchange

Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Pesquisa do Exchange" no tópico [Permissões de destinatários](recipients-permissions-exchange-2013-help.md).

1.  **Verificar o estado do serviço**   O serviço de Pesquisa do Microsoft Exchange (MSExchangeFastSearch) foi iniciado no servidor de Caixa de Correio? Caso tenha sido, vá para a Etapa 2. Caso contrário, use o snap-in de MMC dos Serviços para verificar se o serviço MSExchangeFastSearch está em execução:
    
    1.  Clique em **Iniciar**, aponte para **Ferramentas Administrativas** e clique em **Serviços**.
    
    2.  Em **Serviços**, verifique se o **Status** para o serviço **Pesquisa do Microsoft Exchange** está listado como **Iniciado**.

2.  **Verificar a configuração do banco de dados de caixa de correio**   O parâmetro *IndexEnabled* está definido como true para o banco de dados de caixa de correio do usuário? Se tiver, vá para a Etapa 3. Do contrário, execute o comando a seguir no Shell para verificar se o sinalizador *IndexEnabled* está definido como true.
    
    ```powershell
    Get-MailboxDatabase | Format-Table Name,IndexEnabled
    ```
    
    Para obter informações detalhadas de sintaxes e de parâmetros, consulte [Get-MailboxDatabase](https://technet.microsoft.com/pt-br/library/bb124924\(v=exchg.150\)).

3.  **Verificar o estado de rastreamento do banco de dados de caixa de correio**   O banco de dados do Exchange foi rastreado? Caso tenha sido, vá para a Etapa 4. Caso contrário, use o Monitor de confiabilidade e desempenho para verificar o contador **Rastreador: Caixas de Correio Restantes** do objeto de desempenho **Índices da Pesquisa do MSExchange**. Execute as seguintes etapas:
    
    1.  Abra o **Monitor de desempenho** (perfmon.exe).
    
    2.  Na árvore de console, em **Ferramentas de Monitoramento**, clique em **Monitor de Desempenho**.
    
    3.  No painel Monitor de Desempenho, clique em **Adicionar** (sinal de adição verde).
    
    4.  Em **Adicionar Contadores**, na lista **Selecionar contadores do computador**, selecione o servidor no qual o banco de dados de caixa de correio que você deseja monitorar está localizado.
    
    5.  Na caixa não rotulada abaixo da lista **Selecionar contadores do computador**, selecione o objeto de desempenho **Índices da Pesquisa do MSExchange**.
    
    6.  Na caixa **Instâncias do objeto selecionado**, selecione a instância do banco de dados de caixa de correio do usuário.
    
    7.  Clique em **Adicionar** e clique em **OK**.
        
        No painel Monitor de Desempenho, o objeto de desempenho **Índices da Pesquisa do MSExchange** está listado na coluna **Objeto**, e seus diversos contadores estão listados na coluna **Contador**.
    
    8.  Veja o contador **Rastreador: Caixas de Correio Restantes**. Qualquer valor de 1 ou superior indica que as caixas de correio no banco de dados ainda estão sendo rastreadas. Quando o rastreamento for concluído, o valor será **0**.
    
    Para obter informações sobre como usar o Monitor de desempenho, consulte [desempenho e confiabilidade Monitoring Getting Started Guide para Windows Server 2008](https://go.microsoft.com/fwlink/p/?linkid=178005)

4.  **Verificar a integridade de indexação de cópia de banco de dados**   O índice de conteúdo é íntegro? Use o cmdlet **Get-MailboxDatabaseCopyStatus** para verificar a integridade de indexação do conteúdo de uma cópia de banco de dados.
    
        Get-MailboxDatabaseCopyStatus -Server $env:ComputerName | Format-Table Name,Status,ContentIndex* -Auto
    
    Para informações detalhadas sobre sintaxes e parâmetros, consulte [Get-MailboxDatabaseCopyStatus](https://technet.microsoft.com/pt-br/library/dd298044\(v=exchg.150\)).

5.  **Executar o cmdlet Test-ExchangeSearch**   Se o banco de dados de caixa de correio já tiver sido rastreado, será possível executar o cmdlet **Test-ExchangeSearch** para o banco de dados de caixa de correio ou para uma caixa de correio específica.
    
    ```powershell
    Test-ExchangeSearch -Identity AlanBrewer@contoso.com
    ```
    
    Para informações detalhadas sobre sintaxes e parâmetros, consulte [Test-ExchangeSearch](https://technet.microsoft.com/pt-br/library/bb124733\(v=exchg.150\)).

6.  **Verifique o log de eventos do aplicativo**   Usando o Visualizador de eventos ou o Shell, verifique o log de eventos do aplicativo para mensagens de erro relacionados à pesquisa. Verifique se há seguintes fontes de evento.
    
      - **MSExchangeFastSearch**
    
      - **MSExchangeIS**
    
    Para obter mais informações, visite o link na entrada do log de eventos.

7.  **Reiniciar o serviço Pesquisa do Microsoft Exchange**   Use o snap-in MMC dos Serviços ou o Shell para interromper o serviço Pesquisa do MicrosoftExchange (MSExchangeFastSearch):
    
    1.  Clique em **Iniciar**, aponte para **Ferramentas Administrativas** e clique em **Serviços**.
    
    2.  Em **Serviços**, clique com o botão direito do mouse em em **Pesquisa do Microsoft Exchange** e clique em **Parar**. Depois que o serviço for parado, clique com o botão direito no serviço novamente e clique em **Iniciar**.

8.  **Propagar novamente o catálogo de pesquisa**   Em alguns casos, como quando o catálogo de pesquisa está corrompido, você talvez precise propagar novamente o catálogo. Quando houver a necessidade de propagar novamente um catálogo de pesquisa, a Pesquisa do Exchange notificará você registrando entradas no log de eventos do Aplicativo. Para mais informações sobre como propagar novamente o catálogo de Pesquisa, consulte [Propagar novamente o catálogo de pesquisa](reseed-the-search-catalog-exchange-2013-help.md).

