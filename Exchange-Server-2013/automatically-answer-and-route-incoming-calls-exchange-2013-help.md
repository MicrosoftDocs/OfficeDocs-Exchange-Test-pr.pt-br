---
title: 'Responder e rotear as chamadas de entrada automaticamente: Exchange 2013 Help'
TOCTitle: Responder e rotear as chamadas de entrada automaticamente
ms:assetid: d3dcd488-bd57-44cc-bdd4-ddee42a69dde
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Bb124724(v=EXCHG.150)
ms:contentKeyID: 50486707
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Responder e rotear as chamadas de entrada automaticamente

 

_**Aplica-se a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Tópico modificado em:** 2013-08-26_

A UM (Unificação de Mensagens) do Microsoft Exchange permite criar um ou vários atendedores automáticos do UM, dependendo das necessidades da organização. Ao contrário do que acontece com outros componentes da Unificação de Mensagens, como planos de discagem e gateways IP, você não precisa criar atendedores automáticos de UM. No entanto, os atendedores automáticos ajudam os chamadores internos e externos a localizar usuários ou departamentos existentes em uma organização e a transferir chamadas para eles. Este tópico aborda o recurso de atendedor automático da UM encontrado na Unificação de Mensagens.

**Sumário**

Auto attendants

UM auto attendants

Auto attendants with multiple languages

Non-business and business hours custom greetings

Menu navigation entries

Auto attendant examples

## Atendedores automáticos

Em ambientes de telefonia ou de Unificação de Mensagens, um atendedor automático ou um sistema de menus de atendedor automático transfere os chamadores para o ramal de um usuário ou de um departamento sem a intervenção de uma recepcionista ou um operador. Em muitos sistemas de atendedor automático, é possível entrar em contato com uma recepcionista ou um operador pressionando ou dizendo zero. +O atendedor automático é um recurso presente nas soluções mais modernas de PBXs (Private Branch eXchanges), PBXs IP e Unificação de Mensagens.

Em alguns sistemas de atendedor automático, existem menus de informações somente para mensagens e menus de voz que são usados para que uma organização possa comunicar o horário de atendimento, instruções sobre as instalações, informações sobre oportunidades de emprego e respostas a outras perguntas freqüentes. Depois que a mensagem é reproduzida, o chamador é encaminhado à recepcionista ou ao operador ou retorna ao menu principal.

Em sistemas de atendedor automático mais complexos, o sistema de menus pode ser usado para procurar outros menus de atendedores automáticos, localizar um usuário no sistema ou transferir a ligação para outra linha telefônica externa. Eles também podem ser usados para permitir que o chamador interaja com o sistema em determinada situação, como quando um aluno se matricula em uma aula em uma universidade ou verifica suas notas, ou quando você ativa um cartão de crédito por telefone.

Embora possam ser muito úteis, se os atendedores automáticos não forem projetados e configurados corretamente, eles poderão confundir e frustrar os chamadores. Por exemplo, principalmente em grandes organizações, quando os atendedores automáticos não são projetados corretamente, os chamadores podem passar por uma série interminável de perguntas e prompts de menus antes de serem finalmente transferidos a uma pessoa que responda à sua pergunta.

## atendedores automáticos da UM

A Unificação de Mensagens permite a criação de um ou mais atendedores automáticos da UM, dependendo das necessidades da sua organização. Os atendedores automáticos do UM podem ser usados para criar um sistema de menus de voz para uma organização que permita aos chamadores externos e internos se movimentar pelo sistema de menus do atendedor automático do UM para localizar e fazer ou transferir chamadas para usuários ou departamentos da empresa.

Quando usuários anônimos ou não autenticados ligam para um número de telefone comercial externo, ou quando chamadores internos ligam para um determinado ramal, eles ouvem uma série de prompts de voz que os ajudam a fazer uma chamada para um usuário ou localizar um usuário na organização e, em seguida, fazer uma chamada para esse usuário. O atendedor automático do UM consiste em uma série de prompts de voz ou arquivos .wav que os chamadores ouvem, em vez de um operador humano, quando ligam para uma organização que tem a Unificação de Mensagens. O atendedor automático de UM permite que os chamadores se movimentem pelo sistema de menus, façam chamadas ou localizem usuários usando o DTMF (Dual Tone Multi-Frequency) ou entradas de voz. No entanto, para usar o ASR (Reconhecimento Automático de Fala) ou entradas de voz, você deve habilitar o ASR no atendedor automático da UM.

Um atendedor automático do UM apresenta os seguintes recursos:

  - Fornece saudações corporativas ou informativas.

  - Fornece menus corporativos personalizados. Você pode personalizar esses menus para que tenham mais de um nível.

  - Fornece uma função de pesquisa de diretórios que permite ao chamador pesquisar um nome no diretório da organização.

  - Permite que um chamador se conecte ao telefone de um membro da organização ou deixe uma mensagem para esse membro.

Não há limite para o número de atendedores automáticos da UM que podem ser criados. Cada atendedor automático da Unificação de Mensagens pode aceitar um número ilimitado de ramais. Um atendedor automático da UM pode fazer referência a um, e a apenas um, plano de discagem do UM. Os atendedores automáticos da UM podem também fazer referência ou se vincular a outros atendedores automáticos da UM.

Uma chamada de entrada recebida de um número de telefone externo ou de um ramal telefônico interno é passada entre servidores Exchange, e em seguida enviada para um atendedor automático da UM. O atendedor automático da UM é configurado pelo administrador para usar arquivos de voz pré-gravados (.wav) que são reproduzidos pelo telefone para o chamador e permitem que o chamador movimente-se pelo sistema de menus da Unificação de Mensagens. Você pode personalizar todos os arquivos .wav que são usados quando configura um atendedor automático da UM para atender às necessidades da sua organização.

Voltar ao início

## Atendedores automáticos com vários idiomas

Há duas situações em que pode ser necessário fornecer atendedores automáticos em diferentes idiomas aos chamadores. A definição de idioma disponível em um atendedor automático da UM permite configurar o idioma de prompt padrão no atendedor automático. Quando você usa os prompts padrão do sistema para o atendedor automático, esse é o idioma que o chamador ouvirá sempre que o atendedor automático responder à chamada de entrada. Essa definição de idioma afetará somente os prompts padrão do sistema fornecidos. Essa configuração de idioma não afeta os prompts personalizados configurados em um atendedor automático.

Para implantações locais e híbridas, ao instalar a versão em inglês dos Estados Unidos, este será o único idioma disponível a ser configurado nos atendedores automáticos da UM. Se você instalar uma versão localizada, por exemplo, japonês, poderá configurar o atendedor automático criado para usar japonês ou inglês dos Estados Unidos como o idioma padrão. Pacotes de idioma da UM adicionais podem ser instalados em um servidor de UM (Unificação de Mensagens) para permitir que você use outros idiomas padrão em um atendedor automático.

Por exemplo, se sua empresa estiver sediada nos Estados Unidos, mas exigir um sistema de menus que forneça aos chamadores as opções de idiomas Inglês dos Estados Unidos, Espanhol e Francês, será necessário instalar os pacotes de idiomas da UM. Nesse caso, se você tiver instalado a versão em inglês dos Estados Unidos, será necessário instalar os pacotes de idiomas da UM em espanhol e francês. Entretanto, pelo fato do atendedor automático de Unificação de Mensagens só permitir a configuração de um idioma por vez, seria necessário criar quatro atendedores automáticos: um atendedor principal configurado para usar inglês dos Estados Unidos e um atendedor automático para cada idioma: Inglês dos Estados Unidos, Espanhol e Francês. Em seguida, você configuraria o atendedor automático de forma a conter os mapeamentos de teclas apropriados ou o menu de navegação para acessar os outros atendedores automáticos criados para cada idioma. Nesse exemplo, os atendedores automáticos principais responderiam à chamada de entrada e o chamador ouviria, por exemplo, a mensagem "Welcome to Contoso, Ltd. For English, press or say 1. For Spanish, press or say 2. For French, press or say 3."


> [!TIP]
> No UM do Exchange, os usuários do Outlook Voice Access autenticados e não autenticados não podem procurar por usuários no diretório usando entradas de fala em nenhum idioma. No entanto, os chamadores que ligam para um atendedor automático podem usar entradas de fala em vários idiomas para navegar pelos menus do atendedor automático e procurar usuários no diretório.



Voltar ao início

## Saudações pessoais fora do horário comercial e no horário comercial

Depois de criar um atendedor automático da UM, um prompt padrão do sistema será usado para a saudação do prompt do menu principal para horário não comercial que é ouvido pelos chamadores depois que a saudação de boas-vindas do horário não comercial for tocada. Embora os prompts do sistema não devam ser substituídos ou alterados, é provável que você queira personalizar as saudações e os prompts do menu usados com atendedores automáticos da UM. Freqüentemente, além de configurar uma saudação de boas-vindas para horário não comercial, você também vai querer criar e configurar uma saudação personalizada do prompt do menu principal para horário não comercial. Após configurar uma saudação personalizada do prompt do menu principal para horário não comercial, você deve habilitar os mapeamentos de teclas no atendedor automático do UM para horário não comercial.

Uma saudação personalizada do prompt do menu principal para horário não comercial é uma lista de opções que os chamadores ouvem durante o horário não comercial. Para permitir que os chamadores ouçam uma saudação do prompt do menu principal para horário não comercial, você deve primeiro configurar a agenda de horário comercial e não comercial usando o EAC ou cmdlet **Set-UMAutoAttendant** no Shell. Por exemplo, "Você entrou em contato com Trey Research após o horário comercial. Se houver uma emergência médica, desligue e disque 911. Para deixar uma mensagem para um de nossos médicos, pressione 1. Para deixar uma mensagem para um de nossos fisioterapeutas, pressione 2. Para deixar uma mensagem geral para um de nossos atendentes, pressione 3. Para ser atendido por um operador fora do horário do expediente, pressione 0."

Por padrão, quando você cria um atendedor automático da UM, as saudações ou prompts de horário comercial e não comercial não estão configuradas e não há nenhuma entrada de navegação em menu definida para os prompts do menu principal para horário comercial ou não comercial. Para configurar corretamente as saudações personalizadas do menu principal para horário não comercial, você deve:

1.  Configurar o horário comercial e o horário não comercial na página **Horário comercial**.

2.  Criar o arquivo de saudação que será utilizado para a saudação de boas-vindas para horário não comercial.

3.  Configurar a saudação de boas-vindas do horário não comercial na página **Saudações**.

4.  Criar o arquivo de saudação que será utilizado para a saudação do prompt do menu principal para horário não comercial.

5.  Configurar a saudação do prompt do menu principal para horário não comercial na página **Saudações**.

6.  Habilitar a navegação de menu e adicionar entradas de navegação de menu na página **Navegação de menu**.

Voltar ao início

## Entradas de navegação de menu

Se você usar a saudação padrão do prompt do menu principal e definir uma entrada de navegação de menu ou várias entradas de navegação de menu, o mecanismo de TTS (Conversão de Texto em Fala) da Unificação de Mensagens sintetizará um prompt de menu principal. O mecanismo TTS só sintetizará um prompt de menu principal se a saudação padrão estiver configurada e pelo menos uma entrada de navegação de menu tiver sido definida. O mecanismo TTS não sintetizará um prompt de menu principal se você estiver usando um prompt de menu principal personalizado, por exemplo, "Para o departamento de vendas, pressione 1. Para o departamento de suporte, pressione 2." Para criar esse prompt do menu principal, você precisa criar duas entradas de navegação: um chamado "Departamento de Vendas" e outro chamado "Departamento de Suporte", e depois configurar a entrada do mapeamento de teclas para tocar um arquivo de áudio, transferir para um número de ramal ou enviar o chamador para outro atendedor automático.

Ao configurar entradas de menu de navegação, você definirá as opções e as operações que serão executadas se um chamador disser uma frase enquanto estiver usando um atendedor automático habilitado para fala ou pressionar a tecla no teclado numérico do telefone enquanto estiver usando um atendedor automático que não esteja habilitado para fala. Para configurar entradas de navegação de menu para um atendedor automático, você deve:

  - Habilitar a navegação de menu em horário não comercial.

  - Adicionar entradas de menu de navegação.

  - Digite o nome da entrada de navegação do menu.

  - Selecionar uma opção na lista **Quando essa tecla é pressionada** e usar a caixa **Executar o seguinte arquivo de áudio** para carregar o arquivo de áudio a ser reproduzido.

  - Configurar a ação que você deseja executada:
    
      - Transferir para este ramal
    
      - Transferir para este atendedor automático de UM
    
      - Deixar uma mensagem de voz para este usuário
    
      - Anunciar o local da empresa
    
      - Anunciar o horário comercial

Voltar ao início

## Exemplos de atendedores automáticos

Os exemplos a seguir demonstram como você pode usar os atendedores automáticos de UM juntamente com a Unificação de Mensagens:

  - **Exemplo 1** Em uma empresa chamada Contoso, Ltd., os clientes externos podem usar três números de telefone externos: 425-555-1111 (Escritórios Corporativos), 425-555-0122 (Suporte ao Produto) e 425-555-0133 (Vendas). Os departamentos de Recursos Humanos, Administração e Contabilidade têm ramais internos e devem ser acessados a partir do atendedor automático do UM dos Escritórios Corporativos.
    
    Para criar uma estrutura de atendedor automático do UM que dê suporte a esse cenário, crie e configure três atendedores automáticos do UM, cada um deles com o número de telefone externo apropriado. Crie três outros atendedores automáticos do UM para cada departamento nos Escritórios Corporativos. Em seguida, configure cada atendedor automático da UM com base em seus requisitos, como o tipo de saudação ou outras informações de navegação.

  - **Exemplo 2**   Em uma empresa chamada Contoso, Ltd., os clientes externos ligam para o número principal da empresa, 425-555-0100. Quando um chamador externo liga para o número principal, o atendedor automático da UM atende e se comunica com o chamador dizendo, "Bem-vindo à Contoso, Ltd. Pressione ou diga "Um" para ser transferido para a administração corporativa. Pressione ou diga "Dois" para ser transferido para o suporte ao produto. Pressione ou diga "Três" para ser transferido para as informações corporativas. Pressione ou diga "Zero" para ser transferido ao operador." Para criar uma estrutura para o atendedor automático do UM que ofereça suporta a essa situação, crie um atendedor automático do UM que tenha ramais personalizados que roteiem a chamada para o ramal apropriado.

Voltar ao início

