---
title: 'Configurações de PBX e IP PBX: Exchange 2013 Help'
TOCTitle: Configurações de PBX e IP PBX
ms:assetid: fb086680-6e3e-477a-a5d8-e24ca30196ee
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Bb430797(v=EXCHG.150)
ms:contentKeyID: 54651995
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configurações de PBX e IP PBX

 

_**Aplica-se a:** Exchange Server 2010 Service Pack 2 (SP2), Exchange Server 2013, Exchange Server 2016_

_**Tópico modificado em:** 2016-12-09_

Cada vez mais, as organizações estão adquirindo, instalar, e mantendo os componentes de hardware, por exemplo, Private Branch troca (PBXs) ou IP PBXs, que são necessárias para dar suporte a seus próprios sistemas de telefonia. Muitas organizações são seus próprios equipamentos de telefonia de compra e treinamento suas equipes para reduzir as despesas associadas à manutenção de seus sistemas de telefonia e como eles querem mais controle sobre os recursos de telefonia oferecem.

Para uma organização proprietário e manter sua rede de telefonia, eles devem comprar a telefonia necessária componentes de hardware. Eles também devem considerar a manutenção diária do equipamento de telefonia e o treinamento necessário para sua equipe de suporte para seu sistema de telefonia. Este tópico discute os diferentes tipos de negócios de telefonia ou sistemas organizacionais e os componentes de hardware de telefonia necessários. O tópico também oferece exemplos de diferentes tipos de configurações de telefonia.


> [!IMPORTANT]
> Recomendamos que todos os clientes que planejam implantar o Microsoft Exchange 2013 Unified Messaging Obtenha a Ajuda de um especialista de Unificação de MENSAGENS. Isso ajudará a garantir uma atualização suave de um sistema de correio de voz herdado. Aplicação uma nova implantação da Unificação de MENSAGENS ou executando uma atualização de um sistema de correio de voz existente requer conhecimento significativo sobre PBXs, IP PBXs e Unificação de mensagens. Para obter mais informações sobre quem contatar, consulte o site do <A href="https://go.microsoft.com/fwlink/p/?linkid=261951">Microsoft identifique</A>.



**Sumário**

Visão geral dos sistemas de telefonia

Configurações de PBX tradicional e herdados

Configurações de PBX IP

Identificação do participante chamada ou de chamada

## Visão geral dos sistemas de telefonia

Em redes telefônicas comutadas, como a comutação telefônica PSTN (rede pública), várias chamadas são transmitidas entre o mesmo meio de transmissão. Frequentemente, o meio que é usado em PSTN é cobre. No entanto, cabo de fibra óptica também pode ser usado.

Uma rede baseada em circuitos comutados é uma rede em que existe uma conexão dedicada. Uma conexão dedicada é um circuito ou o canal configurado entre dois nós para que eles possam se comunicar. Depois que uma chamada é estabelecida entre dois nós, a conexão pode ser usada somente por esses dois nós. Quando a chamada é encerrada por um de nós, a conexão será cancelada.

Diferentes tipos ou categorias de sistemas telefônicos encontrados em empresas e organizações incluem uma rede baseada no circuito, uma rede baseada em IP ou ambos. Cada tipo de sistema telefônico tem diferentes vantagens e desvantagens, que você precisa considerar ao planejar e implementar um sistema de telefonia.

  - **Centrex:**  Centrex é um tipo de serviço telefônico que companhias telefônicas arrendar para empresas e organizações. Um sistema tradicional de telefone Centrex elimina a necessidade de uma empresa ou organização adquirir o hardware de telefonia usado no local para dar suporte ao sistema de telefone da organização. Normalmente, sistemas Centrex são usados pelo pequenos escritórios que alugar Centrex serviços de uma companhia telefônica em uma base linha por linha e mês por mês. Sistemas de telefonia Centrex às vezes são usados por organizações maiores, mas com mais frequência são encontrados em organizações de governo, públicos e particulares. Centrex frequentemente usa linhas de telefone analógico para as conexões para uma empresa ou organização. Mas ele também pode usar circuitos T1 com um onsite demultiplexador para suportar telefones analógicos e digitais ou linhas ISDN.
    
    Em um sistema de telefonia baseada em Centrex, as centrais da companhia telefônica atua como a troca de telefone. Ele foi projetado especificamente para oferecer suporte às necessidades de uma organização. O office centrais telefônicas roteia as chamadas originadas dentro da empresa para o número de telefone interno ou externo apropriado. Centrex usa exchange de escritório central da companhia telefônica para rotear chamadas internas volta para uma extensão. Por exemplo, com Centrex, a troca de telefone ou as centrais da companhia telefônica sabe quais extensões são internas. Para que um funcionário que tem localizada dentro da rede de telefonia da organização possa discar outro funcionário na mesma rede de telefonia ou plano de discagem usando um número de ramal de quatro dígitos. Quando uma chamada é discada para o número de ramal de telefone interno, ele tem encaminhadas para o escritório de central da companhia telefônica e então roteado volta para o número do ramal que iniciou a chamada.

Uma variação de um sistema de telefonia tradicional Centrex é chamada *IP Centrex*. Em um sistema de telefone IP Centrex, a chamada será enviada por meio de uma voz sobre IP (VoIP) gateway localizado em escritório central de uma companhia telefônica ou localizado no local em um provedor de serviços. Nesse tipo de sistema telefônico, o gateway VoIP converte a chamada em pacotes de dados com base em IP que podem ser enviadas pela Internet ou por uma rede baseada no VoIP. Entretanto, se a chamada é enviada pela Internet, é normalmente outro gateway VoIP que recebe a chamada e converte a chamada de retorno para uma chamada de comutação por circuito tradicional.

As organizações que atualmente têm uma Centrex tradicional sistema telefônico in-loco precisará instalar, implantar e manter um ou mais gateways de VoIP para Unificação de mensagens funcionar corretamente. A Unificação de mensagens pode exigir que você instala, implantar e manter gateways VoIP para trabalhar com Centrex de IP. Várias variáveis determinará se você precisa de um gateway de VoIP. Essas variáveis incluem o tipo de telefones usados na sua organização (analógico, digital ou IP) e os protocolos com suporte pelo sistema Centrex de IP.

  - **Principais telefone:**  Em um sistema de telefone de chave, sede da companhia telefônica está conectado à organização usando linhas telefônicas analógicas ou digitais padrão. Um número de ramal único está conectado a vários telefones forma quando uma chamada for colocada na organização usando esse número de telefone, todos os telefones associados a esse número de linha ou extensão tocarão ao mesmo tempo.

Com sistemas telefônicos de chave, a usuários individuais compartilham a linhas em telefones. Portanto, os chamadores não experiência frequentes sinais de ocupado quando eles tentam chamá-lo em uma organização. Sistemas telefônicos chave geralmente são usados pelo pequenos escritórios onde volume de chamada interna é alto, mas o volume de chamadas externas é baixo.

Sistemas telefônicos chave tornaram mais sofisticados ao longo do tempo e podem trabalhar com a Unificação de mensagens, se um gateway VoIP for adicionado. No entanto, alguns sistemas menos sofisticados podem não funcionar, mesmo se um gateway de VoIP com suporte é usado.

  - **PBX:**  Um PBX herdado é um dispositivo de telefonia que alterna chamadas em uma rede baseada em circuitos comutados ou de telefonia. Um PBX herdado é um sistema PBX que não tem um adaptador de rede e não é possível passar pacotes IP. Porque eles não podem passar pacotes IP, algumas organizações e empresas substituíram PBXs herdados com PBXs IP. Para obter uma lista dos PBXs suportado pela Unificação de mensagens, consulte [Supervisor de telefonia para o Exchange 2013](https://docs.microsoft.com/pt-br/exchange/voice-mail-unified-messaging/telephone-system-integration-with-um/telephony-advisor-for-exchange-2013).
    
    PBXs são usados pela maioria das empresas de médio e maior porte. Um PBX permite que os usuários ou assinantes do PBX para compartilhar um determinado número de linhas externas para fazer chamadas telefônicas consideradas externas ao PBX. Um PBX é uma solução muito mais barata que oferecendo cada usuário em uma empresa uma linha telefônica externo dedicado. Telefones celulares, além de aparelhos de fax, modems e muitos outros dispositivos de comunicação, podem ser conectados a um PBX.
    
    O equipamento de PBX normalmente está instalado no local de uma organização e os conecta chamadas entre telefones localizados no local e a companhia telefônica. Um número limitado de linhas externas, também conhecido como linhas de tronco, está normalmente disponível para fazer e receber chamadas externas para os negócios de uma fonte externa, como a PSTN.
    
    Para habilitar um PBX herdado ser usado com a Unificação de mensagens, você precisará implantar um gateway VoIP aceito. Para obter uma lista de gateways de VoIP com suporte, consulte [Supervisor de telefonia para o Exchange 2013](https://docs.microsoft.com/pt-br/exchange/voice-mail-unified-messaging/telephone-system-integration-with-um/telephony-advisor-for-exchange-2013).

  - **PBX IP:**  Um PBX IP é um sistema PBX que possui um adaptador de rede que ofereça suporte ao protocolo IP. É uma parte do equipamento que geralmente reside em uma organização ou empresa, em vez de sendo localizada em um escritório de empresa telefônica de comutação telefônica. Existem dois tipos de PBXs IP: tradicional IP PBXs e PBXs IP de híbrida. Tanto tradicional IP PBXs e PBXs IP de híbrido suportam ao protocolo IP para enviar as conversas com voz nos pacotes para telefones com base em VoIP. No entanto, híbrida PBXs IP também conectar tradicionais telefones analógicos e digitais.
    
    PBXs IP são frequentemente mais fácil de administrar que PBXs herdados, pois os administradores podem configurar mais facilmente os serviços de PBX IP usando um navegador da Internet ou outra ferramenta baseada em IP. Além disso, nenhum fiação adicional, cabeamento ou painéis de patch precisa ser instalado. Com um PBX IP, você pode mover um telefone IP-based meramente retirando o telefone e conectá-lo em um novo local. Isso lhe permite evitar as chamadas de serviço dispendiosa necessárias para mover um telefone de fornecedores de PBX herdados. Além disso, as organizações que possuem um IP-PBX não precisam incorrer nos custos de infraestrutura adicional necessários para manter e gerenciar redes separadas em circuitos comutados e comutação de pacotes. Para obter uma lista de IP PBXs suportados para Unificação de mensagens, consulte [Supervisor de telefonia para o Exchange 2013](https://docs.microsoft.com/pt-br/exchange/voice-mail-unified-messaging/telephone-system-integration-with-um/telephony-advisor-for-exchange-2013).
    
    Voltar ao início

## Configurações de PBX herdadas e tradicionais

Em redes de telefonia que tenham PBXs herdados ou tradicionais, um PBX faz o seguinte:

  - Cria conexões ou circuitos entre os conjuntos de telefone de dois usuários.

  - Mantém a conexão, desde que os usuários precisam da conexão.

  - Fornece informações para fins de contabilidade (por exemplo, metros chamadas).

Além das três funções incluídas na lista anterior, PBXs podem oferecer outros recursos de chamada, como:

  - Atendedores automáticos

  - Estatísticas de chamada

  - Coleta de chamada

  - Transferência de chamada

  - Chamada em espera

  - Chamadas de conferência

  - DID (discagem direta)

  - Não incomodar (DND)

Embora existam vários fabricantes de PBXs, todos eles se encaixam duas categorias básicas: analógicas e digitais. Esses tipos de PBXs frequentemente são conhecidos como *legacy* ou *traditional* PBXs.

Normalmente, os sistemas PBX estão conectados ao escritório de central da companhia telefônica usando linhas de telefone especial, conhecidas como T1 - e -linhas E1. Linhas T1 e E1 ter vários canais. Essas linhas telefônicas são também conhecidos como *trunk lines.* permitem que o escritório central ou o PBX enviar várias chamadas na mesma linha para melhorar a eficiência usando um layout fiação simplificado. Um PBX também pode trabalhar com analógico ou linhas ISDN.

Configurando corretamente seu PBX, você pode controlar quantas canais ou linhas que você deseja configurar para receber chamadas que vêm de chamadores externos e quantos canais ou linhas dedicar às chamadas recebidas de chamadores dentro da organização. Configurar o número de linhas ou de canais ajuda a evitar que os sinais de ocupado e permite que você configure o número de canais ou linhas devotado a aplicativos como centros de chamada. Configurar corretamente seu PBX é um método econômico para gerenciar os canais ou linhas em sua organização porque ele reduz o número de linhas dedicadas necessários.

Um PBX pode rotear um número de telefone discado específicos para um telefone específico para que os usuários possam ter seu próprio número de telefone individual ou um número de ramal. Isso é conhecido como um número de discagem direta interna DID. Quando o número de telefone é discado para um usuário, a companhia telefônica envia o número DID ao PBX por meio do serviço de identificação de número discado (DNIS). Como a companhia telefônica usa DNIS para enviar o número, não há nenhuma necessidade de intervenção do operador rotear a chamada. O PBX tem as informações sobre a chamada corretamente roteá-la ao número discado pelo chamador. Para obter uma lista dos PBXs suportado pela Unificação de mensagens, consulte [Supervisor de telefonia para o Exchange 2013](https://docs.microsoft.com/pt-br/exchange/voice-mail-unified-messaging/telephone-system-integration-with-um/telephony-advisor-for-exchange-2013).

Voltar ao início

## Analógico e digitais PBXs

Analógicos PBXs enviar voz e informações de sinalização, como os tons de toque de um número de telefone discado, como um som analógico de chamadas. Portanto, o som nunca é digitalizado. Para direcionar corretamente a chamada, o PBX e o office de central da companhia telefônica tem que escutar as informações de sinalização.


> [!NOTE]
> Touchtone mais tecnicamente é conhecido como multifrequência de tom dual. Quando um chamador pressiona uma tecla no teclado de um telefone, o telefone produz tons separados dois: um tom de alta frequência e um tom de baixa frequência. Quando uma pessoa fala de telefone, somente um único tom ou frequência é emitida. Enviar dois tons com frequências diferentes ao mesmo tempo reduz a possibilidade de que os toques de sinalização serão interpretados como uma voz humana ou que uma voz humana será interpretada como os toques de sinalização.



Digitais PBXs codificar ou digitalize o som analógico, em um formato digital. Normalmente, PBXs digitais codificam os sons de voz usando um codec de áudio padrão do setor como g. 711 ou 729. Depois que a voz digitalizada é codificada, ele é enviado através de um canal usando o recurso de comutação por circuito. Configura comutação por circuito uma ponta a ponta abre a conexão. Ele deixar o canal aberto para o comprimento da chamada e para uso exclusivo do chamador. No entanto, o método de sinalização usado pelo PBX depende do fabricante. Os fabricantes de PBX podem ter seu próprios proprietário sinalização método para a configuração da chamada.


> [!NOTE]
> Digitais PBXs podem oferecer suporte a linhas de tronco analógicas e digitais.



Em organizações maiores, PBXs tornam possível para que os funcionários em locais físicos separados entre em contato com um outro discando um número de ramal de um usuário. Isso pode ser feito por meio de um PBX único ou pode envolver vários PBXs em rede juntos. PBXs em locais diferentes do office podem ser conectados a uma única rede transparente comutadas usando linhas T1 ou E1. Quando essas linhas se conectam PBXs juntos, eles são frequentemente conhecidos como *tie lines*. PBXs se comunicar umas com as outras entre as linhas de tie usando um protocolo de PBX para PBX, como QSIG. QSIG permite que um conjunto de PBXs agir como se fossem um único PBX.

Esse tipo de ambiente de PBX também pode incluir recursos avançados, como chamada transferindo e conferência por telefone. Além de permitir para recursos avançados, ter dois PBXs conectadas também pode salvar o dinheiro organização porque as tarifas de longa distância entre os funcionários em diferentes locais serão reduzidas. Isso ocorre porque uma chamada feita entre dois funcionários permanece em uma linha de tie entre PBXs e requer que o usuário discar apenas um número de ramal para o outro usuário, em vez de fazer uma chamada de longa distância.

Em um ambiente de telefonia que inclui um único ou vários PBXs analógicos ou digitais, um gateway VoIP é necessário entre o PBX e os servidores de acesso para cliente e caixa de correio de Exchange 2013 para converter os protocolos de circuito encontrados em uma rede de telefonia para os protocolos com base em IP encontrados em uma rede de dados. Para obter mais informações sobre os gateways VoIP, consulte os tópicos a seguir:

  - [Gateways IP de UM](um-ip-gateways-exchange-2013-help.md)

  - [Conectar a um gateway VoIP para se comunicar com um PBX](connect-a-voip-gateway-to-communicate-with-a-pbx-exchange-2013-help.md)

Para obter uma lista de gateways VoIP com suporte para a Unificação de mensagens, consulte [Supervisor de telefonia para o Exchange 2013](https://docs.microsoft.com/pt-br/exchange/voice-mail-unified-messaging/telephone-system-integration-with-um/telephony-advisor-for-exchange-2013).

Voltar ao início

## Configurações de IP PBX

Um PBX IP é um sistema PBX que oferece suporte ao protocolo IP para conectar telefones usando uma LAN Ethernet ou comutação de pacotes. Ele envia as conversas com voz em pacotes IP ou dados. Um PBX IP pode ter várias interfaces. Eles incluem interfaces de uma rede de dados e outros que permitem que para uma conexão com uma rede baseada em circuitos comutados ou de telefonia.

O desenvolvimento de protocolos da Internet em tempo real tornou possível com êxito enviar mensagens de voz e fax através de uma rede de dados. Esses protocolos de Internet em tempo real incluem os protocolos de VoIP usados com o Unified Messaging: Session Initiation Protocol (SIP) via protocolo TCP (Transmission Control) para mensagens de voz. Esses protocolos tornaram possível com êxito enviar mensagens de voz e fax através de uma rede de dados. Protocolos de VoIP em tempo real são necessários para enviar mensagens de voz através de uma rede de comutação de pacotes ou dados para a ordem de entrega e o intervalo de pacotes de dados possam ser mantidas e controlados. Se esses protocolos não foram usados para manter e controlar a entrega e timing os pacotes de dados, voz de uma pessoa seria desmembrado e som incoerentes ou as imagens podem aparecer com erros. Para obter uma lista de IP PBXs suportados para Unificação de mensagens, consulte [Supervisor de telefonia para o Exchange 2013](https://docs.microsoft.com/pt-br/exchange/voice-mail-unified-messaging/telephone-system-integration-with-um/telephony-advisor-for-exchange-2013).


> [!NOTE]
> Suporta do Unified Messaging apenas SIP sobre TCP.



## Configurações de IP PBX tradicionais

Um IP PBX tradicional ou padrão contém pelo menos uma interface de rede que se conecta a uma rede de dados usando os protocolos de VoIP. Ele também pode conter interfaces de rede adicionais ou outras interfaces de telefonia que habilitá-lo para se conectar a uma rede de telefonia existente, como a PSTN. A conexão com a rede de dados permite a comunicação com outros hosts de VoIP localizados na rede de dados usando os pacotes de dados IP. Esses hosts VoIP incluem outros IP PBXs, telefones com base em VoIP, gateways VoIP, acesso para cliente e servidores de caixa de correio que estão executando os serviços de Unificação de MENSAGENS. Um IP/PBX tradicional não oferece suporte a telefones analógicos ou digitais. Ele oferece suporte apenas a telefones VoIP.

Como o IP PBX já pode se conectar a uma rede de dados e pode converter os protocolos de circuito da PSTN para protocolos de VoIP de comutação de pacotes, um gateway VoIP talvez não seja necessário habilitar a comunicação com servidores de acesso para cliente e caixa de correio na rede de dados.

## Configurações híbridas de IP PBX

Híbrida IP PBXs pode fornecer recursos de analógicos, digitais e baseada em VoIP. Se as interfaces corretas são instaladas em um IP-PBX e o software que ofereça suporte a vários tipos de interfaces está instalado corretamente, IP PBX é considerado um PBX IP híbrido. Híbrido um PBX IP torna possível usar uma mistura de telefones analógicos, digitais e com base em IP.

Mais modernos IP PBXs pode suportar e fornecer a todos os três tipos de comunicação de voz ou um PBX IP tradicional podem ser atualizados para um PBX IP híbrido instalando as interfaces necessárias e atualizações de software ou firmware.

A mistura de telefones analógicos, digitais e com base em IP permite que os usuários em sua organização usar vários novos recursos e também fornece excelente flexibilidade em seu ambiente de telefonia. Usar híbrida um PBX IP também permite uma migração gradual mais para um ambiente de telefonia completamente baseados em VoIP e o sistema para sua organização de mensagens de voz.

Vários fatores determinam se um gateway VoIP serão necessário quando você se conectar aos servidores de acesso para cliente e caixa de correio. Um desses fatores é a compatibilidade dos protocolos VoIP usados pelo PBX IP ou híbrida IP PBX e Unificação de mensagens. Se um gateway VoIP não é necessário, reduzirá a complexidade da infra-estrutura de telefonia e o suporte que você deve ter para Unificação de mensagens serão mais simples.

Voltar ao início

## Identificação do participante chamado ou de chamada

Identificação do participante chamado ou de chamada é um serviço de empresa de telefone que pode informar a pessoa que está recebendo a chamada, o número de telefone e em alguns casos, o nome da pessoa que está ligando e outras informações sobre a chamada. Essas informações são enviadas por um cabo serial usando-se a sinalização de chamada. Quando uma chamada é recebida por um PBX ou PBX IP de uma companhia telefônica, a chamada inclui chamar as informações de identificação, como o seguinte:

  - Número do chamador

  - Número da parte chamada

  - Códigos de status, como um toque-sem resposta, o estado ou condição da linha, linha ocupados e encaminhar chamadas sempre

  - O número de porta ou a linha que está sendo usado para a chamada

  - Em telefonia, as informações de sinalização são usadas para troca de informações entre pontos de extremidade em uma rede para configurar, controlar e chama final. Vários métodos de sinalização usados por gateways VoIP e PBXs IP são compatíveis com a Unificação de mensagens. O método de sinalização usado depende do tipo de dispositivo que está sendo usado e o tipo de método de sinalização usado pela companhia telefônica. O fator mais importante é que o dispositivo que está se conectando a companhia telefônica e o gateway VoIP ou IP PBX deve suportar pelo menos um dos métodos a sinalização que permitem que as informações de terceiros chamado ou de chamada sejam enviados e recebidos por chamadores. Para obter mais informações sobre a sinalização de informações de configuração de um gateway de VoIP com suporte, consulte [Supervisor de telefonia para o Exchange 2013](https://docs.microsoft.com/pt-br/exchange/voice-mail-unified-messaging/telephone-system-integration-with-um/telephony-advisor-for-exchange-2013).

Embora outros métodos de sinalização podem ser usados, os dois métodos de sinalização mais populares são:

  - **Simplificado de Interface de mesa de mensagem (SMDI):**  SMDI é um protocolo que é usado para fornecer a sinalização, controle de chamadas e chamar as informações de identificação de uma interface entre um sistema telefônico e um sistema de caixa postal. Ele é usado para fornecer o sistema de caixa postal com as informações necessárias para processar uma chamada de entrada. Sempre que uma chamada de entrada é enviada por meio do SMDI em uma interface de serial ou RS-232, identificará as informações que são enviadas a linha ou porta, o tipo de chamada e os números de terceiros chamado ou de chamada. O cabo SMDI conecta-se de um dispositivo, como um PBX para uma conexão serial no gateway VoIP. No entanto, SMDI também é usado com PBXs IP. O protocolo SMDI permite um máximo de dígitos somente a 10 para cada chamada e o número chamado. Isso é uma limitação do protocolo e não pode ser alterado.

  - **Em banda:**  Sinalização em banda permite a troca de sinalização, controle de chamadas e chamar as informações de identificação de uma companhia telefônica. Essas informações são enviadas pelo canal mesmo e na mesma faixa (300 Hz a 3,4 kHz) como a voz e outros sons que estão sendo feitas durante a chamada. Por exemplo, quando um usuário faz uma chamada usando DTMF ou discagem sensível ao toque e fala para a parte chamada, a discagem por tom e a conversa com voz usam o mesmo canal e banda. Sinalização em banda é menos seguro porque os sinais de controle são expostos ao usuário e é um método de sinalização menos popular que SMDI. Sinalização em banda se aplica apenas ao canal associado sinalização (CAS).

Voltar ao início

