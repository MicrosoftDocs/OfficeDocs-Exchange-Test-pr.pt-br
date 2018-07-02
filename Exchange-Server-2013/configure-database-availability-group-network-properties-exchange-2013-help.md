---
title: 'Configurar propriedades de rede do grupo de disponibilidade de banco de dados: Exchange 2013 Help'
TOCTitle: Configurar propriedades de rede do grupo de disponibilidade de banco de dados
ms:assetid: 41197639-988f-476c-9788-51d5191a7dce
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Dd297927(v=EXCHG.150)
ms:contentKeyID: 50485435
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configurar propriedades de rede do grupo de disponibilidade de banco de dados

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2012-10-31_

Cada rede DAG (grupo de disponibilidade de banco de dados) possui diversas propriedades que podem ser configuradas, incluindo o nome da rede DAG, um campo de descrição para a rede DAG, uma lista de sub-redes que são utilizadas pela rede DAG e se a rede DAG está habilitada ou não para replicação.

Procurando outras tarefas de gerenciamento relacionadas a DAGs? Consulte [Gerenciando grupos de disponibilidade de banco de dados](managing-database-availability-groups-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: 1 minuto

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Grupos de Disponibilidade do Banco de Dados" no tópico [Permissões de resiliência de site e disponibilidade altas](high-availability-and-site-resilience-permissions-exchange-2013-help.md).

  - Você pode configurar uma rede do DAG somente quando a configuração de rede automática tiver sido desabilitada para um DAG. Para instruções detalhadas sobre como desabilitar a configuração de rede automática para um DAG, consulte [Configurar as propriedades do grupo de disponibilidade do banco de dados](configure-database-availability-group-properties-exchange-2013-help.md).

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>..



## O que você deseja fazer?

## Usar o EAC para configurar as propriedades de redes de grupos de disponibilidade de banco de dados

1.  No EAC, vá até **Servidores** \> **Grupos de Disponibilidade de Banco de Dados**.

2.  Selecione o DAG que deseja configurar e, no painel Detalhes, na rede do DAG que deseja configurar, escolha:
    
      - **Desabilitar Replicação** ou **Habilitar Replicação**   Define as configurações de replicação para a rede do DAG.
    
      - **Remover**   Remove uma rede de DAG. Para remover uma rede do DAG, você deverá remover primeiro todas as sub-redes associadas da rede do DAG.
    
      - **Exibir detalhes**   Configura as propriedades de rede do DAG, como nome, descrição e sub-redes associadas para a rede de DAG. Também é possível exibir as interfaces de rede associadas a essas sub-redes e habilitar ou desabilitar a replicação para a rede de DAG.

## Usar o Shell para configurar propriedades de redes de grupos de disponibilidade de banco de dados

Este exemplo adiciona uma sub-rede de 10.0.0.0 e uma máscara de sub-rede de 255.0.0.0 à rede de DAG MapiDagNetwork no DAG DAG1.

    Set-DatabaseAvailabilityGroupNetwork -Subnets 10.0.0.0/8 -Identity DAG1\MapiDagNetwork

## Como saber se funcionou?

Para verificar se você configurou com êxito a rede do DAG, faça o seguinte:

  - No Shell, execute o comando a seguir para exibir as definições de configuração de rede do DAG e verificar se a rede do DAG foi configurada com êxito.
    
        Get-DatabaseAvailabilityGroupNetwork <DAGNetworkName> | Format-List

## Para obter mais informações

[Set-DatabaseAvailabilityGroupNetwork](https://technet.microsoft.com/pt-br/library/dd298008\(v=exchg.150\))

[Get-DatabaseAvailabilityGroupNetwork](https://technet.microsoft.com/pt-br/library/dd297938\(v=exchg.150\))

[New-DatabaseAvailabilityGroupNetwork](https://technet.microsoft.com/pt-br/library/dd335225\(v=exchg.150\))

[Remove-DatabaseAvailabilityGroupNetwork](https://technet.microsoft.com/pt-br/library/dd298131\(v=exchg.150\))

