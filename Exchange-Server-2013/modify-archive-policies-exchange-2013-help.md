---
title: 'Modificar políticas de arquivamento: Exchange 2013 Help'
TOCTitle: Modificar políticas de arquivamento
ms:assetid: 1e3002c2-801a-43ea-ae00-52ab34d76b9c
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Hh529919(v=EXCHG.150)
ms:contentKeyID: 50485086
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Modificar políticas de arquivamento

 

_**Aplica-se a:**Exchange Online, Exchange Server 2013_

_**Tópico modificado em:**2016-02-01_

Em Exchange Server 2013 e Exchange Online, você pode usar políticas de arquivamento para mover automaticamente os itens de caixa de correio pessoal (no local) ou arquivos mortos baseados em nuvem. Políticas de arquivamento são marcas de retenção que usam a ação de retenção **Mover para arquivo morto**.

A Configuração do Exchange cria uma política de retenção chamada **Política MRM Padrão**. Essa política tem uma marca de política padrão atribuída que move itens para a caixa de correio de arquivo morto após dois anos. A política também inclui várias marcas pessoais que os usuários podem aplicar a pastas ou itens de caixa de correio para mover ou excluir mensagens automaticamente. Se uma caixa de correio não tiver uma política de retenção atribuída quando for habilitada para arquivo morto, a **Política MRM Padrão** será aplicada automaticamente a ela pelo Exchange. Você também pode criar suas próprias políticas de arquivo morto e retenção e aplicá-las aos usuários de caixas de correio. Para saber mais, consulte [Marcas e políticas de retenção](retention-tags-and-retention-policies-exchange-2013-help.md).

Você pode modificar as marcas de retenção incluídas na política padrão para cumprir com seus requisitos comerciais. Por exemplo, você pode modificar a marca de política padrão de arquivo morto para mover itens para o arquivo morto após três anos em vez de dois. Você também pode criar marcas pessoais adicionais e adicioná-las a uma política de retenção, incluindo a **Política MRM Padrão**, ou permitir que os usuários adicionem marcas pessoais a suas caixas de correio, nas opções do Outlook Web App.

Para tarefas de gerenciamento adicionais relacionadas a arquivos mortos, consulte:

  - **Exchange Server 2013:** [Gerenciar arquivos mortos de In-loco no Exchange 2013](manage-in-place-archives-in-exchange-2013-exchange-2013-help.md)

  - **Exchange Online:** [Habilitar ou desabilitar uma caixa de correio de arquivo morto no Exchange Online](https://technet.microsoft.com/pt-br/library/jj984357\(v=exchg.150\))


> [!TIP]
> &nbsp;&nbsp;&nbsp;Em uma implantação híbrida do Exchange, você pode habilitar uma caixa de correio de arquivo morto baseada em nuvem para uma caixa de correio principal local. Se você atribuir uma política de arquivo morto a uma caixa de correio local, os itens serão transferidos para o arquivo morto baseado em nuvem. Se um item for transferido para a caixa de correio de arquivo morto, nenhuma cópia será mantida na caixa de correio local. Se a caixa de correio local for colocada em espera, uma política de arquivo morto ainda moverá os itens para a caixa de correio de arquivo morto baseada em nuvem, na qual serão preservados durante o período especificado pela retenção.



## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: 5 minutos.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Gerenciamento de registros de mensagens" no tópico [Permissões de política e conformidade de mensagens](messaging-policy-and-compliance-permissions-exchange-2013-help.md).

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>.



## O que você deseja fazer?

## Usar o EMC para modificar a política de arquivo morto padrão

1.  Navegue para **Gerenciamento de conformidade** \> **Marcas de retenção** e depois.

2.  No modo de exibição de lista, selecione a marca **Padrão 2 anos para mover para arquivo morto** e clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").
    

    > [!TIP]
    > Você pode clicar na coluna <STRONG>TIPO</STRONG>, para organizar as marcas de retenção por tipo. A política de arquivo morto padrão é mostrada como o tipo <STRONG>Padrão</STRONG> e tem a ação de retenção <STRONG>Arquivar</STRONG>. Como alternativa, clique em <STRONG>NOME</STRONG>, para classificar as marcas de retenção pelo nome.



3.  
    
    Em **Marca de Retenção**, exiba ou modifica as seguintes configurações e clique em **Salvar**:
    
      - **Nome** Use essa caixa no topo da página para exibir ou alterar o nome da marca.
    
      - **Tipo de marca de retenção**   Esse campo somente leitura exibe o tipo da marca.
    
      - **Ação de retenção** Não modifique esse campo para políticas de arquivamento.
    
      - **Período de retenção** Selecione uma das opções a seguir:
        
          - **Nunca**   Clique nesse botão para desabilitar a marca. Se uma DPT for desabilitada, a marca não será mais aplicada à caixa de correio.
            

            > [!IMPORTANT]
            > Itens que têm uma marca de retenção desabilitada aplicada não são processados pelo Assistente de Caixa de Correio. Se quiser evitar a aplicação de uma marca a itens, recomendamos desabilitar a marca em vez de exclui-la. Quando uma marca é excluída, a configuração da marca é excluída do Active Directory e o Assistente de Caixa de Correio processa todas as mensagens para remover a marca excluída.

            

            > [!TIP]
            > Se um usuário aplicar uma marca a um item acreditando que esse item nunca será movido, a habilitação subsequente da marca pode mover itens que o usuário desejava reter na caixa de correio primária.

        
          - **Quando um item atingir a seguinte idade (dias)**   Clique nesse botão para especificar que os itens devem ser movidos para o arquivo morto após um certo período. Por padrão, essa configuração está definida para mover itens para o arquivo morto após dois anos (730 dias). Para modificar essa configuração, na caixa de texto correspondente, digite a quantidade de dias no período de retenção. O intervalo de valores varia de 1 a 24.855 dias.
    
      - **Comentários**   Use essa caixa para digitar um comentário que será exibido aos usuários do Outlook e do Outlook Web App.

## Usar o Shell para modificar políticas de arquivo morto

Este exemplo modifica a marca `Default 2 year move to archive` para mover itens após 1.095 dias (três anos).

    Set-RetentionPolicyTag "Default 2 year move to archive" -Name "Default 3 year move to archive" -AgeLimitForRetention 1095

Este exemplo desabilita a marca `Default 2 year move to archive`.

    Set-RetentionPolicyTag "Default 2 year move to archive" -RetentionEnabled $false

Este exemplo recupera todas as marcas de política padrão de arquivo morto e marcas pessoais e as desabilita.

    Get-RetentionPolicyTag | ? {$_.RetentionAction -eq "MoveToArchive"} | Set-RetentionPolicyTag -RetentionEnabled $false

Para obter informações detalhadas sobre sintaxe e parâmetros, consulte [Set-RetentionPolicyTag](https://technet.microsoft.com/pt-br/library/dd298042\(v=exchg.150\)) e [Get-RetentionPolicyTag](https://technet.microsoft.com/pt-br/library/dd298009\(v=exchg.150\)).

## Como saber se funcionou?

Use o cmdlet [Get-RetentionPolicyTag](https://technet.microsoft.com/pt-br/library/dd298009\(v=exchg.150\)) para recuperar as configurações da marca de retenção.

Esse comando recupera as propriedades da marcar de retenção `Default 2 year move to archive` e canaliza a saída para o cmdlet **Format-List**, para mostrar todas as propriedades em um formato de lista.

    Get-RetentionPolicyTag "Default 2 year move to archive" | Format-List

