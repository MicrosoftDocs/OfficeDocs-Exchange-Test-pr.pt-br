---
title: 'Permissões de destinatários: Exchange 2013 Help'
TOCTitle: Permissões de destinatários
ms:assetid: 5b690bcb-c6df-4511-90e1-08ca91f43b37
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Dd638132(v=EXCHG.150)
ms:contentKeyID: 50485680
ms.date: 01/10/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Permissões de destinatários

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2015-03-09_

As permissões necessárias para executar tarefas para gerenciar remetentes variam dependendo do procedimento que está sendo executado ou o cmdlet que você deseja executar.

Para descobrir de que permissões você precisa para executar o procedimento ou executar o cmdlet, faça o seguinte:

1.  Na tabela abaixo, localize o recurso que esteja melhor relacionado ao procedimento que você deseja seguir ou ao cmdlet que você deseja executar.

2.  Depois, examine as permissões necessárias para o recurso. Você deve ter sido atribuído a um desses grupos de funções, um grupo de funções personalizado equivalente ou uma função de gerenciamento equivalente. Você também podem clicar em um grupo de funções para ver suas funções de gerenciamento. Se um recurso listar mais de um grupo de funções, você só precisa ter um dos grupos de funções para usar o recurso. Para obter mais informações sobre as funções de gerenciamento e os grupos de funções, confira [Controle de acesso baseado em função de compreensão](understanding-role-based-access-control-exchange-2013-help.md).

3.  Agora, execute o cmdlet **Get-ManagementRoleAssignment** para examinar os grupos de funções ou funções de gerenciamento atribuídas a você, para ver se você tem as permissões necessárias para gerenciar o recurso.
    

    > [!TIP]  
    > A função de gerenciamento Gerenciamento de Funções deve sido atribuída a você, para que você possa executar o cmdlet <STRONG>Get-ManagementRoleAssignment</STRONG>. Se você não tiver as permissões para executar o cmdlet <STRONG>Get-ManagementRoleAssignment</STRONG>, peça ao seu administrador do Exchange para recuperar os grupos de funções ou funções de gerenciamento atribuídas a você.



Se você quiser delegar, a outro usuário, a habilidade para gerenciar um recurso, confira [Atribuições de função de representante](delegate-role-assignments-exchange-2013-help.md).

## Permissões de servidor de Caixa de Correio

Os usuários atribuídos ao grupo de funções Gerenciamento Somente Exibição podem exibir a configuração dos recursos na tabela a seguir. Para saber mais, consulte [Gerenciamento da organização somente exibição](view-only-organization-management-exchange-2013-help.md).


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Recurso</th>
<th>Permissões obrigatórias</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Reparo de calendário, configuração do servidor</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gerenciamento da Organização</a></p>
<p><a href="server-management-exchange-2013-help.md">Gerenciamento de Servidor</a></p></td>
</tr>
<tr class="even">
<td><p>Delegando servidores de Caixa de Correio</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gerenciamento da Organização</a></p></td>
</tr>
<tr class="odd">
<td><p>Políticas de endereço de email</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gerenciamento da Organização</a></p>
<p><a href="server-management-exchange-2013-help.md">Gerenciamento de Servidor</a></p></td>
</tr>
<tr class="even">
<td><p>Pesquisa do Exchange</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gerenciamento da Organização</a></p>
<p><a href="view-only-organization-management-exchange-2013-help.md">Gerenciamento da organização somente exibição</a></p>
<p><a href="server-management-exchange-2013-help.md">Gerenciamento de Servidor</a></p></td>
</tr>
<tr class="odd">
<td><p>Exchange Pesquisar – diagnósticos</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gerenciamento da Organização</a></p>
<p><a href="view-only-organization-management-exchange-2013-help.md">Gerenciamento da organização somente exibição</a></p>
<p>Função Diagnóstico de Suporte</p>

> [!TIP]  
> A função Diagnóstico de Suporte não está atribuída a um grupo de funções. Para mais informações, consulte <A href="add-a-role-to-a-user-or-usg-exchange-2013-help.md">Adicionar uma função a um usuário ou USG</A>.


</td>
</tr>
<tr class="even">
<td><p>Métricas de grupo</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gerenciamento da Organização</a></p>
<p><a href="server-management-exchange-2013-help.md">Gerenciamento de Servidor</a></p></td>
</tr>
<tr class="odd">
<td><p>Importar e exportar</p></td>
<td><p>Função Importar Exportar Caixa de Correio</p>

> [!TIP]  
> A função Importar Exportar Caixa de Correio não está atribuída a um grupo de funções. Para obter mais informações, consulte <A href="mailbox-import-export-role-exchange-2013-help.md">Função Importar Exportar Caixa de Correio</A>.


</td>
</tr>
<tr class="even">
<td><p>Assistentes de Caixa de Correio</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gerenciamento da Organização</a></p>
<p><a href="server-management-exchange-2013-help.md">Gerenciamento de Servidor</a></p></td>
</tr>
<tr class="odd">
<td><p>Movimentações da caixa de correio</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gerenciamento da Organização</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Gerenciamento de Destinatários</a></p></td>
</tr>
<tr class="even">
<td><p>Recuperação da caixa de correio</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gerenciamento da Organização</a></p></td>
</tr>
<tr class="odd">
<td><p>Solicitação de reparo de caixa de correio</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gerenciamento da Organização</a></p>
<p><a href="server-management-exchange-2013-help.md">Gerenciamento de Servidor</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Gerenciamento de Destinatários</a></p></td>
</tr>
<tr class="even">
<td><p>Solicitação de restauração de caixa de correio</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gerenciamento da Organização</a></p></td>
</tr>
<tr class="odd">
<td><p>Configuração do servidor Caixa de Correio</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gerenciamento da Organização</a></p>
<p><a href="server-management-exchange-2013-help.md">Gerenciamento de Servidor</a></p></td>
</tr>
<tr class="even">
<td><p>Gerenciar o s serviço Indexador de Pesquisa do Exchange em um servidor de Caixa de Correio</p></td>
<td><p>Administrador local no servidor de Caixa de Correio</p></td>
</tr>
<tr class="odd">
<td><p>Conectividade MAPI</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gerenciamento da Organização</a></p>
<p><a href="server-management-exchange-2013-help.md">Gerenciamento de Servidor</a></p></td>
</tr>
<tr class="even">
<td><p>Diretórios virtuais do OAB</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gerenciamento da Organização</a></p>
<p><a href="server-management-exchange-2013-help.md">Gerenciamento de Servidor</a></p></td>
</tr>
<tr class="odd">
<td><p>Remover caixa de correio de armazenamento</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gerenciamento da Organização</a></p>
<p><a href="server-management-exchange-2013-help.md">Gerenciamento de Servidor</a></p></td>
</tr>
</tbody>
</table>


## Calendário e permissões de compartilhamento

Os usuários atribuídos ao grupo de funções Gerenciamento Somente Exibição podem exibir a configuração dos recursos na tabela a seguir. Para saber mais, consulte [Gerenciamento da organização somente exibição](view-only-organization-management-exchange-2013-help.md).


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Recurso</th>
<th>Permissões obrigatórias</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Configuração de calendário</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gerenciamento da Organização</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Gerenciamento de Destinatários</a></p>
<p><a href="help-desk-exchange-2013-help.md">Suporte Técnico</a></p></td>
</tr>
<tr class="even">
<td><p>Diagnósticos de calendário</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gerenciamento da Organização</a></p>
<p><a href="records-management-exchange-2013-help.md">Gerenciamento de Registros</a></p>
<p><a href="hygiene-management-exchange-2013-help.md">Gerenciamento de Higienização</a></p>
<p><a href="compliance-management-exchange-2013-help.md">Gerenciamento de Conformidade</a></p>
<p><a href="help-desk-exchange-2013-help.md">Suporte Técnico</a></p></td>
</tr>
<tr class="odd">
<td><p>Processamento de calendário</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gerenciamento da Organização</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Gerenciamento de Destinatários</a></p>
<p><a href="help-desk-exchange-2013-help.md">Suporte Técnico</a></p></td>
</tr>
<tr class="even">
<td><p>Notificações</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gerenciamento da Organização</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Gerenciamento de Destinatários</a></p></td>
</tr>
<tr class="odd">
<td><p>Relações da organização</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gerenciamento da Organização</a></p></td>
</tr>
<tr class="even">
<td><p>Diretivas de compartilhamento</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gerenciamento da Organização</a></p></td>
</tr>
</tbody>
</table>


## Permissões de configuração da Caixa de Correio de recursos

Os usuários atribuídos ao grupo de funções Gerenciamento Somente Exibição podem exibir a configuração dos recursos na tabela a seguir. Para saber mais, consulte [Gerenciamento da organização somente exibição](view-only-organization-management-exchange-2013-help.md).


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Recurso</th>
<th>Permissões obrigatórias</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Diretivas de reserva</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gerenciamento da Organização</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Gerenciamento de Destinatários</a></p>
<p><a href="help-desk-exchange-2013-help.md">Suporte Técnico</a></p></td>
</tr>
<tr class="even">
<td><p>Delegação</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gerenciamento da Organização</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Gerenciamento de Destinatários</a></p></td>
</tr>
<tr class="odd">
<td><p>Configuração do esquema de caixa de correio de recurso</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gerenciamento da Organização</a></p></td>
</tr>
</tbody>
</table>


## Permissões do banco de dados de caixa de correio

Os usuários atribuídos ao grupo de funções Gerenciamento Somente Exibição podem exibir a configuração dos recursos na tabela a seguir. Para saber mais, consulte [Gerenciamento da organização somente exibição](view-only-organization-management-exchange-2013-help.md).


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Recurso</th>
<th>Permissões obrigatórias</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Bancos de dados de caixa de correio</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gerenciamento da Organização</a></p>
<p><a href="server-management-exchange-2013-help.md">Gerenciamento de Servidor</a></p></td>
</tr>
</tbody>
</table>


## Permissões de provisionamento do destinatário

Esta tabela contém as várias permissões obrigatórias ao gerenciamento de destinatários.

Os usuários atribuídos ao grupo de funções Gerenciamento Somente Exibição podem exibir a configuração dos recursos na tabela a seguir. Para saber mais, consulte [Gerenciamento da organização somente exibição](view-only-organization-management-exchange-2013-help.md).


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Recurso</th>
<th>Permissões obrigatórias</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Lista de endereços, GAL</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gerenciamento da Organização</a></p></td>
</tr>
<tr class="even">
<td><p>Antispam</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gerenciamento da Organização</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Gerenciamento de Destinatários</a></p></td>
</tr>
<tr class="odd">
<td><p>Aplicativos para Outlook</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gerenciamento da Organização</a></p>
<p><a href="view-only-organization-management-exchange-2013-help.md">Gerenciamento da organização somente exibição</a></p>
<p><a href="help-desk-exchange-2013-help.md">Suporte Técnico</a></p></td>
</tr>
<tr class="even">
<td><p>Aplicando diretivas de compartilhamento</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gerenciamento da Organização</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Gerenciamento de Destinatários</a></p></td>
</tr>
<tr class="odd">
<td><p>Arbitragem</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gerenciamento da Organização</a></p></td>
</tr>
<tr class="even">
<td><p>Conectividade de arquivo</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gerenciamento da Organização</a></p>
<p><a href="view-only-organization-management-exchange-2013-help.md">Gerenciamento da organização somente exibição</a></p>
<p><a href="server-management-exchange-2013-help.md">Gerenciamento de Servidor</a></p></td>
</tr>
<tr class="odd">
<td><p>Atribuindo catálogos de endereços offline</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gerenciamento da Organização</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Gerenciamento de Destinatários</a></p></td>
</tr>
<tr class="even">
<td><p>Respostas automáticas</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gerenciamento da Organização</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Gerenciamento de Destinatários</a></p>
<p><a href="help-desk-exchange-2013-help.md">Suporte Técnico</a></p></td>
</tr>
<tr class="odd">
<td><p>Configuração de calendário</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gerenciamento da Organização</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Gerenciamento de Destinatários</a></p></td>
</tr>
<tr class="even">
<td><p>Reparo de calendário</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gerenciamento da Organização</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Gerenciamento de Destinatários</a></p></td>
</tr>
<tr class="odd">
<td><p>Configurações de contato de agregação</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gerenciamento da Organização</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Gerenciamento de Destinatários</a></p>
<p><a href="view-only-organization-management-exchange-2013-help.md">Gerenciamento da organização somente exibição</a></p></td>
</tr>
<tr class="even">
<td><p>Caixas de correio desconectadas</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gerenciamento da Organização</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Gerenciamento de Destinatários</a></p>
<p><a href="help-desk-exchange-2013-help.md">Suporte Técnico</a></p></td>
</tr>
<tr class="odd">
<td><p>Grupos de distribuição</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gerenciamento da Organização</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Gerenciamento de Destinatários</a></p></td>
</tr>
<tr class="even">
<td><p>Grupos dinâmicos de distribuição</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gerenciamento da Organização</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Gerenciamento de Destinatários</a></p></td>
</tr>
<tr class="odd">
<td><p>Emails</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gerenciamento da Organização</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Gerenciamento de Destinatários</a></p>
<p><a href="um-management-exchange-2013-help.md">Gerenciamento de UM</a></p></td>
</tr>
<tr class="even">
<td><p>Regras da Caixa de Entrada</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gerenciamento da Organização</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Gerenciamento de Destinatários</a></p>
<p><a href="help-desk-exchange-2013-help.md">Suporte Técnico</a></p></td>
</tr>
<tr class="odd">
<td><p>Contatos de email</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gerenciamento da Organização</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Gerenciamento de Destinatários</a></p></td>
</tr>
<tr class="even">
<td><p>Dicas de email</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gerenciamento da Organização</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Gerenciamento de Destinatários</a></p></td>
</tr>
<tr class="odd">
<td><p>Usuário de email</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gerenciamento da Organização</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Gerenciamento de Destinatários</a></p></td>
</tr>
<tr class="even">
<td><p>Permissões de pasta da Caixa de Correio</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gerenciamento da Organização</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Gerenciamento de Destinatários</a></p>
<p><a href="help-desk-exchange-2013-help.md">Suporte Técnico</a></p></td>
</tr>
<tr class="odd">
<td><p>Pastas de caixa de correio</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gerenciamento da Organização</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Gerenciamento de Destinatários</a></p></td>
</tr>
<tr class="even">
<td><p>Conectividade MAPI</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gerenciamento da Organização</a></p>
<p></p></td>
</tr>
<tr class="odd">
<td><p>Configuração de mensagem</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gerenciamento da Organização</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Gerenciamento de Destinatários</a></p>
<p><a href="help-desk-exchange-2013-help.md">Suporte Técnico</a></p></td>
</tr>
<tr class="even">
<td><p>Cotas de mensagem</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gerenciamento da Organização</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Gerenciamento de Destinatários</a></p></td>
</tr>
<tr class="odd">
<td><p>Moderação</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gerenciamento da Organização</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Gerenciamento de Destinatários</a></p></td>
</tr>
<tr class="even">
<td><p>Permissões e delegação</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gerenciamento da Organização</a></p></td>
</tr>
<tr class="odd">
<td><p>Caixas de correio de arquivo morto</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gerenciamento da Organização</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Gerenciamento de Destinatários</a></p></td>
</tr>
<tr class="even">
<td><p>Propriedades de dados do destinatário</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gerenciamento da Organização</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Gerenciamento de Destinatários</a></p></td>
</tr>
<tr class="odd">
<td><p>Caixas de correio remotas</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gerenciamento da Organização</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Gerenciamento de Destinatários</a></p></td>
</tr>
<tr class="even">
<td><p>Retenção e guardas de documentos</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gerenciamento da Organização</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Gerenciamento de Destinatários</a></p>
<p><a href="records-management-exchange-2013-help.md">Gerenciamento de Registros</a></p></td>
</tr>
<tr class="odd">
<td><p>Enviar como</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gerenciamento da Organização</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Gerenciamento de Destinatários</a></p></td>
</tr>
<tr class="even">
<td><p>Configuração de ortografia</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gerenciamento da Organização</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Gerenciamento de Destinatários</a></p>
<p><a href="help-desk-exchange-2013-help.md">Suporte Técnico</a></p></td>
</tr>
<tr class="odd">
<td><p>Unificação de Mensagens</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gerenciamento da Organização</a></p>
<p><a href="um-management-exchange-2013-help.md">Gerenciamento de UM</a></p></td>
</tr>
<tr class="even">
<td><p>Caixas de correio de usuários</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gerenciamento da Organização</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Gerenciamento de Destinatários</a></p></td>
</tr>
<tr class="odd">
<td><p>Fotos do usuário</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gerenciamento da Organização</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Gerenciamento de Destinatários</a></p>
<p><a href="help-desk-exchange-2013-help.md">Suporte Técnico</a></p></td>
</tr>
</tbody>
</table>


## Movimentação de caixa de correio e permissões de migração

A tabela contém as permissões que são necessárias para mover caixas de correio locais para domínios ou florestas diferentes e para migrar caixas de correio locais de e para sua organização baseada na nuvem.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Recurso</th>
<th>Permissões obrigatórias</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Movimentações de caixa de correio (locais ou entre florestas)</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gerenciamento da Organização</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Gerenciamento de Destinatários</a></p></td>
</tr>
<tr class="even">
<td><p>Movimentações de caixa de correio (implantação híbrida)</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gerenciamento da Organização</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Gerenciamento de Destinatários</a></p></td>
</tr>
<tr class="odd">
<td><p>Migração (inclusão e exclusão da nuvem)</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gerenciamento da Organização</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Gerenciamento de Destinatários</a></p></td>
</tr>
</tbody>
</table>

