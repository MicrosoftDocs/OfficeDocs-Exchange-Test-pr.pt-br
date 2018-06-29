---
title: 'Iniciar o serviço de Unificação de mensagens do Microsoft Exchange: Exchange 2013 Help'
TOCTitle: Iniciar o serviço de Unificação de mensagens do Microsoft Exchange
ms:assetid: b54008e6-172e-4435-8516-57cff740e89c
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Bb124330(v=EXCHG.150)
ms:contentKeyID: 50556281
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Iniciar o serviço de Unificação de mensagens do Microsoft Exchange

 

_**Aplica-se a:**Exchange Server 2013, Exchange Server 2016_

_**Tópico modificado em:**2012-11-16_

Você pode usar o snap-in Serviços no Microsoft Management Console (MMC) ou cmd.exe em um prompt de comando para iniciar o MicrosoftExchange o serviço de Unificação de mensagens em um servidor de caixa de correio. Por padrão, o MicrosoftExchange o serviço de Unificação de mensagens é iniciado depois que um servidor de caixa de correio está instalado. No entanto, pode haver vezes quando você precisar reiniciar MicrosoftExchange o serviço de Unificação de mensagens manualmente, por exemplo, quando você tiver obtido o servidor de caixa de correio offline e precisa ativá-la novamente.

Quando o MicrosoftExchange o serviço de Unificação de mensagens é iniciado em um servidor de caixa de correio, o servidor de caixa de correio está disponível para atender e processar chamadas de Unificação de mensagens de entrada.

Para conhecer tarefas de gerenciamento adicionais relacionadas a servidores de Caixa de Correio, consulte [Procedimentos de serviços de Unificação de mensagens](um-services-procedures-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: Menos de 1 minuto.

  - Para realizar os procedimentos a seguir, faça logon no servidor de Caixa de Correio com uma conta que seja membro do grupo local de Administradores.

  - Verifique se o servidor de Caixa de Correio está instalado no mesmo computador que um servidor de Acesso para Cliente ou em um computador separado.

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>..



## O que você deseja fazer?

## Use o snap-in MMC de serviços para iniciar o serviço de Unificação de mensagens do Microsoft Exchange

1.  Clicar em **Iniciar** e em **Painel de Controle**.

2.  No Painel de Controle, clique duas vezes em **Ferramentas Administrativas**.

3.  Em **Ferramentas Administrativas**, clique duas vezes em **Serviços**.

4.  No painel de detalhes **Serviços**, clique com o botão **De Unificação de mensagens do Microsoft Exchange** e, em seguida, clique em **Iniciar**.

## Use um prompt de comando para iniciar o serviço de Unificação de mensagens do Microsoft Exchange

1.  Clique em **Iniciar** e, em seguida, em **Executar**.

2.  Na caixa **Abrir**, digite o seguinte comando e pressione Enter.
    
        net start MSExchangeUM

