---
title: 'O Coordenador de transações distribuídas deve ser iniciado para instalar'
TOCTitle: O serviço Coordenador de transações distribuídas deve ser iniciado antes da instalação pode continue_MSDTCStopped
ms:assetid: 96e33c94-348e-4a0b-9585-9bee81be4355
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/ms.exch.setupreadiness.msdtcstopped(v=EXCHG.150)
ms:contentKeyID: 50486165
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# O serviço Coordenador de transações distribuídas deve ser iniciado antes da instalação pode continue\_MSDTCStopped

 

_**Aplica-se a:** Exchange Server_

_**Tópico modificado em:** 2012-06-05_

O conteúdo neste tópico não foi atualizado para o Microsoft Exchange Server 2013. Mesmo assim, ele ainda pode se aplicar ao Exchange 2013. Se você ainda precisar de ajuda, verifique os recursos da comunidade, abaixo.

Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), ou [Proteção do Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=285351).

Instalação do Microsoft Exchange Server 2007 não pode continuar porque ao tentar instalar as funções de servidor acesso para cliente ou Unificação de mensagens do servidor falhou porque o serviço Distributed Transaction Coordinator não estiver iniciado no computador de destino.

Instalação do Exchange 2007 exige que o computador que você está instalando o Microsoft Exchange para que o status do serviço Distributed Transaction Coordinator definido como **iniciado**.

O serviço Distributed Transaction Coordinator fornece serviços projetados para garantir transações bem-sucedidas e completas, mesmo com falhas de sistema, processo e falhas de comunicação.

Cada computador que participam de uma transação distribuída gerencia seus próprios recursos e dados e também atua em combinação com outros computadores na transação. Acima de tudo, uma transação distribuída deve confirmar ou anular seu trabalho inteiramente em todos os computadores participantes. O Distributed Transaction Coordinator desempenha a função de coordenação de transação para os componentes envolvidos e atua como um Gerenciador de transações para cada computador que gerencia as transações.

Funções de servidor tanto o servidor acesso para cliente e Unificação de mensagens tem dependências no serviço Coordenador de transações distribuídas.

Para resolver esse problema, verifique se o status do serviço Distributed Transaction Coordinator é definido como **iniciado** no computador local e, em seguida, execute novamente a instalação do Microsoft Exchange.

Para definir o status do serviço Coordenador de transações distribuídas para 'Iniciado'

1.  Clique com o botão **Meu computador** e, em seguida, clique em **Gerenciar**.

2.  Expanda o nó **serviços e aplicativos** e, em seguida, clique no nó de **Serviços**.

3.  No painel direito, localize o **Distributed Transaction Coordinator**.

4.  Clique com o botão **Distributed Transaction Coordinator** e clique em **Propriedades**.

5.  Defina o **Tipo de inicialização** para **automática** e o **status do serviço** como **iniciado**.

6.  Clique em **Aplicar** e em **OK**.

