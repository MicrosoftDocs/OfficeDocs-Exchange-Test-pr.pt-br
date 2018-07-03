---
title: 'Modificar um relacionamento de organização: Exchange 2013 Help'
TOCTitle: Modificar um relacionamento de organização
ms:assetid: 3713ef83-f01a-41bb-b127-62ca242dd7a4
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/JJ673055(v=EXCHG.150)
ms:contentKeyID: 50485336
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Modificar um relacionamento de organização

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2015-01-01_

Um relacionamento de organização permite que os usuários em sua organização do Exchange compartilhem informações de disponibilidade de calendário com uma organização do Office 365 ou outra organização local do Exchange. Talvez você queira alterar as configurações de um relacionamento de organização, como o nome, desabilitar temporariamente o compartilhamento de calendário, alterar o nível de acesso ou alterar quais grupos de segurança compartilharão calendários.

Antes de você poder compartilhar calendários com outra organização, será preciso ter configurado um relacionamento de autenticação com a nuvem (também conhecido como "federação") e ter atendido aos requisitos mínimos de software. Para saber mais sobre compartilhamento federado, consulte [Compartilhamento](sharing-exchange-2013-help.md).

Para tarefas de gerenciamento adicionais relacionadas à dederação, consulte [Procedimentos de Federação](federation-procedures-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: 15 minutos.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o *Calendar and Sharing Permissions* Entrada no tópico [Permissões de destinatários](recipients-permissions-exchange-2013-help.md).

  - É preciso configurar uma relação de confiança de federação ativa para a organização do Exchange local.

  - A organização externa que você deseja configurar no relacionamento da organização também deve ter uma confiança de Federação estabelecida com o sistema de autenticação AD do Azure.

  - Os procedimentos neste tópico fazem alterações a um relacionamento de organização chamado Contoso. Os exemplos mostram como:
    
      - Adicionar um domínio chamado service.contoso.com à organização externa.
    
      - Desabilite o compartilhamento de disponibilidade para o relacionamento de organização.
    
      - Altere o nível de acesso de disponibilidade de *Calendar free/busy information with time, subject, and location* para *Calendar free/busy information with time only*.

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

## O que você deseja fazer?

## Usar o EAC para adicionar um domínio a um relacionamento de organização

1.  Em um servidor do Exchange 2013 na organização local, navegue até **organização** \> **compartilhamento**.

2.  Na visualização de lista, em **Compartilhamento da Organização**, selecione o relacionamento de organização Contoso e depois clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").

3.  Em **relacionamento de organização** \> **geral**, não altere o **Nome** do relacionamento da organização

4.  Na caixa **Domínios com os quais compartilhar**, insira o domínio **service.contoso.com** e clique em **Adicionar**![Ícone Adicionar](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Ícone Adicionar").

5.  Clique em **Salvar** para atualizar o relacionamento da organização.

## Usar o EAC para desabilitar o compartilhamento de disponibilidade para o relacionamento da organização

1.  Vá para **organização**\> **compartilhamento**.

2.  Nesta lista de exibição, em **Compartilhamento de Organização**, selecione o relacionamento de organização Contoso e depois clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").

3.  Em **relacionamento de organização**, clique em **compartilhamento**

4.  Selecione **Informações de disponibilidade de calendário somente com hora**.

5.  Clique em **Salvar** para atualizar o relacionamento da organização.

## Usar o EAC para alterar o nível de acesso de disponibilidade para o relacionamento da organização

1.  Vá para **organização**\> **compartilhamento**.

2.  Nesta lista de exibição, em **Compartilhamento de Organização**, selecione o relacionamento de organização Contoso e depois clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").

3.  Em **relacionamento de organização**, clique em **compartilhamento**

4.  Selecione **Informações de disponibilidade de calendário somente com hora**.

5.  Clique em **Salvar** para atualizar o relacionamento da organização.

## Usar o Shell para modificar um relacionamento da organização

  - Este exemplo adiciona o nome de domínio service.contoso.com ao relacionamento da organização Contoso.
    
        $domains = (Get-OrganizationRelationship Contoso).DomainNames
        $domains += 'service.contoso.com'
        Set-OrganizationRelationship -Identity Contoso -DomainNames $domains

  - Este exemplo desabilita o relacionamento da organização Contoso.
    
        Set-OrganizationRelationship -Identity Contoso -Enabled $false

  - Este exemplo habilita o acesso a informações de disponibilidade do calendário para o relacionamento de organização WoodgroveBank e define o nível de acesso como `AvailabilityOnly` (Informações de disponibilidade de calendário somente com hora).
    
        Set-OrganizationRelationship -Identity Contoso -FreeBusyAccessEnabled $true -FreeBusyAccessLevel AvailabilityOnly

Para obter informações detalhadas sobre sintaxe e parâmetros, consulte [Get-OrganizationRelationship](https://technet.microsoft.com/pt-br/library/ee332343\(v=exchg.150\)) e [Set-OrganizationRelationship](https://technet.microsoft.com/pt-br/library/ee332326\(v=exchg.150\)).

## Como saber se funcionou?

Para verificar se você atualizou o relacionamento da organização com êxito, execute o comando do Shell a seguir e verifique as informações do relacionamento da organização:

    Get-OrganizationRelationship | format-list


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>.


