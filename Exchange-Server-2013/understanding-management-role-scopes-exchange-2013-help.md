---
title: 'Noções básicas sobre escopos da função de gerenciamento: Exchange 2013 Help'
TOCTitle: Noções básicas sobre escopos da função de gerenciamento
ms:assetid: 24ed4a38-438a-4223-9f9c-5d4dea4b046b
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Dd335146(v=EXCHG.150)
ms:contentKeyID: 50485158
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Noções básicas sobre escopos da função de gerenciamento

 

_**Aplica-se a:** Exchange Online, Exchange Server 2013_

_**Tópico modificado em:** 2015-04-07_

Os *Escopos de função de gerenciamento* permitem que você defina o escopo específico do impacto ou da influência de uma função de gerenciamento quando uma atribuição de função de gerenciamento é criada. Quando você aplica um escopo, o destinatário da função pode apenas modificar os objetos contidos nesse escopo. O destinatário da função pode ser um grupo de função de gerenciamento, uma diretiva de atribuição de gerenciamento de função, um usuário ou um USG (grupo de segurança universal). Para mais informações sobre funções de gerenciamento, consulte [Controle de acesso baseado em função de compreensão](understanding-role-based-access-control-exchange-2013-help.md).


> [!TIP]
> Este tópico concentra-se na funcionalidade avançada de RBAC. Se você quiser gerenciar permissões básicas do Exchange 2013, como usar o Centro de Administração do Exchange (EAC) para adicionar e remover membros de grupos de funções, criar e modificar grupos de funções ou criar e modificar políticas de atribuição de função, consulte <A href="permissions-exchange-2013-help.md">Permissões</A>.



Cada função de gerenciamento, se ele é uma função incorporada ou uma função personalizada, tem escopos de gerenciamento. Escopos de gerenciamento podem ser um dos seguintes:

  - **Regular**   Um *escopo regular* não é exclusivo. Ele determina onde, no Active Directory, os objetos podem ser exibidos ou modificados por usuários destinatários da função de gerenciamento. Em geral, uma função de gerenciamento indica o que você pode criar ou modificar e um escopo de função de gerenciamento indica onde você pode criar ou modificar. Os escopos regulares podem ser implícitos ou explícitos - ambos serão discutidos adiante, neste tópico.

  - **Exclusivo**   Um *escopo exclusivo* comporta-se praticamente como um escopo regular. A diferença principal é que ele permite que você impeça que usuários acessem os objetos contidos dentro do escopo exclusivo, se esses usuários não forem os destinatários de uma função associada ao escopo exclusivo. Todos os escopos exclusivos são explícitos, e serão discutidos adiante, neste tópico.
    
    Para mais informações sobre escopos exclusivos, consulte [Noções básicas sobre escopos exclusivos](understanding-exclusive-scopes-exchange-2013-help.md).

Os escopos podem ser herdados da função de gerenciamento, especificados como um escopo relativo predefinido em uma atribuição de função de gerenciamento ou criados através de filtros personalizados em adicionados a uma atribuição de função de gerenciamento. Os escopos herdados de funções de gerenciamento são chamados *escopos implícitos*, enquanto escopos predefinidos e personalizados são chamados de *escopos explícitos*. As seções a seguir descrevem os tipos de escopo:

  - Implicit Scopes

  - Explicit Scopes

  - Predefined Relative Scopes

  - Custom Scopes
    
      - Recipient Filter Scopes
    
      - Configuration Scopes

Cada função pode ter os seguintes tipos de escopos:

  - **Escopo de leitura do destinatário**   O escopo implícito de leitura do destinatário determina quais objetos de destinatário o destinatário da função de gerenciamento terá permissão para ler do Active Directory.

  - **Escopo de gravação do destinatário**   O escopo implícito de gravação do destinatário determina quais objetos de destinatário o destinatário da função de gerenciamento terá permissão para modificar no Active Directory.

  - **Escopo de leitura de configuração**   O escopo implícito de leitura da configuração determina quais objetos de destinatário o destinatário da função de gerenciamento terá permissão para ler do Active Directory.

  - **Escopo de gravação de configuração**   O escopo de gravação de configuração implícito determina quais objetos de servidor, de banco de dados e organizacionais o destinatário da função de gerenciamento terá permissão para modificar no Active Directory.

Objetos de destinatário incluem caixas de correio, grupos de distribuição, os usuários habilitadas para email e outros objetos. Objetos de configuração incluem os servidores que executam o Microsoft Exchange Server 2013 e bancos de dados localizados em servidores executando o Exchange. Cada tipo de escopo pode ser um escopo explícito ou implícito escopo.

## Escopos implícitos

Os escopos implícitos são os escopos-padrão que se aplicam a um tipo de função de gerenciamento. Como os escopos implícitos são associados a um tipo de função de gerenciamento, todas as funções de gerenciamento mães e filhas com o mesmo tipo de função também terão os mesmos escopos implícitos. Os escopos implícitos se aplicam tanto a funções de gerenciamento internas quanto a funções de gerenciamento personalizadas. Para mais informações sobre as funções de gerenciamento e tipos de função de gerenciamento, consulte [Noções básicas sobre funções de gerenciamento](understanding-management-roles-exchange-2013-help.md).

As tabelas a seguir listam todos os escopos implícitos que podem ser definidos em funções de gerenciamento.

### Escopos implícitos definidos nas funções de gerenciamento

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Escopos implícitos</th>
<th>Descrição</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code>Organization</code></p></td>
<td><p>Se <code>Organization</code> estiver presente no escopo de gravação do destinatário da função, essa função pode criar ou modificar objetos de destinatário pela organização do Exchange.</p>
<p>Se <code>Organization</code> estiver presente no escopo de leitura do destinatário da função, essa função pode exibir quaisquer objetos de destinatário pela organização do Exchange.</p>
<p>Esse escopo é usado somente com os escopos de leitura e gravação do destinatário.</p></td>
</tr>
<tr class="even">
<td><p><code>MyGAL</code></p></td>
<td><p>Se <code>MyGAL</code> estiver presente no escopo de gravação do destinatário da função, essa função pode exibir as propriedades de quaisquer destinatários dentro da lista de endereços global (GAL) do usuário atual.</p>
<p>Se <code>MyGAL</code> estiver presente no escopo de gravação do destinatário da função, essa função pode exibir as propriedades de quaisquer destinatários dentro da GAL atual.</p>
<p>Esse escopo é usado somente com os escopos de leitura de destinatário.</p></td>
</tr>
<tr class="odd">
<td><p><code>Self</code></p></td>
<td><p>Se <code>Self</code> estiver no escopo de gravação do destinatário da função, a função poderá modificar somente as propriedades da caixa de correio do usuário atual.</p>
<p>Se <code>Self</code> estiver no escopo de leitura do destinatário da função, a função poderá exibir somente as propriedades da caixa de correio do usuário atual.</p>
<p>Esse escopo é usado somente com os escopos de leitura e gravação do destinatário.</p></td>
</tr>
<tr class="even">
<td><p><code>MyDistributionGroups</code></p></td>
<td><p>Se <code>MyDistributionGroups</code> estiver presente no escopo de gravação do destinatário da função, essa função pode criar ou modificar objetos de lista de distribuição que sejam do usuário atual.</p>
<p>Se <code>MyDistributionGroups</code> estiver presente no escopo de leitura do destinatário da função, essa função pode exibir objetos de lista de distribuição que sejam do usuário atual.</p>
<p>Esse escopo é usado somente com os escopos de leitura e gravação do destinatário.</p></td>
</tr>
<tr class="odd">
<td><p><code>OrganizationConfig</code></p></td>
<td><p>Se <code>OrganizationConfig</code> estiver presente no escopo de gravação do destinatário da função, essa função poderá criar ou modificar quaisquer objetos de configuração de servidor ou banco de dados na organização do Exchange.</p>
<p>Se <code>OrganizationConfig</code> estiver presente no escopo de leitura de configuração da função, essa função poderá exibir quaisquer objetos de configuração de servidor ou banco de dados na organização do Exchange.</p>
<p>Esse escopo é usado somente com escopos de leitura e gravação de configuração.</p></td>
</tr>
<tr class="even">
<td><p><code>None</code></p></td>
<td><p>Se <code>None</code> estiver em um escopo, esse escopo não estará disponível para a função. Por exemplo, uma função que tenha <code>None</code> no escopo de gravação do destinatário não pode modificar os objetos de destinatário na organização do Exchange.</p></td>
</tr>
</tbody>
</table>


Se uma função for atribuída a um destinatário de função e nenhum escopo predefinido ou personalizado for especificado, os escopos implícitos definidos na função serão usados para controlar os objetos de destinatário ou organização que o usuário pode exibir ou modificar.

O escopo de gravação implícito de uma função é sempre igual a ou menor que o escopo de leitura implícito. Isso significa que uma função nunca pode modificar objetos que não podem ser vistos pelo escopo.

Não é possível alterar os escopos implícitos definidos nas funções de gerenciamento. Você pode, entretanto, ignorar o escopo de gravação implícito e o escopo de configuração em uma função de gerenciamento. Quando um escopo relativo predefinido ou personalizado é usado em uma atribuição de função, o escopo de gravação implícito da função é substituído, e o novo escopo prevalece. O escopo de leitura implícito de uma função não pode ser substituído e sempre se aplica. Para mais informações, consulte Predefined Relative Scopes e Custom Scopes.

Expanda a seguinte tabela para ver uma lista de todas as funções de gerenciamento integradas e seus escopos implícitos. Para obter mais informações sobre cada função integrada, consulte [Funções de gerenciamento internas](built-in-management-roles-exchange-2013-help.md).

## Escopos implícitos de funções de gerenciamento internas


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
<th>Função de gerenciamento</th>
<th>Escopo de leitura do destinatário</th>
<th>Escopo de gravação do destinatário</th>
<th>Escopo de leitura da configuração</th>
<th>Escopo de gravação do destinatário</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code>Active Directory Permissions</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>Address Lists</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>ApplicationImpersonation</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>None</code></p></td>
<td><p><code>None</code></p></td>
</tr>
<tr class="even">
<td><p><code>ArchiveApplication</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>Audit Logs</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>Cmdlet Extension Agents</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>Data Loss Prevention</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>Database Availability Groups</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>Database Copies</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>Databases</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>Disaster Recovery</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>Distribution Groups</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>Edge Subscriptions</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>E-Mail Address Policies</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>Exchange Connectors</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>Exchange Server Certificates</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>Exchange Servers</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>Exchange Virtual Directories</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>Federated Sharing</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>Information Rights Management</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>Journaling</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>Legal Hold</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>None</code></p></td>
</tr>
<tr class="odd">
<td><p><code>LegalHoldApplication</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>Mail Enabled Public Folders</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>Mail Recipient Creation</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>Mail Recipients</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>Mail Tips</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>Mailbox Import Export</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>Mailbox Search</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>None</code></p></td>
<td><p><code>None</code></p></td>
</tr>
<tr class="even">
<td><p><code>MailboxSearchApplication</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>Message Tracking</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>Migration</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>Monitoring</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>Move Mailboxes</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>OfficeExtensionApplication</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>My Custom Apps</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>My Marketplace Apps</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>MyAddressInformation</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>MyBaseOptions</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>MyContactInformation</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>MyDiagnostics</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>MyDisplayName</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>MyDistributionGroupMembership</code></p></td>
<td><p><code>MyGAL</code></p></td>
<td><p><code>MyGAL</code></p></td>
<td><p><code>None</code></p></td>
<td><p><code>None</code></p></td>
</tr>
<tr class="even">
<td><p><code>MyDistributionGroups</code></p></td>
<td><p><code>MyGAL</code></p></td>
<td><p><code>MyDistributionGroups</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>None</code></p></td>
</tr>
<tr class="odd">
<td><p><code>MyMobileInformation</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>MyName</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>MyPersonalInformation</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>MyProfileInformation</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>MyRetentionPolicies</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>MyTeamMailboxes</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>MyTextMessaging</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>MyVoiceMail</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>Organization Client Access</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>Organization Configuration</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>Organization Transport Settings</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>POP3 And IMAP4 Protocols</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>Public Folders</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>Receive Connectors</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>Recipient Policies</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>Remote and Accepted Domains</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>Reset Password</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>Retention Management</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>Role Management</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>Security Group Creation and Membership</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>Send Connectors</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>Support Diagnostics</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>TeamMailboxLifecycleApplication</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>Transport Agents</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>Transport Hygiene</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>Transport Queues</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>Transport Rules</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>UM Mailboxes</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>UM Prompts</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>Unified Messaging</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>UnScoped Role Management</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>UserApplication</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>User Options</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>View-Only Audit Logs</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>None</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>None</code></p></td>
</tr>
<tr class="odd">
<td><p><code>View-Only Configuration</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>None</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>None</code></p></td>
</tr>
<tr class="even">
<td><p><code>View-Only Recipients</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>None</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>None</code></p></td>
</tr>
<tr class="odd">
<td><p><code>WorkloadManagement</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
</tbody>
</table>


## Escopos explícitos

Os escopos explícitos são escopos que você mesmo define para controlar que objetos uma função de gerenciamento pode modificar. Embora os escopos implícitos sejam definidos em uma função de gerenciamento, os escopos explícitos são definidos em uma atribuição de função de gerenciamento. Isso permite que os escopos implícitos sejam aplicados consistentemente por todas as funções de gerenciamento, a menos que você escolha usar um escopo explícito de substituição. Para mais informações sobre as atribuições da função de gerenciamento, consulte [Noções básicas sobre as atribuições de função de gerenciamento](understanding-management-role-assignments-exchange-2013-help.md).

Os escopos explícitos substituem os escopos implícitos de gravação e configuração de uma função de gerenciamento. Eles não substituem o escopo de leitura implícito de uma função de gerenciamento. O escopo de leitura implícito continua a definir que objetos a função de gerenciamento pode ler.

Os escopos explícitos são úteis quando o escopo de gravação implícito de uma função de gerenciamento não cumpre as necessidades de seus negócios. Você pode adicionar um escopo explícito para incluir praticamente qualquer coisa que você queira, contanto que o novo escopo não exceda os limites do escopo de leitura implícito. Os cmdlets que são parte de uma função de gerenciamento devem poder ler informações sobre os objetos ou contêineres que contenham objetos para os cmdlets criarem ou modificarem objetos. Por exemplo, se o escopo de leitura implícito de uma função de gerenciamento estiver definido para `Self`, você não poderá adicionar um escopo de gravação explícito da `Organization`, porque o escopo de gravação explícito excede os limites do escopo de leitura implícito.

Para obter mais informações, consulte as seguintes seções:

  - Predefined Relative Scopes

  - Custom Scopes

## Escopos relativos predefinidos

Exchange 2013 fornece várias relativa predefinidos gravar escopos que você pode usar para modificar o escopo de uma função de gerenciamento. Escopos relativos predefinidos fornecem uma maneira fácil de fazer a correspondência de mais de perto as necessidades da sua empresa sem precisar criar escopos personalizados manualmente. São chamados escopos relativos porque eles estão em relação à qual a atribuição de função associada é atribuída o destinatário da função. Por exemplo, o escopo de relativa `Self` predefinidos restringe esse escopo de gravação apenas o usuário atual. O escopo de relativa `MyDistributionGroups` predefinidos restringe o escopo de gravação ao grupo de distribuição que o usuário atual possui apenas. Escopos relativos predefinidos só podem ser usados para objetos de destinatário do escopo. Escopos relativos predefinidos não podem ser usado para objetos de configuração do escopo. A tabela a seguir lista os escopos relativos predefinidos que podem ser usados.

### Escopos relativos predefinidos

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Escopos implícitos</th>
<th>Descrição</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code>Organization</code></p></td>
<td><p>Se <code>Organization</code> estiver presente no escopo de gravação do destinatário da função, essa função pode criar ou modificar objetos de destinatário pela organização do Exchange.</p>
<p>Se <code>Organization</code> estiver presente no escopo de leitura do destinatário da função, essa função pode exibir quaisquer objetos de destinatário pela organização do Exchange.</p>
<p>Esse escopo é usado somente com os escopos de leitura e gravação do destinatário.</p></td>
</tr>
<tr class="even">
<td><p><code>Self</code></p></td>
<td><p>Se <code>Self</code> estiver no escopo de gravação do destinatário da função, a função poderá modificar somente as propriedades da caixa de correio do usuário atual.</p>
<p>Se <code>Self</code> estiver no escopo de leitura do destinatário da função, a função poderá exibir somente as propriedades da caixa de correio do usuário atual.</p>
<p>Esse escopo é usado somente com os escopos de leitura e gravação do destinatário.</p></td>
</tr>
<tr class="odd">
<td><p><code>MyDistributionGroups</code></p></td>
<td><p>Se <code>MyDistributionGroups</code> estiver presente no escopo de gravação do destinatário da função, essa função pode criar ou modificar objetos de lista de distribuição que sejam do usuário atual.</p>
<p>Se <code>MyDistributionGroups</code> estiver presente no escopo de leitura do destinatário da função, essa função pode exibir objetos de lista de distribuição que sejam do usuário atual.</p>
<p>Esse escopo é usado somente com os escopos de leitura e gravação do destinatário.</p></td>
</tr>
</tbody>
</table>


Os escopos relativos predefinidos são aplicados quando você cria uma nova atribuição de função de gerenciamento. Durante a criação de uma atribuição de função, usando o cmdlet **New-ManagementRoleAssignment**, você pode especificar um escopo relativo predefinido usando o parâmetro *RecipientRelativeWriteScope*. Quando a nova atribuição de função é criada, a nova função predefinida substitui o escopo de gravação implícito da função de gerenciamento. Não é possível especificar um escopo de destinatário personalizado quando se cria uma atribuição de função com um escopo relativo predefinido. Entretanto, você poderá especificar um escopo de configuração personalizado, se necessário.

Para mais informações sobre como adicionar uma atribuição de função de gerenciamento com um escopo relativo predefinido, consulte [Adicionar uma função a um usuário ou USG](add-a-role-to-a-user-or-usg-exchange-2013-help.md).

## Escopos personalizados

Escopos personalizados são necessários quando nem o escopo de gravação implícita nem os escopos relativos predefinidos atenderem às necessidades dos seus negócios. Escopos personalizados permitem definir, em um nível granular, o escopo ao qual sua função de gerenciamento será aplicada. Por exemplo, convém direcionar um tipo específico de destinatário, uma unidade organizacional específica (OU) ou ambos. Ou então, você só deseja permitir que um grupo de administradores possam gerenciar um conjunto específico de bancos de dados de caixa de correio.

Assim como os escopos relativos predefinidos, os escopos personalizados substituem os escopos implícitos de gravação e configuração de organização definidos nas funções de gerenciamento. O escopo de leitura implícito nas funções de gerenciamento continua a se aplicar, e o escopo personalizado resultante não deve exceder os limites do escopo de leitura implícito. É possível criar os seguintes três tipos de escopos personalizados:

  - **Escopo da OU**   Um escopo da OU, que é o escopo personalizado mais simples, é criado com o uso do parâmetro *RecipientOrganizationalUnitScope* no cmdlet **New-ManagementRoleAssignment**. Especificando um escopo da OU quando uma função é atribuída, o destinatário da função atribuído á função pode modificar somente os objetos de destinatário dentro dessa OU. Para mais informações sobre como adicionar uma atribuição de função de gerenciamento com um escopo da OU, consulte [Adicionar uma função a um usuário ou USG](add-a-role-to-a-user-or-usg-exchange-2013-help.md).

  - **Escopo de filtro de destinatário**   Os escopos de filtro de destinatário usam filtros para focar destinatários específicos, com base no tipo de destinatário ou outras propriedades de destinatário, como departamento, gerente, local, dentre outros. Para obter mais informações, consulte a seção Recipient Filter Scopes.

  - **Escopo da configuração**   Escopos de configuração usam filtros ou listas para servidores de destino específicos com base em listas de servidores ou propriedades filtráveis que podem ser definidas nos servidores, como um site Active Directory ou uma função de servidor. Escopos de configuração também podem usar os escopos de banco de dados para bancos de dados específicos com base em listas de banco de dados ou propriedades filtráveis do banco de dados de destino. Para obter mais informações, consulte a seção de Configuração de escopos .

Escopos personalizados de destinatário e de configuração complexos e granulares simples e amplos podem ser criados com o uso do cmdlet **New-ManagementScope**. Quando você cria um escopo de destinatário ou configuração, somente os objetos de destinatário, servidor ou banco de dados que correspondam aos respectivos escopos filtrados são retornados. Quando esses escopos são aplicados a uma função de atribuição, usando os cmdlets **New-ManagementRoleAssignment** ou **Set-ManagementRoleAssignment**, somente os objetos que correspondam a esses escopos podem ser modificados pelos destinatários da função a quem a função foi atribuída. Após um escopo personalizado ter sido criado, você não pode alterar o tipo de escopo. Um escopo de destinatário é sempre um escopo de destinatário, e um escopo de configuração é sempre um escopo de configuração.

Por padrão, um escopo personalizado permite que um destinatário de função acessar um conjunto de objetos que coincidem com os escopos que você define. No entanto, eles não excluem ativamente acesso a outros os destinatários da função que não foram atribuídos também o escopo do mesmo ou equivalente. Qualquer escopo personalizado pode acessar os mesmos objetos se as listas ou os filtros desses escopos coincidir com os mesmos objetos. Pode haver objetos onde esse comportamento não desejava, tais como no caso de executivos. Para esses objetos, você pode definir escopos exclusivos. Escopos exclusivos usar filtros ou listas da mesma maneira como os escopos regulares mas diferentemente escopos regulares, negar acesso aos objetos incluídos no escopo para qualquer pessoa que não fazem parte do escopo exclusivo mesmo ou equivalente. Para obter mais informações sobre escopos exclusivos, consulte [Noções básicas sobre escopos exclusivos](understanding-exclusive-scopes-exchange-2013-help.md).

## Escopos de filtro de destinatário

Os escopos de filtro de destinatário permitem controlar quais destinatários de função de objetos de destinatário podem ser gerenciados pela avaliação de uma ou mais propriedades em objeto de destinatário em relação a um valor especificado em uma instrução de filtro. Os destinatários incluídos nos escopos de destinatário são caixas de correio, usuários habilitados para email, grupos de distribuição e contatos de email. Somente os destinatários que correspondam ao filtro especificado podem ser gerenciados pelos destinatários de função com essa atribuição de função. Um exemplo de instrução de filtro é `{ Name -Eq "David" }`, em que **Name** é a propriedade no objeto de destinatário sendo avaliada, e **David**, o valor que deseja avaliar em relação à propriedade. O operador de comparação **-Eq** indica que o valo armazenado na propriedade deve ser igual ao especificado para que o filtro seja verdadeiro. Se o filtro for verdadeiro, esse destinatário será incluído no escopo.

Os escopos de filtro de destinatário são criados com a especificação do filtro de destinatário a ser usado com o parâmetro *RecipientRestrictionFilter* no cmdlet **New-ManagementScope**. Por padrão, o cmdlet **New-ManagementScope** cria escopos regulares. Se quiser criar um escopo exclusivo, inclua o switch *Exclusive* junto com o parâmetro *RecipientRestrictionFilter*.

Quando você cria um filtro de restrição de destinatário, o Exchange avalia o filtro fornecido em relação a qualquer objeto de destinatário na organização por padrão. Se quiser limitar quais destinatários o escopo avalia, você poderá usar o parâmetro *RecipientRoot* junto com o parâmetro *RecipientRestrictionFilter*. O parâmetro *RecipientRoot* aceita uma OU. Quando se utiliza o parâmetro *RecipientRoot*, o Exchange avalia apenas os destinatários incluídos na OU especificada em relação ao filtro fornecido.

Ao adicionar um escopo de filtro de destinatário a uma atribuição de função, especifique o nome do escopo do destinatário no parâmetro *CustomRecipientWriteScope* em **New-ManagementRoleAssignment** se estiver criando uma nova atribuição de função ou no cmdlet **Set-ManagementRoleAssignment** se estiver atualizando uma atribuição de função existente. Cada atribuição de função pode ter um escopo de destinatário, incluindo escopos relativos predefinidos. É possível adicionar um escopo de configuração à mesma atribuição de função adicionada a um escopo de destinatário.

Para mais informações sobre sintaxe de filtro e para uma lista completa de propriedades de destinatário filtráveis em destinatários, consulte [Noções básicas sobre filtros do escopo de função de gerenciamento](understanding-management-role-scope-filters-exchange-2013-help.md).

## Escopos de configuração

Estes são os dois tipos de escopos de configuração oferecidos em Exchange 2013:

  - **Escopos de servidor**   Existem dois tipos de escopos de servidor, escopos de filtro do servidor e escopos da lista de servidor. Configuração do servidor, incluindo os conectores de recebimento, filas de transporte, certificados de servidor, diretórios virtuais e assim por diante, pode ser gerenciada se um objeto de servidor está incluído em um escopo de servidor.
    
      - **Escopos de filtro de servidor**   Os escopos de filtro de servidor permitem controlar quais destinatários de função de objetos de servidor podem ser gerenciados pela avaliação de uma ou mais propriedades em objeto de servidor em relação a um valor especificado em uma instrução de filtro. Para criar um escopo de filtro de servidor, use o parâmetro *ServerRestrictionFilter* no cmdlet **New-ManagementScope**.
    
      - **Escopos de lista de servidor**   Os escopos de lista de servidor permitem controlar quais destinatários de função de objetos de servidor podem ser gerenciados com a definição de uma lista de servidores que um destinatário de função pode acessar. Para criar um escopo de lista de servidor, use o parâmetro *ServerList* no cmdlet **New-ManagementScope**.

  - **Escopos de banco de dados**   Existem dois tipos de escopos de banco de dados, escopos de filtro de banco de dados e escopos da lista de banco de dados. Configuração do banco de dados que pode ser gerenciada se um objeto de banco de dados está incluído no escopo de um banco de dados incluem os limites de cota de banco de dados, a manutenção de banco de dados, a replicação de pasta pública, se um banco de dados é montado, e assim por diante. Além de banco de dados configuração, os escopos de banco de dados também podem ser usado para controlar quais destinatários de bancos de dados podem ser criados no. Se você tiver servidores de pré-Exchange 2010 SP1 em sua organização, consulte a seção de escopos de banco de dados e versões anteriores do Exchange neste tópico.
    
      - **Escopos de filtro de banco de dados**   Os escopos de filtro de banco de dados permitem controlar quais destinatários de função de objetos de banco de dados podem ser gerenciados pela avaliação de uma ou mais propriedades em objeto de banco de dados em relação a um valor especificado em uma instrução de filtro. Para criar um escopo de filtro de banco de dados, use o parâmetro *DatabaseRestrictionFilter* no cmdlet **New-ManagementScope**.
    
      - **Escopos de lista de banco de dados**   Os escopos de lista de banco de dados permitem controlar quais destinatários de função de objetos de banco de dados podem ser gerenciados com a definição de uma lista de bancos de dados que um destinatário de função pode acessar. Para criar um escopo de lista de banco de dados, use o parâmetro *DatabaseList* no cmdlet **New-ManagementScope**.

Para mais informações sobre sintaxe de filtro e para uma lista completa de propriedades de servidor e banco de dados filtráveis, consulte [Noções básicas sobre filtros do escopo de função de gerenciamento](understanding-management-role-scope-filters-exchange-2013-help.md).

As listas de servidor e banco de dados podem ser definidas com a especificação de cada servidor e banco de dados que quiser incluir em seus respectivos escopos. Vários servidores ou bancos de dados podem ser especificados em seus respectivos escopos, separando os nomes de servidor e banco de dados com vírgulas.

Ao adicionar um escopo de configuração de servidor ou banco de dados a uma atribuição de função, especifique o nome do escopo de configuração de servidor ou banco de dados no parâmetro *CustomConfigWriteScope* no cmdlet **New-ManagementRoleAssignment** se estiver criando uma nova atribuição de função ou no cmdlet **Set-ManagementRoleAssignment** se estiver atualizando uma atribuição de função existente. Cada atribuição de função pode ter apenas um escopo de configuração.

Além de controlar quais destinatários de função de bancos de dados podem gerenciar, os escopos de banco de dados também permitem controlar quais destinatários de função de bancos de dados podem criar caixas de correio. Isso é separado do controle de quais destinatários um destinatário de função pode gerenciar. Se um destinatário de função tiver permissões para criar uma nova caixa de correio, habilitar por email um usuário existente ou mover caixas de correio, você poderá refinar as permissões usando escopos de banco de dados para controlar o banco de dados em que a caixa de correio é criada ou para qual banco de dados uma caixa de correio é movida. O controle de quais destinatários um destinatário de função pode gerenciar é feito com o uso de um escopo de destinatário especificado no parâmetro *CustomRecipientWriteScope* no cmdlet **New-ManagementRoleAssignment** ou **Set-ManagementRoleAssignment**. O controle de em quais bancos de dados uma caixa de correio pode ser criada ou movida é feito com o uso de um escopo de banco de dados especificado no parâmetro *CustomConfigurationWriteScope* nos mesmos cmdlets.


> [!TIP]
> Distribuição de caixa de correio automática pode ser controlada usando escopos de banco de dados.



recursos de Exchange podem exigir escopos de servidor, escopos de banco de dados ou ambos, a serem gerenciados. Se um recurso requer o servidor e os escopos de banco de dados a ser gerenciado, duas atribuições de função devem ser criadas e atribuídas para o destinatário da função que deve ter acesso para gerenciar o recurso. Uma atribuição de função deve ser associada com o escopo do servidor, e uma atribuição de função deve ser associada com o escopo de banco de dados.

Alguns cmdlets podem usar escopos de configuração que não sejam imediatamente óbvio. A seguinte tabela inclui uma lista de cmdlets e os escopos de configuração que podem ser usados para controlar seu uso. Para os cmdlets incluídos na área de recursos de destinatários, os escopos de configuração permite controlar quais destinatários de bancos de dados podem ser criados. Eles não controlam quais destinatários podem ser gerenciados. A coluna **Escopos necessários** pode conter o seguinte:

  - **Banco de Dados**   Para executar o cmdlet, o destinatário da função deverá receber uma atribuição de função com um escopo de banco de dados que inclui o banco de dados a ser gerenciado, ou o escopo de gravação de configuração implícito da função deverá incluir o banco de dados a ser gerenciado.

  - **Servidor**   Para executar o cmdlet, o destinatário da função deverá receber uma atribuição de função com um escopo de servidor que inclui o servidor a ser gerenciado, ou o escopo de gravação de configuração implícito da função deverá incluir o servidor a ser gerenciado.

  - **Servidor**   Para executar o cmdlet, o destinatário da função deverá receber uma atribuição de função em que um escopo de banco de dados tenha o banco de dados sendo gerenciado ou em que um escopo de servidor tenha o servidor em que o banco de dados está localizado. Ou, o escopo de gravação de configuração implícito da função deve conter o banco de dados a ser gerenciado ou conter o servidor em que o banco de dados está localizado, e a atribuição de função não pode ter um escopo de gravação personalizado.

  - **Servidor e banco de dados**   Para executar esse cmdlet, o destinatário da função deve receber duas atribuições de função. A primeira atribuição de função deve ter um escopo de banco de dados que inclua o banco de dados a ser gerenciado. A segunda atribuição de função deve ter um escopo de servidor que inclua o servidor em que o banco de dados está localizado. As atribuições de função podem ter escopos de configuração personalizados definidos, ou as atribuições de função podem herdar o escopo de gravação de configuração implícito a partir da função. Para herdar o escopo de gravação implícito da função, a atribuição de função não pode ter um escopo de gravação personalizado.

### Áreas de recurso e escopos de banco de dados e servidor aplicáveis

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Área de recurso</th>
<th>Cmdlet</th>
<th>Escopos necessários</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Bancos de dados</p></td>
<td><p><strong>Dismount-Database</strong></p></td>
<td><p>Banco de Dados</p></td>
</tr>
<tr class="even">
<td><p>Bancos de Dados</p></td>
<td><p><strong>Mount-Database</strong></p></td>
<td><p>Banco de Dados</p></td>
</tr>
<tr class="odd">
<td><p>Bancos de Dados</p></td>
<td><p><strong>Move-DatabasePath</strong></p></td>
<td><p>Servidor e banco de dados</p></td>
</tr>
<tr class="even">
<td><p>Bancos de Dados</p></td>
<td><p><strong>Remove-MailboxDatabase</strong></p></td>
<td><p>Servidor ou banco de dados</p></td>
</tr>
<tr class="odd">
<td><p>Bancos de Dados</p></td>
<td><p><strong>Set-MailboxDatabase</strong></p></td>
<td><p>Banco de Dados</p></td>
</tr>
<tr class="even">
<td><p>Alta disponibilidade</p></td>
<td><p><strong>Add-DatabaseAvailabilityGroupServer</strong></p></td>
<td><p>Servidor</p></td>
</tr>
<tr class="odd">
<td><p>Alta disponibilidade</p></td>
<td><p><strong>Add-MailboxDatabaseCopy</strong></p></td>
<td><p>Servidor</p></td>
</tr>
<tr class="even">
<td><p>Alta disponibilidade</p></td>
<td><p><strong>Move-ActiveMailboxDatabase</strong></p></td>
<td><p>Servidor</p></td>
</tr>
<tr class="odd">
<td><p>Alta disponibilidade</p></td>
<td><p><strong>Remove-DatabaseAvailabilityGroupServer</strong></p></td>
<td><p>Servidor</p></td>
</tr>
<tr class="even">
<td><p>Alta disponibilidade</p></td>
<td><p><strong>Remove-MailboxDatabaseCopy</strong></p></td>
<td><p>Servidor ou banco de dados</p></td>
</tr>
<tr class="odd">
<td><p>Alta disponibilidade</p></td>
<td><p><strong>Resume-MailboxDatabaseCopy</strong></p></td>
<td><p>Servidor ou banco de dados</p></td>
</tr>
<tr class="even">
<td><p>Alta disponibilidade</p></td>
<td><p><strong>Set-MailboxDatabaseCopy</strong></p></td>
<td><p>Servidor ou banco de dados</p></td>
</tr>
<tr class="odd">
<td><p>Alta disponibilidade</p></td>
<td><p><strong>Suspend-MailboxDatabaseCopy</strong></p></td>
<td><p>Servidor ou banco de dados</p></td>
</tr>
<tr class="even">
<td><p>Alta disponibilidade</p></td>
<td><p><strong>Update-MailboxDatabaseCopy</strong></p></td>
<td><p>Servidor ou banco de dados</p></td>
</tr>
<tr class="odd">
<td><p>Destinatários</p></td>
<td><p><strong>Connect-Mailbox</strong></p></td>
<td><p>Banco de Dados</p></td>
</tr>
<tr class="even">
<td><p>Destinatários</p></td>
<td><p><strong>Enable-Mailbox</strong></p></td>
<td><p>Banco de Dados</p></td>
</tr>
<tr class="odd">
<td><p>Destinatários</p></td>
<td><p><strong>New-Mailbox</strong></p></td>
<td><p>Banco de Dados</p></td>
</tr>
<tr class="even">
<td><p>Destinatários</p></td>
<td><p><strong>New-MoveRequest</strong></p></td>
<td><p>Banco de Dados</p></td>
</tr>
<tr class="odd">
<td><p>Solução de problemas</p></td>
<td><p><strong>Test-MapiConnectivity</strong></p></td>
<td><p>Banco de Dados</p></td>
</tr>
</tbody>
</table>


## Escopos de banco de dados e versões anteriores do Exchange

Escopos de banco de dados foram introduzidos no Microsoft Exchange 2010 Service Pack 1 (SP1) e continuam a ter suporte no Exchange 2013. Versões do Exchange antes da Exchange 2010 SP1 suportam apenas escopos de destinatário e escopos de configuração do servidor. Quando você cria um novo escopo de banco de dados em um Exchange 2010 SP1 ou posterior server, você receberá o seguinte aviso:

    WARNING: Database management scopes will only be applied when a user connects to a server running Exchange 2010 SP1 or later. Servers running a version of Exchange prior to Exchange 2010 SP1 won't apply any roles from a role assignment linked to a database scope. Database management scopes also won't be visible to the Get-ManagementScope cmdlet when it's run from a pre-Exchange 2010 SP1 server.

Quando você cria um escopo de banco de dados, ele só é aplicado a usuários que se conectam a servidores que executam o Exchange 2010 SP1 ou posterior. Usuários que se conectam a servidores de pré-Exchange 2010 SP1 não terão nenhuma atribuição de função associadas com os escopos de banco de dados aplicados a eles. Isso significa que qualquer permissão fornecido por essas atribuições de função não ser concedido aos usuários quando eles se conectam a servidores de pré-Exchange 2010 SP1. Escopos de banco de dados não podem ser criados, removidos, modificados ou exibidos dos servidores de pré-Exchange 2010 SP1.

Um escopo de banco de dados pode incluir qualquer banco de dados em sua organização Exchange. Isso inclui servidores Exchange Server 2007, Exchange 2010 e Exchange 2013. Isso permite que você controle quais bancos de dados, independentemente da versão de Exchange, que os usuários podem gerenciar. Como com outros escopos de banco de dados, as atribuições de função associadas com os escopos de banco de dados que contêm bancos de dados Exchange 2007 e Exchange 2010 são aplicadas apenas aos usuários quando eles se conectam a um Exchange 2010 SP1 ou posterior server.

Usuários que se conectam a uma préviaExchange 2010 server SP1 podem visualizar e modificar as atribuições de função associadas com os escopos de banco de dados. Isso inclui a alteração do escopo de configuração em uma atribuição de função existente a um escopo de servidor, se ela está associada a um escopo de banco de dados no momento. No entanto, se o escopo da configuração de uma atribuição de função é alterado para um escopo de servidor e um usuário quiser alterá-lo de volta para um escopo de banco de dados mais tarde, ou se o usuário deseja alterar o escopo da configuração para outro escopo de banco de dados, o usuário deve fazer a alteração enquanto estiver conectado a um Exchange 2010 SP1 ou posterior. Os usuários só poderá especificar escopos do servidor quando eles alteram o escopo de configuração em uma atribuição de função, se eles estiverem conectados a uma préviaExchange 2010 server SP1.

