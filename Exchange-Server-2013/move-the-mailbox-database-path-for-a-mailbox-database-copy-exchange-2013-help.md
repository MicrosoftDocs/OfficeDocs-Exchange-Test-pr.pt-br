---
title: 'Mover o caminho do banco de dados de caixa de correio para uma cópia do banco de dados de caixa de correio: Exchange 2013 Help'
TOCTitle: Mover o caminho do banco de dados de caixa de correio para uma cópia do banco de dados de caixa de correio
ms:assetid: 324f255c-d95d-4a8a-a134-c8cee5c5b9cb
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Dd979782(v=EXCHG.150)
ms:contentKeyID: 50485276
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Mover o caminho do banco de dados de caixa de correio para uma cópia do banco de dados de caixa de correio

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2014-05-07_

Após a criação de um banco de dados de caixa de correio, você pode movê-lo para outro volume, pasta, local ou caminho usando o EAC ou o Shell. Para obter instruções passo a passo sobre como mover o caminho do banco de dados para um banco de dados de caixa de correio não replicado, consulte [Move a mailbox database path](manage-mailbox-databases-in-exchange-2013-exchange-2013-help.md).

Se esse banco de dados sendo movido for replicado para uma ou mais cópias de banco de dados de caixa de correio, siga o procedimento neste tópico para mover o caminho desse banco de dados. Todas as cópias de um banco de dados de caixa de correio devem estar no mesmo caminho em cada servidor que hospeda uma cópia. Por exemplo, se o banco de dados DB1 estiver localizado em C:\\mountpoints\\DB1 no servidor EX1, cópias de DB1 nos servidores EX2, EX3 etc. deverão também estar localizadas em C:\\mountpoints\\DB1.

Procurando outras tarefas de gerenciamento relacionadas a cópias do banco de dados de caixa de correio? Consulte [Gerenciando cópias de banco de dados de caixa de correio](managing-mailbox-database-copies-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para a conclusão da tarefa: 2 minutos, mais o tempo para mover os dados, que depende de diversos fatores, tais como tamanho do banco do dados, velocidade, largura de banda disponível, latência da rede e velocidades de armazenamento.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte oEntrada "Cópias de banco de dados da caixa de correio" no tópico [Permissões de resiliência de site e disponibilidade altas](high-availability-and-site-resilience-permissions-exchange-2013-help.md).

  - Para executar a operação de movimentação, o banco de dados deve ser desmontado temporariamente, tornando-o inacessível para todos os usuários. Se estiver desmontado no momento, o banco de dados não será remontado após a conclusão.

  - Para executar a operação de movimentação, a replicação do banco de dados deverá estar desabilitada para todas as cópias. Não é suficiente suspender a replicação; é preciso desabilitá-la usando o cmdlet [Remove-MailboxDatabaseCopy](https://technet.microsoft.com/pt-br/library/dd335119\(v=exchg.150\)) para remover as cópias de banco de dados.

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>..



## Usar o Shell para mover um banco de dados de caixa de correio replicado para um novo caminho


> [!TIP]
> Não é possível usar o EAC para mover um banco de dados de caixa de correio replicado para um novo caminho.



1.  Observe todas as configurações de tempo de retardo ou retardo de truncamento para todas as cópias do banco de dados de caixa de correio sendo movidas. É possível obter essas informações usando o cmdlet [Get-MailboxDatabase](https://technet.microsoft.com/pt-br/library/bb124924\(v=exchg.150\)), conforme mostrado nesse exemplo.
    
        Get-MailboxDatabase DB1 | Format-List *lag*

2.  Se o log circular for habilitado para o banco de dados, ele deverá ser desabilitado antes de continuar. É possível desabilitar o log circular de um banco de dados de caixa de correio usando o cmdlet [Set-MailboxDatabase](https://technet.microsoft.com/pt-br/library/bb123971\(v=exchg.150\)), conforme mostrado nesse exemplo.
    
        Set-MailboxDatabase DB1 -CircularLoggingEnabled $false

3.  Remova todas as cópias de banco de dados de caixa de correio para o banco de dados sendo movido. Para obter etapas detalhadas, consulte [Remover uma cópia do banco de dados de caixa de correio](remove-a-mailbox-database-copy-exchange-2013-help.md). Após a remoção de todas as cópias, preserve os arquivos de log de banco de dados e de transação de cada servidor a partir do qual a cópia de banco de dados está sendo removida movendo-os para outro local. Esses arquivos estão sendo preservados para que as cópias de banco de dados não exijam o reenvio após terem sido adicionadas novamente.

4.  Mova o caminho do banco de dados de caixa de correio para o novo local. Para obter etapas detalhadas, consulte [Move a mailbox database path](manage-mailbox-databases-in-exchange-2013-exchange-2013-help.md).
    

    > [!IMPORTANT]
    > Durante a operação de movimentação, o banco de dados sendo movido deve ser desmontado. Até a movimentação terminar, esse processo causará uma interrupção no serviço para todos os usuários com caixas de correio no banco de dados sendo movido. Após o término da operação de movimentação, o banco de dados será montado automaticamente.



5.  Crie a estrutura de pastas necessária em cada servidor de caixa de correio que anteriormente tinha uma cópia passiva do banco de dados de caixa de correio movido. Por exemplo, se tiver movido o banco de dados para C:\\mountpoints\\DB1, será preciso criar esse mesmo caminho em cada servidor de caixa de correio que hospedará uma cópia de banco de dados de caixa de correio.

6.  Após a criação da estrutura de pastas, mova a cópia passiva do banco de dados de caixa de correio e seu fluxo de logs para o novo local. Esses são os arquivos que restaram e foram preservados após a Etapa 3. Repita esse processo para cada cópia de banco de dados removida na Etapa 3.

7.  Adicione todas as cópias de banco de dados removidas na Etapa 3. Para obter etapas detalhadas, consulte [Adicionar uma cópia do banco de dados de caixa de correio](add-a-mailbox-database-copy-exchange-2013-help.md).

8.  Em cada servidor que existe uma cópia do banco de dados de caixa de correio sendo movido, execute os seguintes comandos para interromper e reiniciar os serviços de índice de conteúdo.
    
        Net stop MSExchangeFastSearch
        Net start MSExchangeFastSearch

9.  Opcionalmente, habilite o log circular usando o cmdlet [Set-MailboxDatabase](https://technet.microsoft.com/pt-br/library/bb123971\(v=exchg.150\)), como mostrado nesse exemplo.
    
        Set-MailboxDatabase DB1 -CircularLoggingEnabled $true

10. Reconfigure quaisquer valores definidos anteriormente para tempo de retardo de repetição ou tempo de retardo de truncamento usando o cmdlet [Set-MailboxDatabaseCopy](https://technet.microsoft.com/pt-br/library/dd298104\(v=exchg.150\)), como mostrado neste exemplo.
    
        Set-MailboxDatabaseCopy DB1\MBX2 -ReplayLagTime 00:15:00

11. À medida que cada cópia for adicionada, recomendamos verificar a integridade e o status da cópia antes de adicionar a próxima cópia. Você pode verificar a integridade e o status por:
    
    1.  Examinando o log de eventos de qualquer evento de erro ou aviso relacionado ao banco de dados ou à cópia de banco de dados.
    
    2.  Usando o cmdlet [Get-MailboxDatabaseCopyStatus](https://technet.microsoft.com/pt-br/library/dd298044\(v=exchg.150\)) para verificar a integridade e o status de replicação contínua para a cópia de banco de dados.
    
    3.  Usando o cmdlet [Test-ReplicationHealth](https://technet.microsoft.com/pt-br/library/bb691314\(v=exchg.150\)) para verificar a integridade e o status de replicação contínua e do grupo de disponibilidade de banco de dados.

Para obter informações detalhadas sobre sintaxes e parâmetros, consulte os seguintes tópicos:

  - [Get-MailboxDatabase](https://technet.microsoft.com/pt-br/library/bb124924\(v=exchg.150\))

  - [Set-MailboxDatabase](https://technet.microsoft.com/pt-br/library/bb123971\(v=exchg.150\))

  - [Set-MailboxDatabaseCopy](https://technet.microsoft.com/pt-br/library/dd298104\(v=exchg.150\))

  - [Get-MailboxDatabaseCopyStatus](https://technet.microsoft.com/pt-br/library/dd298044\(v=exchg.150\))

  - [Test-ReplicationHealth](https://technet.microsoft.com/pt-br/library/bb691314\(v=exchg.150\))

## Como saber se funcionou?

Para verificar se você moveu com êxito o caminho de uma cópia de banco de dados de caixa de correio, execute um destes procedimentos:

  - No EAC, navegue até **Servidores** \> **Bancos de dados**. Selecione o banco de dados que foi copiado. No painel Detalhes, o status da cópia do banco de dados e o índice do conteúdo são exibidos, assim como o comprimento da fila da cópia atual. Verifique se o status é Íntegro.

  - No Shell, execute o comando a seguir para verificar se a cópia do banco de dados de caixa de correio foi criada e está íntegra:
    
        Get-MailboxDatabaseCopyStatus <DatabaseCopyName>
    
    O Status e o estado do índice de conteúdo devem ser iguais a Íntegro.

