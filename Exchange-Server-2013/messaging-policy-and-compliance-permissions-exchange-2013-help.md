---
title: 'Permissões de política e conformidade de mensagens: Exchange 2013 Help'
TOCTitle: Permissões de política e conformidade de mensagens
ms:assetid: ec4d3b9f-b85a-4cb9-95f5-6fc149c3899b
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Dd638205(v=EXCHG.150)
ms:contentKeyID: 50486939
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Permissões de política e conformidade de mensagens

 

_**Aplica-se a:** Exchange Online, Exchange Server 2013_

_**Tópico modificado em:** 2016-12-09_

As permissões exigidas para configurar as diretivas e a conformidade de mensagens variam dependendo do procedimento que está sendo executado ou do cmdlet que você deseja executar. Para obter mais informações sobre diretivas e conformidade de mensagens, consulte [Conformidade e política de sistema de mensagens](messaging-policy-and-compliance-exchange-2013-help.md).

Para descobrir de que permissões você precisa para executar o procedimento ou executar o cmdlet, faça o seguinte:

1.  Na tabela abaixo, localize o recurso que esteja melhor relacionado ao procedimento que você deseja seguir ou ao cmdlet que você deseja executar.

2.  Depois, examine as permissões necessárias para o recurso. Você deve ter sido atribuído a um desses grupos de funções, um grupo de funções personalizado equivalente ou uma função de gerenciamento equivalente. Você também podem clicar em um grupo de funções para ver suas funções de gerenciamento. Se um recurso listar mais de um grupo de funções, você só precisa ter um dos grupos de funções para usar o recurso. Para obter mais informações sobre as funções de gerenciamento e os grupos de funções, confira [Controle de acesso baseado em função de compreensão](understanding-role-based-access-control-exchange-2013-help.md).

3.  Agora, execute o cmdlet **Get-ManagementRoleAssignment** para examinar os grupos de funções ou funções de gerenciamento atribuídas a você, para ver se você tem as permissões necessárias para gerenciar o recurso.
    

    > [!TIP]  
    > A função de gerenciamento Gerenciamento de Funções deve sido atribuída a você, para que você possa executar o cmdlet <STRONG>Get-ManagementRoleAssignment</STRONG>. Se você não tiver as permissões para executar o cmdlet <STRONG>Get-ManagementRoleAssignment</STRONG>, peça ao seu administrador do Exchange para recuperar os grupos de funções ou funções de gerenciamento atribuídas a você.



Se você quiser delegar, a outro usuário, a habilidade para gerenciar um recurso, confira [Atribuições de função de representante](delegate-role-assignments-exchange-2013-help.md).


> [!TIP]  
> Pode haver, nos servidores de Transporte de Borda, alguns recursos que você queira gerenciar. Para gerenciar os recursos nos servidores de Transporte de Borda, você precisa se tornar um membro do grupo Administradores Locais, no servidor de Transporte de Borda que você deseja gerenciar. Servidores de Transporte de Borda não usam o Controle de Acesso Baseado na Função (RBAC). Os recursos que podem ser gerenciados nos servidores de Transporte de Borda têm Administrador Local de Transporte de Borda na coluna "Permissões necessárias" na tabela abaixo.



## Permissões de política e conformidade de mensagens

Você pode usar os recursos da tabela a seguir para configurar os recursos de diretivas e conformidade de mensagens. Os grupos de função necessários para configurar cada recurso estão listados.

Os usuários atribuídos ao grupo de funções Gerenciamento Somente para Exibição podem visualizar a configuração dos recursos na tabela a seguir. Para obter mais informações, consulte [Gerenciamento da organização somente exibição](view-only-organization-management-exchange-2013-help.md).


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Recurso</th>
<th>Permissões necessárias</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Prevenção de perda de dados (DLP)</p></td>
<td><p>Se usando o Office 365:</p>
<ul>
<li><p><a href="https://go.microsoft.com/fwlink/p/?linkid=335814">Administrador global do office 365</a>, que inclui automaticamente o Exchange <a href="organization-management-exchange-2013-help.md">Gerenciamento da Organização</a></p></li>
<li><p><a href="https://go.microsoft.com/fwlink/p/?linkid=335814">Administrador de serviços do Office 365</a>, mais o grupo de funções de administração de <a href="organization-management-exchange-2013-help.md">Gerenciamento da Organização</a> no Exchange</p></li>
<li><p><a href="https://go.microsoft.com/fwlink/p/?linkid=335814">Administrador de senha do Office 365</a></p></li>
</ul>
<p>Se usando apenas o Exchange Server 2013 ou o Exchange Online:</p>
<ul>
<li><p><a href="compliance-management-exchange-2013-help.md">Gerenciamento de Conformidade</a></p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Excluir conteúdo da caixa de correio (usando o cmdlet <a href="https://technet.microsoft.com/pt-br/library/dd298173(v=exchg.150)">Search-Mailbox</a> com a opção <em>DeleteContent</em>)</p></td>
<td><p><a href="discovery-management-exchange-2013-help.md">Gerenciamento de Descobertas</a> <strong>e</strong></p>
<p><a href="mailbox-import-export-role-exchange-2013-help.md">Função Importar Exportar Caixa de Correio</a></p>

> [!TIP]  
> Por padrão, a função Importar Exportar Caixa de Correio não está atribuída a um grupo de funções. Você pode atribuir uma função de gerenciamento a um grupo de funções personalizado interno, um usuário ou um grupo de segurança universal. É recomendado atribuir uma função a um grupo de funções. Para obter mais informações, consulte <A href="add-a-role-to-a-user-or-usg-exchange-2013-help.md">Adicionar uma função a um usuário ou USG</A>.


</td>
</tr>
<tr class="odd">
<td><p>Caixas de Correio de Descoberta – Criar</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gerenciamento da Organização</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Gerenciamento de Destinatários</a></p></td>
</tr>
<tr class="even">
<td><p>Registro no Diário</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gerenciamento da Organização</a></p>
<p><a href="records-management-exchange-2013-help.md">Gerenciamento de Registros</a></p></td>
</tr>
<tr class="odd">
<td><p>Registro em log de auditoria da caixa de correio</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gerenciamento da Organização</a></p>
<p><a href="records-management-exchange-2013-help.md">Gerenciamento de Registros</a></p></td>
</tr>
<tr class="even">
<td><p>Classificações de mensagem</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gerenciamento da Organização</a></p></td>
</tr>
<tr class="odd">
<td><p>Gerenciamento de registros de mensagens</p></td>
<td><p><a href="compliance-management-exchange-2013-help.md">Gerenciamento de Conformidade</a></p>
<p><a href="organization-management-exchange-2013-help.md">Gerenciamento da Organização</a></p>
<p><a href="records-management-exchange-2013-help.md">Gerenciamento de Registros</a></p></td>
</tr>
<tr class="even">
<td><p>Descoberta eletrônica In-loco</p></td>
<td><p><a href="discovery-management-exchange-2013-help.md">Gerenciamento de Descobertas</a></p>

> [!TIP]  
> Por padrão, o grupo de função Gerenciamento de Descoberta não tem membros. Nenhum usuário, incluindo administradores, tem as permissões necessárias para buscar caixas de correio. Para mais informações, consulte <A href="assign-ediscovery-permissions-in-exchange-exchange-2013-help.md">Atribuir permissões de descoberta eletrônica no Exchange</A>.


</td>
</tr>
<tr class="odd">
<td><p>Retenção Local</p></td>
<td><p><a href="discovery-management-exchange-2013-help.md">Gerenciamento de Descobertas</a></p>
<p><a href="organization-management-exchange-2013-help.md">Gerenciamento da Organização</a></p>

> [!IMPORTANT]  
> Para criar um Bloqueio In-loco baseado em consulta, um usuário requer que as funções de Pesquisa de Caixa de Correio e Retenção de Litígio sejam atribuídas diretamente ou por meio de associação em um grupo de funções que tem ambas as funções atribuídas. Para criar um Bloqueio In-loco sem usar uma consulta, que coloca todos os itens de caixa de correio em retenção, você deve ter a função Retenção de Litígio atribuída. O grupo de funções de Gerenciamento de Descoberta é atribuído a ambas as funções.<BR>O grupo de funções de Gerenciamento de Organização é atribuído à função Retenção de Litígio. Os membros do grupo de funções de Gerenciamento de Organização podem colocar um Bloqueio In-loco em todos os itens de uma caixa de correio, mas não podem criar um Bloqueio In-loco baseado em consulta.


</td>
</tr>
<tr class="even">
<td><p>Arquivo Morto In-loco</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gerenciamento da Organização</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Gerenciamento de Destinatários</a></p></td>
</tr>
<tr class="odd">
<td><p>Arquivo Morto In-loco –Testar conectividade</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gerenciamento da Organização</a></p>
<p><a href="server-management-exchange-2013-help.md">Gerenciamento de Servidor</a></p></td>
</tr>
<tr class="even">
<td><p>Configuração de Gerenciamento de Direitos de Informação (IRM)</p></td>
<td><p><a href="compliance-management-exchange-2013-help.md">Gerenciamento de Conformidade</a></p>
<p><a href="organization-management-exchange-2013-help.md">Gerenciamento da Organização</a></p></td>
</tr>
<tr class="odd">
<td><p>Políticas de retenção – Aplicar</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gerenciamento da Organização</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Gerenciamento de Destinatários</a></p>
<p><a href="records-management-exchange-2013-help.md">Gerenciamento de Registros</a></p></td>
</tr>
<tr class="even">
<td><p>Políticas de retenção – Criar</p></td>
<td><p>Consulte a entrada do Gerenciamento de Registros de Mensagens</p></td>
</tr>
<tr class="odd">
<td><p>Regras de transporte</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gerenciamento da Organização</a></p>
<p><a href="records-management-exchange-2013-help.md">Gerenciamento de Registros</a></p></td>
</tr>
</tbody>
</table>

