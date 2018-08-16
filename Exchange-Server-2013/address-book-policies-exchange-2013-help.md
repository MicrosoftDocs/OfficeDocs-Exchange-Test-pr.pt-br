---
title: 'Políticas de catálogo de endereços: Exchange 2013 Help'
TOCTitle: Políticas de catálogo de endereços
ms:assetid: d0a916a1-e3ed-49ae-b116-a559be0dcce6
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Hh529948(v=EXCHG.150)
ms:contentKeyID: 50486683
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Políticas de catálogo de endereços

 

_**Aplica-se a:** Exchange Online, Exchange Server 2013_

_**Tópico modificado em:** 2016-12-09_

Saiba como você pode segmentar sua lista de endereços global em grupos específicos para criar GALs personalizadas no Outlook e Outlook Web App.

Segmentação de GAL (lista) de endereços global (também conhecido como *segregação de GAL*) é o processo no qual os administradores podem segmentar usuários em população específicas para oferecer exibições personalizadas da GAL da sua organização. Políticas de catálogo de endereços (ABPs) permitem aos usuários do segmento em grupos específicos para fornecer exibições personalizadas da lista de endereços global (GAL) da sua organização. Ao criar uma ABP, atribua um ou mais listas de endereços, um catálogo de endereços offline (OAB), uma lista de salas e um GAL à política. Em seguida, você pode atribuir a ABP aos usuários de caixa de correio, fornecendo acesso a um GAL personalizado no Outlook e Outlook Web App. O objetivo é fornecer um mecanismo mais simples para realizar a segmentação de GAL para organizações de local que exigem vários GALs. .


> [!NOTE]
> ABPs destinam-se para otimizar as listas de endereço e a GAL para cada grupo de usuários, não dificultá-los para ver uns aos outros ou para se comunicar com outros usuários em sua organização. ABPs criar somente uma virtual separação de usuários de uma perspectiva de diretório, e não uma separação legais.



**Sumário**

Como funcionam os ABPs

Exemplo ABP

Entourage, o Outlook para Mac e ABPs

## Como funcionam os ABPs

Entourage, Outlook for Mac, and ABPs

  - Uma GAL

  - ABPs contêm as listas a seguir:

  - Uma GAL

  - Um OAB

Na figura a seguir, uma política de catálogo de endereços consiste em um subconjunto de vários objetos de endereço que existe na organização (mostrada na parte inferior metade da figura). O escopo resultante de uma ABP é igual ao que da GAL contidas na política, neste GAL1 case. Quando o ABP é criada e atribuída a um usuário, os objetos de endereço na ABP se tornam o escopo dos objetos de que usuário é capaz de exibir.

![Visão Geral das Políticas de Catálogo de Endereços](images/Hh529948.68084064-7319-431b-be3b-0cce761258b1(EXCHG.150).gif "Visão Geral das Políticas de Catálogo de Endereços")

Na figura a seguir, a Política de Catálogo de Endereço A consiste em um subconjunto de vários objetos de endereços que existem na organização (mostrado na metade inferior da figura). O escopo resultante de uma ABP é igual ao da GAL contido no política, neste caso GAL1. Quando a ABP é criada e atribuída a um usuário, os objetos de endereços na ABP se tornam o escopo dos objetos que o usuário poderá visualizar.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Caixa de correio de nova ou existente?</th>
<th>Você pode usar os métodos a seguir para atribuir ABPs aos usuários de caixas de correio individuais:</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>New</p></td>
<td><p><a href="https://technet.microsoft.com/pt-br/library/aa997663(v=exchg.150)">New-Mailbox</a> cmdlet com o parâmetro <em>AddressBookPolicy</em></p></td>
</tr>
<tr class="even">
<td><p>Existentes</p></td>
<td><p><a href="https://technet.microsoft.com/pt-br/library/bb123981(v=exchg.150)">Set-Mailbox</a> cmdlet com o parâmetro <em>AddressBookPolicy</em></p>
<p></p></td>
</tr>
</tbody>
</table>


ABPs entrarão em vigor quando o aplicativo de cliente de um usuário se conecta a um servidor de acesso para cliente no Exchange 2013. Se você alterar o ABP, o ABP atualizado não terá efeito até que o usuário reiniciar ou reconecta seus clientes ou até que você reinicie os servidores de acesso para cliente RPC no servidor de caixa de correio Exchange 2013.

## Agente roteamento de diretiva de catálogo de endereços

Em uma organização do Exchange que não usa ABPs, ocorrerá o seguinte quando um email é criado no Outlook ou Outlook Web App e enviado ao destinatário outro em sua organização do Exchange:

1.  O endereço de email é resolvido. Por exemplo, se você digitar **kweku@contoso.com** no campo **para**, o endereço de email SMTP resolveria ao nome de exibição do usuário **Kweku Ako-Adjei**.

2.  É possível exibir o cartão de visita da outra pessoa. Depois que o nome for resolvido, você pode clique duas vezes no nome do usuário e exibir suas informações de contato, como número de telefone e do escritório.

Se você estiver usando a ABPs, e você não quiser que os usuários em organizações virtuais distintas para exibir informações particulares potencialmente uns dos outros, você pode ativar o agente Address Book Policy Routing. O agente roteamento ABP é um agente de transporte que controla como os destinatários são resolvidos em sua organização. Quando o agente roteamento ABP está instalado e configurado, os usuários que estão atribuídos ao GALs diferentes aparecem como destinatários externos que não podem ver os cartões de visita de destinatários externos.

Para obter detalhes sobre como ativar o agente roteamento ABP em Exchange Online, consulte [Ativar a política de catálogo de endereços roteamento](https://technet.microsoft.com/pt-br/library/jj891095\(v=exchg.150\)).

Para obter detalhes sobre como ativar o agente roteamento ABP no Exchange Server, consulte [Instalar e configurar o agente de roteamento de política de catálogo de endereços](install-and-configure-the-address-book-policy-routing-agent-exchange-2013-help.md).

## Exemplo ABP

No diagrama a seguir, Fabrikam e Tailspin Toys compartilham a mesma organização do Exchange e o mesmo CEO. CEO é a única funcionária comuns para ambas as empresas.

![Duas Empresas, um CEO](images/JJ657455.c87a5654-d456-4688-acb2-0be15ba1cda6(EXCHG.150).gif "Duas Empresas, um CEO")

Essa configuração contém três ABPs:

  - Um contém os funcionários da Fabrikam e CEO

  - Um contém funcionários Tailspin Toys e CEO

  - Um contém apenas CEO

As ABPs cumpram as regras a seguir:

  - Os usuários no Tailspin Toys só podem ver os funcionários de Tailspin Toys e CEO que acessam a GAL.

  - Os usuários na Fabrikam só podem ver os funcionários da Fabrikam e CEO quando eles pesquisam GAL.

  - CEO pode ver todos os Fabrikam e Tailspin Toys funcionários quando navegando GAL.

  - Os usuários exibir a associação de grupo do CEO podem ver apenas os grupos que pertencem a empresa do usuário. Eles não verão os grupos que existem na outra empresa.

## Entourage, o Outlook para Mac e ABPs

ABPs não funcionam para usuários do Entourage ou do Outlook para usuários de Mac que estiverem conectados à sua rede corporativa. Quando estiver dentro da rede corporativa, Entourage e o Outlook para clientes Mac conectarem diretamente ao servidor de catálogo global e consultar o Active Directory diretamente, em vez de usar o servidor de acesso para cliente. No entanto, o Outlook para Mac 2011 clientes que se conectam da Internet pode usar um OAB ou serviços Web do Exchange (EWS). Como resultado, esses clientes podem pesquisar a GAL com base no ABP. atribuído Para saber mais sobre como administrar o Outlook para Mac 2011, consulte [planejamento do Outlook para Mac 2011](https://go.microsoft.com/fwlink/p/?linkid=231878)

## Para saber mais

[Cenário: Implantando políticas de catálogo de endereços](scenario-deploying-address-book-policies-exchange-2013-help.md)

[\[Online\] procedimentos de política de catálogo de endereços](https://technet.microsoft.com/pt-br/library/jj891096\(v=exchg.150\)) no Exchange Online

