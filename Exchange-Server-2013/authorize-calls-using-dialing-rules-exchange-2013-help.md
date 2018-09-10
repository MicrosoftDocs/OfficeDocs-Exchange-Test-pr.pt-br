---
title: 'Autorizar chamadas usando regras de discagem: Exchange 2013 Help'
TOCTitle: Autorizar chamadas usando regras de discagem
ms:assetid: 4c18bc07-f55c-42b7-81c1-729878aa93aa
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/JJ898499(v=EXCHG.150)
ms:contentKeyID: 51407875
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Autorizar chamadas usando regras de discagem

 

_**Aplica-se a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Tópico modificado em:** 2015-03-09_

Por padrão, os usuários não são capazes de fazer chamadas de saída. Para especificar que os tipos de chamadas os usuários podem fazer, primeiro crie regras de discagem, e autorize os grupos destas regras de discagem nos planos de discagem, nas políticas de caixa de correio ou nos atendedores automáticos de UM. Para poder autorizar grupos de regras de discagem, é preciso definir as regras de discagem em um plano de discagem de UM. Para obter detalhes, consulte [Criar regras de discagem para usuários](create-dialing-rules-for-users-exchange-2013-help.md).

Cada regra de discagem que você criar irá conter os tipos de chamadas ou padrões de números aos quais você deseja fornecer acesso aos usuários. Você pode permitir que diferentes tipos de usuários façam diferentes tipos de chamadas. As chamadas que você permitir podem ser dentro de um país ou região, ou podem ser internacionais.

Para autorizar ou restringir a discagem, as configurações a seguir devem ser configuradas corretamente:

  - **Regras de discagem**   As regras de discagem definem o número que é discado pelo usuário habilitado para UM e o número que será discado pela PBX (central privada de comutação) ou PBX IP. Você pode criar um grupo de regras de discagem adicionando uma regra de discagem. Depois de criar um grupo de regras de discagem, você pode adicioná-lo à lista de chamadas autorizadas para um grupo de regras de discagem de país/região ou internacionais.

  - **Grupos de regras de discagem**   O grupos de regras de discagem determinam os tipos de chamadas que os usuários podem fazer dentro de um grupo de discagem.

  - **Autorizações de discagem**   As autorizações de discagem são usadas para determinar as restrições que serão aplicadas para impedir que os usuários tenham despesas telefônicas desnecessárias ou que façam chamadas de longa distância.

## Como autorizar um grupo de regras de discagem?

O local onde você autoriza os grupos de regras de discagem depende dos tipos de chamadores que você deseja permitir para fazer chamadas. Por exemplo, se você deseja que apenas usuários do Outlook Voice Access façam chamadas, crie suas regras de discagem e autorize os grupos de regras de discagem para a política de caixa de correio de UM a qual os usuários do Outlook Voice Access estão vinculados. A tabela a seguir mostra como autorizar chamadas para diferentes tipos de chamadores.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Tipo de chamador</th>
<th>Autorizar grupos de regras de discagem aqui</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Chamadores não autenticados que ligam para um número do Outlook Voice Access e não inserem um PIN</p></td>
<td><p>Plano de discagem de UM. Para obter detalhes, consulte <a href="https://docs.microsoft.com/pt-br/exchange/voice-mail-unified-messaging/set-up-client-voice-mail-features/authorize-calls-for-users-in-a-dial-plan">Autorizar chamadas para usuários em um plano de discagem</a>.</p></td>
</tr>
<tr class="even">
<td><p>Chamadores autenticados que ligam para um número do Outlook Voice Access e inserem um PIN</p></td>
<td><p>Política de caixa de correio de UM para o chamador. Para obter detalhes, consulte <a href="authorize-calls-for-a-group-of-users-exchange-2013-help.md">Autorizar chamadas para um grupo de usuários</a>.</p></td>
</tr>
<tr class="odd">
<td><p>Chamadores não autenticados que ligam para um número de telefone configurado em um atendedor automático de UM</p></td>
<td><p>Atendedor automático de UM. Para obter detalhes, consulte <a href="authorize-calls-for-auto-attendant-callers-exchange-2013-help.md">Autorizar chamadas para os chamadores de atendedor automático</a>.</p></td>
</tr>
</tbody>
</table>


Dependendo de quais usuários está autorizando a fazer chamadas, você usará a página **Autorização de discagem** no Centro de Administração do Exchange (EAC) para o plano de discagem, o atendedor automático ou a política de caixa de correio de UM.

