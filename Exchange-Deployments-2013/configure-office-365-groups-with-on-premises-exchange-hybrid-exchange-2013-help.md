---
title: 'Configurar o recurso Grupos do Office 365 com uma implantação híbrida do Exchange local: Exchange 2013 Help'
TOCTitle: Configurar o recurso Grupos do Office 365 com uma implantação híbrida do Exchange local
ms:assetid: 184dfcfe-4b8e-450a-adc6-e647213b9501
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Mt668829(v=EXCHG.150)
ms:contentKeyID: 72513439
ms.date: 01/10/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Configurar o recurso Grupos do Office 365 com uma implantação híbrida do Exchange local

 

_**Tópico modificado em:**2016-12-06_

Saiba como habilitar usuários locais do Exchange para usar o recurso Grupos do Office 365 em uma implantação híbrida.

O recurso Grupos é um serviço do Office 365 com o qual as equipes podem se comunicar, agendar reuniões e colaborar em documentos com mais facilidade. Todas as informações compartilhadas com um grupo, desde mensagens de email enviadas até arquivos armazenados em bibliotecas do grupo no OneDrive for Business ou no SharePoint, estarão disponíveis para todos os membros do grupo. Se você configurou uma implantação híbrida entre sua organização local do Exchange e o Office 365, siga as etapas deste tópico a fim de disponibilizar os grupos criados no Office 365 para os usuários locais.


> [!IMPORTANT]
> O uso de Grupos do Office 365 com usuários locais em uma implantação híbrida do Exchange é um recurso novo. Por ser tão novo, talvez você tenha alguns problemas ao configurá-lo. Confira a seção Problemas conhecidos, no final deste tópico, para saber como corrigir eventuais problemas.



## Pré-requisitos

Antes de começar, certifique-se de que tenha feito o seguinte:

  - Comprou as licenças do Azure Active Directory Premium para o seu locatário. Isso é necessário para habilitar o recurso de write-back dos Grupos no Azure Active Directory Connect.

  - Configurou uma implantação híbrida entre a organização local do Exchange e o Office 365 e verificou se está funcionando corretamente. Para obter mais informações sobre instalações híbridas do Exchange, confira:
    
      - [Implantações Híbridas do Exchange Server](exchange-server-hybrid-deployments-exchange-2013-help.md)
    
      - [Pré-requisitos de implantação híbrida](hybrid-deployment-prerequisites-exchange-2013-help.md)

  - Instalou uma versão com suporte do Exchange local. A integração do Exchange com os Grupos do Office 365 está disponível na atualização cumulativa 1 e versões mais recentes do Exchange 2016 e na atualização cumulativa 11 e versões mais recentes do Exchange 2013. No entanto, a implantação híbrida do Exchange exige que as atualizações cumulativas mais recentes do Exchange 2013 ou do Exchange 2016 sejam instaladas nos servidores Exchange locais. Se não for possível instalar a atualização cumulativa mais recente, use a atualização lançada imediatamente antes da atualização cumulativa atual.

  - Configurou o logon único usando o Azure Active Directory Connect (Azure AD Connect). Isso é necessário para que os usuários possam clicar na opção **Exibir arquivos de grupo** ou em links para anexo de nuvem nas mensagens de email de grupo.
    
    Quando configurar o Azure AD Connect para logon único em uma implantação híbrida do Exchange, recomendamos usar a sincronização de senha. Os Serviços de Federação do Active Directory (AD FS) devem ser usados apenas em organizações de grande porte nos seguintes casos: se você tiver uma implantação complexa do Active Directory local (por exemplo, várias florestas do Active Directory); se outro produto da Microsoft exigir que os AD FS funcionem com o Office 365; ou se não for possível sincronizar senhas fora da rede local devido a políticas de conformidade. Para saber mais sobre logon único, confira o artigo [Integração de suas identidades locais com o Azure Active Directory](http://go.microsoft.com/fwlink/p/?linkid=723513).

## Habilitar o recurso write-back dos Grupos no Azure AD Connect

1.  No assistente do Azure AD Connect, selecione **Personalizar as opções de sincronização** e, em seguida, clique em **Avançar**.

2.  Na página **Conectar-se ao Azure AD**, insira as credenciais locais e do Office 365. Clique em **Avançar**.

3.  Na página **Recursos opcionais**, verifique se as opções que você configurou anteriormente ainda estão selecionadas. As opções mais comumente selecionadas são **Exchange híbrido** e **Sincronização de senha hash**.

4.  Selecione **Write-back de grupo** e, em seguida, clique em **Avançar**.

5.  Na página **Write-back**, selecione uma UO (unidade organizacional) do Active Directory para armazenar os objetos que são sincronizados do Office 365 com a sua organização local e clique em **Avançar**.

6.  Na página **Pronto para configurar**, clique em **Configurar**.

7.  Quando o assistente estiver concluído, clique em **Sair** na página **Configuração concluída**.

8.  Abra a ferramenta Usuários e Computadores do Active Directory em um controlador de domínio do Active Directory e localize a conta de usuário que começa com **AAD\_**. Anote o nome dessa conta.

9.  Abra o Shell de Gerenciamento do Exchange em um servidor Exchange local e execute os comandos a seguir.
    
        $AzureADConnectSWritebackAccount = <AAD_ account name from step 8>
        
        $GroupsOU = <writeback Active Directory OU selected in step 5>
        
        Import-Module "C:\Program Files\Microsoft Azure Active Directory Connect\AdPrep\AdSyncPrep.psm1"
        
        Initialize-ADSyncGroupWriteBack -ADConnectorAccount $AzureADConnectSWritebackAccount -GroupWriteBackContainerDN $GroupsOU

## Configurar um domínio de grupo

O domínio SMTP primário de um Grupo do Office 365 é chamado de *domínio do grupo*. O domínio padrão aceito de uma organização é escolhido como o domínio do grupo por padrão. Caso pretenda adicionar um domínio dedicado para grupos, adicione-o de acordo com as etapas a seguir. Para saber mais sobre suporte para vários domínios dos Grupos do Office 365, confira o artigo [Suporte para vários domínios dos Grupos do Office 365](https://support.office.com/pt-br/article/multi-domain-support-for-office-365-groups-admin-help-7cf5655d-e523-4bc3-a93b-3ccebf44a01a)

1.  Adicione o novo domínio em sua organização do Office 365. Para saber mais sobre como adicionar um domínio ao Office 365, confira o artigo [Adicionar usuários e domínios ao Office 365](https://support.office.com/pt-br/article/add-users-and-domain-to-office-365-6383f56d-3d09-4dcb-9b41-b5f5a5efd611?ui=en-us%26rs=en-us%26ad=us)

2.  Adicione o domínio do grupo como um domínio aceito na organização local do Exchange usando o comando a seguir. Isso é necessário para que o conector de Envio híbrido possa ser usado para entregar emails de saída ao domínio do grupo no Office 365.
    
        New-AcceptedDomain -Name groups.contoso.com -DomainName groups.contoso.com -DomainType InternalRelay

3.  Crie os seguintes registros DNS públicos com seu provedor DNS.
    
    
    <table>
    <colgroup>
    <col style="width: 33%" />
    <col style="width: 33%" />
    <col style="width: 33%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th><p>Nome de registro DNS</p></th>
    <th><p>Tipo de registro DNS</p></th>
    <th><p>Valor de registro DNS</p></th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td><p>groups.contoso.com</p></td>
    <td><p>MX</p></td>
    <td><p>groups-contoso-com.mail.protection.outlook.com</p>

    > [!TIP]
    > O formato desse valor de registro DNS será <EM>&lt;domain key&gt;</EM>.mail.protection.outlook.com. Para descobrir qual é a chave do seu domínio, confira o artigo <A href="https://support.office.com/pt-br/article/gather-the-information-you-need-to-create-office-365-dns-records-77f90d4a-dc7f-4f09-8972-c1b03ea85a67?ui=en-us%26rs=en-us%26ad=us">Coletar as informações de que você precisa para criar registros de DNS do Office 365</A>.


</td>
    </tr>
    <tr class="even">
    <td><p>autodiscover.groups.contoso.com</p></td>
    <td><p>CNAME</p></td>
    <td><p>autodiscover.outlook.com</p></td>
    </tr>
    </tbody>
    </table>
    

    > [!WARNING]
    > Se o registro DNS MX do domínio do grupo for definido para o servidor Exchange local, o fluxo de emails não funcionará corretamente entre os usuários da organização local do Exchange e o Grupo do Office 365.



4.  Adicione o domínio do grupo no conector de Envio híbrido, criado pelo assistente de Configuração híbrida na organização local do Exchange, usando o comando a seguir.
    
        Set-SendConnector -Identity "Outbound to Office 365" -AddressSpaces "contoso.mail.onmicrosoft.com","groups.contoso.com"
    

    > [!TIP]
    > Se o conector de Envio não estiver atualizado ou se o domínio do grupo não for adicionado como um domínio aceito na organização local do Exchange, os emails enviados de uma caixa de correio local não serão entregues para o grupo, a menos que o grupo esteja configurado para receber emails de remetentes externos.



## Como saber se funcionou?

Para garantir que os grupos estejam trabalhando com sua implantação híbrida do Exchange, você deverá testá-los usando uma caixa de correio local e uma caixa de correio que foi movida da sua organização local para o Office 365. Siga as etapas nas próximas seções para realizar os testes.

## Teste com uma caixa de correio local

1.  Adicione uma caixa de correio local a um Grupo do Office 365.

2.  Adicione uma caixa de correio do Office 365 ao mesmo Grupo do Office 365.

3.  Efetue o login na caixa de correio do Office 365 usando o Outlook na Web.

4.  Envie uma mensagem para o grupo usando a caixa de correio do Office 365.

5.  Abra a caixa de correio local usando o Outlook 2016 ou o Outlook na Web.

6.  Verifique se a caixa de correio recebeu a mensagem de email contendo a postagem enviada ao Grupo do Office 365.

7.  Na mesma caixa de correio, escreva uma resposta para a mensagem e envie-a ao grupo.

8.  Verifique se a mensagem pode ser visualizada por todos os membros do grupo.

## Teste usando uma caixa de correio movida para o Office 365

1.  Mova a caixa de correio de sua organização local do Exchange para o Office 365.

2.  Adicione a caixa de correio a um Grupo do Office 365.

3.  Em uma nova sessão no navegador, efetue o login na caixa de correio que foi movida para o Office 365.

4.  No Outlook na Web, verifique se o grupo esta listado na barra de navegação à esquerda.

5.  Envie uma mensagem para o grupo.

6.  Verifique se a mensagem pode ser visualizada por todos os membros do grupo.

## Problemas conhecidos

  - **Os grupos não são exibidos para as caixas de correio migradas para o Office 365** Quando um usuário é migrado de uma organização local do Exchange para o Office 365, os grupos não são exibidos no painel de navegação esquerdo do Outlook ou do Outlook na Web. Para corrigir esse problema, remova a caixa de correio de todos os grupos dos quais ela seja membro e adicione-a novamente em cada um dos grupos.

  - **Os novos grupos não aprecem na lista de endereços global do Exchange (GAL)** Quando um grupo é criado no Office 365, ele não aparece automaticamente na GAL local . Para corrigir esse problema, abra o Exchange Management Shell em um servidor local do Exchange e execute o seguinte comando.
    
        Update-Recipient "<group name>"

  - **Os grupos não recebem as mensagens dos usuários locais** O usuário local não pode enviar emails a um Grupo do Office 365 nas seguintes condições:
    
      - O domínio do grupo está configurado como um domínio autoritativo em sua organização local do Exchange.
    
      - O grupo foi recentemente criado e suas informações ainda não foram gravadas em seu Active Directory local.
    
    Esse problema se resolverá quando o Azure AD Connect realizar a próxima sincronização entre o Office 365 e a organização local. A sincronização do Azure AD Connect ocorre a cada trinta minutos.

  - **Os usuários locais não conseguem usar os links incluídos nos rodapés das mensagens de grupo**Os usuários locais não conseguem usar os links **Exibir conversas do grupo** ou **Cancelar inscrição** que estão incluídos no rodapé das mensagens do grupo enviadas a eles. Para cancelar a inscrição em um grupo, os usuários locais devem falar com o administrador do grupo.

  - **Emails enviados a um endereço SMTP secundário do grupo não são entregues** Quando são adicionados diversos endereços de email a um grupo, apenas o endereço SMTP principal é gravado no Active Directory local. Se um usuário local tentar enviar uma mensagem para o endereço SMTP secundário de um grupo, a mensagem não será entregue. Para evitar esse problema, configure apenas um endereço SMTP em cada grupo.

  - **Os usuários locais não podem se tornar administradores de um grupo** Os usuários locais não conseguem acessar diretamente o espaço do grupo. Por isso, eles não podem ser adicionados como administradores de um grupo.

  - **A entrega de emails externos a um grupo pode falhar, se o fluxo de emails centralizado estiver habilitado** Quando o fluxo de emails centralizado está habilitado, ocorre uma falha na entrega dos emails enviados por usuários externos a um grupo, mesmo que o grupo permita emails de remetentes externos.

  - **Os usuários locais não conseguem enviar emails como grupo** Quando um usuário local tentar enviar uma mensagem como um Grupo do Office 365, receberá um erro de "Permissão negada", mesmo que tenha recebido uma permissão "Enviar Como". As permissões "Enviar Como" em um grupo funcionam apenas para usuários de caixa de correio do Exchange Online.

  - **Selecionar um grupo no painel de navegação esquerdo do Outlook não abre a caixa de correio do grupo** O Outlook usa a URL de Descoberta Automática para abrir uma caixa de correio de grupo. Se o endereço de email principal do grupo estiver em um domínio que não aponta para a URL de Descoberta Automática do Office 365 (autodiscover.outlook.com), não será possível abrir a caixa de correio do grupo no Outlook. Para corrigir o problema, você pode provisionar os grupos com um endereço de email principal em um domínio que aponta para a URL de Descoberta Automática do Office 365. Você pode configurar uma política de endereço de email para adicionar um endereço de email principal em todas as caixas de correio do grupo que apontam para a URL de Descoberta Automática do Office 365. Para saber mais, confira o artigo [Suporte para vários domínios de Grupos do Office 365](https://support.office.com/pt-br/article/multi-domain-support-for-office-365-groups-admin-help-7cf5655d-e523-4bc3-a93b-3ccebf44a01a).

