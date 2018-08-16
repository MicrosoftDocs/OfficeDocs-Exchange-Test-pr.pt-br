---
title: 'Gerenciar dicas de email de relacionamentos da organização: Exchange 2013 Help'
TOCTitle: Gerenciar dicas de email para relacionamentos da organização
ms:assetid: 6e6b48ef-c41c-47ad-8063-66901765c2a5
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/JJ649324(v=EXCHG.150)
ms:contentKeyID: 50485788
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Gerenciar dicas de email para relacionamentos da organização

 

_**Aplica-se a:** Exchange Online, Exchange Server 2013_

_**Tópico modificado em:** 2015-04-08_

Você pode usar o Shell de Gerenciamento do Exchange para definir configurações personalizadas para Dicas de Email entre várias organizações.

Ao estabelecer uma relação organizacional, você pode aprimorar a experiência do usuário de ambas as organizações, compartilhando dados de disponibilidade, configurando o fluxo seguro de mensagens e habilitando o acompanhamento de mensagens. Para informações adicionais sobre as relações organizacionais, consulte [Dicas de email sobre relacionamentos da organização](mailtips-over-organization-relationships-exchange-2013-help.md).

Você pode usar várias configurações para controlar como as Dicas de Email são utilizadas entre duas organizações que estabeleceram uma relação organizacional. Os procedimentos nesta seção ilustram essa variedade de controles. Em todos os exemplos, a organização local é a contoso.com, a organização remota é a online.contoso.com e a relação organizacional foi nomeada como Contoso Online.

Use o cmdlet **Set-OrganizationRelationship** para definir essas configurações.

## O que você precisa saber antes de começar?

  - Tempo estimado para concluir cada procedimento: 5 minutos

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Dicas de Email" no tópico [Permissões de fluxo de email](mail-flow-permissions-exchange-2013-help.md).

  - Você só pode usar o Shell para executar esse procedimento.

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>.



## O que você deseja fazer?

## Usar o Shell para habilitar ou desabilitar as Dicas de Email entre duas organizações

Este exemplo configura a relação organizacional de forma que as Dicas de Email retornem aos remetentes na organização remota ao compor mensagens para os destinatários em sua organização.

    Set-OrganizationRelationship "Contoso Online" -MailTipsAccessEnabled $true

Este exemplo configura a relação organizacional a fim de evitar que as Dicas de Email retornem aos remetentes na organização remota ao compor mensagens para os destinatários em sua organização.

    Set-OrganizationRelationship "Contoso Online" -MailTipsAccessEnabled $false

Para informações detalhadas de sintaxes e de parâmetros, consulte [Set-OrganizationRelationship](https://technet.microsoft.com/pt-br/library/ee332326\(v=exchg.150\)).

## Usar o Shell para configurar quais Dicas de Email retornam à organização remota

Para cada relação organizacional, é possível determinar qual conjunto de Dicas de Email retorna aos remetentes na outra organização. Este exemplo configura a relação organizacional de forma que todas as Dicas de Email retornem.

    Set-OrganizationRelationship "Contoso Online" -MailTipsAccessLevel All

Este exemplo configura a relação organizacional de forma que retornem apenas as Dicas de Email de Respostas Automáticas, Mensagem com Tamanho Excessivo, Destinatário Restrito e Caixa de Correio cheia.

    Set-OrganizationRelationship "Contoso Online" -MailTipsAccessLevel Limited

Este exemplo configura a relação organizacional de forma que nenhuma Dica de Email retorne.


> [!TIP]
> Não use este método para desabilitar as Dicas de Email para esta relação. Para desabilitar as Dicas de Email, defina o parâmetro <EM>MailTipsAccessEnabled</EM> como <CODE>$false</CODE>.



    Set-OrganizationRelationship "Contoso Online" -MailTipsAccessLevel None

Para informações detalhadas de sintaxes e de parâmetros, consulte [Set-OrganizationRelationship](https://technet.microsoft.com/pt-br/library/ee332326\(v=exchg.150\)).

## Usar o Shell para configurar um grupo específico de usuários para o qual são retornadas Dicas de Email específicas de destinatários.

Você pode restringir o retorno de Dicas de Email específicas de destinatários para um determinado grupo de usuários. Como padrão, ao habilitar as Dicas de Email para uma relação organizacional, as seguintes Dicas de Email específicas de destinatários retornam para todos os usuários:

  - Respostas Automáticas

  - Caixa de Correio Cheia

  - Dica de Email personalizada

Você pode especificar um grupo de acesso a Dicas de Email na relação organizacional. Depois de especificar um grupo, as Dicas de Email específicas de destinatários retornam apenas para as caixas de correio, contatos de email e usuários de email que são membros daquele grupo. Este exemplo configura a relação organizacional para retornar Dicas de Email específicas de destinatários apenas para membros do grupo ShareMailTips@contoso.com.

    Set-OrganizationRelationship "Contoso Online" -MailTipsAccessScope ShareMailTips@contoso.com

Para informações detalhadas de sintaxes e de parâmetros, consulte [Set-OrganizationRelationship](https://technet.microsoft.com/pt-br/library/ee332326\(v=exchg.150\)).

