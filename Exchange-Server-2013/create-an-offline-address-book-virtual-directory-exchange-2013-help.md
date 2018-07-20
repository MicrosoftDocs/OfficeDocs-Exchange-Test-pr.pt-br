---
title: 'Criar um diretório virtual do catálogo de endereços offline: Exchange 2013 Help'
TOCTitle: Criar um diretório virtual do catálogo de endereços offline
ms:assetid: 2c70e21f-2b12-414a-9e8c-65634a767c72
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Aa996917(v=EXCHG.150)
ms:contentKeyID: 50485244
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Criar um diretório virtual do catálogo de endereços offline

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2012-10-16_

O diretório virtual do OAB é a distribuição do OAB. Por padrão, quando o Microsoft Exchange Server 2013 é instalado, um novo diretório virtual chamado OAB é criado no site da Web interno padrão no IIS (Serviços de Informações da Internet). Se tiver usuários do lado do cliente que se conectam ao Microsoft Outlook de fora do firewall da organização, você poderá adicionar um site da Web externo. Como alternativa, quando você executar o cmdlet **New-OABVirtualDirectory** no Shell, um novo diretório virtual chamado OAB é criado no site da web padrão do IIS no servidor local do Exchange.

A criação de um diretório virtual do OAB não é uma tarefa comum. O Exchange permite um diretório virtual do OAB denominado OAB, e você deverá criar um diretório virtual do OAB apenas se houver um problema com o diretório virtual do OAB e se o diretório virtual do OAB anterior tiver sido removido.

Para tarefas de gerenciamento adicionais relacionadas a OABs, consulte [Procedimentos do catálogo de endereços offline](offline-address-book-procedures-exchange-2013-help.md).


> [!IMPORTANT]
> Antes de criar um diretório virtual do OAB, verifique se os usuários estão cientes das alterações que estão sendo feitas. Esse procedimento pode interromper o processo de download do OAB para seus usuários.



## O que você precisa saber antes de começar?

  - Tempo estimado para concluir cada procedimento: 5 minutos.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Catálogos de endereços offline" no tópico [Endereço de email e permissões do catálogo de endereços](email-address-and-address-book-permissions-exchange-2013-help.md).

  - O servidor Exchange local tem a função de servidor Acesso para Cliente instalada.

  - Deve haver um site da Web padrão do IIS (por exemplo, /w3svc/1/root).

  - Ainda não existe um diretório virtual chamado OAB.

  - Embora a distribuição baseada na Web esteja habilitada por padrão e não exija configuração adicional, recomendamos que você habilite o SSL (Secure Sockets Layer) para o ponto de distribuição do OAB.

  - Você não pode usar o Centro de Administração do Exchange (EAC) para executar esse procedimento. É necessário usar o Shell.

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>.



## Usar o Shell para criar um diretório virtual do OAB

Para criar um diretório virtual do OAB com todas as configurações padrão, você pode executar o cmdlet **New-OABVirtualDirectory** sem nenhum parâmetro. Use o seguinte procedimento para criar um diretório virtual do OAB com configurações personalizadas.


> [!TIP]
> Ao criar um diretório virtual do OAB, recomendamos que habilite o SSL.



Este exemplo cria um diretório virtual do OAB no servidor de Acesso para Cliente denominado CASServer01 com o SSL habilitado e uma URL externa.

    New-OABVirtualDirectory -Server CASServer01 -RequireSSL $true -ExternalURL "https://www.contoso.com/OAB"

Depois de criar um novo diretório virtual do OAB, você deverá editar as configurações em cada OAB que use distribuição baseada na Web para reconectar o diretório virtual do OAB. Para obter mais informações, consulte [Alterar o agendamento de geração do catálogo de endereços offline](change-the-offline-address-book-generation-schedule-exchange-2013-help.md).

Para informações detalhadas de sintaxes e de parâmetros, consulte [New-OabVirtualDirectory](https://technet.microsoft.com/pt-br/library/bb123735\(v=exchg.150\)).

