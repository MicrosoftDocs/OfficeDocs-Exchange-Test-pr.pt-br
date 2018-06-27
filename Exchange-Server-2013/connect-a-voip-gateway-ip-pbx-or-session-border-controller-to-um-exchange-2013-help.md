---
title: 'Conectar a um controlador de borda de sessão, PBX IP ou gateway VoIP para Unificação de MENSAGENS: Exchange 2013 Help'
TOCTitle: Conectar a um controlador de borda de sessão, PBX IP ou gateway VoIP para Unificação de MENSAGENS
ms:assetid: a7cecf59-b93a-413b-bb88-29f2669ef2cf
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Bb124084(v=EXCHG.150)
ms:contentKeyID: 50556250
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Conectar a um controlador de borda de sessão, PBX IP ou gateway VoIP para Unificação de MENSAGENS

 

_**Aplica-se a:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Tópico modificado em:**2016-12-09_

Você deve configurar a voz através de gateways IP (VoIP) e IP Private Branch troca (PBXs) corretamente quando você implantar a Unificação de mensagens (UM) para sua organização. Se você estiver implantando a Unificação de MENSAGENS em um ambiente híbrido, você também precisará configurar corretamente os controladores de borda de sessão (SBCs). Para fazer isso, você precisará configurar a ou mais interfaces do gateways VoIP, PBXs IP e SBCs se comunicar com os servidores de acesso para cliente que executa o serviço Microsoft Exchange Unified Messaging roteador de chamada e os servidores de caixa de correio executando o serviço de Unificação de mensagens do Microsoft Exchange.


> [!IMPORTANT]
> Quando você executa tarefas administrativas para um gateway VoIP, IP PBX ou SBC usando um navegador da web, as solicitações HTTP enviadas pela rede não são criptografadas. Para aumentar o nível de segurança dos gateways VoIP, IP PBXs ou SBCs na sua rede, use o Internet Protocol security (IPsec) ou Secure Sockets Layer (SSL) para ajudar a proteger as credenciais administrativas e os dados transmitidos na rede. Também recomendamos que você use um mecanismo de autenticação forte e senhas administrativas complexas para proteger as credenciais administrativas para o dispositivo.



## Interfaces de dispositivo telefonia IP

Há vários tipos de portas ou interfaces que devem ser configuradas para habilitar a comunicação entre um PBX, VoIP gateway, IP PBX ou SBC e os servidores de acesso para cliente e caixa de correio em sua rede. Quando você configura um gateway VoIP, IP PBX ou SBC, você deve considerar se o dispositivo é analógico, digital, ou analógico e digital.

Se a interface de gateway VoIP que se conecta a um PBX for analógica, você deve configurar corretamente as configurações apropriadas para habilitar o gateway VoIP para se comunicar com os servidores de acesso para cliente e caixa de correio. Para PBXs IP e SBCs, você deve configurar também corretamente as interfaces IP para permitir que esses dispositivos se comunicar com os servidores de acesso para cliente e caixa de correio. Todos esses dispositivos tem diferentes tipos de conexões ou portas que estão disponíveis, dependendo do modelo do dispositivo e do fornecedor.

Para habilitar a comunicação com os servidores de acesso para cliente e caixa de correio em sua rede:

  - Para os gateways VoIP, você deve configurar as interfaces de telefonia para se comunicar com seus PBXs e você deve configurar a interface IP do dispositivo.

  - Para IP PBXs, você deve configurar o circuito-based e de rede ou conexões baseadas em IP.

  - Para SBCs, você deve configurar ambas as interfaces IP, um para a rede e a outra interface que se conecta pela Internet ou por uma conexão WAN dedicada.

A seguir está uma lista dos recursos encontrados no TechCenter do Exchange que fornecem informações que podem ajudá-lo a configurar corretamente seus gateways VoIP, PBXs IP e SBCs:

  - **Gateway IP com suporte, IP PBX e documentação de PBX** [Supervisor de telefonia para o Exchange 2013](telephony-advisor-for-exchange-2013-exchange-2013-help.md) inclui informações de instalação que você pode usar ao configurar gateways VoIP, IP PBXs, PBXs e SBCs e arquivos de configuração.   

  - **Configuração e notas técnicas** [Notas de configuração para gateways VoIP com suporte, IP PBXs e PBXs](configuration-notes-for-supported-voip-gateways-ip-pbxs-and-pbxs-exchange-2013-help.md) inclui arquivos de configuração e informações de instalação que você pode usar ao configurar gateways VoIP, IP PBXs e PBXs.   

  - **Notas de configuração de UM do Exchange online** [Notas de configuração para controladores de borda de sessão suportados](configuration-notes-for-supported-session-border-controllers-exchange-2013-help.md) inclui informações de instalação que podem ser usados quando você configura SBCs e arquivos de configuração.   

Especialistas do Unified Messaging estão disponíveis para ajudá-lo a configuração de telefonia e dispositivos de rede com base em IP. Uma especialista em Unificação de mensagens pode ajudar a certificar-se de que há uma transição suave para Unificação de mensagens de um legacy ou sistema de email de voz de terceiros ou ajudá-lo a planejar e implantar um novo sistema de caixa postal com a Unificação de mensagens do Exchange. Implantando um novo sistema de caixa postal ou atualizando um herdado exige conhecimento significativo sobre VoIP gateways, IP PBXs, PBXs e Unificação de mensagens. Para obter mais informações sobre como entrar em contato com uma especialista em Unificação de mensagens, consulte [Microsoft Exchange Server 2013 Unified Messaging (UM) especialistas](http://go.microsoft.com/fwlink/p/?linkid=262708) ou parceiros certificados da Unificação de MENSAGENS no [Microsoft identifique](https://go.microsoft.com/fwlink/p/?linkid=261951).

Depois de configurar um gateway VoIP, IP PBX ou SBC IP interface, você deve criar e configurar um gateway IP de UM para representar cada dispositivo que você implantou. Para obter mais informações sobre como criar um gateway IP de UM, consulte [Criar um gateway IP de UM](create-a-um-ip-gateway-exchange-2013-help.md).

Depois de criar um gateway IP de UM, os servidores de acesso para cliente e caixa de correio associados ao gateway IP de UM enviam uma solicitação SIP OPTIONS para o gateway VoIP, IP PBX ou SBC para garantir que ele está respondendo de forma. Se o gateway VoIP, IP PBX ou SBC não responder, o servidor de caixa de correio registrará um evento com ID 1088 informando que a solicitação falhou. Para resolver esse problema, verifique se o gateway VoIP, IP PBX ou SBC está disponível e online e a configuração do serviço de Unificação de mensagens está correta.

Um servidor de acesso para cliente e um servidor de caixa de correio se comunicará somente com um gateway VoIP, IP PBX ou SBC está listado como um ponto de protocolo de iniciação de sessão (SIP) confiável. Um evento com ID 1175 será registrado quando vários hosts DNS compartilham o mesmo endereço IP. Esse evento pode ocorrer se você tiver configurado as zonas DNS com os FQDNs dos gateways VoIP em sua rede. A Unificação de mensagens protege contra solicitações não autorizadas Recuperando a URL interna do diretório virtual do Unified Messaging serviços da Web que está localizado no servidor de caixa de correio e, em seguida, usando a URL para criar a lista de FQDNs para o SIP confiável de correspondentes. Depois de dois FQDNs serão resolvidos para o mesmo endereço IP, esse evento será registrado.


> [!TIP]
> Você deve reiniciar o MicrosoftExchange Unificação de mensagens do serviço se um gateway VoIP, IP PBX, ou SBC está configurado para ter um FQDN e o registro DNS do gateway VoIP, IP PBX ou SBC é alterado depois que o serviço foi iniciado. Se você não reiniciar o serviço, o servidor de caixa de correio não conseguirá localizar o gateway VoIP, IP PBX ou SBC. Isso ocorre porque um servidor de caixa de correio mantém um cache para todos os gateways VoIP, IP PBXs ou SBCs na memória e a resolução DNS é executada somente quando o serviço for reiniciado ou quando a configuração de um gateway VoIP, IP PBX ou SBC foi alterada.


