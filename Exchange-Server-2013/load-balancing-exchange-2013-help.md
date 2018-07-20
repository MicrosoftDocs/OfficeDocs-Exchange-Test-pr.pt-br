---
title: 'Balanceamento de carga: Exchange 2013 Help'
TOCTitle: Balanceamento de carga
ms:assetid: f572c193-6f3a-400e-9085-a9d3e5e18c59
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/JJ898588(v=EXCHG.150)
ms:contentKeyID: 51407938
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Balanceamento de carga

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2016-12-09_

O balanceamento de carga é uma maneira de gerenciar quais servidores recebem tráfego. O balanceamento de carga ajuda a distribuir as conexões de entrada do cliente em vários pontos finais (os servidores de Acesso para Cliente, por exemplo) para garantir que todos os pontos finais fiquem com uma parte proporcional da carga. O balanceamento de carga também pode proporcionar redundância de failover em caso de falha de um ou mais pontos finais. Usando o balanceamento de carga com o Exchange Server 2013, você garante que os usuários continuem a receber o serviço do Exchange em caso de falha do computador. O balanceamento de carga também possibilita que sua implantação lide com mais tráfego do que um servidor pode processar, e oferece um único nome de host para seus clientes.

O balanceamento de carga tem duas finalidades principais. Reduz o impacto da falha de um único servidor de Acesso para Cliente em um de seus sites do Active Directory. Além disso, o balanceamento de carga garante que a carga em cada um dos servidores de Acesso para Cliente seja distribuída igualmente.

O Exchange 2013 também inclui as seguintes soluções para autenticação e redundância de failover:

  - **Alta disponibilidade** O Exchange 2013 usa grupos de disponibilidade de banco de dados (DAGs) para manter várias cópias de suas caixas de correio em diferentes servidores sincronizados. Dessa forma, se um banco de dados de caixa de correio falhar em um servidor, os usuários podem se conectar a uma cópia sincronizada do banco de dados em outros servidor.

  - **Resiliência de site** Você pode implantar dois sites do Active Directory em locais geográficos diferentes, manter os dados de caixa de correio sincronizados entre os dois locais e fazer com que um site assuma toda a carga do outro em caso de falha.

  - **Movimentações de caixas de correio online** Em uma movimentação de caixa de correio online, os usuários podem acessar suas contas de email durante a mudança. Os usuários ficam sem acesso a suas caixas de correio apenas por um breve tempo no final do processo, quando é feita a sincronização final. Você pode realizar movimentações de caixa de correio online entre florestas ou na mesma floresta.

  - **Redundância de sombra**   A redundância de sombra protege a disponibilidade e a capacidade de recuperação das mensagens enquanto estão em trânsito. Com a redundância de sombra, a exclusão de uma mensagem do banco de dados de transporte é atrasada até que o servidor de transporte confirme que todos os próximos saltos da mensagem tenham sido concluídos. Se qualquer um dos próximos saltos falhar antes de relatar sucesso na entrega, a mensagem será reenviada para entrega para o próximo salto que não foi concluído.

## Alterações de arquitetura no balanceamento de carga do Exchange Server 2013

No Exchange Server 2010, as conexões com clientes e o processamento eram feitos pela função do servidor de Acesso para Cliente. Isso requeria que conexões externas e internas do Outlook, além de conexões com dispositivos móveis e de terceiros, fossem balanceadas em toda a matriz dos servidores de Acesso para Cliente em uma implantação para obter tolerância de falha e utilização eficaz dos servidores. Muitos protocolos de Acesso para Cliente do Exchange 2010 requeriam afinidade, um relacionamento entre o cliente e um servidor de Acesso para Cliente específico. Especificamente, o Outlook Web App, o Painel de Controle do Exchange, os serviços Web do Exchange, o Outlook em Qualquer Lugar, conexões TCP/IP MAPI do Outlook, o Exchange ActiveSync, o serviço de Catálogo de Endereços do Exchange e o PowerShell Remoto exigiam ou se beneficiavam da afinidade entre o cliente e o servidor de Acesso para Cliente. As opções de balanceamento de carga do Exchange 2010 incluíam o seguinte:

  - Balanceamento de Carga de Rede do Windows com afinidade de IP de origem

  - Balanceamento de carga de hardware

Devido às diferentes necessidades dos protocolos do cliente no Exchange 2010, é recomendável usar uma solução de balanceamento de carga de camada 7. Camada 7, também conhecido como nível de aplicativo balanceamento de carga, permitida a solução para usar regras complexas para determinar como balancear a cada solicitação entrem no sistema, visto que toda a conversação entre cliente e servidor estaria disponível para a lógica de Balanceador de carga de balanceamento de carga. Essas regras complexas certificar-se de que todas as solicitações de um cliente específico saiu para o mesmo ponto de extremidade de servidor de acesso para cliente. Em Exchange 2010, se todas as solicitações de um cliente específico não foram enviado ao mesmo ponto de extremidade para protocolos que exigiam afinidade, a experiência do usuário seria ser afetada negativamente. Para obter mais informações sobre opções de balanceamento de carga de Exchange 2010, consulte [balanceamento de carga de Understanding no Exchange 2010](https://go.microsoft.com/fwlink/p/?linkid=196447).

No Exchange Server 2013, há dois tipos primários de servidor: o servidor de Acesso para Cliente e o servidor de Caixa de Correio. Os servidores de Acesso para Cliente do Exchange 2013 funcionam como servidores proxy leves e sem estado, o que possibilita que os clientes se conectem a servidores de Caixa de Correio do Exchange 2013. Os servidores de Acesso para Cliente do Exchange 2013 oferecem namespace e autenticação unificados. Além disso, os servidores de Acesso para Cliente do Exchange 2013:

  - São compatíveis com lógica de proxy e redirecionamento para protocolos de cliente.

  - São compatíveis com o uso de balanceamento de carga de Camada 4.

Com a afinidade de sessão e o balanceamento de carga de Camada 7, todas as solicitações entre o cliente e o servidor são enviadas para o mesmo ponto final, conforme requerido por vários protocolos. As solicitações são distribuídas na camada do aplicativo. Com o balanceamento de carga de Camada 4, as solicitações são distribuídas na camada de transporte. A solução de balanceamento de carga distribui as solicitações do cliente, que conhece somente um endereço IP (algumas vezes chamado do endereço de IP virtual ou VIP), para um conjunto de servidores que executa o trabalho. A conexão entre o cliente e o servidor deve ser estabelecida antes de o conteúdo da solicitação ser determinado, para que o balanceador de carga selecione um servidor para receber a solicitação antes de examinar o conteúdo da solicitação. A seleção do servidor de destino pode ser feita de várias formas, como \&quot;round robin\&quot;, em que cada conexão de entrada passa para o próximo servidor de destino em uma lista circular, ou \&quot;menos conexões\&quot;, em que o balanceador de carga envia cada nova conexão ao servidor que tem menos conexões estabelecidas no momento. Agora que a afinidade de sessão não é exigida, você tem mais flexibilidade, escolhas e facilidade em relação à arquitetura de balanceamento de carga a implantar. O balanceamento de carga sem afinidade de sessão permite aumentar a capacidade e a utilização do balanceador de carga, porque o processamento não é usado para manter mais opções de afinidade envolvidas, como o balanceamento de carga baseado em cookies ou a ID de sessão de Secure Sockets Layer (SSL).

## Matriz do servidor de Acesso para Cliente e Exchange 2013

No Exchange 2010, apresentamos o conceito de uma matriz de Acesso para Cliente. Após uma matriz de Acesso para Cliente ser configurada em um site do Active Directory, todos os servidores de Acesso para Cliente no site automaticamente se tornam membros da matriz. Em versões atuais do Exchange 2013, não é necessário configurar a matriz de Acesso para Cliente, porque a implantação de um balanceamento de carga e o serviço de alta disponibilidade são muito mais simples.

## Soluções de balanceamento de carga

O uso dos balanceadores de carga de hardware ainda é suportado para Exchange 2013. Para obter informações sobre as soluções de balanceamento de carga de hardware que concluiu os testes com Exchange 2010 da solução e trabalho provavelmente tão bem com Exchange 2013, verá [implantação de Balanceador de carga do Exchange Server 2010](https://go.microsoft.com/fwlink/p/?linkid=261834). Tenha em mente que esta página mostra a configuração de camada 7 mais complexa de balanceadores de carga de hardware com Exchange 2010. Tráfego de Exchange 2013 balanceamento de carga pode ser muito mais simples, dado as mudanças de arquitetura discutidas anteriormente neste tópico. Em vez de configurar a afinidade de sessão para cada um dos protocolos Exchange, conexões de entrada para Exchange 2013 os servidores de acesso para cliente podem ser direcionadas para um servidor disponível pelo Balanceador de carga com sem afinidade adicional processamento necessário. Balanceador de carga de hardware ainda tem um papel importante no fornecimento de alta disponibilidade do serviço do Exchange, pois ele pode detectar quando um servidor de acesso para cliente específico ficou indisponível e removê-lo do conjunto de servidores que lidará com conexões de entrada.

## Balanceamento de carga de rede do Windows

O Balanceamento de Carga de Rede do Windows (WNLB) é um balanceador de carga de software comum usado em servidores do Exchange. Há várias limitações associadas à implantação do WNLB com o Microsoft Exchange.

  - O WNLB não pode ser usado em servidores do Exchange em que as DAGs de caixas de correio também estão sendo usadas porque o WNLB é incompatível com clusters de failover do Windows. Se você estiver usando um DAG do Exchange 2013 e deseja utilizar o WNLB, será necessário executar a função de servidor de Acesso para Cliente e a função de servidor de Caixa de Correio em servidores separados.

  - O WNLB não detecta interrupções de serviço. O WNLB detecta apenas interrupções de serviço por endereço IP. Isso significa que se determinado serviço Web, como o Outlook Web App, falhar e o servidor ainda estiver em funcionamento, o WNLB não detectará a falha e continuará a direcionar as solicitações para aquele servidor de Acesso para Cliente. Será necessário intervir manualmente para remover do pool de balanceamento de carga o servidor de Acesso para Cliente que está passando por interrupções.

  - Usar o WNLB pode resultar em saturação de porta, que pode sobrecarregar as redes.

  - Como o WNLB desempenha a afinidade de cliente usando apenas o endereço IP de origem, esta não é uma solução eficaz quando o pool de IP de origem é pequeno. Isto pode ocorrer quando o pool de IP de origem vem de uma sub-rede remota ou quando sua organização está usando a conversão de endereços de rede.

