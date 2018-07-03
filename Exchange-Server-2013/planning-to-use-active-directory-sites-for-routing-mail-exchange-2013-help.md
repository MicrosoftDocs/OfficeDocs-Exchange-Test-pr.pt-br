---
title: 'Planejar o uso de sites do Active Directory para roteamento de email: Exchange 2013 Help'
TOCTitle: Planejar o uso de sites do Active Directory para roteamento de email
ms:assetid: 0f697cee-bcaa-4c69-b80c-7a2afd1817d2
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Aa996299(v=EXCHG.150)
ms:contentKeyID: 52058788
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Planejar o uso de sites do Active Directory para roteamento de email

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2013-05-21_

O Microsoft Exchange Server 2013 reconhece os sites do Active Directory e os grupos de disponibilidade de banco de dados (DAGs) como limites de roteamento. No entanto, o Exchange 2013 ainda usa a topologia de sites do Active Directory para determinar como as mensagens são transportadas entre os servidores do Exchange em DAGs diferentes ou em sites dentro da organização. Para obter mais informações, consulte [Roteamento de mensagens](mail-routing-exchange-2013-help.md).

O serviço Transporte em um servidor de Caixa de Correio fornece o transporte de mensagens dentro da organização do Exchange. Quando você implanta uma organização pura do Exchange 2013 ou inclui o Exchange 2013 em uma organização pura do Exchange Server 2010, nenhuma configuração adicional é necessária para estabelecer o roteamento na floresta.

**Sumário**

How Exchange 2013 uses Active Directory site membership

Determine Active Directory site membership

Overview of IP site links

Exchange 2013 server placement in Active Directory sites

## Como o Exchange 2013 usa a associação do site do Active Directory

O Exchange 2013 é um aplicativo com suporte para site. Os aplicativos com suporte para site podem determinar sua própria associação do site do Active Directory e a associação do site de outros servidores, consultando o Active Directory. O Exchange 2013 usa a associação de site para determinar quais controladores de domínio e servidores de catálogo global usar para o processamento de consultas do Active Directory. Além disso, quando um servidor que executa o Exchange tiver que determinar a associação do site do Active Directory de outro servidor do Exchange, ele poderá consultar o Active Directory para recuperar o nome do site.

No Exchange 2013, o serviço de Topologia do Active Directory do Microsoft Exchange é responsável pela atualização do atributo do site do objeto do servidor Exchange. Como a associação do site do Active Directory é um atributo do objeto do servidor, o Exchange não precisa consultar o DNS para resolver um endereço de servidor para uma sub-rede associada a um site do Active Directory. Carimbar o atributo de site do Active Directory em um objeto de servidor do Exchange também permite que a associação de site do Active Directory seja atribuída a um servidor que não seja membro de um domínio, como um servidor de Transporte de Borda inscrito.

Os servidores do Exchange 2013 usam as informações de associação do Active Directory da seguinte maneira:

  - **Envio de email**   O serviço Envio de Transporte de Caixa de Correio em um servidor de Caixa de Correio do Exchange 2013 usa as informações de associação do site do Active Directory para determinar os outros servidores de Caixa de Correio do Exchange 2013 que estão localizados no mesmo site do Active Directory. Se o servidor de Caixa de Correio de origem não pertencer a um DAG, ou se o DAG não envolver vários sites do Active Directory, o serviço de Envio de Transporte de Caixa de Correio no servidor de Caixa de Correio de origem enviará as mensagens para roteamento e transporte ao serviço Transporte em um servidor de Caixa de Correio do Exchange 2013 no mesmo site do Active Directory.

  - **Entrega de email**   O serviço Transporte em um servidor de Caixa de Correio do Exchange 2013 executa resolução de destinatário e consulta o Active Directory a fim de comparar um endereço de email à conta de um destinatário. As informações da conta do destinatário incluem o FQDN (nome de domínio totalmente qualificado) do banco de dados de caixa de correio do usuário. O serviço Transporte consulta o Active Directory para determinar o site do Active Directory do banco de dados de caixa de correio do usuário. Se o banco de dados de caixa de correio não pertencer a um DAG, ele entregará a mensagem a esse servidor de Caixa de Correio. Do contrário, a mensagem será retransmitida para outro servidor de Caixa de Correio no mesmo site que o servidor de Caixa de Correio de destino para entrega.

  - **Roteamento de mensagem**   O serviço Transporte nos servidores de Caixa de Correio do Exchange 2013 recupera informações do Active Directory para determinar como os emails devem ser roteados dentro da organização. O Exchange 2013 usa o conceito de *grupos de entrega* para determinar onde e como rotear as mensagens. Dependendo do destino, a mensagem pode ser roteada para o serviço Transporte ou para o serviço Entrega de Transporte de Caixa de Correio em um servidor de Caixa de Correio do Exchange 2013 ou para um servidor de Transporte de Hub que está executando uma versão anterior do Exchange. Para obter mais informações, consulte [Roteamento de mensagens](mail-routing-exchange-2013-help.md).

  - **Envio de mensagem de Unificação de Mensagens**   O serviço Unificação de Mensagens nos servidores de Caixa de Correio do Exchange 2013 usam informações de associação do site do Active Directory para encontrar outros servidores de Caixa de Correio localizados no mesmo site do Active Directory. O serviço de Unificação de Mensagens envia mensagens para roteamento ao serviço Transporte em um servidor de Caixa de Correio dentro do mesmo site do Active Directory. O servidor do serviço Transporte executa resolução de destinatário e consulta o Active Directory para comparar um número de telefone, o número E.164 ou um endereço SIP a uma conta de destinatário. Depois de concluída a resolução de destinatário, o serviço Transporte entrega a mensagem à caixa de correio de destino da mesma forma que uma mensagem de email comum.

  - **Conexões de cliente ao servidor de Acesso para Cliente**   Quando o servidor de Acesso para Cliente recebe uma solicitação de conexão do usuário, ele consulta o Active Directory para determinar qual servidor de Caixa de Correio está hospedando a caixa de correio do usuário. Em seguida, o servidor de Acesso para Cliente recupera a associação do site do Active Directory desse servidor de Caixa de Correio e executa o proxy na conexão com o servidor de Caixa de Correio.

## Determinar a associação do site do Active Directory

Os clientes do Active Directory presumem a associação de site fazendo a correspondência entre seu endereço IP designado e uma sub-rede definida nos Sites e Serviços do Active Directory e associada a um site do Active Directory. Em seguida, o cliente usa essas informações para determinar quais controladores de domínio e servidores de catálogo global existem nesse site e se comunica com esses servidores de diretório para fins de autenticação e autorização. O Exchange 2013 aproveita esse relacionamento preferindo também recuperar as informações sobre destinatários dos servidores de diretório que estejam no mesmo site do servidor do Exchange 2013.

Todos os computadores que fazem parte do mesmo site do Active Directory são considerados bem conectados, com uma conexão de rede confiável e de alta velocidade. Por padrão, quando uma floresta do Active Directory é implantada pela primeira vez, há um único site chamado `Default-First-Site-Name`. Se nenhum outro site for configurado manualmente pelo administrador, todos os computadores do servidor e do cliente na floresta serão considerados membros do `Default-First-Site-Name`.

Quando mais de um site é definido, o administrador do Active Directory deve definir as sub-redes presentes na organização e associar essas sub-redes aos sites do Active Directory.

O serviço de Topologia do Microsoft Exchange Active Directory verifica o atributo da associação do site no objeto do servidor Exchange quando o servidor é iniciado. Se o atributo do site tiver que ser atualizado, o serviço Topologia do Microsoft Exchange Active Directory carimba o atributo com o novo valor. O serviço de Topologia do Microsoft Exchange Active Directory verifica o atributo do site a cada 15 minutos e atualiza o valor se a associação do site tiver sido alterada. O serviço de Topologia do Microsoft Exchange Active Directory usa o serviço Logon de Rede para obter a associação do site atual. O serviço Logon de Rede atualiza a associação do site a cada cinco minutos. Isso significa que um período de latência de até 20 minutos pode transcorrer entre o horário em que a associação do site é alterada e horário em que o novo valor é carimbado no atributo do site.

## Visão geral de links de site de IP

Os relacionamentos entre os sites do Active Directory são definidos pelos links de site de IP. O link de site de IP é formado por dois ou mais sites do Active Directory. Todos os sites do Active Directory que fazem parte do link se comunicam com o mesmo custo. As propriedades do link de site de IP incluem atribuição de custo, agenda e intervalo. As propriedades de agenda e intervalo são usadas apenas para determinar a frequência de replicação do Active Directory. O Exchange 2013 usa a atribuição de custo para determinar a rota de custo mais baixo a ser usada pelo tráfego quando existirem vários caminhos para o destino. O custo da rota é determinado agregando o custo de todos os links de site de um caminho de transmissão. O administrador do Active Directory atribui o custo a um link com base na velocidade de rede relativa e na largura de banda disponível comparada a outras conexões disponíveis.

Por padrão, o serviço Transporte em um servidor de Caixa de Correio sempre tenta uma conexão direta com o serviço Transporte ou o serviço de Entrega de Transporte de Caixa de Correio em um servidor de Caixa de Correio em outro site do Active Directory. As mensagens sendo transportadas não são retransmitidas por meio do serviço Transporte em cada servidor de Caixa de Correio em um caminho de link de site. No entanto, os servidores de Caixa de Correio em sites intermediários do Active Directory ao longo do caminho de roteamento podem executar a retransmissão de mensagens nas seguintes situações:

  - A retransmissão direta entre os servidores de Caixa de Correio não ocorrerá quando existir um site de hub ao longo do caminho de roteamento de menor custo. Você pode configurar um site do Active Directory como um site de hub para que essas mensagens sejam roteadas pelo site do hub antes que as mensagens sejam retransmitidas para o servidor de destino. Os sites de hub serão discutidos posteriormente neste tópico.

  - O Exchange 2013 usa o caminho de roteamento derivado das informações do link de site de IP quando a comunicação com o site de destino do Active Directory falhar. Se nenhum servidor de Caixa de Correio no site de destino do Active Directory responder, a entrega de mensagem retorna pelo caminho de roteamento de menor custo até que uma conexão seja feita com um servidor de Caixa de Correio em um site do Active Directory ao longo do caminho de roteamento. As mensagens são colocadas em fila nesse site do Active Directory e a fila ficará em estado de repetição. Esse comportamento é chamado *fila no ponto de falha*.

  - Nas organizações do Exchange 2013 sem DAGs, o serviço Transporte em um servidor de Caixa de Correio também pode usar as informações de link de site de IP para aprimorar o roteamento de mensagens enviadas a vários destinatários. O servidor de Caixa de Correio atrasa a bifurcação de mensagens até que cheguem a uma bifurcação nos caminhos de roteamento aos destinatários. A mensagem bifurcada é retransmitida a cada destino do destinatário por um servidor de Caixa de Correio no site do Active Directory que represente a bifurcação nos caminhos de roteamento individuais. Essa funcionalidade é chamada de *fanout em atraso*.

## Designar sites de hub

Você pode usar o cmdlet **Set-AdSite** para configurar um site do Active Directory como um site de hub. Quando um site de hub existir ao longo do caminho de roteamento de menor custo entre dois servidores de transporte, as mensagens serão roteadas pelo site de hub para processamento, antes de serem retransmitidas para o servidor de destino. Para que este comportamento de roteamento ocorra, o site de hub deverá existir ao longo do caminho de roteamento de menor custo entre dois servidores de transporte. Essa configuração só deve ser usada quando for necessária para a topologia da rede, como quando há firewalls entre os sites do Active Directory impedindo a retransmissão de comunicações SMTP. Para obter mais informações, consulte [Configurar definições de roteamento de email do Exchange no Active Directory](configure-exchange-mail-routing-settings-in-active-directory-exchange-2013-help.md).

## Configurar um custo específico do Exchange em um link de site de IP

Você pode usar o cmdlet **Set-AdSiteLink** no Shell de Gerenciamento do Exchange para configurar um custo específico do Exchange para o link do site de IP do Active Directory. O custo específico do Exchange é um atributo separado que é usado em vez do custo atribuído pelo Active Directory para determinar o caminho de roteamento do Exchange. Essa configuração é útil quando os custos do link do site de IP do Active Directory não resultam em uma topologia ideal de roteamento de mensagens do Exchange. Para obter mais informações, consulte [Configurar definições de roteamento de email do Exchange no Active Directory](configure-exchange-mail-routing-settings-in-active-directory-exchange-2013-help.md).

## Definir restrições de tamanho de mensagem em links de site de IP

Por padrão, o Exchange 2013 não impõe um limite máximo de tamanho para as mensagens que são retransmitidas entre os servidores de Caixa de Correio em diferentes sites do Active Directory. Se você utilizar o cmdlet **Set-AdSiteLink** para configurar o tamanho máximo da mensagem em um link de site de IP do Active Directory, o roteamento criará um relatório de falha na entrega (NDR) para as mensagens que possuam um tamanho superior ao limite estipulado no link de site do Active Directory, no caminho de roteamento de menor custo. Essa configuração é útil para restringir o tamanho das mensagens enviadas aos sites remotos do Active Directory que precisam se comunicar por conexões de largura de banda baixa.

## Localização do servidor do Exchange 2013 nos sites do Active Directory

Para que o roteamento de mensagens entre os servidores do Exchange 2013 ocorra corretamente, todos os servidores do Exchange implantados na floresta devem pertencer a um site do Active Directory. Verifique se os endereços IP que você atribuiu estão nas sub-redes que estão associadas corretamente aos sites do Active Directory.

A primeira etapa do planejamento da localização de servidores Exchange 2013 na topologia do site do Active Directory é a documentação da topologia atual. A documentação deverá incluir o seguinte:

  - Sites

  - Sub-redes e suas associações de site

  - Links do site de IP e seus sites membro

  - Custos do link de site de IP

  - Servidores de diretório em cada site

  - Conexões de rede física

  - Locais de firewall

Após ter diagramado esses objetos, planeje a localizações dos servidores do Exchange. Considere as seguintes informações ao decidir onde colocar os servidores:

  - Um servidor de Caixa de Correio precisa se comunicar diretamente com um servidor de catálogo global para executar as pesquisas do Active Directory.

  - Recomendamos que você implante mais de um servidor de Caixa de Correio em cada site do Active Directory para oferecer balanceamento de carga e tolerância a falhas.

  - DAGs e resiliência de site

  - O serviço Unificação de Mensagens nos servidores de Caixa de Correio envia mensagens de correio de voz ao serviço Transporte nos servidores de Caixa de Correio para entrega às caixas de correio. O servidor de Acesso para Cliente que está executando o serviço Roteador de Chamada de Unificação de Mensagens pode estar localizado em um site de hub ou próximo ao gateway IP ou VoIP (Voz sobre IP), PBX IP (IP Private Branch eXchange), PBX habilitado para SIP ou SBC (controladores de borda de sessão). O serviço Transporte em um servidor de Caixa de Correio que tem a mesma associação de site que o servidor de Acesso para Cliente receberá as mensagens de correio de voz para transporte e as roteará até o serviço Transporte em outros servidores de Caixa de Correio na organização.

  - Os servidores de Acesso para Cliente fornecem um ponto de conectividade para a organização do Exchange para os usuários que estiverem acessando o Exchange remotamente. Um servidor de Acesso para Cliente deve ser implantado em cada site do Active Directory que contenha servidores de Caixa de Correio.

Depois de planejar a localização do servidor do Exchange 2013, você pode identificar as áreas onde pode modificar a topologia de site do Active Directory para melhorar o fluxo da comunicação. Convém ajustar os links de site de IP e os custos do link de site para aprimorar a entrega de email. Uma topologia eficiente do Active Directory não exige alterações para oferecer suporte ao Exchange 2013.

