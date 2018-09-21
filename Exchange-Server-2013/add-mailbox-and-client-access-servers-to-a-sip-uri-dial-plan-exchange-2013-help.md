---
title: 'Adicionar serv. acesso para cliente e cx. de correio a plano de disc. URI SIP'
TOCTitle: Adicionar servidores de acesso para cliente e caixa de correio a um plano de discagem URI do SIP
ms:assetid: 17fed308-ff0d-4e61-b9f9-e6680b6eccaa
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Aa996399(v=EXCHG.150)
ms:contentKeyID: 52058791
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Adicionar servidores de acesso para cliente e caixa de correio a um plano de discagem URI do SIP

 

_**Aplica-se a:** Exchange Server 2013, Exchange Server 2016_

_**Tópico modificado em:** 2013-04-16_

Você pode adicionar servidores de Acesso para Cliente e de Caixa de Correio aos planos de discagem URI do SIP. Os servidores de Acesso para Cliente e de Caixa de Correio não podem ser associados aos planos de discagem Ramal ou E.164, mas os servidores atenderão a todas as chamadas de entrada.

Se você estiver implantando o Microsoft Lync Server, para permitir que a chamada de saída funcione corretamente, é necessário adicionar manualmente todos os servidores de Acesso para Cliente e de Caixa de Correio a todos os planos de discagem URI do SIP criados para o Lync Server.

Para conhecer tarefas de gerenciamento adicionais relacionadas a planos de discagem de UM, consulte [Procedimentos de plano de discagem de UM](um-dial-plan-procedures-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: Menos de 1 minuto.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Planos de discagem de UM" no tópico [Permissões de mensagens unificadas](unified-messaging-permissions-exchange-2013-help.md).

  - Antes de executar esses procedimentos, confirme se um plano de discagem URI do SIP foi criado. Para conhecer etapas detalhadas, consulte [Criar um plano de discagem de UM](https://docs.microsoft.com/pt-br/exchange/voice-mail-unified-messaging/connect-voice-mail-system/create-um-dial-plan).

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>..



## O que você deseja fazer?

## Use o EAC para adicionar um servidor de Caixa de Correio a um plano de discagem URI do SIP

1.  No EAC, navegue até **Servidores** \> **Servidores**.

2.  No modo de exibição de lista, selecione o servidor de Caixa de Correio que você deseja modificar e clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").

3.  Na página **Exchange Server**, clique em **Unificação de Mensagens**.

4.  Em **Configurações da UM** \> **Planos de discagem associados**, clique em **Adicionar**![Ícone Adicionar](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Ícone Adicionar").

5.  Na janela **Selecionar um Plano de Discagem de UM**, selecione o plano de discagem URI do SIP, clique em **Adicionar**, em **OK** e clique em **Salvar**.

## Use o Shell para adicionar um servidor de Caixa de Correio a um plano de discagem URI do SIP

Este exemplo adiciona o servidor de Caixa de Correio chamado `MyMailboxServer` a um plano de discagem URI do SIP chamado `MySIPDialPlan` e o impede de aceitar novas chamadas. Ele também define o modo inicial como modo Duplo, que habilita o servidor da Caixa de Correio a aceitar solicitações TCP e TLS.

    Set-UMService -Identity MyMailboxServer -DialPlans MySIPDialPlan -Status Disabled -UMStartupMode Dual

Esse exemplo adiciona o servidor de Caixa de Correio chamado `MyMailboxServer` a dois planos de discagem SIP, chamados `MySIPDialPlan` e `MySIPDialPlan2`, e define o seguinte:

  - Permite endereços IPv4 e IPv6.

  - Define o número máximo de chamadas de entrada para 50.

  - Configura o serviço de acesso SIP para Lync Server.

<!-- end list -->

    Set-UMService -Identity MyMailboxServer -DialPlans MySIPDialPlan, MySIPDialPlan2 -IPAddressFamily Any -MaxCallsAllowed 50 -SipAccessService northamerica.lyncpoolna.contoso.com

## Use o EAC para adicionar um servidor de Acesso para Cliente a um plano de discagem URI do SIP

1.  No EAC, navegue até **Servidores** \> **Servidores**.

2.  No modo de exibição de lista, selecione o servidor de Acesso para Cliente que você deseja modificar e clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").

3.  Na página **Exchange Server**, clique em **Unificação de Mensagens**.

4.  Em **Configurações do Roteador de Chamadas de UM** \> **Planos de discagem associados**, clique em **Adicionar**![Ícone Adicionar](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Ícone Adicionar").

5.  Na janela **Selecionar um Plano de Discagem de UM**, selecione o plano de discagem URI do SIP, clique em **Adicionar**, em **OK** e clique em **Salvar**.

## Use o Shell para adicionar um servidor de Acesso para Cliente a um plano de discagem URI do SIP

Este exemplo adiciona o servidor de Acesso para Cliente chamado `MyClientAccessServer` e um plano de discagem URI do SIP chamado `MySIPDialPlan`. Ele também define o modo inicial como modo Duplo, que habilita o servidor da Acesso para Cliente a aceitar solicitações TCP e TLS.

    Set-UMCallRouterSettings -DialPlans MySIPDialPlan -Server MyClientAccessServer -UMStartupMode Dual

Esse exemplo adiciona o servidor de Acesso para Cliente chamado `MyClientAccessServer` a dois planos de discagem SIP, chamados `MySIPDialPlan` e `MySIPDialPlan2`, e permite que o servidor use endereços IPv4 e IPv6.

    Set-UMCallRouterSettings -DialPlans MySIPDialPlan, MySIPDialPlan2 -IPAddressFamily Any -Server MyClientAccessServer

