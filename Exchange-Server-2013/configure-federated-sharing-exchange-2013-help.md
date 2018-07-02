---
title: 'Configurar o compartilhamento federado: Exchange 2013 Help'
TOCTitle: Configurar o compartilhamento federado
ms:assetid: b25ae450-def3-4797-a5fc-6e9bcee71a5d
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/JJ657483(v=EXCHG.150)
ms:contentKeyID: 50486432
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configurar o compartilhamento federado

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2015-04-07_

Com o compartilhamento federado no Exchange Server 2013, os usuários podem compartilhar informações com destinatários em organizações externas federadas. Isso inclui o compartilhamento de informações sobre sua disponibilidade (também conhecida como disponibilidade de calendário) para fins de agendamento ou, dependendo da natureza da relação comercial, compartilhamento de informações de calendário mais detalhadas. Para saber mais sobre compartilhamento federado, consulte [Compartilhamento](sharing-exchange-2013-help.md).


> [!IMPORTANT]
> Esse recurso do Exchange Server 2013 não é totalmente compatível com o Office 365 operado pelo 21Vianet na China e pode haver algumas limitações de recurso. Para saber mais, confira o artigo <A href="https://go.microsoft.com/fwlink/?linkid=313640">Saiba mais sobre o Office 365 operado pelo 21Vianet</A>.



## O que você precisa saber antes de começar?

  - Tempo estimado para a conclusão da tarefa: 1 hora.

  - Os procedimentos neste tópico exigem permissões específicas. Consulte cada procedimento para ver informações sobre permissões.

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>.



## Como fazer isso?

## Etapa 1: Criar e configurar uma confiança de federação

Uma relação de confiança de Federação estabelece uma relação de confiança entre uma organização Exchange 2013 e o sistema de autenticação Azure Active Directory e é um requisito para o compartilhamento federado.

Para obter instruções detalhadas, consulte [Configurar uma confiança de Federação](configure-a-federation-trust-exchange-2013-help.md).

## Etapa 2: Criar um relacionamento de organização

Um relacionamento de organização permite que os usuários em sua organização do Exchange compartilhar informações de disponibilidade de calendário como parte do compartilhamento federado com outras organizações federadas do Exchange. Compartilhamento federado pode ser configurado entre duas organizações federadas Exchange 2013 ou entre uma organização federada Exchange 2013 e organizações federadas Exchange 2010.

Para obter instruções detalhadas, consulte [Criar um relacionamento de organização](create-an-organization-relationship-exchange-2013-help.md).

## Etapa 3: Criar uma política de compartilhamento

As políticas de compartilhamento habilitam o compartilhamento de informações de calendário estabelecido pelo usuário, de pessoa para pessoa, com diferentes tipos de usuários externos. Essas políticas suportam o compartilhamento de informações de calendário e de contato com organizações externas federadas, organizações externas não federadas e indivíduos com acesso à Internet. Caso não seja necessário configurar o compartilhamento entre pessoas ou de contatos (compartilhamento em nível organizacional apenas), não configure nenhuma política de compartilhamento.

Para obter instruções detalhadas, consulte [Criar uma política de compartilhamento](create-a-sharing-policy-exchange-2013-help.md).

## Etapa 4: Configurar um registro de descoberta automática DNS público

É preciso adicionar um registro de recurso de nome canônico (CNAME) de alias ao seu DNS voltado para público. O novo registro de CNAME deverá apontar para um servidor de Acesso para Cliente Exchange 2013 voltado para a Internet que esteja executando o serviço de Descoberta Automática.

Para obter instruções detalhadas sobre como adicionar registros de CNAME, consulte o serviço de hospedagem dos seus registros DNS públicos. Normalmente, este é um serviço baseado na Internet que também poderá hospedar sites de domínio.

