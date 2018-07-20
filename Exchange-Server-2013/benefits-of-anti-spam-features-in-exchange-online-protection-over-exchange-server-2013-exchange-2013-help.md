---
title: 'Benefícios e recursos antispam do Exchange Online Protection no Exchange Server 2013: Exchange 2013 Help'
TOCTitle: Benefícios e recursos antispam do Exchange Online Protection no Exchange Server 2013
ms:assetid: 00e37a3c-3fbc-488f-bdad-d52a3c80fd72
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/JJ673032(v=EXCHG.150)
ms:contentKeyID: 50484857
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Benefícios e recursos antispam do Exchange Online Protection no Exchange Server 2013

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2016-05-26_

Estes são os benefícios do uso de proteção de anti-spam do Exchange na nuvem (Microsoft Exchange Online ou Microsoft Proteção do Exchange Online ) em vez de Microsoft Exchange Server 2013, que possui a maioria dos mesmos recursos antispam internas como Microsoft Exchange Server 2010:

  - **Mais controle e configuração mais fácil**   Os administradores podem usar o console de gerenciamento baseada na web Centro de administração do Exchange (EAC) para personalizar configurações de filtragem de forma que eles melhor atendem às necessidades da sua organização de spam. Não há nenhuma interface de usuário de antispam no Exchange Server 2013. Recursos de proteção antispam do EOP estão incluídos na Exchange Online

  - **Filtragem de conexão mais forte**   No Exchange 2013, listas de IP permitidos filtragem de conexão e listas de bloqueios de IP estão disponíveis somente se você instalar um servidor de transporte de borda na rede de perímetro. Para mais informações, consulte [Servidores de Transporte de Borda](edge-transport-servers-exchange-2013-help.md). Na nuvem, você pode optar por ignorar as mensagens de email enviadas de remetentes confiáveis (coletados de várias fontes de terceiros), garantindo que essas mensagens não sejam marcadas incorretamente como spam de filtragem de spam. Além disso, o serviço de filtragem hospedado usa listas de bloqueio da Microsoft e agregadas de fornecedores de listas para fornecer a filtragem de maior nível IP.

  - **Filtragem de conteúdo mais forte**   Você pode facilmente configurar sua política de filtro de conteúdo para:
    
      - Filtrar mensagens escritas em idiomas específicos.
    
      - Filtrar mensagens enviadas de determinados países ou regiões.
    
      - Marcar emails em massa (como anúncios e email marketing) como spam.
    
      - Pesquisar atributos em um email e agir em relação à mensagem, se ela combinar com um atributo de opção de spam avançado. Se você estiver preocupado com phishing, algumas dessas opções oferecem uma combinação de ID de Remetente e tecnologias SPF para autenticar e verificar se os emails não são falsificados.
    
    Além das opções de filtro de conteúdo acima que você pode configurar no EAC, o serviço de filtragem hospedado usa listas de URL adicionais para bloquear emails suspeitos que contenham URLs especificas no corpo da mensagem.

  - **Atualizações mais rápidas**   Atualizações de spam são propagadas mais rapidamente através da rede. No Exchange Server 2013, as atualizações ocorrem duas vezes por mês, enquanto o serviço é atualizado várias vezes por hora.

  - **Filtragem de saída**   A filtragem de spam de saída está sempre ativada se você usar o serviço hospedado para envio de email de saída, protegendo as organizações usando o serviço e seus destinatários pretendidos.

