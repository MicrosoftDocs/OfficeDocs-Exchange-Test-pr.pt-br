---
title: 'Notificações de entrega para administradores: Exchange 2013 Help'
TOCTitle: Notificações de entrega para administradores
ms:assetid: d98623d3-e0b7-4cb9-93fb-6351b4a06137
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/JJ919241(v=EXCHG.150)
ms:contentKeyID: 51407920
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Notificações de entrega para administradores

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2016-12-09_

Com os relatórios de entrega para administradores, você pode controlar as informações de entrega sobre as mensagens enviadas por ou recebidas de qualquer caixa de correio específica em sua organização. Especificamente, os relatórios de entrega para administradores usa o Centro de administração do Exchange (EAC) para executar uma pesquisa direcionada da mensagem logs de rastreamento. A pesquisa sempre destinada a uma caixa de correio específica. Você pode pesquisar mensagens enviadas pela caixa de correio ou enviada à caixa de correio, e você pode filtrar os resultados de pesquisa por assunto da mensagem.

O conteúdo do corpo da mensagem não é retornado em um relatório de entrega, mas a linha de assunto é exibida nos resultados. Se você quiser pesquisar as caixas de correio em sua organização para mensagens de email específicos com base no conteúdo da mensagem, consulte [Descoberta Eletrônica In-loco](in-place-ediscovery-exchange-2013-help.md).

Pesquisas de relatório de entrega pode ser útil nas seguintes situações:

  - Um gerente oferece uma análise mais baixa para um estagiário porque o estagiário não ativar em uma atribuição no momento. O estagiário insiste que ele enviou uma mensagem com a atribuição anexada. O Gerenciador de pergunta para verificar o status da mensagem.

  - Um boletim de segurança foi enviado aos usuários, solicitando que eles respondam imediatamente, mas ninguém tiver respondido. Eles ignoram a mensagem ou elas simplesmente não recebeu-lo?

  - Os usuários reclamam que ninguém está recebendo suas mensagens. Eles verificar status de entrega de emails, mas não consegue descobrir o que está acontecendo. Isso pode ocorrer porque uma regra é aplicada às mensagens no nível da organização.

Depois de criar uma pesquisa de relatórios de entrega, o relatório de entrega resultante mostrará as informações a seguir: quem a mensagem foi enviada de e para, a linha de assunto e quando a mensagem foi enviada. O relatório de entrega também mostra o status de entrega da mensagem e os motivos pelos quais entrega pode ser atrasada ou falhou.

## Mais sobre os relatórios de entrega

  - Aqui está como criar um novo relatório de entrega: [Acompanhar mensagens com notificações de entrega](track-messages-with-delivery-reports-exchange-2013-help.md).

  - Local organizações do Exchange podem usar o Shell de gerenciamento do Exchange para consultar a diretamente os logs de rastreamento de mensagens. Para obter mais informações, consulte [Logs de rastreamento de mensagens de pesquisa](search-message-tracking-logs-exchange-2013-help.md).

  - Os usuários podem controlar suas próprias mensagens. Para obter mais informações, consulte [Relatórios de entrega para usuários](https://go.microsoft.com/fwlink/?linkid=279920).

  - Se sua organização contiver uma versão anterior do Exchange, você precisa considerar como a notificações de entrega recurso no Exchange 2013 funciona nas versões do Exchange.
    
      - notificações de entrega Exchange 2013 podem controlar mensagens entre os servidores de Exchange 2010 no mesmo site do Active Directory.
    
      - notificações de entrega Exchange 2013 não é possível controlar mensagens entre os servidores de Exchange 2007 no mesmo site do Active Directory. O recurso de relatórios de entrega usa uma chamada de procedimento remoto e uma interface de serviço web que não existe em Exchange 2007.

