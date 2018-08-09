---
title: 'Habilitar indicador de espera de mensagem (MWI) p/ usuário: Exchange 2013 Help'
TOCTitle: Habilitar o indicador de espera de mensagem (MWI) para usuários
ms:assetid: 3d0ca657-00b6-4108-a850-b092fede1f75
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Dd335216(v=EXCHG.150)
ms:contentKeyID: 50556168
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Habilitar o indicador de espera de mensagem (MWI) para usuários

 

_**Aplica-se a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Tópico modificado em:** 2013-02-21_

Você pode habilitar ou desabilitar o Indicador de Mensagens em Espera para usuários associados a uma política de caixa de correio de UM (Unificação de Mensagens). Indicador de Espera da Mensagem é um recurso encontrado na maioria dos sistemas de caixa postal legados. Em sua forma mais comum, uma luz no telefone do assinante de mensagens de voz acende para indicar a presença de uma nova mensagem de caixa postal. O Indicador de Mensagens em Espera também pode enviar uma mensagem de texto para o telefone celular de um usuário habilitado para UM. A configuração padrão é Habilitado.

Se o Indicador de Mensagens em Espera estiver desabilitado no gateway IP de UM, o recurso não estará disponível para usuários habilitados para UM associados à política de caixa de correio de UM.

Para conhecer tarefas de gerenciamento adicionais relacionadas a políticas de caixa de correio de UM, consulte [Procedimentos de diretiva de caixa de correio de Unificação de mensagens](um-mailbox-policy-procedures-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: Menos de 1 minuto.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Diretivas de caixa de correio da UM" no tópico [Permissões de mensagens unificadas](unified-messaging-permissions-exchange-2013-help.md).

  - Antes de executar esses procedimentos, confirme se um plano de discagem de UM foi criado. Para obter etapas detalhadas, consulte [Criar um plano de discagem de UM](create-a-um-dial-plan-exchange-2013-help.md).

  - Antes de executar esses procedimentos, verifique se uma política de caixa de correio de UM foi criada. Para conhecer etapas detalhadas, consulte [Criar uma política de caixa de correio da UM](create-a-um-mailbox-policy-exchange-2013-help.md).

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>..



## O que você deseja fazer?

## Usar o EAC para habilitar o Indicador de Mensagens em Espera

1.  No EAC, navegue até **Unificação de Mensagens** \> **Planos de discagem de UM**. Na exibição de lista, selecione o plano de discagem de UM que você deseja modificar e clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").

2.  Em **Políticas de Caixa de Correio de UM**, selecione a política de caixa de correio de UM que você deseja gerenciar e clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").

3.  Na página **Política de Caixa de Correio da UM**, marque a caixa de seleção ao lado de **Permitir Indicador de Mensagem em Espera**.

4.  Clique em **Salvar**.

## Usar o Shell para habilitar o Indicador de Mensagens em Espera

Essa exemplo habilita o Indicador de Mensagens em Espera para usuários associados à política de caixa de correio da UM chamada `MyUMMailboxPolicy`.

    Set-UMMailboxPolicy -identity MyUMMailboxPolicy -AllowMessageWaitingIndicator $true

