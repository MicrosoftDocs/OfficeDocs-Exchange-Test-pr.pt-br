---
title: 'Habilitar um informe: Exchange 2013 Help'
TOCTitle: Habilitar um informe
ms:assetid: 07f6c13e-3781-4127-9321-f0f85f054259
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Bb266918(v=EXCHG.150)
ms:contentKeyID: 50556137
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Habilitar um informe

 

_**Aplica-se a:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Tópico modificado em:**2013-04-19_

Você pode habilitar um informe para um atendedor automático da UM (Unificação de Mensagens). Quando um informe é habilitado, ele tocará imediatamente após a saudação de horário comercial ou não comercial. Por padrão, nenhum informe está configurado. Para habilitar um informe, crie um arquivo .wav ou .wma para ser usado como informe e, em seguida, configure o atendedor automático para usar esse arquivo de som.

Para tarefas de gerenciamento adicionais relacionadas a atendedores automáticos de UM, consulte [Procedimentos atendedor automático a Unificação de mensagens](um-auto-attendant-procedures-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: Menos de 1 minuto.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Atendedores automáticos da UM" no tópico [Permissões de mensagens unificadas](unified-messaging-permissions-exchange-2013-help.md).

  - Antes de executar esses procedimentos, confirme se um plano de discagem de UM foi criado. Para obter etapas detalhadas, consulte [Criar um plano de discagem de UM](create-a-um-dial-plan-exchange-2013-help.md).

  - Antes de executar esses procedimentos, verifique se um plano de discagem de UM foi criado. Para instruções detalhadas, consulte [Criar um Atendedor Automático da UM](create-a-um-auto-attendant-exchange-2013-help.md).

  - Crie um arquivo .wav ou .wma para ser usado para o informe.

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>..



## O que você deseja fazer?

## Usar o EAC para habilitar um informe

1.  No EAC, navegue até **Unificação de Mensagens** \> **Planos de discagem de UM**. Na exibição de lista, selecione o plano de discagem de UM que você deseja modificar e clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").

2.  Na página **Plano de Discagem de UM**, em **Atendedores Automáticos da UM**, selecione o atendedor automático da UM para o qual você deseja habilitar um informe e clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").

3.  Na página do **Atendedor Automático da UM**, \> **Saudações**, em **Informe**, clique em **Alterar** e depois clique em **Navegar** para localizar o arquivo de informe que você criou antes de iniciar esse procedimento.
    

    > [!IMPORTANT]
    > O arquivo usado para a saudação deve ser wav. ou .wma.



4.  Depois de ter localizado o arquivo, clique em **Abrir** e em **Salvar**.

## Use o Shell para habilitar um informe

Esse exemplo habilita um informe que usa o arquivo `MyInfoAnnouncement.wav` para o atendedor automático da UM chamado `MyUMAutoAttendant`.

    Set-UMAutoAttendant -Identity MyUMAutoAttendant -InfoAnnouncementEnabled $true -InfoAnnouncementFilename MyInfoAnnouncement.wav

