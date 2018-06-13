---
title: 'Permissões em implantações híbridas do Exchange: Exchange 2013 Help'
TOCTitle: Permissões em implantações híbridas do Exchange
ms:assetid: 58b46b2c-a6b2-424a-8fc2-0f1fe1ad8e18
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/JJ906433(v=EXCHG.150)
ms:contentKeyID: 51406958
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Permissões em implantações híbridas do Exchange

 

_**Aplica-se a:**Exchange Server 2013, Exchange Server 2016_

_**Tópico modificado em:**2018-05-02_

A organização do Exchange Online no Office 365 é baseada no Exchange Server e também usa o RBAC (controle de acesso baseado em função) para controlar permissões, assim como as organizações locais. Os administradores recebem permissões usando grupos de funções de gerenciamento e os usuários finais recebem permissões usando políticas de atribuição de funções de gerenciamento.

Saiba mais sobre permissões do Exchange Online e do Exchange local em: [Permissões](https://technet.microsoft.com/pt-br/library/dd351175\(v=exchg.150\))

## Permissões do administrador

Por padrão, tornamos o usuário usado na criação do locatário do Office 365 um membro do grupo de funções Gerenciamento da Organização do Exchange Online. Esse usuário pode gerenciar toda a organização do Exchange Online, incluindo a definição de configurações em nível de organização e o gerenciamento de destinatários do Exchange Online.

É possível incluir mais administradores na organização do Exchange Online, dependendo do gerenciamento necessário. Por exemplo, é possível incluir mais administradores de organização e de destinatários, permitir que usuários especialistas realizem tarefas de conformidade como descoberta, configurar permissões personalizadas e muito mais. Todo o gerenciamento de permissões do Exchange Online para administradores do Office 365 deve ser realizado na organização do Exchange Online usando o EAC (Centro de Administração do Exchange) ou o PowerShell remoto.


> [!IMPORTANT]
> Não há nenhuma transferência de permissões entre a organização local e a organização do Office 365. As permissões definidas na organização local devem ser recriadas na organização do Office 365.



Para obter mais informações, consulte [Gerenciar grupos de função](https://technet.microsoft.com/pt-br/library/jj657480\(v=exchg.150\)) e [Gerenciar membros do grupo de função](https://technet.microsoft.com/pt-br/library/jj657492\(v=exchg.150\)).

## Delegar permissões de caixa de correio

Nas implantações do Exchange no local, os usuários podem receber uma variedade de permissões para caixas de correio de outros usuários. Isso é chamado permissões delegadas de caixa de correio e de seus útil quando um assistente administrativo precisa gerenciar alguma parte da caixa de correio do outro usuários; Por exemplo, gerenciamento de calendário de um executivo. Implantações híbridas do Exchange suportam o uso de alguns, mas não todos, permissões de caixa de correio entre caixas de correio localizadas em uma organização do Exchange no local e caixas de correio localizadas no Office 365. As seções a seguir detalham quais permissões são e não são suportados; configuração adicional necessária para oferecer suporte a permissões de caixa de correio híbrido; e como as permissões de caixa de correio são sincronizadas entre sua organização local e o Office 365.

## Permissões de caixa de correio suportadas em ambientes híbridos

As permissões seguintes **são** suportados:

  - **Acesso total** Uma caixa de correio em um servidor de Exchange local pode receber a permissão de **Acesso total** para uma caixa de correio do Office 365 e vice-versa. Por exemplo, uma caixa de correio do Office 365 pode receber a permissão de **Acesso total** para uma caixa de correio compartilhada no local. Os usuários precisam abrir a caixa de correio usando o cliente de desktop do Outlook; permissões de caixa de correio entre locais não são suportadas no Outlook na web.
    

    > [!TIP]
    > Os usuários podem receber outras solicitações por credenciais ao acessar pela primeira vez uma caixa de correio da outra organização e adicioná-la ao seu perfil do Outlook.



  - **Enviar em nome de** Uma caixa de correio em um servidor de Exchange local pode ter a permissão **Enviar em nome de** uma caixa de correio do Office 365 e vice-versa. Por exemplo, uma caixa de correio do Office 365 pode receber a permissão **Enviar em nome de** uma caixa de correio compartilhada no local. Os usuários precisam abrir a caixa de correio usando o cliente de desktop do Outlook; permissões de caixa de correio entre locais não são suportadas no Outlook na web.
    
    Algumas alterações são necessários em seu servidor do Azure Active Directory Connect para enviar em nome de permissões para sincronizar entre seus servidores do Exchange no local e o Exchange Online. Para obter detalhes, consulte Habilitando o suporte para permissões de caixa de correio híbrido no Azure Active Directory Connect posteriormente neste tópico.

  - **Folder permissions** Grants access to the contents of a particular folder.

  - **Itens particulares** Ao adicionar que um representante a opção pode ser configurado para permitir que um usuário com permissões de pasta para ver os itens de calendário particular.


> [!TIP]
> A partir de fevereiro de 2018 o recurso para oferecer suporte ao acesso total, enviar em nome e pasta direitos de florestas cruzadas está sendo distribuídas e espera-se ser concluída por de 2018 abril.



As seguintes permissões ou recursos **não são** suportados:

  - **Send-As** Permite ao usuário enviar e-mail, embora ele parece ser provenientes da caixa de correio de outro usuário.

  - **Mapeamento automático** Habilita o Outlook, quando ele for iniciado, para abrir automaticamente qualquer caixa de correio que um usuário tem permissão de **Acesso total** ao.

Qualquer caixa de correio que recebem essas permissões a partir de outra caixa de correio deve ser movida ao mesmo tempo concedendo da caixa de correio. Se uma caixa de correio recebe permissões de várias caixas de correio, essa caixa de correio e todas as caixas de correio concedendo permissões a ele, precisará ser movidos ao mesmo tempo.

## Configurando os servidores do Exchange local para oferecer suporte a permissões de caixa de correio híbrida

Para habilitar o acesso total e enviar em nome de permissões em uma implantação híbrida, configuração adicional alterações pode ser necessárias dependendo da versão do Exchange que você instalou. A tabela a seguir mostra quais versões do Exchange oferece suporte a caixa de correio delegada permissões em uma implantação híbrida com o Office 365 e qual configuração adicional será necessária. Para obter etapas sobre como configurar o Exchange 2013 e 2010 servidores e caixas de correio para suportar as ACLs, consulte [Configurar o Exchange para oferecer suporte à caixa de correio delegada permissões em uma implantação híbrida](configure-exchange-to-support-delegated-mailbox-permissions-in-a-hybrid-deployment-exchange-2013-help.md).


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Versão do Exchange</th>
<th>Pré-requisitos</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Exchange 2016</p></td>
<td><p>Nenhuma configuração adicional necessária.</p></td>
</tr>
<tr class="even">
<td><p>Exchange 2013</p></td>
<td><p>Servidores Exchange 2013 precisará dos seguintes itens:</p>
<ul>
<li><p>A última atualização cumulativa (CU) ou a imediatamente anterior CU, instalado. Servidores Exchange 2013 executando CUs mais antigos não são suportados e talvez não funcione com permissões de caixa de correio delegada em uma implantação híbrida.</p></li>
<li><p>A organização do Exchange está configurada para permitir que o controle de acesso (ACLs) para ser marcados nos objetos de email de lista e sincronizadas com o Office 365.</p></li>
<li><p>No local remotas caixas de correio associadas com caixas de correio movidas para o Office 365 antes do Exchange 2013 CU10 precisam ser configurados manualmente para oferecer suporte a ACLs. Caixas de correio remotas, criado em servidores executando o Exchange 2013 CU10 ou posterior e depois a organização está definida para permitir ACLs, do Exchange são configuradas automaticamente.</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Exchange 2010</p></td>
<td><p>Servidores Exchange 2010 SP3 precisará dos seguintes itens:</p>
<ul>
<li><p>O último pacote cumulativo (RU) ou o imediatamente anterior RU, instalado. Os servidores do Exchange 2010 SP3 executando RU mais antigo não são suportados e talvez não funcione com permissões de caixa de correio delegada em uma implantação híbrida.</p></li>
<li><p>No local remotas caixas de correio associadas com caixas de correio do Office 365 precisam ser configurado para suportar as ACLs. Isso precisa ser feito para cada local remoto da caixa de correio que está associado com uma caixa de correio do Office 365.</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Exchange 2007 ou anterior</p></td>
<td><p>Não suportado.</p></td>
</tr>
</tbody>
</table>


## Habilitando o suporte para permissões de caixa de correio híbrido no Azure Active Directory Connect

Além de configurar seus servidores do Exchange local, você também precisará certificar-se de servidor do Azure Active Directory Connect (conexão AAD) está configurado para sincronizar permissões de caixa de correio híbrida. Aqui está o que você precisa fazer para certificar-se de que seu servidor conectar AAD está pronta para oferecer suporte a essas permissões:

  - **Conectar AAD atualização** Conectar AAD precisa ser atualizado pelo menos a versão 1.1.553.0. Você pode baixar a versão mais recente do AAD Connect do [Microsoft Azure Active Directory Connect](http://go.microsoft.com/fwlink/p/?linkid=510956).

  - **Habilitar Exchange híbrido no AAD conectar** Para sincronizar os atributos que permitem permissões de caixa de correio híbrida (especificamente a enviar em nome de permissão), você precisará certificar-se de que a opção de configuração de **implantação híbrida do Exchange** está habilitada no AAD se conectar. Para obter informações sobre como executar o Assistente de instalação AAD conectar-se novamente para atualizar sua configuração, confira [sincronização do Azure Connect da AD: executar o Assistente de instalação de uma segunda vez](https://docs.microsoft.com/en-us/azure/active-directory/connect/active-directory-aadconnectsync-installation-wizard)

## Como as permissões de caixa de correio são sincronizadas entre seu local e organizações do Office 365

## Permissões do usuário final

Assim como acontece com as permissões de administrador, os usuários finais do Exchange Online podem receber permissões. Por padrão, os usuários finais recebem permissões através da diretiva de atribuição de função padrão. Essa diretiva é aplicada a todas as caixas de correio na organização do Exchange Online. Se as permissões concedidas por padrão forem suficientes, não será necessário mudar nada.

Para modificar as permissões de usuário final, você pode modificar a diretiva de atribuição de função padrão ou criar novas diretivas de atribuição. Ao criar várias diretivas de atribuição, é possível atribuir diretivas diferentes a grupos diferentes de caixas de correio, permitindo controlar as permissões concedidas a cada grupo dependendo das necessidades deles. Todo o gerenciamento de permissões para usuários finais do Exchange Online deve ser realizado na organização do Exchange Online usando o EAC ou o PowerShell remoto.

Assim como acontece com as permissões de administrador, as permissões de usuário final não são transferidas entre a organização local e a organização do Exchange Online. Qualquer permissão definida na organização local terá que ser recriada na organização do Exchange Online.

Para obter mais informações, consulte [Gerenciar políticas de atribuição de função](https://technet.microsoft.com/pt-br/library/jj657511\(v=exchg.150\)) e [Alterar a política de atribuição de uma caixa de correio](https://technet.microsoft.com/pt-br/library/dd638076\(v=exchg.150\)).

A tabela a seguir lista as permissões concedidas pelas diretivas de atribuição de função padrão na organização do Exchange Online.

### Permissões de diretiva de atribuição de função padrão

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Função de gerenciamento</th>
<th>Descrição</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>MyTeamMailboxes</p></td>
<td><p>A função de gerenciamento <code>MyTeamMailboxes</code> permite que os usuários individuais criem caixas de correio de site e as conectem a sites do Microsoft SharePoint.</p></td>
</tr>
<tr class="even">
<td><p>Meus Aplicativos do Marketplace</p></td>
<td><p>A função de gerenciamento <code>My Marketplace Apps</code> permitem que usuários individuais exibam e modifiquem seus aplicativos do marketplace do Microsoft Office.</p></td>
</tr>
<tr class="odd">
<td><p>MyBaseOptions</p></td>
<td><p>A função de gerenciamento <code>MyBaseOptions</code> permite que usuários individuais exibam e modifiquem a configuração básica de sua própria caixa de correio e as definições associadas.</p></td>
</tr>
<tr class="even">
<td><p>MyContactInformation</p></td>
<td><p>A função de gerenciamento <code>MyContactInformation</code> permite que usuários individuais modifiquem suas informações de contato, incluindo endereço e telefones.</p></td>
</tr>
<tr class="odd">
<td><p>MyDistributionGroupMembership</p></td>
<td><p>A função de gerenciamento <code>MyDistributionGroupMembership</code> permite que usuários individuais vejam e modifiquem sua associação em grupos de distribuição em uma organização, contanto que esses grupos de distribuição permitam a manipulação da associação do grupo.</p></td>
</tr>
<tr class="even">
<td><p>MyDistributionGroups</p></td>
<td><p>A função de gerenciamento <code>MyDistributionGroups</code> permite que usuários individuais criem, modifique e exibam grupos de distribuição, e que modifiquem, exibam, removam e adicionem membros a grupos de distribuição de sua propriedade.</p></td>
</tr>
<tr class="odd">
<td><p>MyMailSubscription</p></td>
<td><p>A função <code>MyMailSubscription</code> permite que usuários individuais vejam e modifiquem suas configurações de assinatura de email, como formato de mensagem e padrões de protocolo.</p></td>
</tr>
<tr class="even">
<td><p>MyProfileInformation</p></td>
<td><p>A função de gerenciamento <code>MyProfileInformation</code> permite que usuários individuais modifiquem seus nomes.</p></td>
</tr>
<tr class="odd">
<td><p>MyRetentionPolicies</p></td>
<td><p>A função de gerenciamento <code>MyRetentionPolicies</code> permite que usuários individuais exibam as marcas de retenção e exibam e modifiquem os padrões e as configurações de marca de retenção.</p></td>
</tr>
<tr class="even">
<td><p>MyTextMessaging</p></td>
<td><p>A função de gerenciamento <code>MyTextMessaging</code> permite que usuários individuais criem, exibam e modifiquem suas configurações de mensagens de texto.</p></td>
</tr>
<tr class="odd">
<td><p>MyVoiceMail</p></td>
<td><p>A função de gerenciamento <code>MyVoiceMail</code> permite que usuários individuais exibam e modifiquem suas configurações de caixa postal.</p></td>
</tr>
<tr class="even">
<td><p>Meus aplicativos ReadWriteMailbox</p></td>
<td><p>A função de gerenciamento <code>My ReadWriteMailbox Apps</code> permite que os usuários instalem aplicativos com permissões ReadWriteMailbox.</p></td>
</tr>
<tr class="odd">
<td><p>Meus Aplicativos personalizados</p></td>
<td><p>A função de gerenciamento <code>My Custom Apps</code> permite que os usuários exibam e modifiquem seus aplicativos personalizados.</p></td>
</tr>
</tbody>
</table>

