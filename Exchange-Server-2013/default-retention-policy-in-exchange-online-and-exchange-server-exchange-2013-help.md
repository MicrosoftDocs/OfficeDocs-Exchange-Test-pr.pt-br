---
title: 'Política de retenção padrão no Exchange Online e Exchange Server: Exchange 2013 Help'
TOCTitle: Política de retenção padrão
ms:assetid: bcf31b2d-463b-4623-b488-c8ac40f14f62
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Dn775046(v=EXCHG.150)
ms:contentKeyID: 62625499
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Política de retenção padrão no Exchange Online e Exchange Server

 

_**Aplica-se a:**Exchange Online, Exchange Server 2013_

_**Tópico modificado em:**2015-03-09_

Exchange cria a política MRM padrão da política de retenção no seu Exchange Online e Exchange organização local. A política será automaticamente aplicada a novos usuários no Exchange Online. Em organizações do local, a política é aplicada quando você cria um arquivo morto da caixa de correio. Você pode alterar a política de retenção aplicada a um usuário a qualquer momento.

Você pode modificar marcas incluídas na política MRM padrão, por exemplo, alterando a idade de retenção ou as ações de retenção, desabilitar uma marca ou modificar a política adicionando ou removendo marcas a partir dele. A política atualizada será aplicada às caixas de correio na próxima vez em que eles são processados pelo Assistente de pasta gerenciada

## Marcas de retenção vinculadas à Política MRM Padrão

A tabela a seguir lista as marcas de retenção padrão vinculadas à Política MRM Padrão.


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Nome</th>
<th>Tipo</th>
<th>Tempo de retenção (dias)</th>
<th>Ação de retenção</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Padrão: mover para arquivo morto em 2 anos</p></td>
<td><p>Marca de diretiva padrão (DPT)</p></td>
<td><p>730</p></td>
<td><p>Mover para arquivo morto</p></td>
</tr>
<tr class="even">
<td><p>Itens Recuperáveis: mover para arquivo morto em 14 dias</p></td>
<td><p>Pasta Itens Recuperáveis</p></td>
<td><p>14</p></td>
<td><p>Mover para arquivo morto</p></td>
</tr>
<tr class="odd">
<td><p>Pessoal: mover para arquivo morto em 1 ano</p></td>
<td><p>Marca pessoal</p></td>
<td><p>365</p></td>
<td><p>Mover para arquivo morto</p></td>
</tr>
<tr class="even">
<td><p>Pessoal: mover para arquivo morto em 5 anos</p></td>
<td><p>Marca pessoal</p></td>
<td><p>1,825</p></td>
<td><p>Mover para arquivo morto</p></td>
</tr>
<tr class="odd">
<td><p>Pessoal: nunca mover para arquivo morto</p></td>
<td><p>Marca pessoal</p></td>
<td><p>Não aplicável</p></td>
<td><p>Mover para arquivo morto</p></td>
</tr>
<tr class="even">
<td><p>Excluir em 1 semana</p></td>
<td><p>Marca pessoal</p></td>
<td><p>7</p></td>
<td><p>Excluir e Permitir Recuperação</p></td>
</tr>
<tr class="odd">
<td><p>Excluir em 1 mês</p></td>
<td><p>Marca pessoal</p></td>
<td><p>30</p></td>
<td><p>Excluir e Permitir Recuperação</p></td>
</tr>
<tr class="even">
<td><p>Excluir em 6 meses</p></td>
<td><p>Marca pessoal</p></td>
<td><p>180</p></td>
<td><p>Excluir e Permitir Recuperação</p></td>
</tr>
<tr class="odd">
<td><p>Excluir em 1 ano</p></td>
<td><p>Marca pessoal</p></td>
<td><p>365</p></td>
<td><p>Excluir e Permitir Recuperação</p></td>
</tr>
<tr class="even">
<td><p>Excluir em 5 anos</p></td>
<td><p>Marca pessoal</p></td>
<td><p>1,825</p></td>
<td><p>Excluir e Permitir Recuperação</p></td>
</tr>
<tr class="odd">
<td><p>Nunca excluir</p></td>
<td><p>Marca pessoal</p></td>
<td><p>NA (Not applicable)</p></td>
<td><p>Excluir e Permitir Recuperação</p></td>
</tr>
</tbody>
</table>


## O que você pode fazer com a política MRM padrão


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Você pode …</th>
<th>No Exchange Online …</th>
<th>No Exchange Server …</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Aplicar a política MRM padrão automaticamente aos novos usuários</p></td>
<td><p>Sim, aplicadas por padrão. Nenhuma ação é necessária.</p></td>
<td><p>Sim, aplicadas por padrão, se você também criar um arquivo morto do novo usuário.</p>
<p>Se você criar um arquivo morto para o usuário mais tarde, a política será aplicada automaticamente somente se o usuário não tem uma política de retenção existente.</p></td>
</tr>
<tr class="even">
<td><p>Modificar a idade de retenção ou ação de uma marca de retenção vinculada à política de retenção</p></td>
<td><p>Sim</p></td>
<td><p>Sim</p></td>
</tr>
<tr class="odd">
<td><p>Desabilitar uma marca de retenção vinculada à política</p></td>
<td><p>Sim</p></td>
<td><p>Sim</p></td>
</tr>
<tr class="even">
<td><p>Adicionar uma marca de retenção à política</p></td>
<td><p>Sim</p></td>
<td><p>Sim</p></td>
</tr>
<tr class="odd">
<td><p>Remover uma marca de retenção da política</p></td>
<td><p>Sim</p></td>
<td><p>Sim</p></td>
</tr>
<tr class="even">
<td><p>Definir a diretiva de outra como a política de retenção padrão a serem aplicadas automaticamente aos novos usuários</p></td>
<td><p>Não</p></td>
<td><p>Não</p></td>
</tr>
</tbody>
</table>


## Mais informações

  - Uma marca de retenção pode ser vinculada a mais de uma política de retenção. Para obter detalhes sobre como gerenciar [Marcas e políticas de retenção](retention-tags-and-retention-policies-exchange-2013-help.md), consulte [Procedimentos de gerenciamento de registros de mensagens](messaging-records-management-procedures-exchange-2013-help.md).

  - A política MRM padrão não inclui um DPT para excluir automaticamente os itens (mas conter marcas pessoais com a ação de retenção de exclusão que os usuários podem aplicar a itens de caixa de correio). Se você deseja excluir automaticamente os itens após um período especificado, você pode criar um DPT com a ação de excluir necessários e adicioná-lo à política. Para obter detalhes, consulte [Criar uma política de retenção](create-a-retention-policy-exchange-2013-help.md) e [Adicionar marcas de retenção com ou remova as marcas de retenção uma política de retenção](add-retention-tags-to-or-remove-retention-tags-from-a-retention-policy-exchange-2013-help.md).

  - As políticas de retenção são aplicadas a usuários de caixa de correio. A mesma política se aplica à caixa de correio e ao arquivo morto do usuário.

