---
title: 'Criar um grupo de disponibilidade do banco de dados: Exchange 2013 Help'
TOCTitle: Criar um grupo de disponibilidade do banco de dados
ms:assetid: d6b98299-e203-488b-af73-50753fe152c8
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Dd351172(v=EXCHG.150)
ms:contentKeyID: 50486757
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Criar um grupo de disponibilidade do banco de dados

 

_**Aplica-se a:**Exchange Server 2013_

_**Tópico modificado em:**2015-04-07_

DAG (grupo de disponibilidade do banco de dados) é um conjunto de até 16 servidores de caixa de correio do Microsoft Exchange Server 2013 que fornece recuperação automática no nível de banco de dados, diante de uma falha no banco de dados, no servidor ou na rede. Quando um servidor de caixa de correio é adicionado a um DAG, funciona com outros servidores para fornecer recuperação automática no nível do banco de dados após falhas neste, no servidor e na rede.

Procurando outras tarefas de gerenciamento relacionadas a DAGs? Consulte [Gerenciando grupos de disponibilidade de banco de dados](managing-database-availability-groups-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: 1 minuto

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Grupos de Disponibilidade do Banco de Dados" no tópico [Permissões de resiliência de site e disponibilidade altas](high-availability-and-site-resilience-permissions-exchange-2013-help.md).

  - Quando criar um DAG com servidores de Caixa de Correio com o Windows Server 2012, você deverá pré-configurar o objeto de rede de cluster antes de adicionar membros ao DAG. Se você estiver criando um DAG sem um ponto de acesso administrativo com os servidores de Caixa de Correio que estão executando o Windows Server 2012 R2, não será necessário incluir uma etapa de pré-teste de um CNO para o DAG. Para obter etapas detalhadas, consulte [Preparar o objeto de nome de cluster de um grupo de disponibilidade do banco de dados](pre-stage-the-cluster-name-object-for-a-database-availability-group-exchange-2013-help.md).

  - Você fornece um nome exclusivo de até 15 caracteres a um DAG ao criá-lo. Além de dar um nome para o DAG, atribua também um ou mais endereços IP (seja IPv4 ou IPv4 e IPv6) ao DAG, a não ser que você esteja criando um DAG do Windows Server 2012 R2 sem um ponto de acesso administrativo e sem atribuir qualquer endereço IP ao DAG. Caso contrário, os endereços IP atribuídos deverão estar em cada sub-rede pretendida para a rede MAPI e disponíveis para uso. Se você especificar um ou mais endereços IPv4 e seu sistema estiver configurado para usar IPv6, a tarefa também tentará atribuir automaticamente ao DAG um ou mais endereços IPv6.

  - Ao criar um DAG, você pode opcionalmente especificar um servidor e um diretório testemunha. Se você especificar um servidor testemunha, recomendamos usar um servidor de Acesso para Cliente que não tenham a função de servidor Caixa de Correio instalada. Isso permite que um administrador do Exchange esteja ciente da disponibilidade do testemunha e assegura que todas as permissões de segurança necessárias para usar o servidor testemunha estejam aplicadas.
    
    As seguintes combinações de opções e comportamentos estão disponíveis:
    
      - É possível especificar apenas um nome para o DAG e deixar os campos **Servidor testemunha** e **Diretório testemunha** vazios. Nesta situação, a tarefa buscará pelo servidor de Acesso para Cliente que não possua a função de servidor Caixa de Correio instalada. Ele criará automaticamente o diretório e o compartilhamento testemunha padrão nesse servidor de Acesso para Cliente e configurará o DAG para usar esse servidor como seu servidor testemunha.
    
      - Você pode especificar um nome para o DAG, o servidor testemunha que deseja utilizar e o diretório que deseja que seja criado e compartilhado no servidor testemunha.
    
      - É possível especificar um nome para o DAG e o servidor testemunha que deseja usar, além de deixar o campo **Diretório testemunha** vazio. Nesta situação, a tarefa criará o diretório testemunha padrão no servidor testemunha especificado.
    
      - É possível especificar um nome para o DAG e deixar o campo **Servidor testemunha** vazio, além de especificar o diretório que você deseja criar e compartilhar no servidor testemunha. Nesta situação, o assistente irá procurar um servidor de Acesso para Cliente que não tenha a função de servidor de Caixa de Correio instalada e irá automaticamente criar o diretório testemunha especificado nesse servidor, compartilhar o diretório e configurar o DAG para usar esse servidor de Acesso para Cliente como seu servidor testemunha.
    

    > [!IMPORTANT]
    > Se o servidor testemunha que você especificar não for um servidor Exchange 2013 ou Exchange 2010, você deve adicionar o grupo de segurança universal de subsistema confiável de Exchange ao grupo Administradores local no servidor testemunha. Essas permissões de segurança são necessárias para garantir que Exchange pode criar um diretório e compartilhar no servidor testemunha, conforme necessário. Se as permissões adequadas não estiverem configuradas, o seguinte erro será retornado:<BR><CODE>Error: An error occurred during discovery of the database availability group topology. Error: An error occurred while attempting a cluster operation. Error: Cluster API "AddClusterNode() (MaxPercentage=12) failed with 0x80070005. Error: Access is denied."</CODE>



  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>..



## O que você deseja fazer?

## Usar o EAC para criar um grupo de disponibilidade de banco de dados

1.  No EAC, vá até **Servidores** \> **Grupos de Disponibilidade de Banco de Dados**.

2.  Clique em ![Ícone Adicionar](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Ícone Adicionar") para criar um DAG.

3.  
    
    Na página **Novo Grupo de Disponibilidade de Banco de Dados**, forneça a seguinte informação para o DAG:
    
      - **Nome do grupo de disponibilidade de banco de dados**   Neste campo, insira um nome válido e exclusivo de até 15 caracteres para o DAG. O nome é equivalente ao nome do computador, e um CNO correspondente será criado em Active Directory com esse nome. Esse nome será o nome do DAG e o nome do cluster subjacente.
    
      - **Servidor testemunha**   Use este campo especificar um servidor testemunha para o DAG. Se você deixar esse campo em branco, o sistema tentará automaticamente selecionar um servidor de Acesso para Cliente no site do Active Directory local que não está instalado em um computador com o servidor de Caixa de Correio a ser usado como servidor testemunha.
        

        > [!TIP]
        > Se você especificar um servidor testemunha, deve usar um nome de host ou nome de domínio totalmente qualificado (FQDN). Não há suporte para o uso de um endereço IP ou de um nome com caractere curinga. Além disso, o servidor testemunha não pode ser membro do DAG.

    
      - **Diretório testemunha**   Use este campo para digitar o caminho para um diretório no servidor testemunha que será usado para armazenar os dados de testemunha. Se o diretório não existir, o sistema o criará para você no servidor testemunha. Se você deixar este campo em branco, o diretório padrão (%SystemDrive%\\DAGFileShareWitnesses\\\<DAG FQDN\>) será criado no servidor testemunha.
    
      - **Endereços IP do grupo de disponibilidade de banco de dados**   Use este campo para atribuir um ou mais endereços IPv4 estáticos ao DAG. Insira um endereço IPv4 e clique em ![Ícone Adicionar](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Ícone Adicionar") para adicioná-lo. Deixe este campo em branco, se você quiser que o DAG use o protocolo DHCP para obter os endereços IPv4 necessários. Como opção, insira 255.255.255.255 para criar um DAG sem um endereço IP ou ponto de acesso administrativo do cluster, algo que se aplica apenas aos DAGs que conterão servidores de Caixa de Correio executando o Windows Server 2012 R2.

4.  Clique em **Salvar** para criar o DAG.

## Usar o Shell para criar um grupo de disponibilidade de banco de dados

Este exemplo cria o DAG chamado DAG1, configurado para usar o servidor de testemunha FILESRV1 e o diretório local C:\\DAG1. DAG1 também é configurado para usar DHCP para os endereços IP do DAG.

    New-DatabaseAvailabilityGroup -Name DAG1 -WitnessServer FILESRV1 -WitnessDirectory C:\DAG1

Este exemplo cria o DAG DAG2. O sistema seleciona automaticamente um servidor de Acesso para Cliente no site local do Active Directory que não contém a função de servidor de Caixa de Correio como o servidor de testemunha de DAG. O DAG2 recebe um endereço IP estático, pois todos os membros do DAG têm a rede MAPI na mesma sub-rede.

    New-DatabaseAvailabilityGroup -Name DAG2 -DatabaseAvailabilityGroupIPAddresses 10.0.0.8

Este exemplo cria o DAG DAG3. O DAG3 está configurado para usar o servidor de testemunha MBX2 e o diretório local C:\\DAG3. DAG3 recebe vários endereços IP estáticos, pois seus membros estão em sub-redes diferentes na rede MAPI.

    New-DatabaseAvailabilityGroup -Name DAG3 -WitnessServer MBX2 -WitnessDirectory C:\DAG3 -DatabaseAvailabilityGroupIPAddresses 10.0.0.8,192.168.0.8

Este exemplo cria o DAG DAG4 configurado para usar DHCP. Além disso, o servidor testemunha será selecionado automaticamente pelo sistema e o diretório testemunha padrão será criado.

    New-DatabaseAvailabilityGroup -Name DAG4

Este exemplo cria o DAG chamado DAG5, que não terá um ponto de acesso administrativo (válido somente para DAGs do Windows Server 2012 R2). Além disso, o MBX4 será usado como o servidor de testemunha do DAG e será criado o diretório de testemunha padrão.

    New-DatabaseAvailabilityGroup -Name DAG5 -DatabaseAvailabilityGroupIPAddresses ([System.Net.IPAddress]::None) -WitnessServer MBX4

## Como saber se funcionou?

Para verificar se você criou com êxito um DAG, faça o seguinte:

  - Na EAC, navegue até **Servidores** \> **Grupos de Disponibilidade de Banco de Dados**. O DAG recém-criado é exibido.

  - No Shell, execute o comando a seguir para verificar se o DAG foi criado e para exibir as informações de propriedade do DAG.
    
        Get-DatabaseAvailabilityGroup <DAGName> | Format-List

## Para obter mais informações

[Grupos de Disponibilidade do Banco de Dados (DAGs)](database-availability-groups-dags-exchange-2013-help.md)

[Configurar as propriedades do grupo de disponibilidade do banco de dados](configure-database-availability-group-properties-exchange-2013-help.md)

[Set-DatabaseAvailabilityGroup](https://technet.microsoft.com/pt-br/library/dd297934\(v=exchg.150\))

[New-DatabaseAvailabilityGroup](https://technet.microsoft.com/pt-br/library/dd351107\(v=exchg.150\))

[New-DatabaseAvailabilityGroupNetwork](https://technet.microsoft.com/pt-br/library/dd335225\(v=exchg.150\))

[Add-DatabaseAvailabilityGroupServer](https://technet.microsoft.com/pt-br/library/dd298049\(v=exchg.150\))

