---
title: 'Planos de discagem de Unificação de mensagens: Exchange 2013 Help'
TOCTitle: Planos de discagem de Unificação de mensagens
ms:assetid: ed7afc03-94af-4b23-8745-6a61f203c149
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Bb125151(v=EXCHG.150)
ms:contentKeyID: 50486942
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Planos de discagem de Unificação de mensagens

 

_**Aplica-se a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Tópico modificado em:** 2013-02-21_

Planos de discagem do Unified Messaging (UM) são o principal componente da Unificação de mensagens e são necessárias para implantar com êxito a Unificação de mensagens para a caixa postal na sua rede. As seções a seguir abordam os planos de discagem de Unificação de mensagens e como elas são usadas em uma implantação da Unificação de mensagens.

## Visão geral dos planos de discagem de UM

Um plano de discagem de Unificação de mensagens representa um conjunto de Private Branch eXchanges (PBXs) ou IP PBXs que números de ramal de usuário comum do compartilhamento. Extensões de todos os usuários hospedadas no ou IP PBXs dentro de um plano de discagem contenham o mesmo número de dígitos. Os usuários podem discar extensões de telefone do outro sem como anexar um número especial para a extensão ou discando um número de telefone completo.

Um plano de discagem de UM espelha um plano de discagem de telefonia. Um plano de discagem de telefonia está configurado ou IP PBXs.

Na Unificação de Mensagens, podem existir as seguintes topologias de plano de discagem da UM:

  - Um único plano de discagem que representa um subconjunto de ramais ou todos os ramais de uma organização que tem um PBX ou IP PBX.

  - Um único plano de discagem que representa um subconjunto de ramais ou todos os ramais de uma organização que tem PBX ou IP PBXs em várias redes.

  - Vários planos de discagem que representam um subconjunto de ramais ou todos os ramais de uma organização que tem um PBX ou IP PBX.

  - Vários planos de discagem que representam um subconjunto de ramais ou todos os ramais de uma organização que tem vários PBXs ou IP PBXs.

Os usuários pertencentes ao mesmo plano de discagem têm as seguintes características:

  - Um número de ramal que identifica com exclusividade a caixa de correio do usuário no plano de discagem.

  - A capacidade de chamar ou enviar mensagens de voz para outros membros do plano de discagem usando somente o número do ramal.

Para obter mais informações sobre como habilitar um usuário para Unificação de Mensagens, consulte [Habilitar um usuário para caixa postal](enable-a-user-for-voice-mail-exchange-2013-help.md).

Planos de discagem de Unificação de mensagens são usados na Unificação de mensagens para certificar-se de que as extensões de telefone do usuário são exclusivas. Em algumas redes de telefonia, vários ou IP PBXs existirem. Essas redes de telefonia, pode haver dois usuários que têm o mesmo número de ramal. Planos de discagem de Unificação de mensagens resolver essa situação. Colocar os dois usuários em dois planos de discagem de Unificação de mensagens separados torna suas extensões exclusivo.

## Como os planos de discagem funcionam

Ao integrar uma rede de telefonia pela Unificação de mensagens, deve haver um ou mais dispositivos de hardware chamados de Voice over gateways IP (VoIP) ou PBXs IP que se conectam a sua rede de telefonia para sua pacotes com base em IP comutada de rede. Gateways VoIP converter comutadas protocolos de um PBX encontrado em uma rede de telefonia para um protocolo de comutação de dados, como o IP. IP PBXs também converter comutadas protocolos para um protocolo de comutação de dados. Controladores de borda de sessão (SBCs) permitem conectar duas redes com base em IP juntos em uma WAN pública ou privada e são encontrados na Unificação de mensagens híbrido ou implantações online. Cada gateway VoIP, IP PBX ou controlador de borda de sessão (SBC) em sua organização é representado por um gateway IP de UM. Para obter mais informações sobre gateways IP de UM, consulte [Gateways IP de UM](um-ip-gateways-exchange-2013-help.md).

A Unificação de mensagens exige que você crie pelo menos um plano de discagem de UM. Se você cria um ou mais planos de discagem, todos os servidores do Exchange na sua organização atenderá às chamadas recebidas. Também deve haver um único ou vários gateways de IP de UM associadas ao plano de discagem. No local e as implantações híbridas, depois de instalar os servidores Exchange e associar um gateway IP de UM, todos os servidores do Exchange atenderá às chamadas recebidas para todos os planos de discagem. No entanto, para o local ou híbrida implantações, quando você estiver integrando do Exchange e Lync Server, você deve criar planos de discagem URI do SIP.


> [!IMPORTANT]
> Cada vez que você criar um plano de discagem de Unificação de mensagens, uma política de caixa de correio de Unificação de mensagens padrão também é criada. A diretiva de caixa de correio de Unificação de mensagens é nomeada &lt;<EM>Dial Plan Name</EM>&gt; política padrão. Essa diretiva de caixa de correio de Unificação de mensagens pode ser excluída ou configurada de forma diferente.



Quando você cria primeiro gateway IP de UM e especifica um plano de discagem de Unificação de mensagens no momento que você criá-lo, um grupo de busca UM padrão também é criado. Criação desses componentes permite que os servidores do Exchange receber chamadas de um gateway VoIP, IP PBX ou SBC e, em seguida, processar as chamadas de entrada para os usuários que estão associados a UM plano de discagem. No local ou híbrida implantações, quando uma chamada vem para o gateway VoIP, IP PBX ou SBC, ele encaminha a chamada para um servidor de acesso para cliente. O servidor de acesso para cliente, em seguida, encaminha a chamada para um servidor de caixa de correio e o servidor de caixa de correio tenta coincidir com o número do ramal do usuário para o plano de discagem UM associado.

## Tipos de planos de discagem

Um identificador de recurso uniforme (URI) é uma cadeia de caracteres (números ou alfabético) que é usado para identificar ou nome de um recurso. Na Unificação de mensagens, o objetivo principal de um URI é permitir que os dispositivos de VoIP para se comunicar com outros dispositivos usando protocolos específicos. Um URI que define a nomeação e numeração formato ou esquema usado para a chamada e chamado contidas em um cabeçalho de protocolo de iniciação de sessão (SIP) para uma chamada de entrada ou saída de informações de terceiros.

Os tipos de planos de discagem de Unificação de mensagens, que você pode criar na Unificação de mensagens dependerá os tipos de URI suportados pelo gateways VoIP ou IP PBXs em sua organização. O tipo URI é o tipo de cadeia de caracteres que é enviada do PBX ou PBX IP. Quando você cria um plano de discagem, você deve saber os tipos específicos de URI que são suportados pelo seu ou IP PBXs. Há três formatos ou planos de discagem de tipos de URI que podem ser configurados na Unificação de mensagens:

  - Ramal do Telefone (TeleExtn)

  - URI do SIP

  - E.164

Por padrão, cada vez que você criar um plano de discagem na Unificação de mensagens, o plano de discagem será criado para usar o tipo de URI de ramal de telefone. Depois de criar um plano de discagem, não será possível alterar o tipo URI. Você deve excluir o plano de discagem existente e crie outro com o tipo URI correto.

## Tipo de URI do ramal de telefone

O tipo de URI de ramal de telefone é o tipo mais comuns do plano de discagem de Unificação de mensagens e é usado com IP PBXs e PBXs. Ao configurar um plano de discagem do telefone extensão (TelExtn), os gateways VoIP, PBXs e PBXs IP que você usa devem suportar o tipo de URI TelExtn. Atualmente, a maioria dos PBXs e PBXs IP suportam este tipo URI.

Quando uma chamada for recebida por um PBX e o usuário habilitado para Unificação de mensagens não está disponível para atender à chamada, o PBX irá encaminhar a chamada para um gateway VoIP. O gateway VoIP — ou no IP PBX, se for usado — traduzirá a chamada de um protocolo baseado em circuito para um protocolo com base em IP. No cabeçalho para o pacote SIP recebido do gateway VoIP ou IP PBX, as informações de terceiros chamada e chamada serão listadas em um dos seguintes formatos:

  - Tel:512345

  - 512345@\<*Endereço IP*\>

O formato ramal de telefone (TelExtn) usado baseia-se na configuração do gateway VoIP ou IP PBX.

## Tipo de URI SIP

Protocolo de iniciação de sessão (SIP) é um protocolo padrão para iniciar sessões de usuário interativo que envolvem multimídia elementos como vídeo, voz, chat e jogos. SIP é um protocolo de com base de solicitação-resposta que responde a solicitações de clientes e respostas de servidores. Os clientes são identificados por URIs do SIP. Solicitações podem ser enviadas por meio de qualquer protocolo de transporte, como UDP ou TCP. SIP determina o ponto de extremidade a ser usado para a sessão selecionando os parâmetros de mídia e a mídia de comunicação.

Quando você cria um novo plano de discagem, você tem a opção de criar um plano de discagem URI do SIP se seu ambiente tiver Microsoft Office Communications Server 2007 R2 ou Microsoft Lync Server implantado. Você também pode criar um plano de discagem URI do SIP, se sua organização tiver IP PBXs ou PBXs habilitados para SIP. Neste caso, a sua organização também deve suportar URIs do SIP e roteamento SIP.

Um URI do SIP é o número de telefone SIP do usuário. O URI do SIP é semelhante a um endereço de email e é gravado no seguinte formato: sip*:\<user name\>@\<domain or IP address\>*:*Port*. Quando uma habilitados para SIP IP-PBX ou PBX é usado para enviar uma chamada para os servidores do Exchange, o dispositivo enviará o URI do SIP para que a parte de chamada e de chamada no cabeçalho SIP e não incluirá números de ramal.

## Tipo de URI E.164

E. 164 é um formato de numeração padrão que define a plano usado em algumas redes de dados e de comutação telefônica PSTN (rede pública) de numeração de telecomunicação pública internacional. E. 164 define o formato dos números de telefone. Números e. 164 podem ter um máximo de 15 dígitos e são geralmente grafados com um sinal de adição (+) antes dos dígitos do número de telefone. Para discar um número de telefone e. 164 formatada de um telefone, o prefixo de chamadas internacionais apropriados deve ser incluído no número discado. Em e. 164 numeração plano para sistemas de telefonia pública, cada número atribuído contém um código de país (CC), um código de destino Nacional (NDC) e um número de assinante (SN).

Quando você cria um novo plano de discagem, você tem a opção para criar um plano de discagem e. 164. No entanto, se você cria e configurar um plano de discagem e. 164, os PBXs e PBXs IP devem suportar a roteamento e. 164. Cabeçalho SIP recebido de um gateway VoIP associado a um plano de discagem e. 164 incluirá o número de telefone e. 164 formatada e informações sobre a chamada e chamada de terceiros e será listado no seguinte formato: Tel: + 14255550123. Para implantações de Exchange Online com a Unificação de mensagens do Exchange e o Lync Server, você deve usar números de formatada corretamente e. 164 para números de atendedor automático e de Outlook Voice Access.

## Segurança VoIP

Servidores Exchange se comuniquem com gateways VoIP, IP PBXs e outros computadores do Exchange em um dos Unsecured, SIP protegido ou protegido modo, dependendo de como o plano de discagem de Unificação de mensagens é configurado. No local e híbrido implantações, acesso para cliente e servidores de caixa de correio podem operar no modo de configurar um plano de discagem porque os servidores ouvir na porta TCP 5060 para solicitações não seguras e a porta TCP 5061 para solicitações de Secured ao mesmo tempo, se eles foram configurados para iniciar no modo de duplo. Acesso para cliente e caixa de correio servidores answer tudo entrada chamadas para Unificação de mensagens de todos os planos de discagem, mas esses planos de discagem pode ter diferentes configurações de segurança de VoIP.

No local e híbrido implantações, por padrão, quando você cria um UM plano de discagem, comunicará no modo não seguro, e os servidores de acesso para cliente e caixa de correio serão enviar e receber dados de gateways VoIP, PBXs IP e SBCs sem usar criptografia. No modo não seguro, nem o canal de mídia em tempo real Transport Protocol (RTP) nem a informações de sinalização SIP é criptografada. Você pode usar o cmdlet **Get-UMDialPlan** no Shell para determinar a configuração de segurança para um plano de discagem UM específico.

No local e híbrido implantações, você pode configurar um servidor de acesso para cliente e caixa de correio para usar mutual Transport Layer Security (TLS mútuo) para criptografar o tráfego SIP e RTP enviadas e recebidas de outros dispositivos e servidores. Quando você configura o plano de discagem para usar o SIP protegido modo, apenas o tráfego será criptografado e os canais de mídia RTP ainda usará TCP, que não é criptografado de sinalização do SIP. No entanto, quando você configura o plano de discagem para usar o modo protegido, ambos os a sinalização SIP tráfego e os canais de mídia RTP são criptografadas. Um canal de mídia de sinalização criptografada que usa o protocolo de transporte em tempo real seguro (SRTP) também usa o TLS mútuo para criptografar os dados de VoIP.

Você pode configurar o modo de segurança VoIP quando você estiver criando um novo plano de discagem ou depois de criar um plano de discagem usando o EAC ou o cmdlet **Set-UMDialPlan** no Shell. Quando você configura o plano de discagem de UM para uso SIP protegido ou protegido modo, acesso para cliente e servidores de caixa de correio irá criptografar o tráfego ou os canais de mídia RTP ou ambos de sinalização do SIP. No entanto, para ser capaz de enviar dados criptografados para e dos servidores do Exchange, você deve configurar corretamente o plano de discagem e dispositivos de VoIP como gateways VoIP, PBXs IP e SBCs devem oferecer suporte a TLS mútuo.

## Outlook Voice Access

Existem dois tipos de chamadores que acessam o sistema de caixa postal usando o número do Outlook Voice Access configurado em um plano de discagem de UM: não autenticado chamadores e autenticado chamadores. Quando os chamadores discagem o número do Outlook Voice Access configurado em um plano de discagem, elas são consideradas anônimas ou não autenticados até que eles informações incluindo extensão do correio de voz e um PIN de entrada. A única opção disponível para chamadores anônimos ou não autenticados é o recurso de pesquisa de diretório. Depois que os chamadores de entrada de extensão do correio de voz e seu PIN, eles vai ser autenticados e oferecidos acesso para suas caixas de correio. Depois que elas acessem o sistema de caixa postal, estejam usando o recurso de acesso de voz do Outlook.

Outlook Acesso de voz é uma série de prompts de voz que forneça o acesso do chamador ao correio de voz, email, calendário e outras informações. Outlook Voice Access permite que os chamadores autenticados navegue suas informações pessoais em suas caixas de correio, fazer chamadas ou localizar usuários usando DTMF de tom dual (DTMF), também conhecido como discagem por tom, entradas ou entradas de voz.

## Números do Outlook Voice Access

Depois de criar um plano de discagem de UM, você precisa adicionar pelo menos um número do Outlook Voice Access. Números de acesso de voz do Outlook também são chamados de números piloto do plano de discagem. Esse número é usado pelos usuários do Voice Access Outlook para acessar suas caixas de correio e permite que eles pesquisar o diretório.

Por padrão, quando você cria um UM plano de discagem, nenhum número está configurado do Outlook Voice Access. Para permitir que os usuários utilizem o recurso Outlook Voice Access, você deve configurar pelo menos um número de telefone ou ramal. O número de caracteres alfanuméricos no número do Outlook Voice Access não pode exceder 20. Depois de configurar esse número no plano de discagem, o número será exibido nas opções de correio de voz no Microsoft Outlook e no Outlook Web App.

Você pode usar a caixa de **números do Outlook Voice Access** em UM plano de discagem para adicionar um número de telefone ou ramal que um usuário irá chamar para acessar o sistema de correio de voz utilizando Outlook Voice Access. Na maioria dos casos, você irá inserir um número de ramal ou um número de telefone externo. No entanto, pois este campo aceita caracteres alfanuméricos, um URI do SIP pode ser usado se você estiver usando um IP-PBX, um PBX com SIP habilitado, Office Communications Server 2007 R2 ou Microsoft Lync Server.

Dependendo das necessidades da sua organização, convém configurar um ou mais número do Outlook Voice Access. Você pode ter um único número do Outlook Voice Access configurado em um único UM plano de discagem ou pode haver vários números de acesso de voz do Outlook em um único plano de discagem de Unificação de mensagens, mas você não pode ter um único número do Outlook Voice Access que se estende por vários planos de discagem de Unificação de mensagens.

