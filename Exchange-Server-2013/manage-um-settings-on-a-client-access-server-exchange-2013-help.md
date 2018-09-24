---
title: 'Gerenciar configurações de UM em um servidor de acesso para cliente'
TOCTitle: Gerenciar configurações de Unificação de mensagens em um servidor de acesso para cliente
ms:assetid: 08667911-fa86-404e-84b1-65cedd94d579
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/JJ673507(v=EXCHG.150)
ms:contentKeyID: 50556138
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Gerenciar configurações de Unificação de mensagens em um servidor de acesso para cliente

 

_**Aplica-se a:** Exchange Server 2013, Exchange Server 2016_

_**Tópico modificado em:** 2013-04-09_

Depois de instalar um servidor de Acesso para Cliente que esteja executando o serviço de Roteamento de Chamada de Unificação de Mensagens do Microsoft Exchange, você poderá configurar diversas opções, incluindo o número de chamadas consecutivas, as portas de escuta de protocolo TCP e TLS, o status e o modo de inicialização.


> [!NOTE]
> Não é necessário que os servidores de Acesso para Cliente sejam adicionados a um plano de discagem de UM antes de poderem processar chamadas para a Unificação de Mensagens (UM), exceto quando você estiver integrando a UM e o Microsoft Office Communications Server 2007 R2 ou Microsoft Lync Server. Por padrão, todos os servidores de Acesso para Cliente em uma organização estão disponíveis para atender chamadas de entrada.



Para conhecer tarefas adicionais relacionadas a servidores de Unificação de Mensagens e de Acesso para Cliente, consulte [Procedimentos de serviços de Unificação de mensagens](um-services-procedures-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: 5 minutos.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Servidor de Acesso para Cliente (servidor de roteamento de chamadas de UM)", no tópico [Permissões de mensagens unificadas](unified-messaging-permissions-exchange-2013-help.md).

  - Verifique se o servidor de Acesso para Cliente está instalado no mesmo computador que o servidor de Caixa de Correio ou em um computador separado.

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>..



## O que você deseja fazer?

## Use o Shell para configurar as propriedades de Unificação de Mensagens em um servidor de Acesso para Cliente

Esse exemplo remove um servidor de Acesso para Cliente chamado `MyClientAccessServer` de todos os planos de discagem do Protocolo SIP.

```powershell
Set-UMCallRouterSettings -DialPlans $null - Server MyClientAccessServer
```

Este exemplo adiciona o servidor de Acesso para Cliente chamado `MyClientAccessServer` a um plano de discagem de SIP chamado `MySIPDialPlan`, e também define o número máximo de chamadas de voz de entrada.

```powershell
Set-UMCallRouterSettings -DialPlans MySIPDialPlan -MaxCalls 150 -Server MyClientAccessServer
```

Esse exemplo define a porta de escuta de protocolo TCP SIP como 5077 e o modo de inicialização como modo Dual em um servidor de Acesso para Cliente chamado `MyClientAccessServer`.

    Set-UMCallRouterSettings  -Server MyClientAccessServer-SipTCPListeningPort 5077 -UMStartUpMode -Dual 

## Use o Shell para visualizar as propriedades do servidor de Acesso para Cliente

Esse exemplo exibe uma lista de todos os servidores de Acesso para Cliente.

```powershell
Get-UMCallRouterSettings
```

Esse exemplo exibe uma lista formatada das propriedades do servidor de Acesso para Cliente.

```powershell
Get-UMCallRouterSettings | Format-List
```

