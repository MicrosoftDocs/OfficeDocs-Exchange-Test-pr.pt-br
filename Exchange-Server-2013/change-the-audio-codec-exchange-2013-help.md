---
title: 'Alterar o codec de áudio: Exchange 2013 Help'
TOCTitle: Alterar o codec de áudio
ms:assetid: 139b2ccd-28c5-46c0-9050-777f4f59aade
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Aa996342(v=EXCHG.150)
ms:contentKeyID: 50484974
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Alterar o codec de áudio

 

_**Aplica-se a:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Tópico modificado em:**2013-02-22_

A Unificação de Mensagens pode usar um entre quatro codecs para criar mensagens de voz: MP3, WMA (Windows Media Audio), GSM (Group System Mobile) 06.10 e G.711 PCM (Pulse Code Modulation) Linear. Por padrão, quando você cria um plano de discagem de UM (Unificação de Mensagens), ele usa o codec de áudio MP3 para gravar mensagens de voz. O formato de áudio MP3 é um formato de áudio popular usado em vários sistemas operacionais, clientes de email e MP3 players. Depois de criar um plano de discagem de UM, você pode configurá-lo para usar um dos outros formatos de áudio, incluindo os codecs de áudio WMA, GSM 06.10 ou G.711 PCM Linear. Para ouvir a mensagem de voz, um telefone celular ou computador precisa ter um software de áudio compatível instalado.

Para tarefas adicionais relacionadas a planos de discagem de UM, consulte [Procedimentos de plano de discagem de UM](um-dial-plan-procedures-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: Menos de 1 minuto.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Planos de discagem da UM" no tópico [Permissões de mensagens unificadas](unified-messaging-permissions-exchange-2013-help.md).

  - Antes de executar esses procedimentos, confirme se um plano de discagem de UM foi criado. Para obter etapas detalhadas, consulte [Criar um plano de discagem de UM](create-a-um-dial-plan-exchange-2013-help.md).

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>..



## O que você deseja fazer?

## Usar o EAC para alterar o codec de áudio em um plano de discagem da Unificação de Mensagens

1.  No EAC, navegue até **Unificação de Mensagens** \> **Planos de discagem de UM**.

2.  Na exibição de lista, selecione o plano de discagem de UM que você deseja alterar e clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").

3.  Na página **Plano de discagem de UM**, clique em **Configurar**.

4.  Em **Configurações**, em **Codec de áudio**, use a lista suspensa para selecionar um dos seguintes itens:
    
      - MP3
    
      - WMA
    
      - GSM
    
      - G711

5.  Clique em **Salvar**.

## Use o Shell para alterar o codec de áudio em um plano de discagem da Unificação de Mensagens

Este exemplo define o codec de áudio em um plano de discagem de UM chamado `MyUMDialPlan` como G.711.

    Set-UMDialPlan -Identity MyUMDialPlan -AudioCodec G711

Este exemplo define o codec de áudio em um plano de discagem de UM chamado `MyUMDialPlan` como WMA.

    Set-UMDialPlan -Identity MyUMDialPlan -AudioCodec Wma

