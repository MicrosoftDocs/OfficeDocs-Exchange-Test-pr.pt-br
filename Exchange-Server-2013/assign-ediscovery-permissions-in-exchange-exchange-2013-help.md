---
title: 'Atribuir permissões de descoberta eletrônica no Exchange: Exchange 2013 Help'
TOCTitle: Atribuir permissões de descoberta eletrônica no Exchange
ms:assetid: 729e09d8-614b-431f-ae04-ae41fb4c628e
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Dd298059(v=EXCHG.150)
ms:contentKeyID: 50485922
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Atribuir permissões de descoberta eletrônica no Exchange

 

_**Aplica-se a:** Exchange Online, Exchange Server 2013_

_**Tópico modificado em:** 2014-10-02_

Se desejar que os usuários sejam capazes de usar o Microsoft Exchange Server 2013 In-Place eDiscovery, você deve primeiro autorizá-los adicionando-os ao grupo de funções de gerenciamento de descoberta. Membros do grupo de função Gerenciamento de Descobertas tem permissões de caixa de correio de acesso total para a caixa de correio de descoberta criada por Exchange instalação.


> [!WARNING]
> Membros do grupo de função de gerenciamento de descoberta podem acessar o conteúdo da mensagem confidenciais. Especificamente, esses membros podem usar <A href="in-place-ediscovery-exchange-2013-help.md">Descoberta Eletrônica In-loco</A> para pesquisar todas as caixas de correio em sua organização do Exchange, visualização mensagens (e outros itens de caixa de correio), copiá-los para uma caixa de correio de descoberta e exportar as mensagens copiadas para um arquivo. pst. Na maioria das organizações, esta permissão é concedida para a equipe de recursos humanos, conformidade ou legais.<BR>



Para saber mais sobre o grupo de funções de gerenciamento de descoberta, consulte [Gerenciamento de Descobertas](discovery-management-exchange-2013-help.md). Para saber mais sobre Role Based Access controle (RBAC), consulte [Controle de acesso baseado em função de compreensão](understanding-role-based-access-control-exchange-2013-help.md).

Interessado em cenários em que esse procedimento é usado? Consulte os seguintes tópicos:

  - [Criar uma pesquisa de Descoberta Eletrônica In-loco](create-an-in-place-ediscovery-search-exchange-2013-help.md)

  - [Criar ou remover um bloqueio In-loco](create-or-remove-an-in-place-hold-exchange-2013-help.md)

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: 1 minuto.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Grupos de função" no tópico [Permissões de gerenciamento de função](role-management-permissions-exchange-2013-help.md) .

  - Por padrão, o grupo de funções Gerenciamento de Descobertas não contêm quaisquer membros. Os administradores com a função Gerenciamento da Organização também são não é possível criar ou gerenciar pesquisas de descoberta sem serem adicionados ao grupo de funções Gerenciamento de Descobertas.

  - No Exchange 2013, os membros do grupo de função Gerenciamento da Organização podem criar um [Retenção local e Retenção de litígio](in-place-hold-and-litigation-hold-exchange-2013-help.md) para colocar todo o conteúdo de caixa de correio em espera. No entanto, para criar um bloqueio In-loco de baseado em consulta, o usuário deve ser membro do grupo de funções de gerenciamento de descoberta ou ter a função de pesquisa de caixa de correio atribuída.

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

## Usar o EAC para adicionar um usuário ao grupo de funções de gerenciamento de descoberta

1.  Acesse **permissões** \> **funções de administrador**.

2.  Na exibição de lista, selecione **Gerenciamento de descoberta** e clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição")

3.  No **Grupo de função**, em **membros**, clique em **Adicionar**![Ícone Adicionar](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Ícone Adicionar").

4.  Em **Selecionar membros**, selecione um ou mais usuários, clique em **Adicionar** e, em seguida, clique em **OK**.

5.  No **Grupo de função**, clique em **Salvar**.

## Usar o Shell para adicionar um usuário ao grupo de funções de gerenciamento de descoberta

Este exemplo adiciona o usuário Bsuneja ao grupo de funções de gerenciamento de descoberta.

    Add-RoleGroupMember -Identity "Discovery Management" -Member Bsuneja

Para detalhadas sobre sintaxe e informações de parâmetro, consulte [Add-RoleGroupMember](https://technet.microsoft.com/pt-br/library/dd638207\(v=exchg.150\)).

## Como saber se funcionou?

Para verificar se adicionou o usuário ao grupo de funções de gerenciamento de descoberta, faça o seguinte:

1.  No EAC, vá para **permissões** \> **funções de administrador**.

2.  Na exibição de lista, selecione **Gerenciamento de descoberta**.

3.  No painel de detalhes, verifique se o usuário é listado em **membros**.

Você também pode executar este comando para listar os membros do grupo de funções de gerenciamento de descoberta.

    Get-RoleGroupMember -Identity "Discovery Management"


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>.


