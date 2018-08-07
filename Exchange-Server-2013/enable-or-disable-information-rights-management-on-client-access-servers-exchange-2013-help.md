---
title: 'Habilitar ou desabilitar IRM em servidores de Acesso para Cliente'
TOCTitle: Habilitar ou desabilitar o gerenciamento de direitos de informação nos servidores de acesso do cliente
ms:assetid: c7ce069b-a572-4755-90a3-7105472e4c83
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Dd876938(v=EXCHG.150)
ms:contentKeyID: 50486626
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Habilitar ou desabilitar o gerenciamento de direitos de informação nos servidores de acesso do cliente

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2016-12-09_

Habilitar o gerenciamento de direitos de informação (IRM) nos servidores de acesso para cliente permite que os seguintes recursos:

  - Microsoft OfficeOutlook Web App

  - IRM no Microsoft Exchange ActiveSync

Quando o IRM está habilitado nos servidores de acesso para cliente, Outlook Web App usuários podem proteger o IRM mensagens aplicando um modelo do [Active Directory Rights Management Services (AD RMS)](https://technet.microsoft.com/en-us/library/hh831364.aspx) criado no cluster do AD RMS. Outlook Web App usuários também podem exibir mensagens protegidas por IRM e suporte para anexos. Antes de habilitar o IRM nos servidores de acesso para cliente, você deve adicionar a caixa de correio de Federação ao grupo de superusuários no cluster do AD RMS.


> [!IMPORTANT]
> Membros do grupo recebem um proprietário superusuários usam licença quando eles solicitam uma licença do cluster do AD RMS. Isso permite que eles descriptografar todo o conteúdo protegido por RMS por que o cluster.



Para tarefas de gerenciamento adicionais relacionadas a IRM, consulte [Procedimentos de gerenciamento de direitos de informação](information-rights-management-procedures-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: 1 minuto.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada de "Informações de configuração de Rights Management (IRM)" no tópico [Permissões de política e conformidade de mensagens](messaging-policy-and-compliance-permissions-exchange-2013-help.md) .

  - Um cluster do AD RMS deve ser instalado na floresta do Active Directory.

  - Na caixa de correio de Federação foi adicionada ao grupo de superusuários AD RMS. Para obter instruções detalhadas, consulte [Adicionar a caixa de correio de Federação ao grupo de usuários do AD RMS Super](add-the-federation-mailbox-to-the-ad-rms-super-users-group-exchange-2013-help.md).

  - Recursos de IRM devem ser habilitados para a organização. Para obter instruções detalhadas, consulte [Habilitar ou desabilitar o IRM para mensagens internas](enable-or-disable-irm-for-internal-messages-exchange-2013-help.md).

  - Você pode usar o cmdlet **Set-IRMConfiguration** para habilitar ou desabilitar o IRM no Outlook Web App e o IRM no Exchange ActiveSync para a organização inteira Exchange ou níveis específicos.
    
    Você pode controlar o IRM no Outlook Web App nos seguintes níveis:
    
      - **Por diretório virtual do Outlook Web App**   Para habilitar ou desabilitar o IRM no Outlook Web App para um diretório virtual do Outlook Web App, use o cmdlet **Set-OWAVirtualDirectory** e defina o parâmetro *IRMEnabled* para `$false` ou `$true` (padrão). Isso permite que você desabilite o IRM no Outlook Web App para um diretório virtual em um servidor de Acesso para Cliente do Exchange 2013, ao mesmo tempo em que o mantém habilitado em outro diretório virtual em um servidor de Acesso para Cliente diferente.
    
      - **Por diretiva de caixa de correio do Outlook Web App**   Para habilitar ou desabilitar o IRM no Outlook Web App para uma diretiva de caixa de correio do Outlook Web App, use o cmdlet **Set-OWAMailboxPolicy** e defina o parâmetro *IRMEnabled* para `$false` ou `$true` (padrão). Isso permite que você habilite o IRM no Outlook Web App para um conjunto de usuários e o desabilite para outro conjunto de usuários, atribuindo a eles uma diretiva de caixa de correio do Outlook Web App diferente.
    
    Você pode controlar o IRM no Exchange ActiveSync por Exchange ActiveSync política de caixa de correio. Para desabilitar ou habilitar o IRM no Exchange ActiveSync para uma política de caixa de correio Exchange ActiveSync, use o cmdlet **Set-ActiveSyncMailboxPolicy** e defina o parâmetro *IRMEnabled* para `$false` ou `$true` (padrão). Isso permite que você habilitar o IRM no Exchange ActiveSync para um conjunto de usuários e desabilitá-lo para outro conjunto de usuários, atribuindo-lhes uma política de caixa de correio diferentes Exchange ActiveSync.

  - Você não pode usar o Centro de administração do Exchange (EAC) para habilitar ou desabilitar o IRM nos servidores de acesso para cliente. Você deve usar o Shell.

## O que você deseja fazer?

## Use o Shell para habilitar o IRM nos servidores de acesso para cliente

Este exemplo habilita o IRM em um servidor de acesso para cliente para uma organização de Exchange.

    Set-IRMConfiguration -ClientAccessServerEnabled $true

Para obter informações detalhadas de sintaxes e de parâmetros, confira [Set-IRMConfiguration](https://technet.microsoft.com/pt-br/library/dd979792\(v=exchg.150\)).

## Use o Shell para desabilitar o IRM nos servidores de acesso para cliente

Este exemplo desabilita o IRM em um servidor de acesso para cliente para uma organização Exchange.

    Set-IRMConfiguration -ClientAccessServerEnabled $false

Para informações detalhadas de sintaxes e de parâmetros, consulte [Set-IRMConfiguration](https://technet.microsoft.com/pt-br/library/dd979792\(v=exchg.150\)).

## Como saber se funcionou?

Para verificar que você tenha habilitado ou desabilitado IRM nos servidores de acesso para cliente com êxito, faça o seguinte:

  - Execute o cmdlet **Get-IRMConfiguration** e verificar o valor da propriedade *ClientAccessServerEnabled* .
    
    Para obter um exemplo de como recuperar a configuração do IRM, consulte os [Examples](https://technet.microsoft.com/pt-br/e1821219-fe18-4642-a9c2-58eb0aadd61a\(exchg.150\)#examples) em **Get-IRMConfiguration**.

  - Use Outlook Web App para criar ou ler uma mensagem protegida por IRM.

