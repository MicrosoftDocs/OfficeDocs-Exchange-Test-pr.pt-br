---
title: 'O serviço de sistema de eventos COM + deve ser iniciado antes da instalação pode continue_EventSystemStopped: Exchange 2013 Help'
TOCTitle: O serviço de sistema de eventos COM + deve ser iniciado antes da instalação pode continue_EventSystemStopped
ms:assetid: 3b8d2ba3-87fb-4749-b4d1-5dfec97e1ca4
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/ms.exch.setupreadiness.eventsystemstopped(v=EXCHG.150)
ms:contentKeyID: 50485403
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# O serviço de sistema de eventos COM + deve ser iniciado antes da instalação pode continue\_EventSystemStopped

 

_**Aplica-se a:** Exchange Server_

_**Tópico modificado em:** 2012-06-05_

O conteúdo neste tópico não foi atualizado para o Microsoft Exchange Server 2013. Mesmo assim, ele ainda pode se aplicar ao Exchange 2013. Se você ainda precisar de ajuda, verifique os recursos da comunidade, abaixo.

Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), ou [Proteção do Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=285351).

Instalação do Microsoft Exchange Server 2007 não pode continuar porque ao tentar instalar as funções de servidor Transporte de borda ou de servidor acesso para cliente falhou porque o serviço de sistema de eventos COM + não é iniciado no computador de destino.

Instalação do Exchange 2007 exige que o computador que você está instalando o Microsoft Exchange para que o status do serviço de sistema de eventos COM + definido como **iniciado**.

O serviço de sistema de eventos COM + oferece suporte a notificação de evento do sistema para componentes COM +, que fornecem a distribuição automática de eventos aos componentes COM assinantes.

Funções de servidor a servidor acesso para cliente e o transporte de borda tem dependências em componentes COM + que assinarem o serviço de sistema de eventos COM +.

Para resolver esse problema, verifique se o status do serviço de sistema de eventos COM + é definido como **iniciado** no computador local e, em seguida, execute novamente a instalação do Microsoft Exchange.

Para definir o status do serviço do sistema de eventos COM + para 'Iniciado'

1.  Clique com o botão **Meu computador** e, em seguida, clique em **Gerenciar**.

2.  Expanda o nó **serviços e aplicativos** e, em seguida, clique no nó de **Serviços**.

3.  No painel direito, localize o **Sistema de eventos Com +**.

4.  **Com + sistema de eventos** do mouse em e clique em **Propriedades**.

5.  Defina o **Tipo de inicialização** para **automática** e o **status do serviço** como **iniciado**.

6.  Clique em **Aplicar** e em **OK**.

