---
title: 'Remover serv. acesso para cliente e cx. correio de plano de discagem URI SIP'
TOCTitle: Remover servidores de acesso para cliente e caixa de correio de um plano de discagem URI do SIP
ms:assetid: 367441e1-1a0f-42c8-9fa8-8abe80b3d015
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Aa997238(v=EXCHG.150)
ms:contentKeyID: 54651963
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Remover servidores de acesso para cliente e caixa de correio de um plano de discagem URI do SIP

 

_**Aplica-se a:** Exchange Server 2013, Exchange Server 2016_

_**Tópico modificado em:** 2013-04-16_

Você pode remover servidores de Acesso para Cliente e Caixa de Correio a todos os planos de discagem URI SIP. Quando você estiver implantando o Microsoft Lync Server, para permitir que a chamada de saída funcione corretamente, será preciso adicionar manualmente todos os servidores Acesso para Cliente e Caixa de Correio aos planos de discagem URI SIP criados para o Lync Server. Entretanto, talvez seja necessário remover um servidor Acesso para Cliente ou Caixa de Correio da sua implantação do Lync, por exemplo, se você estiver realizando manutenção ou colocando o servidor offline.

Para conhecer tarefas de gerenciamento adicionais relacionadas a planos de discagem de UM, consulte [Procedimentos de plano de discagem de UM](um-dial-plan-procedures-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: Menos de 1 minuto.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Planos de discagem de UM" no tópico [Permissões de mensagens unificadas](unified-messaging-permissions-exchange-2013-help.md).

  - Antes de executar estes procedimentos, confirme se um plano de discagem URI SIP foi criado. Para conhecer etapas detalhadas, consulte [Criar um plano de discagem de UM](https://docs.microsoft.com/pt-br/exchange/voice-mail-unified-messaging/connect-voice-mail-system/create-um-dial-plan).

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>..



## O que você deseja fazer?

## Usar o EAC para remover um servidor de Caixa de Correio do plano de discagem URI SIP

1.  No EAC, navegue até **Servidores** \> **Servidores**.

2.  No modo de exibição de lista, selecione o servidor Exchange que você deseja modificar e clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").

3.  Na página **Exchange Server**, clique em **Unificação de Mensagens**.

4.  Em **Configurações do Serviço UM** \> **Planos de discagem associados**, localize o plano de discagem URI SIP a ser removido, clique em **Remover**![ícone Remover](images/JJ657492.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "ícone Remover") e então clique em **Salvar**. Se quiser remover mais de um plano de discagem URI SIP, pressione e mantenha pressionada a tecla CTRL, selecione os planos de discagem que você deseja remover e clique em **Salvar**.

## Usar o Shell para remover um servidor de Caixa de Correio do plano de discagem URI SIP

Este exemplo remove um servidor de Caixa de Correio chamado `MyMailboxServer` do plano de discagem URI SIP chamado `MySIPDialPlan`.

    $dp= Get-UMDialPlan "MySIPDialPlan"
    $s=Get-UMService MyMailboxServer
    $s.dialplans-=$dp.identity
    Set-UMService -id MyMailboxServer -dialplans:$s.dialplans

Neste exemplo, existem três planos de discagem de URI SIP: SipDP1, SipDP2 e SipDP3. Este exemplo remove um servidor de Caixa de Correio chamado `MyMailboxServer` do plano de discagem SipDP3.

```powershell
Set-UMService -id MyMailboxServer -DialPlans SipDP1,SipDP2
```

Neste exemplo, existem dois planos de discagem de URI SIP: SipDP1 e SipDP2. Este exemplo remove um servidor de Caixa de Correio chamado `MyMailboxServer` do plano de discagem SipDP2.

```powershell
Set-UMService -id MyMailboxServer -DialPlans SipDP1
```

Este exemplo remove um servidor de Caixa de Correio chamado `MyMailboxServer` de todos os planos de discagem SIP.

```powershell
Set-UMService -id MyUMServer -DialPlans $null
```

## Usar o EAC para remover um servidor de Acesso para Cliente do plano de discagem URI SIP

1.  No EAC, navegue até **Servidores** \> **Servidores**.

2.  No modo de exibição de lista, selecione o servidor de Acesso para Cliente que você deseja modificar e clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").

3.  Na página **Exchange Server**, clique em **Unificação de Mensagens**.

4.  Em **Configurações do Roteador de Chamadas da UM** \> **Planos de discagem associados**, localize o plano de discagem URI SIP a ser removido, clique em **Remover**![ícone Remover](images/JJ657492.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "ícone Remover") e então clique em **Salvar**. Se quiser remover mais de um plano de discagem URI SIP, pressione e mantenha pressionada a tecla CTRL, selecione os planos de discagem que você deseja remover e clique em **Salvar**.

## Usar o Shell para remover um servidor de Acesso para Cliente do plano de discagem URI SIP

Este exemplo remove um servidor de Acesso para Cliente chamado `MyClientAccessServer` do plano de discagem URI SIP chamado `MySIPDialPlan`.

    $dp= Get-UMDialPlan "MySIPDialPlan"
    $s=Get-UMCallRouterSettings MyClientAccessServer
    $s.dialplans-=$dp.identity
    Set-UMCallRouterSettings -id MyClientAccessServer -dialplans:$s.dialplans

Neste exemplo, existem três planos de discagem de URI SIP: SipDP1, SipDP2 e SipDP3. Este exemplo remove um servidor de Acesso para Cliente chamado `MyClientAccessServer` do plano de discagem SipDP3.

```powershell
Set-UMCallRouterSettings -id MyClientAccessServer -DialPlans SipDP1,SipDP2
```

Neste exemplo, existem dois planos de discagem de URI SIP: SipDP1 e SipDP2. Este exemplo remove um servidor de Acesso para Cliente chamado `MyClientAccessServer` do plano de discagem SipDP2.

```powershell
Set-UMCallRouterSettings -id MyClientAccessServer -DialPlans SipDP1
```

Este exemplo remove um servidor de Acesso para Cliente chamado `MyClientAccessServer` de todos os planos de discagem SIP.

```powershell
Set-UMCallRouterSettings -id MyClientAccessServer -DialPlans $null
```

