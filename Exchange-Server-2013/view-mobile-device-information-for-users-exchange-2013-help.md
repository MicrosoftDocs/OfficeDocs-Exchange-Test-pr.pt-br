---
title: 'Exibir informações do dispositivo móvel para usuários: Exchange 2013 Help'
TOCTitle: Exibir informações do dispositivo móvel para usuários
ms:assetid: 4fd263c0-ad61-416c-bd68-339bf66605cf
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Aa997974(v=EXCHG.150)
ms:contentKeyID: 50485571
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Exibir informações do dispositivo móvel para usuários

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2012-11-29_

Os usuários podem configurar vários dispositivos móveis para sincronização com o MicrosoftExchange Server 2013. Você pode usar o EAC ou o Shell para exibir uma lista de dispositivos móveis associados a um usuário específico.

Para tarefas de gerenciamento adicionais relacionadas a dispositivos móveis, consulte [Exchange ActiveSync](exchange-activesync-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para concluir cada procedimento: 5 minutos.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Política de caixa de correio de dispositivo móvel", no tópico [Permissões de dispositivos móveis e clientes](clients-and-mobile-devices-permissions-exchange-2013-help.md).

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>..



## O que você deseja fazer?

## Usar o EAC para exibir informações de dispositivo móvel para usuários

O EAC mostra uma lista de dispositivos móveis que estão se sincronizando com uma caixa de correio de usuário. Você pode exibir dispositivos móveis por família, modelo, número de telefone ou status.

1.  No EAC, clique em **Destinatários** \> **Caixas de correio** e selecione uma caixa de correio.

2.  No painel de Detalhes, role para a tela **Recursos de Telefone e Voz** e clique em **Exibir detalhes**, para mostrar a tela **Detalhes do Dispositivo Móvel**.

## Usar o Shell para exibir informações de dispositivo móvel para usuários

Você pode usar o cmdlet **Get-MobileDevice** para visualizar uma lista de dispositivos móveis para um usuário específico.

1.  Execute o seguinte comando.
    
        Get-MobileDevice -Mailbox useralias

