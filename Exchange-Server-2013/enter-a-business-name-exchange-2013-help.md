---
title: 'Insira um nome de empresa: Exchange 2013 Help'
TOCTitle: Insira um nome de empresa
ms:assetid: a0e7cb24-0f55-442d-8ae2-21b177940b78
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Ee423549(v=EXCHG.150)
ms:contentKeyID: 50556248
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Insira um nome de empresa

 

_**Aplica-se a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Tópico modificado em:** 2013-04-19_

Você pode inserir o nome do seu negócio na caixa **nome de negócios** em um atendedor automático. Por padrão, nenhum nome de negócios é inserido. Se você inserir um nome de empresa, uma saudação prompt com o nome de empresa de padrão será reproduzida para chamadores quando ele liga para o atendedor automático de Unificação de mensagens (UM).

Para tarefas adicionais relacionadas a atendedores automáticos, consulte [Procedimentos atendedor automático a Unificação de mensagens](um-auto-attendant-procedures-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: Menos de 1 minuto.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Atendedores automáticos da UM" no tópico [Permissões de mensagens unificadas](unified-messaging-permissions-exchange-2013-help.md).

  - Antes de executar esses procedimentos, confirme se um plano de discagem da UM foi criado. Para obter etapas detalhadas, consulte [Criar um plano de discagem de UM](create-a-um-dial-plan-exchange-2013-help.md).

  - Antes de executar esses procedimentos, verifique se um plano de discagem de UM foi criado. Para conhecer etapas detalhadas, consulte [Criar um Atendedor Automático da UM](create-a-um-auto-attendant-exchange-2013-help.md).

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>..



## O que você deseja fazer?

## Usar o EAC para configurar um nome de empresa

1.  No EAC, navegue até **Unificação de Mensagens** \> **Planos de discagem de UM**. Na exibição de lista, selecione o plano de discagem de UM que você deseja modificar e clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").

2.  Na página **Plano de discagem de UM**, em **Atendedores automáticos de UM**, selecione o atendedor automático de UM para o qual você deseja definir um nome de negócios e, na barra de ferramentas, clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").

3.  Na página de **Atendedor automático de UM** \> **Geral**, em **nome de empresa**, digite o nome da empresa.

4.  Clique em **Salvar**.

## Use o Shell para configurar um nome de empresa

Este exemplo define o nome de empresa em um atendedor automático de UM chamado `MyUMAutoAttendant`.

    Set-UMAutoAttendant -Identity MyUMAutoAttendant -BusinessName "Northwind Traders"

