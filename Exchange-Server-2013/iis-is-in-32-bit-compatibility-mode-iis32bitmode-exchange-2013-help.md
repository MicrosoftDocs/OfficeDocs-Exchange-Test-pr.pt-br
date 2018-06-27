---
title: 'O IIS é de mode_IIS32BitMode de compatibilidade de 32 bits: Exchange 2013 Help'
TOCTitle: O IIS é de mode_IIS32BitMode de compatibilidade de 32 bits
ms:assetid: 742dfc32-353c-46a2-830e-68aed6a68ce0
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/ms.exch.setupreadiness.iis32bitmode(v=EXCHG.150)
ms:contentKeyID: 50485821
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# O IIS é de mode\_IIS32BitMode de compatibilidade de 32 bits

 

_**Aplica-se a:**Exchange Server_

_**Tópico modificado em:**2012-06-05_

O conteúdo neste tópico não foi atualizado para o Microsoft Exchange Server 2013. Mesmo assim, ele ainda pode se aplicar ao Exchange 2013. Se você ainda precisar de ajuda, verifique os recursos da comunidade, abaixo.

Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), ou [Proteção do Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=285351).

A instalação do Microsoft® Exchange Server 2007 não pode continuar porque o Microsoft Internet Information Service (IIS) está em execução no modo de 32 bits neste computador de 64 bits.

Exchange 2007 requer que o IIS seja no modo de 64 bits completa quando ele é executado em um computador de 64 bits.

Para resolver esse problema, alternar o IIS para o modo de 64 bits e, em seguida, execute novamente a instalação do Microsoft Exchange.

Para alternar o IIS para o modo de 64 bits

1.  Abra um prompt de comando.

2.  Digite o seguinte:
    
    **cscript c:\\inetpub\\adminscripts\\adsutil.vbs SET /w3svc/AppPools/Enable32BitAppOnWin64 False**

3.  Pressione enter

