---
title: 'Ativar uma cópia do banco de dados de caixa de correio: Exchange 2013 Help'
TOCTitle: Ativar uma cópia do banco de dados de caixa de correio
ms:assetid: d948269b-c902-4d8d-8c2b-269473359baa
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Ee364750(v=EXCHG.150)
ms:contentKeyID: 50486804
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Ativar uma cópia do banco de dados de caixa de correio

 

_**Aplica-se a:**Exchange Server 2013_

_**Tópico modificado em:**2012-11-01_

Ativando uma cópia do banco de dados de caixa de correio é o processo de designar uma cópia passiva específica como a nova cópia ativa de um banco de dados de caixa de correio. Esse processo é conhecido como uma *alternância de banco de dados*. Uma alternância de banco de dados envolve desmontar o banco de dados ativo atual e montando a cópia do banco de dados no servidor especificado como a nova cópia do banco de dados de caixa de correio ativas. A cópia do banco de dados que se tornará o banco de dados de caixa de correio ativa deve estar íntegro e atual.

Procurando outras tarefas de gerenciamento relacionadas a cópias do banco de dados de caixa de correio? Consulte [Gerenciando cópias de banco de dados de caixa de correio](managing-mailbox-database-copies-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para a conclusão da tarefa: 1 minuto

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte oEntrada "Cópias de banco de dados da caixa de correio" no tópico [Permissões de resiliência de site e disponibilidade altas](high-availability-and-site-resilience-permissions-exchange-2013-help.md).

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>..



## O que você deseja fazer?

## Usar o EAC para mover o banco de dados de caixa de correio ativas

1.  Na EAC, vá até **Servidores** \> **Bancos de dados**.

2.  Selecione o banco de dados cuja cópia que você deseja ativar.

3.  No painel de detalhes, em **Cópias de banco de dados**, clique em **Ativar** sob a cópia do banco de dados que você deseja ativar.

4.  Clique em **Sim** para ativar a cópia do banco de dados.

## Use o Shell para mover o banco de dados de caixa de correio ativas

Este exemplo ativa e monta uma cópia do banco de dados que db4 hospedado no MBX3, como o novo banco de dados de caixa de correio ativas. Esse comando torna DB4 o novo banco de dados de caixa de correio ativas e ele não substituem as definições de discagem de montagem do banco de dados no MBX3.

    Move-ActiveMailboxDatabase DB4 -ActivateOnServer MBX3 -MountDialOverride:None

Este exemplo executa uma alternância de banco de dados DB2 para o servidor de caixa de correio MBX1. Quando o comando for concluído, MBX1 hospeda a cópia ativa do DB2. Porque o parâmetro *MountDialOverride* está definido como `None`, MBX1 monta o banco de dados usando suas próprias configurações de discagem de montagem do banco de dados definido automático.

    Move-ActiveMailboxDatabase DB2 -ActivateOnServer MBX1 -MountDialOverride:None

Este exemplo executa uma alternância de banco de dados DB1 no servidor de caixa de correio MBX3. Quando o comando for concluído, MBX3 hospeda a cópia ativa do DB1. Porque o parâmetro *MountDialOverride* foi especificado com um valor de `Good Availability`, MBX3 monta o banco de dados usando a montagem automática de um banco de dados configuração da *GoodAvailability*de discagem.

    Move-ActiveMailboxDatabase DB1 -ActivateOnServer MBX3 -MountDialOverride:GoodAvailability

Esse exemplo executa uma alternância do banco de dados DB3 para o servidor de Caixa de Correio MBX4. Quando o comando é concluído, MBX4 hospeda a cópia ativa de DB3. Como o parâmetro *MountDialOverride* não é especificado, o MBX4 monta o banco de dados usando uma configuração de discagem automática da montagem de *Lossless*.

    Move-ActiveMailboxDatabase DB3 -ActivateOnServer MBX4

Este exemplo executa uma alternância para o servidor de Caixa de Correio MBX1. Todas as cópias de banco de dados de caixa de correio no MBX1 serão ativadas em um ou mais servidores de Caixa de Correio, com cópias íntegras dos bancos de dados ativos no MBX1.

    Move-ActiveMailboxDatabase -Server MBX1

Este exemplo executa uma alternância de banco de dados DB4 para o servidor de caixa de correio MBX5. Neste exemplo, a cópia do banco de dados no MBX5 tem uma fila de repetição maior que 6. Como resultado, o parâmetro *SkipLagChecks* deve ser especificado para ativar a cópia do banco de dados no MBX5.

    Move-ActiveMailboxDatabase DB4 MBX5 -SkipLagChecks

Este exemplo executa uma alternância de banco de dados DB5 para o servidor de caixa de correio MBX6. Neste exemplo, a cópia do banco de dados no MBX6 tem um *ContentIndexState* de Failed. Como resultado, o parâmetro *SkipClientExperienceChecks* deve ser especificado para ativar a cópia do banco de dados no MBX6.

    Move-ActiveMailboxDatabase DB5 MBX6 -SkipClientExperienceChecks

## Como saber se funcionou?

Para verificar se você ativou com êxito uma cópia do banco de dados de caixa de correio, siga um destes procedimentos:

  - No EAC, navegue até **Servidores** \> **Bancos de dados**. Selecione o banco de dados apropriado e, no painel Detalhes, clique em **Exibir detalhes**, para exibir as propriedades de cópia do banco de dados.

  - No Shell, execute este comando para mostrar informações de status para uma cópia do banco de dados.
    
        Get-MailboxDatabaseCopyStatus <DatabaseCopyName> | Format-List

## Para saber mais

[Cópias de banco de dados de caixa de correio](mailbox-database-copies-exchange-2013-help.md)

[Configurar propriedades de cópia de banco de dados de caixa de correio](configure-mailbox-database-copy-properties-exchange-2013-help.md)

