---
title: 'Gerenciar agentes de extensão de cmdlet: Exchange 2013 Help'
TOCTitle: Gerenciar agentes de extensão de cmdlet
ms:assetid: 9141b3cb-ad13-4415-be2f-aa89f91445f5
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Dd298143(v=EXCHG.150)
ms:contentKeyID: 50556240
ms.date: 04/05/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Gerenciar agentes de extensão de cmdlet

 

_**Aplica-se a:**Exchange Server 2013_

_**Tópico modificado em:**2012-11-19_

This topic shows you how to enable, disable, view, and change the priority of cmdlet extension agents in Microsoft Exchange Server 2013. For more information about cmdlet extension agents in Exchange 2013, see [Agentes de extensão de cmdlet](cmdlet-extension-agents-exchange-2013-help.md).

## What do you need to know before you begin?

  - Estimated time to complete each procedure: less than 5 minutes

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o "Cmdlet extension agents" entry in the [Permissões de infraestrutura do Exchange e do Shell](exchange-and-shell-infrastructure-permissions-exchange-2013-help.md) topic.

  - Before you enable the `Scripting Agent`, you must verify that it's configured correctly. For more information about the `Scripting Agent`, see [Agentes de extensão de cmdlet](cmdlet-extension-agents-exchange-2013-help.md).

  - You must use the Shell to perform these procedures.

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>.



## What do you want to do?

## Enable a cmdlet extension agent

When you enable a cmdlet extension agent in Exchange 2013, the agent is run on every server running Exchange 2013 in the organization. When an agent is enabled, it's made available to cmdlets, which can then use the agent to perform additional operations.


> [!WARNING]
> Before you enable an agent, be sure that you're aware of how the agent works and what impact the agent will have on your organization.



This example enables a cmdlet extension agent by using the **Enable-CmdletExtensionAgent** cmdlet. You must specify the name of the agent you want to enable when you run the cmdlet. Before you enable the `Scripting Agent`, you need to make sure that you've deployed the `ScriptingAgentConfig.xml` configuration file to all the servers in your organization. If you don't deploy the configuration file first and you enable the `Scripting ``Agent`, all non-**Get** cmdlets fail when they're run. This example enables the `Scripting Agent`.

    Enable-CmdletExtensionAgent "Scripting Agent"

For detailed syntax and parameter information, see [Enable-CmdletExtensionAgent](https://technet.microsoft.com/pt-br/library/dd335192\(v=exchg.150\)).

## Disable a cmdlet extension agent

When you disable a cmdlet extension agent in Exchange 2013, the agent is disabled on every server running Exchange 2013 in the organization. When an agent is disabled, it's not made available to cmdlets. Cmdlets can no longer use the agent to perform additional operations.


> [!WARNING]
> Before you disable an agent, be sure that you're aware of how the agent works and what impact disabling the agent will have on your organization.



To disable a cmdlet extension agent, use the **Disable-CmdletExtensionAgent** cmdlet. Specify the name of the agent you want to disable when you run the cmdlet. This example disables the `Scripting Agent`.

    Disable-CmdletExtensionAgent "Scripting Agent"

For detailed syntax and parameter information, see [Disable-CmdletExtensionAgent](https://technet.microsoft.com/pt-br/library/dd298132\(v=exchg.150\)).

## View existing cmdlet extension agents

Viewing cmdlet extension agents enables you to see which agents are run first and which agents are enabled in an Exchange 2013 organization. For more information about pipelining and the **Format-Table** cmdlet, see the following topics:

  - [Pipelining](https://technet.microsoft.com/pt-br/library/aa998260\(v=exchg.150\))

  - [Trabalhando com a saída do comando](working-with-command-output-exchange-2013-help.md)

This example gets the details of a specific cmdlet extension agent by using the **Get-CmdletExtensionAgent** cmdlet. In this example, the details of the `Mailbox Permissions Agent` are returned.

    Get-CmdletExtensionAgent "Mailbox Permissions Agent"

This example gets multiple cmdlet extension agents by using the **Get-CmdletExtensionAgent** cmdlet, and then pipes the output to the **Format-Table** cmdlet. This example displays a list of all of the cmdlet extension agents in the organization, and by using the **Format-Table** cmdlet, the **Name**, **Enabled**, and **Priority** properties of each agent are displayed in a table.

    Get-CmdletExtensionAgent | Format-Table Name, Enabled, Priority

For detailed syntax and parameter information, see [Get-CmdletExtensionAgent](https://technet.microsoft.com/pt-br/library/dd297946\(v=exchg.150\)).

## Change the priority of a cmdlet extension agent

The ability to change the priority of a cmdlet extension agent in Exchange 2013 is useful when you want a certain agent to be called by a cmdlet before another agent. This is especially useful if you create a custom script that's run in the `Scripting Agent`, and you want that script to take precedence over a built-in agent. For more information about the `Scripting Agent`, see [Agentes de extensão de cmdlet](cmdlet-extension-agents-exchange-2013-help.md).


> [!WARNING]
> Changing the priority or replacing the functionality of a built-in agent is an advanced operation. Be sure that you completely understand the changes you're making.



Agents are ordered from zero to the maximum number of agents. The closer to zero the agent is, the higher the priority of the agent. Agents with a higher priority are called first. For more information about agent priorities, see [Agentes de extensão de cmdlet](cmdlet-extension-agents-exchange-2013-help.md).

This example changes the priority of a cmdlet extension agent by using the **Set-CmdletExtensionAgent** cmdlet. In this example, the priority of the `Scripting Agent` is changed to 3.

    Set-CmdletExtensionAgent "Scripting Agent" -Priority 3

For detailed syntax and parameter information, see [Set-CmdletExtensionAgent](https://technet.microsoft.com/pt-br/library/dd335175\(v=exchg.150\)).

