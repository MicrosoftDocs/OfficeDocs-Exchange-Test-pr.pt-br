---
title: 'Desativar ou suspender o gerenciamento de registros de mensagens: Exchange 2013 Help'
TOCTitle: Desativar ou suspender o gerenciamento de registros de mensagens
ms:assetid: 631191aa-3bba-4ebf-a727-c48ed2ebe176
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Aa998580(v=EXCHG.150)
ms:contentKeyID: 52058822
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Desativar ou suspender o gerenciamento de registros de mensagens

 

_**Aplica-se a:**Exchange Server 2010 Service Pack 2 (SP2), Exchange Server 2013_

_**Tópico modificado em:**2013-02-14_

Para atender aos requisitos de indivíduos, de TI e de empresas, você pode ter que desativar ou suspender temporariamente o MRM (gerenciamento de registros de mensagens) de um usuário individual ou de um servidor de caixa de correio. Alguns motivos pelos quais você pode ter que desativar ou suspender o MRM incluem:

  - Se um usuário de caixa de correio estiver ausente do escritório ou não puder acessar o email, você pode desativar temporariamente o MRM da caixa de correio dele, pondo-a em retenção. Quando uma caixa de correio está em retenção, ela não é mais processada pelo Assistente de Pasta Gerenciada. Quando o usuário de caixa de correio voltar ou puder acessar a caixa de correio novamente, você poderá remover a retenção da caixa de correio.

  - Se precisar testar ou solucionar problemas de desempenho, você pode desativar temporariamente o MRM no servidor limpando o agendamento do Assistente de Pasta Gerenciada.

  - Se você precisar remover uma marca de retenção das caixas de correio (que têm uma diretiva de retenção com essa marca aplicada), é possível remover a marca da diretiva.

  - Se quiser que uma diretiva de retenção ou uma diretiva de caixa de correio de pasta gerenciada não se aplique mais a uma caixa de correio, você pode remover a diretiva da caixa de correio.

  - Se sua organização decidir não usar os recursos de MRM, o MRM pode ser desativado permanentemente para a organização inteira. Se depois você decidir implantar o MRM, será possível fazê-lo.

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: 1 minuto

  - Os procedimentos neste tópico exigem permissões específicas. Consulte cada procedimento para ver informações sobre permissões.

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), ou [Proteção do Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=285351).

## O que você deseja fazer?

## Pôr as caixas de correio em retenção

Você pode colocar caixas de correio em retenção para desativar temporariamente o MRM (por exemplo, quando os usuários estiverem de férias). Isso suspende o processamento das políticas de retenção para caixa de correio até que a retenção seja desabilitada. É diferente de colocar caixas de correio em Bloqueio In-loco ou retenção de litígio.

Para obter detalhes sobre como colocar uma caixa de correio em retenção, consulte [Retenção local de uma caixa de correio em retenção](place-a-mailbox-on-retention-hold-exchange-2013-help.md).

Para saber mais sobre Bloqueio In-loco e retenção de litígio, veja [Retenção local e Retenção de litígio](in-place-hold-and-litigation-hold-exchange-2013-help.md).

## Remover marcas de retenção das caixas de correio

Para remover uma marca de retenção de uma caixa de correio, você deve desvincular a marca da diretiva de retenção. Ao desvincular uma marca de diretiva de retenção de uma pasta padrão, a marca de caixa de correio padrão se aplicará a todos os itens dessa pasta. Ao desvincular uma marca pessoal, ela não estará mais disponível ao usuário. As etiquetas aplicadas às mensagens existentes continuarão a ser processadas salvo se você remover a etiqueta da organização do Exchange.

Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada \&quot;Gerenciamento de registros de mensagens\&quot;, no tópico [Permissões de política e conformidade de mensagens](messaging-policy-and-compliance-permissions-exchange-2013-help.md).

Este exemplo do Shell desvincula a marca de retenção Excluir - 3 Dias da diretiva de retenção Usuários-Corporativos.

    $tags = (Get-RetentionPolicy "Corp-Users").RetentionPolicyTagLinks
    $tags -= "Deleted Items - 3 Days"
    Set-RetentionPolicy "Corp-Users" -RetentionPolicyTagLinks $tags

Para obter informações detalhadas sobre sintaxe e parâmetros, consulte [Get-RetentionPolicy](https://technet.microsoft.com/pt-br/library/dd298086\(v=exchg.150\)) e [Set-RetentionPolicy](https://technet.microsoft.com/pt-br/library/dd335196\(v=exchg.150\)).

## Remover diretivas de retenção de caixas de correio

Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada de \&quot;Aplicar políticas de retenção\&quot; no tópico [Permissões de política e conformidade de mensagens](messaging-policy-and-compliance-permissions-exchange-2013-help.md) .

Você pode impedir que uma diretiva de retenção se aplique a uma caixa de correio, removendo a diretiva das propriedades do usuário da caixa de correio.

Este exemplo do Shell remove a diretiva de retenção da caixa de correio jpeoples.

    Set-Mailbox jpeoples -RetentionPolicy $null.

Este exemplo do Shell remove a diretiva de retenção de todas as caixas de correio da organização do Exchange.

    Get-Mailbox -ResultSize unlimited -Filter {RetentionPolicy -ne $null} | Set-Mailbox -RetentionPolicy $null

Este exemplo do Shell remove a diretiva de retenção Corp-Finance de todos os usuário de caixas de correio que tenham a diretiva aplicada.

    Get-Mailbox -ResultSize unlimited -Filter {RetentionPolicy -eq "Corp-Finance"} | Set-Mailbox -RetentionPolicy $null

Para a sintaxe detalhada e informações sobre o parâmetro, consulte [Set-Mailbox](https://technet.microsoft.com/pt-br/library/bb123981\(v=exchg.150\)) e [Get-Mailbox](https://technet.microsoft.com/pt-br/library/bb123685\(v=exchg.150\)).

## Desativar o MRM permanentemente para toda a empresa

Para desligar o MRM para uma organização, exclua todas as marcas de retenção e as políticas de retenção para a política ArbritationMailbox, que é criada pela Instalação do Exchange. Após a finalização, as políticas de retenção são impostas.


> [!WARNING]
> As políticas de retenção também incluem etiquetas de Mover para Arquivo Morto, que movem as mensagem para a caixa de correio de arquivo morto do usuário. Se você remover uma política de retenção que possui uma etiqueta de Mover para Arquivo Morto, os usuários que tiveram essa política aplicada não terão mais as suas mensagens movidas para o arquivo morto pelo Assitente da Pasta Gerenciada.<BR>Para evitar que isso aconteça, remova somente as etiquetas de Excluir e Permitir Recuperação e Excluir Permanentemente da sua organizção e mantenha as políticas que possuem as etiquetas de Mover para Arquivo Morto aplicadas. De forma alternativa, os usuários que possuírem arquivo morto habilitado podem mover os itens manualmente para a caixa de correio de arquivo morto usando o Outlook ou Outlook Web App.<BR>Antes de remover as marcas de retenção ou as políticas de retenção, recomendamos que você verifique as configurações das etiquetas sendo removidas. Não exclua as etiquetas com a ação de retenção de Arquivo Morto.



Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada \&quot;Gerenciamento de registros de mensagens\&quot;, no tópico [Permissões de política e conformidade de mensagens](messaging-policy-and-compliance-permissions-exchange-2013-help.md).


> [!TIP]
> Inclua a opção <EM>WhatIf</EM> nos seguintes comandos para simular a ação tomada por um comando.



Este exemplo remove todas etiquetas excluídas de uma organização do Exchange exceto a etiqueta Nunca Excluir, que é usada na política ArbitrationMailbox criada pela Instalação do Exchange.

    Get-RetentionPolicyTag | ? {$_.RetentionAction -ne "MoveToArchive" -and $_.Name -ne "Never Delete"} | Remove-RetentionPolicyTag

Este exemplo remove todas marcas de retenção exceto a etiqueta Nunca Excluir.

    Get-RetentionPolicyTag | ? {$_.Name -ne "Never Delete"} | Remove-RetentionPolicyTag

Este comando remove a política de retenção Corp-Users de uma organização do Exchange.

    Remove-RetentionPolicy Corp-Users

Para obter informações detalhadas sobre sintaxes e parâmetros, consulte os seguintes tópicos:

  - [Get-RetentionPolicyTag](https://technet.microsoft.com/pt-br/library/dd298009\(v=exchg.150\))

  - [Remove-RetentionPolicyTag](https://technet.microsoft.com/pt-br/library/dd335092\(v=exchg.150\))

  - [Remove-RetentionPolicy](https://technet.microsoft.com/pt-br/library/dd297962\(v=exchg.150\))

