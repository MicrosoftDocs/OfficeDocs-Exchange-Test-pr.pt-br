---
title: 'Remover uma cópia do banco de dados de caixa de correio: Exchange 2013 Help'
TOCTitle: Remover uma cópia do banco de dados de caixa de correio
ms:assetid: 99fecdde-b158-4dfc-9ca7-ff7c0ada7819
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Dd298164(v=EXCHG.150)
ms:contentKeyID: 50486204
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Remover uma cópia do banco de dados de caixa de correio

 

_**Aplica-se a:**Exchange Server 2013_

_**Tópico modificado em:**2012-11-06_

Estes procedimentos mostram como remover uma cópia de um banco de dados de caixa de correio. Você não pode usar estes procedimentos para remover da última cópia de um banco de dados de caixa de correio. Para obter instruções detalhadas sobre como remover da última cópia de um banco de dados de caixa de correio, consulte [Remove a mailbox database](manage-mailbox-databases-in-exchange-2013-exchange-2013-help.md) ou [Remove-MailboxDatabase](https://technet.microsoft.com/pt-br/library/aa997931\(v=exchg.150\)).

Procurando outras tarefas de gerenciamento relacionadas a cópias do banco de dados de caixa de correio? Consulte [Gerenciando cópias de banco de dados de caixa de correio](managing-mailbox-database-copies-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para a conclusão da tarefa: 1 minuto

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte oEntrada "Cópias de banco de dados da caixa de correio" no tópico [Permissões de resiliência de site e disponibilidade altas](high-availability-and-site-resilience-permissions-exchange-2013-help.md).

  - Cópias de banco de dados de caixa de correio só podem ser removidas de um grupo de disponibilidade de integridade do banco de dados (DAG). Se o DAG não está íntegro (por exemplo, cluster subjacente do DAG está inoperante porque quorum foi perdida), você não poderá remover quaisquer cópias de banco de dados de caixa de correio.

  - Se você estiver removendo a última cópia passiva do banco de dados, o log circular de replicação contínua (CRCL) não deve ser habilitado para o banco de dados de caixa de correio especificada. Se o CRCL está habilitado, você deverá desabilitá-lo. Depois que a cópia do banco de dados de caixa de correio foi removida, o log circular pode ser habilitado. Quando habilitado para um banco de dados de caixa de correio não replicado, log circular do JET é usado no lugar de CRCL. Se você não estiver removendo da última cópia passiva de um banco de dados, CRCL pode permanecer ativada.

  - Após a remoção de uma cópia do banco de dados, você deve excluir manualmente os arquivos de log de transações e de banco de dados do servidor do qual a cópia do banco de dados está sendo removida.

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>..



## O que você deseja fazer?

## Usar o EAC para remover uma cópia do banco de dados de caixa de correio

1.  Na EAC, vá até **Servidores** \> **Bancos de dados**.

2.  Selecione o banco de dados de caixa de correio cuja cópia que você deseja remover.

3.  No painel de detalhes, localize a cópia passiva que você deseja remover e clique em **Remover**.

4.  Confirme a remoção na caixa de diálogo de aviso clicando em **Sim**.

5.  Clique em **okey** para confirmar a remoção após revisar todas as mensagens.

6.  Exclua manualmente os arquivos de log de transações e de banco de dados do servidor do qual a cópia do banco de dados está sendo removida.

## Usar o Shell para remover uma cópia do banco de dados de caixa de correio

Este exemplo remove uma cópia do banco de dados da caixa de correio DB1 do servidor de caixa de correio MBX1.

    Remove-MailboxDatabaseCopy -Identity DB1\MBX1 -Confirm:$False

## Como saber se funcionou?

Para verificar se você removeu com êxito uma cópia do banco de dados de caixa de correio, siga um destes procedimentos:

  - No EAC, navegue até **servidores** \> **bancos de dados**. Selecione o banco de dados apropriado, e no painel de detalhes, a cópia passiva removida não está mais listada.

  - No Shell, execute o seguinte comando para verificar a remoção da cópia.
    
        Get-MailboxDatabase <DatabaseName> | Format-List DatabaseCopies
    
    A cópia passiva removida não está mais listada.

