---
title: 'Lista de verificação: Implantando políticas de retenção: Exchange 2013 Help'
TOCTitle: 'Lista de verificação: Implantando políticas de retenção'
ms:assetid: 59e299fd-b6a8-48f5-88ae-dc20dbe32e90
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Ee364743(v=EXCHG.150)
ms:contentKeyID: 50485648
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Lista de verificação: Implantando políticas de retenção

 

_**Aplica-se a:**Exchange Online, Exchange Server 2013_

_**Tópico modificado em:**2016-12-09_

Use esta lista de verificação para implantar diretivas de retenção em sua organização do Microsoft Exchange Server 2013. Antes de começar a trabalhar com esta lista de verificação, certifique-se de estar familiarizado com os conceitos nos tópicos a seguir:

  - [Gerenciamento de registros de mensagens](messaging-records-management-exchange-2013-help.md)

  - [Marcas e políticas de retenção](retention-tags-and-retention-policies-exchange-2013-help.md)

## Lista de verificação para implementar políticas de retenção


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Pronto?</th>
<th>Tarefas</th>
<th>Recursos</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p> </p></td>
<td><p>Avaliar os requisitos de MRM (gerenciamento de registros de mensagens) para diferentes conjuntos de usuários.</p></td>
<td><p><a href="messaging-records-management-exchange-2013-help.md">Gerenciamento de registros de mensagens</a></p></td>
</tr>
<tr class="even">
<td><p><strong> </strong></p></td>
<td><p>Determinar quais versões de cliente do Microsoft Outlook estão sendo usadas.</p></td>
<td><p>Analise os arquivos de log de acesso para cliente RPC localizados em <code>%ExchangeInstallPath%Logging\RPC Client Access</code>.</p></td>
</tr>
<tr class="odd">
<td><p> </p></td>
<td><p>Criar marcas de retenção.</p></td>
<td><p><a href="create-a-retention-policy-exchange-2013-help.md">Criar uma política de retenção</a></p></td>
</tr>
<tr class="even">
<td><p><strong> </strong></p></td>
<td><p>Criar diretivas de retenção.</p></td>
<td><p><a href="create-a-retention-policy-exchange-2013-help.md">Criar uma política de retenção</a></p></td>
</tr>
<tr class="odd">
<td><p> </p></td>
<td><p>Adicionar marcas de retenção às diretivas de retenção.</p></td>
<td><p><a href="add-retention-tags-to-or-remove-retention-tags-from-a-retention-policy-exchange-2013-help.md">Adicionar marcas de retenção com ou remova as marcas de retenção uma política de retenção</a></p></td>
</tr>
<tr class="even">
<td><p><strong> </strong></p></td>
<td><p>Pôr as caixas de correio em retenção.</p></td>
<td><p><a href="place-a-mailbox-on-retention-hold-exchange-2013-help.md">Retenção local de uma caixa de correio em retenção</a></p></td>
</tr>
<tr class="odd">
<td><p> </p></td>
<td><p>Como teste, aplicar uma diretiva de retenção a uma única caixa de correio.</p></td>
<td><p><a href="apply-a-retention-policy-to-mailboxes-exchange-2013-help.md">Aplicar uma política de retenção a caixas de correio</a></p></td>
</tr>
<tr class="even">
<td><p><strong> </strong></p></td>
<td><p>Opcional: Implementar bloqueio de clientes para bloquear clientes herdados do Outlook.</p></td>
<td><p><a href="configure-outlook-client-blocking-exchange-2013-help.md">Configurar o cliente Outlook bloqueando para gerenciamento de registros de mensagens</a></p></td>
</tr>
<tr class="odd">
<td><p> </p></td>
<td><p>Iniciar comunicação de usuários e atividades de treinamento. Incluir um prazo final em que as diretivas de retenção serão processadas; e os itens, movidos ou excluídos.</p></td>
<td><p>Não se aplica</p></td>
</tr>
<tr class="even">
<td><p><strong> </strong></p></td>
<td><p>Aplicar uma diretiva de retenção às caixas de correio adicionais.</p></td>
<td><p><a href="apply-a-retention-policy-to-mailboxes-exchange-2013-help.md">Aplicar uma política de retenção a caixas de correio</a></p></td>
</tr>
<tr class="odd">
<td><p> </p></td>
<td><p>Com alguns dias de antecedência, lembrar os usuários a respeito do prazo final.</p></td>
<td><p>Não se aplica</p></td>
</tr>
<tr class="even">
<td><p><strong> </strong></p></td>
<td><p>No prazo final, remova a retenção das caixas de correio.</p></td>
<td><p><a href="place-a-mailbox-on-retention-hold-exchange-2013-help.md">Retenção local de uma caixa de correio em retenção</a></p></td>
</tr>
</tbody>
</table>

