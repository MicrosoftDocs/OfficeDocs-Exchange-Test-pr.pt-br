---
title: 'Unificação de mensagens: Exchange 2013 Help'
TOCTitle: Unificação de mensagens
ms:assetid: 004b5d1a-cae8-4034-ab65-db41bd2f7b97
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/JJ150478(v=EXCHG.150)
ms:contentKeyID: 50484855
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Unificação de mensagens

 

_**Aplica-se a:**Exchange Server 2013, Exchange Server 2016_

_**Tópico modificado em:**2016-12-09_

A Unificação de Mensagens (UM) habilita os usuários a usar a caixa postal e outros recursos, incluindo o Outlook Voice Access e as Regras de Atendimento de Chamadas. A UM combina mensagens de voz e emails em uma caixa de correio que pode ser acessada por muitos dispositivos diferentes. Os usuários podem ouvir suas mensagens em sua Caixa de Entrada de email ou usando o Outlook Voice Access em qualquer telefone. Você tem controle sobre como os usuários efetuam chamadas de saída de UM e a experiência que as pessoas têm quando ligam para sua organização.

Atualmente, os administradores de TI normalmente gerenciam a caixa postal ou as redes de telefonia e os sistemas de email ou as redes de dados de suas organizações como sistemas separados. A caixa postal e o email ficam em caixas de entrada separadas hospedadas em servidores separados acessados do computador, no caso do email, e pelo telefone, no caso da caixa postal.

A Unificação de Mensagens possibilita que os administradores do Exchange combinem mensagens de voz e emails em uma caixa de correio, para que os usuários possam ouvir suas mensagens de caixa postal em suas Caixas de Entrada ou usando o Outlook Voice Access de qualquer telefone. Ele usa o armazenamento do Exchange para mensagens de voz e emails.

**Conteúdo**

New features

Unified Messaging features

Planning and deploying UM

Managing UM with the EAC and the Shell

Unified Messaging documentation

## Novos recursos

A Unificação de Mensagens (UM) foi incluída no Microsoft Exchange Server 2007 e também estava disponível no Exchange 2010. O recurso de Unificação de Mensagens definido no Exchange 2013 é similar ao das versões anteriores do Exchange. No entanto, novos recursos foram adicionados, e houve mudanças na arquitetura. A Unificação de Mensagens agora é considerada um componente ou sub-recurso dos recursos relacionados à voz oferecidos no Exchange 2013. O termo *Unificação de Mensagens* ainda é largamente usado nos cmdlets do Shell de Gerenciamento do Exchange e em serviços relacionados a UM, e todos os componentes de Unificação de Mensagens—incluindo planos de discagem, atendedores automáticos, políticas de caixa de correio de UM e gateways IP de UM—juntamente com a habilidade de gerenciar esses componentes de UM, estão localizados no nó de Unificação de Mensagens, no painel de navegação do Centro de Administração do Exchange (EAC).

Os seguintes tópicos levam a informações sobre recursos novos ou aperfeiçoados encontrados na Unificação de Mensagens do Exchange 2013:

  - [Mudanças de arquitetura de voz](voice-architecture-changes-exchange-2013-help.md)

  - [Suporte a IPv6 na Unificação de mensagens](ipv6-support-in-unified-messaging-exchange-2013-help.md)

  - [Melhorias da caixa postal preview](voice-mail-preview-enhancements-exchange-2013-help.md)

  - [Atualizações de cmdlet do Unified Messaging](unified-messaging-cmdlet-updates-exchange-2013-help.md)

Voltar ao início

## Recursos de Unificação de Mensagens

Os recursos de caixa postal encontrados na Unificação de Mensagens oferecem benefícios para usuários finais e administradores de TI.

## Recursos para usuários finais

Quando você implanta a Unificação de Mensagens, os usuários podem acessar caixa postal, email e informações de calendários que estão localizados na caixa de correio a partir de um cliente de email, por exemplo, Outlook ou Microsoft Outlook Web App, de um celular com o Microsoft Exchange ActiveSync configurado, como um Windows Phone, ou de um telefone. Além disso, os usuários podem usar os seguintes recursos:

  - **Acesso a informações do Exchange**   Usuários habilitados para UM podem acessar um conjunto completo de recursos de caixa postal a partir de celulares com acesso à Internet, do Microsoft Office Outlook 2007 ou posteriores e do Outlook Web App. Esses recursos incluem muitas opções de configuração de caixa postal e a capacidade de reproduzir uma mensagem de voz a partir do Painel de Leitura, usando o Media Player integrado do Windows, ou a partir da lista de mensagens, usando alto-falantes do computador.

  - **Tocar no Telefone**   O recurso Tocar no Telefone permite que usuários habilitados para UM reproduzam mensagens de voz pelo telefone. Se um usuário que trabalha em uma baia em um escritório está usando um computador público ou um computador que não está habilitado para multimídia, ou está ouvindo uma mensagem de voz confidencial, talvez ele não queira ou não possa ouvir uma mensagem de voz usando os alto-falantes do computador. O usuário pode reproduzir a mensagem de voz usando qualquer telefone, incluindo telefones residenciais, comerciais ou celulares.

  - **Formulário de caixa postal**   O formulário de caixa postal é semelhante ao formulário de email padrão. Ele fornece aos usuários uma interface para executar ações como reproduzir, parar ou pausar mensagens de voz, reproduzir mensagens de voz em um telefone e adicionar e editar anotações.
    
    O formulário de mensagem de voz inclui o Windows Media Player incorporado e um campo de anotações de Áudio. O Windows Media Player incorporado e o campo de anotações são exibidos no Painel de Leitura quando o usuário visualiza uma mensagem de voz ou em uma janela separada quando uma mensagem de voz é aberta. Se um usuário não estiver habilitado para a Unificação de Mensagens ou um cliente de email suportado não tiver sido instalado no computador cliente, ele visualizará as mensagens de voz como anexos do email e o formulário de caixa postal não estará disponível.

  - **Configuração do usuário**   Um usuário habilitado para a Unificação de Mensagens pode configurar várias opções de caixa postal para a Unificação de Mensagens usando o Outlook Web App. Por exemplo, o usuário pode configurar os números de acesso telefônico, o número de Tocar no Telefone para mensagens de voz e redefinir um PIN de acesso à caixa postal.

  - **Atendimento de chamadas**   O atendimento de chamadas inclui o atendimento de chamadas recebidas em nome de um usuário, a reprodução de saudações pessoais, a gravação de mensagens e seu envio para entrega em uma Caixa de Entrada como uma mensagem de email.

  - **Regras de Atendimento de Chamadas**   As Regras de Atendimento de Chamadas permitem que os usuários habilitados para caixa postal determinem como suas chamadas de resposta a chamadas de entrada devem ser tratadas. A forma como as regras de atendimento de chamadas são aplicadas às chamadas de entrada é semelhante à forma como as regras da Caixa de Entrada são aplicadas às mensagens de email de entrada. Por padrão, nenhuma regra de atendimento de chamadas está configurada. Se uma chamada de entrada for respondida por um servidor de Caixa de Correio, o chamador é solicitado a deixar uma mensagem de voz para a pessoa chamada. Usando as regras de atendimento de chamadas, um chamador pode:
    
      - Deixar uma mensagem de voz para o usuário habilitado para UM.
    
      - Transferir para um contato alternativo do usuário habilitado para UM.
    
      - Transferir para a caixa postal do contato alternativo.
    
      - Transferir para outros números de telefone que o usuário habilitado para UM tenha configurado.
    
      - Usar o recurso Localize-me ou localizar o usuário habilitado para UM via transferência feita por operador.

  - **Visualização da Caixa Postal**   O servidor de Caixa de Entrada usar o Reconhecimento Automático de Fala (ASR) nas mensagens de caixa postal recentemente criadas. Quando um usuário recebe mensagens de voz, as mensagens contêm ambos, uma gravação e um texto que foi criado a partir da gravação da voz. Os usuários vêem o texto da mensagem de voz exibido em um email no Outlook Web App ou em outro cliente de email suportado.

  - **Indicador de espera de mensagem**   O indicador de espera de mensagem é um recurso encontrado em sistemas de caixa postal mais herdados e pode se referir a qualquer mecanismo que indica a existência de uma nova mensagem. Em Exchange 2007, essa funcionalidade foi fornecida por um aplicativo de terceiros, que indicado de recebimento de uma nova mensagem de voz por acendendo a lâmpada do telefone de mesa. Esse recurso foi adicionado ao Exchange 2010 e software de terceiros não é mais necessária. Habilitar ou desabilitar o indicador de espera de mensagem é feito na caixa de correio do usuário ou em uma diretiva de caixa de correio de Unificação de MENSAGENS.

  - **Notificações de chamadas perdidas e caixa postal usando SMS**   Quando um usuário é membro de uma implantação híbrida ou do Office 365 e define suas configurações de caixa postal com seu número de telefone celular e configura o encaminhamento de chamadas, ele pode receber notificações sobre chamadas perdidas e novas mensagens de voz em seu telefone celular, em uma mensagem de texto via Serviço de Mensagens Curtas (SMS). No entanto, para receber estes tipos de notificação, o usuário deve primeiro configurar as mensagens de texto e habilitar notificações em sua conta.

  - **Caixa Postal Protegida**   Caixa Postal Protegida é uma funcionalidade da Unificação de Mensagens que habilita os usuários a enviar emails privados. A mensagem é protegida pelo Active Directory Rights Management Services (AD RMS), e os usuários possuem restrições para encaminhar, copiar ou extrair o arquivo de voz do email. A Caixa Postal Protegida aumenta a confidenciabilidade da Unificação de Mensagens e permite que os usuários limitem quem ouve as mensagens de voz. Essa funcionalidade é similar ao jeito como mensagens de email particulares são tratadas no Exchange 2007, mas agora também se aplica a mensagens de caixa postal.

  - **Outlook Voice Access   **Existem duas interfaces de usuário de Unificação de Mensagens disponíveis para usuários habilitados para a UM: a TUI (interface do usuário de telefone) e a VUI (interface do usuário de voz). Essas duas interfaces juntas são chamadas de Outlook Voice Access. Os usuários do Outlook Voice Access podem usar o Outlook Voice Access quando acessam o sistema da caixa postal usando um telefone interno ou externo. Usuários habilitados para UM que discam no sistema de caixa postal podem acessar suas caixas de correio usando o Outlook Voice Access. Usando um telefone, um usuário habilitado para UM pode:
    
      - Acessar a caixa postal
    
      - Ouvir, encaminhar ou responder emails
    
      - Ouvir informações de calendário
    
      - Acessar ou discar para contatos armazenados no diretório da organização ou para um único contato ou grupo de contato localizado no seus Contatos pessoais.
    
      - Aceitar ou cancelar solicitações de reunião
    
      - Definir uma mensagem de voz para permitir que os chamadores saibam que a pessoa para quem ligam está ausente
    
      - Definir preferências de segurança e opções pessoais do usuário

  - **Endereçamento de grupos usando o Outlook Voice Access**   No Exchange 2007, o usuário podia usar a interface do usuário de telefone (TUI) ou a interface do usuário de voz (VUI) no Outlook Voice Access para enviar emails e mensagens de voz quando estivesse conectado à sua caixa de correio. No entanto, o usuário só poderia enviar um único email para um único usuário em seus Contatos pessoais, para vários destinatários a partir de um diretório, adicionando cada destinatário individualmente ou adicionando o nome de uma lista de distribuição do diretório da sua organização. No Exchange 2013, quando um usuário entra em sua caixa de correio usando o Outlook Voice Access, pode também enviar email e mensagens de voz para usuários em um grupo armazenado em seus Contatos pessoais.

Voltar ao início

## Recursos administrativos

Atualmente, a maior parte dos usuários e departamentos de TI gerenciam suas caixas postais e emails separadamente. A caixa postal e o email existem como caixas de entrada separadas, hospedadas em servidores separados, acessados do computador, no caso do email, e pelo telefone, no caso da caixa postal. A Unificação de Mensagens oferece um repositório integrado para todas as mensagens e acesso ao conteúdo por computador e telefone.

Os administradores do Exchange podem gerenciar a Unificação de Mensagens usando a mesma interface utilizada para gerenciar o resto do Exchange, através do Console de Gerenciamento do Exchange e do Shell de Gerenciamento do Exchange. Eles podem:

  - Gerenciar a caixa postal e emails a partir de uma plataforma única

  - Gerenciar a Unificação de Mensagens usando comandos que podem executar scripts

  - Criar infraestruturas de Unificação de Mensagens altamente disponíveis e confiáveis

A Unificação de Mensagens do Exchange 2013 oferece aos administradores:

  - **Um sistema completo de caixa postal**   A Unificação de Mensagens oferece uma solução completa de caixa postal, usando uma infraestrutura única de repositório, transporte e diretório. O armazenamento é oferecido por um servidor de Caixa de Correio, e o encaminhamento de chamadas de entrada de um gateway VoIP ou de um PBX IP é tratado por um servidor de Acesso para Cliente. Todas as mensagens de email e de voz podem ser gerenciadas a partir de um único ponto de gerenciamento, usando uma única interface de administração e um conjunto de ferramentas.

  - **Um modelo de segurança do Exchange**   O serviço de Unificação de Mensagens do MicrosoftExchange em um servidor de Caixa de Correio e o serviço de Roteamento de Chamadas de Unificação de Chamadas do MicrosoftExchange em um servidor de Acesso para Cliente funcionam como uma única conta do servidor Exchange.

  - **Consolidação dos sistemas de caixa postal**   Atualmente, a maioria dos sistemas de mensagens de voz exige que todos os componentes do sistema sejam instalados em cada escritório físico da organização. Neste tipo de disposição, os sistemas de mensagens de voz dessas filiais localizam-se fora do escritório central e devem ser administrados localmente. Geralmente isso resulta em maiores custos de administração e complexidade. A Unificação de Mensagens permite que você gerencie o sistema de caixa postal a partir de um local central. Para criar um sistema de gerenciamento centralizado para Unificação de Mensagens, você pode colocar alguns dos seus servidores Exchange em um datacenter ou em outro local e o restante de seus servidores Exchange no local, e depois implantar gateways VoIP, PBXs IP ou Controladores de Borda de Sessão (SBCs) em cada uma de suas filiais, para substituir o sistema de mensagens de voz de cada filial. Implantar um sistema de mensagens de voz centralizado desse jeito pode resultar em economias significativas em hardware e custos administrativos.

  - **Funções administrativas de Unificação de Mensagens integradas**   O conjunto de funções administrativas específicas para UM, para gerenciar recursos de Unificação de Mensagens e caixa postal inclui o seguinte:
    
      - Caixas de Correio de UM
    
      - Prompts de UM
    
      - Unificação de Mensagens

  - **Suporte de fax de entrada**   O Exchange 2013 oferece suporte integrado a fax de entrada, para usuários que tenham uma caixa de correio habilitada para UM. Eles podem receber mensagens de fax através de chamadas feitas para seu ramal.
    
    Os clientes que requerem uma solução de fax precisará implantar uma solução de parceiro de fax. Soluções de parceiros de fax foram disponibilizadas por vários parceiros de fax. As soluções de parceiro de fax foram projetadas para ser estreitamente integrado com o Exchange e habilitar usuários habilitados receber mensagens de fax de entrada. Você pode encontrar uma solução de parceiro de fax visitando [Identifique da Microsoft para parceiros de Fax](https://go.microsoft.com/fwlink/?linkid=190238).

  - **Suporte para vários idiomas**   Todos os pacotes de idiomas disponíveis contêm o mecanismo de fala (TTS) e os prompts pré-gravado para um idioma especificado e o suporte de ASR. No entanto, somente alguns pacotes de idiomas contêm suporte para visualização da caixa postal. O pacote de idioma inglês dos Estados Unidos (en-US) é incluído na mídia de instalação e pacotes de idioma UM adicionais podem ser baixados do [Centro de Download da Microsoft](https://go.microsoft.com/fwlink/p/?linkid=266542).

  - **Atendedor automático**   Um atendedor automático é um conjunto de prompts de voz que oferece aos usuários externos e internos acesso ao sistema de caixa postal. Os usuários podem usar o teclado do telefone ou entradas de fala para navegar pelo menu do atendedor automático, fazer uma chamada para um usuário ou localizar um usuário e depois fazer uma chamada para esse usuário. Um atendedor automático fornece ao administrador funcionalidades para:
    
      - Criar um menu personalizado para usuários externos.
    
      - Definir saudações informativas, saudações para horário comercial e saudações para horário não comercial.
    
      - Definir agendas de feriado.
    
      - Descrever como pesquisar o diretório da organização.
    
      - Descrever como se conectar a um ramal de usuário para que os chamadores externos possam ligar para os usuários especificando seu ramal.
    
      - Descrever como pesquisar o diretório da organização para que chamadores externos possam pesquisar o diretório da organização e ligar para um usuário específico.
    
      - Habilitar usuários externos a ligar para a recepção.

Voltar ao início

## Planejar e implantar UM

A Unificação de Mensagens (UM) exige que você integre a sua implantação do Exchange Server a um sistema de telefonia existente em sua organização. Uma implantação bem-sucedida exige uma análise cuidadosa da infraestrutura de telefonia existente para que você execute as etapas corretas de planejamento a fim de implantar e gerenciar a caixa postal na Unificação de Mensagens.

Quando você planeja sua implantação de Unificação de Mensagens, deve levar em conta o design e outras questões que podem afetar a sua capacidade de atingir as metas organizacionais ao implantar a Unificação de Mensagens. Normalmente, quanto mais simples a topologia da Unificação de Mensagens, mais fácil sua implantação e seu gerenciamento. Instale o mínimo necessário de servidores de Acesso para Cliente e de Caixa de Correio e crie o mínimo necessário de componentes de Unificação de Mensagens, como planos de discagem de UM, atendedores automáticos e políticas de caixa de correio de UM para suportar seus objetivos de negócios e organização. Grandes empresas com ambientes complexos de rede e telefonia, várias unidades de negócios ou outras complexidades exigem mais planejamento do que organizações menores com necessidades de Unificação de Mensagens relativamente diretas.

Há várias áreas que devem ser consideradas e avaliadas para se fazer uma implantação bem-sucedida da Unificação de Mensagens. Você deve entender os diferentes aspectos de Unificação de Mensagens e cada componente e recurso, para que seja possível planejar adequadamente a infraestrutura e a implantação da Unificação de Mensagens. Alocar tempo para planejar e trabalhar nesses aspectos irá ajudar a evitar problemas, quando você implantar a Unificação de Mensagens na sua organização. Estas são algumas das áreas que você deve considerar e avaliar ao planejar a Unificação de Mensagens na sua organização:

  - As necessidades de sua organização.

  - Os requisitos de segurança em sua organização.

  - Sua telefonia existente, rede de comutação de circuito e seu sistema de caixa postal atual.

  - Seu design atual de rede IP de comutação de pacotes. Isso inclui pontos e dispositivos da conectividade da sua rede local (LAN) e WAN.

  - Seu ambiente atual de Active Directory.

  - O número de usuários aos quais você terá que oferecer suporte.

  - O número de servidores de Acesso para Cliente e Caixa de Correio de que você vai precisar.

  - Se você está integrando a UM ao Microsoft Lync Server para habilitar o Enterprise Voice.

  - A colocação de gateways VoIP, equipamento de telefonia e servidores de Acesso para Cliente e Caixa de Correio.

  - O tipo de implantação de UM: local ou híbrido.

  - Os requisitos de armazenamento dos usuários de caixa postal.

Voltar ao início

## Gerenciar UM com o EAC e o Shell

**Gerenciamento de EAC**

O Exchange 2013 oferece um console único e unificado de gerenciamento para sua organização, incluindo todos os componentes e recursos de UM. O Centro de Administração do Exchange (EAC) oferece uma interface otimizada, ágil para o gerenciamento de implantações locais, online ou híbridas. O EAC no Exchange 2013 substitui o Console de Gerenciamento do Exchange (EMC) e o Painel de Controle do Exchange (ECP) no Exchange 2010. Alguns dos recursos do EAC incluem:

  - **Modo de exibição de lista**   O modo de exibição de lista do EAC foi projetado para remover as limitações que existiam no ECP. O ECP era limitado a exibir até 500 objetos e, para exibir objetos que não estavam listados no painel de detalhes, você precisava usar pesquisas e filtros para encontrar esses objetivos específicos. No Exchange 2013, o limite de exibição de dentro do modo de exibição em lista do EAC é de, aproximadamente, 20.000 objetos. Além disso, foi adicionada paginação, para que você possa paginar os resultados. Você pode também configurar o tamanho da página e exportar para um arquivo CSV.

  - **Adicionar/Remover colunas para o modo de exibição de lista do Destinatário**   Você pode escolher que colunas exibir e salvar seus modos de exibição de lista personalizados.

  - **Proteger o diretório virtual do ECP**   Você pode acessar partições da Internet e de intranets de dentro do diretório virtual do IIS do ECP, para permitir ou bloquear recursos de gerenciamento. Com esse recurso, você pode permitir ou negar acesso a usuários tentando acessar o EAC da Internet fora do seu ambiente organizacional, enquanto ainda permite acesso às opções do Outlook Web App do usuário final.

  - **Gerenciamento de Pasta Pública**   No Exchange 2010 e no Exchange 2007, as pastas públicas eram gerenciadas através do console de administração de Pasta Pública. As pastas públicas agora estão no EAC, e você não precisa de uma ferramenta separada, para gerenciá-las.

  - **Notificações**   No Exchange 2013, o EAC agora tem um visualizador de Notificações, para que você possa exibir o status os processos de longa duração e, se preferir, receber uma notificação via email, quando o processo terminar.

  - **Editor de usuários o Controle de Acesso Baseado em Regras (RBAC)**   No Exchange 2010, você podia usar o Editor de Usuários do RBAC para adicionar usuários aos grupos de função de gerenciamento. No Exchange 2013, a funcionalidade do Editor de Usuários do RBAC agora está no EAC, e você não precisa de uma ferramenta separada para gerenciar o RBAC.

  - **Ferramentas de Unificação de Mensagem**   No Exchange 2010, você podia usar as ferramentas Estatísticas de Chamada e Logs de Chamadas de Usuários para ajudar a fornecer estatísticas de UM e informações sobre chamadas específicas para um usuário habilitado para UM. No Exchange 2013, as ferramentas Estatísticas de Chamada e Logs de Chamadas de Usuários agora estão no EAC, e você não precisa de uma ferramenta separada para gerenciá-las.

**Gerenciamento do shell**

O Shell de Gerenciamento do Exchange, baseado na tecnologia do Windows PowerShell, oferece uma interface de linha de comando poderosa que permite a automação de tarefas administrativas. Com o Shell, você pode gerenciar todos os aspectos do Exchange. Você pode habilitar novas contas de email, criar conectores de Envio e de Recebimento, configurar propriedades de banco de dados, gerenciar todos os aspectos da Unificação de Mensagens e mais. O Shell pode executar todas as tarefas que podem ser executadas pelo EAC, além de tarefas que não podem ser executadas no EAC. De fato, quando você fizer algo no EAC, será o Shell que vai fazer o trabalho nos bastidores.

Voltar ao início

## Documentação de Unificação de Mensagens

A tabela a seguir contém links para tópicos que irão ajudar você a aprender sobre e gerenciar a Unificação de Mensagens do Exchange.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Tópico</th>
<th>Descrição</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="new-voice-mail-features-exchange-2013-help.md">Novos recursos de caixa postal</a></p></td>
<td><p>Saiba mais sobre os novos recursos do Microsoft Exchange 2013.</p></td>
</tr>
<tr class="even">
<td><p><a href="planning-for-unified-messaging-exchange-2013-help.md">Planejamento para o Unified Messaging</a></p></td>
<td><p>Veja os conceitos e as informações de que você precisa para planejar uma implantação de Unificação de Mensagens.</p></td>
</tr>
<tr class="odd">
<td><p><a href="deploying-voice-mail-and-um-exchange-2013-help.md">Implantando a caixa postal e Unificação de MENSAGENS</a></p></td>
<td><p>Conheça os requisitos e etapas envolvidas na implantação da caixa postal e da UM.</p></td>
</tr>
<tr class="even">
<td><p><a href="um-languages-prompts-and-greetings-exchange-2013-help.md">Saudações e prompts de idiomas de Unificação de MENSAGENS</a></p></td>
<td><p>Saiba mais sobrte os pacotes e as configurações de idioma de UM.</p></td>
</tr>
<tr class="odd">
<td><p><a href="telephone-system-integration-with-um-exchange-2013-help.md">Integração com a Unificação de MENSAGENS do sistema de telefone</a></p></td>
<td><p>Saiba mais sobre a integração de sua rede telefônica com a UM.</p></td>
</tr>
<tr class="even">
<td><p><a href="connect-your-voice-mail-system-to-your-telephone-network-exchange-2013-help.md">Conectar seu sistema de caixa postal à sua rede de telefone</a></p></td>
<td><p>Saiba como usar e configurar componentes de UM para conectar sua rede de telefonia à UM do Exchange.</p></td>
</tr>
<tr class="odd">
<td><p><a href="automatically-answer-and-route-incoming-calls-exchange-2013-help.md">Responder e rotear as chamadas de entrada automaticamente</a></p></td>
<td><p>Saiba como criar atendedores automáticos de UM e gerenciar configurações para menus de navegação, saudações e horários comercial e não comercial.</p></td>
</tr>
<tr class="even">
<td><p><a href="set-up-voice-mail-for-users-exchange-2013-help.md">Configurar caixa postal para usuários</a></p></td>
<td><p>Saiba como criar e gerenciar políticas de caixa de correio de UM e como habilitar os usuários para UM.</p></td>
</tr>
<tr class="odd">
<td><p><a href="set-up-client-voice-mail-features-exchange-2013-help.md">Configurar Recursos do Cliente de Caixa Postal</a></p></td>
<td><p>Saiba como configurar os recursos de cliente a fim de permitir que os usuários acessem e gerenciem suas mensagens de correio de voz.</p></td>
</tr>
<tr class="even">
<td><p><a href="set-outlook-voice-access-pin-security-exchange-2013-help.md">Definir segurança de PIN do Outlook Voice Access</a></p></td>
<td><p>Saiba como definir os requisitos de PIN para usuários do Outlook Voice Access.</p></td>
</tr>
<tr class="odd">
<td><p><a href="protect-voice-mail-exchange-2013-help.md">Caixa postal protegida</a></p></td>
<td><p>Saiba como usar a UM para proteger as mensagens de voz.</p></td>
</tr>
<tr class="even">
<td><p><a href="run-reports-for-voice-mail-calls-exchange-2013-help.md">Executar relatórios para chamadas de correio de voz</a></p></td>
<td><p>Saiba mais sobre os relatórios de chamada da UM.</p></td>
</tr>
</tbody>
</table>

