---
title: 'Implantar o Exchange 2013 em uma topologia de floresta de recursos do Exchange'
TOCTitle: Implantar o Exchange 2013 em uma topologia de floresta de recursos do Exchange
ms:assetid: 537a7b2b-d002-40a6-84ae-fd02635f9e23
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Aa998031(v=EXCHG.150)
ms:contentKeyID: 51407857
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Implantar o Exchange 2013 em uma topologia de floresta de recursos do Exchange

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2016-12-09_

Este tópico explica como implantar o Microsoft Exchange 2013 em uma topologia de floresta de recurso Exchange. Uma floresta de recursos Exchange também é chamada de uma floresta dedicado Exchange. Este tópico pressupõe que você não possui uma topologia existente do Exchange 2013.

A figura a seguir mostra uma organização do Exchange com uma floresta de recursos.

**Exemplo de uma organização do Exchange com uma floresta de recursos do Exchange**

![Organização complexa do Exchange com floresta de recursos](images/Aa998031.706725cf-e520-4b89-a275-acd8fb58943a(EXCHG.150).gif "Organização complexa do Exchange com floresta de recursos")

## O que você precisa saber antes de começar?

Para executar o procedimento a seguir Exchange 2013, confirme que você tem o seguinte:

  - Você tem estas duas florestas do Active Directory:
    
      - Uma floresta contém as contas de usuário da organização. Neste procedimento, essa floresta será chamada de *floresta de contas*.
    
      - Uma floresta não contém as contas de usuário e ainda não tem Exchange instalado. Neste procedimento, floresta é chamada de *floresta do Exchange*. Você usará o procedimento para instalar o Exchange 2013 da floresta.

  - Você tiver configurado corretamente sistema de nome de domínio (DNS) para resolução de nomes entre florestas em sua organização. Para verificar se você possui o DNS configurado corretamente, execute ping cada floresta a partir da floresta ou florestas em sua organização. Para obter mais informações sobre como configurar o DNS, consulte o [Guia de operações de servidores DNS](https://go.microsoft.com/fwlink/p/?linkid=282295).

## Implantar o Exchange 2013 em uma topologia de floresta de recursos do Exchange

1.  A partir de um controlador de domínio na floresta Exchange, crie uma relação de confiança unidirecional de saída para a floresta Exchange relações de confiança da floresta de contas. Para obter etapas detalhadas, consulte [criar uma relação de confiança de floresta unidirecional de saída, para ambos os lados da relação de confiança](https://go.microsoft.com/fwlink/p/?linkid=69130).
    

    > [!NOTE]
    > Embora seja recomendável criar uma confiança de floresta, você pode criar uma confiança de floresta ou uma confiança externa. Se você criar uma confiança externa, quando criar caixas de correio vinculadas na Etapa 3, na página <STRONG>Conta Principal</STRONG> do assistente de Nova Caixa de Correio, especifique uma conta de usuário que possa acessar o controlador de domínio na floresta confiável. Você não pode usar as credenciais com as quais está conectado atualmente. Se você criar caixas de correio vinculadas usando o cmdlet <STRONG>New-Mailbox</STRONG>, deverá especificar uma conta de usuário que possa acessar o controlador de domínio na floresta confiável usando o parâmetro <EM>LinkedCredential</EM>.



2.  Na floresta Exchange, instale o Exchange 2013. Instale o Exchange da mesma forma que faria em um cenário de floresta única. Para obter instruções detalhadas sobre como instalar o Exchange 2013, consulte um dos seguintes tópicos:
    
      - [Implantar uma nova instalação do Exchange 2013](deploy-a-new-installation-of-exchange-2013-exchange-2013-help.md)
    
      - [Instalar o Exchange 2013 usando o Assistente para Configuração](install-exchange-2013-using-the-setup-wizard-exchange-2013-help.md)

3.  Na floresta Exchange, para cada usuário na floresta de contas que terão uma caixa de correio na floresta Exchange, crie uma caixa de correio que está associada uma conta externa. Para obter etapas detalhadas, consulte [Gerenciar caixas de correio vinculadas](manage-linked-mailboxes-exchange-2013-help.md).

