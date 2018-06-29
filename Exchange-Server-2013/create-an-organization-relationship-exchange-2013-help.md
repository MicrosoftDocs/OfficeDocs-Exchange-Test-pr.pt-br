---
title: 'Criar um relacionamento de organização: Exchange 2013 Help'
TOCTitle: Criar um relacionamento de organização
ms:assetid: 5ea61b96-c8ca-44fc-b8b5-ca4341af36a6
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/JJ657451(v=EXCHG.150)
ms:contentKeyID: 50485709
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Criar um relacionamento de organização

 

_**Aplica-se a:**Exchange Server 2013_

_**Tópico modificado em:**2015-04-07_

Configure um relacionamento de organização para compartilhar informações de calendário com um parceiro de negócios externos. Você pode configurar um relacionamento de organização entre duas organizações federadas Exchange 2013 ou entre uma organização federada Exchange 2013 e organizações federadas Exchange 2010. Você também pode configurar um relacionamento de organização entre sua organização do Exchange no local e uma organização do Office 365.


> [!IMPORTANT]
> Criar um relacionamento de organização é uma das várias etapas para configurar o compartilhamento federado na sua organização do Exchange e requer a configuração de uma confiança de federação na sua organização do Exchange local.



Para saber mais sobre compartilhamento federado, consulte [Compartilhamento](sharing-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: 15 minutos.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o "Calendário e permissões de compartilhamento? seção no tópico [Permissões de destinatários](recipients-permissions-exchange-2013-help.md) .

  - É preciso configurar uma relação de confiança de federação ativa para a organização do Exchange local. Para detalhes, consulte [Configurar uma confiança de Federação](configure-a-federation-trust-exchange-2013-help.md).

  - A organização externa que você deseja configurar no relacionamento da organização também deve ter uma confiança de Federação estabelecida com o sistema de autenticação AD do Azure. Você usará o domínio federado primário para a organização do Exchange externa ao configurar o relacionamento da organização.

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

## O que você deseja fazer?

## Usar o EAC para criar um relacionamento de organização

1.  Em um servidor do Exchange 2013 na organização local, navegue até **organização** \> **compartilhamento**.

2.  Em **Compartilhamento de Organização**, clique em **Novo**![Ícone Adicionar](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Ícone Adicionar").

3.  Em **novo relacionamento de organização**, na caixa **Nome do relacionamento**, digite um nome amigável para o relacionamento de organização.

4.  Na caixa **Domínios com os quais compartilhar**, digite o domínio federado ou o subdomínio federado para a organização do Office 365 ou do Exchange local que você deseja permitir que veja seus calendários. Se precisar adicionar vários domínios à organização externa, separe-os com vírgulas. Por exemplo, **contoso.com, service.contoso.com**.

5.  Desmarque a caixa de seleção **Habilitar compartilhamento de informações de disponibilidade de calendário** para ativar o compartilhamento de calendário com os domínios listados. Defina o nível de compartilhamento para as informações de disponibilidade de calendário e defina quais usuários poderão compartilhar informações de disponibilidade.
    
    Para definir o nível de disponibilidade de acesso, selecione uma das seguintes opções:
    
      - **Informações de disponibilidade de calendário somente com hora**
    
      - **Disponibilidade de calendário com hora, assunto e local**
    
    Para definir quais usuários internos compartilharão as informações de disponibilidade de calendário, selecione uma destas opções:
    
      - **Todos em sua organização**
    
      - **Um grupo de segurança especificado**
        
        Para especificar um grupo de segurança, clique em **procurar**.

6.  Clique em **salvar** para criar o relacionamento da organização.

## Usar o Shell para criar um relacionamento de organização

Este exemplo cria um relacionamento de organização com Contoso, Ltd com as seguintes condições:

  - O relacionamento de organização é habilitado para contoso.com, northamerica.contoso.com e europe.contoso.com.

  - O acesso de disponibilidade está habilitado.

  - A organização da solicitação recebe as informações de tempo de disponibilidade, assunto e localização da organização de destino.

<!-- end list -->

    New-OrganizationRelationship -Name "Contoso" -DomainNames "contoso.com","northamerica.contoso.com","europe.contoso.com" -FreeBusyAccessEnabled $true -FreeBusyAccessLevel LimitedDetails

Este exemplo tenta descobrir automaticamente informações de configuração de descoberta da organização do Exchange externa Contoso.com, utilizando os nomes de domínio fornecidos no cmdlet **Get-FederationInformation**. Se você usar esse método para criar seu relacionamento de organização, primeiro verifique se criou um identificador de organização, usando o cmdlet **Set-FederatedOrganizationIdentifier**.

    Get-FederationInformation -DomainName Contoso.com | New-OrganizationRelationship -Name "Contoso" -FreeBusyAccessEnabled $true -FreeBusyAccessLevel -LimitedDetails

Para obter informações detalhadas sobre sintaxe e parâmetros, consulte [Get-FederationInformation](https://technet.microsoft.com/pt-br/library/dd351221\(v=exchg.150\)) e [New-OrganizationRelationship](https://technet.microsoft.com/pt-br/library/ee332357\(v=exchg.150\)).

Este exemplo cria um relacionamento de organização com Fourth Coffee. Neste exemplo, as configurações de conexão com a organização do Exchange externa são fornecidas. A seguintes condições se aplicam:

  - O relacionamento de organização é estabelecido com o domínio fourthcoffee.com. um domínio federado de Fourth Coffee.

  - A URL de aplicativo de Serviços Web do Exchange é mail.fourthcoffee.com.

  - A URL de Descoberta Automática é https://mail.fourthcoffee.com/autodiscover/autodiscover.svc/wssecurity.

  - O acesso de disponibilidade está habilitado.

  - A organização solicitante recebe apenas informações de disponibilidade com o horário.

<!-- end list -->

    New-OrganizationRelationship -Name "Fourth Coffee" -DomainNames "fourthcoffee.com" -FreeBusyAccessEnabled $true -FreeBusyAccessLevel -AvailabilityOnly -TargetAutodiscoverEpr "https://mail.fourthcoffee.com/autodiscover/autodiscover.svc/wssecurity" -TargetApplicationUri "mail.fourthcoffee.com"

Para informações detalhadas de sintaxes e de parâmetros, consulte [New-OrganizationRelationship](https://technet.microsoft.com/pt-br/library/ee332357\(v=exchg.150\)).

## Como saber se funcionou?

A conclusão bem-sucedida do assistente **Novo relacionamento de organização** será a primeira indicação de que a criação do relacionamento da organização decorreu conforme o esperado.

Para verificar mais ainda se você criou o relacionamento de organização com êxito, execute o seguinte comando do Shell, para verificar as informações de relacionamento de organização:

    Get-OrganizationRelationship | format-list


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>.


