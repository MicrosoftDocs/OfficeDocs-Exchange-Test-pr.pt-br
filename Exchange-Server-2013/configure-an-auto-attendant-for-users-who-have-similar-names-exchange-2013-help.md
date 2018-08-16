
---
title: 'Configurar um atendedor automático para usuários que tenham nomes semelhantes'
TOCTitle: Configurar um atendedor automático para usuários que tenham nomes semelhantes
ms:assetid: 2e7318a0-67f9-4d7b-8300-5f0ef77656a8
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Aa997135(v=EXCHG.150)
ms:contentKeyID: 52058389
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configurar um atendedor automático para usuários que tenham nomes semelhantes

 

_**Aplica-se a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Tópico modificado em:** 2012-12-16_

Você pode configurar o método a ser usado para usuários com nomes semelhantes nas opções **Catálogo de endereços e acesso do operador** de um atendedor automático ou pode deixar a configuração padrão no atendedor automático e definir essa configuração no plano de discagem associado ao atendedor automático. Por padrão, um atendedor automático não é capaz de distinguir entre dois ou mais usuários que tenham o mesmo nome ou nomes semelhantes porque a configuração padrão do atendedor automático é **Herdar de plano de discagem**.


> [!TIP]
> Para que as informações que serão incluídas para usuários com nomes semelhantes funcionem corretamente, você deverá fornecer informações sobre o cargo, o departamento e a localização dos destinatários da organização do Microsoft Exchange.



Para conhecer tarefas de gerenciamento adicionais relacionadas a atendedores automáticos de UM, consulte [Procedimentos atendedor automático a Unificação de mensagens](um-auto-attendant-procedures-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: Menos de 1 minuto.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Atendedores automáticos de UM", no tópico [Permissões de mensagens unificadas](unified-messaging-permissions-exchange-2013-help.md).

  - Antes de executar esses procedimentos, confirme se um plano de discagem de UM foi criado. Para conhecer etapas detalhadas, consulte [Criar um plano de discagem de UM](create-a-um-dial-plan-exchange-2013-help.md).

  - Antes de executar esses procedimentos, verifique se um plano de discagem de UM foi criado. Para conhecer etapas detalhadas, consulte [Criar um Atendedor Automático da UM](create-a-um-auto-attendant-exchange-2013-help.md).

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>..



## O que você deseja fazer?

## Usar o EAC para configurar um atendedor automático do UM para usuários com nomes semelhantes

1.  No EAC, navegue até **Unificação de Mensagens** \> **Planos de discagem de UM**. Na exibição de lista, selecione o plano de discagem de UM que você deseja modificar e clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").

2.  Na página **Plano de Discagem da UM**, em **Atendedores Automáticos da UM**, selecione o atendedor automático da UM que deseja alterar e clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").

3.  Na página **Atendedor Automático da UM**, clique em **Catálogo de endereços e acesso de operador** e, em **Informações a serem incluídas para usuários com o mesmo nome**, selecione uma destas opções:
    
      - **Cargo**O atendedor automático incluirá o cargo de cada usuário quando ele listar as correspondências.
    
      - **Departamento**   O atendedor automático incluirá o departamento de cada usuário quando ele listar as correspondências.
    
      - **Local**   O atendedor automático incluirá o local de cada usuário quando ele listar as correspondências.
    
      - **Nenhum**   O atendedor automático não incluirá nenhuma informação adicional quando ele listar as correspondências.
    
      - **Solicitar alias**   O atendedor automático solicitará ao chamador o alias do usuário.
    
      - **Herdar do plano de discagem**   O atendedor automático usará a configuração padrão do plano de discagem associado ao atendedor automático.

4.  Clique em **Salvar**.

## Usar o Shell para configurar um atendedor automático da UM para usuários com nomes semelhantes

Este exemplo define as informações a serem incluídas com usuários com nomes semelhantes em Solicitar Alias para um atendedor automático da UM chamado `MyUMAutoAttendant`.

    Set-UMAutoAttendant -Identity MyUMAutoAttendant -MatchedNameSelectionMethod PromptForAlias

Este exemplo define as informações a serem incluídas com usuários com nomes semelhantes no cargo dos usuários, habilita pesquisas de nome e permite que chamadores que discarem para o atendedor automático para pressionar \* vejam a saudação de boas-vindas do Outlook Voice Access de um atendedor automático da UM chamado `MyUMAutoAttendant`.

    Set-UMAutoAttendant -Identity MyUMAutoAttendant -MatchedNameSelectionMethod Title -NameLookupEnabled $true -StarOutToDialPlanEnabled $true

