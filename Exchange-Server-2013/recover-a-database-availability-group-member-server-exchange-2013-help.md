---
title: 'Recuperar um servidor membro de grupo de disponibilidade de banco de dados: Exchange 2013 Help'
TOCTitle: Recuperar um servidor membro de grupo de disponibilidade de banco de dados
ms:assetid: eccd8f61-9706-4bb7-a62a-ec7c166f8019
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Dd638206(v=EXCHG.150)
ms:contentKeyID: 50486940
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Recuperar um servidor membro de grupo de disponibilidade de banco de dados

 

_**Aplica-se a:**Exchange Server 2013_

_**Tópico modificado em:**2016-12-09_

Se um servidor de correio que seja membro de um grupo de disponibilidade do banco de dados (DAG) é perdido ou caso contrário, falha e é irrecuperável e precisa substituição, você pode executar uma operação de recuperação do servidor. Microsoft Exchange Server 2013 instalação inclui a opção */m:RecoverServer* que podem ser usados para executar a operação de recuperação do servidor. Executando a instalação com as causas de comutador */m:RecoverServer* Setup para ler informações de configuração do servidor de Active Directory para um servidor com o mesmo nome que o servidor do qual você está executando a instalação. Após a configuração do servidor informações forem coletadas das Active Directory, os arquivos originais de Exchange serviços então são instalados no servidor e as funções e as configurações que foram armazenadas nos Active Directory são aplicadas ao servidor.

Procurando outras tarefas de gerenciamento relacionadas a DAGs? Consulte [Gerenciando grupos de disponibilidade de banco de dados](managing-database-availability-groups-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: 30 minutos

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte oEntrada "Cópias de banco de dados da caixa de correio" no tópico [Permissões de resiliência de site e disponibilidade altas](high-availability-and-site-resilience-permissions-exchange-2013-help.md).

  - Se Exchange estiver instalado em um local diferente do local padrão, você deve usar a opção de instalação do */TargetDir* para especificar a localização dos arquivos de programa do Exchange. Se você não usar a opção */TargetDir* , os arquivos de programa do Exchange serão instalados no local padrão (%programfiles%\\Microsoft\\Exchange Server\\V15).
    
    Para determinar o local de instalação, siga estas etapas:
    
    1.  Abra o ADSIEDIT.MSC ou LDP.EXE.
    
    2.  Navegue para o seguinte local: **CN=ExServerName,CN=Servers,CN=First Administrative Group,CN=Administrative Groups,CN=ExOrg Name,CN=Microsoft Exchange,CN=Services,CN=Configuration,DC=DomainName,CN=Com**
    
    3.  Clique com o botão direito no objeto do servidor Exchange e clique em **Propriedades**.
    
    4.  Localize o atributo **msExchInstallPath**. Este atributo armazena o caminho de instalação atual.

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>..



## Usar o Setup /m:RecoverServer para recuperar um servidor

1.  Recupere configurações de atraso de repetição e atraso de truncamento para quaisquer cópias de bancos de dados de caixa de correio que existam no servidor que está sendo recuperado usando o cmdlet [Get-MailboxDatabase](https://technet.microsoft.com/pt-br/library/bb124924\(v=exchg.150\)):
    
        Get-MailboxDatabase DB1 | Format-List *lag*

2.  Remova quaisquer cópias de bancos de dados de caixa de correio que existam no servidor que está sendo recuperado usando o cmdlet [Remove-MailboxDatabaseCopy](https://technet.microsoft.com/pt-br/library/dd335119\(v=exchg.150\)):
    
        Remove-MailboxDatabaseCopy DB1\MBX1

3.  Remova a configuração de servidores com falha do DAG usando o cmdlet [Remove-DatabaseAvailabilityGroupServer](https://technet.microsoft.com/pt-br/library/dd297956\(v=exchg.150\)):
    
        Remove-DatabaseAvailabilityGroupServer -Identity DAG1 -MailboxServer MBX1
    

    > [!TIP]
    > Se o membro do DAG que está sendo removido estiver offline e não pode ser colocado online, você deve adicionar o parâmetro <EM>ConfigurationOnly</EM> para o comando anterior. Se você usar a opção <EM>ConfigurationOnly</EM> , você deve remover também manualmente o nó do cluster.



4.  Redefina a conta de computador do servidor no Active Directory. Para obter etapas detalhadas, consulte [Redefinir uma conta de computador](http://go.microsoft.com/fwlink/p/?linkid=167188).

5.  Abra uma janela do Prompt de Comando. Usando a mídia de Instalação original, execute este comando:
    
        Setup /m:RecoverServer

6.  Ao término do processo de recuperação da Instalação, adicione o servidor recuperado ao DAG usando o cmdlet [Add-DatabaseAvailabilityGroupServer](https://technet.microsoft.com/pt-br/library/dd298049\(v=exchg.150\)):
    
        Add-DatabaseAvailabilityGroupServer -Identity DAG1 -MailboxServer MBX1

7.  Após a inclusão do servidor de volta ao DAG, você pode reconfigurar as cópias do banco de dados de caixa de correio usando o cmdlet [Add-MailboxDatabaseCopy](https://technet.microsoft.com/pt-br/library/dd298105\(v=exchg.150\)). Se uma das cópias de banco de dados adicionada teve antes tempo de atraso de repetição ou tempo de atraso de truncamento superior a 0, você pode usar os parâmetros *ReplayLagTime* e *TruncationLagTime* do cmdlet [Add-MailboxDatabaseCopy](https://technet.microsoft.com/pt-br/library/dd298105\(v=exchg.150\)) para reconfigurar estas definições:
    
        Add-MailboxDatabaseCopy -Identity DB1 -MailboxServer MBX1
        Add-MailboxDatabaseCopy -Identity DB2 -MailboxServer MBX1 -ReplayLagTime 3.00:00:00
        Add-MailboxDatabaseCopy -Identity DB3 -MailboxServer MBX1 -ReplayLagTime 3.00:00:00 -TruncationLagTime 3.00:00:00

## Como saber se funcionou?

Para verificar que você tiver recuperado com êxito o membro do DAG, faça o seguinte:

  - No Shell, execute o seguinte comando para verificar a integridade e o status do membro DAG recuperado.
    
        Test-ReplicationHealth <ServerName>
    
        Get-MailboxDatabaseCopyStatus -Server <ServerName>
    
    Todos os testes de integridade de replicação devem passar com êxito e o status dos bancos de dados e seus índices de conteúdo deve estar íntegro.

