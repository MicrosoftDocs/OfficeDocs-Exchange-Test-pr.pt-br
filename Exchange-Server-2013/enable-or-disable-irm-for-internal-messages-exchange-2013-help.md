---
title: 'Habilitar ou desabilitar o IRM para mensagens internas: Exchange 2013 Help'
TOCTitle: Habilitar ou desabilitar o IRM para mensagens internas
ms:assetid: a6a17f57-5304-41f1-954d-7301857d54a1
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Bb124077(v=EXCHG.150)
ms:contentKeyID: 50486329
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Habilitar ou desabilitar o IRM para mensagens internas

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2012-10-12_

No Microsoft Exchange Server 2013, gerenciamento de direitos de informação (IRM) é habilitado por padrão para mensagens internas. Isso permite que você crie regras de proteção de transporte e o Microsoft Outlook regras de proteção de IRM Proteja mensagens no transporte e em Microsoft Outlook 2010 e clientes posteriores. Habilitar o IRM para mensagens internas é um pré-requisito para todos os outros recursos IRM no Exchange Server 2013, como o IRM no Microsoft Exchange ActiveSync, descriptografia de regra de diário, IRM no Microsoft OfficeOutlook Web App e a descriptografia de transporte.


> [!CAUTION]
> Desabilitar o IRM para mensagens internas desabilita todos os recursos IRM na organização Exchange. Os recursos IRM do lado do cliente no Outlook (por exemplo, a capacidade de ler, responder, encaminhar e criar mensagens protegidas por IRM usando um servidor de Rights Management Services (AD RMS) Active Directory ) não serão afetados.



Para tarefas de gerenciamento adicionais relacionadas a IRM, consulte [Procedimentos de gerenciamento de direitos de informação](information-rights-management-procedures-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: 1 minuto.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Proteção por direitos" no tópico [Permissões de política e conformidade de mensagens](messaging-policy-and-compliance-permissions-exchange-2013-help.md).

  - Você não pode usar o Centro de administração do Exchange (EAC) para habilitar ou desabilitar o IRM para mensagens internas. Você deve usar o Shell.

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>.



## Use o Shell para habilitar o IRM para mensagens internas

Este exemplo habilita o IRM para mensagens internas para a organização Exchange.

    Set-IRMConfiguration -InternalLicensingEnabled $true

Para informações detalhadas de sintaxes e de parâmetros, consulte [Set-IRMConfiguration](https://technet.microsoft.com/pt-br/library/dd979792\(v=exchg.150\)).

## Use o Shell para desabilitar o IRM para mensagens internas

Este exemplo desabilita o IRM para mensagens internas para a organização Exchange.

    Set-IRMConfiguration -InternalLicensingEnabled $false

Para informações detalhadas de sintaxes e de parâmetros, consulte [Set-IRMConfiguration](https://technet.microsoft.com/pt-br/library/dd979792\(v=exchg.150\)).

## Como saber se funcionou?

Para verificar que você tiver habilitado ou desabilitado o IRM para mensagens internas, use o cmdlet [Get-IRMConfiguration](https://technet.microsoft.com/pt-br/library/dd776120\(v=exchg.150\)) para verificar a configuração.

