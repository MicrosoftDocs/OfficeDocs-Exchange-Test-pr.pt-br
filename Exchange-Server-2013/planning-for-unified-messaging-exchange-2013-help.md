---
title: 'Planejamento para o Unified Messaging: Exchange 2013 Help'
TOCTitle: Planejamento para o Unified Messaging
ms:assetid: 942788b1-b19d-40b3-a52e-2e1fef8df3f9
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/JJ674306(v=EXCHG.150)
ms:contentKeyID: 50486150
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Planejamento para o Unified Messaging

 

_**Aplica-se a:** Exchange Server 2013, Exchange Server 2016_

_**Tópico modificado em:** 2016-12-09_

Ao planejar sua implantação da Unificação de mensagens (UM), há vários fatores que devem ser consideradas para poder implantar com êxito a Unificação de MENSAGENS. Você deve compreender os diferentes elementos da Unificação de mensagens e cada componente e recurso para que você possa planejar sua infraestrutura de Unificação de mensagens e implantação apropriadamente. Alocar hora para planejar e superar esses problemas ajudará a evitar problemas ao implantar a Unificação de mensagens em sua organização.

Você pode implantar a Unificação de mensagens em uma nova organização do Exchange ou atualizando de uma solução de correio de voz herdado ou de terceiros. Se você estiver atualizando, você precisará decidir se deseja converter os dispositivos que estão aceitando protocolos de telefonia baseada em circuitos para uma rede de dados usando IP ou implantar uma solução de Enterprise Voice, como o Microsoft Lync Server. Esta é a primeira etapa da preparação sozinho entender e implantar a Unificação de MENSAGENS para sua organização.

## Seu sistema de caixa postal de planejamento

Unificação de MENSAGENS oferece um repositório que pode ser acessado a partir de um telefone, um computador do usuário ou um dispositivo móvel de mensagens de email, fax e caixa postal. Os usuários podem acessar mensagens de voz, email, as informações de calendário e contatos pessoais que estão localizados em suas caixas de correio do Exchange de clientes de email como Outlook e Outlook Web App.

Servidores de acesso para cliente que executa o serviço Microsoft Exchange Unified Messaging roteador de chamada e os servidores de caixa de correio executando o serviço de Unificação de mensagens do Microsoft Exchange foram projetados para fornecer recursos de correio de voz para usuários em sua organização.

Servidores de caixa de correio se baseiam nos servidores de acesso para cliente para encaminhar o tráfego SIP de chamadas de entrada e, em seguida, estabelecer uma conexão com um gateway VoIP, IP PBX ou controlador de borda de sessão (SBC) e aceitam o tráfego de mídia RTP/SRTP. Todas as mensagens de email e fax de voz são enviadas do serviço de Unificação de mensagens do Microsoft Exchange em um servidor de caixa de correio deve ser entregue à caixa de correio do usuário. Para um usuário usar os recursos de caixa postal com o Unified Messaging, eles devem ter uma caixa de correio do Exchange.

## Planejando a implantação da Unificação de MENSAGENS

Em geral, mais simples a topologia de Unificação de mensagens, a Unificação de MENSAGENS mais fácil é implantar e manter. Instale o menor número de servidores de acesso para cliente e caixa de correio e crie componentes de Unificação de mensagens, no mínimo — como políticas de caixa de correio de Unificação de MENSAGENS, atendedores automáticos e planos de discagem de UM — conforme necessário dar suporte a suas metas comerciais e organizacionais. Empresas de grandes porte com ambientes complexos de rede e de telefonia, várias unidades de negócios ou outra complexidade exigirá mais planejamento que organizações menores com necessidades relativamente simples de Unificação de mensagens.

Estes são alguns das áreas que devem ser consideradas durante o planejamento para Unificação de mensagens em sua organização:

  - **Requisitos organizacionais**   Avalie as suas necessidades de negócios, a utilidade da implantação de um sistema de caixa postal, sua rede física e topologia de negócios e os requisitos de segurança para sua organização.

  - **Requisitos de telefonia**   Analise seu telefonia existente, rede baseada em circuitos comutados e sistema de caixa postal.

  - **Requisitos de rede**   Analise sua topologia de rede, atual comutação de pacotes IP design de sua rede incluindo seus pontos de conectividade de LAN e WAN e dispositivos.

  - **Active Directory (serviço de diretório)**   Inspecionar sua implementação atual e o design e pensar sobre como integrar a Unificação de MENSAGENS.

  - **Modelo de implantação**   Decida se desejar ter um híbrido, apenas online ou implantação de UM local.

  - **Requisitos do Exchange**   Determine o seguinte:
    
      - Quantos usuários estará usando caixa postal.
    
      - Quais recursos de Unificação de MENSAGENS e serviços que você deseja implantar, como chamadas simultâneas, acesso interno e externo para usuários, entrada de envio de fax, visualização da caixa postal e assim por diante.
    
      - O número de servidores de acesso para cliente e caixa de correio, que você precisará implantar.
    
      - Os requisitos de armazenamento e cotas para usuários de correio de voz.
    
      - O melhor design para resiliência de site e disponibilidade alta. Isso inclui os requisitos de sistema de Unificação de MENSAGENS, fornecendo uma implantação de Unificação de MENSAGENS altamente disponível e escalonável e os requisitos de hardware do sistema para assegurar o desempenho.

  - **Integração com os componentes de telefonia e dispositivos**   Decida quanto ao uso de equipamentos de telefonia tradicional ou Microsoft Lync Server. Considere onde colocar os gateways VoIP, equipamentos de telefonia e servidores de acesso para cliente e caixa de correio e se você deseja habilitar o Enterprise Voice em sua organização.

## Conectando a sua rede de telefonia

A Unificação de mensagens requer que você integre sua implantação do Exchange Server com seu sistema de telefonia existente ou integrá-lo com o Microsoft Lync Server. Você precisa fazer uma análise cuidadosa da sua infra-estrutura de telefonia existente e o Microsoft Lync Server e siga as etapas de planejamento corretas para poder implantar e gerenciar o correio de voz da Unificação de MENSAGENS com êxito.

**Gateways VoIP** Escolhendo o correto VoIP gateway, IP PBX, habilitados para SIP PBX ou SBC é a primeira etapa na integração com a Unificação de MENSAGENS de sua rede de telefonia. Você deve configurar esses dispositivos para trabalhar com a Unificação de MENSAGENS, implante os servidores de acesso para cliente e caixa de correio necessários e criar e configurar todos os componentes necessários de Unificação de MENSAGENS. Esses componentes permitem que você verifique a conexão da sua rede de protocolo baseado no circuito à sua rede de dados IP e habilitar a caixa postal para seus usuários.

**Microsoft Lync Server**   A Unificação de mensagens pode usar o Microsoft Lync Server para combinar mensagens de voz, mensagens instantâneas, presença avançada, conferência de áudio/vídeo e email em uma experiência de comunicação familiar e integrada. Integrando a Unificação de MENSAGENS e Microsoft Lync Server tem os seguintes benefícios:

  - Notificações de presença avançadas entre vários aplicativos que mantém os usuários informados da disponibilidade dos contatos.

  - Integração de mensagens instantâneas, voz mensagens, conferência, email e outros métodos de comunicação, que permite que os usuários selecionem o método mais apropriado para a tarefa. Os usuários também podem alternar de um método para outro conforme necessário.

  - Disponibilidade de alternativas de comunicação de qualquer local onde uma conexão à Internet esteja disponível.

  - Um cliente inteligente Microsoft Lync) para telefonia, mensagens instantâneas e conferência.

  - Continuidade da experiência do usuário entre diversos dispositivos.

Para obter mais informações sobre o Microsoft Lync Server, consulte [Microsoft Lync Server](https://go.microsoft.com/fwlink/p/?linkid=265752).


> [!TIP]
> Planejando e implantando a Unificação de mensagens podem representar determinados desafios. Dependendo da sua experiência técnica com sistemas de correio de voz e do Exchange, talvez você queira obter a assistência de uma especialista em Unificação de mensagens. Uma especialista em Exchange Unified Messaging ajudará a certificar-se de que haja uma transição suave de um sistema de correio de voz herdado ou de terceiros para Unificação de mensagens do Exchange. Realizando uma nova implantação ou atualizando um sistema de correio de voz herdado exige conhecimento significativo sobre gateways VoIP, PBXs e Unificação de mensagens. Para obter mais informações sobre como entrar em contato com uma especialista em Unificação de mensagens, consulte <A href="http://go.microsoft.com/fwlink/p/?linkid=262708">Microsoft Exchange Server 2013 Unified Messaging (UM) especialistas</A>.



## Etapas de implantação

Muitas opções de implantação estão disponíveis para Unificação de mensagens. Cada opção tem várias etapas em comum que são necessárias para criar um sistema flexível e altamente disponível para oferecer suporte a grandes números de usuários. Estas etapas são:

1.  Implante e configure seus componentes de telefonia ou o Microsoft Lync Server com Unificação de Mensagens.

2.  Verifique se você instalou corretamente os servidores de Acesso para Cliente e Caixa de Correio requeridos pela Unificação de Mensagens.

3.  Criar e configurar os componentes necessários de Unificação de mensagens, incluindo planos de discagem UM, gateways IP de UM, grupos de busca de Unificação de MENSAGENS e políticas de caixa de correio de Unificação de MENSAGENS.

4.  Execute tarefas de pós-implantação, incluindo Obtendo certificados para TLS mútuo, criar atendedores automáticos e configurando o envio de fax.

Para detalhes sobre como implantar a Unificação de Mensagens, consulte [Implementar o UM do Exchange 2013](deploy-exchange-2013-um-exchange-2013-help.md).

Se você estiver integrando o seu ambiente de Unificação de Mensagens ao Microsoft Lync Server, há considerações de planejamento adicionais. Para detalhes, consulte [Implantando a visão geral da Unificação de MENSAGENS do Exchange 2013 e Lync Server](deploying-exchange-2013-um-and-lync-server-overview-exchange-2013-help.md).

