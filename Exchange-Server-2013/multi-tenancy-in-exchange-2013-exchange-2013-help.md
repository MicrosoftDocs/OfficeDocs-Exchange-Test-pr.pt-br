---
title: 'A multilocação no Exchange 2013: Exchange 2013 Help'
TOCTitle: A multilocação no Exchange 2013
ms:assetid: df09257d-dd98-4f59-b830-1818cedda15c
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/JJ862352(v=EXCHG.150)
ms:contentKeyID: 50556298
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# A multilocação no Exchange 2013

 

_**Aplica-se a:** Exchange Online, Exchange Server, Exchange Server 2013_

_**Tópico modificado em:** 2016-12-09_

Uma implantação de multilocatário (hospedado) Exchange 2013 é definida como where de uma organização do Exchange está configurada para hospedar vários e organizações distintas ou unidades de negócios (os locatários) que normalmente não compartilham email, dados, usuários, listas de endereços global (GALs) ou outro comumente usados objetos do Exchange. Esse compartilhamento de hardware, software e recursos (all, mantendo uma separação lógica entre locatários), permite que as organizações a aproveitar a simplicidade de uma implantação do Exchange standard fornecendo funcionalidade de multilocatário e serviços para atender suas necessidades de hospedagem.

## A multilocação em organizações do Exchange 2013

No Exchange 2013, podemos continue dão suporte à hospedagem usando um standard, a instalação do Exchange local semelhante à abordagem usada em Exchange 2010 Service Pack 2 (SP2). Podemos descontinuados a opção de modo `/hosting` e são enfatiza o uso de políticas de catálogo de endereços (ABPs) em combinação com a hospedagem de soluções de gerenciamento e ferramentas de automação fornecidas pelo aprovados fornecedores independentes de Software (ISVs). Essas soluções são criadas em uma estrutura de práticas e diretrizes de configuração de aprovados pela Microsoft e deve oferecer uma maneira mais fácil e mais robusta para fornecer serviços de hospedagem e recursos de organizações do Exchange.

Exchange 2013 oferece suporte a multilocação, utilizando os recursos e os seguintes componentes principais:

  - **Do Active Directory**   Em vez de informarem contêineres do Active Directory separada *ExchangeOrganization* para cada unidade de negócios em uma organização do Exchange de multilocatário, Exchange 2013 multilocação é suportada por meio de um contêiner do Active Directory único *ExchangeOrganization* . Isso permite uma estrutura mais simples do Active Directory e reduz a probabilidade de problemas de permissão relacionadas ao Active Directory.
    
    Para saber mais sobre alterações do Active Directory no Exchange 2013, consulte [Active Directory](active-directory-exchange-2013-help.md).

  - **Políticas de catálogo de endereços (ABPs)**   Introduzidos em Exchange 2010 SP2, ABPs são usados em Exchange 2013 para controlar o acesso de usuário a uma lista de endereços, o endereço global (GAL) de lista e um endereço offline (OABs) manuais online na organização do Exchange. ABPs agrupar esses objetos do Active Directory diferentes em um único objeto virtual que pode ser atribuído a usuários individuais e para criar um agrupamento lógico desses recursos ao longo de uma estrutura organizacional de multilocatário. Funcionalidade ABP em Exchange 2013 é semelhante à qual ele foi Exchange 2010 SP2.
    
    Para saber mais sobre ABPs em Exchange 2013, consulte [Políticas de catálogo de endereços](address-book-policies-exchange-2013-help.md).

  - **Gerenciamento de soluções de hospedagem**   Alguns administradores usando Exchange 2013 para fornecer uma solução hospedada do Exchange beneficiarão usando uma abordagem de gerenciamento de hospedagem personalizada. Devido a algumas limitações do Centro de administração do Exchange (EAC), a Microsoft trabalha com fornecedores de terceiros para ajudá-los no desenvolvimento de soluções de automação e painel de controle que estão em conformidade com as diretrizes e framework aprovado para organizações hospedada Exchange 2013. É recomendável que as organizações Configurando uma solução hospedada do Exchange aproveitar essas ferramentas para gerenciar suas organizações hospedadas onde circunstâncias exigirem.
    
    Para saber mais sobre o gerenciamento hospedado soluções, incluindo fornecedores de solução validada, consulte [hospedagem do Exchange Server 2013 e soluções de multilocação e orientação](https://go.microsoft.com/fwlink/?linkid=275036)

