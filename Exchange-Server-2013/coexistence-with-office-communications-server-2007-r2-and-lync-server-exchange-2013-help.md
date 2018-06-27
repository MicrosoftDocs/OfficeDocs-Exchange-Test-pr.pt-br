---
title: 'Coexistência com o Office Communications Server 2007 R2 e o Lync Server: Exchange 2013 Help'
TOCTitle: Coexistência com o Office Communications Server 2007 R2 e o Lync Server
ms:assetid: f12d65c7-0b2c-46a1-a14a-802a76296fa1
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/JJ851069(v=EXCHG.150)
ms:contentKeyID: 50556309
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Coexistência com o Office Communications Server 2007 R2 e o Lync Server

 

_**Aplica-se a:**Exchange Server 2013, Exchange Server 2016_

_**Tópico modificado em:**2015-03-09_

Communications Server 2007 R2 e o Lync Server oferecem vários recursos do usuário final, incluindo mensagens instantâneas (IM), presença, mensagens Instantâneas com vários participantes e sua funcionalidade de caixa postal podem ser integrados com Exchange Unified Messaging (UM). Para implantações que integram o Lync Server 2010 ou 2013, os usuários podem ser habilitados para o Enterprise Voice, que permite que os usuários habilitados para o acesso de email de voz própria voz de email usando os componentes do Lync Server.

Ao integrar a Unificação de mensagens com as versões anteriores do Office Communications Server ou o Lync Server, nem todos os recursos estão disponíveis. Para os usuários se beneficiam dos novos recursos do usuário final avançada como fotos de alta resolução, o armazenamento unificado de contatos e integração de arquivamento do Lync, eles devem ter contas de usuário no Lync Server 2013 e Exchange Server 2013 e devem estar usando a versão mais recente do software de cliente do Lync 2013. Por exemplo, o armazenamento unificado de contatos não está disponível para usuários que tenham sido habilitados para o Enterprise Voice no Lync Server 2010. Além disso, fotos de alta resolução não podem ser exibidas no Lync 2010.

Quando você estiver integrando UM do Exchange com o Office Communications Server 2007 R2 ou o Lync Server 2010, talvez seja necessário instalar os hotfixes adicionais, resumos, atualizações cumulativas e service packs nos servidores do Office Communications Server 2007 R2 ou o Lync 2010 que foram implantados em sua organização. O que você está necessários para instalar dependerá de sua topologia de implantação e as versões de produto que você estiver integrando com o UM do Exchange.

## Hotfixes necessários, resumos, atualizações cumulativas e service packs

A tabela a seguir mostra as correções necessários para cada versão dos produtos para integração com a Unificação de mensagens.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Office Communications Server 2007 R2</p></td>
<td><p>Office Communications Server 2007 R2 atualização cumulativa 10 ou posterior.</p></td>
</tr>
<tr class="even">
<td><p>Lync Server 2010</p></td>
<td><p>Lync Server 2010 atualização cumulativa 3 ou posterior.</p></td>
</tr>
<tr class="odd">
<td><p>Lync Server 2013</p></td>
<td><p>Não há atualizações são necessárias.</p></td>
</tr>
</tbody>
</table>

