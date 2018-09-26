---
title: 'Criar um banco de dados de recuperação: Exchange 2013 Help'
TOCTitle: Criar um banco de dados de recuperação
ms:assetid: 34d87491-b7b7-44a9-8d69-e1a9c1fe5852
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Ee332321(v=EXCHG.150)
ms:contentKeyID: 50485316
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Criar um banco de dados de recuperação

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2013-01-21_

Você pode usar o Shell para criar um banco de dados de recuperação, um tipo especial de banco de dados de caixa de correio que é usado para montar e extrair dados do banco de dados restaurado como parte de uma operação de recuperação. Depois de criar um banco de dados de recuperação, é possível mover um banco de dados de caixa de correio recuperado ou restaurado para o banco de dados de recuperação e usar o cmdlet [New-MailboxRestoreRequest](https://technet.microsoft.com/pt-br/library/ff829875\(v=exchg.150\)) para extrair dados do banco de dados recuperado. Após a extração, os dados podem ser exportados para uma pasta ou mesclados em uma caixa de correio existente. Usando-se bancos de dados de recuperação, é possível recuperar dados de um backup ou cópia de um banco de dados sem interromper o acesso do usuário aos dados atuais.

Procurando outras tarefas de gerenciamento relacionadas a bancos de dados de recuperação? Consulte [Bancos de dados de recuperação](recovery-databases-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para a conclusão da tarefa: 1 minuto

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Recuperação da caixa de correio" no tópico [Permissões de destinatários](recipients-permissions-exchange-2013-help.md) .

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]  
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>..



## Usar o Shell para criar um banco de dados de recuperação

Este exemplo cria o banco de dados de recuperação RDB1 no servidor Caixa de Correio MBX2.

```powershell
New-MailboxDatabase -Recovery -Name RDB1 -Server MBX2
```

Este exemplo cria o banco de dados de recuperação RDB2 no servidor Caixa de Correio MBX1 usando um caminho personalizado para o arquivo de banco de dados e a pasta de log.

  ```powershell
  New-MailboxDatabase -Recovery -Name RDB2 -Server MBX1 -EdbFilePath "C:\Recovery\RDB2\RDB2.EDB" -LogFolderPath "C:\Recovery\RDB2"
  ```

Para informações detalhadas sobre sintaxes e parâmetros, consulte [New-MailboxDatabase](https://technet.microsoft.com/pt-br/library/aa997976\(v=exchg.150\)).

## Como saber se funcionou?

Para verificar se você criou um banco de dados de recuperação com êxito, faça o seguinte:

  - No Shell, execute este comando para mostrar informações de configuração para uma cópia do banco de dados de recuperação:
    
    ```powershell
    Get-MailboxDatabase <RecoveryDatabaseName> | Format-List
    ```

## Outras tarefas

Depois de criar um banco de dados de recuperação, você talvez queira restaurar dados usando um banco de dados de recuperação. Para instruções detalhadas, consulte [Restaurar dados usando um banco de dados de recuperação](restore-data-using-a-recovery-database-exchange-2013-help.md).