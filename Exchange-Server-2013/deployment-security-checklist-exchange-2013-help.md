---
title: 'Lista de verificação de segurança de implantação: Exchange 2013 Help'
TOCTitle: Lista de verificação de segurança de implantação
ms:assetid: 0cbfad59-f503-48a0-8184-6ca999d89e61
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Aa996026(v=EXCHG.150)
ms:contentKeyID: 50484996
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Lista de verificação de segurança de implantação

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2016-12-09_

Os recursos do Microsoft Exchange Server 2013 foram projetados para ajudar a melhorar a segurança de seu ambiente de sistema de mensagens. Geralmente, para o Exchange 2013, as seguintes condições são verdadeiras:

  - As contas que são usadas pelo Exchange 2013 possuem os direitos mínimos necessários para executar os conjuntos de tarefas determinados.

  - Por padrão, os serviços são iniciados apenas quando solicitados.

  - Os direitos da ACL (lista de controle de acesso) dos objetos do Exchange estão minimizados.

  - As permissões administrativas são definidas de acordo com o escopo da alteração no objeto que uma determinada modificação exige.

  - Por padrão, todos os caminhos de mensagem padrão internos são criptografados.

Este tópico descreve etapas recomendadas que você pode adotar para aumentar a segurança de seu ambiente de sistema de mensagens antes de instalar o Microsoft Exchange. Recomendamos que você consulte essa lista de verificação sempre que instalar uma nova função de servidor do Exchange.

Antes de instalar o Exchange 2013, execute os procedimentos a seguir.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Procedimento</th>
<th>Pronto?</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Execute o <a href="https://go.microsoft.com/fwlink/p/?linkid=54836">Microsoft Update</a>.</p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Executar a Ferramenta de Remoção de Software Mal-Intencionado do Microsoft Windows. A ferramenta Malicious Software Removal Tool está incluída na Atualização do Microsoft. Mais informações sobre a ferramenta podem ser encontradas em <a href="http://go.microsoft.com/fwlink/p/?linkid=73452">Ferramenta de Remoção de Software Mal-intencionado</a>.</p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Execute o <a href="https://go.microsoft.com/fwlink/p/?linkid=16526">Microsoft Baseline Security Analyzer</a>.</p></td>
<td><p></p></td>
</tr>
</tbody>
</table>

