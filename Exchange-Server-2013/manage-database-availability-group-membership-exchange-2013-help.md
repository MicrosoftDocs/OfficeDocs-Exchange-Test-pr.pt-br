---
title: 'Gerenciar a associação de grupo de disponibilidade do banco de dados'
TOCTitle: Gerenciar a associação de grupo de disponibilidade do banco de dados
ms:assetid: fb2ea15e-96d5-4045-b75b-b0aa5fc60479
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Dd351278(v=EXCHG.150)
ms:contentKeyID: 50487041
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Gerenciar a associação de grupo de disponibilidade do banco de dados

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2014-08-13_

Ao adicionar um servidor a um grupo de disponibilidade do banco de dados (DAG), ele funciona com os demais servidores no DAG para fornecer recuperação automática, a nível de banco de dados, de falhas de banco de dados, de servidor e de rede. Ao se remover um servidor de um DAG, ele não está mais automaticamente protegido contra falhas.

Procurando outras tarefas de gerenciamento relacionadas a DAGs? Consulte [Gerenciando grupos de disponibilidade de banco de dados](managing-database-availability-groups-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: 5 minutos por servidor

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Grupos de Disponibilidade do Banco de Dados" no tópico [Permissões de resiliência de site e disponibilidade altas](high-availability-and-site-resilience-permissions-exchange-2013-help.md).

  - Os DAGs usam as tecnologias do Cluster de Failover do Windows (WFC). Cada servidor de Caixa de Correio membro de um DAG também é um nó no cluster subjacente usado pelo DAG. Assim, em um momento específico, um servidor de Caixa de Correio só pode ser membro de um único DAG. Como os DAGs usam a tecnologia WFC, todos os servidores adicionados a um DAG devem executar o mesmo sistema operacional: O Windows Server 2008 R2 Enterprise ou Datacenter Edition, ou o Standard ou Datacenter Edition do Windows Server 2012 ou o Windows Server 2012 R2.

  - Se você estiver adicionando servidores de Caixa de Correio com o Windows Server 2012, você deverá pré-configurar o objeto de rede de cluster (CNO) antes de adicionar membros ao DAG. Se você estiver adicionando servidores de Caixa de Correio em execução no Windows Server 2012 R2 e seu DAG não tiver um ponto de acesso administrativo, não será necessário incluir uma etapa de pré-teste de um CNO, pois os DAGs sem pontos de acesso administrativo não têm um CNO. Para obter etapas detalhadas, consulte [Preparar o objeto de nome de cluster de um grupo de disponibilidade do banco de dados](pre-stage-the-cluster-name-object-for-a-database-availability-group-exchange-2013-help.md).

  - Para poder adicionar membros a um DAG, você deverá primeiro criar o DAG. Para etapas detalhadas, consulte [Criar um grupo de disponibilidade do banco de dados](create-a-database-availability-group-exchange-2013-help.md).

  - Você deve remover todas as cópias de bancos de dados replicadas do servidor, antes de removê-lo de um DAG.

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>..



## O que você deseja fazer?

## Usar o EAC para gerenciar a associação ao grupo de disponibilidade de banco de dados

1.  No EAC, vá até **Servidores** \> **Grupos de Disponibilidade de Banco de Dados**.

2.  Selecione o DAG que você deseja configurar e clique em ![Gerenciar membros DAG](images/Dd351278.d567ae56-d6cd-4edb-ab67-ad8f7c58f337(EXCHG.150).gif "Gerenciar membros DAG").
    
      - Para adicionar ou um mais servidores de Caixa de Correio ao DAG, clique em ![Ícone Adicionar](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Ícone Adicionar"), selecione os servidores na lista, clique em **Adicionar** e em **OK**.
    
      - Para remover um ou mais servidores de Caixa de Correio do DAG, selecione os servidores e clique no ícone de menos (-).

3.  Clique em **Salvar** para salvar as alterações.

4.  Quando a tarefa tiver sido concluída com êxito, clique em **Fechar**.

## Usar o Shell para gerenciar a associação ao grupo de disponibilidade de banco de dados

Este exemplo adiciona o servidor de Caixa de Correio MBX1 ao DAG DAG1.

```powershell
Add-DatabaseAvailabilityGroupServer -Identity DAG1 -MailboxServer MBX1
```

Este exemplo remove a o servidor de Caixa de Correio MBX1 do DAG DAG1. Antes de executar este comando, verifique se não há nenhum banco de dados replicado no servidor de Caixa de Correio.

```powershell
Remove-DatabaseAvailabilityGroupServer -Identity DAG1 -MailboxServer MBX1
```

Este exemplo remove as configurações do servidor de Caixa de Correio MBX4 do DAG2 DAG. O MBX4 deve permanecer offline por um longo período, por isso suas configurações são removidas de um DAG enquanto ele estiver offline para estabelecer quórum com os membros do DAG online remanescente.

```powershell
Remove-DatabaseAvailabilityGroupServer -Identity DAG2 -MailboxServer MBX4 -ConfigurationOnly
```

## Como saber se funcionou?

Para verificar se você gerenciou com êxito a associação ao DAG, execute um dos seguintes procedimentos:

  - Na EAC, navegue até **Servidores** \> **Grupos de Disponibilidade de Banco de Dados**. A associação ao DAG atual é exibida na coluna **Servidores Membro**.

  - No Shell, execute o comando a seguir para exibir as informações de associação ao DAG.
    
    ```powershell
    Get-DatabaseAvailabilityGroup <DAGName> | Format-List Servers
    ```

## Para obter mais informações

[Add-DatabaseAvailabilityGroupServer](https://technet.microsoft.com/pt-br/library/dd298049\(v=exchg.150\))

[Remove-DatabaseAvailabilityGroupServer](https://technet.microsoft.com/pt-br/library/dd297956\(v=exchg.150\))

