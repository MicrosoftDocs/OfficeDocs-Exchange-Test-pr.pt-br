---
title: 'Habilitar ou desabilitar a descriptografia do relatório de diário: Exchange 2013 Help'
TOCTitle: Habilitar ou desabilitar a descriptografia do relatório de diário
ms:assetid: 1dedbe73-2c1a-4b14-8799-5091aaec7965
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Dd638092(v=EXCHG.150)
ms:contentKeyID: 50485084
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Habilitar ou desabilitar a descriptografia do relatório de diário

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2016-12-09_

Habilitação descriptografia do relatório de diário permite que o agente de registro no diário anexar uma cópia descriptografada de uma mensagem protegida por direitos para o relatório de diário. Antes de habilitar a descriptografia do relatório de diário, você deve adicionar a caixa de correio de entrega federada ao grupo superusuários configurado em seu servidor do [Active Directory Rights Management Services (AD RMS)](https://technet.microsoft.com/en-us/library/hh831364.aspx) .

Para ver outras tarefas de gerenciamento relacionadas ao IRM (Gerenciamento de Direitos de Informação), consulte [Procedimentos de gerenciamento de direitos de informação](information-rights-management-procedures-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: 1 minuto

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Proteção por direitos" no tópico [Permissões de política e conformidade de mensagens](messaging-policy-and-compliance-permissions-exchange-2013-help.md).

  - Os membros do grupo de superusuários recebem uma licença de usuário de proprietário quando solicitam uma licença ao cluster do AD RMS. Isso permite a eles descriptografar todo o conteúdo protegido por DRM criado por esse cluster do AD RMS.

  - Um cluster do AD RMS deve ser instalado na floresta do Active Directory.

  - Caixa de correio Entrega Federada adicionada a um grupo de superusuários do AD RMS. Para obter detalhes, consulte [Adicionar a caixa de correio de Federação ao grupo de usuários do AD RMS Super](add-the-federation-mailbox-to-the-ad-rms-super-users-group-exchange-2013-help.md).

  - Não é possível usar o Centro de Administração do Exchange (EAC) para habilitar a descriptografia de relatório do diário. É necessário usar o Shell.

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>.



## O que você deseja fazer?

## Usar o Shell para habilitar a descriptografia de relatório do diário

Este exemplo habilita a descriptografia de relatório do diário para a organização do Exchange.

    Set-IRMConfiguration -JournalReportDecryptionEnabled $true

Para informações detalhadas de sintaxes e de parâmetros, consulte [Set-IRMConfiguration](https://technet.microsoft.com/pt-br/library/dd979792\(v=exchg.150\)).

## Usar o Shell para desabilitar a descriptografia de relatório do diário

Este exemplo desabilita a descriptografia de relatório do diário para a organização do Exchange.

    Set-IRMConfiguration -JournalReportDecryptionEnabled $false

Para informações detalhadas de sintaxes e de parâmetros, consulte [Set-IRMConfiguration](https://technet.microsoft.com/pt-br/library/dd979792\(v=exchg.150\)).

## Como saber se funcionou?

Para verificar se a descriptografia de relatório está habilitada ou desabilitada, execute o cmdlet **Get-IRMConfiguration** e verifique o valor da propriedade *JournalDecryptionEnabled*.

Para um exemplo de como verificar a configuração do IRM, consulte [Examples](https://technet.microsoft.com/pt-br/e1821219-fe18-4642-a9c2-58eb0aadd61a\(exchg.150\)#examples), em **Get-IRMConfiguration**.

