---
title: 'Usar uma VM do Microsoft Azure como um servidor testemunha do DAG'
TOCTitle: Usando uma VM do Microsoft Azure como um servidor de testemunha do DAG
ms:assetid: 03d1e215-518b-4b48-bfcd-8d187ff8f5ef
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Dn903504(v=EXCHG.150)
ms:contentKeyID: 63892251
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Usando uma VM do Microsoft Azure como um servidor de testemunha do DAG

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2016-12-09_

Exchange Server 2013 permite configurar seus bancos de dados de caixa de correio em um grupo de disponibilidade do banco de dados (DAG) para que o failover automático do datacenter. Essa configuração requer três locais físicos separados: dois datacenters para servidores correio e um terceiro local para colocar o servidor testemunha do DAG. Organizações com apenas dois locais físicos também podem tirar proveito de failover automático do datacenter por meio de uma máquina virtual de servidor de arquivo de Microsoft Azure para agir como servidor de testemunha do DAG.

Este artigo enfoca o posicionamento da testemunha do DAG no Microsoft Azure e pressupõe que você está familiarizado com os conceitos de resiliência do site e já tiver uma infraestrutura de DAG totalmente funcional abrangência dois datacenters. Se você ainda não tiver configurada sua infra-estrutura de DAG, recomendamos que você primeiro examine os seguintes artigos:

[Alta disponibilidade e resiliência de site](high-availability-and-site-resilience-exchange-2013-help.md)

[Grupos de Disponibilidade do Banco de Dados (DAGs)](database-availability-groups-dags-exchange-2013-help.md)

[Planejamento de alta disponibilidade e de resiliência do site](planning-for-high-availability-and-site-resilience-exchange-2013-help.md)

## Alterações no Microsoft Azure

Essa configuração requer uma VPN multi-site. Sempre foi possível conectar a rede da sua organização ao Microsoft Azure usando uma conexão VPN de site a site. No entanto, no passado, Azure suportada apenas uma VPN to-site única. Como a configuração de um DAG e seu testemunha em três datacenters necessária vários VPNs de site a site, o posicionamento da testemunha do DAG em uma VM do Windows Azure não era inicialmente possível.

Em junho de 2014, o Microsoft Azure introduziu suporte a VPN multi-site, que é habilitado para as organizações a se conectar vários centros de dados para a mesma rede virtual do Azure. Essa alteração também o tornou possíveis para organizações com dois datacenters que utilizam o Microsoft Azure como um local de terceiro para colocar seus servidores de testemunha do DAG. Para saber mais sobre o recurso VPN multi-site no Windows Azure, consulte [Configure uma VPN multi-Site](http://go.microsoft.com/fwlink/?linkid=522621).


> [!NOTE]
> Essa configuração utiliza uma VPN de vários local e máquinas virtuais do Azure para implantar o servidor testemunha e não usa a testemunha de nuvem do Windows Azure.



## Testemunha de servidor de arquivos do Microsoft Azure

O diagrama a seguir é uma visão geral do uso de um servidor de arquivos do Microsoft Azure VM como uma testemunha do DAG. Você precisa de uma rede virtual do Azure, uma VPN multi-site que conecta os data centers para sua rede virtual do Azure e um controlador de domínio e um servidor de arquivos implantados em máquinas virtuais do Azure.


> [!NOTE]
> É tecnicamente possível usar uma única VM do Windows Azure para essa finalidade e colocar o compartilhamento de arquivos testemunha no controlador de domínio. No entanto, isso resultará em uma desnecessária elevação de privilégios. Portanto, não é uma configuração recomendada.



**Servidor de testemunha do DAG no Microsoft Azure**

![Exchange DAG testemunha sobre a visão geral do Azure](images/Dn903504.7cbda882-bbae-4be7-b0ea-60947b8aa4ef(EXCHG.150).png "Exchange DAG testemunha sobre a visão geral do Azure")

A primeira coisa que você precisa fazer para usar uma VM do Microsoft Azure para seu testemunha do DAG é obter uma assinatura. Consulte [como comprar o Azure](http://go.microsoft.com/fwlink/?linkid=398989) para a melhor maneira de adquirir uma assinatura do Windows Azure.

Depois de ter sua assinatura do Windows Azure, você precisa fazer o seguinte na ordem:

1.  Preparar a rede virtual do Microsoft Azure

2.  Configurar uma VPN de vários local

3.  Configurar máquinas virtuais

4.  Configurar a testemunha do DAG


> [!NOTE]
> Uma parte significativa das diretrizes deste artigo envolve a configuração de Microsoft Azure. Portanto, os links para documentação do Azure é usada sempre que aplicável.



## Pré-requisitos

  - Dois datacenters capazes de suportar uma implantação de resiliência Exchange site e disponibilidade alta. Consulte [Planejamento de alta disponibilidade e de resiliência do site](planning-for-high-availability-and-site-resilience-exchange-2013-help.md) para obter mais informações

  - Um endereço IP público que não é protegido por NAT para os gateways VPN em cada site

  - Um dispositivo VPN em cada site que seja compatível com o Microsoft Azure. Consulte [Sobre dispositivos VPN para a rede Virtual](http://go.microsoft.com/fwlink/?linkid=522619) para obter mais informações sobre dispositivos compatíveis

  - Familiaridade com os conceitos de DAG e gerenciamento

  - Familiaridade com o Windows PowerShell

## Fase 1: Preparar a rede virtual do Microsoft Azure

Configurando a rede Microsoft Azure é a parte mais importante do processo de implantação. Ao final dessa fase, você terá uma rede virtual do Azure totalmente funcional que está conectada ao seus dois datacenters via VPN multi-site.

## Registre os servidores DNS

Como essa configuração requer a resolução de nomes entre os servidores locais e máquinas virtuais do Windows Azure, você precisará configurar o Azure para usar seus próprios servidores DNS. [Resolução de nomes (DNS)](http://msdn.microsoft.com/en-us/library/azure/jj156088.aspx) tópico fornece uma visão geral de resolução de nomes no Windows Azure.

Faça o seguinte procedimento para registrar seus servidores DNS:

1.  No portal do Azure, vá para **redes** e clique em **nova**.

2.  Clique em **Serviços de rede** \> **rede VIRTUAL** \> **registrar o servidor DNS**.

3.  Digite o nome e o endereço IP do seu servidor DNS. O nome especificado aqui é um nome lógico usado no portal de gerenciamento e não deve corresponder ao nome real do seu servidor DNS.

4.  Repita as etapas 1 a 3 para quaisquer outros servidores DNS que você deseja adicionar.
    

    > [!NOTE]
    > Os servidores DNS que você registre não são usados em rodízio. Azure VMs usarão o primeiro servidor DNS listado e usarão apenas quaisquer servidores adicionais se primeiro não estiver disponível.



5.  Repita as etapas 1 a 3 para adicionar o endereço IP que você usará para o controlador de domínio que você implantará no Microsoft Azure.

## Local de criar objetos de rede (local) no Windows Azure

Em seguida, faça o seguinte para criar objetos de rede lógica que representam os data centers in Microsoft Azure:

1.  No portal do Azure, vá para **redes** e, em seguida, clique em **novo**.

2.  Clique em **Serviços de rede** \> **rede VIRTUAL** \> **Adicionar rede LOCAL**.

3.  Digite o nome de seu site de datacenter primeiro e o endereço IP do dispositivo VPN nesse site. Esse endereço IP deve ser um endereço IP público estático que não está atrás do NAT.

4.  Na próxima tela, especifique as subredes de IP para o seu primeiro site.

5.  Repita as etapas 1through 4 para o segundo site.

## Criar a rede virtual do Azure

Agora, execute o seguinte procedimento para criar uma rede virtual do Azure que será usada pelas VMs:

1.  No portal do Azure, vá para **redes** e, em seguida, clique em **novo**.

2.  Clique em **Serviços de rede** \> **rede VIRTUAL** \> **Criar personalizado**.

3.  Na página **Detalhes de rede Virtual**, especifique um nome para a rede virtual e selecione uma localização geográfica para a rede.

4.  Na página **servidores DNS e conectividade VPN**, verifique se que os servidores DNS que você registrou anteriormente estão listados como os servidores DNS.

5.  Marque a opção **Configure uma VPN site a site** em **Conectividade TO-SITE**.
    

    > [!IMPORTANT]
    > Não marque <STRONG>Uso ExpressRoute</STRONG> porque isso impedirá que as alterações de configuração necessárias necessárias para configurar uma VPN multi-site.



6.  Em **Locais de rede**, selecione uma das duas redes locais que você configurou.

7.  Na página de **Espaços de endereço de rede Virtual**, especifique o intervalo de endereços IP que você usará para sua rede virtual do Azure.

## Ponto de verificação: Revisar a configuração de rede

Neste ponto, quando você vai para **redes**, você deverá ver a rede virtual que você configurou em **Redes virtuais,** sites em **Redes locais** e os servidores DNS registrados em **Servidores DNS** do seu local.

## Fase 2: Configurar uma VPN de vários local

A próxima etapa é estabelecer os gateways VPN aos seus sites do local. Para fazer isso, você precisa:

1.  Estabelece um gateway VPN para um dos seus sites usando o portal do Azure.

2.  Exporte as definições de configuração de rede virtual.

3.  Modificar o arquivo de configuração para multi-site VPN.

4.  Importe a configuração de rede Azure atualizado.

5.  Registre o endereço IP do gateway do Azure e chaves pré compartilhadas.

6.  Configure dispositivos VPN local.

Para mais informações sobre como configurar uma VPN de vários local, consulte [Configure uma VPN multi-Site](http://go.microsoft.com/fwlink/?linkid=522621).

## Estabelecer um gateway VPN para seu primeiro site

Ao criar seu gateway virtual, observe que você especificou já que ele será conectado ao seu primeiro site local. Quando você vai para o painel de rede virtual, você verá que o gateway não foi criado.

Para estabelecer o gateway VPN no lado do Azure, siga as instruções na seção [Iniciar do gateway de rede virtual](http://msdn.microsoft.com/en-us/library/azure/jj156210.aspx#bkmk_startgateway) da [Configure um Gateway de rede Virtual no Portal de gerenciamento](http://msdn.microsoft.com/en-us/library/azure/jj156210.aspx).


> [!IMPORTANT]
> Somente execute as etapas na seção "Iniciar o gateway de rede virtual" do artigo e não continue nas seções subsequentes.



## Exportar definições de configuração de rede virtual

O portal de gerenciamento do Windows Azure não atualmente permitem que você configure uma VPN multi-site. Para essa configuração, você precisa exportar as definições de configuração de rede virtual para um arquivo XML e, em seguida, modificar esse arquivo. Siga as instruções em[Exportar configurações de rede Virtual para um arquivo de configuração de rede](http://msdn.microsoft.com/en-us/library/azure/dn133804.aspx) para exportar as configurações.

## Modificar as definições de configuração de rede para vários local VPN

Abra o arquivo exportado em qualquer editor de XML. As conexões de gateway aos seus sites locais estão listadas na seção "ConnectionsToLocalNetwork". No arquivo XML para localizar a seção de pesquisa para esse termo. Esta seção no arquivo de configuração será ser semelhante ao seguinte (supondo que o nome do site que você criou para seu site local é "Site uma").

```powershell
<ConnectionsToLocalNetwork>

    <LocalNetworkSiteRef name="Site A">

        <Connection type="IPsec" />

</LocalNetworkSiteRef>
```

Para configurar seu segundo site, adicione outra seção "LocalNetworkSiteRef" sob a seção "ConnectionsToLocalNetwork". A seção no arquivo de configuração atualizado será parecer com o seguinte (supondo que o nome do site para o seu site local em segundo lugar é "Site B").

```powershell
<ConnectionsToLocalNetwork>

    <LocalNetworkSiteRef name="Site A">

        <Connection type="IPsec" />

    <LocalNetworkSiteRef name="Site B">

        <Connection type="IPsec" />

</LocalNetworkSiteRef>
```

Salve o arquivo de definições de configuração atualizados.

## Importar definições de configuração de rede virtual

A segunda referência de site que você tenha adicionado ao arquivo de configuração irá disparar Microsoft Azure para criar um novo túnel. Importe o arquivo atualizado, usando as instruções no [Importar um arquivo de configuração de rede](http://msdn.microsoft.com/en-us/library/azure/jj156213.aspx). Depois de concluir a importação, o painel de rede virtual mostrará as conexões de gateway com ambos dos sites do locais.

## Registre o endereço IP do gateway do Azure e chaves pré-compartilhadas

Depois que as novas definições de configuração de rede são importadas, o painel de rede virtual exibirá o endereço IP do gateway do Azure. Este é o endereço IP que os dispositivos VPN em ambos os sites se conectará. Registre esse endereço IP para referência.

Você também precisará obter as chaves IKE do IPsec pré compartilhadas para cada encapsulamento que foi criado. Você usará essas chaves, juntamente com o endereço IP do gateway do Azure para configurar seus dispositivos VPN local.

Você precisa usar o PowerShell para obter as chaves pré compartilhadas. Se você não estiver familiarizado com o uso do PowerShell para gerenciar o Windows Azure, consulte [Azure PowerShell](http://msdn.microsoft.com/en-us/library/azure/jj156055.aspx).

Use o cmdlet [Get-AzureVNetGatewayKey](http://msdn.microsoft.com/en-us/library/azure/dn495198.aspx) para extrair as chaves pré compartilhadas. Execute esse cmdlet uma vez para cada túnel. O exemplo a seguir mostra os comandos que você precisará executar para extrair as chaves para encapsulamento entre a rede virtual "Azure Site" e sites de "Site uma" e "Site B." Neste exemplo, as saídas são salvas em arquivos separados. Como alternativa, você pode canalizar essas chaves outros cmdlets do PowerShell ou usá-los em um script.

```powershell
Get-AzureVNETGatewayKey -VNetName "Azure Site" -LocalNetworkSiteName "Site A" > C:\Keys\KeysForTunnelToSiteA.txt 
```
    
```powershell
Get-AzureVNETGatewayKey -VNetName "Azure Site" -LocalNetworkSiteName "Site B" > C:\Keys\KeysForTunnelToSiteB.txt
```

## Configurar dispositivos VPN local

Microsoft Azure fornece os scripts de configuração de dispositivo VPN para os dispositivos VPN com suporte. Clique no link **Baixar Script de dispositivo VPN** no painel de rede virtual para o script apropriado para seus dispositivos VPN.

O script que você baixe terão a definição de configuração para o primeiro site configurado quando você configurar a rede virtual e pode ser usado como está para configurar o dispositivo VPN para esse site. Por exemplo, se você especificou Site A como da **Rede LOCAL** quando você criou a sua rede virtual, o script de dispositivo VPN pode ser usado para Site A. No entanto, você precisará modificá-lo para configurar o dispositivo VPN para o local B. Especificamente, você precisa atualizar a chave pré compartilhada para coincidir com a chave para o segundo site.

Por exemplo, se você estiver usando um dispositivo de roteamento e acesso remoto (RRAS) VPN para seus sites, você precisará:

1.  Abra o script de configuração em qualquer editor de texto.

2.  Localize a seção `#Add S2S VPN interface` .

3.  Encontre o comando **Add-VpnS2SInterface** nesta seção. Verifique se o valor do parâmetro *SharedSecret* corresponde a chave pré compartilhada para o site do qual você está configurando o dispositivo VPN.

Outros dispositivos podem exigir verificações adicionais. Por exemplo, os scripts de configuração para dispositivos Cisco definir regras ACL utilizando-se os intervalos de endereços IP locais. Você precisará Revise e verifique se todas as referências para o site local em que o script de configuração antes de você usá-lo. Consulte os tópicos a seguir para obter mais informações:

[Modelos de roteamento e acesso remoto (RRAS)](http://msdn.microsoft.com/en-us/library/azure/dn133801.aspx)

[Modelos de ASR Cisco](http://msdn.microsoft.com/en-us/library/azure/dn133802.aspx)

[Modelos de Cisco ISR](http://msdn.microsoft.com/en-us/library/azure/dn133800.aspx)

[Juniper SRX modelos](http://msdn.microsoft.com/en-us/library/azure/dn133794.aspx)

[Modelos de Juniper J-series](http://msdn.microsoft.com/en-us/library/azure/dn133799.aspx)

[Modelos de Juniper ISG](http://msdn.microsoft.com/en-us/library/azure/dn133797.aspx)

[Juniper SSG modelos](http://msdn.microsoft.com/en-us/library/azure/dn133796.aspx)

## Ponto de verificação: Revise o status VPN

Neste ponto, ambos os sites estiverem conectados a sua rede virtual do Azure por meio de gateways VPN. É possível validar o status da VPN multi-site executando o seguinte comando no PowerShell.

```powershell
Get-AzureVnetConnection -VNetName "Azure Site" | Format-Table LocalNetworkSiteName, ConnectivityState
```

Se ambos os encapsulamento estiverem em execução, a saída deste comando irá parecer com o seguinte.

```powershell
LocalNetworkSiteName    ConnectivityState

--------------------    -----------------

Site A                  Connected

Site B                  Connected
```

Você também pode verificar a conectividade exibindo o painel de rede virtual no portal de gerenciamento do Windows Azure. A coluna **STATUS** para ambos os sites serão exibidas como **conectado**.


> [!NOTE]
> Pode levar vários minutos após a conexão for estabelecida com êxito para que a alteração de status apareça no portal de gerenciamento do Windows Azure.



## Fase 3: Configurar máquinas virtuais

Você precisa criar um mínimo de duas máquinas virtuais in Microsoft Azure para esta implantação: um controlador de domínio e um servidor de arquivos que servirá como testemunha do DAG.

1.  Crie máquinas virtuais para seu controlador de domínio e o seu servidor de arquivos usando as instruções de [criar uma máquina Virtual executando Windows](http://azure.microsoft.com/en-us/documentation/articles/virtual-machines-windows-tutorial/). Certifique-se de que você selecione a rede virtual que você criou **para/AFINIDADE de região de rede de grupo/virtuais** ao especificar as configurações de suas máquinas virtuais.

2.  Especifica endereços IP preferenciais para o controlador de domínio e o servidor de arquivos usando o Azure PowerShell. Quando você especificar um endereço IP preferencial para uma VM, ele precisa ser atualizado, que requer a reinicialização a VM. O exemplo a seguir define os endereços IP para FSW do Windows Azure e o Azure-DC como 10.0.0.10 e 10.0.0.11 respectivamente.
    
    ```powershell
    Get-AzureVM Azure-DC | Set-AzureStaticVNetIP -IPAddress 10.0.0.10 | Update-AzureVM
    ```
        
    ```powershell
    Get-AzureVM Azure-FSW | Set-AzureStaticVNetIP -IPAddress 10.0.0.11 | Update-AzureVM
    ```
    

    > [!NOTE]
    > Uma VM com um endereço IP preferencial tentará usar esse endereço. No entanto, se esse endereço tiver sido atribuído a uma VM diferente, a VM com a configuração de endereço IP preferencial não será iniciado. Para evitar essa situação, certifique-se de que o endereço IP usado não for atribuído a outra VM. Consulte <A href="http://msdn.microsoft.com/library/azure/dn630228.aspx">Configurar um endereço de IP estático interno de uma VM</A> para obter mais informações.



3.  Provisione o controlador de domínio VM no Azure usando os padrões usados por sua organização.

4.  Prepare o servidor de arquivos com os pré-requisitos para uma testemunha do DAG do Exchange:
    
    1.  Adicione a função de servidor de arquivos usando o Assistente de recursos e adicionar funções ou o cmdlet [Add-WindowsFeature](http://technet.microsoft.com/en-us/library/ee662309.aspx) .
    
    2.  Adicione o grupo de segurança universal de subsistemas confiáveis do Exchange ao grupo Administradores Local.

## Ponto de verificação: Revisar status da máquina virtual

Neste ponto, suas máquinas virtuais deve estar em execução e deve ser capazes de se comunicar com os servidores nos dois datacenters seu local:

  - Verifique se que seu controlador de domínio no Azure estiver replicando com os controladores de domínio local.

  - Verifique se você pode acessar o servidor de arquivo no Azure pelo nome e estabelecer uma conexão SMB dos seus servidores Exchange.

  - Verifique se que você pode acessar seus servidores Exchange pelo nome do servidor de arquivos no Azure.

## Fase 4: Configurar a testemunha do DAG

Finalmente, você precisará configurar seu DAG para usar o novo servidor de testemunha. Por padrão, o Exchange usa o C:\\DAGFileShareWitnesses como o caminho de testemunha de compartilhamento de arquivo no seu servidor testemunha. Se você estiver usando um caminho de arquivo XML personalizado, você deverá atualizar também o diretório testemunha para o compartilhamento específico.

1.  Conecte ao Shell de Gerenciamento do Exchange.

2.  Execute o seguinte comando para configurar o servidor de testemunha para suas DAGs.
    
    ```powershell
    Set-DatabaseAvailabilityGroup -Identity DAG1 -WitnessServer Azure-FSW
    ```

Consulte os tópicos a seguir para obter mais informações:

[Configurar propriedades do grupo de disponibilidade do banco de dados](configure-database-availability-group-properties-exchange-2013-help.md)

[Set-DatabaseAvailabilityGroup](http://technet.microsoft.com/en-us/library/dd297934\(v=exchg.150\).aspx)

## Ponto de verificação: Validar a testemunha de compartilhamento de arquivo do DAG

Neste ponto, você configurou o DAG para usar o servidor de arquivos no Azure como seu testemunha do DAG. Faça o seguinte para validar sua configuração:

1.  Valide a configuração do DAG executando o seguinte comando.
    
    ```powershell
    Get-DatabaseAvailabilityGroup -Identity DAG1 -Status | Format-List Name, WitnessServer, WitnessDirectory, WitnessShareInUse
    ```
    
    Verifique se o parâmetro *WitnessServer* é definido como o servidor de arquivos no Azure, o parâmetro *WitnessDirectory* é definido para o caminho correto, e o parâmetro *WitnessShareInUse* mostra **Primary**.

2.  Se o DAG tiver um número par de nós, a testemunha de compartilhamento de arquivo será configurada. Valide a testemunha de compartilhamento de arquivo a definição nas propriedades de cluster executando o seguinte comando. O valor do parâmetro *SharePath* deve apontar para o servidor de arquivos e exibir o caminho correto.
    
    ```powershell
    Get-ClusterResource -Cluster MBX1 | Get-ClusterParameter | Format-List
    ```

3.  Em seguida, verifique o status do recurso "Testemunha de compartilhamento de arquivo" cluster executando o seguinte comando. O *State* do recurso cluster deve exibir **Online**.
    
    ```powershell
    Get-ClusterResource -Cluster MBX1
    ```

4.  Por fim, verifique se o compartilhamento é criado com êxito no servidor de arquivos examinando a pasta no Gerenciador de arquivos e os compartilhamentos no Gerenciador de servidores.

## Consulte também


[Planejamento de alta disponibilidade e de resiliência do site](planning-for-high-availability-and-site-resilience-exchange-2013-help.md)  
[Switchovers e Failovers](switchovers-and-failovers-exchange-2013-help.md)  
[Gerenciando grupos de disponibilidade de banco de dados](managing-database-availability-groups-exchange-2013-help.md)

