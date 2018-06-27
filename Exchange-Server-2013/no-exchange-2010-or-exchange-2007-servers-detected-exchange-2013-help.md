---
title: 'Nenhum servidor Exchange 2010 ou Exchange 2007 detectada: Exchange 2013 Help'
TOCTitle: Nenhum servidor Exchange 2010 ou Exchange 2007 detectada
ms:assetid: 789cabab-c769-4a16-a6c8-3db82cff8861
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/ms.exch.setupreadiness.noe14serverwarning(v=EXCHG.150)
ms:contentKeyID: 50485917
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Nenhum servidor Exchange 2010 ou Exchange 2007 detectada

 

_**Aplica-se a:**Exchange Server_

_**Tópico modificado em:**2012-11-08_

Microsoft Exchange Server 2013 instalação exibido esse aviso, porque nenhuma função de servidor Exchange Server 2010 ou Exchange Server 2007 existe na organização.


> [!WARNING]
> Se você continuar com a instalação do Exchange Server 2013, você não conseguirá adicionar servidores Exchange 2010 ou Exchange 2007 para a organização futuramente.



Antes de implantar Exchange 2013, considere os seguintes fatores que podem exigir a implantação de servidores Exchange 2010 ou Exchange 2007 antes da implantação Exchange 2013:

  - **Aplicativos desenvolvidos na empresa ou de terceiros**   Aplicativos desenvolvidos para versões anteriores do Exchange podem não ser compatíveis com Exchange 2013. Você pode precisar manter Exchange 2010 ou Exchange 2007 servidores para oferecer suporte a esses aplicativos.

  - **Requisitos de coexistência ou a migração**   Se você planeja migrar caixas de correio em sua organização, algumas soluções podem exigir o uso de servidores Exchange 2010 ou Exchange 2007.

Se você decidir que você precisa para implantar servidores Exchange 2010 ou Exchange 2007, você deve fazer isso antes de implantar o Exchange 2013. Active Directory deve ser preparado para cada versão do Exchange na seguinte ordem:

1.  Exchange 2007

2.  Exchange 2010

3.  Exchange 2013

Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), ou [Proteção do Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=285351).

Você encontrou o que você está procurando? Por favor, separe um minuto do seu tempo para [enviar seus comentários para nós](mailto:exsetuphelpfeedback@microsoft.com?subject=exchange%202013%20setup%20help%20feedback) sobre as informações que você estava esperando encontrar.

