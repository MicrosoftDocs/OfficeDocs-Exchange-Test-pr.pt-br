---
title: 'Mover uma lista de endereços: Exchange 2013 Help'
TOCTitle: Mover uma lista de endereços
ms:assetid: c843bbd5-6c0e-41e1-b749-7ae87c1beb25
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Bb124534(v=EXCHG.150)
ms:contentKeyID: 50486634
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Mover uma lista de endereços

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2012-10-14_

Este tópico explica como mover uma lista de endereços existente para um novo contêiner na lista de endereços raiz.

Para tarefas de gerenciamento adicionais relacionadas a listas de endereços, consulte [Procedimentos da lista de endereços](address-list-procedures-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para concluir cada procedimento: 5 minutos.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Listas de endereços" no tópico [Endereço de email e permissões do catálogo de endereços](email-address-and-address-book-permissions-exchange-2013-help.md) .

  - Você não pode usar o Centro de Administração do Exchange (EAC) para executar esse procedimento. É necessário usar o Shell.

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>.



## Use o Shell para mover uma lista de endereços

Este exemplo usa o GUID da lista de endereços para mover a lista de endereços para o contêiner de 4 de construção, que está localizado no contêiner All users\\sales..

```powershell
Move-AddressList -Identity c3fffd8e-026b-41b9-88c4-8c21697ac8ac -Target "\All Users\Sales\Building4"
```

Digite **Y** para confirmar que você deseja mover esta lista de endereços e pressione ENTER.

Para detalhadas sobre sintaxe e informações de parâmetro, consulte [Move-AddressList](https://technet.microsoft.com/pt-br/library/bb124520\(v=exchg.150\)).

