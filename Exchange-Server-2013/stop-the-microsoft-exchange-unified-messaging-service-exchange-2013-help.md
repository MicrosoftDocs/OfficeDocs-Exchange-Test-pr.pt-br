---
title: 'Pare o serviço de UM do Microsoft Exchange: Exchange 2013 Help'
TOCTitle: Pare o serviço de Unificação de mensagens do Microsoft Exchange
ms:assetid: 64fa5535-8150-45c6-82e6-d2346892a031
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Aa998595(v=EXCHG.150)
ms:contentKeyID: 50556213
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Pare o serviço de Unificação de mensagens do Microsoft Exchange

 

_**Aplica-se a:** Exchange Server 2013, Exchange Server 2016_

_**Tópico modificado em:** 2012-11-16_

Você pode usar o snap-in Serviços no Console de Gerenciamento Microsoft (MMC) ou cmd.exe no prompt de comando para interromper o serviço Unificação de Mensagens do MicrosoftExchange em um servidor de Caixa de Correio. Em alguns momentos, pode ser preciso interromper esse serviço, por exemplo, quando for necessário deixar o servidor de Caixa de Correio offline. Quando você interromper o serviço Unificação de Mensagens do Microsoft Exchange, o servidor de Caixa de Correio não poderá aceitar e processar chamadas de entrada.

Para conhecer tarefas de gerenciamento adicionais relacionadas a servidores de Caixa de Correio, consulte [Procedimentos de serviços de Unificação de mensagens](um-services-procedures-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: Menos de 1 minuto.

  - Para realizar os procedimentos a seguir, faça logon no servidor de Caixa de Correio com uma conta que seja membro do grupo local de Administradores.

  - Verifique se o servidor de Caixa de Correio está instalado no mesmo computador que um servidor de Acesso para Cliente ou em um computador separado.

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>..



## O que você deseja fazer?

## Usar o snap-in Serviços do MMC para interromper o serviço de UM do Microsoft Exchange

1.  Clicar em **Iniciar** e em **Painel de Controle**.

2.  No Painel de Controle, clique duas vezes em **Ferramentas Administrativas**.

3.  Em **Ferramentas Administrativas**, clique duas vezes em **Serviços**.

4.  No painel de detalhes **Serviços**, clique com o botão direito em **Unificação de Mensagens do Microsoft Exchange** e, em seguida, clique em **Parar**.

## Usar um prompt de comando para interromper o serviço de UM do Microsoft Exchange

1.  Clique em **Iniciar** e, em seguida, em **Executar**.

2.  Na caixa **Abrir**, digite o seguinte comando e pressione Enter.
    
        net stop MSExchangeUM

