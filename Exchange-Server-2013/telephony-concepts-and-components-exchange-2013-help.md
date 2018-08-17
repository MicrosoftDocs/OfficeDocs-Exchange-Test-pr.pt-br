---
title: 'Componentes e conceitos de telefonia: Exchange 2013 Help'
TOCTitle: Componentes e conceitos de telefonia
ms:assetid: ce70bf6a-db85-411b-8b93-2987703963a9
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Bb124606(v=EXCHG.150)
ms:contentKeyID: 54651983
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Componentes e conceitos de telefonia

 

_**Aplica-se a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Tópico modificado em:** 2013-04-25_

Se você estiver planejando e implantando MicrosoftExchange 2013 Unificação de mensagens (UM) em sua rede, é preciso entender as redes de Unificação de mensagens e telefonia. Este tópico fornece uma visão geral de telefonia conceitos de infraestrutura e componentes que ajudarão você a planejar e implantar servidores que executam Exchange 2013 Unificação de mensagens.

**Sumário**

Visão geral

Conceitos e componentes

Redes telefônicas comutadas

Redes de comutação de pacotes

PBX

PBX IP

PBX habilitado para SIP

VoIP

Gateways IP

## Visão geral

Nas versões do Microsoft Exchange antes de Exchange Server 2007, principal responsabilidade Exchange do administrador foi gerenciar mensagens de email e, às vezes, gerenciando uma infraestrutura de rede. Versões anteriores do Exchange não têm recursos de Unificação de mensagens. os administradores Exchange Server versão 5.5, Exchange 2000 Server e Exchange Server 2003 voltadas para o ambiente de Exchange e a infraestrutura de rede e se baseavam intensamente em consultores de telefonia para gerenciar o seu ambiente de telefonia e infra-estrutura.

## Conceitos e componentes

Para implantar a Unificação de mensagens no Exchange 2013, você deve ter uma boa compreensão dos conceitos de telefonia básica e componentes de telefonia. Depois de você obter uma boa compreensão de Noções básicas de telefonia, você pode integrar com êxito Exchange 2013 Unificação de mensagens em uma organização Exchange 2013. Componentes e conceitos básicos incluem o seguinte:

  - Redes comutadas e comutação de pacotes

  - PBX (Central Privada de Comutação Telefônica)

  - PBX IP

  - Voice over Internet Protocol (VoIP)

  - Gateways VoIP

## Redes telefônicas comutadas

Em redes telefônicas comutadas, como a comutação telefônica PSTN (rede pública), várias chamadas são transmitidas entre o mesmo meio de transmissão. Frequentemente, a mídia usada no PSTN é cobre. No entanto, cabo de fibra óptica também pode ser usado.

Uma rede baseada em circuitos comutados é uma rede em que existe uma conexão dedicada. Uma conexão dedicada é um circuito ou o canal configurar entre dois nós para que eles possam se comunicar. Depois que uma chamada é estabelecida entre dois nós, a conexão pode ser usada somente por esses dois nós. Quando a chamada é encerrada por um de nós, a conexão será cancelada.


> [!NOTE]
> A PSTN é um agrupamento das redes públicas mundiais de telefone de comutação de circuitos. Esse agrupamento assemelha-se à Internet, que é um agrupamento das redes públicas mundiais de comutação de pacotes baseada em IP.



Existem dois tipos básicos de redes telefônicas comutadas: analógicas e digitais. Analógico foi projetado para transmissão de voz. Por muitos anos, estava apenas PSTN analógico, mas hoje em dia, redes baseadas no circuito como PSTN deixaram de analógico para digital. Para dar suporte a um voz analógicos transmissão sinalizam por uma rede digital, o sinal de transmissão analógico deve ser codificado ou convertido em formato digital antes que ele entre a telefonia WAN. Na extremidade de recepção da conexão, o sinal digital deve ser decodificado ou convertido de volta em um formato de sinal analógico.

Há vantagens e desvantagens para redes telefônicas comutadas. Redes telefônicas comutadas tem várias desvantagens. Redes telefônicas comutadas podem ser relativamente ineficientes, porque a largura de banda pode ser perdida. Isso não é o caso quando VoIP for usado em uma rede de comutação de pacotes. VoIP compartilha a largura de banda disponível com todos os outros aplicativos de rede e faz uso mais eficiente de largura de banda disponível. Redes telefônicas comutadas outra desvantagem é que você precisa provisão para o número máximo de chamadas telefônicas que serão necessários para os horários de pico de uso e pagando o uso do circuito ou circuitos para suportar o número máximo de chamadas.

Comutação por circuito tem uma grande vantagem sobre redes de comutação de pacotes. Em uma rede baseada em circuitos comutados, quando você usa um circuito, você tem o circuito completo para o tempo que você está usando o circuito sem concorrência de outros usuários. Isso não é o caso com redes de comutação de pacotes.


> [!NOTE]
> Síncrono Digital Hierarchy (SDH) tornou-se o protocolo de transmissão primário para a maioria das redes PSTN. SDH é realizada através de redes de fibra óptica.



Voltar ao início

## Redes de comutação de pacotes

Comutação de pacotes é uma técnica que divide uma mensagem de dados em unidades menores, chamadas de pacotes. Os pacotes são enviados ao seu destino pela melhor rota disponível e, em seguida, eles são reorganizados na extremidade de recepção.

Em redes de comutação de pacotes, como a Internet, pacotes são roteados para seu destino por meio da rota mais apropriada, mas não todos os pacotes entre dois hosts em viagem viajam da mesma rota, mesmo aqueles partir de uma única mensagem. Isso quase garante que os pacotes chegará em momentos diferentes e fora de ordem. Em uma rede de comutação de pacotes, pacotes (mensagens ou fragmentos de mensagens) são roteados individualmente entre os nós links de dados que podem ser compartilhados por outros nós. Com comutação de pacotes, ao contrário de alternar de circuito, várias conexões a nós na rede compartilham a largura de banda disponível.


> [!NOTE]
> Com a alternância circuito, todos os pacotes vá para o receptor em ordem e um único caminho.



Redes de comutação de pacotes existirem para habilitar a comunicação de dados na Internet em todo o mundo. Uma rede pública de dados ou comutação de pacotes é o equivalente de dados para o PSTN.

Redes de comutação de pacotes também são encontradas em ambientes de rede tais como LAN e WAN redes. Um ambiente WAN de comutação de pacotes se baseia em circuitos telefônicos, mas os circuitos são organizados para que elas mantenham uma conexão permanente com seu ponto de extremidade. Em um ambiente de comutação de pacotes de LAN, tais como uma rede Ethernet, a transmissão de pacotes de dados se baseia em pacotes comutadores, roteadores e cabos da LAN. Em uma LAN, a opção estabelece uma conexão entre dois segmentos de tempo suficiente para enviar o pacote atual. Pacotes de entrada são salvas em uma área de memória temporária ou no buffer na memória. Em uma LAN Ethernet-based, um quadro de Ethernet contém a parte de carga ou dados do pacote e um cabeçalho especial que inclui as informações de endereço (MAC) do controle de acesso mídia para a origem e destino do pacote. Quando os pacotes chegam ao seu destino, eles são devolvidos na ordem por assembler um pacote. Assembler um pacote é necessário devido às rotas diferentes que levam os pacotes.

Rede de comutação de pacotes possibilitou para a Internet existam e, ao mesmo tempo, fez redes de dados — redes IP especialmente baseado em LAN — vasta e mais disponível.

Voltar ao início

## PBX

Um PBX herdado é um dispositivo de telefonia que atua como um comutador para alternar entre as chamadas em uma rede baseada em circuitos comutados ou de telefonia.


> [!NOTE]
> Um PBX herdado é um sistema PBX que não é possível passar pacotes IP. Em muitas empresas, PBXs herdados foram substituídos por PBXs IP.



Um PBX é um dispositivo de telefonia usado pelas empresas mais médias e tamanho maior. Um PBX permite que os usuários ou assinantes do PBX para compartilhar um determinado número de linhas externas para fazer chamadas telefônicas consideradas externas ao PBX. Um PBX é uma solução muito mais barata que oferecendo cada usuário em uma empresa uma linha telefônica externo dedicado. Conjuntos de telefone, além para muitos outros dispositivos de comunicação, modems e máquinas de fax podem ser conectados a um PBX.

O equipamento de PBX normalmente está instalado no local de uma empresa e os conecta chamadas entre os telefones localizado e instalado no site de negócios. Um número limitado de linhas externas, também conhecido como linhas de tronco, está normalmente disponível para fazer e receber chamadas externas para os negócios de uma fonte externa, como a PSTN.

Chamadas de negócios internos feitas para números de telefone externo usando um sistema PBX são feitas por discar 9 ou 0 alguns sistemas seguidos do número externo. Uma linha de tronco a saída será selecionada automaticamente para completar a chamada. Por outro lado, as chamadas feitas entre usuários dentro da empresa normalmente não exigem dígitos de discagem especiais ou o uso de uma linha externa do tronco. Isso ocorre porque as chamadas internas são roteadas ou comutadas pelo PBX entre telefones fisicamente conectado ao PBX.

Em empresas de médio porte e tamanho maior, as seguintes configurações de PBX são possíveis:

  - Um PBX único que ofereça suporte a empresa inteira.

  - Um agrupamento de dois ou mais PBXs não ou na rede conectados entre si.

  - Um agrupamento de dois ou mais PBXs conectados juntos ou em rede.


> [!NOTE]
> Um plano de discagem UM Exchange 2013 pode abranger mais de um PBX ou PBX IP.



Voltar ao início

## PBX IP

Um PBX IP é um sistema PBX que oferece suporte ao protocolo IP para estabelecer uma conexão usando uma LAN Ethernet ou comutação de pacotes de telefones e envia suas conversas com voz nos pacotes IP. Um PBX IP híbrido oferece suporte ao protocolo IP para enviar as conversas com voz em pacotes, mas também se conecta tradicional analógicas e digitais comutadas Multiplex de divisão de tempo (TDM) telefones. Um PBX IP é equipamento reside em uma empresa privada, em vez da companhia telefônica de comutação telefônica.

PBXs IP são freqüentemente mais fácil de administrar que PBXs herdados, pois os administradores podem facilmente configurar seus serviços de PBX IP usando um navegador da Internet ou outro utilitário com base em IP. Além disso, nenhum fiação adicional, cabeamento ou painéis de patch devem ser instalados. Com um PBX IP, mover um telefone com base em IP é tão simple quanto desconectando um telefone e conectá-lo em um novo local, em vez das chamadas de serviço dispendiosa para mover um telefone de fornecedores de PBX herdados. Além disso, as empresas que possuem um IP-PBX não têm os custos de infraestrutura adicional necessários para manter e gerenciar as duas separada baseada em circuitos comutados e redes de comutação de pacotes.

## PBXs habilitados para SIP

Um PBX habilitado para SIP é um dispositivo de telefonia que atua como comutador de rede para transferir chamadas em uma rede de telefonia ou de comutação de circuitos. Entretanto, a diferença entre um PBX habilitado para SIP e um PBX tradicional é que o PBX habilitado para SIP pode se conectar à Internet e usar o protocolo SIP para fazer chamadas pela Internet.

PBXs habilitados para SIP usam um formato para chamadas que inclui um URI do SIP contendo um número e. 164 global e o "usuário = telefone" parâmetro. Por exemplo: sip:+14255551234@contoso.com;user=phone

O número de E164 começa com um prefixo "+" e não contém um parâmetro de contexto de telefone ou qualquer separadores. Suportam a PBXs habilitados para SIP TCP e UDP. UDP ainda é muito usada com sistemas herdados. PBXs habilitados para SIP também suportam Mutual Transport Layer Security (TLS mútuo) e pesquisas DNS.

## VoIP

Voice over Internet Protocol (VoIP) é uma tecnologia que contém o hardware e software que permite que as pessoas usar uma rede baseada em IP como o meio de transmissão para chamadas telefônicas. No VoIP, dados de voz serão enviados em pacotes usando IP, em vez de transmissões de circuito tradicional ou as linhas telefônicas comutadas de PSTN. Um gateway de VoIP que você se conectar à sua rede IP usa protocolos VoIP para enviar pacotes de dados entre os servidores de acesso para cliente e caixa de correio de Exchange 2013 e um sistema PBX de voz.

## Gateways VoIP

Um gateway VoIP é um dispositivo de hardware de terceiros ou o produto que se conecta a um PBX herdado à sua rede local. O gateway VoIP permite que o sistema PBX se comunicar com seu Exchange 2013 caixa de correio e servidores de acesso para cliente executando a Unificação de mensagens do Microsoft Exchange e serviços de Unificação de mensagens de chamada roteador.


> [!NOTE]
> O gateway de VoIP também pode se conectar aos sistemas de PBX que usam o VoIP em vez de protocolos comutadas de PSTN.



Exchange 2013 A Unificação de mensagens depende de capacidades do gateway VoIP para traduzir ou converter TDM ou de telefonia baseada em circuitos comutados com base protocolos, como ISDN e QSIG de um PBX a protocolos baseado em VoIP ou IP como protocolo de iniciadas de sessão (SIP), protocolo de transporte em tempo real (RTP) ou t. 38 para transporte de fax em tempo real. O gateway de VoIP é integral para a funcionalidade e a operação da Unificação de mensagens.


> [!IMPORTANT]
> Depois de instalar o gateway de VoIP, IP PBX ou PBX com SIP habilitado, você deve criar um gateway IP de UM para representar o dispositivo físico. Depois de criar um gateway IP de UM, os servidores de acesso para cliente e caixa de correio vinculados com o gateway IP de UM enviará uma solicitação SIP OPTIONS para o gateway VoIP, IP PBX ou PBX com SIP habilitado para garantir que o dispositivo está respondendo de forma. Se o gateway VoIP não responder à solicitação de opções do SIP do servidor de caixa de correio, o servidor de caixa de correio registrará um evento com ID 1088 informando que a solicitação falhou. Para resolver esse problema, certifique-se de que o gateway de VoIP, IP PBX, ou está disponível e online e se a configuração da Unificação de mensagens no servidor de acesso para cliente e de caixa de correio está correta.



Para obter mais informações sobre configurações de PBX e IP PBX, consulte [Configurações de PBX e IP PBX](pbx-and-ip-pbx-configurations-exchange-2013-help.md).

Voltar ao início

## Para obter mais informações

[Serviços, portas e protocolos de Unificação de mensagens](um-protocols-ports-and-services-exchange-2013-help.md)

[Supervisor de telefonia para o Exchange 2013](telephony-advisor-for-exchange-2013-exchange-2013-help.md)

