---
title: 'Suspender ou retomar uma cópia de banco de dados de caixa de correio'
TOCTitle: Suspender ou retomar uma cópia do banco de dados de caixa de correio
ms:assetid: 96aa1b82-3e15-4215-843e-3d583af9504b
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Dd298159(v=EXCHG.150)
ms:contentKeyID: 50486234
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Suspender ou retomar uma cópia do banco de dados de caixa de correio

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2012-11-02_

Você pode precisar suspender ou retomar uma cópia do banco de dados para uma variedade de motivos, como manutenção no disco que contém uma cópia do banco de dados, ou suspender uma cópia do banco de dados individual de ativação para fins de recuperação de desastres.

Procurando outras tarefas de gerenciamento relacionadas a cópias do banco de dados de caixa de correio? Consulte [Gerenciando cópias de banco de dados de caixa de correio](managing-mailbox-database-copies-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para a conclusão da tarefa: 1 minuto

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte oEntrada "Cópias de banco de dados da caixa de correio" no tópico [Permissões de resiliência de site e disponibilidade altas](high-availability-and-site-resilience-permissions-exchange-2013-help.md).

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>..



## O que você deseja fazer?

## Usar o EAC para suspender uma cópia do banco de dados de caixa de correio

1.  Na EAC, vá até **Servidores** \> **Bancos de dados**.

2.  Selecione o banco de dados cuja cópia você optar por suspender.

3.  No painel de detalhes, em **Cópias de banco de dados**, clique em **Suspend** sob a cópia do banco de dados que deseja suspender.

4.  No campo **comentários**, adicione um comentário opcional de até 512 caracteres especificando o motivo para a suspensão.

5.  Para suspender a cópia do banco de dados de ativação automática, marque a caixa de seleção **Esta cópia só pode ser ativada por intervenção manual**.

6.  Clique em **Salvar** para suspender a cópia do banco de dados.

## Use o EAT para retomar uma cópia do banco de dados de caixa de correio

1.  Na EAC, vá até **Servidores** \> **Bancos de dados**.

2.  Selecione o banco de dados cuja cópia que deseja reiniciar.

3.  No painel de detalhes, em **Cópias de banco de dados**, clique em **continuar** na cópia do banco de dados que deseja reiniciar.

4.  Clique em **Sim** para retomar a cópia do banco de dados.

## Use o Shell para suspender uma cópia do banco de dados de caixa de correio

Este exemplo suspende a replicação contínua de uma cópia do banco de dados que db1 hospedado no servidor MBX1. Um comentário opcional também foi especificado.

```powershell
Suspend-MailboxDatabaseCopy -Identity DB1\MBX1 -SuspendComment "Maintenance on MBX1" -Confirm:$False
```

Este exemplo suspende a ativação de uma cópia do banco de dados que DB2 hospedado no servidor MBX2.

```powershell
Suspend-MailboxDatabaseCopy -Identity DB2\MBX2 -ActivationOnly -Confirm:$False
```

## Use o Shell para retomar uma cópia do banco de dados de caixa de correio

Este exemplo retoma uma cópia do banco de dados DB1 do servidor MBX1.

```powershell
Resume-MailboxDatabaseCopy -Identity DB1\MBX1
```

Este exemplo retoma uma cópia do banco de dados DB2 no servidor MBX2 para somente a replicação.

```powershell
Resume-MailboxDatabaseCopy -Identity DB2\MBX2 -ReplicationOnly
```

## Como saber se funcionou?

Para verificar que você tenha suspensa ou retomada uma cópia do banco de dados de caixa de correio com êxito, siga um destes procedimentos:

  - No EAC, navegue até **Servidores** \> **Bancos de dados**. Selecione o banco de dados apropriado e, no painel Detalhes, clique em **Exibir detalhes**, para exibir as propriedades de cópia do banco de dados.

  - No Shell, execute este comando para mostrar informações de status para uma cópia do banco de dados.
    
    ```powershell
    Get-MailboxDatabaseCopyStatus <DatabaseCopyName> | Format-List
    ```

