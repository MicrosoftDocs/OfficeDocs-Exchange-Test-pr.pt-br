---
title: 'Criar rede de grupo de disponibilidade do banco de dados: Exchange 2013 Help'
TOCTitle: Criar uma rede de grupo de disponibilidade do banco de dados
ms:assetid: 6caec7be-788a-4058-87a7-f31c575b870c
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Dd298051(v=EXCHG.150)
ms:contentKeyID: 50485890
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Criar uma rede de grupo de disponibilidade do banco de dados

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2012-11-02_

Se necessário, você pode criar redes adicionais para uso em um grupo de disponibilidade de banco de dados (DAG). Você pode usar o EAC ou o Shell para criar uma rede do DAG.

Procurando outras tarefas de gerenciamento relacionadas a DAGs? Consulte [Gerenciando grupos de disponibilidade de banco de dados](managing-database-availability-groups-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: 1 minuto

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Grupos de Disponibilidade do Banco de Dados" no tópico [Permissões de resiliência de site e disponibilidade altas](high-availability-and-site-resilience-permissions-exchange-2013-help.md).

  - Você pode criar uma rede do DAG somente quando a configuração de rede automática tiver sido desabilitada para um DAG. Para instruções detalhadas de como desabilitar a configuração de rede automática para um DAG, consulte [Configurar as propriedades do grupo de disponibilidade do banco de dados](configure-database-availability-group-properties-exchange-2013-help.md).

  - Ao criar uma rede do DAG, você deve atribuir sub-redes exclusivas que não estejam em uso por outra rede do DAG. Se você usar sub-redes que estão atribuídas a uma rede do DAG existente, elas serão removidas da rede do DAG e adicionadas a rede do DAG recém-criada.

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>..



## O que você deseja fazer?

## Usar o EAC para criar uma rede de grupo de disponibilidade de banco de dados

1.  Na EAC, vá até **Servidores** \> **Grupos de Disponibilidade de Banco de Dados**.

2.  Selecione o DAG que você deseja configurar e clique em ![Adicionar rede DAG](images/Dd298051.befcdc4e-7f7a-451d-a0a8-608c79f5d186(EXCHG.150).gif "Adicionar rede DAG").

3.      
    Na página **nova rede do grupo de disponibilidade de banco de dados**, forneça as seguintes informações:
    
      - **Nome de rede do grupo de disponibilidade do banco de dados**   Use esse campo para digitar um nome para a rede que seja exclusiva para o DAG.
    
      - **Descrição**   Use esse campo para fornecer uma descrição em texto da rede do DAG.
    
      - **Sub-redes**   Use esse campo para associar uma ou mais sub-redes à rede DAG. Clique em ![Ícone Adicionar](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Ícone Adicionar"), para adicionar uma sub-rede, em ![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição") para editar uma sub-rede e clique no sinal de menos (-) para remover uma sub-rede.

4.  Clique em **Salvar** para criar a rede do DAG.

## Use o Shell para criar uma rede de grupo de disponibilidade de banco de dados

Este exemplo cria a rede ReplicationDagNetwork02 com uma sub-rede de 10.0.0.0 e uma bitmask de 8 em um DAG chamado DAG1. A replicação é habilitada na rede, e uma descrição opcional da rede também está sendo acrescentada.

    New-DatabaseAvailabilityGroupNetwork -DatabaseAvailabilityGroup DAG1 -Name ReplicationDagNetwork02 -Description "Replication network 2" -Subnets 10.0.0.0/8 -ReplicationEnabled:$True

## Como saber se funcionou?

Para verificar se você criou com êxito uma rede do DAG, faça o seguinte:

  - Na EAC, navegue até **Servidores** \> **Grupos de Disponibilidade de Banco de Dados**. Selecione o DAG apropriado, e a rede do DAG recém-criada será exibida no painel de detalhes.

  - No Shell, execute o comando a seguir para exibir as informações de configuração de rede do DAG e verificar se a rede do DAG foi configurada com êxito.
    
        Get-DatabaseAvailabilityGroupNetwork <DAGNetworkName> | Format-List

## Para obter mais informações

[Set-DatabaseAvailabilityGroupNetwork](https://technet.microsoft.com/pt-br/library/dd298008\(v=exchg.150\))

[Get-DatabaseAvailabilityGroupNetwork](https://technet.microsoft.com/pt-br/library/dd297938\(v=exchg.150\))

[New-DatabaseAvailabilityGroupNetwork](https://technet.microsoft.com/pt-br/library/dd335225\(v=exchg.150\))

[Remove-DatabaseAvailabilityGroupNetwork](https://technet.microsoft.com/pt-br/library/dd298131\(v=exchg.150\))

