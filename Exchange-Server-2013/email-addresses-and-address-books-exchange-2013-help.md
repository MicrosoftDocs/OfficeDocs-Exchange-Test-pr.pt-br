---
title: 'Endereços de email e catálogos de endereços: Exchange 2013 Help'
TOCTitle: Endereços de email e catálogos de endereços
ms:assetid: b97d0f68-691a-42af-9a6c-4dcc37b28a42
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/JJ657488(v=EXCHG.150)
ms:contentKeyID: 50486487
ms.date: 01/10/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Endereços de email e catálogos de endereços

 

_**Aplica-se a:**Exchange Server 2013_

_**Tópico modificado em:**2015-03-09_

Destinatários (que incluem usuários, recursos, contatos e grupos) são qualquer objeto habilitado para email no Active Directory para o qual o Microsoft Exchange pode entregar ou rotear mensagens. Para que um destinatário envie ou receba mensagens de email, ele deve ter um endereço de email. Catálogos de endereços são o método pelo qual os usuários podem se localizar e enviar emails uns aos outros. Existem inúmeros métodos diferentes para organizar catálogos de endereços. Consulte Terminologia principal para obter descrições detalhadas dos recursos de catálogo de endereços no Exchange Server 2013.

## Terminologia principal

Os termos a seguir definem os principais componentes associados a endereços de email e catálogos de endereços no Exchange 2013.

  - **políticas de catálogo de endereços**  
    Políticas de catálogo de endereços (ABPs) permitem segmentar usuários em grupos específicos para fornecer visualizações personalizadas da GAL (lista de endereços global) da sua organização. Ao criar uma ABP, atribua uma GAL, um OAB (catálogo de endereços offline), uma lista de salas e uma ou mais listas de endereços para a política. Você pode então atribuir a ABP para usuários de caixa de correio, fornecendo acesso a uma GAL personalizada no Outlook e Outlook Web App. O objetivo é fornecer um mecanismo mais simples para realizar segmentação GAL para as organizações locais que exigem várias GALs.

<!-- end list -->

  - **listas de endereços**  
    Listas de endereços são um subconjunto de uma GAL. Cada lista de endereços corresponde a uma coleção de um ou mais tipos de destinatários habilitados para email (por exemplo, usuários, contatos, grupos, pastas públicas, conferências e outros recursos). Você pode usar listas de endereços para organizar destinatários e recursos, facilitando para os usuários a localização dos destinatários e recursos necessários. Listas de endereços são atualizadas dinamicamente. Portanto, quando novos destinatários são adicionados à sua organização, eles são automaticamente incluídos nas listas de endereços adequadas.

<!-- end list -->

  - **políticas de endereço de email**  
    Políticas de endereços de email geram os endereços de email primário e secundário dos seus destinatários, para que eles possam receber e enviar emails. Por padrão, o Exchange contém uma política de endereço de email para cada usuário habilitado para email.

<!-- end list -->

  - **catálogos de endereços hierárquicos**  
    O HAB (catálogo de endereços hierárquico) permite que os usuários procurarem destinatários em suas organizações do Exchange utilizando uma hierarquia organizacional, como tempo de serviço ou estrutura de gestão. Normalmente, usuários são limitados para a GAL padrão e suas propriedades de destinatários associados e a estrutura da GAL frequentemente não refletem precisamente as relações de gestão e tempo de serviço para destinatários na sua organização. A capacidade de personalizar um HAB que mapeia a estrutura corporativa exclusiva de sua organização propicia aos usuários um método eficiente para localizar destinatários internos.

<!-- end list -->

  - **catálogos de endereços offline**  
    Um OAB (catálogo de endereços offline) é uma cópia de uma coleção de listas de endereços obtidas por download, para que um usuário do Microsoft Outlook possa acessar as informações nele contidas enquanto estiver desconectado do servidor.

## Documentação de endereços de email e catálogos de endereços

A tabela a seguir contém links para tópicos que o ajudarão a conhecer e gerenciar endereços de email e catálogos de endereços no Exchange 2013.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Tópico</th>
<th>Descrição</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="address-lists-exchange-2013-help.md">Listas de endereços</a></p></td>
<td><p>Saiba mais sobre o uso de listas de endereços e GALs como métodos de organizar seus destinatários para facilitar o acesso do usuário final.</p></td>
</tr>
<tr class="even">
<td><p><a href="address-book-policies-exchange-2013-help.md">Políticas de catálogo de endereços</a></p></td>
<td><p>Saiba mais sobre como dividir suas listas de endereços e GALs em organizações virtuais distintas.</p></td>
</tr>
<tr class="odd">
<td><p><a href="details-templates-exchange-2013-help.md">Modelos de detalhes</a></p></td>
<td><p>Saiba mais sobre como personalizar cartões de endereço no Outlook.</p></td>
</tr>
<tr class="even">
<td><p><a href="email-address-policies-exchange-2013-help.md">Políticas de endereço de email</a></p></td>
<td><p>Saiba mais sobre endereços de email de proxy para tornar os destinatários mais detectáveis.</p></td>
</tr>
<tr class="odd">
<td><p><a href="hierarchical-address-books-exchange-2013-help.md">Catálogos de endereços hierárquicos</a></p></td>
<td><p>Saiba mais sobre como personalizar a GAL e as listas de endereços para ajustar-se à estrutura de negócios exclusiva da sua organização.</p></td>
</tr>
<tr class="even">
<td><p><a href="offline-address-books-exchange-2013-help.md">Catálogos de endereços offline</a></p></td>
<td><p>Saiba mais sobre como disponibilizar para os usuários acesso offline às listas de endereços da sua organização.</p></td>
</tr>
</tbody>
</table>

