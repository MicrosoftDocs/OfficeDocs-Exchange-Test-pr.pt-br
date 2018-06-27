---
title: 'Modificar uma pesquisa de descoberta eletrônica In-loco: Exchange 2013 Help'
TOCTitle: Modificar uma pesquisa de descoberta eletrônica In-loco
ms:assetid: 3162743c-cc12-4997-91e0-bcbfea8bcb17
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Dd335182(v=EXCHG.150)
ms:contentKeyID: 50485286
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Modificar uma pesquisa de descoberta eletrônica In-loco

 

_**Aplica-se a:**Exchange Server 2013_

_**Tópico modificado em:**2014-08-27_

Depois de criar uma pesquisa de descoberta eletrônica In-loco, você pode modificá-lo para alterar os parâmetros de pesquisa. Por exemplo, você pode alterar as caixas de correio a ser pesquisado, intervalos de datas, palavras-chave, opções de log ou você pode especificar uma caixa de correio de descoberta diferente para armazenar os resultados da pesquisa. Quaisquer alterações feitas nas propriedades de pesquisa serão usadas quando você reiniciar a pesquisa.


> [!WARNING]
> Se estiver executando uma pesquisa de descoberta eletrônica In-loco, você deve pará-lo antes de modificá-lo. Quando você reiniciar a pesquisa, os resultados da última vez que a pesquisa foi executada são removidos da caixa de correio de descoberta. No entanto, os logs de pesquisas anteriores são salvas.



## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: 2 a 5 minutos.

  - Uma pesquisa de descoberta eletrônica In-loco foi criada e não está sendo executado.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Descoberta" no tópico [Permissões de política e conformidade de mensagens](messaging-policy-and-compliance-permissions-exchange-2013-help.md).

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

## O que você deseja fazer?

## Usar o EAC para modificar uma pesquisa de descoberta eletrônica In-loco

1.  Navegue até **Gerenciamento de conformidade** \> **Retenção e Descoberta Eletrônica Locais**.

2.  Na exibição de lista, selecione a pesquisa de descoberta eletrônica In-loco que você deseja modificar e, em seguida, clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").

3.  Na **Descoberta eletrônica In-loco & bloqueio**, você pode modificar as configurações a seguir:
    
      - Na página **nome**, modifique o nome para a pesquisa e a descrição opcional.
    
      - Na página **caixas de correio**, modifique as caixas de correio a ser pesquisado. Você pode pesquisar em todas as caixas de correio ou selecionar aqueles específicos a ser pesquisado.
        

        > [!IMPORTANT]
        > Você não pode usar a opção de <STRONG>todas as caixas de pesquisa</STRONG> para colocar todas as caixas de correio em servidores de caixa de correio Exchange 2013 em espera. Para criar um bloqueio In-loco, você deve selecionar <STRONG>caixas de correio de especificar a ser pesquisado</STRONG>. Para obter mais detalhes, consulte <A href="create-or-remove-an-in-place-hold-exchange-2013-help.md">Criar ou remover um bloqueio In-loco</A>.

    
      - Na página **consulta de pesquisa**, modifique os seguintes campos:
        
          - **Incluir todo conteúdo de caixa de correio do usuário**    Selecione essa opção para colocar todo o conteúdo em caixas de correio selecionadas em espera.
        
          - **Filtrar baseado em critérios**   Selecione esta opção para especificar os critérios de pesquisa, incluindo palavras-chave, datas de início e término, endereços do remetente e do destinatário e tipos de mensagens.
    
      - Na página **Retenção In-loco**, marque a caixa de seleção **conteúdo local correspondente à consulta de pesquisa em caixas de correio selecionadas em espera** e selecione uma das seguintes opções para colocar itens em bloqueio In-loco:
        
          - **Reter indefinidamente**   Selecione esta opção para colocar os itens retornados em uma retenção indefinida. Itens retidos serão preservados até que você remova a caixa de correio da pesquisa ou remova a pesquisa.
        
          - **Especificar número de dias para reter itens relativos para a data de recebimento** Use esta opção para reter itens por um período específico. Por exemplo, você pode usar essa opção se sua organização exigir que todas as mensagens sejam retidas por pelo menos sete anos. Você pode usar uma Retenção Local *com base no tempo* juntamente com uma política de retenção para garantir que itens sejam excluídos em sete anos.
            

            > [!IMPORTANT]
            > Ao Reter In-Loco caixas de correio ou itens por motivos jurídicos, geralmente, recomenda-se reter itens indefinidamente e remover a retenção quando o caso ou a investigação for concluído.



4.  Clique em **Salvar**.

## Use o Shell para modificar uma pesquisa de descoberta eletrônica In-loco

Este exemplo modifica a pesquisa de descoberta eletrônica In-loco Contoso de projeto de pesquisa para pesquisar caixas de correio que pertencem aos membros do grupo de distribuição DG-ProjectManagers.

    Set-MailboxSearch -Identity "Search-Project Contoso" -SourceMailboxes "DG-ProjectManagers"

## Como saber se funcionou?

Para verificar se você modificou com êxito uma pesquisa de descoberta eletrônica In-loco, siga um destes procedimentos:

  - Use o EAC para verificar as propriedades da pesquisa.

  - Use o cmdlet **Get-MailboxSearch** do Shell para verificar as propriedades da pesquisa. Para obter exemplos de como verificar as propriedades de uma pesquisa de caixa de correio, consulte a seção "Exemplos" em [Get-MailboxSearch](https://technet.microsoft.com/pt-br/library/dd351021\(v=exchg.150\)).


> [!TIP]
> Se você usar <STRONG>Get-MailboxSearch</STRONG> em Exchange Online para recuperar informações sobre uma pesquisa de descoberta eletrônica, você precisa especificar o nome de uma pesquisa para retornar uma lista completa das propriedades de pesquisa; Por exemplo, <CODE>Get-MailboxSearch "Contoso Legal Case"</CODE>. Se você executar o cmdlet <STRONG>Get-MailboxSearch</STRONG> sem usar quaisquer parâmetros, as propriedades a seguir não são retornadas: 
> <UL>
> <LI>
> <P>SourceMailboxes</P>
> <LI>
> <P>Sources</P>
> <LI>
> <P>SearchQuery</P>
> <LI>
> <P>ResultsLink</P>
> <LI>
> <P>PreviewResultsLink</P>
> <LI>
> <P>Errors</P></LI></UL>O motivo é que ele requer muitos recursos para retornar essas propriedades para todas as pesquisas de descoberta eletrônica em sua organização.


