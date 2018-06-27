---
title: 'Desabilitar a publicação de calendário da Internet: Exchange 2013 Help'
TOCTitle: Desabilitar a publicação de calendário da Internet
ms:assetid: f26dbf04-9dae-460f-a987-2ad3dfbc7b7e
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/JJ853047(v=EXCHG.150)
ms:contentKeyID: 50556310
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Desabilitar a publicação de calendário da Internet

 

_**Aplica-se a:**Exchange Server 2013_

_**Tópico modificado em:**2014-02-15_

Como desabilitar a publicação de calendário de Internet depende de como você a habilitou. Se você tiver criado uma política de compartilhamento dedicada à publicação de calendário da Internet, você poderá desabilitar a política ou excluí-la totalmente. Se você tiver configurado a publicação de calendário de Internet como uma regra de compartilhamento na política de compartilhamento padrão, basta remover a regra de compartilhamento do domínio **Anônimo**.

Quando você desabilitar a publicação de calendário da Internet, os usuários que podem usar a política de compartilhamento não poderão compartilhar informações de calendário com o domínio **Anônimo** na Internet especificado na política. Entretanto, você não pode excluir ou desabilitar uma política de compartilhamento dedicada à publicação de calendário da Internet, até que todos os usuários provisionados para usar essa política tenham a configuração de política removida de suas caixas de correio. Para detalhes sobre como alterar a configuração de política para um usuário, consulte [Gerenciar caixas de correio do usuário](manage-user-mailboxes-exchange-2013-help.md).


> [!TIP]
> Quando uma política de compartilhamento é habilitada ou desabilitada, os usuários provisionados para usar a política continuam compartilhando informações até que o Assistente de Política de Compartilhamento seja executada. Para especificar com que frequência o Assistente de Política de Compartilhamento será executado, use o cmdlet <A href="https://technet.microsoft.com/pt-br/library/aa998651(v=exchg.150)">Set-MailboxServer</A> com o parâmetro <EM>SharingPolicySchedule</EM>.



Para desabilitar completamente a publicação de calendário na Internet, você deve também desabilitar o diretório virtual do Outlook Web App utilizado para a publicação do calendário. Isso proibirá o acesso aos links de calendários publicados que antes eram compartilhados pelos usuários de sua organização do Exchange com usuários externos na Internet. Esta etapa é detalhada posteriormente neste tópico.

Para saber mais sobre publicação de calendário na Internet e diretivas de compartilhamento, consulte [Compartilhamento](sharing-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para a conclusão da tarefa: 15 minutos.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Calendário e Permissões de Compartilhamento" no tópico [Permissões de destinatários](recipients-permissions-exchange-2013-help.md).

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>.



## Como fazer isso?

## Etapa 1: Usar o EAC ou o Shell para desabilitar ou excluir a política de compartilhamento para publicação de calendário da Internet

## Usar o EAC

1.  Navegue até **Organização** \> **Compartilhamento**.

2.  No modo de exibição de lista, em **Compartilhamento Individual**, siga uma destas instruções:
    
      - Se você tiver criado uma política de compartilhamento especificamente para publicação de calendário da Internet, selecione essa política e desmarque a caixa de seleção na coluna **Ativado**, para desabilitar a política, ou clique em **Excluir**![Excluir ícone](images/JJ673559.14f639f6-61e8-4418-bbfb-0db14de9d2f5(EXCHG.150).gif "Excluir ícone"), para excluí-la.
    
      - Se você tiver configurado a publicação de calendário da Internet como uma regra de compartilhamento em uma política de compartilhamento padrão, siga estas instruções:
        
        1.  Selecione a política de compartilhamento padrão e clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").
        
        2.  Em **política de compartilhamento**, selecione a regra de compartilhamento **Anônimo** e clique em **Remover**![ícone Remover](images/JJ657492.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "ícone Remover") para remover a regra de compartilhamento.
        
        3.  Clique em **Salvar**.

## Usar o Shell

Este exemplo desabilita a política de compartilhamento de publicação de calendário da Internet chamada **Internet**.

    Set-SharingPolicy -Identity "Internet" -Enabled $false

Este exemplo exclui uma política de compartilhamento de publicação de calendário da Internet chamada **Internet**.

    Remove-SharingPolicy -Identity "Internet"

Para obter informações detalhadas sobre sintaxe e parâmetros, consulte [Set-SharingPolicy](https://technet.microsoft.com/pt-br/library/dd297931\(v=exchg.150\)).

## Como saber se essa etapa funcionou?

Para verificar se você removeu ou atualizou a política de compartilhamento com êxito, execute o seguinte comando do Shell e verifique as informações de política de compartilhamento.

    Get-SharingPolicy <policy name> | format-list

Se você tiver removido a política de compartilhamento de publicação de calendário da Internet dedicada, você não verá a política nos resultados do cmdlet.

Se você tiver atualizado a política de compartilhamento padrão, verifique se o domínio `Anonymous` foi removido do parâmetro *Domains*.

Para obter informações detalhadas sobre sintaxe e parâmetros, consulte [Get-SharingPolicy](https://technet.microsoft.com/pt-br/library/dd335081\(v=exchg.150\)).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>.



## Etapa 2: Usar o Shell para desabilitar os recursos de Anônimo do diretório virtual do Outlook Web App


> [!TIP]
> Você não pode usar o EAC para desabilitar os recursos de Anônimo do diretório virtual do Outlook Web App.



Este exemplo desabilita os recursos de Anônimo para o diretório virtual do Outlook Web App no servidor de Acesso para Cliente CAS01.

    Set-OwaVirtualDirectory -Identity "CAS01" - AnonymousFeaturesEnabled -$false

Para obter informações detalhadas sobre sintaxe e parâmetros, consulte [Set-OwaVirtualDirectory](https://technet.microsoft.com/pt-br/library/bb123515\(v=exchg.150\)).

## Como saber se essa etapa funcionou?

Para verificar se você desabilitou com êxito os recursos de Anônimo do diretório virtual do Outlook Web App no servidor de Acesso para Cliente, execute este comando do Shell e verifique se o parâmetro *AnonymousFeaturesEnabled* está como `$false`.

    Get-OwaVirtualDirectory | format-list

Para obter informações detalhadas sobre sintaxe e parâmetros, consulte [Get-OwaVirtualDirectory](https://technet.microsoft.com/pt-br/library/aa998588\(v=exchg.150\)).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>.


