---
title: 'Configurar um número do Outlook Voice Access: Exchange 2013 Help'
TOCTitle: Configurar um número do Outlook Voice Access
ms:assetid: 443c838e-f266-4893-b6b2-e5fc96579b55
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Aa997680(v=EXCHG.150)
ms:contentKeyID: 50556176
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configurar um número do Outlook Voice Access

 

_**Aplica-se a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Tópico modificado em:** 2016-12-09_

Um número do Outlook Voice Access permite que um usuário que esteja habilitado para a Unificação de Mensagens (UM) e caixa postal acesse sua caixa de correio usando o Outlook Voice Access. Quando você configura um número do Outlook Voice Access ou de acesso do assinante em um plano de discagem, usuários habilitados para UM podem ligar para o número, fazer logon em sua caixa de correio e acessar seus emails, mensagens de voz, calendário e informações de contato pessoais.

Por padrão, quando você cria um plano de discagem de UM, nenhum número do Outlook Voice Access é configurado. Para configurar um número do Outlook Voice Access, primeiro, é necessário criar o plano de discagem e depois configurar um número do Outlook Voice Access na opção **Outlook Voice Access** do plano de discagem. Embora um número do Outlook Voice Access não seja necessário, você deve configurar pelo menos um número do Outlook Voice Access para permitir que um usuário habilitado para UM use o Outlook Voice Access para acessar sua caixa de correio. Você pode configurar vários números do Outlook Voice Access para um único plano de discagem.

Os números do Outlook Voice Access podem conter caracteres alfanuméricos, numéricos e especiais, separadores e espaços. Por exemplo:

  - \+14255551010

  - \+1-425-555-1010

  - 4255551010

  - \+1 425 555 1010

  - 1-800-555-CALL

Para obter mais informações sobre as opções de menu disponíveis para usuários do Outlook Voice Access, consulte o guia de referência rápida para Outlook Voice Access, que é disponível a partir do [Centro de Download da Microsoft](https://go.microsoft.com/fwlink/p/?linkid=64645).

Para mais tarefas de gerenciamento relacionadas a planos de discagem de UM, consulte [Procedimentos de plano de discagem de UM](um-dial-plan-procedures-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: Menos de 1 minuto.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Planos de discagem da UM" no tópico [Permissões de mensagens unificadas](unified-messaging-permissions-exchange-2013-help.md).

  - Antes de executar esses procedimentos, confirme se um plano de discagem de UM foi criado. Para obter etapas detalhadas, consulte [Criar um plano de discagem de UM](create-a-um-dial-plan-exchange-2013-help.md).

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>..



## O que você deseja fazer?

## Usar o EAC para configurar um número de acesso do Outlook Voice Access

1.  No EAC, navegue até **Unificação de Mensagens** \> **Planos de discagem de UM**.

2.  Na exibição de lista, selecione o plano de discagem de UM que você deseja modificar e, na barra de ferramentas, clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").

3.  Na página **Plano de discagem de UM**, clique em **Configurar**.

4.  No **Outlook Voice Access**, em **Números do Outlook Voice Access**, use a caixa para inserir o número que deseja usar e depois clique em **Adicionar**![Ícone Adicionar](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Ícone Adicionar").

5.  Clique em **Salvar**.

## Usar o Shell para configurar um número do Outlook Voice Access

Este exemplo define o número de acesso do Outlook Voice Access como 4255550100 para um plano de discagem de UM chamado `MyUMDialPlan`.

    Set-UMDialPlan -identity MyUMDialPlan -AccessTelephoneNumbers 4255550100

