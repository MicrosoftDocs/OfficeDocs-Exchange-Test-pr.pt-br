---
title: 'Configurar propriedades de grupo de disponibilidade de banco de dados'
TOCTitle: Configurar as propriedades do grupo de disponibilidade do banco de dados
ms:assetid: 50daeac5-a16f-4362-a325-19e0fe25d59d
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Dd297985(v=EXCHG.150)
ms:contentKeyID: 50485576
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configurar as propriedades do grupo de disponibilidade do banco de dados

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2014-06-24_

Você pode usar o EAC ou o Shell para configurar as propriedades de um grupo de disponibilidade de banco de dados (DAG), incluindo a configuração do endereço IP do DAG e o servidor e o diretório testemunhas usados pelo DAG. O Shell permite que você configure as propriedades do DAG que não estão disponíveis no EAC, como informações de servidor testemunha alternativo e de diretório testemunha alternativo, a porta TCP usada para replicação e o modo de coordenação de ativação de data center (DAC).

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: 1 minuto

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Grupos de Disponibilidade do Banco de Dados" no tópico [Permissões de resiliência de site e disponibilidade altas](high-availability-and-site-resilience-permissions-exchange-2013-help.md).

  - Os valores de propriedades de DAG são armazenados no Active Directory e no banco de dados de cluster. No entanto, algumas propriedades são armazenadas somente no banco de dados de cluster. Como resultado, o cluster subjacente do DAG deve estar operando e ter quorum para definir as propriedades de:
    
      - ReplicationPort
    
      - NetworkCompression
    
      - NetworkEncryption
    
      - DiscoverNetworks

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>..



## O que você deseja fazer?

## Usar o EAC para configurar propriedades de grupos de disponibilidade de banco de dados

1.  Na EAC, vá até **Servidores** \> **Grupos de Disponibilidade de Banco de Dados**.

2.  Selecione o DAG que você deseja configurar e clique em ![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").

3.  Use a página **Geral** para exibir o status de associação e operação do DAG e para configurar o servidor testemunha do DAG, o diretório testemunha e a configuração automática de rede:
    
      - **Servidor testemunhas**   O nome de host ou nome de domínio totalmente qualificado (FQDN) do servidor testemunha do DAG. Apesar de essa ser uma propriedade requerida por todos os DAGs, o servidor testemunha é usado quando há um número par de membros do DAG e o modelo de quórum em uso pelo cluster é Maioria dos Nós e Compartilhamentos de Arquivos.
    
      - **Diretório testemunha**   O caminho completo do diretório usado para armazenar o arquivo witness.log no servidor testemunha. Apesar de essa ser uma propriedade exigida por todos os DAGs, o diretório testemunha é usado somente quando o servidor testemunha do DAG está em uso.
    
      - **Servidores operacionais**   Um campo somente leitura que mostra uma lista de membros de DAG e seu status operacional atual.
    
      - **Configurar a rede do grupo de bancos de dados manualmente**   Uma caixa de seleção que você marca quando deseja configurar todas as redes do DAG manualmente. Quando você deixa a caixa de seleção desmarcada, o sistema configura as redes do DAG automaticamente, com base na configuração da interface de rede. Se a caixa de seleção forem desmarcadas, o cmdlets **Set-DatabaseAvailabilityGroupNetwork** e **New-DatabaseAvailabilityGroupNetwork** serão desabilitados para uso administrativo com base no DAG.

4.  Use a página **Endereço IP** para exibir e modificar os endereços IP atribuídos ao DAG:
    
      - Selecione um endereço IP existente e clique em ![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição") para modificá-lo.
    
      - Selecione um endereço IP existente e clique no ícone de menos (excluir), para remover o endereço.
    
      - Insira um endereço IP e clique em ![Ícone Adicionar](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Ícone Adicionar"), para adicioná-lo ao DAG.

5.  Clique em **Salvar** para salvar quaisquer alterações feitas.

## Usar o Shell para configurar propriedades de grupos de disponibilidade de banco de dados

Este exemplo define o diretório testemunha como C:\\DAG1DIR para um DAG chamado DAG1.

```powershell
Set-DatabaseAvailabilityGroup -Identity DAG1 -WitnessDirectory C:\DAG1DIR
```

Este exemplo configura previamente o servidor testemunha alternativo CAS3 e um diretório testemunha alternativo C:\\DAGFileShareWitnesses\\DAG1.contoso.com para o DAG chamado DAG1.

```powershell
Set-DatabaseAvailabilityGroup -Identity DAG1 -AlternateWitnessDirectory 
```

```powershell
C:\DAGFileShareWitnesses\DAG1.contoso.com -AlternateWitnessServer CAS3
```

Este exemplo configura um DAG chamado DAG1 para utilizar Dynamic Host Configuration Protocol (DHCP) a fim de obter um endereço IP.

```powershell
Set-DatabaseAvailabilityGroup -Identity DAG1 -DatabaseAvailabilityGroupIPAddresses 0.0.0.0
```

Este exemplo configura um DAG chamado DAG1 para utilizar o endereço IP estático 10.0.0.8.

```powershell
Set-DatabaseAvailabilityGroup -Identity DAG1 -DatabaseAvailabilityGroupIPAddresses 10.0.0.8
```

Este exemplo configura um DAG com múltiplas sub-redes chamado DAG1 com múltiplos endereços IP estáticos.

```powershell
Set-DatabaseAvailabilityGroup -Identity DAG1 -DatabaseAvailabilityGroupIPAddresses 10.0.0.8,10.0.1.8
```

Este exemplo configura um DAG chamado DAG1 para o modo DAC.

```powershell
Set-DatabaseAvailabilityGroup -Identity DAG1 -DatacenterActivationMode DagOnly
```

Este exemplo configura como 63132 a porta de replicação do DAG chamado DAG1.

```powershell
Set-DatabaseAvailabilityGroup -Identity DAG1 -ReplicationPort 63132
```

> [!NOTE]
> Após alterar a porta de replicação padrão de um DAG, você deverá modificar manualmente as exceções do Firewall do Windows em cada membro do DAG, a fim de permitir a comunicação pela porta especificada.



## Como saber se funcionou?

Para verificar se você configurou com êxito o DAG, faça o seguinte:

  - No Shell, execute o comando a seguir para exibir as configurações do DAG e verificar se o DAG foi configurado com êxito.
    
    ```powershell
    Get-DatabaseAvailabilityGroup <DAGName> | Format-List
    ```

## Para obter mais informações

[Criar um grupo de disponibilidade do banco de dados](create-a-database-availability-group-exchange-2013-help.md)

[Remover um grupo de disponibilidade do banco de dados](remove-a-database-availability-group-exchange-2013-help.md)

[Criar uma rede de grupo de disponibilidade do banco de dados](create-a-database-availability-group-network-exchange-2013-help.md)

[Gerenciar a associação de grupo de disponibilidade do banco de dados](manage-database-availability-group-membership-exchange-2013-help.md)

[Get-DatabaseAvailabilityGroup](https://technet.microsoft.com/pt-br/library/dd351226\(v=exchg.150\))

[Set-DatabaseAvailabilityGroup](https://technet.microsoft.com/pt-br/library/dd297934\(v=exchg.150\))
