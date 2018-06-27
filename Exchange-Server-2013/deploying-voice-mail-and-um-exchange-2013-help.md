---
title: 'Implantando a caixa postal e Unificação de MENSAGENS: Exchange 2013 Help'
TOCTitle: Implantando a caixa postal e Unificação de MENSAGENS
ms:assetid: 3df61b62-a1e4-41fb-969c-319189ae4e42
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/JJ673519(v=EXCHG.150)
ms:contentKeyID: 50485412
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Implantando a caixa postal e Unificação de MENSAGENS

 

_**Aplica-se a:**Exchange Server 2013, Exchange Server 2016_

_**Tópico modificado em:**2016-12-09_

A Unificação de Mensagens (UM) do Exchange permite que você forneça serviços de caixa postal a usuários em sua organização. Ao implantar a Unificação de Mensagens, você deve integrar sua implantação do Exchange Server com o sistema de telefonia existente para sua organização ou integrá-la ao Microsoft Lync Server. Uma implantação bem-sucedida exige uma análise cuidadosa da infraestrutura de telefonia existente para que você execute as etapas corretas de planejamento a fim de implantar e gerenciar a caixa postal na Unificação de Mensagens. Se você estiver integrando o Exchange ao Lync Server, você também deve se familiarizar com o produto.

Ao implantar a Unificação de Mensagens, você possui diversas opções, que dependem do hardware de telefonia encontrado em sua organização. Se você estiver conectando a UM à sua rede de telefonia, você pode ter uma das seguintes configurações de telefonia em sua organização:

  - Um ou vários gateways VoIP com um ou vários PBXs

  - Um ou vários PBXs IP

  - Um ou vários PBXs habilitados para SIP

  - Microsoft Office Communications Server 2007 R2 ou Microsoft Lync Server 2010 ou 2013


> [!WARNING]
> Ao implantar a UM do Exchange em um ambiente híbrido ou hospedado, você deve implantar os controladores de borda de sessão (SBCs). Os SBCs não permitem que a UM se conecte a uma rede de telefonia e não fornecem um tom de discagem para uma organização. No entanto, eles conectam sua implantação de UM local a um datacenter usando o protocolo IP em uma WAN pública ou privada.



**Hardware de Telefonia** A escolha correta do gateway VoIP, do PBX IP ou do SBC é apenas a primeira etapa na integração de sua rede de telefonia com a UM. Você deve configurar esses dispositivos para funcionar com a UM, implantar os servidores de Acesso para Cliente e Caixa de Correio e criar e configurar todos os componentes de UM necessários. Esses componentes permitem que você conecte sua rede de protocolo baseada em circuitos à sua rede de dados IP e habilite a caixa postal para usuários na sua organização. Para detalhes, consulte [Supervisor de telefonia para o Exchange 2013](telephony-advisor-for-exchange-2013-exchange-2013-help.md).

**Microsoft Lync Server**   A Unificação de Mensagens pode usar o Microsoft Lync Server para combinar caixa postal, mensagens instantâneas, presença avançada, conferência de áudio/vídeo e email em uma experiência de comunicação familiar e integrada. A integração entre a UM e o Lync Server tem os seguintes benefícios:

  - Notificações de presença avançadas entre vários aplicativos que mantém os usuários informados da disponibilidade dos contatos.

  - Integração de mensagens instantâneas, mensagens de voz, conferência, email e outros modos de comunicação, o que permite aos usuários selecionarem o método mais apropriado para a tarefa. Os usuários também podem alternar de um método para outro conforme necessário.

  - Disponibilidade de alternativas de comunicação de qualquer local onde uma conexão à Internet esteja disponível.

  - Um cliente inteligente Microsoft Lync) para telefonia, mensagens instantâneas e conferência.

  - Continuidade da experiência do usuário entre diversos dispositivos.

Para obter mais informações sobre o Lync Server, consulte [Microsoft Lync Server](https://go.microsoft.com/fwlink/p/?linkid=265752).

## Etapas de implantação

Muitas opções de implantação estão disponíveis para Unificação de Mensagens. Cada opção tem várias etapas em comum que são necessárias para criar um sistema escalonável e altamente disponível para suportar grande número de usuários. As etapas são as seguintes:

1.  Implante e configure seus componentes de telefonia ou o Microsoft Lync Server com Unificação de Mensagens.

2.  Verifique se você instalou corretamente os servidores de Acesso para Cliente e Caixa de Correio requeridos pela Unificação de Mensagens.
    

    > [!WARNING]
    > Você deve implantar pelo menos um servidor de Caixa de Correio do Exchange 2013 em sua organização antes de configurar os gateways VoIP ou PBXs IP para enviar tráfego SIP e RTP UM para os servidores de Acesso para Cliente do Exchange 2013.



3.  Crie e configure os componentes necessários de Unificação de Mensagens, incluindo planos de discagem de UM, gateways IP de UM, grupos de busca de UM e políticas de caixa do correio de UM.

4.  Execute tarefas de pós-implantação, incluindo implantar certificados para TLS mútuo, criar atendedores automáticos de UM e recursos de clientes.

Para detalhes sobre como implantar a Unificação de Mensagens, consulte [Implementar o UM do Exchange 2013](deploy-exchange-2013-um-exchange-2013-help.md).

Se você estiver integrando o seu ambiente de Unificação de Mensagens ao Microsoft Lync Server, há considerações de planejamento adicionais. Para detalhes, consulte [Implantando a visão geral da Unificação de MENSAGENS do Exchange 2013 e Lync Server](deploying-exchange-2013-um-and-lync-server-overview-exchange-2013-help.md).

