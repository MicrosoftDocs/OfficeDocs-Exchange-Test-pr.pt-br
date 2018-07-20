---
title: 'Exibir estatísticas de pastas públicas e itens de pasta pública: Exchange 2013 Help'
TOCTitle: Exibir estatísticas de pastas públicas e itens de pasta pública
ms:assetid: 4e412710-9a74-4649-ab01-502e969a7eda
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Aa997949(v=EXCHG.150)
ms:contentKeyID: 50485563
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Exibir estatísticas de pastas públicas e itens de pasta pública

 

_**Aplica-se a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Tópico modificado em:** 2013-02-14_

Este tópico explica como obter estatísticas de uma pasta pública, como nome para exibição, hora de criação, horário da última modificação, último acesso do usuário e tamanho do item. Você pode usar essas informações para tomar decisões sobre a exclusão ou não de pastas públicas.


> [!TIP]
> No centro de administração do Exchange (EAC), você pode ver algumas informações de cota e de uso de pastas públicas navegando para <STRONG>Pastas Públicas</STRONG> &gt; <STRONG>Editar</STRONG><IMG title="Ícone de edição" alt="Ícone de edição" src="images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif"> &gt; <STRONG>Uso de caixa de correio</STRONG>. No entanto, estas informações são incompletas, e é recomendável que você use o Shell para exibir estatísticas de pasta pública.



Para conhecer tarefas de gerenciamento adicionais relacionadas ao gerenciamento de pastas públicas, consulte [Procedimentos de pasta pública](public-folder-procedures-exchange-2013-help.md).

Para conhecer tarefas de gerenciamento adicionais relacionadas a pastas públicas, consulte [Procedimentos de pasta pública no Office 365 e Exchange Online](https://technet.microsoft.com/pt-br/library/jj966272\(v=exchg.150\)).

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: 1 minuto.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Pastas públicas" no tópico [Permissões de compartilhamento e colaboração](sharing-and-collaboration-permissions-exchange-2013-help.md).

  - Você não pode usar o EAC para recuperar estatísticas de pastas públicas.

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>.



## O que você deseja fazer?

## Use o Shell para obter estatísticas de pasta pública

Este exemplo retorna as estatísticas da pasta pública Marketing com um comando canalizado para formatar a lista.

    Get-PublicFolderStatistics -Identity \Marketing | Format-List


> [!TIP]
> O valor do parâmetro <EM>Identity</EM> precisa incluir o caminho para a pasta pública. Por exemplo, se a pasta pública Marketing existisse sob a pasta pai Business, seria necessário fornecer o seguinte valor: <CODE>\Business\Marketing</CODE>



Para informações detalhadas de sintaxes e de parâmetros, consulte [Get-PublicFolderStatistics](https://technet.microsoft.com/pt-br/library/aa998663\(v=exchg.150\)).

## Usar o Shell para ver estatísticas de itens de pasta pública

É possível exibir as seguintes informações sobre itens dentro de uma pasta pública:

  - Tipo de item

  - Assunto

  - Hora da última modificação pelo usuário

  - Horário do último acesso de usuário

  - Hora de criação

  - Anexos

  - Tamanho da mensagem

É possível usar essas informações para tomar decisões sobre quais ações tomar para as pastas públicas, como quais pastas públicas excluir. Por exemplo, você talvez queira excluir uma pasta pública se os itens não tiverem sido acessados durante dois anos, ou você talvez queira converter uma pasta pública que esteja sendo usada como um repositório de documentos em outro aplicativo de acesso para cliente.

Este exemplo retorna estatísticas padrão para todos os itens dentro da pasta pública Pamphlets no caminho \\Marketing\\2013. As informações padrão incluem a identidade de itens, a hora de criação e o assunto.

    Get-PublicFolderItemStatistics -Identity "\Marketing\2013\Pamphlets"

Este exemplo retorna informações adicionais sobre os itens em uma pasta pública Pamphlets, como assunto, hora da última modificação, hora de criação, anexos, tamanho da mensagem e o tipo de item. Ele também inclui um comando direcionado para formatar a lista.

    Get-PublicFolderItemStatistics -Identity "\Marketing\2010\Pamphlets" | Format-List

Para informações detalhadas de sintaxes e de parâmetros, consulte [Get-PublicFolderItemStatistics](https://technet.microsoft.com/pt-br/library/ee332344\(v=exchg.150\)).

## Usar o Shell para exportar a saída do cmdlet Get-PublicFolderItemStatistics para um arquivo .csv

Este exemplo exporta a saída do cmdlet para o arquivo PFItemStats.csv que inclui as seguintes informações de todos os itens da pasta pública \\Marketing\\Reports:

  - Assunto da mensagem (`Subject`)

  - Data e hora em que o item foi modificado pela última vez (`LastModificationTime`)

  - Se o item tem anexos (`HasAttachments`)

  - Tipo de item (`ItemType)`)

  - Tamanho do item (`MessageSize`)

<!-- end list -->

    Get-PublicFolderItemStatistics -Identity "\Marketing\Reports" | Select Subject,LastModificationTime,HasAttachments,ItemType,MessageSize | Export-CSV C:\PFItemStats.csv

Para informações detalhadas de sintaxes e de parâmetros, consulte [Get-PublicFolderItemStatistics](https://technet.microsoft.com/pt-br/library/ee332344\(v=exchg.150\)).

