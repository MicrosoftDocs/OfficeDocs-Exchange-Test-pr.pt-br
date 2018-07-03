---
title: 'Esse servidor é a origem para um Connector_ServerIsSourceForSendConnector enviar: Exchange 2013 Help'
TOCTitle: Esse servidor é a origem para um Connector_ServerIsSourceForSendConnector enviar
ms:assetid: 151c0014-c90c-4c52-8e74-4b3f1bc7aaf1
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/ms.exch.setupreadiness.serverissourceforsendconnector(v=EXCHG.150)
ms:contentKeyID: 50484989
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Esse servidor é a origem para um Connector\_ServerIsSourceForSendConnector enviar

 

_**Aplica-se a:** Exchange Server_

_**Tópico modificado em:** 2016-12-09_

O conteúdo neste tópico não foi atualizado para o Microsoft Exchange Server 2013. Mesmo assim, ele ainda pode se aplicar ao Exchange 2013. Se você ainda precisar de ajuda, verifique os recursos da comunidade, abaixo.

Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), ou [Proteção do Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=285351).

Instalação do Microsoft Exchange Server 2007 não pode continuar porque falhou ao tentar remover a função de servidor de transporte de Hub. O computador local é a origem para um ou mais conectores de envio na organização do Exchange.

Um conector de envio representa um gateway lógico através do qual as mensagens de saída são enviadas.

Instalação do Exchange 2007 requer que todos os conectores de envio de uma organização do Exchange deve ser movidos ou excluídos do computador servidor Transporte de Hub para a função de servidor possa ser excluída.

Para resolver esse problema, mover ou excluir todos os conectores de envio do computador local e, em seguida, execute novamente a instalação.

Para obter mais informações sobre como modificar ou remover conectores de envio, consulte os seguintes tópicos na documentação do produto Exchange Server 2007:

  - "Como remover um conector de envio" ([https://go.microsoft.com/fwlink/?LinkId=86655](https://go.microsoft.com/fwlink/?linkid=86655)).

  - "Como modificar a configuração de um conector de envio" ([https://go.microsoft.com/fwlink/?LinkId=86656](https://go.microsoft.com/fwlink/?linkid=86656)).

