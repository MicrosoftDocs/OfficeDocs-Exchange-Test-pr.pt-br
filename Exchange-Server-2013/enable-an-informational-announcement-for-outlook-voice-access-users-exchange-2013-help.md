---
title: 'Habilitar um informe para usuários do Outlook Voice Access: Exchange 2013 Help'
TOCTitle: Habilitar um informe para usuários do Outlook Voice Access
ms:assetid: b69ed0e1-f978-498a-963e-42a047678db4
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Bb124344(v=EXCHG.150)
ms:contentKeyID: 50556285
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Habilitar um informe para usuários do Outlook Voice Access

 

_**Aplica-se a:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Tópico modificado em:**2016-12-09_

É possível habilitar um informe em um plano de discagem de Unificação de mensagens (UM). Anúncios informativos são usados para comunicados gerais que alteração com mais frequência que a saudação de boas-vindas faz ou para os comunicados que são exigidos por políticas de conformidade corporativa.

Por padrão, os chamadores, incluindo usuários de acesso de voz Outlook que discam para um número de Outlook Voice Access estiver configurado, não ouvem um informe. Se desejar que um a ser reproduzido, você deve criar um. wav ou. wma arquivo a ser usado para o informe depois que você crie um UM plano de discagem e habilite o informe no plano de discagem.

Quando é importante que o informe toda é ouvido, você pode configurar o comunicado a ser ininterrupto. Isso impede que um chamador desde pressionando uma tecla ou falando de um comando para interromper e parar o comunicado.

Para obter mais informações sobre as opções de menu que estão disponíveis para usuários com acesso de voz Outlook, consulte o guia de referência rápida para Outlook Voice Access, que é disponível a partir do [Centro de Download Microsoft](https://go.microsoft.com/fwlink/p/?linkid=272767).

Para mais tarefas de gerenciamento relacionadas a planos de discagem de UM, consulte [Procedimentos de plano de discagem de UM](um-dial-plan-procedures-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: Menos de 1 minuto.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Planos de discagem de UM" no tópico [Permissões de mensagens unificadas](unified-messaging-permissions-exchange-2013-help.md).

  - Antes de executar esses procedimentos, confirme se um plano de discagem da UM foi criado. Para obter etapas detalhadas, consulte [Criar um plano de discagem de UM](create-a-um-dial-plan-exchange-2013-help.md).

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>..



## O que você deseja fazer?

## Usar o EAC para habilitar um informe

1.  No EAC, navegue até **Unificação de Mensagens** \> **Planos de discagem de UM**.

2.  Na exibição de lista, selecione o plano de discagem de Unificação de MENSAGENS que você deseja modificar e, em seguida, clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").

3.  Na página **Plano de discagem de UM**, clique em **Configurar**.

4.  No **Outlook Voice Access**, sob **Informe**, clique em **Alterar** e clique em **Procurar** para localizar o arquivo de comunicado.
    

    > [!IMPORTANT]
    > O arquivo que você pode usar para o informe deve ser um arquivo. wav ou. wma.



5.  Depois de ter localizado o arquivo, clique em **Abrir** e em **Salvar**.

## Use o Shell para habilitar um informe

Este exemplo habilita um informe que usa o arquivo de informe informational.wav em um plano de discagem UM chamado `MyUMDialPlan`.

    Set-UMDialPlan -Identity MyUMDialPlan -InfoAnnouncementEnabled $true-InfoAnnouncementFilename c:\UMGreetings\informational.wav

