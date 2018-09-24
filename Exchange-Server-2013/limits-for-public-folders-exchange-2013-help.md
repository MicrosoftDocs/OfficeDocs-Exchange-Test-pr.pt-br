---
title: 'Limites para pastas públicas: Exchange 2013 Help'
TOCTitle: Limites para pastas públicas
ms:assetid: 709b075e-9584-484b-bcaa-e781c26497b4
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Dn594582(v=EXCHG.150)
ms:contentKeyID: 61170939
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Limites para pastas públicas

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2016-12-09_

No Exchange Server 2013, nós movemos as pastas públicas de uma arquitetura de banco de dados tradicional para uma arquitetura de caixa de correio. Esta mudança permite que pastas públicas se beneficiem de coisas como a resiliência de um Grupo de Disponibilidade de Banco de Dados (DAG) e outros aprimoramentos feitos ao longo dos anos. Entretanto, existem novos limites e preocupações de desempenho que devem ser levados em consideração. Neste documento, oferecemos uma orientação de alto nível sobre opções de configuração disponíveis que poderiam afetar o desempenho e a conectividade da pasta pública.

## Limites

A tabela a seguir lista os limites de pastas públicas no Exchange Server 2013 no local. Exceto quando os limites são declarados especificamente conforme recomendado, os valores listados nesta tabela são os limites com suporte para pastas públicas.


> [!IMPORTANT]
> Procurando por limites do Exchange Online para Office 365? Consulte <A href="https://go.microsoft.com/fwlink/?linkid=391188">limites do Exchange Online</A>.




<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Item</th>
<th>Limites</th>
<th>Observações</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Quantidade total de caixas de correio de pasta pública</p></td>
<td><p>100</p></td>
<td><p>Embora você possa criar mais de 100 caixas de correio de pasta pública, não há suporte para uma quantidade maior. <a href="https://docs.microsoft.com/pt-br/exchange/collaboration-exo/public-folders/create-public-folder-mailbox">Criar uma caixa de correio de pasta pública</a></p></td>
</tr>
<tr class="even">
<td><p>Total de pastas públicas na hierarquia</p></td>
<td><p>1,000,000</p></td>
<td><p>Embora você possa criar mais de 1.000.000 pastas públicas, isso não é suportado. Para qualquer implantação de pastas de 100.000 ou mais públicas, recomendamos a leitura <a href="considerations-when-deploying-public-folders-exchange-2013-help.md">Considerações ao implantar a pastas públicas</a>.</p></td>
</tr>
<tr class="odd">
<td><p>Subpastas sob a pasta pai</p></td>
<td><p>10,000</p></td>
<td><p>Embora você possa criar mais de 1.000 subpastas sob uma pasta pai, não recomendamos que isso seja feito.</p>
<p>Parâmetro <em>FolderHierarchyChildrenCountReceiveQuota</em> no cmdlet <a href="https://technet.microsoft.com/pt-br/library/bb123981(v=exchg.150)">Set-Mailbox</a>.</p></td>
</tr>
<tr class="even">
<td><p>Profundidade da pasta</p></td>
<td><p>300</p></td>
<td><p>A profundidade da pasta é o número de níveis de pastas aninhadas que pode existir em um ramo de uma árvore de pastas públicas. Parâmetro <em>FolderHierarchyDepthRecieveQuota</em> no cmdlet <a href="https://technet.microsoft.com/pt-br/library/bb123981(v=exchg.150)">Set-Mailbox</a>.</p></td>
</tr>
<tr class="odd">
<td><p>Máximo de mensagens por pasta pública</p></td>
<td><p>1 milhão</p></td>
<td><p>Parâmetro <em>MailboxMessagesPerFolderCountRecieveQuota</em> no cmdlet <a href="https://technet.microsoft.com/pt-br/library/bb123981(v=exchg.150)">Set-Mailbox</a>.</p></td>
</tr>
<tr class="even">
<td><p>Tamanho máximo de pasta pública individual</p></td>
<td><p>10 GB</p></td>
<td><p>Este limite não inclui subpastas em uma única pasta.</p>
<p><a href="configure-storage-quotas-for-a-mailbox-exchange-2013-help.md">Configurar cotas de armazenamento para uma caixa de correio</a></p></td>
</tr>
<tr class="odd">
<td><p>Tamanho da caixa de correio da pasta pública</p></td>
<td><p>100 GB</p></td>
<td><p><a href="configure-storage-quotas-for-a-mailbox-exchange-2013-help.md">Configurar cotas de armazenamento para uma caixa de correio</a></p></td>
</tr>
<tr class="even">
<td><p>Número de logons de usuário por caixa de correio de pasta pública</p></td>
<td><p>2.000 logons de usuários simultâneos</p></td>
<td><p>Recomendamos que você configure sua hierarquia para não ter mais de 2.000 usuários por caixa de correio de pasta pública. Por exemplo, se você tiver 20.000 usuários, deverá ter 10 caixas de correio de pasta pública.</p></td>
</tr>
<tr class="odd">
<td><p>Retenção de item movido</p></td>
<td><p>14 dias recomendados</p></td>
<td><p>Use o parâmetro <em>DefaultPublicFolderMovedItemRetention</em> no cmdlet <strong>Set-OrganizationConfig</strong>.</p></td>
</tr>
<tr class="even">
<td><p>Limites de idade</p></td>
<td><p>Recomendamos que você defina esta configuração com o mesmo padrão usado para caixas de correio regulares.</p></td>
<td><p>Essas configurações podem ser definidas nos seguintes níveis:</p>
<ul>
<li><p><strong>Nível organizacional:</strong> Use o parâmetro <em>DefaultPublicFolderAgeLimit</em> no cmdlet <strong>Set-OrganizationConfig</strong>.</p></li>
<li><p><strong>Nível de caixa de correio:</strong> Parâmetro <em>AgeLimit</em> no cmdlet <strong>Set-Mailbox</strong>.</p></li>
<li><p><strong>Nível de pasta:</strong> Parâmetro <em>AgeLimit</em> no cmdlet <strong>Set-PublicFolder</strong>.</p></li>
</ul>
<p></p></td>
</tr>
<tr class="odd">
<td><p>Retenção de item excluído</p></td>
<td><p>Recomendamos que você defina esta configuração com o mesmo padrão usado para caixas de correio regulares.</p></td>
<td><p>Essas configurações podem ser definidas nos seguintes níveis:</p>
<ul>
<li><p><strong>Nível organizacional:Use o parâmetro</strong> <em>DefaultPublicFolderMovedItemRetention</em> no cmdlet <strong>Set-OrganizationConfig</strong>.</p></li>
<li><p><strong>Nível de caixa de correio:</strong> Parâmetro <em>RetainDeletedItemsFor</em> no cmdlet <strong>Set-Mailbox</strong>.</p></li>
<li><p><strong>Nível de pasta:</strong> Parâmetro <em>RetainDeleteItemsFor</em> no cmdlet <strong>Set-PublicFolder</strong>.</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Número máximo de pastas públicas que podem ser migrados para o Exchange 2013</p></td>
<td><p>500,000</p></td>
<td><p>Este é o número máximo de pastas públicas, que você pode mover de uma versão herdada do Exchange em uma única migração para o Exchange 2013. Para obter detalhes sobre a migração de pastas públicas, consulte <a href="use-batch-migration-to-migrate-public-folders-to-exchange-2013-from-previous-versions-exchange-2013-help.md">Usar a migração de lote para migrar pastas públicas para o Exchange 2013 de versões anteriores</a></p></td>
</tr>
</tbody>
</table>

