---
title: 'Pare o serviço Microsoft Exchange Unified Messaging roteador de chamadas: Exchange 2013 Help'
TOCTitle: Pare o serviço Microsoft Exchange Unified Messaging roteador de chamadas
ms:assetid: 79935528-1a8c-4f22-826c-8f9a60f4f6f4
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/JJ673535(v=EXCHG.150)
ms:contentKeyID: 50556232
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Pare o serviço Microsoft Exchange Unified Messaging roteador de chamadas

 

_**Aplica-se a:** Exchange Server 2013, Exchange Server 2016_

_**Tópico modificado em:** 2012-11-16_

Você pode usar o snap-in Serviços no Microsoft Management Console (MMC) ou cmd.exe em um prompt de comando para parar MicrosoftExchange o serviço de roteador de Unificação de chamada em um servidor de acesso para cliente. Pode haver ocasiões quando você precisar parar desse serviço, por exemplo, quando você tem que colocar o servidor de acesso para cliente offline. Quando você parar MicrosoftExchange o serviço de roteador de Unificação de chamada, o servidor de acesso para cliente não conseguirá aceite e processe as chamadas recebidas.

Para tarefas de gerenciamento adicionais relacionadas a servidores acesso para cliente, consulte [Procedimentos de serviços de Unificação de mensagens](um-services-procedures-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: Menos de 1 minuto.

  - Para executar os procedimentos a seguir, faça logon para o servidor de acesso para cliente, usando uma conta que seja membro do grupo Administradores local.

  - Verifique se o servidor de Acesso para Cliente está instalado no mesmo computador que o servidor de Caixa de Correio ou em um computador separado.

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>..



## O que você deseja fazer?

## Use o snap-in MMC de serviços para interromper o serviço Microsoft Exchange Unified Messaging roteador de chamadas

1.  Clicar em **Iniciar** e em **Painel de Controle**.

2.  No Painel de Controle, clique duas vezes em **Ferramentas Administrativas**.

3.  Em **Ferramentas Administrativas**, clique duas vezes em **Serviços**.

4.  No painel de detalhes **Serviços**, clique com o botão **Microsoft Exchange Unified Messaging roteador de chamada** e clique em **Parar**.

## Use um prompt de comando para parar o serviço Microsoft Exchange Unified Messaging roteador de chamada

1.  Clique em **Iniciar** e, em seguida, em **Executar**.

2.  Na caixa **Abrir**, digite o seguinte comando e pressione Enter.
    
        net stop MSExchangeUMCR

