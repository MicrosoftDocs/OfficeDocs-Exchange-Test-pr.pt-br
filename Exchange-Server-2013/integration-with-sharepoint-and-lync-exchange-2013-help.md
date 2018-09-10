---
title: 'Integração com o SharePoint e o Lync: Exchange 2013 Help'
TOCTitle: Integração com o SharePoint e o Lync
ms:assetid: 056b29f6-e0e9-4974-b763-002518857a93
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/JJ150480(v=EXCHG.150)
ms:contentKeyID: 50484894
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Integração com o SharePoint e o Lync

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2016-12-09_

Microsoft O Exchange Server 2013 inclui muitos recursos que se integram ao Microsoft SharePoint 2013 e ao Microsoft Lync 2013. Juntos, esses produtos oferecem um conjunto de recursos que possibilitam cenários como Descoberta eletrônica empresarial e colaboração usando caixas de correio de site.

## Arquivamento, isenção e descoberta eletrônica

O arquivamento de emails e documentos, preservando-os pelo tempo necessário para cumprir com os requisitos comerciais e de conformidade regulamentar, e a capacidade de pesquisá-los rapidamente para atender às solicitações de descoberta eletrônica são essenciais para a maioria das organizações. Juntos, o Exchange 2013, o SharePoint 2013 e o Lync Server 2013 integram funcionalidades de arquivamento, isenção e descoberta eletrônica, permitindo que você preserve dados importantes no local em caixas de correio do Exchange, documentos e sites do SharePoint e conteúdo arquivado do Lync. O Centro de descoberta eletrônica do SharePoint 2013 permite que gerentes de descoberta autorizados realizem uma pesquisa de descoberta eletrônica por conteúdo nesses armazenamento, visualizando os resultados da pequisa e exportando os dados para análise jurídica.

## Arquivar conteúdo do Lync Server 2013 no Exchange 2013

Com o Lync Server 2013 implantado em uma organização com o Exchange 2013, você pode configurar o Lync para arquivar o conteúdo do sistema de mensagens instantâneas e de reuniões online, como apresentações compartilhadas ou documentos na caixa de correio do Exchange 2013 do usuário. O arquivamento de dados do Lync no Exchange 2013 permite que você aplique políticas de retenção a eles. O conteúdo arquivado do Lync também aparece nas pesquisas de descoberta eletrônica. Para mais detalhes sobre o arquivamento do Lync e como implantá-lo, consulte estes tópicos:

  - [Planejamento para arquivamento](https://go.microsoft.com/fwlink/p/?linkid=265005)

  - [Implantando o arquivamento](https://go.microsoft.com/fwlink/p/?linkid=265006)

## Pesquisar dados do Exchange, SharePoint e Lync usando o Centro de descoberta do SharePoint 2013

O Exchange 2013 permite que o SharePoint 2013 pesquise conteúdo de caixas de correio do Exchange usando a API de pesquisa federada. O SharePoint 2013 oferece um Centro de descoberta eletrônica para permitir que uma equipe autorizada realize a descoberta eletrônica. A Microsoft Search Foundation proporciona uma infraestrutura comum de indexação e pesquisa para o Exchange 2013 e o SharePoint 2013 e permite o uso da mesma sintaxe de consulta nos dois aplicativos. Isso garante que a pesquisa de descoberta eletrônica realizada no SharePoint 2013 retornará o mesmo conteúdo do Exchange 2013 que a mesma pesquisa usando a descoberta eletrônica no local do Exchange 2013. Com o Centro de descoberta eletrônica do SharePoint 2013, você também pode exportar o conteúdo retornado em uma pesquisa de descoberta eletrônica, incluindo a exportação do conteúdo do Exchange 2013 para um arquivo PST.

Para obter mais detalhes, consulte os seguintes tópicos:

  - [Descoberta Eletrônica In-loco](https://docs.microsoft.com/pt-br/exchange/security-and-compliance/in-place-ediscovery/in-place-ediscovery)

  - [Retenção local e Retenção de litígio](in-place-hold-and-litigation-hold-exchange-2013-help.md)

  - [Configurar o eDiscovery no SharePoint 2013](https://go.microsoft.com/fwlink/p/?linkid=257727)

  - [Novidades no eDiscovery no SharePoint Server 2013](https://go.microsoft.com/fwlink/?linkid=275091)

  - [Configurar o Exchange para o SharePoint eDiscovery Center](configure-exchange-for-sharepoint-ediscovery-center-exchange-2013-help.md)

## Caixas de correio locais

Em muitas organizações, as informações residem em dois repositórios diferentes: no email do Microsoft Exchange e nos documentos do SharePoint. Ou seja, há duas interfaces diferentes para acessar essas informações. Isso resulta em uma experiência de usuário confusa e torna impossível uma colaboração eficaz. Com as caixas de correio de sites, os usuários podem colaborar de maneira eficaz, reunindo emails do Exchange e documentos do SharePoint. Para os usuários, uma caixa de correio de site funciona como um arquivo central, um local para que eles arquivem emails e documentos de projetos que só podem ser acessados e editados por membros do site. As caixas de correio de site estão na superfície do Outlook 2013 e oferecem, aos usuários, acesso fácil aos emails e documentos dos projetos de sua responsabilidade. Adicionalmente, o mesmo conjunto de conteúdos pode ser acessado diretamente do site do SharePoint em si.

Sob a proteção de uma caixa de correio de site, o conteúdo estará em um local adequado. O Exchange armazena os emails, oferecendo, aos usuários, o mesmo modo de exibição de mensagens para conversas por email que eles usam todos os dias, em suas próprias caixas de correio. O SharePoint armazena os documentos, proporcionando controle de versão e coautoria de documentos. O Exchange sincroniza apenas os metadados suficientes do SharePoint para criar a visualização do documento no Outlook (por exemplo, título do documento, data da última atualização, autor da última modificação, tamanho).

As caixas de correio de site são provisionadas e gerenciadas a partir do SharePoint 2013. Para mais detalhes, consulte os tópicos abaixo:

  - [Caixas de correio locais](site-mailboxes-exchange-2013-help.md)

  - [Configurar caixas de correio de site no SharePoint Server 2013](https://go.microsoft.com/fwlink/p/?linkid=258264)

## Repositório unificado de contatos

O Repositório unificado de contatos (UCS) é um recurso que oferece uma experiência de contato consistente nos produtos Microsoft Office. Esse recurso permite que os usuários armazenem todas as informações de contato em suas caixas de correio do Exchange 2013. Dessa forma, as mesmas informações de contato estarão disponíveis globalmente no Lync, no Exchange, no Outlook e no Outlook Web App.

Depois de Lync Server 2013 está instalado em um ambiente com Exchange 2013 e você tiver configurado a autenticação de servidor-para-servidor entre os dois, os usuários podem iniciar a migração de contatos existentes de Lync Server 2013 para Exchange 2013. Para obter detalhes, consulte [Planning and Deploying Unified Contact Store](https://go.microsoft.com/fwlink/p/?linkid=275092).

## Fotos do usuário

Fotos do usuário é um recurso que permite que você armazene as fotos de usuários de alta resolução no Exchange 2013 que possa ser acessado por aplicativos do cliente, incluindo Outlook, Outlook Web App, SharePoint 2013, Lync 2013 e clientes de email móvel. Uma foto de baixa resolução também é armazenada em Active Directory. Como com repositórios de contato unificado, fotos dos usuários permitem que sua organização manter uma foto de perfil de usuário consistente que pode ser consumida por aplicativos do cliente, sem exigir que cada aplicativo tem seus próprios fotos dos usuários e as diferentes maneiras para adicionar e gerenciá-los. Os usuários podem gerenciar suas próprias fotos usando Outlook Web App, SharePoint 2013 ou Lync 2013. Para detalhes sobre como gerenciar as fotos no Outlook Web App, consulte [Minha conta](https://go.microsoft.com/fwlink/p/?linkid=269646).

## Presença do Lync no Outlook Web App

Em ambientes do Exchange 2013 com o Lync Server 2013 instalado, você pode configurá-los para permitir que os usuários vejam as informações de presença no Outlook Web App. Os usuários podem ver seus contatos e grupos de mensagens instantâneas no painel de navegação do Outlook Web App, responder a sessões de mensagens instantâneas ou iniciá-las a partir do Outlook Web App e gerenciar seus contatos e grupos de mensagens instantâneas.

## Autenticação OAuth

O Exchange 2013, o SharePoint 2013 e o Lync Server 2013 fornecem a funcionalidade avançada entre produtos descrita acima usando o protocolo de autorização OAuth para autenticação de servidor a servidor. O uso do mesmo protocolo de autenticação permite que esses aplicativos façam a autenticação um do outro de forma perfeita e segura. O mecanismo de autenticação aceita autenticação como um aplicativo usando o contexto de uma conta vinculada e representação de usuário onde a solicitação de acesso é feita no contexto do usuário.

OAuth é um protocolo de autorização padrão usado por muitos sites e serviços da web. Ele permite que os clientes acessar os recursos fornecidos por um servidor de recurso sem precisar fornecer um nome de usuário e senha. Autenticação é realizada por um servidor de autorização confiável pelo proprietário do recurso, que fornece ao cliente com um token de acesso. O token concede acesso a um conjunto específico de recursos por um período especificado. Para obter mais detalhes sobre a Exchange 2013 da implementação do OAuth, consulte [\[MS-XOAUTH\]: extensões de protocolo de autorização do OAuth 2.0](https://go.microsoft.com/fwlink/p/?linkid=275093).

**OAuth em implantações no local**

Em uma implantação no local, o Exchange 2013, o SharePoint 2013 e o Lync Server 2013 não precisam de um servidor de autorização para emitir tokens. Cada um desses aplicativos emite tokens autoassinados para acessar recursos fornecidos por outros aplicativos. O aplicativo que fornece acesso aos recursos, como o Exchange 2013, por exemplo, precisa confiar nos tokens autoassinados apresentados pelo aplicativo que fez a chamada. A confiança é estabelecida com a criação de uma configuração de *aplicativo de parceiros* para o aplicativo que faz a chamada, incluindo ApplicationID, certificado e AuthMetadataUrl do aplicativo de chamada. O Exchange 2013, o SharePoint 2013 e o Lync Server 2013 publicam o documento de metadados de autorização em um URL bastante conhecido.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p><strong>Servidor</strong></p></td>
<td><p><strong>AuthMetadataUrl</strong></p></td>
</tr>
<tr class="even">
<td><p>Exchange 2013</p></td>
<td><p><code>https://&lt;serverfqdn&gt;/autodiscover/metadata/json/1</code></p></td>
</tr>
<tr class="odd">
<td><p>Lync Server 2013</p></td>
<td><p><code>https://&lt;serverfqdn&gt;/metadata/json/1</code></p></td>
</tr>
<tr class="even">
<td><p>SharePoint 2013</p></td>
<td><p><code>https://&lt;serverfqdn&gt;/_layouts/15/metadata/json/1</code></p></td>
</tr>
</tbody>
</table>


**Certificado de autenticação de servidor do Exchange 2013**

O programa de instalação do Exchange 2013 cria um certificado autoassinado com o nome amigável Certificado de autorização de servidor do Microsoft Exchange. O certificado é replicado para todos os servidores front-end na organização do Exchange 2013. A impressão digital do certificado é especificada na configuração de autorização do Exchange 2013, junto com o nome do serviço, um GUID conhecido que representa o Exchange 2013 no local. O Exchange usa a configuração de autorização para publicar o seu documento de metadados de autorização.


> [!IMPORTANT]
> O certificado de autenticação de servidor padrão criado pelo Exchange 2013 é válido por cinco anos. Você deve garantir que a configuração de autorização inclua um certificado atual.



Quando o Exchange 2013 recebe uma solicitação de acesso de um aplicativo de parceiro através dos Serviços Web do Exchange (EWS), ele analisa o cabeçalho `www-authenticate` da solicitação https, que contém o token de acesso assinado pelo servidor de chamada usando sua chave privada. O módulo de autenticação valida o token de acesso usando a configuração do aplicativo de parceiro. Em seguida, ele concede acesso a recursos com base nas permissões RBAC concedidas ao aplicativo. Se o token de acesso for em nome de um usuário, as permissões RBAC concedidas ao usuário são verificadas. Por exemplo, se um usuário realizar uma pesquisa de descoberta eletrônica usando o Centro de descoberta eletrônica no SharePoint 2013, o Exchange verifica se o usuário é membro do grupo de funções Gerenciamento de descoberta ou se tem a função Pesquisa de caixa de correio atribuída, e se as caixas de correio que estão sendo pesquisadas estão dentro do escopo da atribuição de função RBAC. Para mais detalhes, consulte [Permissões](permissions-exchange-2013-help.md).

## Gerenciar autenticação OAuth

Há dois objetos de configurações no Exchange 2013 que você precisa gerenciar para a autenticação OAuth com aplicativos de parceiros:

  - **AuthConfig**   O AuthConfig é criada pelo Exchange 2013 instalação e é usado para publicar os metadados de autenticação. Não é necessário gerenciar o config auth exceto to provisionar um novo certificado quando o certificado existente está prestes a expirar. Quando isso acontece, você pode renovar o certificado existente e configurar o novo certificado como o próximo certificado no AuthConfig juntamente com sua data efetiva. O novo certificado é replicado automaticamente para outros Exchange 2013 da organização, o documento de metadados de autenticação é atualizado com detalhes sobre o novo certificado e o AuthConfig muda para o novo certificado na data efetiva.

  - **Aplicativos de parceiros**   Para habilitar os aplicativos de parceiros solicitar tokens de acesso do Exchange 2013, você deve criar uma configuração do aplicativo de parceiro. Exchange 2013 fornece o script de `Configure-EnterprisePartnerApplication.ps1` , que permite que você rapidamente e facilmente cria configurações de aplicativo de parceiro e minimize os erros de configuração. Para obter informações detalhadas, consulte [Configurar a autenticação OAuth com o SharePoint 2013 e Lync 2013](configure-oauth-authentication-with-sharepoint-2013-and-lync-2013-exchange-2013-help.md).

