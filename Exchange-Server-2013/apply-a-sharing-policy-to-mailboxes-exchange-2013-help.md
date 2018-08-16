---
title: 'Aplicar política de compartilhamento às caixas de correio: Exchange 2013 Help'
TOCTitle: Aplicar uma política de compartilhamento às caixas de correio
ms:assetid: dd4cc765-8469-4176-bb6e-d5b0f5235927
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/JJ657501(v=EXCHG.150)
ms:contentKeyID: 50486854
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Aplicar uma política de compartilhamento às caixas de correio

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2014-02-15_

As políticas de compartilhamento são uma parte do compartilhamento federado e permitem o compartilhamento estabelecido pelo usuário, de pessoa para pessoa, das informações de calendário com tipos diferentes de usuários externos. A política de compartilhamento que o administrador aplica à caixa de correio do usuário determina até qual nível de compartilhamento o usuário tem acesso e com quem ele pode compartilhar. Se você não alterar algo, a política de compartilhamento padrão será aplicada a todos os usuários. Se você criar uma nova política de compartilhamento, terá que aplicá-la às caixas de correio antes que ela entre em vigor. Uma política de compartilhamento pode ser aplicada a uma caixa de correio de usuário única ou a várias caixas de correio de usuário simultaneamente. O administrador também pode desabilitar políticas de compartilhamento de usuários para evitar o acesso externo aos calendários.

Para saber mais sobre compartilhamento federado, consulte [Compartilhamento](sharing-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: 5 minutos.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o *Recipient Provisioning Permissions* Entrada no tópico [Permissões de destinatários](recipients-permissions-exchange-2013-help.md).

  - Uma política de compartilhamento deve existir. Para detalhes, consulte [Criar uma política de compartilhamento](create-a-sharing-policy-exchange-2013-help.md).

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

## O que você deseja fazer?

## Usar o EAC para aplicar uma política de compartilhamento a uma única caixa de correio

1.  Navegue até **destinatários** \> **caixas de correio**.

2.  Na exibição de lista, selecione a caixa de correio desejada e clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").

3.  Em **Caixa de Correio do Usuário**, clique em **Recursos da Caixa de Correio**.

4.  Na lista **Política de compartilhamento**, selecione a política de compartilhamento que você deseja aplicar a essa caixa de correio.

5.  Clique em **Salvar** para aplicar a política de compartilhamento.

## Usar o EAC para aplicar uma política de compartilhamento a várias caixas de correio

1.  Navegue até **destinatários** \> **caixas de correio**.

2.  No modo de exibição de lista, segure a tecla Ctrl enquanto seleciona diversas caixas de correio.

3.  No painel de detalhes, as propriedades de caixa de correio serão configuradas para edição em massa. Clique em **Mais opções**.

4.  Em **Política de compartilhamento**, clique em **Atualizar**.

5.  Em **atribuir política de compartilhamento em massa**, use a lista **Selecionar a política de compartilhamento** para escolher uma política de compartilhamento para atribuir às caixas de correio.

6.  Clique em **Salvar** para aplicar a política de compartilhamento às caixas de correio selecionadas.

## Usar o Shell para aplicar uma política de compartilhamento a uma ou mais caixas de correio

Este exemplo aplica a política de compartilhamento Contoso a uma caixa de correio única para o usuário Barbara.

    Set-Mailbox -Identity Barbara -SharingPolicy "Contoso"

Este exemplo especifica que todas as caixas de correio de usuário do departamento de Marketing devem usar a política de compartilhamento Marketing da Contoso.

    Get-Mailbox -Filter {Department -eq "Marketing"} | Set-Mailbox -SharingPolicy "Contoso Marketing"

Este exemplo retorna todas as caixas de correio que tenham a política de compartilhamento Contoso aplicada e organiza os usuários em uma tabela que exibe apenas seus aliases e endereços de email.

    Get-Mailbox -ResultSize unlimited | Where {$_.SharingPolicy -eq "Contoso" } | format-table Alias, EmailAddresses

Para obter informações detalhadas sobre sintaxe e parâmetros, consulte [Set-Mailbox](https://technet.microsoft.com/pt-br/library/bb123981\(v=exchg.150\)) e [Get-Mailbox](https://technet.microsoft.com/pt-br/library/bb123685\(v=exchg.150\)).

## Como saber se funcionou?

Para verificar se você aplicou com êxito a política de compartilhamento a uma caixa de correio de usuário, siga um destes procedimentos:

  - No EAC, navegue até **Destinatários** \> **Caixas de Correio** e selecione a caixa de correio à qual aplicou a política de compartilhamento. Clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição"), em **recursos da caixa de correio** e confirme que a política de compartilhamento correta está sendo exibida na lista **Política de Compartilhamento**.

  - Execute o seguinte comando do Shell para verificar se a política de compartilhamento foi atribuída a uma caixa de correio de usuário. Verifique se a política de compartilhamento correta está listada no parâmetro *SharingPolicy*.
    
        Get-Mailbox <user name> | format-list


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>.


