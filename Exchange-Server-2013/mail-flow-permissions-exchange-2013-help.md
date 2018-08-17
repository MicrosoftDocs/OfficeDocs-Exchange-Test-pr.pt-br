---
title: 'Permissões de fluxo de email: Exchange 2013 Help'
TOCTitle: Permissões de fluxo de email
ms:assetid: f49f4fb5-af75-43cb-900f-c5f7b8cfa143
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Dd638213(v=EXCHG.150)
ms:contentKeyID: 50487005
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Permissões de fluxo de email

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2016-12-09_

As permissões necessárias para executar tarefas relacionadas a fluxo de email variam dependendo do procedimento que está sendo executado ou o cmdlet que você deseja executar. Para mais informações sobre os recursos de transporte, consulte [Fluxo de mensagens](mail-flow-exchange-2013-help.md).

Este tópico lista as permissões necessárias para gerenciar os recursos de fluxo de email do Microsoft Exchange Server 2013. Para obter informações sobre como o Office 365 permissões se relacionam com permissões do Exchange, consulte [permissões no Office 365](https://go.microsoft.com/fwlink/p/?linkid=335814).

Para descobrir de que permissões você precisa para executar o procedimento ou executar o cmdlet, faça o seguinte:

1.  Na tabela abaixo, localize o recurso que esteja melhor relacionado ao procedimento que você deseja seguir ou ao cmdlet que você deseja executar.

2.  Depois, examine as permissões necessárias para o recurso. Você deve ter sido atribuído a um desses grupos de funções, um grupo de funções personalizado equivalente ou uma função de gerenciamento equivalente. Você também podem clicar em um grupo de funções para ver suas funções de gerenciamento. Se um recurso listar mais de um grupo de funções, você só precisa ter um dos grupos de funções para usar o recurso. Para obter mais informações sobre as funções de gerenciamento e os grupos de funções, confira [Controle de acesso baseado em função de compreensão](understanding-role-based-access-control-exchange-2013-help.md).

3.  Agora, execute o cmdlet **Get-ManagementRoleAssignment** para examinar os grupos de funções ou funções de gerenciamento atribuídas a você, para ver se você tem as permissões necessárias para gerenciar o recurso.
    

    > [!NOTE]
    > A função de gerenciamento Gerenciamento de Funções deve sido atribuída a você, para que você possa executar o cmdlet <STRONG>Get-ManagementRoleAssignment</STRONG>. Se você não tiver as permissões para executar o cmdlet <STRONG>Get-ManagementRoleAssignment</STRONG>, peça ao seu administrador do Exchange para recuperar os grupos de funções ou funções de gerenciamento atribuídas a você.



Se você quiser delegar, a outro usuário, a habilidade para gerenciar um recurso, confira [Atribuições de função de representante](delegate-role-assignments-exchange-2013-help.md).


> [!NOTE]
> Pode haver, nos servidores de Transporte de Borda, alguns recursos que você queira gerenciar. Para gerenciar os recursos nos servidores de Transporte de Borda, você precisa se tornar um membro do grupo Administradores Locais, no servidor de Transporte de Borda que você deseja gerenciar. Servidores de Transporte de Borda não usam o Controle de Acesso Baseado na Função (RBAC). Os recursos que podem ser gerenciados nos servidores de Transporte de Borda têm Administrador Local de Transporte de Borda na coluna "Permissões necessárias" na tabela abaixo.




> [!NOTE]
> Alguns recursos podem exigir que você tenha permissões de administrador local no servidor que você quer gerenciar. Para gerenciar esses recursos, você deve ser membro do grupo Administradores Locais no servidor.



## Permissões de fluxo de email

Você pode usar os recursos nas seguintes tabelas para definir as configurações de fluxo de email no serviço de Transporte de Front-End nos servidores de Acesso para Cliente, no serviço de Transporte em servidores de Caixa de Correio, no serviço de Transporte de Caixa de Correio em servidores de Caixa de Correio e em servidores de Transporte de Borda. As permissões necessárias para configurar cada recurso estão listadas.

Os usuários atribuídos ao grupo de funções Gerenciamento Somente para Exibição podem visualizar a configuração dos recursos mostrados na tabela a seguir. Para mais informações, consulte [Gerenciamento da organização somente exibição](view-only-organization-management-exchange-2013-help.md).

**Servidores de Caixa de Correio e servidores de Acesso para Cliente**


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Feature</th>
<th>Permissões necessárias</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Domínios aceitos</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gerenciamento da Organização</a></p></td>
</tr>
<tr class="even">
<td><p>Site do Active Directory e gerenciamento do link do site</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gerenciamento da Organização</a></p></td>
</tr>
<tr class="odd">
<td><p>Recursos anti-spam</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gerenciamento da Organização</a></p>
<p><a href="hygiene-management-exchange-2013-help.md">Gerenciamento de Higienização</a></p></td>
</tr>
<tr class="even">
<td><p>Atualizações de anti-spam</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gerenciamento da Organização</a></p>
<p><a href="hygiene-management-exchange-2013-help.md">Gerenciamento de Higienização</a></p></td>
</tr>
<tr class="odd">
<td><p>Gerenciamento de certificados</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gerenciamento da Organização</a></p></td>
</tr>
<tr class="even">
<td><p>Conectores de Agente de Entrega</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gerenciamento da Organização</a></p>
<p><a href="server-management-exchange-2013-help.md">Gerenciamento de Servidor</a></p></td>
</tr>
<tr class="odd">
<td><p>DSNs</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gerenciamento da Organização</a></p></td>
</tr>
<tr class="even">
<td><p>EdgeSync</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gerenciamento da Organização</a></p></td>
</tr>
<tr class="odd">
<td><p>Conectores externos</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gerenciamento da Organização</a></p></td>
</tr>
<tr class="even">
<td><p>Serviço de Transporte de Front End</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gerenciamento da Organização</a></p>
<p><a href="server-management-exchange-2013-help.md">Gerenciamento de Servidor</a></p>
<p><a href="hygiene-management-exchange-2013-help.md">Gerenciamento de Higienização</a></p></td>
</tr>
<tr class="odd">
<td><p>Registro no Diário</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gerenciamento da Organização</a></p>
<p><a href="records-management-exchange-2013-help.md">Gerenciamento de Registros</a></p></td>
</tr>
<tr class="even">
<td><p>Acesso à caixa de correio</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gerenciamento da Organização</a></p></td>
</tr>
<tr class="odd">
<td><p>Configuração de lixo eletrônico de caixa de correio</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gerenciamento da Organização</a></p>
<p><a href="records-management-exchange-2013-help.md">Gerenciamento de Registros</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Gerenciamento de Destinatários</a></p>
<p><a href="help-desk-exchange-2013-help.md">Suporte Técnico</a></p></td>
</tr>
<tr class="even">
<td><p>Serviço de Transporte de Caixa de Correio</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gerenciamento da Organização</a></p>
<p><a href="server-management-exchange-2013-help.md">Gerenciamento de Servidor</a></p>
<p><a href="hygiene-management-exchange-2013-help.md">Gerenciamento de Higienização</a></p></td>
</tr>
<tr class="odd">
<td><p>Dicas de Email</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gerenciamento da Organização</a></p></td>
</tr>
<tr class="even">
<td><p>Classificações de mensagem</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gerenciamento da Organização</a></p>
<p><a href="records-management-exchange-2013-help.md">Gerenciamento de Registros</a></p></td>
</tr>
<tr class="odd">
<td><p>Controle de mensagens</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gerenciamento da Organização</a></p>
<p><a href="records-management-exchange-2013-help.md">Gerenciamento de Registros</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Gerenciamento de Destinatários</a></p></td>
</tr>
<tr class="even">
<td><p>Transporte moderado</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gerenciamento da Organização</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Gerenciamento de Destinatários</a></p></td>
</tr>
<tr class="odd">
<td><p>Filas</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gerenciamento da Organização</a></p>
<p><a href="server-management-exchange-2013-help.md">Gerenciamento de Servidor</a></p></td>
</tr>
<tr class="even">
<td><p>Conectores de recebimento</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gerenciamento da Organização</a></p>
<p><a href="server-management-exchange-2013-help.md">Gerenciamento de Servidor</a></p>
<p><a href="hygiene-management-exchange-2013-help.md">Gerenciamento de Higienização</a></p></td>
</tr>
<tr class="odd">
<td><p>Domínios remotos</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gerenciamento da Organização</a></p></td>
</tr>
<tr class="even">
<td><p>Agregação de Lista Segura</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gerenciamento da Organização</a></p>
<p><a href="records-management-exchange-2013-help.md">Gerenciamento de Registros</a></p></td>
</tr>
<tr class="odd">
<td><p>Conectores de envio</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gerenciamento da Organização</a></p></td>
</tr>
<tr class="even">
<td><p>Redundância de sombra</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gerenciamento da Organização</a></p></td>
</tr>
<tr class="odd">
<td><p>Testando o fluxo de emails</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gerenciamento da Organização</a></p>
<p><a href="server-management-exchange-2013-help.md">Gerenciamento de Servidor</a></p></td>
</tr>
<tr class="even">
<td><p>Testando o processamento da regra de Transporte</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gerenciamento da Organização</a></p></td>
</tr>
<tr class="odd">
<td><p>Agentes de transporte</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gerenciamento da Organização</a></p>
<p><a href="records-management-exchange-2013-help.md">Gerenciamento de Registros</a></p></td>
</tr>
<tr class="even">
<td><p>Configuração de transporte</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gerenciamento da Organização</a></p></td>
</tr>
<tr class="odd">
<td><p>Logs de transporte</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gerenciamento da Organização</a></p>
<p><a href="server-management-exchange-2013-help.md">Gerenciamento de Servidor</a></p></td>
</tr>
<tr class="even">
<td><p>Regras de transporte</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gerenciamento da Organização</a></p>
<p><a href="records-management-exchange-2013-help.md">Gerenciamento de Registros</a></p></td>
</tr>
<tr class="odd">
<td><p>Serviço de Transporte</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gerenciamento da Organização</a></p>
<p><a href="server-management-exchange-2013-help.md">Gerenciamento de Servidor</a></p>
<p><a href="hygiene-management-exchange-2013-help.md">Gerenciamento de Higienização</a></p></td>
</tr>
<tr class="even">
<td><p>Domínios X.400</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gerenciamento da Organização</a></p></td>
</tr>
</tbody>
</table>


**Servidores de Transporte de Borda**


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Feature</th>
<th>Permissões obrigatórias</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Domínios aceitos - Transporte de Borda</p></td>
<td><p>Administrador Local de Transporte de Borda</p></td>
</tr>
<tr class="even">
<td><p>Reconfiguração de endereço - Transporte de Borda</p></td>
<td><p>Administrador Local de Transporte de Borda</p></td>
</tr>
<tr class="odd">
<td><p>Servidor de Transporte de Borda</p></td>
<td><p>Administrador Local de Transporte de Borda</p></td>
</tr>
<tr class="even">
<td><p>EdgeSync - Transporte de Borda</p></td>
<td><p>Administrador Local de Transporte de Borda</p></td>
</tr>
<tr class="odd">
<td><p>Filas - Transporte de Borda</p></td>
<td><p>Administrador Local de Transporte de Borda</p></td>
</tr>
<tr class="even">
<td><p>Conectores de recebimento - Transporte de Borda</p></td>
<td><p>Administrador Local de Transporte de Borda</p></td>
</tr>
<tr class="odd">
<td><p>Conectores de envio - Transporte de Borda</p></td>
<td><p>Administrador Local de Transporte de Borda</p></td>
</tr>
<tr class="even">
<td><p>Configuração de transporte - Transporte de Borda</p></td>
<td><p>Administrador Local de Transporte de Borda</p></td>
</tr>
<tr class="odd">
<td><p>Logs de transporte - Transporte de Borda</p></td>
<td><p>Administrador Local de Transporte de Borda</p></td>
</tr>
<tr class="even">
<td><p>Regras de Transporte - Transporte de Borda</p></td>
<td><p>Administrador Local de Transporte de Borda</p></td>
</tr>
</tbody>
</table>

