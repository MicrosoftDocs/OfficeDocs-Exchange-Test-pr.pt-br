---
title: 'Gerenciar um plano de discagem de Unificação de mensagens: Exchange 2013 Help'
TOCTitle: Gerenciar um plano de discagem de Unificação de mensagens
ms:assetid: a89735e4-36ec-49fb-ad0f-192fad37e801
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Bb124090(v=EXCHG.150)
ms:contentKeyID: 50486358
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
f1_keywords:
- Microsoft.Exchange.Management.SnapIn.Esm.Servers.UnifiedMessaging.DialPlanGeneralPropertyPage
ms.translationtype: MT
---

# Gerenciar um plano de discagem de Unificação de mensagens

 

_**Aplica-se a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Tópico modificado em:** 2018-04-26_

Depois de criar um plano de discagem de Unificação de mensagens (UM), você pode exibir e configurar uma variedade de configurações. Por exemplo, você pode configurar o nível de voz sobre IP (VoIP) de segurança, o codec de áudio e restrições de discagem. As configurações que você configurar em UM discagem plano afetam todos os usuários que estão vinculados ao plano de discagem através de uma diretiva de caixa de correio de Unificação de mensagens.

Para mais tarefas de gerenciamento relacionadas a planos de discagem de UM, consulte [Procedimentos de plano de discagem de UM](um-dial-plan-procedures-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: 5 minutos.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Planos de discagem da UM" no tópico [Permissões de mensagens unificadas](unified-messaging-permissions-exchange-2013-help.md).

  - Antes de executar esses procedimentos, confirme se um plano de discagem da UM foi criado. Para obter etapas detalhadas, consulte [Criar um plano de discagem de UM](create-a-um-dial-plan-exchange-2013-help.md).

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>..



## O que você deseja fazer?

## Usar o EAC para exibir ou definir configurações do plano de discagem da UM

1.  No EAC, navegue até **Unificação de Mensagens** \> **Planos de discagem de UM**.

2.  No modo de exibição de lista, selecione o plano de discagem de UM que você deseja modificar e clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").

3.  Na página de **Plano de discagem de UM**, clique em **Configurar**. Use as opções de configuração para exibir as configurações de plano de discagem específico e para habilitar ou desabilitar recursos conforme descrito nas etapas a seguir.

4.  **Geral**   Use esta página para exibir configurações de plano de discagem específicas ou habilitar ou desabilitar recursos para usuários habilitados para UM:
    
      - **Nome**    Este é o nome do plano de discagem que foi criado. O comprimento máximo de um nome de plano de discagem de Unificação de mensagens é de 64 caracteres e pode incluir espaços. No entanto, ele não pode incluir qualquer um dos seguintes caracteres: "/ \\ \[\]:; | = , + \* ? \< \>.
    
      - Embora você possa incluir espaços em um nome de plano de discagem de Unificação de mensagens, se você integrar a Unificação de mensagens com o Office Communications Server 2007 R2 ou Microsoft Lync Server, o nome do plano de discagem não pode incluir espaços. Portanto, se você criou um plano de discagem com espaços no nome de exibição e você estiver integrando com o Office Communications Server 2007 R2 ou o Lync Server, você deve primeiro exclua que plano de discagem e, em seguida, criar outro plano de discagem que não incluem espaços no nome de exibição.
        

        > [!IMPORTANT]
        > Embora a caixa para o nome do plano de discagem pode aceitar 64 caracteres, o nome do plano de discagem não pode ter mais de 49 caracteres. Se você tentar criar um nome de plano de discagem que contém mais de 49 caracteres, você receberá uma mensagem de erro. A mensagem será dizer que a diretiva de caixa de correio de Unificação de mensagens não pôde ser gerada porque o nome de plano de discagem de Unificação de mensagens é muito longo. Isso acontece porque, como mencionado anteriormente, quando você cria um plano de discagem uma diretiva de caixa de correio de Unificação de mensagens padrão denominada <EM>&lt;DialPlanName&gt;</EM> política padrão também será criada. Quando os 15 caracteres na política padrão são adicionados ao nome do plano de discagem, o total de caracteres exceder o limite. Planejar ao parâmetro <EM>name</EM> para ambas as situações de discagem de UM e política de caixa de correio de Unificação de mensagens pode ser 64 caracteres. No entanto, se o nome do plano de discagem for maior que 49 caracteres, o nome da diretiva de caixa de correio de Unificação de mensagens padrão será mais de 64 caracteres, e isso não é permitido.

    
      - **Comprimento da extensão (dígitos)**    Esse é o número de dígitos nos números de ramal para usuários que estão associados este plano de discagem. Por exemplo, se um usuário associado a um plano de discagem discar uma extensão de 4 dígitos para chamar o outro usuário no mesmo plano de discagem, selecione 4 como o número de dígitos no ramal.
        
        O número de dígitos para números de ramal baseia-se no plano de discagem de telefonia criado em um PBX IP ou PBX. Este é um campo obrigatório que tem um intervalo de valores de 1 a 20. O comprimento da extensão típico é de 3 por meio de 7 dígitos. Se o ambiente de telefonia existente incluir números de ramal, você deve especificar um número de dígitos que corresponde ao número de dígitos nestas extensões ao criar UM plano de discagem.
    
      - **Tipo de plano de discagem**    Um identificador de recurso uniforme (URI) é uma cadeia de caracteres que identifica ou nomes de um recurso. O principal objetivo dessa identificação é habilitar os dispositivos de VoIP e PBXs para se comunicar com outros dispositivos em uma rede usando os protocolos específicos. URIs são definidas em esquemas que definem uma sintaxe específica e o formato e os protocolos para a chamada. Em termos simples, neste formato é passado do PBX IP ou PBX e o tipo de plano de discagem que você criar deve corresponder a esse formato. Depois de criar um plano de discagem de Unificação de mensagens, não será possível alterar o tipo de plano de discagem sem excluir o plano de discagem e criar novamente o tipo de plano de discagem correto. Você pode selecionar um dos seguintes tipos de plano de discagem:
        
          - **Ramal de telefone**    Este é o tipo de plano de discagem mais comuns. As informações de terceiros de chamada e chamada do gateway VoIP ou IP Private Branch eXchange (PBX) são listadas em um dos seguintes formatos: Tel:512345 ou 512345 @\<*IP address*\>. Este é o tipo de padrão para planos de discagem.
        
          - **URI do SIP**    Se você deve ter um plano de discagem URI do protocolo de iniciação de sessão (SIP) como um PBX IP que ofereça suporte a roteamento SIP, e um PBX habilitado para SIP, ou se você estiver integrando Microsoft Office Communications Server 2007 R2 ou Microsoft Lync Server e Unificação de mensagens, use este tipo de plano de discagem. As informações de terceiros do chamada e de chamada do gateway VoIP. PBX IP, PBX com SIP habilitado, ou o Communications Server 2007 R2 ou do Lync Server está listado como um endereço SIP no seguinte formato: sip: \<*username*\> @\<*domain* ou *IP address*\>: porta.
        
          - **E. 164** e. 164 é um plano de numeração internacional para sistemas de telefonia pública na qual cada número atribuído contém um código de país, um código de destino nacional e um número de telefone do assinante. As informações de terceiros de chamada e chamado enviadas a partir do gateway VoIP e PBX ou PBX IP estão listadas no seguinte formato: Tel: + 14255550123.
        

        > [!TIP]
        > Após criar um plano de discagem, você não poderá alterar o tipo de plano de discagem sem excluir o mesmo e então recriar o tipo de plano de discagem correto.

    
      - **Modo de segurança de VoIP**   Use esta lista suspensa para selecionar a configuração de segurança de VoIP para o plano de discagem da UM. Você pode selecionar uma das seguintes definições de segurança para o plano de discagem:
        
          - **Não protegido**    Por padrão, quando você cria um plano de discagem de Unificação de mensagens, ele definiu para não criptografar o tráfego RTP ou a sinalização SIP. No modo não seguro, os servidores do Exchange associados a UM envio do plano de discagem em recebem dados dos gateways VoIP, IP PBXs, SBCs e outros servidores do Exchange usando sem criptografia. No modo não seguro, nem o canal de mídia em tempo real Transport Protocol (RTP) nem a informações de sinalização SIP é criptografada.
        
          - **SIP protegido**   Quando você seleciona **SIP protegido**, apenas o tráfego de sinalização SIP é criptografado e os canais de mídia RTP ainda usam TCP, que não é criptografado. Com SIP protegido, mútuo segurança de camada de transporte (TLS) é usado para criptografar o dados de VoIP e tráfego de sinalização do SIP.
        
          - **Seguro**    Quando você seleciona **Seguro**, o tráfego de sinalização SIP e os canais de mídia RTP são criptografados. Tanto o canal de mídia de sinalização que usa o SRTP (Protocolo de Transporte em Tempo Real Seguro) como o tráfego de sinalização do SIP usam TLS mútuo para criptografar os dados VoIP.

5.  **Códigos de discagem**    Use esta página para configurar os códigos de discagem para um plano de discagem de UM. Várias configurações de código de discagem podem ser configuradas no plano de discagem. Eles incluem as opções de chamada de entrada e saídas. Você pode configurar o seguinte:
    
      - **Códigos de discagem para chamadas de saída**    Use essas configurações para especificar os códigos de discagem para chamadas de saída que podem ser feitas pelos usuários habilitados para UM. Essas chamadas de saída são chamadas feitas com o Outlook Voice Access ou de uma mensagem de voz.
        
          - **Código de acesso de linha externo**    Use este campo para digitar o número ou números usados para acessar um número de telefone externo para chamadas externas. Esse número terão precedência sobre o número de telefone discado. Isso também é denominado um código de acesso do tronco. Este campo aceita de 1 a 16 dígitos. Para muitas organizações, esse número é 9. Por padrão, esse campo não estiver preenchido.
            
            Frequentemente, essa configuração é usada em ambientes de telefonia onde uma PBX ou PBX IP está localizado onsite ou mantido em uma organização. Ele não precisará ser configurada se o ambiente de telefonia da sua organização é mantido por um comerciais externos ou fornecedor.
        
          - **Código de acesso internacional**    Use este campo para digitar o código de número usado para acessar os números de telefone internacional para chamadas de saída. Esse número terão precedência sobre o número de telefone discado. Por padrão, esse campo não estiver preenchido. Este campo aceita de 1 a 4 dígitos. Por exemplo, o código de acesso internacional para os Estados Unidos é 011. Para Europa, ele 's 00.
        
          - **Prefixo de número nacional**    Use este campo para digitar o código de número usado para discar os números de telefone que estão fora de um código de área, mas com a país/região. Esse número terão precedência sobre o número de telefone discado. Por padrão, esse campo não estiver preenchido. Este campo aceita de 1 a 4 dígitos. Por exemplo, 0 é usado na Europa e 1 é usado na América do Norte.
        
          - **Código de país/região**    Use este campo para digitar o número de código de país/região usado para chamadas de saída. Esse número terão precedência sobre o número de telefone discado. Por padrão, esse campo não estiver preenchido. Este campo aceita de 1 a 4 dígitos. Por exemplo, nos Estados Unidos, o código de país/região é 1. No Reino Unido, ele 's 44.
    
      - **Formatos de número para discagem entre planos de discagem de UM**   Use essas definições para configurar chamadas entre usuários em planos de discagem separados quando eles fizerem chamadas entre os planos de discagem.
        
          - **Formato de número do país/região**    Use este campo para especificar como o número de telefone do usuário deve ser discado pelos servidores Exchange quando os usuários estiverem em um plano de discagem diferentes que tem o mesmo código de país. Isso é usado pelo atendedores automáticos e quando um usuário de acesso de voz Outlook procura e tenta chamar o usuário no diretório.
            
            Essa entrada consiste em um prefixo e um número variável de caracteres (por exemplo, 020*xxxxxxx*). Para determinar o número de telefone, a Unificação de Mensagens irá colocar os últimos *x* dígitos do número de telefone especificado no diretório para o prefixo especificado.
        
          - **Formato de número internacional**    Use este campo para especificar como o número de telefone do usuário deve ser discado pela Unificação de mensagens quando os usuários estão em planos de discagem diferentes que possuem códigos de país diferente. Isso é usado por um atendedor automático e quando um usuário de acesso de voz Outlook procura e tenta chamar o usuário no diretório.
            
            Essa entrada consiste em um prefixo de número e um número variável de caracteres (por exemplo, 4420*xxxxxxx*). Para determinar o número de telefone, a Unificação de mensagens irá acrescentar os dígitos *x* últimos em relação ao número de telefone especificado no diretório ao prefixo especificado.
        
          - **Formatos de número para chamadas de entrada no mesmo plano de discagem**    Use este campo para adicionar ou remover um formato de número de chamadas de entrada que são colocados entre usuários no mesmo plano de discagem. Este campo aceita os números e a letra "x" como um caractere curinga. Não há outras letras podem ser usadas neste campo.
            
            Para chamadas de entrada no mesmo plano de discagem, adicione um formato de número. Por exemplo, para adicionar um formato de número para extensões de 5 dígitos, insira, 142570xxxxx e clique em ![Ícone Adicionar](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Ícone Adicionar"). Para remover um formato de número, clique em ![ícone Remover](images/JJ657492.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "ícone Remover").

6.  **Outlook Voice Access**    Use esta página para definir configurações do Outlook Voice Access para UM plano de discagem. Outlook Acesso de voz permite que os usuários acessem suas caixas de correio individuais para recuperar mensagens de voz, email, contatos e informações de calendário usando um telefone. Você pode exibir ou configurar o seguinte:
    
      - **Saudação de boas-vindas**   Esse campo somente exibição mostra o nome do arquivo de som que será usado para a saudação de boas-vindas.
        
          - **Padrão de saudação**    A saudação de boas-vindas é usada quando um usuário do Outlook Voice Access ou outro chamador liga para o número do Outlook Voice Access e um diretório de pesquisa. Esse arquivo de áudio é a saudação de padrão de um plano de discagem de UM. No entanto, convém alterar essa saudação de boas-vindas e oferecem boas-vindas de saudação específico para sua empresa, como outro, "Bem-vindo à Outlook Voice Access para Contoso, Ltd."
            
            Se você decidir personalizar esta saudação, você deve primeiro gravar a saudação personalizada, salvá-lo como um arquivo. wav e, em seguida, configure o plano de discagem para usar essa saudação personalizada. O nome do arquivo e o caminho não devem exceder 255 caracteres.
            
            Você pode adicionar uma saudação personalizada clicando em **Alterar** e, em seguida, clicando em **Procurar** para selecionar uma saudação personalizada gravada anteriormente e especificar o arquivo de áudio (. wav) a ser usado para a saudação de boas-vindas. Se você não especificar um arquivo de áudio, os usuários do Outlook Voice Access ouvirá um padrão de saudação de boas-vindas que diz "Bem-vindo, você está conectado ao Microsoft Exchange."
    
      - **Informe**    Quando habilitada, essa gravação opcional reproduz imediatamente após a empresa ou saudação de boas-vindas do horário não comercial. Um informe poderá informar que políticas de segurança da organização para acessar o sistema, como, por exemplo, "quando você obter acesso a nossa system usando o Outlook Voice Access, você concordou com os termos do contrato de negócios e aplicam todas as diretivas de segurança para a nossa organização. Acesso ao nosso sistema é monitorado e que tenha acesso ilegal será processado." Um Informe também pode fornecer informações que é necessário para conformidade com a política da empresa, por exemplo, "Chamadas podem ser monitoradas para fins de treinamento." Se for importante que os chamadores ouvem o informe toda, ele pode ser marcado como ininterrupto.
        
        Por padrão, não há nenhuma informe configurado em planos de discagem de Unificação de mensagens. Para habilitar um informe e usar um arquivo de áudio personalizado específico para sua organização, clique em **Alterar** e, em seguida, clique em **Procurar**.
    
      - **Permitir que o comunicado seja interrompida**    Marque esta caixa de seleção para permitir que o usuário do Outlook Voice Access interrompam o informe. Você deve fazer isso se você possui comunicados longos informativos. Os usuários do Outlook Voice Access poderão ficar desapontados se o informe for longo e eles não podem interrompê-lo para acessar as opções fornecidas por UM plano de discagem.
    
      - **Números do Outlook Voice Access**    Use este campo para adicionar um telefone ou ramal ou um URI do SIP que um usuário do Outlook Voice Access chamará para acessar o sistema de correio de voz utilizando Outlook Voice Access. Na maioria dos casos, você pode inserir um número de ramal ou um número de telefone externo. No entanto, pois este campo aceita todos os caracteres alfanuméricos, um URI do SIP pode ser usado se você estiver usando um PBX IP, Office Communications Server 2007 R2 ou Microsoft Lync Server.
        
        Por padrão, quando um plano de discagem é criado, são definidos sem números do Outlook Voice Access. Para permitir que os usuários do Outlook Voice Access façam chamadas no Outlook Voice Access, você deve configurar pelo menos um número de telefone. O número de caracteres alfanuméricos não pode exceder 20.
        
        Quando você configurar esse número no plano de discagem, ele será exibido no Microsoft OfficeOutlook 2007 ou versões posteriores e no Outlook Web App para opções da caixa postal.
        
        Para adicionar um novo número do Outlook Voice Access, insira o número na caixa e clique em ![Ícone Adicionar](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Ícone Adicionar"). Para remover um número do Outlook Voice Access, clique em ![ícone Remover](images/JJ657492.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "ícone Remover").

7.  **Configurações**    Use esta página para definir as configurações de plano de discagem para Unificação de mensagens. Quando você define as configurações nessa página, você pode controlar como os usuários do Outlook Voice Access e os chamadores externos ligações para um atendedor automático vinculado ao plano de discagem localizam usuários em sua organização, o codec de áudio que é usado para mensagens de caixa postal, o número de falhas de entrar e valores de tempo limite. Você pode configurar o seguinte:
    
      - **Principal maneira de procurar nomes**   Use essa lista para selecionar a forma principal de os chamadores localizarem um usuário ao discarem no sistema.
        
        Por padrão, o **Último primeiro** está selecionada. Isto significa que quando os usuários estão pesquisando um usuário no diretório, eles serão digitar sobrenome do usuário primeiro e, em seguida, o primeiro nome.
        
        Quando um usuário do Outlook Voice Access liga para um número do Outlook Voice Access para acessar sua caixa de correio, um chamador liga para um número do Outlook Voice Access para realizar uma pesquisa de diretório ou liga para um atendedor automático vinculado a um plano de discagem de UM. Ele pode pesquisar um usuário no diretório soletrando seu nome ou alias.
        
        Você deve selecionar um dos métodos suportados para poder usar o método principal de discagem por nome. Há suporte para os seguintes métodos:
        
          - **Sobrenome Nome (padrão)**
        
          - **Nome Sobrenome**
        
          - **Endereço SMTP**
    
      - **Modo secundário de procurar nomes**   Use essa lista para selecionar a forma secundária de os chamadores localizarem um usuário ao discarem no sistema.
        
        Por padrão, o **endereço SMTP** está selecionada. Isso significa que quando os usuários pesquisarem um usuário no diretório, eles serão digitar o alias de email do usuário ou o endereço SMTP.
        
        Quando um usuário do Outlook Voice Access chama um número do Outlook Voice Access para acessar suas caixas de correio, um chamador chama um número do Outlook Voice Access para executar uma pesquisa de diretório ou um chamador chama um atendedor automático vinculado a um plano de discagem de UM, eles podem procurar por um usuário no diretório por seus nomes ou o alias de ortografia. Quando você seleciona uma destas opções, os chamadores podem usar a principal maneira de pesquisar nomes ou o modo secundário para procurar nomes para localizar usuários no diretório.
        
        Não é necessário selecionar um dos quatro métodos que são suportados. No entanto, se você não marcar uma maneira secundária para procurar usuários, os chamadores receberá apenas uma maneira de pesquisar por um usuário. As seguintes opções estão disponíveis:
        
          - **Sobrenome Nome**
        
          - **Nome Sobrenome**
        
          - **Endereço SMTP** (padrão)
        
          - **Nenhum**
    
      - **Codec de áudio**    Use esta lista para selecionar o codec de áudio que será usado pelo plano de discagem. Quando um chamador faz uma chamada para um usuário que está associado com o plano de discagem e deixa uma mensagem de voz da Unificação de mensagens usa o codec de áudio que você selecionar dessa lista para mensagens de voz de registro que serão enviadas aos usuários habilitados para email de voz. Os seguintes codecs de áudio são suportados:
        
          - **MP3** (padrão)
        
          - **WMA** (Windows Media Audio)
        
          - **G711** (Pulse Code Modulation (PCM) Linear)
        
          - **GSM** (Group System Mobile 06.10)
        
        Por padrão, o formato MP3 está selecionado. O formato de MP3 é um formato de arquivo de áudio comum que é usado para reduzir significativamente o tamanho do arquivo de áudio e é mais comumente usado pelos dispositivos de áudio pessoais ou MP3 players. MP3 é um tipo de plataforma cruzada de codec de áudio e é usado para compatibilidade com muitos telefone celular e dispositivos e vários sistemas operacionais de computador.
        
        WMA é usado porque ele é altamente compactado e tem as propriedades de formato de alta qualidade. G. 711 PCM Linear é um formato de codec de áudio de qualidade de telefone que é o menos compactado e tem o formato de qualidade inferior. GSM 06.10 é um formato de codec de áudio que é usado pelos fornecedores de telefone celular e é o padrão para serviços de celular digital.
        
        Se você estiver preocupado com as cotas de disco dos usuários, selecione WMA como o codec de áudio. Arquivos de voz salvos no formato. wma são aproximadamente metade do tamanho da gravação de voz mesmo feita usando um dos outros codecs de áudio.
    
      - **Ramal do operador**    Use esta caixa de texto para inserir o número de telefone ou um número de ramal para o operador do plano de discagem. Isso é diferente de uma extensão do operador que está configurada em um atendedor automático. No entanto, você pode colocar o mesmo número de telefone ou ramal para ambos os tipos de operadores.
        
        Você pode configurar essa definição para transferir chamadas para um atendedor automático se houver um configurado, para um operador, para números de telefone externos ou para números de ramais.
        
        Quando um chamador que está usando o teclado do telefone pressionar 0 ou disser "recepção" ou "operador," ou o limite do **Número de falhas de entrada antes de desconectar** for excedido, o chamador será transferido para o número de telefone ou o número de ramal especificado nessa caixa de texto.
        
        Esse número de telefone pode ser um número externo para a organização ou um número de ramal de telefone interno. Por exemplo, se o número do ramal do operador ou recepcionista é 81964 e sua organização tiver apenas um plano de discagem, digite 81964.
        
        Por padrão, essa configuração está em branco. Se você não inserir um número na caixa de texto, a capacidade de transferir chamadas para o operador está desabilitada e os chamadores são desconectados educadamente porque não há ninguém para atender à chamada.
        
        É recomendável que você preencha essa caixa de texto com um número de telefone que transfira os chamadores para a recepção, caso não localizem um determinado usuário no diretório.
    
      - **Número de falhas de entrada antes de desconectar**   Use essa caixa de texto para inserir o número de tentativas de logon sequenciais malsucedidas permitidas antes de um chamador ser desconectado.
        
        O valor dessa configuração pode ser de 1 a 20. A definição desse valor muito baixo pode frustram os usuários. Na maioria das organizações, este valor deve ser definido como o padrão de três tentativas.
    
      - **Tempos limite e repetições**   Essas configurações se aplicam aos usuários do Outlook Voice Access e a chamadores externos que ligam para um atendedor automático de UM.
        
          - **Máximo de chamadas duração (minutos)**    Use esta caixa de texto para digitar o número máximo de minutos que uma chamada de entrada pode ser conectada ao sistema sem que está sendo transferida para um número de ramal válido antes que a chamada é encerrada. Na maioria das organizações, este valor deve ser definido como o padrão de 30 minutos.
            
            Essa configuração se aplica a todos os tipos de chamadas. Isso inclui as chamadas recebidas do Outlook Voice Access, chamadas de voz interno para sua organização e voz e fax de entrada chama externo à sua organização.
            
            O valor dessa configuração pode ser entre 10 e 120. A definição desse valor muito baixo pode causar chamadas recebidas sejam desconectados antes que sejam concluídas. Por exemplo, se sua organização recebe mensagens de fax grande muitos, convém considerar o aumento desse valor do padrão para que todas as páginas para mensagens de fax são recebidas.
        
          - **Máximo de gravação duração (minutos)**    Use esta caixa de texto para digitar o número máximo de minutos permitido para cada gravação quando um chamador deixar uma mensagem de voz de voz. Na maioria das organizações, este valor deve ser definido como o padrão de 20 minutos.
            
            O valor dessa configuração pode ser de 1 a 100. A definição desse valor muito baixo pode causar mensagens de voz long sejam desconectados antes que sejam concluídas. A definição desse valor muito alto permite que os usuários a salvar mensagens de voz longos em suas caixas de entrada.
            
            Essa configuração é importante se você tiver implementado as cotas de disco estrito para usuários. Este valor deve ser menor do que o valor definido para a configuração **máximo chamada duração (minutos)**.
        
          - **Gravação de tempo limite ocioso (segundos)**    Use esta caixa de texto para inserir o número de segundos de silêncio que o sistema permite quando uma mensagem de voz está sendo registrada antes que a chamada é encerrada. Na maioria das organizações, este valor deve ser definido como o padrão de 5 segundos.
            
            O valor dessa configuração pode ser entre 2 e 10. A definição desse valor muito baixo pode causar o sistema desconectar chamadores antes que tenham terminado deixando suas mensagens de voz. A definição desse valor muito alto permite silencia longas em mensagens de voz.
        
          - **Número de falhas de entrada antes de se desconectar**    Use esta caixa de texto para configurar o número de vezes que os chamadores podem digitar escolhas de menu incorretas antes que elas são desconectadas. Na maioria das organizações, este valor deve ser definido como o padrão de três tentativas. Esta é uma configuração importante para planos de discagem de Unificação de mensagens habilitado para fala.
            
            Exemplos de dados incorretos incluem quando um chamador solicita um número de ramal que não é encontrado no sistema, o sistema não consegue localizar o número de ramal do usuário para transferir a chamada ou o chamador pressiona uma opção de menu que não é válida.
            
            O valor dessa configuração pode estar entre 1 e 20. A configuração de um valor muito baixo pode desconectar prematuramente o chamador.
    
      - **Idioma de áudio**    Use essa lista para especificar o idioma padrão a ser utilizado pelos usuários do Outlook Voice Access. Essa configuração não se aplica a configuração do idioma em um atendedor automático. Você pode definir o idioma do Outlook Voice Access a ser igual ou diferente do idioma usado em um atendedor automático. Quando um usuário faz uma chamada para um usuário que está vinculada com um plano de discagem, o idioma de áudio é o idioma padrão que usa o operador registradas de voz. Os prompts de sistema que os chamadores ouvem são executados no mesmo idioma. O idioma escolhido em UM plano de discagem é usado para ler email, caixa postal e itens de calendário; o nome do usuário que informa se um pessoal saudação não foi registrada; transcrever uma mensagem de voz usando o recurso de visualização da caixa postal; e habilitar o reconhecimento de fala automático (ASR) funcione corretamente.
        
        Para implantações de local, adicionar outras linguagens permite Outlook Voice Access usar um idioma diferente do inglês (EUA). Por exemplo, se um usuário do Outlook Voice Access chama usando um número do Outlook Voice Access de um telefone de mesa, o usuário é recebido com voz do operador de um pré-gravado em inglês. Mesmo se o mesmo usuário seleciona um idioma diferente, como francês, em Outlook Web App, os menus ainda são lidas em inglês dos EUA. Para o usuário possa ouvir os menus de operador pré-gravado em francês, você deve instalar o pacote de idiomas apropriado.
        

        > [!TIP]
        > Todos os idiomas estão disponíveis para o Exchange Online.



8.  **Regras de discagem**    Use esta página para especificar as regras de discagem para chamadas de país/região e internacionais feitas pelos usuários habilitados para UM. Cada entrada definida na regra de discagem determina os tipos de chamadas que os usuários dentro de um grupo de regras de discagem específicas podem fazer. Depois de usar a página de **regras de discagem** para configurar as regras de discagem, você deve configurar UM plano de discagem, uma política de caixa de correio de Unificação de mensagens ou um atendedor automático de UM para usar a regra de discagem apropriada. Após configurar a diretiva de caixa de correio de Unificação de mensagens para usar um grupo de regras de discagem, as restrições de discagem configuradas se aplicam a todos os usuários habilitados para Unificação de mensagens que estão associados a diretiva de caixa de correio de Unificação de mensagens. Por exemplo, você pode configurar um grupo de regras de discagem que não exija a usuários que estão associados com o plano de discagem para discar um código de acesso de linha externa, quando eles realiza uma chamada para um número de telefone do país/região. Você pode configurar o seguinte:
    
      - **Regras de discagem do país/região**    Use esta caixa para adicionar, remover ou editar grupos de regras de discagem do país/região usados por políticas de caixa de correio de Unificação de mensagens. Para criar uma regra de discagem, clique em ![Ícone Adicionar](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Ícone Adicionar"). Para editar uma regra de discagem existente, clique em ![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição"). Para remover uma regra de discagem, clique em ![ícone Remover](images/JJ657492.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "ícone Remover"). Quando você cria uma regra de discagem, adicione as seguintes informações na página **nova regra de discagem**:
        
          - **Nome da regra de discagem**    Use esta caixa de texto para digitar o nome da regra de discagem que você está criando. Você pode usar o mesmo nome para coletar várias regras em um grupo e, em seguida, habilitar ou desabilitá-los em **autorização de discagem**. O nome pode ter até 32 caracteres.
        
          - **Padrão de número para transformar (máscara de número)**    Use esta caixa de texto para inserir o padrão de número para transformar antes de discar, por exemplo, 91425xxxxxxx. Se um usuário insere um número que corresponde a este padrão, a Unificação de mensagens transformará o número discado em um número discado antes de fazer a chamada. Você só pode inserir números e o caractere curinga, "x".
        
          - **Número de Dialed**    Use esta caixa de texto para digitar o número que você deseja discar que coincida com o padrão numérico que você definir no **padrão de número para transformar (máscara de número)**. O número discado é usado para determinar a cadeia de caracteres de discagem reais enviada para o gateway VoIP ou IP PBX. Esse número pode ser diferente do número obtido pela Unificação de mensagens para a chamada de saída. No entanto, seu PBX ou PBX IP também pode ser configurada para omitir o código de área para chamadas locais e pode ser configurada para planos de numeração de voz privada. Nenhum caractere curinga (*x*) na sequência de discagem é substituído pelos dígitos do número original que foram correspondidos pela máscara na regra de discagem do número. Um exemplo de um número discado válido é 9*xxxxxxx*. Este campo pode conter apenas números e o caractere *x*.
        
          - **Comentário**    Use esta caixa de texto para colocar em um comentário ou uma descrição para a regra de discagem que você está adicionando ou modificando. Por padrão, esta caixa de texto está em branco.
            

            > [!TIP]
            > Se você estiver integrando com o Office Communications Server 2007 R2 ou Microsoft Lync Server, você provavelmente encontrará desnecessárias para configurar as regras de discagem ou grupos de regras de discagem na Unificação de mensagens. Office Communications Server 2007 R2 e o Lync Server foram projetados para executar o roteamento de chamadas e conversão de número de usuários em sua organização e também fará isso quando as chamadas são feitas em nome de usuários.

    
      - **Regras internacionais**   Use essa caixa de texto para adicionar, remover ou editar grupos de regras de discagem internacional usados pelas diretivas de caixa de correio da UM.
        
          - **Nome da regra de discagem**    Use esta caixa de texto para digitar o nome da regra de discagem que você está criando. Você pode usar o mesmo nome para coletar várias regras em um grupo e, em seguida, habilitar ou desabilitá-los em **autorização de discagem**. O nome pode ter até 32 caracteres.
        
          - **Padrão de número para transformar (máscara de número)**    Use esta caixa de texto para inserir o padrão de número para transformar antes de discar, por exemplo, 91425xxxxxxx. Se um usuário insere um número que corresponde a este padrão, a Unificação de mensagens transformará o número discado em um número discado antes de fazer a chamada. Você só pode inserir números e o caractere curinga, "x".
        
          - **Número de Dialed**    Use esta caixa de texto para digitar o número que você deseja discar que coincida com o padrão numérico que você definir no **padrão de número para transformar (máscara de número)**. O número discado é usado para determinar a cadeia de caracteres de discagem reais enviada para o gateway VoIP ou IP PBX. Esse número pode ser diferente do número obtido pela Unificação de mensagens para a chamada de saída. No entanto, seu PBX ou PBX IP também pode ser configurada para omitir o código de área para chamadas locais e pode ser configurada para planos de numeração de voz privada. Nenhum caractere curinga (*x*) na sequência de discagem é substituído pelos dígitos do número original que foram correspondidos pela máscara na regra de discagem do número. Um exemplo de um número discado válido é 9*xxxxxxx*. Este campo pode conter apenas números e o caractere *x*.
        
          - **Comentário**    Use esta caixa de texto para colocar em um comentário ou uma descrição para a regra de discagem que você está adicionando ou modificando. Por padrão, esta caixa de texto está em branco.
            

            > [!TIP]
            > Para implantações de local, se você estiver integrando com o Office Communications Server 2007 R2 ou Microsoft Lync Server, você provavelmente encontrará desnecessárias para configurar as regras de discagem ou grupos de regras de discagem na Unificação de mensagens. Office Communications Server 2007 R2 ou o Lync Server foram projetados para executar o roteamento de chamadas e conversão de número de usuários em sua organização e também fará isso quando as chamadas são feitas em nome de usuários.



9.  **Autorização de discagem**    Use esta página para selecionar as regras de discagem para chamadores que ligam para um número do Outlook Voice Access configurado em um plano de discagem de UM. Você pode restringir o tipo de chamadas feitas pelos chamadores quando um usuário não autenticado ou um usuário de acesso de voz Outlook chama para um número do Outlook Voice Access configurado em um plano de discagem, configurando grupos de regras de discagem e restrições de discagem. Você pode configurar o seguinte:
    
      - **Chamadas em UM mesmo plano de discagem**    Marque essa caixa de seleção para permitir que os usuários que ligam para um número do Outlook Voice Access configurado em um plano de discagem colocar ou transferir chamadas para um número de ramal associado a um usuário habilitado para UM que esteja no mesmo plano de discagem. Por padrão, essa configuração estiver habilitada.
        
        Quando você desabilitar essa configuração, os usuários que ligam para o número do Outlook Voice Access não poderá colocar ou transferir chamadas para todos os usuários que não são habilitados para Unificação de mensagens, para outros números de ramal ou aos usuários habilitados para UM associados com o mesmo plano de discagem. Isso ocorre porque a configuração **Permitir chamadas para qualquer extensão** está desabilitada por padrão.
    
      - **Permitir chamadas para qualquer extensão**    Quando essa configuração está desabilitada, os usuários que ligam para um número do Outlook Voice Access no plano de discagem não podem fazer chamadas para usuários que não são habilitados para UM ou outros números de extensão não associados a um usuário habilitado para UM. No entanto, eles podem fazer uma chamada ou transferir uma chamada para os números de ramal associados a usuários habilitados para UM. Isso ocorre porque a configuração de **chamadas no mesmo plano de discagem de Unificação de mensagens** é habilitada por padrão. A configuração **Permitir chamadas para qualquer extensão** está desabilitada por padrão.
        
        Quando essa configuração estiver habilitada, os usuários que ligam para um número do Outlook Voice Access configurado no plano de discagem podem fazer chamadas para usuários que não estão habilitados, para outros números de extensão não associados a um usuário habilitado para Unificação de mensagens e para usuários habilitados para UM. Isso ocorre porque a configuração de **chamadas no mesmo plano de discagem de Unificação de mensagens** é habilitada por padrão.
        
        Você pode habilitar essa configuração em um ambiente onde nem todos os usuários tiverem sido habilitados para UM. Essa configuração também é útil quando você deseja permitir que os usuários que ligam para um número do Outlook Voice Access configurado em um plano de discagem para chamar números de ramal que não estão associados.
    
      - **Autorizado a grupos de regras de discagem do país/região**    Use esta seção para adicionar ou remover as regras de discagem do país/região permitidos. Por padrão, não há nenhuma regras de discagem do país/região configuradas em planos de discagem de Unificação de mensagens.
        
        Grupos de regras de discagem do país/região são usados para permitir ou restringir os números de telefone dentro de um país ou região que qualquer usuário que tenha discaram para o número de acesso do assinante pode discar. Isso ajuda a evitar telefonemas desnecessárias ou não autorizadas e encargos.
        
        Para adicionar regras de discagem do país/região, você deve primeiro criar a regra de discagem do país/região apropriada no plano de discagem e, em seguida, adicione as entradas de regra de discagem apropriado na regra de discagem. Depois de criar as regras de discagem necessários no plano de discagem, você deve adicionar, em seguida, a regra de discagem à lista de autorizações de discagem na página de **autorização de discagem** no plano de discagem.
        
        Grupos de regras de discagem do país/região podem ser usados para permitir ou restringir o acesso aos números de telefone dentro de um país ou região. Isso é aplicado a todos os usuários que ligou para um número do Outlook Voice Access.
    
      - **Autorizado a grupos de regras de discagem internacional**    Use esta seção para adicionar ou remover as regras de discagem internacional permitidos. Por padrão, não há nenhuma regras de discagem internacional configuradas em planos de discagem de Unificação de mensagens.
        
        As regras de discagem internacional são usadas para permitir ou restringir os números de telefone fora de um país ou região que qualquer usuário que tenha discaram para o número do Outlook Voice Access pode discar. Isso ajuda a evitar telefonemas desnecessárias ou não autorizadas e encargos.
        
        Para adicionar internacional discando de grupos de regras, você deve primeiro criar as regras de discagem internacional apropriado no plano de discagem e, em seguida, adicione as entradas de regra de discagem apropriado. Depois de criar as regras de discagem necessários no plano de discagem, você deve adicionar, em seguida, a regra de discagem à lista de autorizações de discagem na página de **autorização de discagem** no plano de discagem.
        
        International grupos de regras de discagem pode ser usado para permitir ou restringir o acesso aos números de telefone fora de um país ou região. Isso é aplicado a todos os usuários que ligou para um número do Outlook Voice Access.

10. **Pesquisa e transferência**    Use esta página para configurar os recursos de plano de discagem de Unificação de mensagens. Vários recursos podem ser configurados em UM plano de discagem. Eles incluem transferindo chamadas, enviar mensagens de voz e pesquisa para usuários. Você pode configurar o seguinte:
    
      - **Permitir que chamadores**    Use estas configurações para determinar como os usuários que ligam para um número do Outlook Voice Access podem contatar os usuários. Você pode configurar o seguinte:
        
          - **Transferir para usuários**    Marque esta caixa de seleção para permitir que os usuários do Outlook Voice Access transferir chamadas para usuários. Por padrão, essa opção está habilitada. Isso permite que os usuários associados com as chamadas de transferência do plano de discagem aos usuários em UM mesmo plano de discagem. Após você marcar essa caixa de seleção, você pode definir o grupo de usuários que os chamadores podem procurar selecionando a opção apropriada na seção **Permitir que chamadores procurar usuários por nome ou alias** nesta página.
            
            Se esta opção for desabilitada, o Outlook Voice Access não permitirá que os chamadores sejam transferidos para nenhum usuário no plano de discagem.
        
          - **Deixar as mensagens de voz sem precisar ligar o telefone de um usuário**    Marque esta caixa de seleção para permitir que os chamadores enviar mensagens de voz aos usuários. Por padrão, essa opção está habilitada. Isso permite que os usuários do Outlook Voice Access que estão associados com as mensagens de voz de envio da plano de discagem aos usuários no mesmo plano de discagem de Unificação de mensagens. Após você marcar essa caixa de seleção, você pode definir o grupo de usuários que os chamadores podem procurar selecionando a opção apropriada na seção **Permitir que chamadores procurar usuários por nome ou alias** nesta página.
            
            Se esta opção for desabilitada, o Outlook Voice Access não convidará chamadores a enviar uma mensagem de voz durante uma solicitação do sistema.
    
      - **Permitir que os chamadores para procurar usuários por nome ou alias**    Use essas opções para determinar um agrupamento de usuários que podem ser pesquisados. Por padrão, a **Este plano de discagem** opção está selecionada. No entanto, você pode alterar o agrupamento de usuários. Escolha entre as seguintes opções:
        
          - **Neste plano de discagem apenas**   Use esta opção para permitir que os chamadores que se conectarem ao Outlook Voice Access localizem e entrem em contato com usuários que estão no plano de discagem de que são um membro.
        
          - **Em toda a organização**    Use esta opção para permitir que os chamadores que se conectam ao Outlook Voice Access para localizar e contatar qualquer pessoa que está listado em toda a organização. Isso inclui todos os usuários que foram habilitados para caixa de correio ou usuários habilitados para UM em todos os planos de discagem.
        
          - **Somente neste atendedor automático**    Use esta lista para permitir que os usuários do Outlook Voice Access me conectar a um atendedor automático e, em seguida, potencialmente se conectar a outro atendedor você configurou. Você deve criar este atendedor automático para permitir que os chamadores a ser transferida para outro atendedor automático especificado.
        
          - **Somente para essa extensão**    Use esta opção para permitir que os usuários do Outlook Voice Access para se conectar a um número de ramal especificadas no campo para essa opção. Este campo aceita apenas os dígitos numéricos. O número de dígitos que você define neste campo deve corresponder ao número de dígitos configurados no plano de discagem associado com o atendedor automático.
    
      - **Informações a serem incluídas para usuários com o mesmo nome**    Use este campo para selecionar como o plano de discagem diferencia entre os usuários que têm os nomes iguais ou semelhantes. Quando um chamador é solicitado a digitar letras ou diga o nome da pessoa para localizar um usuário específico na organização, às vezes, mais de um nome faz a correspondência de entrada do chamador. Se houver dois usuários com o mesmo nome, a Unificação de mensagens usará uma das seguintes maneiras para adicionar informações adicionais para o nome do usuário. Por exemplo, se você selecionar **departamento**, quando um usuário do Outlook Voice Access chama no Outlook Voice Access e pesquisas de um usuário e existem nomes semelhantes ou duplicados no diretório, o chamador escutará nome do usuário e o departamento, por exemplo:
        
        1.  Sistema: "Bem-vindo ao Outlook Voice Access. Insira seu PIN e pressione a tecla de cerquilha."
        
        2.  O chamador insere seu PIN seguido da tecla \#.
        
        3.  Sistema: "Please disser caixa postal, email, calendário, contatos pessoais, diretório ou opções pessoais".
        
        4.  Chamador: "diretório"
        
        5.  Sistema: "pesquisa de diretório. Por favor, observe, das seguintes tarefas do sistema exige que você use o teclado do telefone em vez de falando. Usar o teclado numérico para digitar o nome da pessoa que você está tentando localizar, sobrenome em primeiro lugar, ou para a primeira parte do seu endereço de email de ortografia, pressione a tecla de cerquilha duas vezes, se você souber a extensão, pressione a tecla de cerquilha."
        
        6.  Chamador usa o teclado e entradas "smithtony" e pressiona a tecla \#.
        
        7.  Sistema: "de Tony Smith, research, pressione 1. De Tony Smith, administração, pressione 2. De Tony Smith, suporte técnico, pressione 3".
        
        8.  O chamador pressiona a tecla apropriada no teclado, e a chamada é transferida ao usuário.
        
        Por padrão, todos os atendedores automáticos de UM associado a este plano de discagem herdam essa configuração. No entanto, você pode alterar essa configuração em cada atendedor automático que criar.
        
        Selecione um dos seguintes métodos para fornecer aos chamadores mais informações para ajudar a localizar o usuário correto na organização:
        
          - **Nenhum**    Nenhuma informação adicional é fornecida quando as correspondências são listadas. Por padrão, esse método está selecionado.
        
          - **Cargo**   O sistema de caixa postal inclui o cargo de cada usuário quando as correspondências são listadas.
        
          - **Departamento**   O sistema de caixa postal inclui o departamento de cada usuário quando as correspondências são listadas.
        
          - **Localidade**   O sistema de caixa postal inclui a localidade de cada usuário quando as correspondências são listadas.
        
          - **Prompt por Alias**   O sistema de caixa postal solicita ao chamador o alias do usuário.

11. Depois de definir as configurações solicitadas, clique em **Salvar** para salvar suas alterações.

## Usar o Shell para definir configurações do plano de discagem da UM

Este exemplo configura um plano de discagem da UM denominado `MyDialPlan` para usar 9 como código de acesso à linha externa.

    Set-UMDialplan -Identity MyDialPlan -OutsideLineAccessCode 9

Este exemplo configura um plano de discagem da UM denominado `MyDialPlan` para usar uma saudação de boas-vindas.

    Set-UMDialplan -Identity MyDialPlan -WelcomeGreetingEnabled $true -WelcomeGreetingFilename welcome.wav

Este exemplo configura um plano de discagem da UM denominado `MyDialPlan` com regras de discagem.

    $csv=import-csv "C:\MyInCountryGroups.csv"
    Set-UMDialPlan -Identity MyDialPlan -ConfiguredInCountryGroups $csv
    Set-UMDialPlan -Identity MyDialPlan -AllowedInCountryGroups "local, long distance"

## Usar o Shell para exibir as configurações do plano de discagem da UM

Este exemplo exibe uma lista com todos os planos de discagem da UM.

    Get-UMDialplan

Este exemplo exibe uma lista formatada de todas as configurações em um plano de discagem de UM com o nome `MyUMDialPlan`.

    Get-UMDialplan -Identity MyUMDialPlan | Format-List

