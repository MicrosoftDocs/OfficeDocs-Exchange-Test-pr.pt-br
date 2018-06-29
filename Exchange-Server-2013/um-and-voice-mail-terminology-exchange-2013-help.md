---
title: 'Terminologia de correio de Unificação de mensagens e voz: Exchange 2013 Help'
TOCTitle: Terminologia de correio de Unificação de mensagens e voz
ms:assetid: 3a6d93f2-1802-4aed-8b83-35c7fd004d0c
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Ee633462(v=EXCHG.150)
ms:contentKeyID: 54651936
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Terminologia de correio de Unificação de mensagens e voz

 

_**Aplica-se a:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Tópico modificado em:**2013-04-22_

Este tópico contém os termos e as definições usados com a Unificação de Mensagens.

  - codec de áudio  
    Uma codificação digital de um sinal de voz analógico. A maioria dos codecs de áudio oferece compactação dos dados, às custas de alguma perda de fidelidade quando os dados são recuperados. Os codecs de áudio podem variar na qualidade percebida do som, na largura de banda necessária para usá-los e em requisitos de sistema necessários para a codificação.

<!-- end list -->

  - anotações de áudio  
    Anotações baseadas em texto que podem ser adicionadas a uma mensagem de caixa postal recebida no Outlook ou no Outlook Web App.

<!-- end list -->

  - atendedor automático  
    Sistema de software que atende chamadas, reproduz prompts ou instruções e então coleta entrada do chamador como discagens por tom ou fala. Os atendedores automáticos podem direcionar uma chamada para números de telefone ou usuários e entidades nomeados (como por exemplo, departamentos) que o chamador especificar, sem a intervenção de um operador humano.

<!-- end list -->

  - Reconhecimento Automático de Fala (ASR)  
    Uma tecnologia que permite ao computador corresponder a fala humana a um conjunto predefinido de palavras ou expressões.

<!-- end list -->

  - atendimento de chamadas  
    Processo pelo qual um chamador interage com um sistema de caixa postal quando o número chamado originalmente não atende. Geralmente, o sistema executa uma saudação ou outro prompt e permite ao chamador gravar uma mensagem de voz.

<!-- end list -->

  - Regras de Atendimento de Chamada  
    Uma forma de atendimento de chamadas em que o usuário para o qual a chamada está sendo atendida pode especificar regras para determinar o comportamento apresentado aos chamadores. O usuário pode especificar condições a serem avaliadas, saudações e escolhas a serem oferecidas ao chamador, e ações (como, por exemplo, transferir ou deixar uma mensagem) a serem tomadas em resposta à escolha do chamador.

<!-- end list -->

  - redes de comutação de circuitos  
    Rede na qual existe uma conexão dedicada. Uma conexão dedicada é um circuito ou canal configurado entre dois nós para que eles possam se comunicar.

<!-- end list -->

  - encaminhamento de chamada condicional  
    Um conjunto de condições escolhidas por um usuário para serem usadas quando esse usuário receber uma chamada de entrada. A chamada é redirecionada com base nas condições estabelecidas.

<!-- end list -->

  - Discagem por Nome  
    Um recurso que permite a um chamador soletrar o nome de uma pessoa usando as teclas do telefone (ABC=2, DEF=3 etc).

<!-- end list -->

  - plano de discagem  
    Para a Unificação de Mensagens, é um conjunto de pontos de extremidade compatíveis com telefonia que compartilham um plano de numeração comum. Os detalhes do plano são determinados pelo sistema de telefone ao qual a UM está conectada. Na situação mais simples, ele pode ser um PBX com ramais, cada um com um número único e de tamanho fixo.

<!-- end list -->

  - grupo de regras de discagem  
    Grupos de regras de discagem são criados para permitir que telefones sejam modificados antes de serem enviados para o PBX habilitado para SIP ou PBX IP de chamadas de saída. Grupos de regras de discagem podem remover ou adicionar dígitos a números de telefone que são usados para fazer chamadas pelo servidor da Unificação de Mensagens.
    
    Cada grupo de regras de discagem contém entradas de regras de discagem que determinam os tipos de chamadas locais/região e internacionais que os usuários pertencentes a um grupo de regras podem fazer. Cada regra de grupo de discagem deve conter pelo menos uma entrada de regra de discagem.

<!-- end list -->

  - parceiro de fax  
    Os parceiros de fax da UM fornecem aplicativos ou serviços que podem aceitar chamadas liberadas pela UM quando um tom de fax é detectado. O produto ou serviço do parceiro então recebe os dados do fax, cria uma mensagem e a entrega ao usuário habilitado para UM como uma mensagem de email com um anexo .tif. Essas mensagens aparecerão na pasta de pesquisa Fax no Outlook e no Outlook Web App.

<!-- end list -->

  - grupo de busca  
    Um conjunto de ramais organizados em um grupo, através do qual o PBX habilitado para SIP ou PBX IP "busca" um ramal disponível. Um grupo de busca é usado para direcionar chamadas para pontos de extremidade com capacidade idêntica ou para um aplicativo, como uma caixa postal.

<!-- end list -->

  - formato de número do país/região  
    O formato de número do país/região especifica como um número de telefone do usuário deve ser discado pelo servidor de Unificação de Mensagens em um plano de discagem diferente, que tenha o mesmo código de país. Isso é usado por um atendedor automático e quando um usuário do Outlook Voice Access pesquisa e tenta chamar o usuário no diretório.
    
    Essa entrada consiste em um prefixo de número e em um número variável de caracteres (por exemplo, 020xxxxxxx).

<!-- end list -->

  - informe  
    Uma mensagem de áudio que é reproduzida quando um usuário disca pela primeira vez para um sistema de Unificação de Mensagens e que descreve alguma condição temporária de interesse de todos os usuários.

<!-- end list -->

  - código de acesso internacional  
    O prefixo usado para direcionar uma chamada internacionalmente. O código de Acesso Internacional é 011 nos Estados Unidos e 00 na maioria dos outros países.

<!-- end list -->

  - formato de número internacional  
    A cadeia de caracteres de dígitos usada para definir como discar para alguém fora de um país especifico.

<!-- end list -->

  - PBX IP (Internet Protocol Private Branch eXchange)  
    Um comutador telefônico que nativamente dá suporte a VoIP (voz sobre IP). Um PBX IP usa protocolos baseados em VoIP para se comunicar com hosts baseados em IP, como telefones VoIP em uma rede de comutação de pacotes. Alguns PBXs IP também oferecem suporte ao uso de telefones analógicos e digitais tradicionais.

<!-- end list -->

  - método de seleção de correspondência de nome  
    O mecanismo usado para ajudar um chamador a diferenciar entre usuários com nomes que correspondem à entrada de tom de discagem ou de fala.

<!-- end list -->

  - indicador de espera de mensagem  
    Um sinal que indica a presença de uma ou mais mensagens de voz não lidas. Para sistemas de caixa postal, costuma ser uma lâmpada no telefone ou um tom de discagem intermitente.

<!-- end list -->

  - Serviço Roteador de Chamadas da Unificação de Mensagens do Microsoft Exchange  
    Serviço que direciona chamadas de entrada para usuários habilitados para UM para o serviço Unificação de Mensagens do Microsoft Exchange.

<!-- end list -->

  - Serviço de Unificação de Mensagens do Microsoft Exchange  
    Serviço que implementa recursos de Unificação de Mensagens para usuários habilitados para UM.

<!-- end list -->

  - notificação de chamada não atendida  
    Uma mensagem de email enviada para um usuário habilitado para UM que indica que alguém chamou mas não deixou uma mensagem na caixa postal.

<!-- end list -->

  - prefixo de número nacional  
    Prefixo usado para direcionar uma chamada como chamada nacional. Nos Estados Unidos, esse prefixo é 1. No Reino Unido e na maioria dos outros países, esse prefixo é 0.

<!-- end list -->

  - máscara de número  
    Conjunto de números e caracteres curinga usado para determinar o número de telefone que o servidor de Caixa de Correio discará. Um "X" representa um dígito único (0 ... 9). Um asterisco (\*) representa qualquer número de tais dígitos.

<!-- end list -->

  - ramal numérico  
    Uma cadeia de caracteres de dígitos que não contém um "+" ou um código de país/região. Em planos de discagem, os ramis precisam ter um tamanho especificado.

<!-- end list -->

  - discagem externa  
    Um processo em que a Unificação de Mensagens (UM) disca ou transfere chamadas. Geralmente, a Unificação de Mensagens recebe chamadas, mas algumas vezes ela disca. Por exemplo, a discagem para fora ocorre quando um atendedor automático da UM transfere uma chamada para o ramal de um usuário, ou quando o usuário habilitado para UM usa o Tocar no Telefone do Outlook.

<!-- end list -->

  - Outlook Voice Access  
    Série de prompts de voz que permitem que chamadores autenticados acessem suas informações de email, caixa postal, calendário e contatos usando um telefone celular, digital ou analógico padrão. O Outlook Voice Access também permite que chamadores autenticados naveguem por informações pessoais em suas caixas de correio, realizem chamadas, localizem usuários e naveguem por prompts e menus do sistema usando DTMF, também conhecido como discagem por tom, ou entradas de voz.

<!-- end list -->

  - código de acesso de linha externa  
    O prefixo usado pela UM (ou uma pessoa que esteja usando um ramal interno no PBX ou PBX IP) para acessar uma linha externa. Geralmente, é o número 9.

<!-- end list -->

  - comutação de pacotes  
    Técnica que divide uma mensagem de dados em pequenas unidades, chamadas pacotes. Os pacotes são enviados para seus destinos pela melhor rota disponível e, em seguida, são reagrupados na extremidade de recepção.

<!-- end list -->

  - identificador piloto  
    Um número de telefone que indica um grupo de busca e é o número de acesso para as chamadas roteadas para a Unificação de Mensagens. É algumas vezes chamado de número piloto.

<!-- end list -->

  - PIN  
    Uma senha inserida pelo usuário no telefone para acesso à caixa de correio.

<!-- end list -->

  - Tocar no Telefone  
    Um recurso da Unificação de Mensagens que os usuários podem usar para tocar suas mensagens de voz ou tocar e gravar saudações de caixa postal personalizadas pelo telefone.

<!-- end list -->

  - PBX (Central Privada de Comutação Telefônica)  
    Uma rede telefônica privada em uma organização. Números de telefone ou de ramais individuais são aceitos e chamadas são roteadas automaticamente para eles. Os usuários podem chamar uns aos outros usando ramais, mesmo entre locais distribuídos.

<!-- end list -->

  - prompt  
    Uma mensagem de áudio tocada pelo telefone para explicar as opções válidas para os usuários.

<!-- end list -->

  - Caixa postal protegida  
    Um recurso da UM que usa gerenciamento de direitos de informação para criptografar o conteúdo de mensagens de voz e especificar as operações permitidas nelas. A proteção pode ser acionada por ação do chamador (marcando a mensagem como particular) ou por um política do sistema.

<!-- end list -->

  - rede telefônica comutada pública (PSTN)  
    A PSTN é um agrupamento das redes públicas mundiais de telefone de comutação de circuitos. Esse agrupamento assemelha-se à Internet, que é um agrupamento das redes públicas mundiais de comutação de pacotes baseada em IP.

<!-- end list -->

  - redefinir  
    Quando um PIN ou senha é redefinido, o sistema escolhe aleatoriamente um novo PIN ou senha temporário. O usuário precisará então alterar o PIN temporário na próxima vez em que entrar no Outlook Voice Access.

<!-- end list -->

  - pesquisa inversa de número (RNL)  
    Método usado para tentar localizar o nome de uma pessoa, a partir de um diretório ou de outro armazenamento de informações, com base em seu número de telefone.

<!-- end list -->

  - Codec RTAudio  
    Um codec de fala avançado projetado para aplicações VoIP bidirecionais e em tempo real, como jogos, audioconferência e aplicativos sem fio sobre IP. O RTAudio é o codec de áudio preferencial da Microsoft e o codec padrão de plataformas do Microsoft Lync Server.

<!-- end list -->

  - PBX habilitado para SIP  
    Um PBX habilitado para SIP é um dispositivo de telefonia que atua como comutador de rede para transferir chamadas em uma rede de telefonia ou de comutação de circuitos. Entretanto, a diferença entre um PBX habilitado para SIP e um PBX tradicional é que o PBX habilitado para SIP pode se conectar à Internet e usar o protocolo SIP para fazer chamadas pela Internet.

<!-- end list -->

  - Notificação SIP  
    Uma notificação SIP é uma mensagem SIP enviada de um par SIP para outro para avisá-lo sobre uma alteração.

<!-- end list -->

  - Par SIP  
    Dispositivo habilitado para SIP que oferece comunicações de telefonia entre um gateway VoIP, PBX IP, PBX habilitado para SIP, servidores Microsoft Lync ou telefones VoIP e serviços da Unificação de Mensagens.

<!-- end list -->

  - usar asterisco  
    Ação que um chamador pode executar quando discar para um atendedor automático da Unificação de Mensagens e quiser acessar o Outlook Voice Access para acessar email e caixa postal. Para fazer isso, ele pressiona a tecla asterisco (\*) enquanto os prompts do atendedor automático estiverem sendo reproduzidos.

<!-- end list -->

  - número de acesso do assinante (número do Outlook Voice Access)  
    Número configurado em um PBX tradicional ou habilitado para SIP ou IP e em um plano de discagem da UM que permite aos usuários acessarem a caixa de correio usando o Outlook Voice Access. Em alguns casos, isso pode ser configurado com o mesmo número do acesso do assinante ou o número piloto (também chamado de identificador piloto) no PBX tradicional ou habilitado para SIP ou IP e no grupo de busca da UM.

<!-- end list -->

  - prompt do sistema  
    Uma gravação de áudio curta para a Unificação de Mensagens, que é tocada para chamadores pelo servidor. Os prompts do sistema são usados para dar as boas-vindas aos chamadores e para informar as opções que eles terão quando usarem o sistema de caixa postal.

<!-- end list -->

  - interface de telefone (TUI)  
    Uma interface usada para navegar nos menus de um sistema de caixa postal usando DTMF, também conhecido como tom de discagem, entradas.

<!-- end list -->

  - TTS (Conversão de texto em fala)  
    Tecnologias para converter texto digitado em fala.

<!-- end list -->

  - Gateway IP da UM  
    (Consulte gateway IP). Um gateway IP da UM é a representação da Unificação de Mensagens do Exchange de qualquer par SIP com o qual é possível se comunicar usando protocolos VoIP. Pode representar um dispositivo que faz interface com um PBX tradicional ou habilitado para SIP ou IP, ou o Microsoft Lync Server.

<!-- end list -->

  - Processo de trabalho do UM  
    Um processo criado durante a inicialização do serviço de Unificação de Mensagens do Exchange. O serviço da UM, ao receber uma solicitação para lidar com uma chamada de entrada, redireciona essa solicitação imediatamente para um processo de trabalho da UM, que conduz todas as interações subsequentes com o chamador.

<!-- end list -->

  - Gerenciador de Processo de Trabalho da UM  
    Um componente que lida com a criação e o monitoramento de todos os processos de trabalho da UM que são criados.

<!-- end list -->

  - Unificação de Mensagens  
    Um aplicativo que consolida a caixa postal e os emails de um usuário em uma só caixa postal, para que o usuário só precise verificar um único local para mensagens, independentemente do tipo. O servidor de email é usado como plataforma para todos os tipos de mensagens, tornando desnecessário manter infraestruturas de caixa postal e de email separadas.

<!-- end list -->

  - caixa postal  
    Um sistema que registra e armazena mensagens de telefone em uma caixa de correio do usuário.

<!-- end list -->

  - Visualização de Caixa Postal  
    Um recurso que oferece texto, transcrito a partir da gravação de áudio, em uma mensagem de voz ao ser entregue.

<!-- end list -->

  - mensagem de voz  
    Uma mensagem eletrônica com conteúdo principal formado por áudio digitalizado.

<!-- end list -->

  - Voice over IP (VoIP)  
    A prática de usar uma rede de dados IP para transmitir chamadas de voz.

<!-- end list -->

  - VUI (interface de voz)  
    Uma interface usada para navegar nos menus de um sistema de Unificação de Mensagens (UM) usando entradas de fala.

<!-- end list -->

  - gateway VoIP
    
    1.  Um dispositivo ou produto de hardware de terceiros que se conecta a um PBX ou uma LAN herdados. Um gateway VoIP converte protocolos TDM ou de comutação telefônica em protocolos de comutação de pacotes que podem ser usados em uma rede baseada em VoIP.
    
    2.  A representação da Unificação de Mensagens do Exchange de qualquer par SIP com o qual possa se comunicar usando protocolos VoIP. Pode representar um dispositivo que faz interface com um PBX legado, um PBX IP ou o Microsoft Lync Server.

<!-- end list -->

  - saudação de boas-vindas  
    Saudação tocada quando um chamador externo liga para um atendedor automático da UM ou quando um usuário do Outlook Voice Access ou outro chamador liga para um número de acesso de usuário configurado em um plano de discagem da UM. As saudações de boas-vindas padrão podem ser alteradas por um cliente para que sejam específicas de uma organização ou localidade.

