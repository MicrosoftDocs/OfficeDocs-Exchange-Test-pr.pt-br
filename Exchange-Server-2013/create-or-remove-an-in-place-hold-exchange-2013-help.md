---
title: 'Criar ou remover um bloqueio In-loco: Exchange 2013 Help'
TOCTitle: Criar ou remover um bloqueio In-loco
ms:assetid: 9d5d8d37-a053-4830-9cb1-6e1ede25e963
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Dd979797(v=EXCHG.150)
ms:contentKeyID: 50486258
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Criar ou remover um bloqueio In-loco

 

_**Aplica-se a:**Exchange Online, Exchange Server 2013_

_**Tópico modificado em:**2017-01-18_


> [!TIP]
> Adiamos o prazo de 1 de julho de 2017 para criar novos Bloqueios In-loco no Exchange Online (em planos autônomos do Office 365 e do Exchange Online). No entanto, mais para o fim deste ano ou no início do próximo ano, não será possível criar novos Bloqueios In-loco no Exchange Online. Como alternativa ao uso de Bloqueios In-loco, use <A href="https://go.microsoft.com/fwlink/?linkid=780738">casos de descoberta eletrônica</A> ou <A href="https://go.microsoft.com/fwlink/?linkid=827811">políticas de retenção</A> no Centro de Conformidade e Segurança do Office 365. Após encerrarmos os novos Bloqueios In-loco, você ainda conseguirá modificar os existentes, e a criação de novos bloqueios em implantações híbridas no Exchange Server 2013 e no Exchange ainda terão suporte. Além disso, você poderá posicionar caixas de entrada em Retenção de Litígio.



Um bloqueio In-loco preserva todo o conteúdo de caixa de correio, incluindo itens excluídos e versões originais de itens modificados. Esses itens da caixa de correio são retornados em uma pesquisa de [Descoberta Eletrônica In-loco](in-place-ediscovery-exchange-2013-help.md) . Quando você coloca um bloqueio In-loco na caixa de correio de um usuário em, o conteúdo na caixa de correio de arquivo morto correspondente (se ele estiver habilitado) é também colocado em espera e retornado em uma pesquisa de descoberta eletrônica.

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: 5 minutos

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Bloqueio in-loco" no [Permissões de política e conformidade de mensagens](messaging-policy-and-compliance-permissions-exchange-2013-help.md) tópico.

  - Para colocar uma caixa de correio Exchange Online em bloqueio In-loco, ele deve ser atribuído a uma licença do Exchange Online (plano 2). Se uma caixa de correio for atribuída a uma licença do Exchange Online (plano 1), você teria atribuí-lo de uma licença separada de arquivamento do Exchange Online para colocá-la em espera.

  - Dependendo da sua latência de topologia e replicação Active Directory, ele pode demorar umas uma hora para um bloqueio In-loco entrem em vigor.

  - Conforme explicado anteriormente, quando você coloca um bloqueio In-loco em caixa de correio de um usuário, o conteúdo em correio de arquivo morto do usuário também é colocado em isenção. Se você colocar um bloqueio In-loco em uma caixa de correio principal no local em uma implantação híbrida de Exchange, a caixa de correio de arquivamento baseado em nuvem (se ativado) também é colocada em espera.

  - Se um usuário é colocado em vários In-Place Holds, as consultas de pesquisa de qualquer retenção baseada em consulta são combinadas (com operadores **OR** ). Nesse caso, o número máximo de palavras-chave em todas as isenções baseado em consulta colocadas em uma caixa de correio é 500. Se houver mais de 500 palavras-chave e, em seguida, todo o conteúdo na caixa de correio é colocada em espera (não apenas se o conteúdo que corresponde aos critérios de pesquisa). Todo o conteúdo é retido até que a quantidade total de palavras-chave é reduzida para 500 ou menos.

  - Em Exchange Online, a cota da pasta itens recuperáveis automaticamente é aumentada para 100 GB quando você realiza um bloqueio In-loco em uma caixa de correio. O tamanho padrão da pasta itens recuperáveis é 30 GB.

  - Em Exchange Online, você pode colocar um bloqueio In-loco nos grupos Office 365. Quando você realiza um grupo Office 365 em espera, a caixa de correio de grupo é colocada em espera; as caixas de correio dos membros do grupo não são colocadas em espera. Para obter informações sobre grupos de Office 365, consulte [Saiba mais sobre o Office 365 grupos](https://go.microsoft.com/fwlink/p/?linkid=724066).

## Criar um Bloqueio In-loco

**Usar o EAC para criar um bloqueio In-loco**

1.  Navegue até **Gerenciamento de conformidade** \> **Retenção e Descoberta Eletrônica Locais**.

2.  Clique em **Novo**![Ícone Adicionar](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Ícone Adicionar").

3.  Na **Descoberta eletrônica In-loco & bloqueio**, na página **nome e descrição**, digite um nome para a pesquisa e uma descrição opcional e clique em **Avançar**.

4.  Na página **caixas de correio e pastas públicas**, escolha os locais de conteúdo que você deseja colocar em espera e, em seguida, clique em **Avançar**.
    
    ![Escolher os locais de conteúdo para colocar em espera](images/Dd979797.bbe76c50-a93b-4e5e-acd2-78e0d747ea19(EXCHG.150).png "Escolher os locais de conteúdo para colocar em espera")  
    
    1.  **Todas as caixas de pesquisa**   Você não pode selecionar essa opção para criar um bloqueio In-loco. Você pode selecionar essa opção para pesquisas de descoberta eletrônica In-loco, mas para criar um bloqueio In-loco, selecione as caixas de correio específicas que você deseja colocar em espera.
    
    2.  **Não pesquise qualquer caixa de correio**   Selecione essa opção quando você estiver criando um bloqueio In-loco exclusivamente para pastas públicas.
    
    3.  **Especificar as caixas de correio para pesquisar**   Selecione essa opção e clique em **Adicionar**![Ícone Adicionar](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Ícone Adicionar") para selecionar as caixas de correio ou grupos de distribuição que você deseja colocar em espera. Exchange Online, você também pode selecionar os grupos de Office 365 deve ser colocado em espera.
    
    4.  **Pesquisar todas as pastas públicas**   Em Exchange Online, você pode selecionar essa caixa de seleção para colocar todas as pastas públicas em sua organização em espera. Conforme explicado anteriormente, para criar um bloqueio In-loco somente para pastas públicas, não deixe de marcar a opção **Não pesquisar qualquer caixa de correio**.

5.  Na página **consulta de pesquisa**, preencha os seguintes campos e clique em **Next**:
    
      - **Incluir todo conteúdo de caixa de correio do usuário**    Clique nesse botão para colocar todo o conteúdo em caixas de correio selecionadas em espera.
    
      - **Filtro com base nos critérios**    Clique nesse botão para especificar os critérios de pesquisa, incluindo palavras-chave, datas de início e término, endereços de destinatário e remetente e tipos de mensagens. Quando você cria uma consulta com base em espera, somente os itens que correspondem a critérios são preservados de pesquisa.
        

        > [!TIP]
        > Quando você coloca pastas públicas em bloqueio In-loco, relacionadas ao processo de sincronização de hierarquia de pastas públicas de mensagens de email também são preservadas. Isso pode resultar em milhares de hierarquia sincronização relacionadas a itens de email que está sendo preservadas. Essas mensagens podem preencher a cota de armazenamento para a pasta itens recuperáveis em caixas de correio de pasta pública. Para impedir isso, você pode criar um bloqueio In-loco de baseado em consulta e adicionar o seguinte par <CODE>property:value</CODE> a consulta de pesquisa:<BR><CODE>NOT(subject:HierarchySync*)</CODE><BR>O resultado é que qualquer mensagem (relacionada à sincronização de hierarquia de pasta pública) que contenha a frase "HierarchySync" na linha de assunto não será colocada em espera.



6.  Na página **configurações de bloqueio In-loco**, marque a caixa de seleção **conteúdo local correspondente à consulta de pesquisa em caixas de correio selecionadas em espera** e selecione uma das seguintes opções:
    
      - **Reter indefinidamente**    Clique nesse botão para colocar os itens retornados pela pesquisa em um bloqueio indefinido. Itens em espera serão preservadas até que você remova a caixa de correio de pesquisa ou remover a pesquisa.
    
      - **Especificar número de dias para manter os itens em relação ao seu data de recebimento**    Clique nesse botão para reter itens por um período específico. Por exemplo, você pode usar essa opção se a organização exigir que todas as mensagens ser retidos pelo menos sete anos. Você pode usar um *baseadas em tempo* bloqueio In-loco, juntamente com uma política de retenção para certificar-se de que os itens são excluídos em sete anos. Para saber mais sobre a retenção de políticas, consulte [Marcas e políticas de retenção](retention-tags-and-retention-policies-exchange-2013-help.md).

**Use o Shell para criar um bloqueio In-loco**

Este exemplo cria um bloqueio In-loco Discovery-CaseId012 de espera de chamada e adiciona o joe@contoso.com da caixa de correio à isenção.


> [!IMPORTANT]
> Se você não especificar os parâmetros de pesquisa adicionais para um bloqueio In-loco, todos os itens a fonte especificada caixas de correio são colocadas em espera. Se você não especificar o parâmetro <EM>ItemHoldPeriod</EM> , os itens são colocados em espera indefinidamente ou até que a caixa de correio foi removida da isenção ou a suspensão seja excluída.



    New-MailboxSearch "Hold-CaseId012"-SourceMailboxes "joe@contoso.com" -InPlaceHoldEnabled $true

Para informações detalhadas de sintaxes e de parâmetros, consulte [New-MailboxSearch](https://technet.microsoft.com/pt-br/library/dd298064\(v=exchg.150\)).

**Como saber se funcionou?**

Para verificar se você criou com êxito o bloqueio In-loco, siga um destes procedimentos:

  - Use o EAC para verificar que o bloqueio In-loco está listado na exibição de lista da guia **Manter & eDiscovery In-loco**.

  - Use o cmdlet **Get-MailboxSearch** recuperar a pesquisa da caixa de correio e verificar os parâmetros de pesquisa. Para obter um exemplo de como recuperar uma pesquisa de caixa de correio, consulte os exemplos em [Get-MailboxSearch](https://technet.microsoft.com/pt-br/library/dd351021\(v=exchg.150\)).

Voltar ao início

## Remover um bloqueio In-loco


> [!IMPORTANT]
> Em Exchange 2013, pesquisas de caixa de correio podem ser usadas para um bloqueio In-loco e descoberta eletrônica In-loco. Não é possível remover uma pesquisa de caixa de correio que é usada para bloqueio In-loco. Desabilite primeiro o In-Place Hold desmarcando a caixa de seleção <STRONG>conteúdo local correspondente à consulta de pesquisa nas caixas de correio selecionadas em mantenha</STRONG> na página <STRONG>configurações de In-Place Hold</STRONG> ou pela configuração do parâmetro de <EM>InPlaceHoldEnabled</EM> como <CODE>$false</CODE> no Shell. Você também pode remover uma caixa de correio usando o parâmetro <EM>SourceMailboxes</EM> especificado em uma pesquisa.



**Usar o EAC para remover um bloqueio In-loco**

1.  Navegue até **gerenciamento de conformidade** \> **bloqueio e descoberta eletrônica In-loco**.

2.  Na exibição de lista, selecione o bloqueio In-loco você deseja remover e clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").

3.  Nas propriedades de **Descoberta eletrônica In-loco & bloqueio**, na página **Retenção In-loco**, desmarque o **conteúdo do local que corresponda a consulta de pesquisa em caixas de correio selecionadas em espera** e clique em **Salvar**.

4.  Selecione o bloqueio In-loco novamente o modo de exibição de lista e clique em **Excluir**![Excluir ícone](images/JJ673559.14f639f6-61e8-4418-bbfb-0db14de9d2f5(EXCHG.150).gif "Excluir ícone").

5.  No aviso, clique em **Sim** para remover a pesquisa.

**Use o Shell para remover um bloqueio In-loco**

Este exemplo desabilita primeiramente chamado Discovery-CaseId012 de espera de bloqueio In-loco e, em seguida, remove a pesquisa de caixa de correio.

    Set-MailboxSearch "Hold-CaseId012"  -InPlaceHoldEnabled $false
    Remove-MailboxSearch "Hold-CaseId012"

Para detalhadas sobre sintaxe e informações de parâmetro, consulte [Set-MailboxSearch](https://technet.microsoft.com/pt-br/library/dd335145\(v=exchg.150\)).

**Como saber se funcionou?**

Para verificar se você removeu com êxito um bloqueio In-loco, siga um destes procedimentos:

  - Use o EAC para verificar se o bloqueio In-loco não são exibidas no modo de exibição de lista da guia **Manter & eDiscovery In-loco**.

  - Use o cmdlet **Get-MailboxSearch** para recuperar todas as pesquisas de caixa de correio e verifique se a pesquisa que você removeu não está mais listada. Para obter um exemplo de como recuperar uma pesquisa de caixa de correio, consulte os exemplos em [Get-MailboxSearch](https://technet.microsoft.com/pt-br/library/dd351021\(v=exchg.150\)).

Retornar ao topo

