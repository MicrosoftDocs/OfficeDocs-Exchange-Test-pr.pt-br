---
title: 'Adicionar uma cópia do banco de dados de caixa de correio: Exchange 2013 Help'
TOCTitle: Adicionar uma cópia do banco de dados de caixa de correio
ms:assetid: 784bf48f-8af5-422c-a63f-2f01fc0cf151
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Dd298080(v=EXCHG.150)
ms:contentKeyID: 50485843
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Adicionar uma cópia do banco de dados de caixa de correio

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2012-10-30_

Quando você adiciona uma cópia de um banco de dados de caixa de correio, a replicação contínua é ativada automaticamente entre a cópia do banco de dados e o banco de dados existente. Cópias de banco de dados são automaticamente atribuídas a uma identidade no formato de \<*DatabaseName*\> \\ \<*HostMailboxServerName*\>. Por exemplo, uma cópia do banco de dados DB1 hospedado no servidor MBX3 seria DB1\\MBX3.

Procurando outras tarefas de gerenciamento relacionadas a cópias do banco de dados de caixa de correio? Consulte [Gerenciando cópias de banco de dados de caixa de correio](managing-mailbox-database-copies-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão da tarefa: 2 minutos, mais o tempo para propagar a cópia do banco de dados, que depende de diversos fatores, como o tamanho do banco de dados, a velocidade, largura de banda disponível e latência da rede, e storage acelera.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte oEntrada "Cópias de banco de dados da caixa de correio" no tópico [Permissões de resiliência de site e disponibilidade altas](high-availability-and-site-resilience-permissions-exchange-2013-help.md).

  - A cópia ativa do banco de dados deve ser montada.

  - O servidor de caixa de correio especificado não deve hospedar uma cópia do banco de dados.

  - O caminho para a cópia do banco de dados e seus arquivos de log deve estar disponível no servidor de caixa de correio selecionado.

  - O servidor que hospeda a cópia ativa e o servidor que hospedará a cópia passiva deve estar no mesmo grupo de disponibilidade de banco de dados (DAG). O DAG também deve ter quórum e estar íntegro.

  - Se você estiver adicionando a segunda cópia de um banco de dados (por exemplo, criando a primeira cópia passiva do banco de dados), o log circular não deve ser habilitado para o banco de dados de caixa de correio especificada. Se o log circular estiver habilitado, você deverá desabilitá-lo. Após ter sido adicionada a cópia do banco de dados de caixa de correio, o log circular pode ser habilitado. Depois que o log circular estiver habilitado para um banco de dados de caixa de correio replicado, log circular de replicação contínua (CRCL) é usado no lugar de log circular do JET. Se você estiver adicionando a cópia de terceira ou subsequente de um banco de dados, CRCL pode permanecer ativada.

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>..



## O que você deseja fazer?

## Usar o EAC para adicionar uma cópia do banco de dados de caixa de correio

1.  
    
    Na EAC, vá até **Servidores** \> **Bancos de dados**.

2.  Selecione o banco de dados que você deseja copiar e clique em ![Adicionar cópia do banco de dados](images/Dd298080.435c15ff-abf2-4de8-b280-f053db1afa13(EXCHG.150).gif "Adicionar cópia do banco de dados").

3.  
    
    Na página **Adicionar a cópia do banco de dados de caixa de correio**, clique em **Procurar …**, selecione o servidor de caixa de correio que hospedará a cópia do banco de dados e clique em **Okey**.

4.  Se desejar, configure o **número de preferência de ativação** para a cópia do banco de dados.

5.  Clique em **mais opções …** para designar a cópia do banco de dados como uma cópia do banco de dados com retardamento Configurando um tempo de retardo de repetição ou adiar a propagação automática da cópia do banco de dados.

6.  Clique em **Salvar** para salvar as alterações na configuração e adicionar a cópia do banco de dados de caixa de correio.

7.  Clique em **Okey** para confirmar todas as mensagens que aparecem.

## Use o Shell para adicionar uma cópia do banco de dados de caixa de correio

Este exemplo adiciona uma cópia do banco de dados de caixa de correio DB1 para o servidor de caixa de correio MBX3. Tempo de retardo de repetição e tempo de retardo de truncamento forem deixadas em valores padrão de zero e a preferência de ativação é configurada com um valor de 2.

    Add-MailboxDatabaseCopy -Identity DB1 -MailboxServer MBX3 -ActivationPreference 2

Este exemplo adiciona uma cópia do banco de dados de caixa de correio DB2 para o servidor de caixa de correio MBX4. Tempo de retardo de repetição e tempo de retardo de truncamento forem deixadas em valores padrão de zero, e a preferência de ativação é configurada com um valor de `5`. Além disso, propagação está sendo adiado por essa cópia para que ele pode ser propagado usando um servidor de origem local, em vez da cópia ativa do banco de dados atual, o que é geograficamente distante de MBX4.

    Add-MailboxDatabaseCopy -Identity DB2 -MailboxServer MBX4 -ActivationPreference 5 -SeedingPostponed

Este exemplo adiciona uma cópia do banco de dados de caixa de correio DB3 para o servidor de caixa de correio MBX5. Tempo de retardo de repetição é definido como 3 dias, tempo de retardo de truncamento é deixado no valor padrão de zero e a preferência de ativação é configurada com um valor de `4`.

    Add-MailboxDatabaseCopy -Identity DB3 -MailboxServer MBX5 -ReplayLagTime 3.00:00:00 -ActivationPreference 4

## Como saber se funcionou?

Para verificar se você criou com êxito uma cópia do banco de dados de caixa de correio, siga um destes procedimentos:

  - No EAC, navegue até **servidores** \> **bancos de dados**. Selecione o banco de dados que foi copiado. No painel de detalhes, o status da cópia do banco de dados e seu índice de conteúdo são exibidos, juntamente com o comprimento da fila de cópia atual.

  - No Shell, execute o comando a seguir para verificar se a cópia do banco de dados de caixa de correio foi criada e está íntegra:
    
        Get-MailboxDatabaseCopyStatus <DatabaseCopyName>
    
    O Status e o estado do índice de conteúdo devem ser iguais a Íntegro.

## Para saber mais

[Cópias de banco de dados de caixa de correio](mailbox-database-copies-exchange-2013-help.md)

[Gerenciando cópias de banco de dados de caixa de correio](managing-mailbox-database-copies-exchange-2013-help.md)

