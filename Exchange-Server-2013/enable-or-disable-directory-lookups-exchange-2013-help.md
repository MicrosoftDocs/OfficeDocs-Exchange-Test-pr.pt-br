---
title: 'Habilitar ou desabilitar pesquisas de diretório: Exchange 2013 Help'
TOCTitle: Habilitar ou desabilitar pesquisas de diretório
ms:assetid: c0768815-8578-4385-8d4c-7d1e40304cec
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Ee423557(v=EXCHG.150)
ms:contentKeyID: 52058490
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Habilitar ou desabilitar pesquisas de diretório

 

_**Aplica-se a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Tópico modificado em:** 2016-05-10_

Você pode habilitar pesquisas de diretório para que os chamadores que ligam para um atendedor automático de Unificação de mensagens (UM) podem pesquisar nomes no diretório usando o teclado de seus telefones, mas não conseguir pesquisar o diretório usando entradas de voz. Essa configuração estiver habilitada por padrão. Se essa configuração estiver desativada, os chamadores não será capazes de pesquisar o diretório para uma pessoa específica usando discagem por tom ou comandos de voz.

Para conhecer tarefas de gerenciamento adicionais relacionadas a atendedores automáticos de UM, consulte [Procedimentos atendedor automático a Unificação de mensagens](um-auto-attendant-procedures-exchange-2013-help.md).


> [!TIP]
> Outlook usuários Voice Access não podem usar o reconhecimento automático de fala (ASR) ou entradas de fala para localizar usuários no diretório, eles só podem usar DTMF ou entradas de toque.



## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: Menos de 1 minuto.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Atendedores automáticos da UM" no tópico [Permissões de mensagens unificadas](unified-messaging-permissions-exchange-2013-help.md).

  - Antes de executar esses procedimentos, confirme se um plano de discagem da UM foi criado. Para obter etapas detalhadas, consulte [Criar um plano de discagem de UM](create-a-um-dial-plan-exchange-2013-help.md).

  - Antes de executar esses procedimentos, verifique se um plano de discagem de UM foi criado. Para conhecer etapas detalhadas, consulte [Criar um Atendedor Automático da UM](create-a-um-auto-attendant-exchange-2013-help.md).

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>..



## O que você deseja fazer?

## Usar o EAC para habilitar ou desabilitar pesquisas de diretório

1.  No EAC, navegue até **Unificação de Mensagens** \> **Planos de discagem de UM**. Na exibição de lista, selecione o plano de discagem de UM que você deseja modificar e clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").

2.  Na página **Plano de discagem de UM**, em **Atendedores automáticos de UM**, selecione o atendedor automático de UM para o qual você deseja habilitar ou desabilitar pesquisas de diretório e, em seguida, clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").

3.  Na página de **Atendedor automático de UM** \> **Catálogo de endereços e o operador de acesso**, em **Opções para pesquisar o catálogo de endereços**, marque a caixa de seleção ao lado de **Permitir que os chamadores para procurar usuários por nome ou alias** para permitir que os chamadores procurar usuários. Para desabilitar os chamadores de verificação ortográfica para usuários, desmarque essa caixa de seleção.

4.  Clique em **Salvar**.

## Usar o Shell para habilitar ou desabilitar pesquisas de diretório

Este exemplo desativa as pesquisas de diretório em um atendedor automático de UM chamado `MyUMAutoAttendant`.

    Set-UMAutoAttendant -Identity MyUMAutoAttendant -NameLookupEnabled $false

