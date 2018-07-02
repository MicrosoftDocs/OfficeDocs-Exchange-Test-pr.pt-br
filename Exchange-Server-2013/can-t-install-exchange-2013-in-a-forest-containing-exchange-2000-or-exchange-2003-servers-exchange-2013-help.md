---
title: 'Não é possível instalar o Exchange 2013 em uma floresta que contém os servidores Exchange 2000 ou Exchange 2003.: Exchange 2013 Help'
TOCTitle: Não é possível instalar o Exchange 2013 em uma floresta que contém os servidores Exchange 2000 ou Exchange 2003.
ms:assetid: a115b182-cbd2-4d31-aa0e-375240939301
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/ms.exch.setupreadiness.exchange2000or2003presentinorg(v=EXCHG.150)
ms:contentKeyID: 50486280
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Não é possível instalar o Exchange 2013 em uma floresta que contém os servidores Exchange 2000 ou Exchange 2003.

 

_**Aplica-se a:** Exchange Server_

_**Tópico modificado em:** 2016-12-09_

Microsoft Exchange Server 2013 não pode continuar porque um ou mais computadores que executam o Exchange 2000 Server ou Exchange Server 2003 foram encontrados na floresta do Active Directory. Antes de instalar o Exchange 2013, todos os servidores Exchange 2000 e Exchange 2003 devem ser removidos da floresta. Caixas de correio, pastas públicas e todos os outros objetos do Exchange ou componentes devem ser atualizados para Exchange Server 2007 ou Exchange Server 2010. Você não pode atualizar do Exchange 2000 ou Exchange 2003 diretamente ao Exchange 2013.

O caminho que precisam ser seguidas para instalar o Exchange 2013 em sua organização depende da versão do Exchange que você tiver instalado em sua floresta. Consulte a tabela a seguir para obter mais informações.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Se você tiver este produto instalado em sua organização</th>
<th>Você deve tomar esse caminho para atualizar para o Exchange 2013</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Exchange 2000</p></td>
<td><ol>
<li><p>Instale o Exchange 2007 na sua organização do Exchange 2000.</p></li>
<li><p>Configure a coexistência do Exchange 2007 e Exchange 2000.</p></li>
<li><p>Migre as caixas de correio, as pastas públicas e outros componentes do Exchange 2000 para o Exchange 2007.</p></li>
<li><p>Desative e remova todos os servidores do Exchange 2000.</p></li>
<li><p>Instale o Exchange 2013 em sua organização do Exchange 2007.</p></li>
<li><p>Configure a coexistência do Exchange 2013 e Exchange 2007.</p></li>
<li><p>Migre as caixas de correio, as pastas públicas e outros componentes do Exchange 2007 para o Exchange 2013.</p></li>
<li><p>Desative e remova todos os servidores do Exchange 2007.</p></li>
</ol>
<p>Para obter mais informações, consulte <a href="https://go.microsoft.com/fwlink/p/?linkid=103281">Atualizando para o Exchange 2007</a> e <a href="upgrade-from-exchange-2007-to-exchange-2013-exchange-2013-help.md">Atualização do Exchange 2007 para o Exchange 2013</a>.</p></td>
</tr>
<tr class="even">
<td><p>Exchange 2003</p></td>
<td><ol>
<li><p>Instale o Exchange 2010 na sua organização do Exchange 2003.</p></li>
<li><p>Configure a coexistência do Exchange 2010 e Exchange 2003.</p></li>
<li><p>Migre as caixas de correio, as pastas públicas e outros componentes do Exchange 2003 para o Exchange 2010.</p></li>
<li><p>Desative e remova todos os servidores do Exchange 2003.</p></li>
<li><p>Instale o Exchange 2013 em sua organização do Exchange 2010.</p></li>
<li><p>Configure a coexistência do Exchange 2013 e Exchange 2010.</p></li>
<li><p>Migre caixas de correio, pastas públicas e outros componentes do Exchange 2010 para o Exchange 2013.</p></li>
<li><p>Desative e remova todos os servidores do Exchange 2010.</p></li>
</ol>
<p>Para obter mais informações, consulte <a href="https://go.microsoft.com/fwlink/p/?linkid=268414">Exchange 2003 – mapa de planejamento para atualização e coexistência</a> e <a href="upgrade-from-exchange-2010-to-exchange-2013-exchange-2013-help.md">Atualizar do Exchange 2010 para o Exchange 2013</a>.</p></td>
</tr>
</tbody>
</table>


Ao atualizar para Exchange 2010 ou Exchange 2013, você pode usar o Assistente de implantação do Exchange para ajudá-lo a concluir sua implantação. Para obter mais informações, consulte os seguintes links:

  - [Assistente de implantação do Exchange 2010](https://go.microsoft.com/fwlink/p/?linkid=171086)

  - [Exchange 2013 Deployment Assistant](https://go.microsoft.com/fwlink/p/?linkid=277105)

Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), ou [Proteção do Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=285351).

Você encontrou o que você está procurando? Por favor, separe um minuto do seu tempo para [enviar seus comentários para nós](mailto:exsetuphelpfeedback@microsoft.com?subject=exchange%202013%20setup%20help%20feedback) sobre as informações que você estava esperando encontrar.

