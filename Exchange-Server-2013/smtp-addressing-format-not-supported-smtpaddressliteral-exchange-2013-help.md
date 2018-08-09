---
title: 'Formato de endereçamento SMTP não Supported_SMTPAddressLiteral'
TOCTitle: Formato de endereçamento SMTP não Supported_SMTPAddressLiteral
ms:assetid: b8b55917-d81f-4c0a-ad65-7bb10ac58df8
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/ms.exch.setupreadiness.smtpaddressliteral(v=EXCHG.150)
ms:contentKeyID: 50486473
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Formato de endereçamento SMTP não Supported\_SMTPAddressLiteral

 

_**Aplica-se a:** Exchange Server_

_**Tópico modificado em:** 2016-12-09_

O conteúdo neste tópico não foi atualizado para o Microsoft Exchange Server 2013. Mesmo assim, ele ainda pode se aplicar ao Exchange 2013. Se você ainda precisar de ajuda, verifique os recursos da comunidade, abaixo.

Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), ou [Proteção do Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=285351).

Instalação do Microsoft Exchange Server 2007 e o Exchange Server 2010 não pode continuar porque a diretiva de destinatário especificada usa um formato de endereço de Simple Mail Transfer Protocol (SMTP) sem suporte.

Requer a instalação do Exchange 2007 e Exchange 2010 que todos os endereços SMTP usados para as políticas de endereço de email não contêm literais de endereço IP, por exemplo: *user@\[10.10.1.1\]*.

Para resolver esse problema, altere o valor do endereço SMTP na diretiva de destinatário para que ele não contiver um endereço IP literal. Substituir colchetes (\[\]) e números (10.10.1.1) do endereço IP literal com o formato de nomenclatura do sistema de nome de domínio (DNS), por exemplo: *user@contoso.com*e, em seguida, execute novamente a instalação do Exchange.

Para obter mais informações sobre como gerenciar políticas de destinatário no Exchange Server 2007, consulte "Gerenciando email" políticas de endereços ([https://go.microsoft.com/fwlink/?LinkId=86653](https://go.microsoft.com/fwlink/?linkid=86653)).

Para obter mais informações sobre como gerenciar políticas de destinatário no Exchange Server 2010, consulte "Gerenciando email" políticas de endereços ([https://go.microsoft.com/fwlink/?LinkId=179519](https://go.microsoft.com/fwlink/?linkid=179519)).

