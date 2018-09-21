---
title: 'Gerenciar domínios remotos: Exchange 2013 Help'
TOCTitle: Gerenciar domínios remotos
ms:assetid: 41a86907-bd9e-40d0-94d3-6deb95a0bffa
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Aa997639(v=EXCHG.150)
ms:contentKeyID: 52058409
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
f1_keywords:
- Microsoft.Exchange.Management.SnapIn.Esm.OrganizationConfiguration.NewRemoteDomainWizardForm.NewRemoteDomainWizardPage
ms.translationtype: MT
---

# Gerenciar domínios remotos

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2015-04-13_

Domínios remotos são domínios de SMTP que são externos à sua organização do Microsoft Exchange. Você pode criar entradas de domínios remotos para definir as configurações para transferência de mensagens entre a organização do Exchange e domínios externos específicos. As configurações na entrada de domínio remoto para um domínio externo específico substituem as configurações no domínio remoto padrão que normalmente se aplicam a todos os destinatários externos. As configurações do domínio remoto são globais para a organização do Exchange.

Se você remover uma entrada de domínio remoto, as configurações para transferência de mensagens não se aplicarão mais às mensagens enviadas para o domínio remoto. A remoção de uma entrada de domínio remoto não desabilita o fluxo de mensagens para o domínio remoto. Depois da remoção da entrada do domínio remoto, as definições de configuração do domínio remoto padrão se aplicam a novas mensagens enviadas para esse domínio. Você não pode remover o domínio remoto padrão.

## O que você precisa saber antes de começar?

  - Tempo estimado para finalizar cada procedimento: 10 minutos.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Domínios remotos" no tópico [Permissões de fluxo de email](mail-flow-permissions-exchange-2013-help.md).

  - Você só pode usar o Shell para executar esse procedimento.

  - Não é possível criar um domínio remoto para um espaço de endereço configurado como um domínio aceito em sua organização. Por exemplo, se sua organização aceita emails de fabrikam.com, você não pode criar um domínio remoto fabrikam.com.

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>.



## O que você deseja fazer?

## Usar o Shell para criar um domínio remoto

Para criar uma nova entrada de domínio remoto, use a sintaxe a seguir.

```powershell
New-RemoteDomain -Name <Descriptive Name> -DomainName <SMTP address space>
```

Este exemplo cria uma entrada de domínio remoto para mensagens enviadas ao domínio contoso.com.

```powershell
New-RemoteDomain -Name Contoso -DomainName contoso.com
```

Este exemplo cria uma entrada de domínio remoto para mensagens enviadas para o domínio fabrikam.com e todos os subdomínios.

    New-RemoteDomain -Name Fabrikam -DomainName *.fabrikam.com

## Como saber se funcionou?

Para verificar se você criou com êxito um banco de dados remoto, faça o seguinte:

1.  Execute o comando **Get-RemoteDomain** e verifique se o domínio remoto está listado.

2.  Execute o comando `Get-RemoteDomain <Remote Domain Name> | Format-List` para verificar as configurações no novo domínio remoto. Envie uma mensagem de teste para um destinatário no espaço de endereço especificado na nova entrada do domínio remoto e verifique se as configurações da mensagem correspondem às especificadas pela nova entrada de domínio remoto.

## Usar o Shell para configurar um domínio remoto

Defina as configurações na entrada de domínio remoto usando o cmdlet **Set-RemoteDomain**. Existem várias configurações diferentes que estão relacionadas a respostas automáticas, formato e codificação da mensagem e outras configurações de mensagem. Para obter mais informações, consulte [Set-RemoteDomain](https://technet.microsoft.com/pt-br/library/aa997857\(v=exchg.150\)).

Para configurar domínios remotos para cenários específicos, consulte os seguintes tópicos:

  - [Configurar um domínio remoto respostas de ausência temporária](configure-remote-domain-out-of-office-replies-exchange-2013-help.md)

  - [Configurar as respostas automáticas de domínio remoto](configure-remote-domain-automatic-replies-exchange-2013-help.md)

  - [Configurar os relatórios de mensagem do domínio remoto](configure-remote-domain-message-reporting-exchange-2013-help.md)

## Use o shell para remover um domínio remoto

Para remover uma entrada de domínio remoto, use a sintaxe a seguir.

```powershell
Remove-RemoteDomain <RemoteDomainName>
```

Este exemplo remove a entrada de domínio remoto chamada Contoso

```powershell
Remove-RemoteDomain Contoso
```

## Como saber se funcionou?

Para verificar se você removeu com êxito o domínio remoto, siga este procedimento:

1.  Execute o comando **Get-RemoteDomain** e verifique se o domínio remoto não está listado.

2.  Execute o comando `Get-RemoteDomain Default | Format-List` para verificar as configurações no domínio remoto padrão. Envie uma mensagem de teste para um destinatário no espaço de endereço especificado no domínio remoto removido e verifique se as configurações da mensagem correspondem às especificadas pelo domínio remoto padrão.

