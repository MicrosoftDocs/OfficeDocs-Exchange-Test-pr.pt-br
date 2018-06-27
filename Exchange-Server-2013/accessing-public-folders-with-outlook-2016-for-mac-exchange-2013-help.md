---
title: 'Acesso a pastas públicas com 2016 do Outlook para Mac: Exchange 2013 Help'
TOCTitle: Acesso a pastas públicas com 2016 do Outlook para Mac
ms:assetid: bc9b8226-bd8b-4edc-882b-4f19cfe118eb
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Mt788631(v=EXCHG.150)
ms:contentKeyID: 74115364
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Acesso a pastas públicas com 2016 do Outlook para Mac

 

_**Aplica-se a:**Exchange Online, Exchange Server 2013, Exchange Server 2016, Office 365_

_**Tópico modificado em:**2017-05-19_

**Resumo:** O mais recente com suporte a topologias do Exchange que permitem aos usuários acessar pastas públicas com 2016 do Outlook para Mac.

Com as versões de [atualização de abril de 2016](https://go.microsoft.com/fwlink/?linkid=829202) o para 2016 Outlook clientes Mac, [14 de atualização cumulativa (CU14)](https://go.microsoft.com/fwlink/p/?linkid=849432) for Exchange 2013 e [2 de atualização cumulativa (CU 2)](https://go.microsoft.com/fwlink/p/?linkid=849793) , para Exchange 2016, usuários de 2016 Outlook para Mac agora podem acessar pastas públicas no mais tipos de topologias do que poderiam antes.

## Outlook para limitações do Mac

Todas as versões do Outlook para Mac podem acessar pastas públicas do Exchange, mas até recentemente esses clientes não foi possível acessar pastas públicas nos seguintes cenários de implantação:

  - **Coexistência com pastas públicas herdadas.** Quando a caixa de correio de um usuário está em um servidor Exchange 2013 ou Exchange 2016, o usuário não pode usar o Outlook para Mac para acessar pastas públicas implantadas em servidores executando o Exchange 2010 SP3 ou posteriores. Outros clientes podem acessar essas pastas públicas herdadas neste cenário.

  - **Topologias híbridas.** Usuários locais com uma caixa de correio com base no Exchange Online não poderiam usar o Outlook para Mac para acessar pastas públicas moderno do local. Da mesma forma, os usuários com um Exchange 2013 ou 2016 Exchange da caixa de correio local não pôde usar Outlook para Mac para acessar pastas públicas implantado no Exchange Online.

## Outlook 2016 para Mac

Com a atualização de abril de 2016 para 2016 do Outlook para Mac, bem como CU14 para o Exchange 2013 e atualização cumulativa 2 para Exchange 2016, os cenários acima agora funcionará para Outlook 2016 clientes Mac.

A tabela a seguir resume as topologias com suporte para usuários com o Outlook 2016 clientes Mac tentando acessar pastas públicas no Exchange 2013, 2016 do Exchange e o Exchange Online.


> [!TIP]
> Cenários mostrados na tabela a seguir pressupõem que a atualização de abril de 2016 para 2016 do Outlook para Mac foi aplicada a todos os clientes.




<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>Pastas públicas são implantadas em …</th>
<th>Caixa de correio do usuário está no Exchange 2010 SP3 ou posterior</th>
<th>Caixa de correio do usuário está no Exchange 2013 CU13 ou posterior</th>
<th>Caixa de correio do usuário está no Exchange 2016 CU2 ou posterior</th>
<th>Caixa de correio do usuário está no Office 365/Exchange Online</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Exchange Server 2010 SP3 ou posterior</p></td>
<td><p>Com suporte</p></td>
<td><p>Com suporte</p></td>
<td><p>Com suporte</p></td>
<td><p>Sem suporte</p></td>
</tr>
<tr class="even">
<td><p>Exchange Server 2013 CU13 ou posterior</p></td>
<td><p>Sem suporte</p></td>
<td><p>Com suporte</p></td>
<td><p>Com suporte</p></td>
<td><p>Com suporte</p></td>
</tr>
<tr class="odd">
<td><p>Exchange Server 2016 CU2 ou posterior</p></td>
<td><p>Sem suporte</p></td>
<td><p>Com suporte</p></td>
<td><p>Com suporte</p></td>
<td><p>Com suporte</p></td>
</tr>
<tr class="even">
<td><p>O Office 365 / Exchange Online</p></td>
<td><p>Sem suporte</p></td>
<td><p>Com suporte</p></td>
<td><p>Com suporte</p></td>
<td><p>Com suporte</p></td>
</tr>
</tbody>
</table>


Os seguintes artigos descrevem como implantar as pastas públicas em sua organização do Exchange em uma coexistência ou topologia híbrida. Desde que seu 2016 Outlook clientes Mac instalou a atualização de abril de 2016, eles poderão acessar pastas públicas nas configurações detalhadas nestes artigos:

  - [Configurar as pastas públicas herdadas nas quais as caixas de correio dos usuários estão em servidores do Exchange 2013](configure-legacy-public-folders-where-user-mailboxes-are-on-exchange-2013-servers-exchange-2013-help.md)

  - [Configurar pastas públicas do Exchange 2013 para uma implantação híbrida](configure-exchange-2013-public-folders-for-a-hybrid-deployment-exchange-2013-help.md)

  - [Configurar pastas públicas do Exchange Online para uma implantação híbrida](configure-exchange-online-public-folders-for-a-hybrid-deployment-exchange-2013-help.md)

