---
title: 'Implementar o UM do Exchange 2013: Exchange 2013 Help'
TOCTitle: Implementar o UM do Exchange 2013
ms:assetid: d147d4b1-32d7-476b-b76f-ee3c0b35ba49
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/JJ673564(v=EXCHG.150)
ms:contentKeyID: 50486704
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Implementar o UM do Exchange 2013

 

_**Aplica-se a:** Exchange Server 2013, Exchange Server 2016_

_**Tópico modificado em:** 2016-12-09_

A Unificação de Mensagens (UM) exige que você integre a sua implantação do Exchange Server a um sistema de telefonia existente em sua organização. Uma implantação bem-sucedida exige uma análise cuidadosa da infraestrutura de telefonia existente para que você execute as etapas corretas de planejamento a fim de implantar e gerenciar a caixa postal na Unificação de Mensagens.

**Conteúdo**

Before you deploy

Deploying Unified Messaging

Post-deployment tasks for Unified Messaging

## Antes de implantar

Antes de implantar a UM, recomendamos que se familiarize com os conceitos dos seguintes tópicos:

  - [Planos de discagem de Unificação de mensagens](https://docs.microsoft.com/pt-br/exchange/voice-mail-unified-messaging/connect-voice-mail-system/um-dial-plans)

  - [Gateways IP de UM](um-ip-gateways-exchange-2013-help.md)

  - [Serviços de Unificação de mensagens](um-services-exchange-2013-help.md)

  - [Grupos de busca de Unificação de mensagens](https://docs.microsoft.com/pt-br/exchange/voice-mail-unified-messaging/connect-voice-mail-system/um-hunt-groups)

  - [Responder e rotear as chamadas de entrada automaticamente](automatically-answer-and-route-incoming-calls-exchange-2013-help.md)

  - [políticas de caixa de correio de UM](https://docs.microsoft.com/pt-br/exchange/voice-mail-unified-messaging/set-up-voice-mail/um-mailbox-policies)

  - [Caixa postal para usuários](https://docs.microsoft.com/pt-br/exchange/voice-mail-unified-messaging/set-up-voice-mail/voice-mail-for-users)

## Implantando a UM

Se você estiver implantando a UM usando IP Private Branch eXchanges (IP PBXs), gateways VoIP ou o Microsoft Lync Server, todas as opções de implantação de Unificação de Mensagens terão várias etapas em comum. Essas etapas são necessárias para criar um sistema escalonável e de alta disponibilidade para suporte a grandes números de usuários de UM. As etapas são as seguintes:

1.  Implantar e configurar componentes de telefonia para UM.

2.  Verificar se instalou corretamente o servidor de Acesso para Cliente executando o serviço Roteador de Chamadas de Unificação de Mensagens do Microsoft Exchange e o servidor de Caixa de Correio executando o serviço de Unificação de Mensagens do Microsoft Exchange.

3.  Criar e configurar os componentes de UM necessários.

4.  Executar todas tarefas de pós-implantação para UM.

## Implantar e configurar componentes de telefonia

Para implantar com êxito a Unificação de Mensagens em uma organização do Exchange, o administrador do Exchange deve estar informado sobre os conceitos da rede de dados e a terminologia e os conceitos de telefonia e deve estar preparado para configurar corretamente os componentes de telefonia solicitados pela UM. A realização de uma nova implantação ou a atualização de um sistema de caixa postal herdado exige conhecimento significativo sobre redes de telefonia e Unificação de Mensagens.

Geralmente, você precisa concluir três tarefas para configurar com êxito os componentes de telefonia solicitados pela UM:

1.  **Provisionar linhas PBX**   A primeira etapa na implantação de uma solução de UM escalonável é com alta escalabilidade é provisionar linhas PBX.

2.  **Organizar canais**   Depois que tiver disponibilizado canais de voz baseados em PBX, você poderá organizar os canais em grupos de busca.

3.  **Implantar gateways VoIP**   Depois que tiver organizado seus canais de voz como grupos de busca, você deverá finalizar esses canais em gateways VoIP. Gateways VoIP são usados com um PBX herdado para converter os protocolos de comutação de circuitos encontrados em uma rede de telefonia em protocolos de comutação de pacotes baseados em IP.

Quando você integra as redes de dados e telefonia da organização durante a implantação da Unificação de Mensagens, é necessário configurar corretamente os componentes de rede de dados e telefonia. Você deverá também configurar os seguintes componentes ou interfaces para implantar a Unificação de Mensagens com êxito:

  - **Configure a conexão dos PBXs de sua organização para que se comuniquem com os gateways VoIP.**   Para obter detalhes, consulte [Conectar a um gateway VoIP para se comunicar com um PBX](connect-a-voip-gateway-to-communicate-with-a-pbx-exchange-2013-help.md).

  - **Configure a conexão da interface de gateway VoIP para o PBX.**   Para obter mais informações sobre como configurar sua interface PBX para se comunicar com o gateway VoIP suportado, consulte a documentação do produto específica para o seu PBX ou consulte [Conectar a um gateway VoIP para se comunicar com um PBX](connect-a-voip-gateway-to-communicate-with-a-pbx-exchange-2013-help.md).

  - **Configure a conexão da interface de gateway VoIP para os servidores de Acesso para Cliente e Caixa de Correio.**   Para obter detalhes, consulte [Conectar a um controlador de borda de sessão, PBX IP ou gateway VoIP para Unificação de MENSAGENS](connect-a-voip-gateway-ip-pbx-or-session-border-controller-to-um-exchange-2013-help.md).

  - **Configure a conexão da interface de gateway VoIP para os servidores de Acesso para Cliente e Caixa de Correio.**   Para obter detalhes, consulte [Conecte-se a Unificação de mensagens a um gateway de VoIP com suporte](connect-um-to-a-supported-voip-gateway-exchange-2013-help.md).

Voltar ao início

## Instalar os servidores de Caixa de Correio e Acesso para Cliente

Caminhos de implantação diferentes estão disponíveis para organizações que planejam implantar a Unificação de Mensagens do Exchange. Embora esses caminhos levem todos ao mesmo ponto (uma implantação bem-sucedida da Unificação de Mensagens), cada caminho é ligeiramente diferente, porque as necessidades e pontos de partida de cada cliente são distintos. Contudo, geralmente há pontos de partida e caminhos comuns que englobam todos os cenários de implantação para os quais há suporte, o que inclui novas instalações e atualizações. Siga estas etapas para implantar seus servidores de Acesso para Cliente e de Caixa de Correio:

1.  Verifique se sua infraestrutura existente atende a determinados pré-requisitos. Para detalhes, consulte [Pré-requisitos do Exchange 2013](exchange-2013-prerequisites-exchange-2013-help.md).

2.  Implante a sua nova organização do Exchange 2013. Para obter detalhes, consulte [Instalar o Exchange 2013 usando o Assistente para Configuração](install-exchange-2013-using-the-setup-wizard-exchange-2013-help.md).
    

    > [!CAUTION]
    > Você deve implantar pelo menos um servidor de caixa de correio do Exchange 2013 em sua organização antes de configurar gateways VoIP ou PBXs de IP para enviar SIP do UM e tráfego RTP para os servidores de Acesso para Cliente do Exchange 2013.



3.  Verifique se você instalou corretamente os servidores de Acesso para Cliente e de Caixa de Correio. Depois que você instalar os servidores, recomendamos que verifique a instalação e analise os logs de instalação do servidor. Para detalhes, consulte [Verificar uma instalação do Exchange 2013](verify-an-exchange-2013-installation-exchange-2013-help.md).

## Adicionar os pacotes de idioma de UM necessários

Pacotes de idioma de UM permitem que chamadores e usuários do Outlook Voice Access interajam com o sistema de caixa postal em vários idiomas. Depois de instalar um pacote de idiomas adicional em um servidor de Caixa de Correio, os chamadores e os usuários do Outlook Voice Access poderão ouvir as mensagens de email e interagir com o sistema de caixa postal nesse idioma.

Ao instalar o Exchange pela primeira vez, o inglês (EUA) será o idioma padrão e a única opção de idioma disponível para o seu plano de discagem. Depois de instalar um pacote de idiomas de UM em um servidor de Caixa de Correio, o idioma associado ao pacote de idiomas também será listado como uma opção disponível quando você configurar o idioma padrão para o plano de discagem. Por padrão, já que os atendedores automáticos são associados a um plano de discagem da UM quando criados, eles usam a definição do idioma padrão do plano de discagem da UM associado. Entretanto, essa definição pode ser alterada após a criação de um atendedor automático de UM.

Você pode adicionar os pacotes de idiomas de Unificação de MENSAGENS usando o comando Setup.exe ou executando o programa de instalação do *\<UMLanguagePack\>*.exe depois de baixar o pacote de idiomas de Unificação de MENSAGENS do [Exchange Server 2013 UM pacotes de idiomas](https://go.microsoft.com/fwlink/p/?linkid=266542). No entanto, você precisará usar o comando Setup.exe para remover um pacote de idiomas de Unificação de MENSAGENS. Não há nenhum cmdlet do Shell de gerenciamento de Exchange que você pode usar para adicionar ou remover idiomas de um servidor de caixa de correio. Para obter mais informações sobre como instalar um pacote de idiomas de Unificação de MENSAGENS, consulte [Instalar um pacote de idiomas para UM](install-a-um-language-pack-exchange-2013-help.md).


> [!NOTE]
> Por padrão, quando você instala um servidor de caixa de correio, o idioma Inglês dos EUA (en-US) é instalado. Ele não poderá ser removido, a menos que você remova o servidor de Caixa de Correio do computador.



Voltar ao início

## Criar e configurar componentes de UM

Vários componentes suportados da UM são necessários para a implementação e a operação da Unificação de Mensagens. Os componentes de UM conectam a infraestrutura de telefonia ao ambiente da Unificação de Mensagens. Após instalar com êxito os servidores de Acesso para Cliente e de Caixa de Correio, siga estas etapas.

## Etapa 1: Criar e configurar planos de discagem de UM

Os planos de discagem de UM são importantes para a operação da Unificação de Mensagens e são necessários para a implantação bem-sucedida da Unificação de Mensagens em sua rede. Depois de verificar se instalou com êxito os servidores de Acesso para Cliente e Caixa de Correio, um plano de discagem de UM será o primeiro componente a ser criado.

Por padrão, os planos de discagem de UM e os servidores de Acesso para Cliente e Caixa de Correio associados ao plano de discagem enviam e recebem dados sem usar criptografia. No modo não-seguro, o tráfego VoIP e SIP não será criptografado. Quando você cria o plano de discagem ou após tê-lo criado, é possível configurá-lo para criptografar o tráfego de VoIP e SIP usando o protocolo TLS mútuo. Se você usará TLS mútuo, deve definir o plano de discagem para SIP protegido ou Protegido, defina o modo de início da UM como TLS ou Dual, e crie e distribua um certificado confiável, sejam os servidores Exchange e os gateways VoIP, IP PBXs ou controladores de borda de sessão (SBCs). Após configurar a definição de segurança de VoIP, será preciso configurar o modo de inicialização para os servidores de Acesso para Cliente e Caixa de Correio. Para mais detalhes, consulte [Configurar o modo de inicialização em um servidor de caixa de correio](configure-the-startup-mode-on-a-mailbox-server-exchange-2013-help.md) ou [Configurar o modo de inicialização em um servidor de acesso para cliente](configure-the-startup-mode-on-a-client-access-server-exchange-2013-help.md).

Execute o seguinte procedimento para criar um novo plano de discagem de UM.

## Criar um plano de discagem de UM

1.  No Centro de Administração do Exchange (EAC), navegue até **Unificação de Mensagens** \> **Planos de discagem de UM**, e clique em **Adicionar**![Ícone Adicionar](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Ícone Adicionar").

2.  Na página **Novo Plano de Discagem de UM**, preencha as seguintes caixas:
    
      - **Nome**   Digite o nome do plano de discagem. O nome plano de discagem da UM é obrigatório e deve ser exclusivo. O nome digitado é usado apenas para fins de exibição no EAC e no Shell. O comprimento máximo de nome de plano de discagem de UM é 64 caracteres e pode incluir espaços. Entretanto, não pode incluir nenhum dos seguintes caracteres: " / \\ \[ \] : ; | = , + \* ? \< \>.
        

        > [!IMPORTANT]
        > Embora a caixa para o nome do plano de discagem possa aceitar 64 caracteres, esse nome não pode ter mais de 49 caracteres. Isso ocorre porque, quando você cria um plano de discagem, uma diretiva de caixa de correio de UM padrão é também criada com a mesma diretiva padrão <EM>&lt;DialPlanName&gt;</EM>. O parâmetro <EM>name</EM> do plano de discagem de UM e da diretiva de caixa de correio de UM pode ter 64 caracteres.

    
      - **Comprimento do ramal (dígitos)**   Insira o número de dígitos para números de ramal no plano de discagem. O número de dígitos em números de ramal baseia-se no plano de discagem de telefonia criado em um PBX. Por exemplo, se um usuário associado a um plano de discagem de telefonia discar um ramal com quatro dígitos para chamar outro usuário do mesmo plano de discagem de telefonia, selecione 4 como o número de dígitos do ramal.
        
        Essa é uma caixa necessária que tem um intervalo de valor de 1 a 20. O tamanho de ramal normalmente varia de 3 a 7 números. Se o ambiente de telefonia existente incluir números de ramais, será preciso especificar um número de dígitos que corresponda ao número de dígitos nesses ramais.
        
        Ao criar um plano de discagem de ramal telefônico, você é obrigado a inserir um número de ramal para o usuário quando ele está vinculado a um plano de discagem de ramal telefônico. Um número de ramal é também necessário com planos de discagem de Session Initiation Protocol (SIP) ou planos de discagem E.164 quando um usuário habilitado para UM é vinculado a um plano de discagem URI SIP ou E.164. Esse número de ramal é usado pelos usuários do Outlook Voice Access quando acessam sua caixa de correio do Exchange.
    
      - UNRESOLVED\_TOKENBLOCK\_VAL(Tipo UI\_URI)
    
      - UNRESOLVED\_TOKENBLOCK\_VAL(Segurança UI\_VoIP)
    
      - **Código de País/Região**   Use essa caixa para digitar o código numérico do país/região usado para chamadas de saída. Esse número precederá automaticamente o número de telefone discado. Essa caixa aceita de 1 a 4 dígitos. Por exemplo, nos Estados Unidos, o código de país/região é 1. No Reino Unido, é 44.

3.  Clique em **Salvar**.
    

    > [!IMPORTANT]
    > Em versões anteriores do Exchange, o servidor de Unificação de Mensagens preciso ser adicionado a um plano de discagem de UM. No Exchange 2013, os servidores de Acesso para Cliente e de Caixa de Correio não podem ser associados a um ramal telefônico ou plano de discagem E.164. Os servidores de Acesso para Cliente e de Caixa de Correio responderão todas as chamadas de entrada de todos os tipos de planos de discagem. Porém, se estiver integrando a UM ao Microsoft Lync Server, você deverá adicionar todos os servidores de Acesso para Cliente e Caixa de Correio a todos os planos de discagem URI SIP para permitir que o roteamento de mensagens funcione corretamente com o Lync Server.



Voltar ao início

## Etapa 2: Criar e configurar gateways IP de UM

O gateway IP de UM representa um dispositivo de hardware de gateway VoIP ou IP PBX. A combinação do objeto de gateway IP de UM e um objeto de grupo de busca de UM estabelece um vínculo entre um gateway VoIP ou IP PBX e um plano de discagem de UM.

Se tiver criado ou habilitado a segurança de VoIP em um plano de discagem, o gateway IP da UM que você cria usando um dos seguintes procedimentos será associado a um plano de discagem de UM que usa segurança de VoIP. Nesse caso, é preciso usar um nome de domínio totalmente qualificado (FQDN) para criar o gateway IP de UM e não um endereço IP. É necessário também configurar o gateway IP de UM para escutar em TCP na porta 5061. Para configurar o gateway para que escute nesse porta, execute o seguinte comando: `Set-UMIPGateway -identity MyUMIPGateway -Port 5061`. Você também deverá verificar se gateways VoIP ou IP PBXs foram configurados para escutar a porta 5061 do protocolo TLS mútuo.

Execute o seguinte procedimento para criar um novo gateway IP de UM.

## Criar um gateway IP de UM

1.  
    
    No EAC, navegue até **Unificação de Mensagens** \> **Gateways IP da UM** e clique em **Adicionar**![Ícone Adicionar](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Ícone Adicionar").

2.  Na página do **Novo gateway IP da UM**, insira as seguintes informações:
    
      - **Nome**   Use essa caixa para especificar um nome exclusivo para o gateway IP de UM. Esse é um nome de exibição que aparece no EAC. Se você precisar alterar o nome de exibição do gateway IP de UM depois da sua criação, primeiro exclua o gateway IP de UM existente e depois crie outro com o nome apropriado. O nome do gateway IP de UM é necessário, mas é usado apenas para fins de exibição. Como sua organização pode usar vários gateways IP de UM, recomendamos que você use nomes significativos para eles. O comprimento máximo de um nome de gateway IP de UM é 64 caracteres e pode incluir espaços. Entretanto, não pode incluir nenhum dos seguintes caracteres: " / \\ \[ \] : ; | = , + \* ? \< \>.
    
      - **Endereço**   Você pode configurar um gateway IP de UM com um endereço IP ou um FQDN (nome de domínio totalmente qualificado). Use essa caixa para especificar o endereço IP configurado no gateway VoIP, PBX habilitado para SIP, PBX IP, SBC ou FQDN. Essa caixa aceita somente FQDNs válidos e formatados corretamente.
        
        Você pode inserir caracteres alfabéticos e numéricos nessa caixa. Há suporte para FQDNs, endereços IPv6 e endereços IPv4. Se você quiser usar TLS mútua entre um gateway de IP da UM e um plano de discagem funcionando no modo SIP seguro ou Seguro, você deverá configurar o gateway IP da UM com um FQDN. Você também deve configurá-lo para escutar na porta 5061 e verificar se gateways VoIP ou PBXs IP também foram configurados para escutar solicitações de TLS mútuas na porta 5061. Para configurar um gateway IP de UM, execute o seguinte comando: `Set-UMIPGateway -identity MyUMIPGateway -Port 5061`.
        
        Se você usar um FQDN, você também deve se certificar que configurou corretamente um registro de host DNS para o gateway VoIP, de modo que o nome de host seja resolvido corretamente para um endereço IP. Se você utilizar um FQDN em vez de um endereço IP, e a configuração DNS para o gateway IP da UM for alterada, você deverá desabilitar e, em seguida, habilitar o gateway IP de UM para certificar-se de que as informações de configuração do gateway IP da UM estejam atualizadas corretamente
    
      - **Plano de discagem da UM**   Clique no botão **Procurar** para selecionar o plano de discagem da UM que deseja associar ao gateway IP da UM. Quando você seleciona um plano de discagem de UM para associar a um gateway IP de UM, um número coletivo padrão de UM é também criado e associado ao plano de discagem de UM selecionado. Se você não selecionar um plano de discagem de UM, deverá criar manualmente um grupo de busca de UM e depois associar esse grupo de busca de UM ao gateway IP de UM a ser criado.

3.  
    
    Clique em **Salvar**.

## Etapa 3: Criar e configurar os grupos de busca de UM (opcionais)

*Grupo de busca* é um termo usado para descrever um grupo de recursos de PBX ou IP PBX ou números de ramais compartilhados por usuários. Os grupos de busca são usados para distribuir chamadas com eficiência para/de uma determinada unidade comercial.

Se tiver criado um gateway IP de UM e associá-lo a um plano de discagem, o grupo de busca de UM padrão será criado. É possível associar outro grupo de busca de UM ao mesmo gateway IP de UM ou a um diferente, dependendo do número de gateways criados.

Ao criar um grupo de busca de UM, você habilita todos os servidores de Caixa de Correio especificados em um plano de discagem da UM para comunicação com um gateway VoIP. Para obter detalhes, consulte [Grupos de busca de Unificação de mensagens](https://docs.microsoft.com/pt-br/exchange/voice-mail-unified-messaging/connect-voice-mail-system/um-hunt-groups).

## Criar um grupo de busca de UM

1.  No EAC, navegue até **Unificação de Mensagens** \> **Planos de discagem de UM**. Na exibição de lista, selecione o plano de discagem de UM que você deseja modificar e clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").

2.  Na página **Plano de discagem da UM**, em **Grupos de Busca da UM**, clique em **Adicionar**![Ícone Adicionar](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Ícone Adicionar").

3.  Na página **Novo Grupos de Busca da UM**, preencha as seguintes caixas:
    
      - **Gateway IP da UM associado**   Esta caixa apenas para exibição mostra o nome do gateway IP da UM que será associado ao grupo de busca da UM.
    
      - **Nome**   Use essa caixa para criar o nome de exibição do grupo de busca de UM. Um nome para o grupo de busca de UM é necessário e deve ser exclusivo, mas é usado apenas para fins de exibição no EAC e no Shell. Se você precisar alterar o nome de exibição do grupo de busca depois da sua criação, primeiro exclua o grupo de busca existente e depois crie outro grupo de busca com o nome apropriado.
        
        Se a sua organização usa vários grupos de busca, convém usar nomes significativos para eles. O comprimento máximo do nome do grupo de busca de UM é 64 caracteres e pode incluir espaços. Entretanto, não pode incluir nenhum dos seguintes caracteres: " / \\ \[ \] : ; | = , + \* ? \< \>.
    
      - **Plano de discagem**   Clique em **Procurar** para selecionar o plano de discagem que será associado ao grupo de busca da UM. É necessário associar um grupo de busca a um plano de discagem. Um grupo de busca da UM pode ser associado a apenas um gateway IP da UM e um plano de discagem da UM.
    
      - **Identificador piloto**   Use esta caixa para especificar uma cadeia de caracteres que identifique exclusivamente o identificador piloto ou o ID piloto configurado no PBX ou no IP PBX.
        
        É possível usar um número de ramal ou um URI (Uniform Resource Identifier) SIP (Session Initiation Protocol) nesta caixa. Caracteres alfanuméricos são aceitos nesta caixa. Para PBXs herdados, é usado um valor numérico com identificador piloto. No entanto, alguns IP PBXs podem usar URIs SIP.

4.  Clique em **Salvar**.

Voltar ao início

## Etapa 4: Criar e configurar diretiva de caixa de correio de UM

As diretivas de caixa de correio de UM são necessárias quando os usuários são habilitados para a Unificação de Mensagens. A caixa de correio de cada usuário habilitado para UM deve estar vinculada a uma única diretiva de caixa de correio de UM. Depois de criar uma política de caixa de correio de UM, você vincula uma ou mais caixas de correio habilitadas para UM à política de caixa de correio de UM. Isso permite controlar as configurações de segurança de PIN, como o número mínimo de dígitos em um PIN ou o número máximo de tentativas de logon com falha para os usuários habilitados para UM que estão associados à diretiva de caixa de correio do UM.

Sempre que você cria um plano de discagem de UM, uma diretiva de caixa de correio de UM também é criada. A diretiva de caixa de correio de UM será chamada Diretiva Padrão do \<*DialPlanName*\>. Entretanto, se for preciso criar uma nova política de caixa de correio de UM, execute o seguinte procedimento.

## Criar uma política de caixa de correio da UM

1.  
    
    No EAC, navegue até **Unificação de Mensagens** \> **Planos de discagem de UM**. Na exibição de lista, selecione o plano de discagem de UM que você deseja alterar e clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").

2.  Na página **Plano de discagem de UM**, em **Políticas de Caixa de Correio de UM**, clique em **Adicionar**![Ícone Adicionar](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Ícone Adicionar").

3.  Na página **Nova Política de Caixa de Correio do UM** , na caixa de texto **Nome**, digite o nome da política de caixa de correio do UM.
    
    Use essa caixa para especificar um nome exclusivo para a política de caixa de correio de UM. Esse é um nome de exibição que aparece no EAC. Se for necessário alterar o nome de exibição da diretiva de caixa de correio de UM depois da sua criação, primeiro você deve excluir a diretiva de caixa de correio de UM existente e, em seguida, criar outra diretiva de caixa de correio de UM com o nome adequado. Não será possível excluir uma política de caixa de correio de UM se um usuário habilitado para UM estiver associado a ela.
    
    O nome da diretiva de caixa de correio do UM é obrigatório, mas ele é usado apenas para fins de exibição. Como a sua organização pode utilizar várias políticas de caixa de correio de UM, recomendamos que você use nomes significativos para elas. O comprimento máximo para um nome de política de caixa de correio de UM é de 64 caracteres e pode conter espaços. Entretanto, não pode incluir nenhum dos seguintes caracteres: " / \\ \[ \] : ; | = , + \* ? \< \>.

4.  Clique em **Salvar** para salvar a nova política de caixa de correio de UM. Quando você salva a política de caixa de correio de UM, todas as configurações padrão, incluindo as políticas de PIN, os recursos de caixa postal e as configurações de Caixa Postal Protegida, são habilitadas. Se quiser personalizar ou alterar configurações padrão, use o cmdlet **Set-UMMailbox** para alterar as configurações da política de caixa de correio de UM recém-criada.

## Etapa 5: Criar e configurar atendedores automáticos de UM (opcionais)

A Unificação de Mensagens permite a criação de um ou mais atendedores automáticos da UM, dependendo das necessidades da sua organização. Ao criar um atendedor automático de UM, você cria um sistema de menu de voz para a sua organização. Os chamadores de fora ou de dentro da organização podem navegar pelo sistema de menu para localizar e fazer ou transferir chamadas a usuários ou departamentos de sua organização.

Os chamadores podem navegar pelo sistema de menu usando um tom DTMF, também conhecido como discagem por tom ou entradas por voz. Para usar o ASR (Reconhecimento Automático de Fala), para que os usuários possam utilizar entradas de voz, você deve habilitar para fala o atendedor automático de UM.

Criar e usar atendedores automáticos é opcional na Unificação de Mensagens. Entretanto, se quiser criar um novo atendedor automático de UM, execute o seguinte procedimento.

## Criar um Atendedor Automático da UM

1.  
    
    No EAC, navegue até **Unificação de Mensagens** \> **Planos de discagem da UM**, selecione o plano de discagem da UM que deseja adicionar a um atendedor automático e clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").

2.  Na página **Plano de discagem da UM**, em **Atendedores automáticos da UM**, clique em **Adicionar**![Ícone Adicionar](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Ícone Adicionar").

3.  Na página **Novo Atendedor Automático da UM**, preencha as seguintes caixas:
    
      - **Nome**   Use essa caixa para criar o nome de exibição do atendedor automático de UM. O nome do atendedor automático da UM é necessário e deve ser exclusivo. Porém, ele é usado apenas para fins de exibição no EAC e no Shell.
        
        Se você precisar alterar o nome de exibição do atendedor automático depois da sua criação, primeiro exclua o atendedor automático de UM existente e depois crie outro atendedor com o nome apropriado. Se a sua organização usa vários atendedores automáticos de UM, convém usar nomes significativos para eles. O tamanho máximo do nome do atendedor automático de UM é 64 caracteres e pode incluir espaços.
        
        Embora seja possível nomear um novo atendedor automático da UM incluindo espaços, se você integrar a Unificação de Mensagens ao Office Communications Server 2007 R2 ou ao Microsoft Lync Server, o nome do atendedor automático não poderá incluir espaços. Sendo assim, se você criar um atendedor automático com espaços no nome de exibição, e se estiver fazendo a integração com o Office Communications Server 2007 R2 ou o Lync Server, primeiro exclua o atendedor automático e depois crie outro que não inclua espaços no nome de exibição.
    
      - **Criar este atendedor automático como habilitado**   Marque esta caixa de seleção para permitir que o atendedor automático atenda chamadas de entrada quando você concluir a criação do atendedor automático da UM. Por padrão, o novo atendedor automático é criado como desabilitado.
        
        Se você decidir criar o atendedor automático da UM como desabilitado, você pode usar o EAC ou o Shell para habilitar o atendedor automático após concluir a criação do atendedor automático.
    
      - **Configurar o atendedor automático para responder a comandos de voz**   Marque essa caixa de seleção para habilitar o atendedor automático de UM para voz. Se o atendedor automático for habilitado para fala, os chamadores poderão responder aos prompts do sistema ou a prompts personalizados usados pelo atendedor automático de UM usando entradas de discagem por tom ou voz. Por padrão, quando um atendedor automático é criado, não está habilitado para fala.
        
        Para que os chamadores usem um atendedor automático habilitado para fala em um idioma diferente do Inglês dos EUA (en-US), é necessário instalar o pacote de idioma da UM apropriado e configurar as propriedades do atendedor automático para usar esse idioma. O pacote de idioma da UM en-US é instalado por padrão quando você instala um servidor de caixa de correio.
    
      - **Números de acesso**   Use esta caixa para digitar os números de ramal ou de telefone que os chamadores utilizarão para acessar o atendedor automático. Digite um número de ramal ou telefone na caixa e clique em **Adicionar**![Ícone Adicionar](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Ícone Adicionar") para incluir o número na lista. A quantidade de dígitos no número de ramal ou telefone fornecido não precisa corresponder à quantidade de dígitos para um número de ramal configurado no plano de discagem de UM associado. Isso acontece porque atendedores automáticos de UM podem fazer chamadas diretas.
        
        O número de ramais ou de identificadores piloto que você pode inserir é ilimitado. Entretanto, você pode criar um novo atendedor automático sem listar um número de ramal ou de telefone. Não é obrigatório fornecer um número de ramal ou telefone.
        
        É possível editar ou remover um número de ramal ou identificador piloto existente. Para editar um número de ramal ou telefone existente, clique no botão **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição"). Para remover da lista um número de ramal ou telefone existente, clique no botão **Remover**![ícone Remover](images/JJ657492.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "ícone Remover").

4.  Clique em **Salvar**.

Voltar ao início

## Tarefas pós-implantação para Unificação de Mensagens

Após concluir uma nova instalação dos servidores de Acesso para Cliente e de Caixa de Correio e ter implementado com êxito a Unificação de Mensagens, você deverá concluir as tarefas de pós-implantação. Essas tarefas o ajudarão a habilitar usuários para a UM, proteger sua implantação de UM e implantar o recebimento de faxes para usuários habilitados para UM.

## Habilite os usuários para caixa postal

Após ter implantado os gateways VoIP ou IP PBXs, instalado os servidores de Acesso para Cliente e de Caixa de Correio e criado os componentes necessários para a Unificação de Mensagens, você deverá habilitar os usuários para a Unificação de Mensagens. Para obter detalhes, consulte [Habilitar um usuário para caixa postal](enable-a-user-for-voice-mail-exchange-2013-help.md).

## Caixa postal protegida

A Unificação de Mensagens pode ser configurada para usar o Active Directory Rights Management Services (AD RMS) para proteger as mensagens de voz de uma organização. Esse recurso é conhecido como Caixa Postal Protegida. Quando uma mensagem de voz é protegida, o destinatário não é bloqueado apenas de encaminhar a mensagem, mas a UM também assegura que somente o destinatário ou destinatários pretendidos da mensagem possam acessar seu conteúdo. As mensagens de voz protegidas podem ser acessadas usando o Microsoft Outlook 2010 ou posterior, Outlook Web App, ou o Outlook Voice Access. Para obter detalhes, consulte [Caixa postal protegida](protect-voice-mail-exchange-2013-help.md).

## Protocolo TLS mútuo para UM

Para usar o protocolo TLS mútuo para criptografar SIP e tráfego de RTP enviado e recebido pelos servidores de Acesso para Cliente e de Caixa de Correio, execute as seguintes tarefas:

  - Execute o Assistente de Certificado do Exchange. Para obter detalhes, consulte [Implantar certificados para Unificação de mensagens](deploying-certificates-for-um-exchange-2013-help.md).

  - Importe o certificado nos servidores de Acesso para Cliente e de Caixa de Correio.

  - Importe os certificados necessários nos gateways VoIP e no IP PBX e nos servidores de Acesso para Cliente e de Caixa de Correio de sua organização.

  - Configurar segurança de VoIP nos planos de discagem de UM. Para obter detalhes, consulte [Definir a configuração de segurança de VoIP](https://docs.microsoft.com/pt-br/exchange/voice-mail-unified-messaging/connect-voice-mail-system/configure-voip-security-setting).

  - Configure o modo de inicialização nos servidores de Acesso para Cliente e de Caixa de Correio. Para obter detalhes, consulte [Configurar o modo de inicialização em um servidor de caixa de correio](configure-the-startup-mode-on-a-mailbox-server-exchange-2013-help.md) e [Configurar o modo de inicialização em um servidor de acesso para cliente](configure-the-startup-mode-on-a-client-access-server-exchange-2013-help.md).

  - Configure os gateways IP de UM para escutar na porta 5061. Para mais detalhes, consulte [Configure a porta de escuta](https://docs.microsoft.com/pt-br/exchange/voice-mail-unified-messaging/connect-voice-mail-system/configure-listening-port).

## Políticas de PIN para usuários habilitados para UM

Em Unificação de Mensagens, as políticas de PIN são definidas e configuradas em uma política de caixa de correio de UM. Ao permitir que um usuário utilize a Unificação de Mensagens, você associa o usuário a uma política existente de caixa de correio de UM. As diretivas de PIN de UM configuradas na diretiva de caixa de correio de UM devem ser baseadas nos requisitos de segurança de sua organização. Para obter mais informações sobre como definir as configurações de PIN para usuários habilitados para UM, consulte [Definir segurança de PIN do Outlook Voice Access](set-outlook-voice-access-pin-security-exchange-2013-help.md).

## Configurar Recursos do Cliente de Caixa Postal

Depois de ter implantado seus servidores e os componentes da UM necessários, há vários recursos opcionais relacionados a caixa postal que você pode configurar. Para obter mais informações, consulte o seguinte:

  - [Configurando o Outlook Voice Access](https://docs.microsoft.com/pt-br/exchange/voice-mail-unified-messaging/set-up-client-voice-mail-features/set-up-outlook-voice-access)

  - [Permitir usuários de email encaminhar chamadas de voz](https://docs.microsoft.com/pt-br/exchange/voice-mail-unified-messaging/set-up-client-voice-mail-features/allow-voice-mail-users-to-forward-calls)

  - [Permitir que os usuários vejam uma transcrição do correio de voz](allow-users-to-see-a-voice-mail-transcript-exchange-2013-help.md)

  - [Permitir que os usuários de email de voz receber faxes](enable-voice-mail-users-to-receive-faxes-exchange-2013-help.md)


> [!IMPORTANT]
> Se você estiver integrando o seu ambiente de Unificação de Mensagens ao Microsoft Lync Server, há considerações de planejamento adicionais. Para obter detalhes, consulte <A href="deploying-exchange-2013-um-and-lync-server-overview-exchange-2013-help.md">Implantando a visão geral da Unificação de MENSAGENS do Exchange 2013 e Lync Server</A>.



Voltar ao início

