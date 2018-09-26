---
title: 'Gerenciar conjuntos de integridade e a integridade do servidor'
TOCTitle: Gerenciar conjuntos de integridade e a integridade do servidor
ms:assetid: a4f84312-6cfa-4f17-9707-676aadab1143
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Dn482054(v=EXCHG.150)
ms:contentKeyID: 59890400
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Gerenciar conjuntos de integridade e a integridade do servidor

 

_**Aplica-se a:** Exchange Online, Exchange Server 2013 SP1_

_**Tópico modificado em:** 2013-12-02_

Você pode usar os cmdlets internos de relatório de integridade para executar várias tarefas relacionadas à disponibilidade gerenciada; por exemplo:

  - Exibir a integridade de um servidor ou de um grupo de servidores

  - Exibir uma lista de conjuntos de integridade

  - Exibir uma lista de sondas, monitores e respondentes associados a um conjunto específico de integridade

  - Exibir uma lista de monitores e respectivos estados vigentes

## O que você precisa saber antes de começar?

  - Tempo estimado para concluir cada procedimento: 2 minutos

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>.



## O que você deseja fazer?

## Exibir a integridade do servidor

Você pode usar o Shell para obter um resumo da integridade de um servidor que executa o Exchange 2013.

## Usar o Shell para exibir a integridade do servidor

Execute um destes comandos para exibir os conjuntos e as informações de integridade em um servidor que executa o Exchange 2013.


```powershell
Get-HealthReport -Identity <ServerName>
```

```powershell
Get-ServerHealth -Identity <ServerName> | Format-Table Server,CurrentHealthSetState,Name,HealthSetName,AlertValue,HealthGroupName -Auto
```

Execute qualquer um destes comandos para exibir os conjuntos de integridade em um servidor ou em um grupo de disponibilidade de banco de dados com o Exchange 2013 em execução.


```powershell
Get-ExchangeServer | Get-HealthReport -RollupGroup
```

```powershell
Get-ExchangeServer | Get-HealthReport -RollupGroup -HealthSetName <HealthSet>
```

```powershell
(Get-DatabaseAvailabiltyGroup <DAGName>).Servers | Get-HealthReport -RollupGroup
```

## Exibir uma lista de conjuntos de integridade

Um conjunto de integridade é um grupo de monitores, sondas e respondentes de um componente, que determina se o componente está íntegro ou não. Você pode usar o Shell para exibir a lista de conjuntos de integridade em um servidor que executa o Exchange 2013.

## Usar o Shell para exibir uma lista de conjuntos de integridade

Execute este comando para exibir os conjuntos de integridade em um servidor que executa o Exchange 2013.

```powershell
Get-HealthReport -Server <ServerName>
```

## Exibir sondas, monitores e respondentes de um conjunto de integridade

Um conjunto de integridade é um grupo de monitores, sondas e respondentes de um componente, que determina se o componente está íntegro ou não. Você pode usar o Shell para exibir a lista de sondas, monitores e respondentes associados a um conjunto de integridade, em um servidor executando o Exchange 2013.

## Usar o Shell para exibir sondas, monitores e respondentes de um conjunto de integridade

Execute este comando para exibir sondas, monitores e respondentes associados a um conjunto de integridade, em um servidor executando o Exchange 2013.

```powershell
Get-MonitoringItemIdentity -Server <ServerName> -Identity <HealthSetName> | Format-Table Identity,ItemType,Name -Auto
```

## Exibir uma lista de monitores e respectivos estados vigentes

A integridade de um monitor é relatada por meio do "pior caso" no conjunto de integridade. Você pode exibir os detalhes de um conjunto de integridade para ver quais monitores estão íntegros e quais não estão.

## Usar o Shell para exibir uma lista de monitores e respectivos estados vigentes

Execute este comando para exibir uma lista dos monitores e respectiva integridade vigente em um servidor que executa o Exchange 2013.

```powershell
Get-ServerHealth -HealthSet <HealthSetName> -Server <ServerName> | Format-Table Name, AlertValue -Auto
```

