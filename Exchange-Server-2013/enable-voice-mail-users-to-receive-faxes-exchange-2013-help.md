---
title: 'Permitir que os usuários de email de voz receber faxes: Exchange 2013 Help'
TOCTitle: Permitir que os usuários de email de voz receber faxes
ms:assetid: 451ab0ea-21e1-4c1f-ae62-4ba7cdfd1e4d
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Bb232022(v=EXCHG.150)
ms:contentKeyID: 52058830
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Permitir que os usuários de email de voz receber faxes

 

_**Aplica-se a:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Tópico modificado em:**2015-04-07_

Microsoft Exchange Unified Messaging (UM) permite que mensagens de caixa postal ao ser entregue à caixa de correio do usuário e também permite que os usuários receber faxes em suas caixas de correio. Em UM, um fax é enviado à caixa de correio do usuário, como uma mensagem de email que tenha um arquivo de imagem com uma extensão. tif anexada. O usuário pode abrir o arquivo anexado usando um aplicativo de software que pode abrir e exibir os arquivos de imagem que tenham uma extensão. tif. Este tópico aborda o envio de fax e como ele funciona em Unificação de mensagens.


> [!TIP]
> Embora a Unificação de mensagens não permitir que usuários envie faxes de saída, várias soluções de terceiros, como um serviço de fax da Internet, um email, serviço ou um aplicativo de servidor de fax de terceiros, de envio de fax pode ser usado para enviar o faxes de entrada.



**Sumário**

Visão geral do envio de fax

Métodos de envio de fax

T.38

Visão geral do envio de fax pela Unificação de mensagens

Receba faxes de entrada

Métodos de referência de chamada de fax

Configurando o envio de fax

Números de telefone e o envio de fax

Mensagens de fax de Unificação de mensagens de registro no diário

## Visão geral do envio de fax

Fax é uma abreviação de fax word. É uma tecnologia que é usada para transferir eletronicamente documentos. Geralmente, aparelhos de fax são enviados e recebidos pelo aparelhos de fax ou modems de fax do computador usando a comutação telefônica PSTN (rede pública), que é uma rede baseada no circuito ou telefonia. No entanto, outras opções podem ser usadas para enviar e receber faxes.

Atualmente, a maioria das organizações desejam seus usuários sejam capazes de enviar e receber faxes. Organizações usam um ou mais dos métodos descritos na lista a seguir para enviar ou receber faxes no PSTN ou pela Internet. Há vantagens e desvantagens de cada um desses métodos.

  - Aparelhos de fax tradicional e envio de fax baseados no computador

  - Envio de fax usando servidores de fax ou gateways de fax

  - Envio de fax usando uma voz pela rede IP (VoIP)

  - Envio de fax usando um aplicativo de cliente de email

Para enviar uma mensagem de fax, os usuários em uma organização podem ter que fazer o seguinte:

  - Imprima uma cópia do documento enviado por fax e usar um aparelho de fax físico para enviá-la.

  - Salvar o documento no seu computador e usar um fax modem para enviar o fax, mas isso requer uma linha telefônica conectada ao computador.

  - Use um serviço de fax da Internet que permite a um documento a partir de um aplicativo de software específica do fornecedor de fax.

  - Envie um fax de saída para um servidor de fax usando um aplicativo de software que está configurado para usar o servidor de fax.

Para receber um fax, os usuários em uma organização podem ter que fazer o seguinte:

  - Receba um fax em um aparelho de fax físico dentro da organização.

  - Receba um fax usando um fax modem que está instalado no seu computador.

  - Receba um fax de uma serviço de fax da Internet.

  - Receba um fax de um servidor de fax está configurado em uma rede.

  - Receba um fax de servidor de um parceiro de fax que usa a Unificação de mensagens para entregar o fax usando uma rede VoIP.

Voltar ao início

## Métodos de envio de fax

Há várias opções para envio e recebimento de faxes, incluindo o seguinte:

**Aparelhos de fax tradicional e envio de fax baseados no computador**   Um scanner, um fax modem em um computador, uma impressora com recursos de fax internos ou um aparelho de fax dedicado pode ser usado para enviar e receber faxes. Todos esses podem ser usados para transmitir dados na forma de pulsos usando uma linha telefônica para outro dispositivo de fax, geralmente outro aparelho de fax ou computador que tenha um fax modem. Em seguida, o pulsa é transformado em imagens ou usado para imprimir a imagem em papel.

O método de fax tradicional requer pelo menos uma linha de telefone único no dispositivo de envio e recebimento e apenas um fax pode ser enviado ou recebido por vez. Uma desvantagem de envio e recebimento de faxes usando um fax modem é que o computador deve ser ativado e execução de software de fax ou um serviço de fax. Esse tipo de envio de fax baseados no computador não usa a Internet para enviar ou receber faxes.

**Envio de fax tradicional e baseados no computador**

![Envio de Fax Tradicional](images/Bb232022.7bdc1cab-9504-4314-a6e0-eccdfe2a9cd6(EXCHG.150).gif "Envio de Fax Tradicional")

**Servidores de fax ou gateways e serviços de fax da Internet**   Há várias maneiras de enviar e receber faxes pela Internet. Eles incluem usando um aplicativo de software em um computador ou usando um cliente de email para receber faxes. Na maioria dos casos, esse tipo de envio de fax envolve o uso de um servidor de fax ou gateway de fax para converter entre faxes e email. Esse método se tornou cada vez mais popular pois permite que as organizações a remover ou evitar a compra de aparelhos de fax adicionais. Ele também elimina a necessidade de instalar linhas telefônicas adicionais. Esse tipo de envio de fax envolve a criação de um documento, incluindo uma página de rosto de fax com as informações de identificação corretas e, em seguida, enviar o documento para um aparelho de fax tradicional. Por exemplo, o usuário usa um aplicativo de software, como Microsoft Word ou Microsoft Outlook para criar e enviar o fax para o servidor de fax ou gateway. O servidor de fax ou gateway recebe o fax e depois enviá-la usando uma linha telefônica tradicional para um aparelho de fax ou um fax modem que está instalado em um computador.

**Envio de fax por meio de gateways ou servidores de fax**

![Envio de fax com servidores/gateways](images/Bb232022.d6fa2402-b4ca-4313-956c-62e5fe7731ad(EXCHG.150).gif "Envio de fax com servidores/gateways")

Serviços de fax da Internet permitem que um usuário envie faxes de um computador usando a Internet. Um aplicativo de software, como Word ou Outlook pode ser usado para criar e enviar o fax para um serviço de fax da Internet. Muitas empresas oferecem serviços de fax da Internet por assinatura ou pela alteração para cada mensagem de fax é enviada. Serviços de fax da Internet oferecem as seguintes vantagens:

  - Nenhum aparelho de fax é necessário.

  - Nenhum hardware ou software deve ser instalado.

  - Nenhuma linha telefônica dedicado é necessária.

  - Confidencialidade.

  - Vários faxes podem ser enviados ao mesmo tempo.

  - Faxes podem ser recebidos quando o computador está desativado.

A figura a seguir mostra como os serviços de fax da Internet podem ser usados para enviar e receber faxes.

**Serviços de fax da Internet**

![Serviços de Fax pela Internet](images/Bb232022.5d0fb3d6-95f4-4fbf-80e5-64f5de553e65(EXCHG.150).gif "Serviços de Fax pela Internet")

**Usando aparelhos de fax, usando um aplicativo de cliente de email**   Faxes podem ser enviados e recebidos por um aparelho de fax pela Internet e, em seguida, recebidos por um cliente de email como Outlook.

O protocolo T.37 foi projetado para habilitar um aparelho de fax enviar mensagens de fax pela Internet para um cliente de email. Os faxes são enviados pela Internet como anexos de email, normalmente como arquivos. tif ou. PDF. Esse tipo de envio de fax, um aparelho de fax com suporte a iFax ou T.37 será necessário, além de um endereço de email para as máquinas de fax de envio e recebimento. Para trabalhar com aparelhos de fax tradicional e fax modems, todos os aparelhos de fax T.37 suportam para envio de fax padrão por meio de uma linha telefônica. No entanto, em alguns casos, aparelhos de fax T.37 podem ser usados quando um gateway de fax também está sendo usado. A figura a seguir mostra como T.37-based aparelhos de fax e clientes de email podem ser usados para enviar e receber faxes.

**Envio de fax com email**

![Envio de fax com email](images/Bb232022.086f086b-dc39-4439-a694-7a98e03e65d1(EXCHG.150).gif "Envio de fax com email")

**Usando aparelhos de fax, usando uma rede VoIP**   O VoIP é uma tecnologia que fornece o hardware e software que permite que as pessoas usar uma rede baseada em IP como o meio de transmissão para chamadas telefônicas. Em uma rede VoIP, os dados de voz e fax são enviados em pacotes usando IP em vez de transmissões de circuito tradicional ou as linhas telefônicas comutadas de PSTN. Um gateway de VoIP que você se conectar à sua rede IP usa VoIP para enviar pacotes de dados entre um servidor de acesso para cliente que executa o serviço Microsoft Exchange Unified Messaging roteador de chamada e um servidor de caixa de correio executando o serviço de Unificação de mensagens do Microsoft Exchange e um sistema de Private Branch eXchange (PBX) de voz. Você também pode usar um PBX IP para executar as funções de um gateway VoIP e um PBX.

Há dois tipos básicos de redes: baseada em circuitos comutados e comutação de pacotes. Uma rede baseada em circuitos comutados é uma rede em que existe uma conexão dedicada. Uma conexão dedicada é um circuito ou o canal que está configurado entre dois nós para que eles possam se comunicar. Depois que uma chamada é estabelecida entre dois nós, a conexão pode ser usada somente por esses dois nós. Quando a chamada é encerrada por um de nós, a conexão será cancelada. Em redes telefônicas comutadas, como a PSTN, várias chamadas são transmitidas entre o mesmo meio de transmissão. Frequentemente, o meio que é usado em PSTN é cobre. No entanto, cabo de fibra óptica também pode ser usado.

Em redes de comutação de pacotes, como a Internet ou em uma rede local (LAN), pacotes são roteados para seu destino por meio da rota mais apropriada, mas não todos os pacotes entre dois hosts em viagem viajam da mesma rota, mesmo aqueles partir de uma única mensagem. Isso quase garante que os pacotes chegará em momentos diferentes e fora de ordem. Em uma rede de comutação de pacotes, pacotes (mensagens ou fragmentos de mensagens) são roteados individualmente entre os nós links de dados que podem ser compartilhados por outros nós. Com comutação de pacotes, ao contrário de alternar de circuito, várias conexões a nós na rede compartilham a largura de banda disponível. Rede de comutação de pacotes possibilitou para a Internet existam e, ao mesmo tempo, fez redes de dados — redes IP e VoIP especialmente baseadas em LAN — vasta e mais disponível.

Voltar ao início

## T.38

T. 38 é um padrão de fax e protocolo que permite o envio de fax através de uma rede baseada em IP. Uma rede baseada em IP, que usa o protocolo t. 38 usa Simple Mail Transfer Protocol (SMTP) e email extensão MIME (Multipurpose Internet) para enviar uma mensagem para a caixa de correio do destinatário. T. 38 permite transmissões de fax IP para gateways de fax e dispositivos de fax habilitados para IP. Os dispositivos podem incluir hosts baseados em rede IP, como computadores cliente e impressoras. No Exchange Unified Messaging, as imagens de fax são documentos separados codificadas como arquivos. tif e anexado a uma mensagem de email. A mensagem de email e o anexo de arquivo. tif são enviadas à caixa de correio do usuário habilitado para UM.

A Unificação de mensagens depende de capacidades do gateway para converter ou converter Multiplex de divisão de tempo (TDM) ou para protocolos de telefonia baseada em circuitos comutados com base em como Integrated Services Digital Network (ISDN) e QSIG de um PBX para protocolos, baseado em VoIP ou IP como protocolo de iniciação de sessão (SIP), Real-time Transport Protocol (RTP) ou t. 38 para receber mensagens de fax. O gateway de VoIP é integral para a funcionalidade e a operação da Unificação de mensagens. O gateway VoIP é responsável por detecção tons de fax. Servidores de acesso para cliente e caixa de correio contam com o gateway VoIP para enviar uma notificação que foi detectado um fax. Em seguida, os servidores de acesso para cliente e caixa de correio serão renegociar a sessão de mídia e usar o protocolo t. 38.

Voltar ao início

## Visão geral do envio de fax pela Unificação de mensagens

Na Unificação de mensagens, o usuário recebe as imagens de fax como documentos separados codificados como arquivos de imagem. tif que estejam anexados a uma mensagem de email. A mensagem de email e o anexo. tif são enviadas à caixa de correio do usuário habilitado para UM.

Há diversas vantagens em enviar uma mensagem de fax a caixa de correio do usuário. Essas vantagens incluem o seguinte:

  - Você pode reduzir o número de máquinas de fax físico ou tradicional.

  - O número de linhas de telefone usado para envio de fax em uma organização pode ser reduzido, pois o servidor de caixa de correio pode muitos faxes de fila e enviar cada fax quando uma das linhas telefônicas se tornar disponível.

  - Faxes que são recebidos como um arquivo de imagem. tif são melhor qualidade do que um fax tradicional. Os faxes de entrada podem ser impressas por uma impressora local ou compartilhada.

  - Faxes enviados para a caixa de correio do usuário são mais seguros, pois eles estão menos prováveis que faxes impresso pode ser retirado por alguém que não seja o destinatário.

  - Os usuários podem receber faxes sem sair da mesa.

  - Mensagens de fax são recebidas podem ser monitoradas para certificar-se de que eles atendam às diretivas de segurança de uma organização.

Uma mensagem de fax único pode ser enviada apenas para um único usuário habilitado para UM. A Unificação de mensagens não é possível encaminhar mensagens a uma lista de distribuição de fax. Se você precisar têm essa funcionalidade, você deve seguir estas etapas:

1.  Crie uma caixa de correio para atender a chamada de fax. Esse será a caixa de correio para a lista de distribuição.

2.  Habilitar Unificação de mensagens da caixa de correio de lista de distribuição.

3.  Crie uma regra para esta caixa de correio habilitada para UM. A regra será configurada para encaminhar todas as mensagens à lista de distribuição selecionada.

Voltar ao início

## Receba faxes de entrada

Recebendo um fax em uma rede VoIP difere de recebimento de fax em uma máquina de fax padrão ou por meio de um servidor de fax que está localizado em uma rede baseada em IP. Para habilitar os faxes sejam enviados e recebidos por meio de uma rede VoIP, você deve ter um gateway VoIP ou um PBX IP que suporta o protocolo t. 38 e um servidor que também dá suporte à t. 38. T. 38 permite que para transmissões de fax com base em IP hosts baseada em rede IP, por exemplo, computadores cliente, impressoras com recursos de fax internos e servidores como um servidor de caixa de correio.


> [!IMPORTANT]
> Enviar e receber faxes usando t. 38 ou g. 711 não não suportado em um ambiente onde a Unificação de mensagens e Microsoft Office Communications Server 2007 R2 ou Microsoft Lync Server são integrados.



Quando um PBX recebe uma chamada, ele encaminha a chamada para a extensão apropriada. Se não houver nenhuma resposta no número de ramal do usuário, o PBX encaminha a chamada para um gateway VoIP e o gateway encaminha a chamada para o servidor de caixa de correio apropriado. O servidor de caixa de correio determina se a chamada é uma chamada de voz ou uma chamada de fax, com base no protocolo usado para a chamada. Quando o protocolo SIP é usado, o servidor de caixa de correio processa a chamada como uma mensagem de voz. No entanto, se for usado o protocolo de t. 38 do gateway VoIP, o servidor de caixa de correio reconhece que a chamada é para um fax e processa-lo conforme descrito no parágrafo a seguir. Um servidor de caixa de correio encaminha chamadas de fax de entrada para um servidor de parceiro de fax dedicado, que então estabelece a chamada de fax com o remetente de fax e recebe o fax em nome do usuário habilitado para UM. O servidor de parceiro de fax envia o fax incluído como um anexo. tif em uma mensagem SMTP à caixa de correio do destinatário.

Quando um servidor de caixa de correio recebe um sinal de fax t. 38 entrada de um gateway VoIP, o servidor de caixa de correio consulta o diretório usando o LDAP Lightweight Directory Access Protocol () para determinar se o destinatário pretendido da chamada de fax de entrada é permitido para receber mensagens de fax de entrada e para determinar o endereço SIP do servidor de parceiro de fax. Depois que ele tenha verificado essas informações, o servidor de caixa de correio envia uma solicitação de referências de chamada de fax ao gateway VoIP ou peer SIP, que, em seguida, encaminha a solicitação de fax no servidor de parceiro de fax. Após o fax chamada tiver sido estabelecida com êxito, remetente do fax envia a mídia de fax e os dados para o servidor de parceiro de fax. Depois que o servidor de parceiro de fax recebe a mídia de fax e os dados, ele usa o SMTP para enviar uma mensagem de email para um servidor de caixa de correio. Esta mensagem contém uma imagem. tif da mensagem de fax e cabeçalhos X especiais para o destinatário pretendido.

Após o fax a mensagem é autenticada e é enviada de um servidor de parceiro de fax válido, o Assistente de caixa de correio de Unificação de mensagens no servidor de caixa de correio emite uma chamada RPC para o serviço de Unificação de mensagens do Microsoft Exchange. Isso garante que as propriedades da mensagem de fax correspondem às mensagens de fax que são criadas por um servidor de caixa de correio. Finalmente, o servidor de caixa de correio novamente envia a mensagem final do fax, que inclui o anexo. tif e mensagens de email para o fax de entrada. Em seguida, a versão concluída e formatada da mensagem fax usando MAPI RPC, é entregue para o servidor de caixa de correio que contém a caixa de correio do destinatário.

Voltar ao início

## Métodos de referência de chamada de fax

Uma chamada de fax de entrada pode ser AVISADA para uma caixa de correio server por meio do SIP reenviar INVITE do gateway VoIP ou peer SIP (gateway de mídia), notificação de CNG (tom de fax de chamada) pelo peer SIP ou detecção de CNG pelo servidor de caixa de correio. As subseções a seguir detalham a referência de chamada de fax em cada caso.

## Reenviar INVITE do SIP de mesmo nível

Uma chamada de entrada para um número piloto da Unificação de mensagens seja direcionada para Unificação de mensagens como um convite com um perfil SDP (RTP/áudio) de voz

1.  Unificação de mensagens aceita o convite e fluxos de mídia são estabelecidos. Depois que a chamada tiver sido estabelecida, transmissão de fax foi iniciada pelo chamador.

2.  O peer SIP detecta o tom de fax chamada (CNG). O peer SIP emite um INVITE novamente para o servidor de caixa de correio, desta vez, especificando um perfil de fax (t. 38 ou g. 711) do SDP.

3.  Unificação de mensagens responde OK ao convite com uma 200 que coloca o peer SIP "em espera?.

4.  Uma referência, referindo-se o ponto do SIP (CNG) a um ponto de extremidade em solução fax parceiro, obtido de seus dados de configuração de problemas de Unificação de mensagens.

5.  O peer SIP envia a sessão de fax CONVIDAR para a solução de parceiro de fax.

6.  A solução de parceiro de fax aceita o convite e uma sessão de mídia é estabelecida com o peer SIP.

## Notificação de CNG por um peer SIP

Uma chamada de entrada para um número piloto de UM for direcionada a Unificação de mensagens como um convite com um perfil SDP (RTP/áudio) de voz.

1.  Unificação de mensagens aceita o convite e fluxos de mídia são estabelecidos. Depois que a chamada tiver sido estabelecida, transmissão de fax foi iniciada pelo chamador.

2.  O peer SIP detecta o tom de fax chamada (CNG). O peer SIP notifica o servidor de Unificação de mensagens do fax enviando uma notificação de CNG no stream RTP, compatível com RFC 4733.

3.  Unificação de mensagens responde a notificação emitindo imediatamente uma referência e consultando o peer SIP para um ponto de final de solução de parceiro de fax, obtidos de seus dados de configuração.

4.  O peer SIP envia a sessão de fax CONVIDAR para a solução de parceiro de fax.

5.  A solução de parceiro de fax aceita o convite.

6.  Uma sessão de mídia é estabelecida com o peer SIP.

## Detecção de CNG por um servidor de caixa de correio

Uma chamada de entrada para um número piloto de UM for direcionada a Unificação de mensagens como um convite com um perfil SDP (RTP/áudio) de voz. Unificação de mensagens aceita o convite e fluxos de mídia são estabelecidos.

1.  Depois que a chamada tiver sido estabelecida, transmissão de fax foi iniciada pelo chamador.

2.  O servidor de caixa de correio detecta o tom de fax (CNG) no fluxo de áudio RTP.

3.  Unificação de mensagens responde a notificação emitindo imediatamente uma referência e consultando o peer SIP para um ponto de final de solução de parceiro de fax, obtidos de seus dados de configuração.

4.  O peer SIP envia a sessão de fax CONVIDAR para a solução de parceiro de fax.

5.  A solução de parceiro de fax aceita o convite.

6.  Uma sessão de mídia é estabelecida com o peer SIP.

Voltar ao início

## Configurando o envio de fax

Por padrão, quando você instala o servidor de caixa de correio, o servidor não está configurado para permitir chamadas de fax de entrada para serem processadas ou entregues a um usuário habilitado para UM. Para configurar a Unificação de mensagens com um servidor parceiro de fax, você deve configurar a política de caixa de correio de Unificação de mensagens e configurar a autenticação entre o servidor de caixa de correio e o servidor de parceiro de fax. Para obter mais informações, consulte [Configurando o envio de fax de entrada](setting-up-incoming-faxing-exchange-2013-help.md).

Voltar ao início

## Números de telefone e o envio de fax

Unificação de mensagens do Exchange oferece as seguintes opções quando você estiver configurando usuários habilitados para receber mensagens de fax:

  - Um número de telefone de discagem DID (direta) para um usuário individual que é usado para aparelhos de fax e caixa postal.

  - Um número de telefone DID separado para um usuário individual que é usado para receber faxes.

  - Central de fax número de telefone para todos os usuários que recebe todos os aparelhos de fax.

## Um único número de telefone DID

Quando você habilita um usuário para Unificação de mensagens usando a página de **correio de habilitar UM** ou o cmdlet **Enable-UMMailbox** , você deve especificar pelo menos um número de ramal único para o usuário. Este número de ramal está habilitado em uma base por usuário e deve ser exclusivo dentro de um plano de discagem específico. A extensão é usada pela Unificação de mensagens para localizar o usuário correto e enviar mensagens de voz e fax à caixa de correio do usuário. Para obter mais informações, consulte [Enable-UMMailbox](https://technet.microsoft.com/pt-br/library/aa998033\(v=exchg.150\)).

Usando um único número DID, você pode configurar para que um usuário usa um único número DID para voz e fax de envio de fax. Essa configuração é fácil de administrar e não gastar outros números DID. Se o usuário estiver ausente ou no telefone quando chega uma chamada de fax, UM atende a chamada, detecta o tom de fax, cria a mensagem de fax e enviá-la ao usuário.

Se tiver um usuário cujo envio de fax é configurado por meio de um único número de telefone recebe uma chamada de um aparelho de fax quando eles não estejam ausente ou no telefone, eles podem:

  - Não atender o telefone quando ele toca para que a chamada de fax será encaminhada e respondida por um servidor de caixa de correio e a mensagem de fax será criado e encaminhado para a caixa de correio do usuário.

  - Atender a chamada de fax e, em seguida, transferi-la para si mesmo ou por conta própria para que a chamada será encaminhada e atendida por um servidor de caixa de correio e a mensagem de fax será criada e encaminhada para a caixa de correio do usuário.

  - Aguarde até que o chamador repetir o envio de fax e permitir que a chamada de fax seja transferida para um servidor de caixa de correio.

Em resumo, usar um único número DID requer que o usuário realizar ações adicionais para poder receber mensagens de fax.

Voltar ao início

## Vários números de telefone DID

Quando você habilita um usuário para Unificação de mensagens, você deve inserir pelo menos um número de ramal único para esse usuário. Você pode adicionar vários números de ramal para um usuário habilitado para Unificação de mensagens usando o Centro de administração do Exchange (EAC). Para obter mais informações, consulte [Adicionar um número de ramal](add-an-extension-number-exchange-2013-help.md).

Adicionar vários números de ramal é útil quando um usuário habilitado para Unificação de mensagens:

  - Receber faxes muitos.

  - Não deseja ser incomodado com atender o telefone para receber fax.

  - Não querer ouvir um tom de fax quando eles atender o telefone dela.

Adição de múltiplas extensões é mais complexo que usando uma extensão única e pode exigir a definições de configuração adicionais em um sistema PBX ou um PBX IP. Para configurar vários números de ramal para um usuário habilitado, você deve ter a extensão números DID disponíveis que não estão sendo usados em sua organização. Não é uma boa idéia usar vários números de um usuário habilitado se sua organização tem um número limitado de números de ramal DID disponíveis.

Os benefícios do uso de vários números de ramal DID é que um usuário habilitado recebe chamadas de voz em um número de ramal DID e fax ligar em outro número de ramal DID. Usando separado tenha números para caixa postal e chamadas de fax é mais fácil para o usuário.

Se você configurar dois números de ramal DID para um usuário específico, os números de extensão DID podem vir de planos de discagem de Unificação de mensagens separados. Para usar os dois números DID, você pode criar um plano de discagem e usar um servidor de caixa de correio como um servidor dedicado que receberá as chamadas de fax e mensagens de fax encaminhar aos usuários. Para obter mais informações, consulte [Criar um plano de discagem de UM](create-a-um-dial-plan-exchange-2013-help.md).

Quando você estiver configurando vários números de ramal DID para usuários habilitados para Unificação de mensagens, você tem as seguintes opções:

  - **Uma extensão para fax sem Unificação de mensagens e outro para voz**   Esse tipo de configuração está habilitado em uma base por usuário e é usado quando você tem extras ou não utilizados números de ramal do DID disponíveis. Um número de ramal DID está publicado como o número da caixa postal do usuário e o outro número de extensão DID está publicado como o número de fax do usuário. Chamadas de voz que são respondidas porque o usuário não atender o telefone ou um sinal de ocupado for encontrado são encaminhadas para um servidor de caixa de correio e uma mensagem de voz é criada e enviada à caixa de correio do usuário habilitado para UM. O número do ramal pode estar conectado a um aparelho de fax ou para outro computador que tenha um fax modem. Com essa configuração, um servidor de caixa de correio não processa chamadas de fax e mensagens de fax não são enviadas à caixa de correio do usuário habilitado para UM.

  - **Uma extensão para fax e outra para voz**   Esse tipo de configuração está habilitado em uma base por usuário e pode ser usado quando a sua organização tiver vários números de ramal DID disponíveis. Nesta configuração, as duas extensão DID números que são respondidos porque ele não atender o telefone ou um sinal de ocupado for encontrado são encaminhadas para um servidor de caixa de correio, que cria uma mensagem de voz ou fax, dependendo do número de extensão DID que é chamado. Embora o usuário publica um número para voz e outro para fax, o servidor de caixa de correio detecta o tipo de chamada que está sendo recebido no número DID extensão e pode criar uma mensagem de voz ou fax de chamadas a qualquer um dos números de extensão DID. Isso é muito útil quando um usuário não tem um computador dedicado que tem um fax modem para atender chamadas de fax de entrada ou um aparelho de fax.

  - **Um "fantasma? extensão para fax e outra para voz** esse tipo de configuração está habilitado em uma base por usuário. Ele é essencialmente o mesmo como a configuração que usa dois fez números (um para fax) e outro para voz. No entanto, nessa configuração, o número que será publicado para chamadas de fax para o usuário habilitado para UM está configurado no PBX como "fantasma? extensão. Chamadas de entrada que são recebidas neste número de ramal DID "fantasma" sempre são encaminhadas para um servidor de caixa de correio.
    
    A vantagem desse tipo de configuração é que as chamadas de fax são respondidas por um servidor de caixa de correio. Quando o telefone toca, mas não for atendido, um fax é criado e encaminhado pelo servidor de caixa de correio para a caixa de correio do usuário habilitado sem perturbar o usuário. Isso acontece automaticamente porque nenhum dispositivo de telefone ou fax é posicionado e está perto do usuário e o usuário não ouve o toque a chamada de entrada.
    
    As desvantagens desse tipo de configuração são que você deve ter as extensões DID adicionais disponíveis e você deverá configurar o PBX ou PBX IP para encaminhar a chamada para um servidor de caixa de correio.

## Número de telefone de fax central

Quando você habilita um usuário para Unificação de mensagens usando a página de **Habilitar o correio de UM** ou o cmdlet **Enable-UMMailbox** , você deve especificar pelo menos um número de ramal único para o usuário. No entanto, se você precisar configurar um número de fax central faxes de entrada, você deve configurar uma separados UM habilitado caixa de correio é usada para receber faxes de todos os.

Em algumas organizações, especialmente aquelas que receber faxes muitos cada dia, talvez você queira publicar um número de fax para toda a organização. Esse número de fax seria usado por todos os chamadores quando eles enviam faxes aos usuários na organização.

Publicar um número de fax para toda a organização permite que sua organização controlar os tipos de aparelhos de fax são recebidos pelos usuários. A vantagem dessa configuração é que ele requer apenas um único número de ramal DID ou um número de telefone externo. Além disso, ele não exige um número DID separado para envio de fax para cada usuário habilitado para UM. No entanto, ele requer um "secretary fax" ou outra pessoa distribuir os faxes de entrada aos usuários dentro da organização com base nas informações que tem incluído na página de rosto de fax ou na própria mensagem fax.


> [!TIP]
> Usando um número de fax central com reconhecimento óptico de caracteres (OCR) não está disponível no Exchange Unified Messaging. Esse tipo de configuração pode usar um número de fax central. No entanto, em vez de ser roteada para o destinatário por uma pessoa, o software de fax receberá o fax, executa o OCR e, em seguida, tenta localizar o destinatário com base nas informações na mensagem de fax ou página de rosto.



Usando um número de fax único para a organização inteira é útil nas seguintes situações:

  - Um usuário dentro da organização recebe muitos faxes em suas caixas de correio para gerenciar de forma eficaz.

  - Um usuário recebe muitos faxes de spam em suas caixas de correio.

  - Necessidades de negócios são muito complexas para garantem a criação de uma regra de transporte para aceitar os faxes de entrada e roteá-los para a caixa de correio pretendida. Isso talvez não seja prático, por exemplo, se sua organização requer que você rotear determinados os faxes para um grupo e outros faxes para outro grupo. Para obter mais informações, consulte [Regras de fluxo de emails ou de transporte](mail-flow-rules-transport-rules-in-exchange-2013-exchange-2013-help.md).

  - A filtragem de mensagens de fax usando Outlook não é eficiente.

Voltar ao início

## Mensagens de fax de Unificação de mensagens de registro no diário

Muitas organizações que implementam o registro no diário também podem usar Unificação de mensagens para consolidar o seu email, caixa postal e infraestrutura de fax. No entanto, não convém o processo de registro no diário para gerar relatórios de diário para mensagens que são gerados pela Unificação de mensagens. Nesse caso, você poderá decidir se a caixa postal do diário mensagens e mensagens de notificação de chamada perdida são manipuladas por um servidor de caixa de correio ou para ignorar a essas mensagens. Se a organização não exigir o registro no diário de notificações de chamada perdida e caixa postal, você pode reduzir o espaço em disco necessário para armazenar os relatórios de diário ignorando essas mensagens. Quando você ativar ou desativar o registro no diário de mensagens da caixa postal e mensagens de notificação de chamada perdida, sua alteração é aplicada a todos os serviços de transporte em sua organização. Para obter mais informações, consulte [Registro no Diário](journaling-exchange-2013-help.md).


> [!TIP]
> Mensagens que contêm os faxes que são gerados por um servidor de caixa de correio sempre são registradas, mesmo se você configurar uma regra de diário que especifica não para o correio de voz da Unificação de mensagens do diário e chamadas não atendidas mensagens de notificação.



Voltar ao início

