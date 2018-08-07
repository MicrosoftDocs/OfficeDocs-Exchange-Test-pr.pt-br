---
title: 'Reduzir o tamanho de uma caixa de correio de descoberta no Exchange'
TOCTitle: Reduzir o tamanho de uma caixa de correio de descoberta no Exchange
ms:assetid: fa762d14-f942-4728-8813-887d11441a68
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Dn750895(v=EXCHG.150)
ms:contentKeyID: 62371339
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Reduzir o tamanho de uma caixa de correio de descoberta no Exchange

 

_**Aplica-se a:** Exchange Online, Exchange Server 2013_

_**Tópico modificado em:** 2015-04-07_

Possui uma caixa de correio de descoberta que excedeu o limite de 50 GB? Você pode corrigir esse problema criando novas caixas de correio de descoberta e copiando os resultados da pesquisa da caixa de correio de descoberta grande para as novas.

## Por que eu faria isso?

Em Exchange Server 2013 e Exchange Online, o tamanho máximo de caixas de correio de descoberta, que são usadas para armazenar os resultados da pesquisa de descoberta eletrônica In-loco, é de 50 GB. Antes do limite de tamanho atual, você conseguiu aumentar a cota de armazenamento para mais de 50 GB, que resultaram em ter caixas de correio de descoberta muito maiores do que 50 GB. Existem três problemas com caixas de correio de descoberta maiores que 50 GB:

  - Elas não são suportadas.

  - Não é possível migrá-las para o Office 365.

  - Se elas forem caixas de correio de descoberta no Exchange Server 2010, eles não podem ser atualizados para Exchange Server 2013.

## O processo em um relance

Veja rapidamente o que você precisará fazer para reduzir o tamanho de uma caixa de correio de descoberta que ultrapassou o limite de 50 GB:

1.  Create caixas de correio de descoberta adicionais às quais distribuir os resultados de pesquisa.

2.  Copy os resultados da pesquisa da caixa de correio de descoberta existente para uma ou mais caixas de correio de descoberta novas.

3.  Delete pesquisas de Descoberta Eletrônica da caixa de correio de descoberta original a fim de reduzir seu tamanho.

A estratégia apresentada aqui agrupa os resultados de pesquisa da caixa de correio de descoberta original em pesquisas separadas de Descoberta eletrônica com base em intervalos de datas. Essa é uma maneira rápida de copiar muitos resultados da pesquisa em uma nova caixa de correio de descoberta. O gráfico a seguir ilustra essa abordagem.

![Reduzir o tamanho de uma caixa de correio de descoberta](images/Dn750895.4400df18-c7ed-4c62-b304-f9060ffbdba5(EXCHG.150).gif "Reduzir o tamanho de uma caixa de correio de descoberta")

## O que você precisa saber antes de começar?

  - Tempo estimado para a conclusão da tarefa: O tempo poderá variar conforme a quantidade e o tamanho dos resultados da pesquisa que serão copiados em caixas de correio de descoberta diferentes.

  - Execute o comando a seguir para determinar o tamanho das caixas de correio de descoberta em sua organização.
    
        Get-Mailbox -RecipientTypeDetails DiscoveryMailbox | Get-MailboxStatistics | FL DisplayName,TotalItemSize

  - Determine se você precisa manter alguns ou todos os resultados de pesquisa da caixa de correio de descoberta que ultrapassou o limite de 50 GB. Execute as etapas deste tópico para manter os resultados de pesquisa, copiando-os em uma caixa de correio de descoberta diferente. Se não for necessário manter os resultados de uma pesquisa de Descoberta Eletrônica específica, você poderá excluir a pesquisa, conforme explicado na etapa 3. A exclusão de uma pesquisa excluirá seus resultados da caixa de correio de descoberta.

  - Se você não precisar dos resultados de pesquisa de uma caixa de correio de descoberta que ultrapassou o limite de 50 GB, exclua-os. Se essa for a caixa de correio de descoberta padrão criada quando sua organização do Exchange foi provisionada, recrie-a. Para obter mais informações, consulte [Excluir e recriar a caixa de correio de descoberta padrão no Exchange](delete-and-re-create-the-default-discovery-mailbox-in-exchange-exchange-2013-help.md).

  - Para casos jurídicos em andamento, convém exportar os resultados das pesquisas de Descoberta Eletrônica selecionadas para arquivos .pst. Isso mantém os resultados de uma pesquisa específica intactos. Além dos arquivos .pst que contém os resultados de pesquisa, um log de resultados da pesquisa (formato de arquivo .csv) que contém uma entrada para cada mensagem retornada nos resultados da pesquisa também é exportado. Cada entrada nesse arquivo identifica a caixa de correio de origem onde a mensagem está localizada. Para obter mais informações, consulte [Exportar resultados de pesquisa de Descoberta Eletrônica para um arquivo PST](export-ediscovery-search-results-to-a-pst-file-exchange-2013-help.md).
    
    Após a exportação dos resultados da pesquisa para arquivos .pst, será necessário usar o Outlook se você quiser importá-los para uma nova caixa de correio de descoberta.

## Etapa 1: criar caixas de correio de descoberta

A primeira etapa é criar caixas de correio de descoberta adicionais, para que você possa copiar os resultados da pesquisa da caixa de correio de descoberta que ultrapassou o limite de tamanho. Com base no limite de tamanho de 50 GB para caixas de correio de descoberta, determine quantas caixas de correio de descoberta adicionais serão necessárias e crie-as. Em seguida, será necessário atribuir aos usuários ou grupos as permissões necessárias para abrir essas novas caixas de correio de descoberta.

1.  Execute o seguinte comando para criar uma nova caixa de correio de descoberta.
    
        New-Mailbox -Name <discovery mailbox name> -Discovery

2.  Para atribuir permissões a um usuário ou grupo para abrir a caixa de correio de descoberta e acessar os resultados da pesquisa, execute o seguinte comando:
    
        Add-MailboxPermission <discovery mailbox name> -User <name of user or group> -AccessRights FullAccess -InheritanceType all

## Etapa 2: copiar os resultados da pesquisa em uma caixa de correio de descoberta

A próxima etapa é usar o cmdlet **New-MailboxSearch** para copiar os resultados de pesquisa da caixa de correio de descoberta existente para uma nova caixa de correio de descoberta criada na etapa anterior. Esse procedimento usa os parâmetros *StartDate* e *EndDate* para definir o escopo dos resultados da pesquisa em lotes menores do que 50 GB. Isso pode exigir testes (fazendo estimativas dos resultados de pesquisa) para dimensionar os resultados de pesquisa adequadamente.

1.  Execute o seguinte comando para criar uma nova pesquisa de Descoberta Eletrônica.
    
        New-MailboxSearch -Name "Search results from 2010" -SourceMailboxes "Discovery Search Mailbox" -StartDate "01/01/2010" -EndDate "12/31/2010" -TargetMailbox "Discovery Mailbox Backup 01" -EstimateOnly -StatusMailRecipients admin@contoso.com
    
    Este exemplo usa os seguintes parâmetros:
    
      - *Name* Este parâmetro especifica o nome da nova pesquisa de Descoberta Eletrônica. Como o escopo da pesquisa é definido pelas datas de envio e recebimento, é útil incluir o intervalo de datas no nome da pesquisa.
    
      - *SourceMailboxes* Este parâmetro especifica a caixa de correio de descoberta padrão. Você também pode especificar o nome da outra caixa de correio de descoberta que ultrapassou o limite de tamanho.
    
      - *StartDate* e *EndDate*   Esses parâmetros especificam o intervalo de datas dos resultados da pesquisa na caixa de correio de descoberta padrão a fim de incluir os resultados da pesquisa.
        

        > [!TIP]
        > Para as datas, use o formato de data abreviada mm/dd/aaaa, mesmo que as definições de Opções Regionais no computador local estejam configuradas com outro formato; por exemplo, dd/mm/aaaa. Por exemplo, use <STRONG>03/01/2014</STRONG> para especificar 1 de março de 2014.

    
      - *TargetMailbox*   Este parâmetro especifica os resultados da pesquisa que devem ser copiados para a caixa de correio de descoberta chamada "Discovery Mailbox Backup 01".
    
      - *EstimateOnly* Esta opção especifica que seja fornecida apenas uma estimativa do número de itens que serão retornados quando a pesquisa for iniciada. Se você não incluir essa opção, as mensagens serão copiadas na caixa de correio de destino quando a pesquisa for iniciada. O uso dessa opção permite que você ajuste os intervalos de datas, se for necessário, para aumentar ou diminuir o número de resultados da pesquisa.
    
      - *StatusMailRecipients*   Este parâmetro especifica se a mensagem de status deve ser enviada ao destinatário especificado.

2.  Após a criação da pesquisa, comece-a usando o Shell ou o Centro de administração do Exchange (EAC).
    
      - **Usando o Shell:**  Execute o seguinte comando para iniciar a pesquisa criada na etapa anterior. Como a opção *EstimateOnly* foi incluída quando a pesquisa foi criada, os resultados da pesquisa não serão copiados na caixa de correio de descoberta de destino.
        
            Start-MailboxSearch "Search results from 2010"
    
      - **Usando o EAC:**  Vá em **Gerenciamento de conformidade** \> **Bloqueio & Descoberta Eletrônica In-loco**. Selecione a pesquisa criada na etapa anterior, clique em **Pesquisar**![Ícone Pesquisar](images/Dn750895.773574d0-9b92-4cab-9f6b-81532c7418b9(EXCHG.150).gif "Ícone Pesquisar") e clique em **Estimar resultados da pesquisa**.

3.  Se for necessário, ajuste o intervalo de datas a fim de aumentar ou diminuir a quantidade de resultados de pesquisa retornados. Se você alterar o intervalo de datas, execute a pesquisa novamente para obter uma nova estimativa dos resultados. Considere a possibilidade de alterar o nome da pesquisa para refletir o novo intervalo de datas.

4.  Quando você concluir os testes da pesquisa, use o Shell ou o EAC para copiar os resultados de pesquisa para a caixa de correio de descoberta de destino.
    
      - **Usando o Shell:**  Execute o seguinte comando para copiar os resultados de pesquisa. É necessário remover a opção *EstimateOnly* antes de poder copiar os resultados da pesquisa.
        
      ```
            Set-MailboxSearch "Search results from 2010" -EstimateOnly $false
      ```
      ```        
            Start-MailboxSearch "Search results from 2010"
      ``` 
      - **Usando o EAC:**  Vá em **Gerenciamento de conformidade** \> **Bloqueio & Descoberta Eletrônica In-loco**. Selecione a pesquisa, clique em **Pesquisar**![Ícone Pesquisar](images/Dn750895.773574d0-9b92-4cab-9f6b-81532c7418b9(EXCHG.150).gif "Ícone Pesquisar") e clique em **Copiar resultados da pesquisa**.
    
    Para obter mais informações, consulte [Copiar os resultados de pesquisa de descoberta eletrônica para uma caixa de correio de descoberta](copy-ediscovery-search-results-to-a-discovery-mailbox-exchange-2013-help.md).

5.  Repita as etapas um a quatro para criar novas pesquisas para intervalos de data adicionais. Inclua o intervalo de datas no nome da nova pesquisa para indicar o intervalo de resultados. Para ter certeza de que nenhuma das caixas de correio de descoberta ultrapassa o limite de 50 GB, use as caixas de correio de descoberta diferentes como a caixa de correio de destino.

## Etapa 3: excluir as pesquisas de Descoberta Eletrônica

Depois de copiar os resultados de pesquisa da caixa de correio de descoberta original para a outra caixa de correio de descoberta, exclua as pesquisas da Descoberta Eletrônica originais. A exclusão de uma pesquisa de Descoberta Eletrônica excluirá os resultados de pesquisa da caixa de correio de descoberta onde esses resultados de pesquisa estão armazenados.

Antes de excluir uma pesquisa, você pode executar o seguinte comando para identificar o tamanho dos resultados da pesquisa que foram copiadas em uma caixa de correio de descoberta para todas as pesquisa em sua organização.

    Get-MailboxSearch | FL Name,TargetMailbox,ResultSizeCopied

Você pode usar o Shell ou o EAC para excluir uma pesquisa de Descoberta Eletrônica.

  - **Usando o Shell:**  Execute o seguinte comando.
    
        Remove-MailboxSearch -Identity <name of search>

  - **Usando o EAC:**  Vá em **Gerenciamento de conformidade** \> **Bloqueio & Descoberta Eletrônica In-loco**. Selecione a pesquisa que você deseja excluir e clique em **Excluir**![Excluir ícone](images/JJ673559.14f639f6-61e8-4418-bbfb-0db14de9d2f5(EXCHG.150).gif "Excluir ícone").

## Como saber se funcionou?

Após a exclusão das pesquisas de Descoberta Eletrônica a fim de remover os resultados da caixa de correio de descoberta onde foram armazenadas, execute o seguinte comando para exibir o tamanho de uma caixa de correio de descoberta selecionada.

    Get-Mailbox <name of discovery mailbox> | Get-MailboxStatistics | FL TotalItemSize

