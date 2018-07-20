---
title: 'Não é possível remover o banco de dados de caixa de correio: Exchange 2013 Help'
TOCTitle: Não é possível remover o banco de dados de caixa de correio
ms:assetid: 5881e4c0-c2e2-48db-84b4-7f9ce3cf46a7
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/ms.exch.setupreadiness.unwillingtoremovemailboxdatabase(v=EXCHG.150)
ms:contentKeyID: 50485654
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Não é possível remover o banco de dados de caixa de correio

 

_**Aplica-se a:** Exchange Server_

_**Tópico modificado em:** 2012-11-08_

Microsoft Exchange Server 2013 instalação não pode continuar porque ele não é possível remover um banco de dados de caixa de correio de usuário do servidor local sem incorrer em perda de dados.

Exchange 2013 Instalação determina se todos os bancos de dados de caixa de correio foram removidos do servidor antes que a função de servidor de caixa de correio seja removida. No entanto, as caixas de correio do usuário ainda poderá permanecer no servidor.

Para resolver esse problema, mova qualquer caixa de correio no servidor para outro servidor Exchange ou, se as caixas de correio e os dados neles contidas não são mais necessários, desabilite as caixas de correio. Execute Exchange 2013 instalação novamente.

  - Para obter mais informações sobre como identificar uma caixa de correio no banco de dados, consulte [Get-Mailbox](https://technet.microsoft.com/pt-br/library/bb123685\(v=exchg.150\)).

  - Para obter mais informações sobre como mover uma caixa de correio, consulte [Movimentações de caixa de correio no Exchange 2013](mailbox-moves-in-exchange-2013-exchange-2013-help.md).

  - Para obter mais informações sobre como desabilitar uma caixa de correio, consulte [Disable-Mailbox](https://technet.microsoft.com/pt-br/library/aa997210\(v=exchg.150\)).

  - Para obter mais informações sobre como remover um banco de dados de caixa de correio, consulte [Gerenciar bancos de dados de caixa de correio no Exchange 2013](manage-mailbox-databases-in-exchange-2013-exchange-2013-help.md).

Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), ou [Proteção do Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=285351).

Você encontrou o que você está procurando? Por favor, separe um minuto do seu tempo para [enviar seus comentários para nós](mailto:exsetuphelpfeedback@microsoft.com?subject=exchange%202013%20setup%20help%20feedback) sobre as informações que você estava esperando encontrar.

