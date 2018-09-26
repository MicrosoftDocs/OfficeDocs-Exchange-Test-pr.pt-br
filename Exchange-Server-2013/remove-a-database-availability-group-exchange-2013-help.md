---
title: 'Remover um grupo de disponibilidade do banco de dados: Exchange 2013 Help'
TOCTitle: Remover um grupo de disponibilidade do banco de dados
ms:assetid: 071296e9-31b0-40f4-9a02-177d97486ebd
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Dd335069(v=EXCHG.150)
ms:contentKeyID: 50484909
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Remover um grupo de disponibilidade do banco de dados

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2012-11-16_

Remover um grupo de disponibilidade de banco de dados (DAG) é uma tarefa fácil e rápida. Você pode usar o EAC ou o Shell para remover um DAG.

Procurando outras tarefas de gerenciamento relacionadas a DAGs? Consulte [Gerenciando grupos de disponibilidade de banco de dados](managing-database-availability-groups-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: 1 minuto

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Grupos de Disponibilidade do Banco de Dados" no tópico [Permissões de resiliência de site e disponibilidade altas](high-availability-and-site-resilience-permissions-exchange-2013-help.md).

  - Antes de ser possível remover um DAG, ele deve estar vazio. Se o DAG que você deseja remover contiver quaisquer servidores de Caixa de Correio, primeiramente é preciso remover os servidores do DAG. Para obter as etapas detalhadas sobre como remover um servidor de Caixa de Correio de um DAG, consulte [Gerenciar a associação de grupo de disponibilidade do banco de dados](manage-database-availability-group-membership-exchange-2013-help.md).

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>..



## O que você deseja fazer?

## Usar o EAC para remover um grupo de disponibilidade de banco de dados

1.  Navegue para **Servidores** \> **Grupos de disponibilidade de banco de dados**.

2.  Selecione o DAG que você deseja remover e clique em **Excluir**![Excluir ícone](images/JJ673559.14f639f6-61e8-4418-bbfb-0db14de9d2f5(EXCHG.150).gif "Excluir ícone").

3.  Clique em **Sim** para confirmar o aviso e remover o DAG.

## Use o Shell para remover um grupo de disponibilidade de banco de dados

Este exemplo remove o DAG DAG1.

```powershell
Remove-DatabaseAvailabilityGroup -Identity DAG1
```

## Como saber se funcionou?

Para verificar se você removeu o DAG com êxito, siga um dos seguintes procedimentos:

  - No EAC, vá para **Servidores** \> **Grupos de Disponibilidade de Banco de Dados** e veja se o DAG ainda é exibido.

  - No Shell, execute o comando a seguir para ver se o DAG ainda existe:
    
    ```powershell
    Get-DatabaseAvailabilityGroup <DAGName>
    ```
    
    Se o DAG tiver sido excluído com êxito, o comando acima produzirá uma mensagem de erro indicando que o objeto não pôde ser encontrado.

