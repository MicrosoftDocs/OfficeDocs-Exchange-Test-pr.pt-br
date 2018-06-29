---
title: 'Identidade da mensagem DSN: Exchange 2013 Help'
TOCTitle: Identidade da mensagem DSN
ms:assetid: 70ffba22-e4fd-4cd3-98f5-8bfca2df89e4
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Aa998835(v=EXCHG.150)
ms:contentKeyID: 50485911
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Identidade da mensagem DSN

 

_**Aplica-se a:**Exchange Server 2013_

_**Tópico modificado em:**2015-03-09_

Você pode identificar uma mensagem de notificação (DSN) de status de entrega personalizada com base em sua sintaxe. A identidade é a GUID da mensagem DSN personalizada ou uma cadeia de caracteres que consiste dos seguintes valores:

  - **Localidade**   Essa variável Especifica a localidade do idioma que será exibida a mensagem DSN em. Para obter uma lista dos códigos de localidade que você pode usar com o comando **New-SystemMessage** , consulte [Idiomas com suporte para mensagens do sistema](supported-languages-for-system-messages-exchange-2013-help.md).

  - **Interno ou externo**   Essa variável Especifica se a mensagem DSN é enviada apenas aos remetentes que são parte da Microsoft Exchange Server 2013 organização interna ou também aos remetentes fora da organização do Exchange. Você pode usar a opção Internal quando você deseja incluir um contato de email específicos ou a resolução nas mensagens DSN enviadas para remetentes internos, mas não deseja expor essas informações aos remetentes fora da sua organização.

  - **Código DSN**   Essa variável Especifica o código DSN da mensagem DSN personalizada.

A sintaxe da identidade de mensagem DSN é `<Locale>\<Internal or External>\<DSN code>`.

Para cada código DSN, você pode criar mais de uma mensagem DSN personalizada, que pode direcionar remetentes internos ou remetentes externos e localidades diferentes. Por exemplo, a tabela a seguir mostra algumas das configurações possíveis para o código DSN 5.1.2 e as identidades de mensagem DSN correspondentes.

### Identidades e exemplos de configurações de DSN

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Configuração de DSN</th>
<th>Identidade DSN</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Exibir mensagens DSN para remetentes internos com uma localidade em inglês (em inglês)</p></td>
<td><p>En\Internal\5.1.2</p></td>
</tr>
<tr class="even">
<td><p>Exibir mensagens DSN para remetentes externos com uma localidade em inglês (em inglês)</p></td>
<td><p>En\External\5.1.2</p></td>
</tr>
<tr class="odd">
<td><p>Exibir mensagens DSN para remetentes internos com uma localidade em japonês (ja)</p></td>
<td><p>Ja\Internal\5.1.2</p></td>
</tr>
<tr class="even">
<td><p>Exibir mensagens DSN para remetentes externos com uma localidade em japonês (ja)</p></td>
<td><p>Ja\External\5.1.2</p></td>
</tr>
</tbody>
</table>

