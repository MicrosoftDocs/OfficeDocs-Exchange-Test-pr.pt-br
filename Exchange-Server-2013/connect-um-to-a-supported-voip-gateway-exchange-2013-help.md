---
title: 'Conectar a UM a um gateway de VoIP com suporte: Exchange 2013 Help'
TOCTitle: Conecte-se a Unificação de mensagens a um gateway de VoIP com suporte
ms:assetid: b8dfc8bd-2ee5-418d-b0a4-4fa2ec7e2a2e
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Bb124360(v=EXCHG.150)
ms:contentKeyID: 50556267
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Conecte-se a Unificação de mensagens a um gateway de VoIP com suporte

 

_**Aplica-se a:** Exchange Server 2013, Exchange Server 2016_

_**Tópico modificado em:** 2013-04-19_

Quando você está definindo o Unified Messaging (UM), você deve configurar a voz sobre IP (VoIP) gateways, IP PBXs, PBXs habilitados para SIP ou controladores de borda de sessão (SBCs) em sua rede para se comunicar com os servidores de acesso para cliente que executa o serviço Microsoft Exchange Unified Messaging roteador de chamada e os servidores de caixa de correio executando o serviço de Unificação de mensagens do Microsoft Exchange em sua organização Exchange. Você também deve configurar o acesso para cliente e os servidores de caixa de correio para se comunicar com os gateways VoIP, IP PBXs, SBCs ou PBXs habilitados para SIP.


> [!TIP]
> Depois de se conectar os servidores de acesso para cliente e caixa de correio para os gateways VoIP, IP PBXs, PBXs habilitados para SIP ou SBCs em sua rede de dados, você deve criar os componentes necessários de Unificação de mensagens e também permitem que os usuários para Unificação de mensagens para que possam usar o sistema de caixa postal.



## Etapas

Aqui estão as etapas básicas para conectar os gateways VoIP, IP PBXs, SBCs ou PBXs habilitados para SIP para servidores de caixa de correio e acesso para cliente:

Etapa 1: Instale os servidores de acesso para cliente e caixa de correio em sua organização.

Etapa 2: Criar e configurar um plano de discagem de ramal de telefone, URI do SIP ou UM e. 164.

Etapa 3: Criar e configurar um gateway IP de UM. Você deve criar e configurar um gateway IP de UM para cada gateway VoIP, IP PBX, habilitados para SIP PBX ou SBC que irá aceitar chamadas de entrada e envio de chamadas de saída.

Etapa 4: Crie um novo grupo de busca de Unificação de mensagens, se necessário. Se você cria um gateway IP de UM e um plano de discagem de Unificação de mensagens não for especificado, um grupo de busca de UM será criado automaticamente.

Consulte as seções a seguir para obter informações sobre cada etapa.

## Etapa 1: Instalar os servidores de acesso para cliente e caixa de correio

Quando você estiver implantando os servidores do Exchange em sua organização, você pode instalar o acesso para cliente e os servidores de caixa de correio no mesmo computador ou instalar o servidor de acesso para cliente em um computador separado a partir do servidor de caixa de correio. Para instalar o servidor de acesso para cliente, execute Setup.exe da mídia de instalação. Quando você estiver instalando o servidor de acesso para cliente em um computador separado a partir do servidor de caixa de correio ou instalá-lo no mesmo computador, você usar o mesmo comando. Para obter detalhes, consulte [Instalar o Exchange 2013 usando o Assistente para Configuração](install-exchange-2013-using-the-setup-wizard-exchange-2013-help.md). Se você deseja adicionar recursos e funcionalidades para seu servidor Exchange existente, você pode usar **programas e recursos** ou Setup.exe.

## Etapa 2: Criar e configurar um plano de discagem de Unificação de mensagens

Após ter instalado os servidores necessários, crie primeiro um plano de discagem de UM. Um plano de discagem de UM contém as definições de configuração que permitem conectar à sua rede de telefonia, vinculando para um único ou vários os gateways IP de UM. Um gateway IP de UM e o grupo de busca estiverem diretamente ligados a um plano de discagem de UM e também são necessários. Para obter detalhes, consulte [Criar um plano de discagem de UM](create-a-um-dial-plan-exchange-2013-help.md).

Um plano de discagem UM estabelece um link do número de ramal de um usuário para suas caixas de correio habilitadas para UM. Quando você cria um plano de discagem de UM, você pode configurar o número de dígitos nos ramais, o tipo de identificador de recurso uniforme (URI) e o plano de discagem da configuração de segurança de VoIP.

Existem três tipos de planos de discagem: ramal de telefone, o URI do protocolo de iniciação de sessão (SIP) e e. 164. Quando você cria e configurar um plano de discagem de Unificação de mensagens, você deve determinar o tipo de informação que tiver enviado do seu PBX IP, habilitados para SIP PBX, ou PBX e se estão sendo enviadas as chamadas para um servidor de acesso para cliente ou caixa de correio em um ramal de telefone ou o formato e. 164. Se você estiver implantando o Microsoft Office Communications Server 2007 R2 ou Microsoft Lync Server, você deve criar e configurar um plano de discagem URI do SIP.

## Etapa 3: Criar e configurar um gateway IP de UM

Depois de criar um UM plano de discagem, você deve criar um gateway IP de UM para representar cada gateway VoIP, IP PBX ou SBC em sua rede. Quando você cria um gateway IP de UM, você poderá configurá-lo para usar um endereço IP ou um nome de domínio totalmente qualificado (FQDN). Se você usar um FQDN, você deve se certificar que foi configurado corretamente um registro de host DNS para o gateway IP para que o nome do host será resolvido corretamente como um endereço IP.

Após instalar um gateway VoIP, IP PBX ou SBC, você deve criar um gateway IP de UM para representar o dispositivo de hardware físico. Depois que você criou um gateway IP de UM, o servidor de acesso para cliente que usam o gateway IP de UM enviará uma solicitação SIP OPTIONS para o gateway VoIP, IP PBX ou SBC para garantir que ele está respondendo de forma. Se o gateway VoIP, IP PBX, habilitados para SIP PBX ou SBC não responder, o servidor de acesso para cliente registrará um evento com ID 1088 informando que a solicitação falhou. Para resolver esse problema, certifique-se de que o gateway VoIP, IP PBX ou SBC está disponível e online e se a configuração do serviço de Unificação de mensagens está correta.

Servidores de acesso para cliente e caixa de correio se comunicará somente com um gateway VoIP, IP PBX ou SBC está listado como um ponto confiável do SIP. Em alguns casos, se dois gateways VoIP, IP PBXs ou SBCs estão configurados para usar o mesmo endereço IP, um evento com ID 1175 será registrado. Esse evento pode ocorrer se você configurou as zonas DNS com nomes de domínio totalmente qualificados (FQDNs) para os gateways VoIP em sua rede. A Unificação de mensagens protege contra solicitações não autorizadas Recuperando a URL interna do diretório virtual do Unified Messaging serviços da Web que está localizado no servidor de caixa de correio e, em seguida, usando a URL para criar a lista de FQDNs para o SIP confiável de correspondentes. Depois de dois FQDNs serão resolvidos para o mesmo endereço IP, esse evento será registrado.

Você deve reiniciar o MicrosoftExchange o serviço de Unificação de mensagens se um gateway IP de UM estiver configurado para usar um FQDN e o registro DNS do gateway IP de UM for alterado depois que o serviço foi iniciado. Se você não reiniciar o serviço, o servidor de caixa de correio não conseguirá localizar o gateway IP de UM. Isso ocorre porque um servidor de caixa de correio mantém um cache para todos os gateways IP de UM na memória e a resolução DNS é executada somente quando o serviço for reiniciado ou quando a configuração de um gateway VoIP, IP PBX ou SBC foi alterada.

Unificação de mensagens do Exchange oferece suporte a vários fornecedores de gateway VoIP e de outros fornecedores de IP PBXs, SBCs e PBXs habilitados para SIP. Cada um dos gateways VoIP com suporte foi projetado para se conectar a uma variedade de sistemas de PBX de terceiros.

Para obter informações detalhadas sobre os gateways VoIP, consulte os tópicos a seguir:

  - [Criar um gateway IP de UM](create-a-um-ip-gateway-exchange-2013-help.md)

  - [Notas de configuração para gateways VoIP com suporte, IP PBXs e PBXs](configuration-notes-for-supported-voip-gateways-ip-pbxs-and-pbxs-exchange-2013-help.md)

  - [Conectar a um controlador de borda de sessão, PBX IP ou gateway VoIP para Unificação de MENSAGENS](connect-a-voip-gateway-ip-pbx-or-session-border-controller-to-um-exchange-2013-help.md)

Para obter detalhes, consulte [Conectar seu sistema de caixa postal à sua rede de telefone](connect-your-voice-mail-system-to-your-telephone-network-exchange-2013-help.md).

## Etapa 4: Criar um novo grupo de busca de Unificação de mensagens (se necessário)

Grupo de busca é um termo usado para descrever um grupo de números de ramais de PBX (central privada de comutação telefônica) ou PBX IP compartilhados por usuários. Os grupos de busca são usados para distribuir chamadas com eficiência para/de uma unidade comercial específica. A criação e a definição de um grupo de busca minimiza as chances de um chamador receber o sinal de ocupado quando a chamada é recebida.

Grupos de busca UM espelham de grupos de busca que são usados nas PBXs e PBXs IP. Quando você configura seu ou IP PBXs, você deve criar e configurar uma ou grupos de busca de Unificação de mensagens mais. Grupos de busca de Unificação de mensagens atuam como um link entre o gateway IP de UM e UM plano de discagem.

Dependendo de como criar seu gateway IP de UM, talvez seja necessário criar um ou UM novo vários grupos de busca. Se você não vincular um gateway IP de UM com um plano de discagem quando você cria UM novo gateway IP, um único grupo de busca de Unificação de mensagens é criado por padrão. Se você vincular um gateway IP de UM para um UM plano de discagem quando você cria UM novo gateway IP, todas as chamadas recebidas serão enviadas através do gateway IP de UM e essas chamadas serão aceitas pelos servidores de acesso para cliente e caixa de correio. Se você não vincular um gateway IP de UM a um plano de discagem de UM, quando você cria UM novo gateway IP, você precisará criar um grupo de busca de Unificação de mensagens com o identificador piloto correto para as chamadas recebidas sejam encaminhadas de um gateway IP de UM a um plano de discagem.

Se você tiver vários números de atendedor automático e de Outlook Voice Access e tiver vinculado a um gateway IP de UM a um plano de discagem, você precisará excluir o grupo de busca que foi criado por padrão e cria vários grupos de busca de Unificação de mensagens. Para obter detalhes sobre como criar um UM grupo de busca, consulte [Criar um grupo de busca de UM](create-a-um-hunt-group-exchange-2013-help.md).

