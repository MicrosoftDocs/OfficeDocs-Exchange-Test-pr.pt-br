---
title: 'Permissões de dispositivos móveis e clientes: Exchange 2013 Help'
TOCTitle: Permissões de dispositivos móveis e clientes
ms:assetid: 57eca42a-5a7f-4c65-89f0-7a84f2dbea19
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Dd638131(v=EXCHG.150)
ms:contentKeyID: 50485645
ms.date: 01/10/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Permissões de dispositivos móveis e clientes

 

_**Aplica-se a:**Exchange Server 2013_

_**Tópico modificado em:**2015-11-10_

As permissões necessárias à execução de tarefas para dispositivos móveis e clientes variam de acordo com o procedimento realizado ou o cmdlet que você deseja executar. Para saber mais sobre recursos para dispositivos móveis e clientes, confira [Clientes e dispositivos móveis](clients-and-mobile-exchange-2013-help.md).

Para descobrir de que permissões você precisa para executar o procedimento ou executar o cmdlet, faça o seguinte:

1.  Na tabela abaixo, localize o recurso que esteja melhor relacionado ao procedimento que você deseja seguir ou ao cmdlet que você deseja executar.

2.  Depois, examine as permissões necessárias para o recurso. Você deve ter sido atribuído a um desses grupos de funções, um grupo de funções personalizado equivalente ou uma função de gerenciamento equivalente. Você também podem clicar em um grupo de funções para ver suas funções de gerenciamento. Se um recurso listar mais de um grupo de funções, você só precisa ter um dos grupos de funções para usar o recurso. Para obter mais informações sobre as funções de gerenciamento e os grupos de funções, confira [Controle de acesso baseado em função de compreensão](understanding-role-based-access-control-exchange-2013-help.md).

3.  Agora, execute o cmdlet **Get-ManagementRoleAssignment** para examinar os grupos de funções ou funções de gerenciamento atribuídas a você, para ver se você tem as permissões necessárias para gerenciar o recurso.
    

    > [!TIP]
    > A função de gerenciamento Gerenciamento de Funções deve sido atribuída a você, para que você possa executar o cmdlet <STRONG>Get-ManagementRoleAssignment</STRONG>. Se você não tiver as permissões para executar o cmdlet <STRONG>Get-ManagementRoleAssignment</STRONG>, peça ao seu administrador do Exchange para recuperar os grupos de funções ou funções de gerenciamento atribuídas a você.



Se você quiser delegar, a outro usuário, a habilidade para gerenciar um recurso, confira [Atribuições de função de representante](delegate-role-assignments-exchange-2013-help.md).


> [!TIP]
> Alguns recursos podem exigir que você tenha permissões de administrador local no servidor que você quer gerenciar. Para gerenciar esses recursos, você deve ser membro do grupo Administradores Locais no servidor.



## Permissões de servidor Acesso para Cliente

É possível configurar qualquer um dos seguintes recursos para o servidor Acesso para Cliente.

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
<td><p>Configurações de matriz de servidor Acesso para Cliente</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gerenciamento da Organização</a></p>
<p><a href="server-management-exchange-2013-help.md">Gerenciamento de Servidor</a></p></td>
</tr>
<tr class="even">
<td><p>Configurações de servidor Acesso para Cliente</p></td>
<td><p><a href="server-management-exchange-2013-help.md">Gerenciamento de Servidor</a></p></td>
</tr>
<tr class="odd">
<td><p>Configurações de canal de email do serviço Acesso para Cliente</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gerenciamento da Organização</a></p>
<p><a href="server-management-exchange-2013-help.md">Gerenciamento de Servidor</a></p></td>
</tr>
<tr class="even">
<td><p>Configurações de usuário de Acesso para Cliente</p></td>
<td><p><a href="server-management-exchange-2013-help.md">Gerenciamento de Servidor</a></p></td>
</tr>
<tr class="odd">
<td><p>Configurações do diretório virtual de Acesso para Cliente</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gerenciamento da Organização</a></p>
<p><a href="server-management-exchange-2013-help.md">Gerenciamento de Servidor</a></p></td>
</tr>
<tr class="even">
<td><p>Configurações de Acesso para Cliente RPC</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gerenciamento da Organização</a></p>
<p><a href="server-management-exchange-2013-help.md">Gerenciamento de Servidor</a></p>
<p><a href="view-only-organization-management-exchange-2013-help.md">Gerenciamento da organização somente exibição</a></p></td>
</tr>
<tr class="odd">
<td><p>Configurações de proxy para notificação por push</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gerenciamento da Organização</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Gerenciamento de Destinatários</a></p></td>
</tr>
<tr class="even">
<td><p>Configurações de redirecionamento de autenticação OAuth</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gerenciamento da Organização</a></p></td>
</tr>
</tbody>
</table>


## Permissões do Exchange ActiveSync

É possível configurar qualquer um dos seguintes valores para Exchange ActiveSync.

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
<td><p>Configurações de bloqueio automático do Exchange ActiveSync</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gerenciamento da Organização</a></p></td>
</tr>
<tr class="even">
<td><p>Configurações de diretiva de caixa de correio do Exchange ActiveSync</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gerenciamento da Organização</a></p>
<p><a href="server-management-exchange-2013-help.md">Gerenciamento de Servidor</a></p></td>
</tr>
<tr class="odd">
<td><p>Configurações de servidor do Exchange ActiveSync</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gerenciamento da Organização</a></p>
<p><a href="server-management-exchange-2013-help.md">Gerenciamento de Servidor</a></p></td>
</tr>
<tr class="even">
<td><p>Configurações do Exchange ActiveSync</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gerenciamento da Organização</a></p>
<p><a href="server-management-exchange-2013-help.md">Gerenciamento de Servidor</a></p></td>
</tr>
<tr class="odd">
<td><p>Configurações de usuário do Exchange ActiveSync</p></td>
<td><p><a href="recipient-management-exchange-2013-help.md">Gerenciamento de Destinatários</a></p></td>
</tr>
<tr class="even">
<td><p>Configurações do diretório virtual do Exchange ActiveSync</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gerenciamento da Organização</a></p>
<p><a href="server-management-exchange-2013-help.md">Gerenciamento de Servidor</a></p></td>
</tr>
<tr class="odd">
<td><p>Configurações de política de caixa de correio do dispositivo móvel</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gerenciamento da Organização</a></p>
<p><a href="server-management-exchange-2013-help.md">Gerenciamento de Servidor</a></p></td>
</tr>
<tr class="even">
<td><p>Configurações de usuário do dispositivo móvel</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gerenciamento da Organização</a></p>
<p><a href="server-management-exchange-2013-help.md">Gerenciamento de Servidor</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Gerenciamento de Destinatários</a></p></td>
</tr>
</tbody>
</table>


## Permissões de Descoberta Automática

Você pode configurar o seguinte para o serviço de Descoberta Automática.

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
<td><p>Definições de configuração do serviço de Descoberta Automática</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gerenciamento da Organização</a></p>
<p><a href="server-management-exchange-2013-help.md">Gerenciamento de Servidor</a></p>
<p><a href="view-only-organization-management-exchange-2013-help.md">Gerenciamento da organização somente exibição</a></p>
<p><a href="delegated-setup-exchange-2013-help.md">Configuração Delegada</a></p>
<p><a href="hygiene-management-exchange-2013-help.md">Gerenciamento de Higienização</a></p></td>
</tr>
<tr class="even">
<td><p>Configurações do diretório virtual de Descoberta Automática</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gerenciamento da Organização</a></p>
<p><a href="server-management-exchange-2013-help.md">Gerenciamento de Servidor</a></p></td>
</tr>
</tbody>
</table>


## Permissões do serviço de Disponibilidade

Você pode configurar o seguinte para o serviço de Disponibilidade.

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
<td><p>Configurações de espaço de endereço do serviço de Disponibilidade</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gerenciamento da Organização</a></p>
<p><a href="view-only-organization-management-exchange-2013-help.md">Gerenciamento da organização somente exibição</a></p></td>
</tr>
<tr class="even">
<td><p>Definições de configuração do serviço de Disponibilidade</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gerenciamento da Organização</a></p>
<p><a href="server-management-exchange-2013-help.md">Gerenciamento de Servidor</a></p>
<p><a href="view-only-organization-management-exchange-2013-help.md">Gerenciamento da organização somente exibição</a></p></td>
</tr>
</tbody>
</table>


## Permissões de limitação do cliente

Você pode configurar o seguinte para limitação do cliente.

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
<td><p>Configurações de limitação do cliente</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gerenciamento da Organização</a></p>
<p><a href="view-only-organization-management-exchange-2013-help.md">Gerenciamento da organização somente exibição</a></p></td>
</tr>
</tbody>
</table>


## Permissões de Serviços Web do Exchange

Você pode configurar o seguinte para diretórios virtuais dos Serviços Web.

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
<td><p>As configurações do diretório virtual de Serviços Web do Exchange</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gerenciamento da Organização</a></p>
<p><a href="server-management-exchange-2013-help.md">Gerenciamento de Servidor</a></p></td>
</tr>
<tr class="even">
<td><p>Testar Serviços Web do Exchange</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gerenciamento da Organização</a></p>
<p><a href="server-management-exchange-2013-help.md">Gerenciamento de Servidor</a></p></td>
</tr>
<tr class="odd">
<td><p>Testar Serviços Web do Outlook</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gerenciamento da Organização</a></p></td>
</tr>
</tbody>
</table>


## Permissões do Outlook em Qualquer Lugar

Você pode configurar e gerenciar as configurações a seguir para o Outlook em Qualquer Lugar.

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
<td><p>Configuração do Outlook em Qualquer Lugar (habilitar, desabilitar, alterar, exibir)</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gerenciamento da Organização</a></p>
<p><a href="server-management-exchange-2013-help.md">Gerenciamento de Servidor</a></p>
<p><a href="view-only-organization-management-exchange-2013-help.md">Gerenciamento da organização somente exibição</a></p>
<p><a href="delegated-setup-exchange-2013-help.md">Configuração Delegada</a></p>
<p><a href="hygiene-management-exchange-2013-help.md">Gerenciamento de Higienização</a></p></td>
</tr>
<tr class="even">
<td><p>RPC sobre componente proxy HTTP</p></td>
<td><p>Administrador de Servidor Local</p></td>
</tr>
<tr class="odd">
<td><p>Testar a conectividade do Outlook em Qualquer Lugar</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gerenciamento da Organização</a></p>
<p><a href="view-only-organization-management-exchange-2013-help.md">Gerenciamento da organização somente exibição</a></p>
<p><a href="server-management-exchange-2013-help.md">Gerenciamento de Servidor</a></p></td>
</tr>
</tbody>
</table>


## Permissões do Outlook Web App

Você pode usar os seguintes recursos para exibir as configurações do Outlook Web App, controlar a segurança e o acesso do usuário ao Outlook Web App e testar a conectividade do Outlook Web App.

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
<td><p>Editor de elementos gráficos</p></td>
<td><p>Administrador de Servidor Local</p></td>
</tr>
<tr class="even">
<td><p>Gerenciador do IIS</p></td>
<td><p>Administrador de Servidor Local</p></td>
</tr>
<tr class="odd">
<td><p>ISA Server 2006</p></td>
<td><p>Administrador de Empresas do ISA Server</p></td>
</tr>
<tr class="even">
<td><p>diretivas de caixa de correio do Outlook Web App</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gerenciamento da Organização</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Gerenciamento de Destinatários</a></p></td>
</tr>
<tr class="odd">
<td><p>Diretórios virtuais do Outlook Web App</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gerenciamento da Organização</a></p>
<p><a href="server-management-exchange-2013-help.md">Gerenciamento de Servidor</a></p></td>
</tr>
<tr class="even">
<td><p>Editor do Registro</p></td>
<td><p>Administrador de Servidor Local</p></td>
</tr>
<tr class="odd">
<td><p>Configuração S/MIME</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gerenciamento da Organização</a></p></td>
</tr>
<tr class="even">
<td><p>Editor de texto</p></td>
<td><p>Administrador de Servidor Local</p></td>
</tr>
<tr class="odd">
<td><p>Exibir diretivas de caixa de correio do Outlook Web App</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gerenciamento da Organização</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Gerenciamento de Destinatários</a></p>
<p><a href="view-only-organization-management-exchange-2013-help.md">Gerenciamento da organização somente exibição</a></p>
<p><a href="delegated-setup-exchange-2013-help.md">Configuração Delegada</a></p>
<p><a href="hygiene-management-exchange-2013-help.md">Gerenciamento de Higienização</a></p></td>
</tr>
</tbody>
</table>


## Permissões de POP3 e IMAP4

Você pode configurar o seguinte para POP3 e IMAP4.

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
<td><p>Configurações de IMAP4</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gerenciamento da Organização</a></p>
<p><a href="server-management-exchange-2013-help.md">Gerenciamento de Servidor</a></p>
<p><a href="view-only-organization-management-exchange-2013-help.md">Gerenciamento da organização somente exibição</a></p></td>
</tr>
<tr class="even">
<td><p>Configurações de POP3</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gerenciamento da Organização</a></p>
<p><a href="server-management-exchange-2013-help.md">Gerenciamento de Servidor</a></p>
<p><a href="view-only-organization-management-exchange-2013-help.md">Gerenciamento da organização somente exibição</a></p></td>
</tr>
<tr class="odd">
<td><p>Testar as configurações de IMAP4</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gerenciamento da Organização</a></p>
<p><a href="server-management-exchange-2013-help.md">Gerenciamento de Servidor</a></p>
<p><a href="view-only-organization-management-exchange-2013-help.md">Gerenciamento da organização somente exibição</a></p></td>
</tr>
<tr class="even">
<td><p>Testar as configurações de POP3</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gerenciamento da Organização</a></p>
<p><a href="server-management-exchange-2013-help.md">Gerenciamento de Servidor</a></p>
<p><a href="view-only-organization-management-exchange-2013-help.md">Gerenciamento da organização somente exibição</a></p></td>
</tr>
</tbody>
</table>


## Permissões do diretório virtual do Windows PowerShell

Você pode configurar o seguinte para o Windows PowerShell.

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
<td><p>Testar o Windows PowerShell</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gerenciamento da Organização</a></p></td>
</tr>
<tr class="even">
<td><p>Configurações do Windows PowerShell</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Gerenciamento da Organização</a></p></td>
</tr>
</tbody>
</table>


## Permissões de mensagens de texto

Você pode configurar o seguinte para mensagens de texto.

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
<td><p>Configurações de notificação de mensagens de texto</p></td>
<td><p><a href="recipient-management-exchange-2013-help.md">Gerenciamento de Destinatários</a></p></td>
</tr>
<tr class="even">
<td><p>Configurações de mensagens de texto</p></td>
<td><p><a href="recipient-management-exchange-2013-help.md">Gerenciamento de Destinatários</a></p></td>
</tr>
<tr class="odd">
<td><p>Configurações de usuário de mensagens de texto</p></td>
<td><p><a href="mytextmessaging-role-exchange-2013-help.md">Função MyTextMessaging</a></p>
<p>Os usuários podem definir as configurações de mensagens de texto em suas próprias caixas de correio. Os administradores não podem definir as configurações de mensagens de texto na caixa de correio de outro usuário.</p></td>
</tr>
</tbody>
</table>

