---
title: 'Roteamento de mensagens: Exchange 2013 Help'
TOCTitle: Roteamento de mensagens
ms:assetid: 6fd39079-9655-4fd9-9269-c7462c76e0a7
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Aa998825(v=EXCHG.150)
ms:contentKeyID: 50485792
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Roteamento de mensagens

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2015-03-09_

A tarefa principal do serviço de Transporte que existe em todos os servidores de Caixa de Correio na sua organização do Microsoft Exchange Server 2013 é rotear mensagens recebidas de usuários e fontes externas para seus destinos. As decisões de roteamento são feitas durante a categorização de mensagens. O categorizador é um componente do serviço de Transporte em um servidor de Caixa de Correio que processa todas as mensagens de entrada e determina o que fazer com as mensagens com base nas informações sobre seus destinos.

O roteamento no Exchange 2013 agora reconhece totalmente os Grupos de Disponibilidade de Bancos de Dados (DAGs) e usa a associação ao DAG como um limite de roteamento. Por quê? Em Exchange 2013, todos os servidores de Caixa de Correio hospedam o serviço de Transporte. Assim, quando um servidor de Caixa de Correio faz parte de um DAG, o mecanismo principal para rotear mensagens fica bastante alinhado ao DAG. E, quando um DAG se distribui por vários sites do Active Directory, usar o site do Active Directory como limite de roteamento principal não é eficiente. O Exchange 2013 também usa a associação ao site do Active Directory como um limite de roteamento para servidores de Caixa de Correio que não pertençam aos DAGs e para interoperabilidade com versões anteriores do Exchange. Outras alterações notáveis no roteamento do Exchange 2013 incluem:

  - O serviço de Transporte em um servidor de Caixa de Correio nunca se comunica diretamente a um banco de dados de caixa de correio. Em vez disso, o serviço de Transporte se comunica com o serviço de Transporte de Caixa de Correio no servidor de Caixa de Correio. Somente o serviço de Transporte da Caixa de Correio se comunica com o banco de dados de caixa de correio no servidor de Caixa de Correio local. Quando o servidor de Caixa de Correio é um membro de um DAG, somente o serviço de Transporte de Caixa de Correio, no servidor de Caixa de Correio que contém a cópia ativa do banco de dados de caixa de correio, aceita a mensagem para o destinatário de destino.

  - Chamadas de procedimentos remotos (RPCs) são usadas somente pelo serviço de Transporte de Caixa de Correio ao enviar mensagens para ou responder mensagens do banco de dados de caixa de correio local. Quando o servidor de Caixa de Correio é um membro de um DAG, o serviço de Transporte de Caixa de Correio usa apenas RPCs para se comunicar localmente com as cópias ativas dos bancos de dados de caixas de correio. Em outras palavras, a RPC nunca é usada para comunicação entre servidores. Em vez disso, o serviço de Transporte de Caixa de Correio e o serviço de Transporte em diferentes servidores de Caixa de Correio sempre se comunicam usando SMTP.

  - O Exchange 2013usa um processo de fila mais preciso para destinos remotos. Em vez de usar uma fila para todos os destinos em um site do Active Directory remoto, o Exchange 2013 coloca as mensagens em fila para destinos específicos dentro do site do Active Directory, como conectores de Envio individuais.

  - Conectores vinculados foram preteridos. Um conector vinculado era um conector de Recebimento vinculado a um conector de Envio. Todas as mensagens recebidas pelo conector de Recebimento eram encaminhadas automaticamente para o conector de Envio.

**Sumário**

Routing components

  - Routing destinations

  - Delivery groups

  - Queues

Routing messages

  - Routing messages between Active Directory sites

  - Routing in the Front End Transport service

  - Routing in the Mailbox Transport service

  - Routing in the Transport service on Edge Transport servers

## Componentes de roteamento

Quando uma mensagem é recebida por um serviço de Transporte em um servidor de Caixa de Correio do Exchange 2013, essa mensagem deve ser categorizada. A primeira fase da categorização da mensagem é a resolução do destinatário. Depois que o destinatário é resolvido, o destino final pode ser determinado. A fase seguinte, o roteamento, determina a melhor maneira de se chegar a esse destino. O roteamento no Exchange 2013 foi generalizado para maior flexibilidade e menor complexidade, apresentando os conceitos de destinos de roteamento e grupos de entrega.

## Destinos de roteamento

No Exchange 2013, o destino final de uma mensagem é chamado de *destino de roteamento*. Os seguintes destinos de roteamento existem no Exchange 2013:

  - **Um banco de dados de caixa de correio**   Esse é o destino de roteamento para qualquer destinatário com uma caixa de correio em um servidor de Caixa de Correio na organização do Exchange. No Exchange 2013, as pastas públicas são um tipo de caixa de correio, então, rotear mensagens para destinatários de pastas públicas é o mesmo que rotear mensagens para destinatários de caixa de correio.

  - **Um conector**   Um conector é um conector de Envio para mensagens SMTP quando usado como um destino de roteamento. Um conector de Agente de Entrega ou um conector Externo é usado como um destino de roteamento para mensagens que não sejam SMTP.

  - **Um servidor de expansão de grupo de distribuição**   Esse é o destino de roteamento quando um grupo de distribuição tiver um servidor de expansão designado que é responsável por expandir a lista de associação do grupo. Um servidor de expansão de um grupo de distribuição é sempre um servidor de Transporte de Hub ou um servidor de Caixa de Correio do Exchange 2013.

Observe que esses mesmos destinos de roteamento também existiam em versões anteriores do Exchange.

Voltar ao início

## Grupos de entrega

Cada destino de roteamento no Exchange 2013 tem uma coleção de um ou mais servidores de transporte que são responsáveis por entregar mensagens para o destino de roteamento. Essa coleção de servidores de transporte é chamada de *grupo de entrega*. Um servidor de transporte pode ser um servidor de Caixa de Correio do Exchange 2013 , ou um servidor do Exchange 2010 ou um servidor do Exchange 2007 que possui a função de servidor Transporte de Hub instalada. Quando o destino de roteamento for um banco de dados de caixa de correio, os servidores de transporte no grupo de entrega têm a mesma versão do Exchange que o banco de dados de caixa de correio. Quando o destino do roteamento é um conector ou um servidor de expansão do grupo de distribuição, o grupo de entrega contém uma mistura de servidores de Caixa de Correio do Exchange 2013 e do Exchange 2010 ou servidores de Transporte de Hub do Exchange 2007 . Como a mensagem é roteada depende do relacionamento entre o servidor de transporte de origem e o grupo de entrega de destino:

  - Se o servidor de transporte de origem estiver no grupo de entrega de destino, o destino de roteamento em si será o salto seguinte para a mensagem. A mensagem é entregue pelo servidor de transporte de origem para o banco de dados de caixa de correio ou conector em um servidor de transporte no grupo de entrega. Observe que, quando um servidor de expansão de grupo de distribuição for o destino de roteamento, o grupo de distribuição já estará expandido no momento em que as mensagens alcançarem o estágio de roteamento da categorização no servidor de expansão de grupo de distribuição. Entretanto, o destino de roteamento do servidor de expansão do grupo de distribuição sempre será um banco de dados de caixa de correio ou um conector.

  - Se o servidor de transporte de origem estiver fora do grupo de entrega de destino, a mensagem será retransmitida pelo caminho de roteamento de menor custo para o grupo de entrega de destino. Dependendo do tamanho e da complexidade da topologia do Exchange, a mensagem será retransmitida para outros servidores de transporte no caminho de roteamento de menor custo ou a mensagem será retransmitida diretamente para um servidor de transporte no grupo de entrega de destino.

Os seguintes tipos de grupos de entrega existem no Exchange 2013:

  - **DAG roteável**   É uma coleção de servidores de Caixa de Correio do Exchange 2013 que pertencem a um DAG. Os bancos de dados de caixa de correio no DAG estão são os destinos de roteamento que são servidos por esse grupo de entrega. Depois de a mensagem chegar ao serviço de Transporte em um servidor de Caixa de Correio que faça parte do DAG, o serviço de Transporte roteia a mensagem ao serviço de Transporte de Caixa de Correio, no servidor de Caixa de Correio no DAG que atualmente retenha a cópia ativa do banco de dados da caixa de correio de destino. Então, o serviço de Transporte da Caixa de Correio no servidor de Caixa de Correio de destino entrega a mensagem ao banco de dados de caixa de correio local. Apesar de um DAG poder conter servidores de Caixa de Correio localizados em sites do Active Directory diferentes, o DAG fica no limite do grupo de entrega.

  - **Grupo de entrega de caixa de correio**   É uma coleção de servidores Exchange da mesma versão localizados em um site do Active Directory. O site do Active Directory fica no limite do grupo de entrega. Os destinos de roteamento e os grupos de entrega que os atendem são separados pelas versões principais do Exchange no site do Active Directory. Os bancos de dados de caixa de correio localizados nos servidores de Caixa de Correio do Exchange 2010 são atendidos pelos servidores de Transporte de Hub do Exchange 2010 localizados no site do Active Directory. Os bancos de dados da caixa de correio localizados nos servidores de Caixa de Correio do Exchange 2007 são mantidos pelos servidores de Transporte de Hub do Exchange 2007 localizados no site do Active Directory. Os bancos de dados de caixa de correio localizados nos servidores de Caixa de Correio do Exchange 2013 no site do Active Directory que não fazem parte de um DAG são atendidos pelo serviço de Transporte nos servidores de Caixa de Correio do Exchange 2013 no site do Active Directory. Como a mensagem é entregue ao banco de dados de caixa de correio depende da versão do Exchange:
    
      - **Exchange 2013**    Depois de a mensagem chegar ao servidor de Caixa de Correio de destino no site do Active Directory de destino, o serviço de Transporte usa SMTP para transferir a mensagem ao serviço de Transporte da Caixa de Correio. O serviço de Transporte da Caixa de Correio, então, entrega a mensagem ao banco de dados de caixa de correio local, usando RPC.
    
      - **Exchange 2010 ou Exchange 2007**   Após a mensagem chegar a um servidor de Transporte de Hub aleatório da mesma versão que do site de destino do Active Directory, o driver de armazenamento no servidor de Transporte de Hub usa o RPC para gravar a mensagem no banco de dados de caixa de correio.

  - **Servidores de origem do conector**   Esta é uma cloeção mista dos servidores de Transporte de Hub do Exchange 2010 ou do Exchange 2007 , ou dos servidores de Caixa de Correio do Exchange 2013 que estão no escopo como a servidor de origem para um conector de Envio, um conector do Agente de Entrega ou um conector Externo. O conector é o destino de roteamento que é atendido por esse grupo de roteamento. Quando um conector é colocado no escopo de um servidor específico, somente esse servidor ter permissão para rotear mensagens para um destino definido pelo conector. Este grupo de entrega pode conter os servidores de Transporte de Hub do Exchange 2010 ou do Exchange 2007 , ou os servidores de Caixa de Correio do Exchange 2013 em diferentes sites do Active Directory.

  - **Site do AD**   Em alguns casos, um site do Active Directory não é o último destino de uma mensagem, mas a mensagem deve passar por um servidor de Transporte de Hub do Exchange 2010 ou do Exchange 2007 ou por um servidor de Caixa de Correio do Exchange 2013 naquele site do Active Directory. Essas circunstâncias incluem:
    
      - Quando o site do Active Directory é configurado como um site de hub. Sempre que houver um site de hub ao longo do caminho de roteamento de menor custo para entrega de mensagens, as mensagens serão colocadas em fila e processadas por um servidor de Transporte no site de hub antes de serem retransmitidas para o destino final.
    
      - Quando um servidor de Transporte de Borda for inscrito no site do Active Directory. Esses servidores de Transporte de Borda inscritos não são acessíveis diretamente de outros sites do Active Directory. Observe que o servidor de Transporte de Borda poderia ser o Exchange 2013, o Exchange 2010 ou o Exchange 2007.
    

    > [!NOTE]
    > O fan-out em atraso é usado somente quando o grupo de entrega está em um site do Active Directory. O fan-out em atraso tenta reduzir o número de transmissões de mensagens, quando vários destinatários compartilham qualquer parte do caminho de roteamento de menor custo.



  - **Lista de servidores**   Esta é uma coleção de um ou mais servidores de Transporte de Hub do Exchange 2010 ou do Exchange 2007 ou de servidores de Caixa de Correio do Exchange 2013 configurados como servidores de expansão do grupo de distribuição. O servidor de expansão do grupo de distribuição é o destino de roteamento atendido por esse grupo de entrega.

A associação ao grupo de entrega não é mutuamente exclusiva. Por exemplo, um servidor de Caixa de Correio do Exchange 2013 que seja membro de um DAG também pode ser o servidor de origem de um conector de Envio dentro do escopo. Esse servidor de Caixa de Correio faria parte do grupo de entrega de DAG roteável para os bancos de dados de caixa de correio no DAG e também de um grupo de entrega de servidores de origem de conector para o conector de Envio dentro do escopo.

A seguinte tabela mapeia os destinos de roteamento para o grupo de entrega, com base na versão do Exchange envolvida:


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th> </th>
<th>Servidor de Caixa de Correio do Exchange 2013</th>
<th>ou servidor de Transporte de Hub Exchange 2007</th>
<th>Servidor de Transporte de Borda na rede de perímetro</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Banco de dados de caixa de correio em um DAG</p></td>
<td><p>DAG roteável</p></td>
<td><p>Grupo de entrega de caixa de correio</p></td>
<td><p>n/a</p></td>
</tr>
<tr class="even">
<td><p>Banco de dados de caixa de correio não em um DAG</p></td>
<td><p>Grupo de entrega de caixa de correio</p></td>
<td><p>Grupo de entrega de caixa de correio</p></td>
<td><p>n/a</p></td>
</tr>
<tr class="odd">
<td><p>Conector</p></td>
<td><p>Servidores de origem do conector</p></td>
<td><p>Servidores de origem do conector</p></td>
<td><p>Site do AD</p></td>
</tr>
<tr class="even">
<td><p>Servidor de expansão do grupo de distribuição</p></td>
<td><p>Lista de servidores</p></td>
<td><p>Lista de servidores</p></td>
<td><p>n/a</p></td>
</tr>
</tbody>
</table>


Voltar ao início

## Filas

Da perspectiva do servidor de envio, cada fila de entrega representa o destino de uma mensagem determinada. Quando o serviço de Transporte no servidor de Caixa de Correio do Exchange 2013 seleciona o destino de uma mensagem, esse destino é marcado no destinatário como o atributo **NextHopSolutionKey**. Se uma única mensagem estiver sendo enviada a mais de um destinatário, cada destinatário possui o atributo **NextHopSolutionKey**. O servidor de destino também executa a categorização da mensagem e coloca em fila a mensagem para entrega. Depois que uma mensagem é colocada em fila, você pode examinar o tipo de entrega de uma determinada fila para saber se a mensagem será retransmitida novamente ao chegar ao destino do próximo salto. Cada valor exclusivo do atributo **NextHopSolutionKey** corresponde a uma fila de entrega separada.

Para obter mais informações, consulte a seção "NextHopSolutionKey", no tópico [Filas](queues-exchange-2013-help.md).

Voltar ao início

## Rotear mensagens

Quando uma mensagem precisa ser entregue por um grupo de distribuição remoto, um caminho de roteamento deve ser definido para a mensagem. use a seguinte lógica para escolher um caminho de roteamento para uma mensagem. Essa lógica está basicamente inalterada desde o Exchange 2010:

1.  Calcule o caminho de roteamento de menor custo, adicionando o custo dos links de site IP que devem ser percorridos para chegar ao destino. Se o destino for um conector, o custo atribuído ao espaço de endereçamento é adicionado ao custo para chegar ao conector selecionado. Se forem possíveis vários caminhos de roteamento, o caminho de roteamento de menor custo agregado será usado.

2.  Se houver mais de um caminho de roteamento com o mesmo custo agregado, o número de saltos em cada caminho será avaliado e será usado o caminho de roteamento com o menor número de saltos.

3.  Se ainda houver mais de um caminho de roteamento disponível, o nome atribuído aos sites do Active Directory antes do destino será considerado. Será usado o caminho de roteamento no qual o site do Active Directory mais próximo ao destino estiver mais abaixo na ordem alfanumérica. Se o site mais próximo do destino for o mesmo para todos os caminhos de roteamento avaliados, será considerado um nome de site anterior.

No Exchange 2010, cada destinatário de mensagem estará sempre associado a apenas um site do Active Directory, e haverá somente uma rota de menor custo do site do Active Directory para o site do Active Directory de destino. No Exchange 2013, um grupo de distribuição pode percorrer vários sites do Active Directory, e podem haver vários caminhos de roteamento de menor custo para estes vários sites do Active Directory. designa um site do Active Directory no grupo de distribuição de destino como o *site principal*. O site principal é o site do Active Directory mais próximo, com base na lógica de roteamento descrita anteriormente. Para rotear com êxito mensagens entre grupos de entrega, o Exchange 2013 leva os seguintes pontos em consideração:

  - **A presença de um ou mais sites de hub no caminho de roteamento de menor custo**   Se o caminho de roteamento de menor custo para o site principal contiver sites de hub, a mensagem deve ser roteada através dos sites de hub. O site de hub mais próximo no caminho de roteamento de menor custo é selecionado como um novo grupo de entrega do tipo **AD site**, que inclui todos os servidores de transporte no site de hub. Depois de a mensagem atravessar o site de hub, o roteamento da mensagem no caminho de roteamento de menor custo continua. Se o site principal for um site de hub, o site principal ainda será considerado um site de hub, por estas razões:
    
      - Se o grupo de entrega de destino abranger vários sites de Active Directory, o servidor de origem deverá se conectar somente aos servidores no site de hub.
    
      - Os servidores no site de hub que realmente pertencem ao grupo de entrega de destino terão preferência.
    
    Em uma versão anterior do Exchange, quaisquer sites de hub que não estiverem no caminho de roteamento de menor custo para o site principal serão ignorados.

  - **O servidor Exchange de destino para selecionar o grupo de roteamento de destino**   Quando o grupo de entrega de destino abrange vários sites do Active Directory, o caminho de roteamento para servidores específicos dentro do grupo de entrega podem ter custos diferentes. Os servidores localizados no site do Active Directory mais próximos são selecionados como servidores de destino para o grupo de entrega, com base no caminho de roteamento de menor custo e o site do Active Directory cujos servidores estiverem selecionados como o site principal.

  - **Opções de fallback quando as tentativas de conexão a todos os servidores no grupo de roteamento de destino falham**   Se o grupo de entrega de destino abranger vários sites do Active Directory, a primeira opção de fallback será todos os outros servidores no grupo de entrega de destino em outros sites do Active Directory que não forem selecionados como servidores de destino. A seleção do servidor é feita com base no custo do caminho de roteamento para esses outros sites do Active Directory. Se o grupo de entrega de destino tiver quaisquer servidores no site do Active Directory local, não haverá outras opções de fallback, porque a mensagem já está o mais próximo possível do destino de roteamento. Se o grupo de entrega de destino tiver servidores nos sites do Active Directory remotos, a opção será tentar se conectar a todos os outros servidores no site principal. Se isso não der certo, um caminho de retirada no caminho de roteamento de menor custo para o site principal será usado. O Exchange 2013 tenta entregar a mensagem o mais perto possível do destino recuando, salto por salto, ao longo do caminho de roteamento de menor custo até que uma conexão seja feita.

Voltar ao início

## Roteamento de mensagens entre sites do Active Directory

O modo como o Exchange 2013 roteia mensagens entre sites do Active Directory é virtualmente o mesmo que o Exchange 2010. Para obter mais informações, consulte [Roteamento de email entre sites do Active Directory](route-mail-between-active-directory-sites-exchange-2013-help.md).

Voltar ao início

## Direcionar no serviço de Transporte de front-end nos servidores de Acesso ao Cliente

Isso agre como um proxy sem estado para todo o tráfego SMTP externo de entrada e, opcionalmente, de saída para a organização do Exchange 2013. Para mensagens de saída, o serviço de Transporte usa os conectores de Envio para se comunicar com o serviço de Transporte de Front End em um servidor de Acesso para Cliente. Especificamente as mensagens de saída, têm o proxy definido através do serviço de Transporte Front End quando o parâmetro *FrontEndProxyEnabled* em um Enviar conector aplicável é definido como `$true`, ou quando a opção **Proxy através do servidor de Acesso para Cliente** estiver selecionada nas propriedades de Enviar conector no centro de administração do Exchange (EAC). Qualquer servidor de Acesso para Cliente no site local do Active Directory será escolhido. Observe que o serviço de Transporte de front-end não tem Conectores de envio.

Para mensagens de entrada, o serviço de Transporte de Front End deve encontrar rapidamente um serviço de Transporte único e íntegro em um servidor de Caixa de Correio, para receber a transmissão da mensagem, independente do número ou tipo de destinatários. Não fazer isso fará com que o serviço de email seja percebido como indisponível pelos remetentes externos. Assim como o serviço de Transporte, o serviço de Transporte de Front End carrega as tabelas de roteamento com base nas informações do Active Directory e usa grupo de entrega para determinar como rotear mensagens. Entretanto, as tabelas de roteamento usadas pelo serviço de Transporte de Front End têm as seguintes características exclusivas:

  - O serviço de Transporte de Front End nunca é considerada um membro de um grupo de entregas, mesmo quando o servidor de Caixa de Correio e o servidor de Acesso para Cliente estiverem instalados no mesmo servidor físico. Isso força o serviço de Transporte de Front End a se comunicar somente com o serviço de Transporte.

  - As tabelas de roteamento não contêm quaisquer rotas de conector de Envio.

  - As tabelas de roteamento contêm uma lista especial de servidores de Caixa de Correio no site do Active Directory local, para fins de failover rápido.

O roteamento no serviço de Transporte de Front End resolve os destinatários de mensagens para bancos de dados de caixa de correio. A lista de servidores de Caixa de Correio usada pelo serviço de Transporte de Front End é baseada nos bancos de dados de caixa de correio dos destinatários de mensagens. Observe que é possível que nenhum dos destinatários tenha caixas de correio, por exemplo, se o destinatário for um grupo de distribuição ou usuário de email. Para cada banco de dados de caixa de correio, o serviço de Transporte de Front End procura o grupo de entregas e as informações de roteamento associadas. Os grupos de entrega usados pelo serviço de Transporte de Front End são:

  - DAG roteável

  - Grupo de entrega de caixa de correio

  - Site do AD

Dependendo do número e do tipo de destinatários, o serviço de Transporte de Front end executa uma destas ações:

  - Para mensagens com um único destinatário de caixa de correio, selecione um servidor de Caixa de Correio no grupo de entrega de destino e dê preferência ao servidor de Caixa de Correio com base na proximidade do site do Active Directory. Rotear a mensagem para o destinatário pode envolver rotear a mensagem através de um site de hub.

  - Para mensagens com vários destinatários de caixa de correio, use os primeiros 20 destinatários para selecionar um servidor de Caixa de Correio no grupo de entrega mais próximo, com base na proximidade do site do Active Directory. Observe que a bifurcação da mensagem não ocorre no Transporte de Front End, então, somente um servidor de Caixa de Correio é selecionado, no final, independente do número de destinatários em uma mensagem.

  - Se a mensagem não tiver destinatários de caixa de correio, selecione um servidor de Caixa de Correio aleatório, no site do Active Directory local.

Voltar ao início

## Direcionar no serviço de Transporte da Caixa de Correio em servidores de Caixa de Correio

Isso consiste de dois serviços separados: o serviço de Envio de Transporte de Caixa de Correio e serviço de Entrega de Transporte de Caixa de Correio. Para mensagens de entrada, o serviço de Entrega do Transporte de Caixa de Correio recebe mensagens de SMTP do serviço de Transporte e se conecta ao banco de dados de caixa de correio local, usando o RPC para entregar a mensagem. Para mensagens de saída, o serviço de Envio de Transporte de Caixa de Correio se conecta ao banco de dados de caixa de correio local, usando RPC, para recuperar mensagens e envia as mensagens por SMTP para o serviço de Transporte. O serviço de Transporte de Caixa de Correio não tem estado e não coloca quaisquer mensagens localmente na fila.

Assim como o serviço de Transporte, o serviço de Transporte de Caixa de Correio carrega as tabelas de roteamento com base nas informações do Active Directory e usa grupo de entrega para determinar como rotear mensagens. Entretanto, há aspectos do roteamento que são exclusivos do serviço de Transporte de Caixa de Correio:

  - Como os serviços de Transporte e de Transporte de Caixa de Correio existem no mesmo servidor de Caixa de Correio do Exchange 2013, o serviço de Transporte de Caixa de correio sempre faz parte do mesmo grupo de entregas que o servidor de Caixa de Correio. Esse grupo de entregas é conhecido como o *grupo de entregas local*.

  - O serviço de Envio de Transporte de Caixa de Correio não envia automaticamente mensagens para o serviço de Transporte no servidor de Caixa de Correio local ou em outros servidores de Caixa de Correio em seu próprio grupo de entregas local. O serviço de Envio de Transporte de Caixa de Correio tem acesso às mesmas informações de topologia de roteamento que o serviço de Transporte, de forma que o serviço de envio de Transporte de Caixa de Correio possa enviar mensagens para o serviço de Transporte em servidores de Caixa de Correio fora do grupo de entrega. Os servidores de Caixa de Correio no grupo de entregas local são usados como opções de fallback e para entrega para destinatários que não estejam na caixa de correio.

  - O serviço de Transporte de Caixa de Correio se comunica somente com o serviço de Transporte em servidores de Caixa de Correio do Exchange 2013.

  - O serviço de Transporte de Caixa de Correio se comunica somente com bancos de dados de caixa de correio no servidor de Caixa de Correio do Exchange 2013 local. O serviço de Transporte de Caixa de Correio nunca se comunica com bancos de dados de caixa de correio em outros servidores de Caixa de Correio.

Quando um usuário envia uma mensagem de sua caixa de correio, o serviço de Envio de Transporte de Caixa de Correio resolve os destinatários de mensagens para bancos de dados de caixas de correio. A lista de servidores de Caixa de Correio usada pelo serviço de Envio de Transporte de Caixa de Correio é baseada nos bancos de dados de caixa de correio dos destinatários de mensagens. Observe que é possível que nenhum dos destinatários tenha caixas de correio, por exemplo, se o destinatário for um grupo de distribuição ou usuário de email. Para cada banco de dados de caixa de correio, o serviço de Envio de Transporte de Caixa de Correio procura o grupo de entregas e as informações de roteamento associadas. Os grupos de entrega usados pelo serviço de Envio de Transporte de Caixa de Correio são:

  - DAG roteável

  - Grupo de entrega de caixa de correio

  - Site do AD

Dependendo do número e do tipo de destinatários, o serviço de Envio de Transporte de Caixa de Correio executa uma destas ações:

  - Para mensagens com um único destinatário de caixa de correio, selecione um servidor de Caixa de Correio no grupo de entrega de destino e dê preferência ao servidor de Caixa de Correio com base na proximidade do site do Active Directory. Rotear a mensagem para o destinatário pode envolver rotear a mensagem através de um site de hub.

  - Para mensagens com vários destinatários de caixa de correio, use os primeiros 20 destinatários para selecionar um servidor de Caixa de Correio no grupo de entrega mais próximo, com base na proximidade do site do Active Directory.

  - Se a mensagem não tiver destinatários de caixa de correio, selecione um servidor de Caixa de Correio no grupo de entregas local.

Quando o serviço de Entrega de Transporte de Caixa de Correio receber uma mensagem do serviço de Transporte, ele aceita ou rejeita a mensagem para entrega para um banco de dados de caixa de correio local. O serviço de Entrega de Transporte de Caixa de Correio pode entregar a mensagem, se o destinatário residir em uma cópia ativa de um banco de dados de caixa de correio local. Mas, se o destinatário não residir em uma cópia ativa de um banco de dados de caixa de correio local, o serviço de Entrega de Transporte de Caixa de Correio não consegue entregar a mensagem e deve oferecer uma resposta de falha de entrega ao serviço de Transporte. Por exemplo, se a cópia ativa do banco de dados de caixa de correio tiver se movido recentemente para outro servidor, o serviço de transporte pode, erroneamente, transmitir uma mensagem para um servidor de Caixa de Correio que, agora, retém uma cópia do banco de dados de caixa de correio. As respostas de falha de entrega que o serviço de Entrega de Transporte de Caixa de Correio retorna para o serviço de Transporte incluem:

  - Tentar novamente a entrega

  - Gerar uma NDR

  - Rotear novamente a mensagem

Voltar ao início

## Direcionar no serviço de Transporte em servidores de Transporte de Borda

Se você tiver um servidor de Transporte de Borda instalado em sua rede de perímetro, o serviço deste oferecerá retransmissão SMTP e serviços de host inteligente para todo o fluxo de email voltado para a Internet. As mensagens enviadas e recebidas da Internet são enfileiradas localmente no servidor de Transporte de Borda. As filas correspondem a domínios externos ou a Conectores de envio. Para obter mais informações, consulte a seção "NextHopSolutionKey", no tópico [Filas](queues-exchange-2013-help.md).

Normalmente, quando você instala um servidor de Transporte de Borda em sua rede de período, inscreve o servidor de Transporte de Borda em um site do Active Directory. O site do Active Directory contém os servidores de Caixa de Correio que farão a retransmissão das mensagens de e para o servidor de Transporte de Borda. O processo de Inscrição de Borda cria uma afiliação de associação do site do Active Directory para o servidor de Transporte de Borda. A afiliação de site permite que servidores de Caixa de Correio na organização do Active Directory retransmitam mensagens ao servidor de Transporte de Borda para que sejam entregues na Internet sem necessidade de configurar Conectores de envio explícitos.

Em configurações de vários sites, o email de saída de destinatários internos para destinatários externos é direcionado primeiro para o site do Active Directory inscrito. O site do Active Directory de destino é o grupo de entrega. O destino de roteamento é o Conector de envio dentro da organização no serviço de Transporte em qualquer um dos servidores de Caixa de Correio no site do Active Directory inscrito. O *Conector de envio dentro da organização* é um Conector de envio especial existente no serviço de Transporte em todos os servidores de Caixa de Correio. Este Conector de envio é criado implicitamente, é invisível, não exige gerenciamento e é usado para retransmitir mensagens entre servidores do Exchange.

O email de saída para destinatários externos é direcionado do servidor de Caixa de Correio para o servidor de Transporte de Borda. O servidor de Acesso para Cliente não está envolvido no direcionamento de email para um servidor de Transporte de Borda inscrito. O email é transmitido do conector de envio dentro da organização no serviço de Transporte do serviço de Caixa de Correio para um Conector de recebimento no serviço de Transporte do servidor de Transporte de Borda. Em um servidor de Transporte de Borda inscrito, o Conector de recebimento padrão está configurado para ouvir conexões de servidores de Caixa de Correio internos no site do Active Directory inscrito e conexões anônimas da Internet. Depois que a mensagem for categorizada pelo serviço de Transporte no servidor de Transporte de Borda, a mensagem será enfileirada localmente para entrega na Internet usando o Conector de envio dedicado criado durante a Inscrição de Borda.

O email de entrada de destinatários externos chega no Transporte de Borda por meio do Conector de recebimento padrão e as mensagens são categorizadas e enfileiradas para entrega. As mensagens são retransmitidas por meio do Conector de envio dedicado criado pela Inscrição de Borda para enviar emails para a organização do Exchange. Para onde as mensagens irão a seguir dependerá de como seus servidores internos do Exchange estão configurados.

  - **Servidor de Caixa de Correio e servidor de Acesso para Cliente instalados no mesmo computador**   Nesta configuração, o servidor de Acesso para Cliente é usado para o fluxo de emails de entrada. O email flui do Conector de envio no serviço de Transporte do servidor de Transporte de Borda para o Conector de recebimento padrão no serviço de Transporte de front-end do servidor de Acesso para Cliente e, então, para o serviço de Transporte do servidor de Caixa de Correio.

  - **Servidor de Caixa de Correio e servidor de Acesso para Cliente instalados em computadores diferentes**   Nesta configuração, o servidor de Acesso para Cliente é ignorado pelo fluxo de emails de entrada. Os emails fluem do Conector de envio no serviço de Transporte do servidor de Transporte de Borda para o Conector de recebimento padrão no serviço de Transporte do servidor de Caixa de Correio.

Se você tiver um servidor de Transporte do Borda do Exchange 2007 ou do Exchange 2010 na rede de perímetro, o fluxo de emails de entrada e de saída sempre ocorrerá diretamente entre o servidor de Transporte de Borda e o servidor de Caixa de Correio. O servidor de Acesso para Cliente não é usado.

Voltar ao início

