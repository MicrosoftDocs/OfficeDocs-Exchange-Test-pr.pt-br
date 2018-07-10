---
title: 'Atualizar uma cópia de banco de dados de caixa de correio: Exchange 2013 Help'
TOCTitle: Atualizar uma cópia de banco de dados de caixa de correio
ms:assetid: bead3cc5-7d50-446f-95b7-e432bcb7968e
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Dd351100(v=EXCHG.150)
ms:contentKeyID: 50486532
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Atualizar uma cópia de banco de dados de caixa de correio

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2012-11-02_

Atualizando, também conhecido como *propagação*, é o processo no qual uma cópia de um banco de dados de caixa de correio é adicionada para outro servidor de caixa de correio em um grupo de disponibilidade do banco de dados (DAG). A cópia recém-adicionado torna-se o banco de dados de linha de base para a cópia passiva em que os arquivos de log copiados da cópia ativa são repetidos. Propagação, é necessário nas seguintes condições:

  - Quando uma nova cópia passiva de um banco de dados é criada. Propagação pode ser adiado por uma nova cópia do banco de dados de caixa de correio, mas eventualmente, cada cópia passiva do banco de dados deve ser propagada para funcionar como uma cópia do banco de dados redundantes.

  - Após um failover ocorrer na qual os dados é perdida como resultado a cópia passiva do banco de dados ter se tornam divergência entre e não serão recuperáveis.

  - Quando o sistema detectou um arquivo de log corrompido que não pode ser copiado para a cópia passiva do banco de dados.

  - Após uma desfragmentação offline de qualquer cópia do banco de dados ocorre.

  - Após o log de sequência de geração do banco de dados foi redefinida novamente como 1.

Você pode executar a propagação usando os seguintes métodos:

  - **Propagação automática**   A propagação automática produz uma cópia passiva do banco de dados ativo no servidor de caixa de correio de destino. Propagação automática ocorre durante a criação de um banco de dados.

  - **Propagação usando o cmdlet Update-MailboxDatabaseCopy**   Você pode usar o cmdlet [Update-MailboxDatabaseCopy](https://technet.microsoft.com/pt-br/library/dd335201\(v=exchg.150\)) no Shell para propagar uma cópia do banco de dados a qualquer momento.

  - **Propagação usando o Assistente de cópia de banco de dados de caixa de correio de atualização**   Você pode usar o Assistente de cópia de banco de dados de caixa de correio de atualização no EAC para propagar uma cópia do banco de dados a qualquer momento.

  - **Copiando manualmente o banco de dados offline**   Você poderá desmontar a cópia ativa do banco de dados e copie o arquivo de banco de dados no mesmo local em outro servidor de caixa de correio no mesmo DAG. Se você usar esse método, haverá uma interrupção do serviço porque o processo requer que você desmonte o banco de dados.

Atualizando uma cópia do banco de dados pode levar muito tempo, especialmente se o banco de dados que está sendo copiado é grande, ou se não houver alta latência de rede ou baixa largura de banda. Depois de iniciado o processo de propagação, não feche o EAC ou o Shell até que o processo for concluído. Se fizer isso, a operação de propagação será encerrada.

Uma cópia do banco de dados pode ser propagada usando a cópia ativa ou uma cópia passiva atualizada como a fonte para a propagação. Quando a propagação de uma cópia passiva, lembre-se de que a operação de propagação terminará com um erro de comunicação de rede nas seguintes circunstâncias:

  - Se o status da propagação da fonte cópia altera a falha ou FailedAndSuspended.

  - Se o banco de dados realizar failover outra cópia.

Várias cópias de banco de dados podem ser propagadas simultaneamente. No entanto, quando várias cópias de propagação simultaneamente, você deve propagar somente o arquivo de banco de dados e omitir o catálogo de índice de conteúdo. Você pode fazer isso usando o parâmetro *DatabaseOnly* com o cmdlet [Update-MailboxDatabaseCopy](https://technet.microsoft.com/pt-br/library/dd335201\(v=exchg.150\)) .


> [!TIP]
> Se você não usar o parâmetro <EM>DatabaseOnly</EM> quando vários destinos da mesma origem de propagação, a tarefa falhará com erro SeedInProgressException FE1C6491.



Procurando outras tarefas de gerenciamento relacionadas a cópias do banco de dados de caixa de correio? Consulte [Gerenciando cópias de banco de dados de caixa de correio](managing-mailbox-database-copies-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão da tarefa: 2 minutos, mais o tempo para propagar a cópia do banco de dados, que depende de diversos fatores, como o tamanho do banco de dados, a velocidade, largura de banda disponível e latência da rede, e storage acelera.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte oEntrada "Cópias de banco de dados da caixa de correio" no tópico [Permissões de resiliência de site e disponibilidade altas](high-availability-and-site-resilience-permissions-exchange-2013-help.md).

  - A cópia do banco de dados de caixa de correio deve ser suspenso. Para obter etapas detalhadas, consulte [Suspender ou retomar uma cópia do banco de dados de caixa de correio](suspend-or-resume-a-mailbox-database-copy-exchange-2013-help.md).

  - O serviço de registro remoto deve estar executando no servidor que hospeda a cópia passiva do banco de dados que você está atualizando.

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>..



## O que você deseja fazer?

## Usar o EAC para atualizar uma cópia do banco de dados de caixa de correio

1.  Na EAC, vá até **Servidores** \> **Bancos de dados**.

2.  Selecione o banco de dados de caixa de correio cuja cópia passiva que você deseja atualizar.

3.  No painel de detalhes, em **Cópias de banco de dados**, clique em **Suspend** sob a cópia passiva do banco de dados que deseja propagação. Forneça qualquer comentário opcional e clique em **Salvar**.

4.  No painel de detalhes, em **Cópias de banco de dados**, clique em **Atualizar** sob a cópia passiva do banco de dados que deseja propagação.

5.  
    
    Por padrão, a cópia ativa do banco de dados é usada como o banco de dados de origem para propagação. Se você preferir usar uma cópia passiva do banco de dados para propagação, clique em **Procurar...** para selecionar o servidor que contém a cópia passiva do banco de dados que você deseja usar para a fonte.

6.  Clique em **Salvar** para atualizar a cópia passiva do banco de dados.

## Use o Shell para atualizar uma cópia do banco de dados de caixa de correio

Este exemplo mostra como propagar uma cópia do banco de dados DB1 no MBX1.

    Update-MailboxDatabaseCopy -Identity DB1\MBX1

Este exemplo mostra como propagar uma cópia do banco de dados DB1 MBX1 usando o MBX2 como o servidor de caixa de correio de origem para a propagação.

    Update-MailboxDatabaseCopy -Identity DB1\MBX1 -SourceServer MBX2

Este exemplo mostra como propagar uma cópia do banco de dados DB1 no MBX1 sem propagar o catálogo de índice de conteúdo.

    Update-MailboxDatabaseCopy -Identity DB1\MBX1 -DatabaseOnly

Este exemplo mostra como propagar o catálogo de índice de conteúdo para a cópia do banco de dados DB1 MBX1 sem propagar o arquivo de banco de dados.

    Update-MailboxDatabaseCopy -Identity DB1\MBX1 -CatalogOnly

## Copiar manualmente um banco de dados offline

1.  Se o log circular for habilitado para o banco de dados, ele deverá ser desabilitado antes de continuar. É possível desabilitar o log circular de um banco de dados de caixa de correio usando o cmdlet [Set-MailboxDatabase](https://technet.microsoft.com/pt-br/library/bb123971\(v=exchg.150\)), conforme mostrado nesse exemplo.
    
        Set-MailboxDatabase DB1 -CircularLoggingEnabled $false

2.  Desmonte o banco de dados. Você pode usar o cmdlet [Dismount-Database](https://technet.microsoft.com/pt-br/library/bb124936\(v=exchg.150\)) , conforme mostrado neste exemplo.
    
        Dismount-Database DB1 -Confirm $false

3.  Copie manualmente os arquivos de banco de dados (o arquivo de banco de dados e todos os arquivos de log) para um local de segundo, como uma unidade de disco externa ou compartilhamento de rede.

4.  Monte o banco de dados. Você pode usar o cmdlet [Mount-Database](https://technet.microsoft.com/pt-br/library/aa998871\(v=exchg.150\)) , conforme mostrado neste exemplo.
    
        Mount-Database DB1

5.  No servidor que hospedará a cópia, copie os arquivos de banco de dados do compartilhamento de rede ou unidade externo para o mesmo caminho como a cópia do banco de dados ativo. Por exemplo, se o caminho do banco de dados de cópia ativa é D:\\DB1\\DB1.edb e o caminho do arquivo de log é D:\\DB1, copie os arquivos de banco de dados para D:\\DB1 no servidor que irá hospedar a cópia.

6.  Adicione a cópia do banco de dados de caixa de correio usando o cmdlet [Add-MailboxDatabaseCopy](https://technet.microsoft.com/pt-br/library/dd298105\(v=exchg.150\)) com o parâmetro *SeedingPostponed* , conforme mostrado neste exemplo.
    
        Add-MailboxDatabaseCopy -Identity DB1 -MailboxServer MBX3 -SeedingPostponed

7.  Se o log circular está habilitado para o banco de dados, habilitá-lo novamente usando o cmdlet [Set-MailboxDatabase](https://technet.microsoft.com/pt-br/library/bb123971\(v=exchg.150\)) , conforme mostrado neste exemplo.
    
        Set-MailboxDatabase DB1 -CircularLoggingEnabled $true

## Como saber se funcionou?

Para verificar se você tiver propagado com êxito uma cópia do banco de dados de caixa de correio, siga um destes procedimentos:

  - No EAC, navegue até **servidores** \> **bancos de dados**. Selecione o banco de dados que foi propagado. No painel de detalhes, o status da cópia do banco de dados e seu índice de conteúdo são exibidos, juntamente com o comprimento da fila de cópia atual.

  - No Shell, execute o seguinte comando para verificar a cópia do banco de dados de caixa de correio foi propagada com êxito e está íntegra.
    
        Get-MailboxDatabaseCopyStatus <DatabaseCopyName>
    
    O Status e o estado do índice de conteúdo devem ser iguais a Íntegro.

