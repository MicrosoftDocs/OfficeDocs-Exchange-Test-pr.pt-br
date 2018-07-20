---
title: 'Copiar os resultados de pesquisa de descoberta eletrônica para uma caixa de correio de descoberta: Exchange 2013 Help'
TOCTitle: Copiar os resultados de pesquisa de descoberta eletrônica para uma caixa de correio de descoberta
ms:assetid: bff2ce89-9e6f-494a-bd6a-2f2011507845
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Dn624163(v=EXCHG.150)
ms:contentKeyID: 61183356
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Copiar os resultados de pesquisa de descoberta eletrônica para uma caixa de correio de descoberta

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2014-02-24_

Depois de criar uma pesquisa de descoberta eletrônica In-loco, você pode usar o EAC para copiar os resultados para uma caixa de correio de descoberta. Você também pode usar o Shell para iniciar uma pesquisa de descoberta eletrônica que foi criada usando o cmdlet de **New-MailboxSearch** , que irá copiar os resultados para a caixa de correio de descoberta que foi especificada quando você criou a pesquisa.

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: 5 minutos ou mais dependendo do número de itens de caixa de correio são retornadas nos resultados da pesquisa

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Descoberta" no tópico [Permissões de política e conformidade de mensagens](messaging-policy-and-compliance-permissions-exchange-2013-help.md).

  - Uma pesquisa de descoberta eletrônica tem de ser criado, usando o EAC ou o Shell, antes de copiar os resultados da pesquisa. Para obter detalhes, consulte [Criar uma pesquisa de Descoberta Eletrônica In-loco](create-an-in-place-ediscovery-search-exchange-2013-help.md).

  - Exchange 2013 A instalação cria uma caixa de correio de descoberta chamada de **Caixa de correio de pesquisa de descoberta** para copiar os resultados da pesquisa. A caixa de correio de pesquisa de descoberta também é criada por padrão em Exchange Online. Você pode criar caixas de correio de descoberta adicionais. Para obter detalhes, consulte [Criar uma caixa de correio de descoberta](create-a-discovery-mailbox-exchange-2013-help.md).

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>.



## O que você deseja fazer?

## Usar o EAC para copiar os resultados de pesquisa

1.  No EAC, vá até **gerenciamento de conformidade** \> **bloqueio e descoberta eletrônica In-loco**.

2.  Na exibição de lista, selecione uma pesquisa de descoberta eletrônica.

3.  Clique em **Pesquisar**![Ícone Pesquisar](images/Dn750895.773574d0-9b92-4cab-9f6b-81532c7418b9(EXCHG.150).gif "Ícone Pesquisar") e, em seguida, clique em **Copiar os resultados de pesquisa** da lista suspensa.

4.  Em **Copiar Resultados da Pesquisa**, selecione uma das seguintes opções:
    
      - **Incluir itens não pesquisáveis**    Marque esta caixa de seleção para incluir os itens de caixa de correio que não puderam ser pesquisados (por exemplo, mensagens com anexos de tipos de arquivo que não puderam ser indexados pela Exchange pesquisa). Para obter mais informações, consulte [Itens não pesquisáveis na descoberta eletrônica do Exchange](unsearchable-items-in-exchange-ediscovery-exchange-2013-help.md).
    
      - **Habilitar desduplicação**   Marque esta caixa de seleção para excluir mensagens duplicadas. Somente uma única instância de uma mensagem será copiada para a caixa de correio de descoberta.
    
      - **Habilitar o log completo**   Marque esta caixa de seleção para incluir um log completo nos resultados da pesquisa.
    
      - **Enviar um email para mim quando a cópia terminar**   Marque esta caixa de seleção para obter uma notificação por email quando a pesquisa terminar.
    
      - **Copiar os resultados desta caixa de correio de descoberta**   Clique em **Procurar** para selecionar a caixa de correio de descoberta para a qual você deseja copiar os resultados da pesquisa.
        
        ![Copiar os resultados da pesquisa](images/Dn624163.875e25ed-8308-408c-92c4-8c76fc9d9bfc(EXCHG.150).gif "Copiar os resultados da pesquisa")  

5.  Clique em **Copiar** para iniciar o processo de cópia dos resultados da pesquisa para a caixa de correio de descoberta especificada.

6.  Clique em **Atualizar**![Ícone Atualizar](images/Dd353189.85f271ca-32a4-426c-842a-d2172567099d(EXCHG.150).gif "Ícone Atualizar") para atualizar as informações sobre o status de cópia exibido no painel de detalhes.

7.  Após a conclusão da cópia, clique em **Abrir** para abrir a caixa de correio de descoberta e exibir os resultados da pesquisa.

## Use o Shell para copiar os resultados de pesquisa

Depois de usar o cmdlet **New-MailboxSearch** para criar uma pesquisa de descoberta eletrônica In-loco, você deve iniciar a pesquisa para copiar mensagens para a caixa de correio de descoberta especificado no parâmetro *TargetMailbox* . Para obter informações sobre como criar pesquisas de descoberta eletrônica usando o Shell, consulte:

  - [Usar o Shell para criar uma pesquisa de Descoberta Eletrônica In-loco](create-an-in-place-ediscovery-search-exchange-2013-help.md)

  - [New-MailboxSearch](https://technet.microsoft.com/pt-br/library/dd298064\(v=exchg.150\))

Você poderia, por exemplo, execute o seguinte comando para iniciar uma pesquisa de descoberta eletrônica chamada *Fabrikam investigação* para copiar os resultados da pesquisa para a caixa de correio de descoberta especificado.

    Start-MailboxSearch "Fabrikam Investigation"

Se você usou a opção *EstimateOnly* para fazer uma estimativa dos resultados da pesquisa, você precisa remover o comutador antes de copiar os resultados da pesquisa. Você também precisa especificar uma caixa de correio de descoberta para copiar para os resultados de pesquisa. Por exemplo, que você criou uma pesquisa somente estimativa usando o seguinte comando:

    New-MailboxSearch "FY13 Q2 Financial Results" -StartDate "04/01/2013" -EndDate "06/30/2013" -SourceMailboxes "DG-Finance" -SearchQuery '"Financial" AND "Fabrikam"' -EstimateOnly -IncludeUnsearchableItems

Para copiar os resultados da pesquisa para uma caixa de correio de descoberta, você faria execute os seguintes comandos:

```
Set-MailboxSearch "FY13 Q2 Financial Results" -EstimateOnly $false -TargetMailbox "Discovery Search Mailbox"
```
```
    Start-MailboxSearch "FY13 Q2 Financial Results"
```

## Para obter mais informações sobre como copiar os resultados da pesquisa

  - Depois de copiar os resultados da pesquisa na caixa de correio de descoberta, você pode exportar os resultados da pesquisa para um arquivo PST. Para obter mais informações, consulte [Exportar resultados de pesquisa de Descoberta Eletrônica para um arquivo PST](export-ediscovery-search-results-to-a-pst-file-exchange-2013-help.md).

  - Para obter mais informações sobre itens não pesquisáveis, consulte [Itens não pesquisáveis na descoberta eletrônica do Exchange](unsearchable-items-in-exchange-ediscovery-exchange-2013-help.md).

  - Se você está copiando todo o conteúdo de caixa de correio dentro de um intervalo de datas específico (por sem especificar qualquer palavra-chave nos critérios de pesquisa), em seguida, todos os itens não pesquisáveis dentro desse intervalo de datas serão automaticamente incluídos nos resultados da pesquisa. Portanto, não selecione a caixa de seleção **incluir itens não pesquisáveis** ao copiar os resultados da pesquisa. Caso contrário, uma cópia duplicada de todos os itens não pesquisáveis será copiada para a caixa de correio de descoberta.

  - Além de copiar os resultados da pesquisa para uma caixa de correio de descoberta, você também pode estimativa ou visualizar os resultados da pesquisa para uma pesquisa selecionado.
    
      - **Resultados da pesquisa de estimativa**   Essa opção retorna uma estimativa do tamanho total e o número de itens que retornarão na pesquisa com base nos critérios especificados por você. Estimativas são exibidas no painel de detalhes no EAC.
    
      - **Resultados da pesquisa de visualização**   Essa opção permite visualizar os resultados da pesquisa retornados pela pesquisa em vez de informarem copiá-los para uma caixa de correio de descoberta para exibir. Isso permite rapidamente determinar se os resultados da pesquisa são relevantes. Depois que você visualizar os resultados, você pode revisar sua consulta de pesquisa para restringir os resultados da pesquisa e execute novamente a pesquisa. Itens na página visualização são versões somente leitura dos resultados da pesquisa real, portanto você não pode mover, editar, excluir ou encaminhar na página de visualização.
    
    Para obter mais informações, consulte [estimativa ou visualização de resultados da pesquisa](create-an-in-place-ediscovery-search-exchange-2013-help.md).

