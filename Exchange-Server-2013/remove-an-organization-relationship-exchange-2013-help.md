---
title: 'Remover um relacionamento de organização: Exchange 2013 Help'
TOCTitle: Remover um relacionamento de organização
ms:assetid: ff211394-f58b-4da7-bb3a-df6abcb5950e
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/JJ657513(v=EXCHG.150)
ms:contentKeyID: 50487090
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Remover um relacionamento de organização

 

_**Aplica-se a:**Exchange Server 2013_

_**Tópico modificado em:**2015-01-04_

Uma relação de organização permite que os usuários em sua organização do Exchange compartilhem informações de disponibilidade do calendário com uma organização do Office 365 ou com outra organização local do Exchange. Você pode remover uma relação de organização para desabilitar o compartilhamento de calendário com a outra organização.

Para poder compartilhar calendários com outra organização, você precisa configurar um relacionamento de autenticação com o sistema de autenticação Azure Active Directory (também conhecido como "federação") e deve atender aos requisitos mínimos de software. Para saber mais sobre compartilhamento federado, consulte [Compartilhamento](sharing-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: 5 minutos.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Seção "Calendário e Permissões de Compartilhamento" no tópico [Permissões de destinatários](recipients-permissions-exchange-2013-help.md).

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

## O que você deseja fazer?

## Usar o EAC para remover um relacionamento da organização

1.  Em um servidor do Exchange 2013 na organização local, navegue até **organização** \> **compartilhamento**.

2.  Em **Compartilhamento de Organização**, selecione um relacionamento de organização e clique em **Excluir**![Excluir ícone](images/JJ673559.14f639f6-61e8-4418-bbfb-0db14de9d2f5(EXCHG.150).gif "Excluir ícone") para remover um relacionamento de organização.

3.  No aviso exibido, clique em **sim**.

## Usar o Shell para remover um relacionamento da organização

Este exemplo remove o relacionamento da organização Contoso da organização do Exchange

    Remove-OrganizationRelationship -Identity "Contoso"

Para informações detalhadas de sintaxes e de parâmetros, consulte [Remove-OrganizationRelationship](https://technet.microsoft.com/pt-br/library/ee332362\(v=exchg.150\)).

## Como saber se funcionou?

Para verificar se você removeu com êxito o relacionamento de organização, proceda de uma das seguintes formas:

  - No EAC, navegue até **Organização** \> **Compartilhamento** e verifique se o relacionamento da organização está sendo exibido na exibição em lista sob **Compartilhamento da organização**.

  - Execute o seguinte comando do Shell para verificar se as informações de relacionamento da organização foram removidas.
    
        Get-OrganizationRelationship | Format-List


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>.


