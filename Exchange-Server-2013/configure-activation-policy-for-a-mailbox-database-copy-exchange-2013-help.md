---
title: 'Configurar a ativação da cópia do banco de dados de caixa de correio'
TOCTitle: Configurar a política de ativação para uma cópia do banco de dados de caixa de correio
ms:assetid: 6b37ed6e-2e36-4688-b485-8fdbb8193ec8
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Dd298046(v=EXCHG.150)
ms:contentKeyID: 50485885
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configurar a política de ativação para uma cópia do banco de dados de caixa de correio

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2012-11-02_

*Ativação* é o processo de alterar uma cópia de banco de dados de caixa de correio de uma cópia passiva para uma cópia ativa. A ativação ocorre automaticamente no sistema como parte de uma operação de failover de banco de dados ou servidor e pode ser executada manualmente por um administrador como parte de uma operação de alternância de banco de dados ou servidor. O bloqueio de um banco de dados para ativação impede que ele se torne a cópia ativa durante um failover de banco de dados ou servidor.

Procurando outras tarefas de gerenciamento relacionadas a cópias do banco de dados de caixa de correio? Consulte [Gerenciando cópias de banco de dados de caixa de correio](managing-mailbox-database-copies-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para a conclusão da tarefa: 1 minuto

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte oEntrada "Cópias de banco de dados da caixa de correio" no tópico [Permissões de resiliência de site e disponibilidade altas](high-availability-and-site-resilience-permissions-exchange-2013-help.md).

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>..



## O que você deseja fazer?

## Usar o EAC para configurar a política de ativação para uma cópia de banco de dados de caixa de correio

1.  Na EAC, vá até **Servidores** \> **Bancos de dados**.

2.  Selecione os bancos de dados que você deseja configurar.

3.  No painel Detalhes, em **Cópias de Banco de Dados**, localize a cópia de banco de dados que você deseja configurar e clique em **Suspender**.

4.  Opcionalmente, adicione um comentário e marque a caixa que diz **Esta cópia pode ser ativada somente por intervenção manual**.

5.  Clique em **Salvar** para salvar as alterações na configuração da cópia do banco de dados de caixa de correio.

## Usar o Shell para suspender ou retomar uma cópia do banco de dados para ativação

Esse exemplo bloqueia a cópia do banco de dados DB1 no servidor MBX2 para ativação.

```powershell
Suspend-MailboxDatabaseCopy -Identity DB1\MBX2 -ActivationOnly
```

Esse exemplo retoma a cópia do banco de dados DB1 no servidor MBX2 para ativação.

```powershell
Resume-MailboxDatabaseCopy -Identity DB1\MBX2
```

Para informações detalhadas de sintaxes e de parâmetros, consulte [Suspend-MailboxDatabaseCopy](https://technet.microsoft.com/pt-br/library/dd351074\(v=exchg.150\)) ou [Resume-MailboxDatabaseCopy](https://technet.microsoft.com/pt-br/library/dd335220\(v=exchg.150\)).

## Usar o Shell para configurar a política de ativação de um servidor

Este exemplo configura as cópias de banco de dados no servidor MBX2 como bloqueadas para ativação.

```powershell
Set-MailboxServer -Identity MBX2 -DatabaseCopyAutoActivationPolicy Blocked
```

Este exemplo configura as cópias de banco de dados no servidor MBX3 como bloqueadas para ativação fora do site.

```powershell
Set-MailboxServer -Identity MBX3 -DatabaseCopyAutoActivationPolicy IntrasiteOnly
```

Este exemplo configura as cópias de banco de dados no servidor MBX4 como desbloqueadas para ativação.

```powershell
Set-MailboxServer -Identity MBX4 -DatabaseCopyAutoActivationPolicy Unrestricted
```

Para informações detalhadas de sintaxe e de parâmetros, consulte [Suspend-MailboxDatabaseCopy](https://technet.microsoft.com/pt-br/library/dd351074\(v=exchg.150\)), [Resume-MailboxDatabaseCopy](https://technet.microsoft.com/pt-br/library/dd335220\(v=exchg.150\)) ou [Set-MailboxServer](https://technet.microsoft.com/pt-br/library/aa998651\(v=exchg.150\)).

## Como saber se funcionou?

Para verificar se você configurou com êxito a política de ativação, faça o seguinte:

  - No Shell, execute o seguinte comando, para verificar as configurações de ativação para uma cópia do banco de dados.
    
    ```powershell
    Get-MailboxDatabaseCopyStatus <DatabaseCopyName> | Format-List ActivationSuspended
    ```

  - No Shell, execute o seguinte comando, para verificar as configurações de ativação para um membro do DAG.
    
    ```powershell
    Get-MailboxServer <ServerName> | Format-List DatabaseCopyAutoActivationPolicy
    ```

