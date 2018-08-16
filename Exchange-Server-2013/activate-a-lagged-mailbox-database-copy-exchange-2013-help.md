---
title: 'Ativar uma cópia do banco de dados de caixa de correio com atraso'
TOCTitle: Ativar uma cópia do banco de dados de caixa de correio com atraso
ms:assetid: 493d9c40-644d-49d6-9291-949acbcfdcb6
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Dd979786(v=EXCHG.150)
ms:contentKeyID: 50485506
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Ativar uma cópia do banco de dados de caixa de correio com atraso

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2014-01-28_

Uma cópia de banco de dados de caixa de correio com atraso é uma cópia de banco de dados de caixa de correio configurada com um tempo de atraso para repetição maior do que 0. A ativação e a recuperação de um banco de dados de caixa de correio é um processo simples caso deseje que o banco de dados repita todos os arquivos de log e torne atual a cópia do banco de dados. Se você quiser repetir arquivos de log até um ponto específico no tempo, a operação é mais difícil, porque é preciso manipular manualmente os arquivos de log e executar o Eseutil.

Você está procurando por outras informações relacionadas a cópias de bancos de dados de caixa de correio atrasadas? Consulte [Gerenciando cópias de banco de dados de caixa de correio](managing-mailbox-database-copies-exchange-2013-help.md).


> [!NOTE]
> O tempo para a ativação direta de uma cópia de banco de dados de caixa de correio com atraso depende diretamente de quantos arquivos de log precisam ser repetidos e da velocidade com que o hardware pode repeti-los. Você deverá ver uma taxa de repetição de log de, pelo menos, dois logs por segundo por banco de dados.



## O que você precisa saber antes de começar?

  - Tempo estimado para a conclusão da tarefa: 1 minuto, mais o tempo necessário para duplicar a cópia com atraso, repetir os arquivos de log necessários e extrair os dados ou montar o banco de dados para atividade do cliente.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte oEntrada "Cópias de banco de dados da caixa de correio" no tópico [Permissões de resiliência de site e disponibilidade altas](high-availability-and-site-resilience-permissions-exchange-2013-help.md).

  - A cópia de banco de dados de caixa de correio que está sendo ativada deve ser configurada com um tempo de atraso de repetição maior do que 0.

  - A cópia de banco de dados de caixa de correio que está sendo ativada deve ter todos os arquivos de log até o momento específico que você deseja recuperar. Tenha em mente que as transações de banco de dados podem conter vários arquivos de log ao determinar o momento específico que você deseja recuperar.

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>..



## O que você deseja fazer?

## Usar o Shell para ativar uma cópia de banco de dados de caixa de correio com atraso até um momento específico


> [!NOTE]
> O EAC não pode ser usado para ativar uma cópia de banco de dados de caixa de correio com atraso em um momento específico. Em vez disso, você segue uma série de etapas usando o Shell e a linha de comando.



1.  Este exemplo suspende a replicação para a cópia com atraso que está sendo ativada usando o cmdlet [Suspend-MailboxDatabaseCopy](https://technet.microsoft.com/pt-br/library/dd351074\(v=exchg.150\)).
    
        Suspend-MailboxDatabaseCopy DB1\EX3 -SuspendComment "Activate lagged copy of DB1 on Server EX3" -Confirm:$false

2.  Opcionalmente (para preservar uma cópia com atraso), faça uma cópia do banco de dados e de seus arquivos de log.
    

    > [!NOTE]
    > Neste ponto, continuar realizando este procedimento no volume existente levaria a uma penalidade de desempenho de cópia na gravação. Se isso não for o que você deseja, é possível copiar o banco de dados e os arquivos de log para outro volume para realizar a recuperação.



3.  Determine quais arquivos de log precisam ser repetidos para o banco de dados para atingir o momento específico desejado para a recuperação (baseado na data e na hora dos arquivos de log, conforme exibidas no Windows Explorer). Todos os logs criados após esse ponto devem ser movidos para um diretório diferente, até que o processo de recuperação seja concluído e os logs não sejam mais necessários.

4.  Exclua o arquivo de verificação (.chk) do banco de dados.

5.  Este exemplo usa o Eseutil para executar a operação de recuperação.
    
        Eseutil.exe /r eXX /a
    

    > [!NOTE]
    > No exemplo anterior, e<EM>XX</EM> é o prefixo de geração de log do banco de dados (por exemplo, E00, E01, E02 e assim por diante).

    

    > [!IMPORTANT]
    > Essa etapa pode levar um tempo considerável, dependendo de diversos fatores, como a extensão do tempo de atraso de repetição, o número de arquivos de log gerados durante esse período e a velocidade com que o hardware pode repetir esses logs para o banco de dados que está sendo recuperado.



6.  Depois que a repetição de log é concluída, o banco de dados está em um estado de desligamento normal e pode ser copiado e usado para fins de recuperação.

7.  Após a conclusão do processo de recuperação, este exemplo retoma a replicação do banco de dados usado como parte do processo de recuperação.
    
        Resume-MailboxDatabaseCopy DB1\EX3

Para informações detalhadas de sintaxes e de parâmetros, consulte [Suspend-MailboxDatabaseCopy](https://technet.microsoft.com/pt-br/library/dd351074\(v=exchg.150\)) ou [Resume-MailboxDatabaseCopy](https://technet.microsoft.com/pt-br/library/dd335220\(v=exchg.150\)).

## Usar o Shell para ativar uma cópia de banco de dados de caixa de correio com atraso repetindo todos os arquivos de log não confirmados

1.  Opcionalmente (para preservar uma cópia com atraso), faça uma cópia do banco de dados e de seus arquivos de log.
    
    1.  Este exemplo suspende a replicação para a cópia com atraso que está sendo ativada usando o cmdlet [Suspend-MailboxDatabaseCopy](https://technet.microsoft.com/pt-br/library/dd351074\(v=exchg.150\)).
        
            Suspend-MailboxDatabaseCopy DB1\EX3 -SuspendComment "Activate lagged copy of DB1 on Server EX3" -Confirm:$false
    
    2.  Opcionalmente (para preservar uma cópia com atraso), faça uma cópia do banco de dados e de seus arquivos de log.
        

        > [!NOTE]
        > Neste ponto, continuar realizando este procedimento no volume existente levaria a uma penalidade de desempenho de cópia na gravação. Se isso não for o que você deseja, é possível copiar o banco de dados e os arquivos de log para outro volume para realizar a recuperação.



2.  Este exemplo ativa a cópia do banco de dados de caixa de correio com atraso usando o cmdlet [Move-ActiveMailboxDatabase](https://technet.microsoft.com/pt-br/library/dd298068\(v=exchg.150\)) com o parâmetro *SkipLagChecks*.
    
        Move-ActiveMailboxDatabase DB1 -ActivateOnServer EX3 -SkipLagChecks

## Use o Shell para ativar uma cópia do banco de dados de caixa de correio com atraso usando a recuperação SafetyNet

1.  Outra opção (para preservar uma cópia com atraso) é criar um instantâneo do VSS (Serviço de Cópias de Sombra de Volume), com base no sistema de arquivos (não ciente do Exchange), dos volumes que contêm a cópia do banco de dados e seus arquivos de log.
    
    1.  Este exemplo suspende a replicação para a cópia com atraso que está sendo ativada usando o cmdlet [Suspend-MailboxDatabaseCopy](https://technet.microsoft.com/pt-br/library/dd351074\(v=exchg.150\)).
        
            Suspend-MailboxDatabaseCopy DB1\EX3 -SuspendComment "Activate lagged copy of DB1 on Server EX3" -Confirm:$false
    
    2.  Opcionalmente (para preservar uma cópia com atraso), faça uma cópia do banco de dados e de seus arquivos de log.
        

        > [!NOTE]
        > Neste ponto, continuar realizando este procedimento no volume existente levaria a uma penalidade de desempenho de cópia na gravação. Se isso não for o que você deseja, é possível copiar o banco de dados e os arquivos de log para outro volume para realizar a recuperação.



2.  Determine os logs necessários para a cópia de banco de dados com atraso ao procurar por "Log Necessário:" valor na saída de cabeçalho de banco de dados de ESEUTIL
    
        Eseutil /mh <DBPath> | findstr /c:"Log Required"
    
    Tome nota dos números hexadecimais entre parênteses. O primeiro número é a geração mais baixa necessária (mencionada como LowGeneration), e o segundo número é a geração mais alta necessária (mencionada como HighGeneration). Mova todos os arquivos de geração de log com uma sequência de geração maior do que HighGeneration para um local diferente para que eles não sejam reproduzidos novamente no banco de dados.

3.  No servidor que hospeda a cópia ativa do banco de dados, exclua os arquivos de log da cópia com atraso sendo ativada da cópia ativa ou pare o serviço de Replicação do Microsoft Exchange.

4.  Execute uma alternância de banco de dados e ative a cópia com atraso. Este exemplo ativa o banco de dados usando o cmdlet [Move-ActiveMailboxDatabase](https://technet.microsoft.com/pt-br/library/dd298068\(v=exchg.150\)) com vários parâmetros.
    
        Move-ActiveMailboxDatabase DB1 -ActivateOnServer EX3 -MountDialOverride BestEffort -SkipActiveCopyChecks -SkipClientExperienceChecks -SkipHealthChecks -SkipLagChecks

5.  Nesse momento, o banco de dados montará automaticamente e solicitará a nova entrega de mensagens ausentes do SafetyNet.

## Como saber se funcionou?

Para verificar se você ativou com êxito uma cópia de banco de dados de caixa de correio com atraso, execute um destes procedimentos:

  - No EAC, navegue até **Servidores** \> **Bancos de dados**. Selecione o banco de dados apropriado e, no painel Detalhes, clique em **Exibir detalhes**, para exibir as propriedades de cópia do banco de dados.

  - No Shell, execute este comando para mostrar informações de status para uma cópia do banco de dados.
    
        Get-MailboxDatabaseCopyStatus <DatabaseCopyName> | Format-List

