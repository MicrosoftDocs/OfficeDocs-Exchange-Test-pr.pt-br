---
title: 'Executar uma recuperação de sinal de linha: Exchange 2013 Help'
TOCTitle: Executar uma recuperação de sinal de linha
ms:assetid: 158817fa-4b17-4fa9-8341-a86609e6a388
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Dd979810(v=EXCHG.150)
ms:contentKeyID: 51407839
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Executar uma recuperação de sinal de linha

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2014-06-27_

O uso da portabilidade de sinal de linha permite que os usuários tenham uma caixa de correio temporária para envio e recebimento de email enquanto a caixa de correio original está sendo restaurada ou reparada. A caixa de correio temporária pode estar no mesmo servidor de Caixa de Correio do Exchange 2013 ou em qualquer outro servidor de Caixa de Correio do Exchange 2013 em sua organização. O processo de uso da portabilidade de sinal de linha é chamado de recuperação de sinal de linha, que envolve a criação de um banco de dados vazio em um servidor de Caixa de Correio para substituir o banco de dados com falha. Para obter mais informações, consulte [Portabilidade de tom de discagem](dial-tone-portability-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: 5 minutos, mais o tempo que leva para restaurar e mover os dados

  - É preciso ter um número menor do que o máximo permitido de bancos de dados implantados para se criar um banco de dados de sinal de linha. O Exchange 2013 Standard Edition oferece suporte a um máximo de cinco bancos de dados por servidor. Exchange 2013 O Enterprise Edition suporta um máximo de 50 bancos de dados por servidor na RTM e CU1, e 100 bancos de dados por servidor no CU2 e posterior.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Recuperação da caixa de correio" no tópico [Permissões de destinatários](recipients-permissions-exchange-2013-help.md).

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>..



## Usar o Shell para executar uma recuperação de sinal de linha em um único servidor


> [!NOTE]
> Não é possível usar o EAC para executar uma recuperação de sinal de linha em um único servidor



1.  Verifique se possíveis arquivos existentes referentes ao banco de dados sendo movido são preservados caso eles sejam necessários para operações de recuperação futuras.

2.  Use o cmdlet [New-MailboxDatabase](https://technet.microsoft.com/pt-br/library/aa997976\(v=exchg.150\)) para criar um banco de dados de sinal de linha, como mostrado neste exemplo.
    
    ```powershell
    New-MailboxDatabase -Name DTDB1 -EdbFilePath D:\DialTone\DTDB1.EDB
    ```

3.  Use o cmdlet [Set-Mailbox](https://technet.microsoft.com/pt-br/library/bb123981\(v=exchg.150\)) para mover as caixas de correio do usuário hospedadas no banco de dados sendo recuperado, como mostrado neste exemplo.
    
    ```powershell
    Get-Mailbox -Database DB1 | Set-Mailbox -Database DTDB1
    ```

4.  Use o cmdlet [Mount-Database](https://technet.microsoft.com/pt-br/library/aa998871\(v=exchg.150\)) para montar o banco de dados para que os computadores clientes possam acessar o banco de dados e enviar e receber mensagens, como mostrado neste exemplo.
    
    ```powershell
    Mount-Database -Identity DTDB1
    ```

5.  Crie um banco de dados de recuperação (RDB) e restaure ou copie o banco de dados e os arquivos de log contendo os dados que deseja recuperar no RDB. Para obter etapas detalhadas, consulte [Criar um banco de dados de recuperação](create-a-recovery-database-exchange-2013-help.md).

6.  Após copiar os dados no RDB, mas antes de montar o banco de dados restaurado, copie os arquivos de log do banco de dados que apresentou falha para a pasta de logs de banco de dados de recuperação para que eles possam ser reproduzidos para o banco de dados restaurado.

7.  Monte o RDB e use o cmdlet [Dismount-Database](https://technet.microsoft.com/pt-br/library/bb124936\(v=exchg.150\)) para desmontá-lo, como mostrado neste exemplo.
    
    ```powershell
        Mount-Database -Identity RDB1  

        Dismount-Database -Identity RDB1
    ```

8.  Após a desmontagem do RDB, move o banco de dados atual e os arquivos de log que estão na pasta RDB para um local seguro. Isso é feito como preparação para trocar o banco de dados recuperado pelo banco de dados de sinal de linha.

9.  Desmonte o banco de dados de sinal de linha, como mostrado neste exemplo. Observe que os usuários finais terão uma interrupção no serviço quando você desmontar esse banco de dados.
    
    ```powershell
    Dismount-Database -Identity DTDB1
    ```

10. Mova o banco de dados e os arquivos de log da pasta do banco de dados de sinal de linha para a pasta do RDB.

11. Mova o banco de dados e os arquivos de log do local seguro que contém o banco de dados recuperado para a pasta do banco de dados de sinal de linha e monte o banco de dados, como mostrado neste exemplo.
    
    ```powershell
    Mount-Database -Identity DTDB1
    ```
    
    Isso encerra a interrupção de serviço para os seus usuários finais. Eles poderão acessar o banco de dados de produção original e enviar e receber mensagens.

12. Monte o RDB, como mostrado neste exemplo.
    
    ```powershell
    Mount-Database -Identity RDB1
    ```

13. Use os cmdlets [Get-Mailbox](https://technet.microsoft.com/pt-br/library/bb123685\(v=exchg.150\)) e [New-MailboxRestoreRequest](https://technet.microsoft.com/pt-br/library/ff829875\(v=exchg.150\)) para exportar os dados do RDB e importá-los no banco de dados recuperado, como mostrado neste exemplo. Essa ação importará todas as mensagens enviadas e recebidas, com o uso do banco de dados de sinal de linha no banco de dados de produção.
    

    ```powershell
        $mailboxes = Get-Mailbox -Database DTDB1
    ```

    ```powershell
        $mailboxes | %{ New-MailboxRestoreRequest -SourceStoreMailbox $_.ExchangeGuid -SourceDatabase RDB1 -TargetMailbox $_ }
    ```

14. Após o término da operação de restauração, você poderá desmontar e remover o RDB, como mostrado neste exemplo.
    
    ```powershell
        Dismount-Database -Identity RDB1  
        Remove-MailboxDatabase -Identity RDB1
    ```

Para obter informações detalhadas sobre sintaxes e parâmetros, consulte os seguintes tópicos:

  - [New-MailboxDatabase](https://technet.microsoft.com/pt-br/library/aa997976\(v=exchg.150\))

  - [Get-Mailbox](https://technet.microsoft.com/pt-br/library/bb123685\(v=exchg.150\))

  - [Set-Mailbox](https://technet.microsoft.com/pt-br/library/bb123981\(v=exchg.150\))

  - [Mount-Database](https://technet.microsoft.com/pt-br/library/aa998871\(v=exchg.150\))

  - [Dismount-Database](https://technet.microsoft.com/pt-br/library/bb124936\(v=exchg.150\))

  - [Remove-MailboxDatabase](https://technet.microsoft.com/pt-br/library/aa997931\(v=exchg.150\))

## Como saber se funcionou?

Para verificar se você moveu com êxito a caixa de correio, faça o seguinte:

  - Abra a caixa de correio usando o Microsoft Office Outlook Web App.

  - Abra a caixa de correio usando o Microsoft Outlook.

