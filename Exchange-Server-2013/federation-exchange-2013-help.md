---
title: 'Federação: Exchange 2013 Help'
TOCTitle: Federação
ms:assetid: 0046e2eb-6940-4941-bd5b-cbe6bffa3b94
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Dd335047(v=EXCHG.150)
ms:contentKeyID: 50484856
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Federação

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2016-12-09_

Pessoas que trabalham com informações frequentemente precisam colaborar com destinatários externos, fornecedores, parceiros e clientes e compartilhar suas informações de disponibilidade (o que também é conhecido como disponibilidade de calendário). A federação no Microsoft Exchange Server 2013 ajuda nesses esforços de colaboração. *Federação* se refere à infraestrutura de confiança subjacente que oferece suporte ao *compartilhamento federado*, um método fácil para os usuários compartilharem informações de calendário com destinatários de organizações federadas externas. Para saber mais sobre compartilhamento federado, consulte [Compartilhamento](sharing-exchange-2013-help.md).


> [!IMPORTANT]
> Esse recurso do Exchange Server 2013 não é totalmente compatível com o Office 365 operado pelo 21Vianet na China e pode haver algumas limitações de recurso. Para saber mais, confira o artigo <A href="https://go.microsoft.com/fwlink/?linkid=313640">Saiba mais sobre o Office 365 operado pelo 21Vianet</A>.



**Sumário**

Key terminology

Sistema de autenticação do Windows Azure AD

Federation trust

Federated organization identifier

Federation example

Certificate requirements for Federation

Transitioning to a new certificate

Firewall Considerations for Federation

## Terminologia principal

A tabela a seguir define os componentes principais associadas à federação no Exchange 2013.

  - **identificador de aplicativo (AppID)**  
    Um número exclusivo gerado pelo sistema de autenticação Azure Active Directory para identificar Exchange organizações. A AppID é gerada automaticamente quando você cria uma relação de confiança de federação com o sistema de autenticação Azure Active Directory.

<!-- end list -->

  - **token de delegação**  
    Um token de SAML Security Assertion Markup Language () emitido pelo sistema de autenticação Azure Active Directory que permite aos usuários de uma organização federada confiança outra organização federada. Um token de delegação contém informações associadas a oferta de para o qual o token emitido para ação, um identificador imutável e endereço de email do usuário.

<!-- end list -->

  - **organização federada externa**  
    Uma organização externa Exchange que estabeleceu uma confiança de federação com o sistema de autenticação Azure Active Directory.

<!-- end list -->

  - **compartilhamento federado**  
    Um grupo de recursos de Exchange que aproveitam uma confiança de federação com o sistema de autenticação Azure Active Directory para trabalhar em organizações Exchange, incluindo locais cruzados Exchange implantações. Juntos, esses recursos são usados para fazer solicitações autenticadas entre os servidores em nome de usuários em organizações de vários Exchange.

<!-- end list -->

  - **domínio federado**  
    Um domínio autoritativo aceito adicionado ao identificador da organização (OrgId) para uma organização do Exchange.

<!-- end list -->

  - **cadeia de caracteres de criptografia de prova de domínio**  
    Uma cadeia de caracteres criptograficamente segura usada por uma organização Exchange para fornecer uma prova de que a organização possui o domínio usado com o sistema de autenticação Azure Active Directory. A cadeia de caracteres é gerada automaticamente quando usando o Assistente para **Habilitar a confiança de Federação** ou pode ser gerado usando o cmdlet **Get-FederatedDomainProof** .

<!-- end list -->

  - **diretiva de compartilhamento federado**  
    Uma política no nível da organização que habilita e controla o compartilhamento estabelecido pelo usuário, de pessoa para pessoa, das informações de calendário.

<!-- end list -->

  - **federação**  
    Um acordo baseado em confiança entre duas organizações do Exchange para atingir um propósito comum. Com a federação, as duas organizações querem que asserções de autenticação de uma sejam reconhecidas pela outra.

<!-- end list -->

  - **confiança de federação**  
    Uma relação com o sistema de autenticação Azure Active Directory que define os seguintes componentes para sua organização Exchange:
    
      - Namespace de conta
    
      - Identificador de aplicativo (AppID)
    
      - Identificador de organização (OrgID)
    
      - Domínios federados
    
    Para configurar o compartilhamento federado com outras organizações federadas Exchange, uma confiança de federação deve ser estabelecida com o sistema de autenticação Azure Active Directory.

<!-- end list -->

  - **organização não federada**  
    Organizações que não têm uma relação de confiança de Federação estabelecida com o sistema de autenticação Azure Active Directory.

<!-- end list -->

  - **identificador de organização (OrgID)**  
    Define a qual dos domínios autoritativos aceitos configurados em uma organização estão habilitados para federação. Somente os destinatários que possuem endereços de email com domínios federados configurados no OrgID são reconhecidos pelo sistema de autenticação Azure Active Directory e são capazes de usar recursos de compartilhamento federado. O OrgID é uma combinação de uma cadeia de caracteres pré-definidos e o domínio aceito primeiro selecionado para a federação no Assistente para **Habilitar a confiança de Federação**. Por exemplo, se você especificar o domínio federado contoso.com como o domínio de SMTP principal da sua organização, o namespace de conta FYDIBOHF25SPDLT.contoso.com será automaticamente criado como o OrgID para a confiança de Federação.

<!-- end list -->

  - **relação de organização**  
    Um relacionamento individual entre duas organizações federadas Exchange que permite que os destinatários compartilhar informações de livre/ocupado (disponibilidade de calendário). Um relacionamento de organização requer uma relação de confiança de federação com o sistema de autenticação Azure Active Directory e substitui a necessidade de usar Active Directory confianças de floresta ou domínio entre organizações Exchange.

<!-- end list -->

  - **sistema de autenticação Azure Active Directory**  
    Um serviço de identidade gratuita baseada na nuvem, que atua como o agente de confiança entre organizações federadas de Exchange Microsoft. Ele é responsável por emitindo tokens de delegação para destinatários Exchange, quando eles solicitam informações de destinatários em outras organizações federadas Exchange. Para saber mais, consulte [Active Directory do Azure](https://go.microsoft.com/fwlink/?linkid=392500).

## Sistema de autenticação do Windows Azure AD

O sistema de autenticação Azure Active Directory, um serviço de nuvem gratuito oferecido pela Microsoft, atua como o agente de confiança entre sua organização local do Exchange 2013 e outros federados Exchange 2010 e Exchange 2013 organizações. Se você deseja configurar a federação na sua organização Exchange, é necessário estabelecer uma confiança de Federação ocasional com o sistema de autenticação Azure Active Directory, para que ele pode se tornar um parceiro de federação com sua organização. Com essa confiança in-loco, os usuários autenticados pelo Active Directory (conhecido como *provedores de identidade*) são Security Assertion Markup Language (SAML) delegação tokens emitidos pelo sistema de autenticação AD do Azure. Esses tokens de delegação permitem que os usuários da organização federado um Exchange outra organização federada Exchange a confiança. Com o sistema de autenticação AD do Azure atuando como o agente de confiança, as organizações não são necessárias para estabelecer relações de confiança individuais de vários com outras organizações e os usuários podem acessar os recursos externos usando uma experiência de logon único (SSO). Para obter mais informações, consulte [Active Directory do Azure](https://go.microsoft.com/fwlink/?linkid=392500).

Voltar ao início

## Confiança de federação

Para usar os recursos de compartilhamento de Exchange 2013 federado, você precisa estabelecer uma confiança de federação entre sua organização de Exchange 2013 e o sistema de autenticação de AD do Azure. Estabelecer uma confiança de federação com o sistema de autenticação AD do Azure troca de certificado de segurança digital da sua organização com o sistema de autenticação AD do Azure e recupera os metadados de certificado e federação de sistema do autenticação AD do Azure. Você pode estabelecer uma confiança de Federação usando o assistente **Habilitar a confiança de Federação** no Centro de administração do Exchange (EAC) ou o cmdlet **New-FederationTrust** no Exchange Management Shell. Um certificado autoassinado é criado automaticamente pelo Assistente para **Habilitar a confiança de Federação** e é usado para assinatura e criptografia de tokens de delegação do sistema de autenticação do AD do Azure que permitem aos usuários a confiança externas organizações federadas. Para obter detalhes sobre os requisitos de certificado, consulte Requisitos de certificado para federação posteriormente neste tópico.

Quando você cria uma relação de confiança de federação com o sistema de autenticação AD do Azure, um *identificador de aplicativo* (AppID) é gerado para sua organização Exchange e fornecidas na saída do cmdlet **Get-FederationTrust** automaticamente. A AppID é usada pelo sistema de autenticação AD do Azure para identificar exclusivamente a sua organização Exchange. Ele também é usado pela organização Exchange para fornecer prova de que sua organização possui o domínio para uso com o sistema de autenticação AD do Azure. Isso é feito criando um registro de texto (TXT) na zona de (DNS) do sistema de nomes de domínio público para cada domínio federado.

Voltar ao início

## Identificador de organização federada

O *federados identificador da organização* (OrgID) define quais dos domínios autoritativos aceitos configurados em sua organização estão habilitados para federação. Somente os destinatários que possuem endereços de email com domínios aceitos configurados no OrgID são reconhecidos pelo sistema de autenticação AD do Azure e são capazes de usar recursos de compartilhamento federado. Quando você cria uma nova relação de confiança de federação, um OrgID é criado automaticamente com o sistema de autenticação AD do Azure. Este OrgID é uma combinação de uma cadeia de caracteres pré-definidos e o domínio aceito selecionado como o domínio compartilhado principal no assistente. Por exemplo, no Assistente de domínios de Edit Sharing-Enabled, se você especificar o domínio federado **contoso.com** como o domínio compartilhado principal em sua organização, o namespace de conta **FYDIBOHF25SPDLT.contoso.com** será automaticamente criado como o OrgID para a confiança de federação para sua organização Exchange.

Embora normalmente o domínio SMTP primário para a organização Exchange, esse domínio não precisa ser um domínio aceito na sua organização do Exchange e não exige um domínio nome DNS (sistema) prova de propriedade registro TXT. O único requisito é que os domínios aceitos selecionados seja federado são limitados a um máximo de 32 caracteres. O único objetivo deste subdomínio é servir como o namespace federado para o sistema de autenticação AD do Azure manter os identificadores exclusivos para destinatários que tokens de delegação de SAML de solicitação. Para obter mais informações sobre tokens SAML, consulte [Tokens SAML e declarações](https://go.microsoft.com/fwlink/?linkid=198561)

Você pode adicionar ou remover os domínios aceitos da confiança de federação, a qualquer momento. Para habilitar ou desabilitar todos os recursos de compartilhamento de federação da sua organização, tudo o que você tem a fazer é habilitar ou desabilitar o OrgID da confiança de federação.


> [!IMPORTANT]
> Se você alterar o OrgID, os domínios aceitos ou o AppID usado para confiança de federação, todos os recursos de compartilhamento de federação serão afetados em sua organização. Isso também afeta as organizações do Exchange federadas externas, incluindo o Exchange Online e configurações de implantação híbrida. Recomendamos notificar todos os parceiros federados externos sobre todas as alterações efetuadas nessas configurações de confiança de federação.



Voltar ao início

## Exemplo de federação

Duas organizações Exchange, Contoso, Ltd. e Fabrikam, Inc., queiram que os usuários possam compartilhar informações de disponibilidade de calendário uns com os outros. Cada organização cria uma confiança de federação com o sistema de autenticação AD do Azure e configura o seu namespace de conta para incluir o domínio usado para o domínio do endereço de email do seu usuário.

Os funcionários da Contoso usam um dos domínios de endereço de email a seguir: contoso.com, contoso.co.uk ou contoso.ca. Os funcionários da Fabrikam usam um dos seguintes domínios de endereço de email: fabrikam.com, fabrikam.org ou fabrikam.net. Ambas as organizações Certifique-se de que todos aceitas domínios de email estão incluídos no namespace da conta para seu confiança de federação com o sistema de autenticação AD do Azure. Em vez de exigir um complexo Active Directory floresta ou domínio configuração de confiança entre as duas organizações, ambas as organizações configurar um relacionamento de organização com os outros para habilitar o compartilhamento de disponibilidade de calendário.

A seguinte figura mostra a configuração de federação entre Contoso, Ltd. e Fabrikam, Inc.

**Exemplo de compartilhamento federado**

![Relações de Confiança de Federação e Compartilhamento Federado](images/Dd335047.310f0698-b67d-4b0e-91e4-231c6e9db952(EXCHG.150).gif "Relações de Confiança de Federação e Compartilhamento Federado")

## Requisitos de certificado para federação

Para estabelecer uma confiança de federação com o sistema de autenticação AD do Azure, um certificado autoassinado ou um certificado x. 509 assinado por uma autoridade de certificação (CA) deve ser criado e instalado no servidor de Exchange 2013 usado para criar a relação de confiança. É altamente recomendável usar um certificado autoassinado, que é automaticamente criado e instalado usando o Assistente para **Habilitar a confiança de Federação** no EAC. Esse certificado é usado somente para assinar e criptografar tokens de delegação usados para compartilhamento federado e apenas um certificado é necessário para a confiança de Federação. Exchange 2013 distribui automaticamente o certificado a todos os outros servidores Exchange 2013 na organização.

Se quiser usar um certificado X.509 assinado por um CA externo, o certificado deverá atender aos seguintes requisitos:

  - **CA confiável**   Se possível, o certificado SSL X.509 deve ser emitido por um CA de confiança do Windows Live. No entanto, você pode usar certificados emitidos pelos CAs que atualmente não estejam certificados pela Microsoft. Para uma lista atual de CAs de confiança, consulte [Autoridades de certificação raiz confiáveis para confianças de federação](trusted-root-certification-authorities-for-federation-trusts-exchange-2013-help.md).

  - **Identificador de chave do requerente**   O certificado deve ter um campo de identificador de chave do requerente. A maioria doa certificados X.509 emitidos por CAs comerciais tem esse identificador.

  - **CryptoAPI provedor de serviços de criptografia (CSP)**   O certificado deve usar um CSP CryptoAPI. Certificados que usam a API de criptografia: provedores CNG Next Generation () não são suportados para federação. Se você usar Exchange para criar uma solicitação de certificado, um provedor de CryptoAPI é usado. Para obter mais informações, consulte [API de criptografia: próxima geração](https://go.microsoft.com/fwlink/?linkid=187890).

  - **Algoritmo de assinatura RSA** O certificado deve usar RSA como o algoritmo de assinatura.

  - **Chave privada exportável**   A chave privada usada para gerar o certificado deve ser exportável. Você pode especificar que a chave privada seja exportável, quando você criar a solicitação de certificado usando o assistente **Novo certificado do Exchange** no EAC ou no cmdlet [New-ExchangeCertificate](https://technet.microsoft.com/pt-br/library/aa998327\(v=exchg.150\)) no Shell.

  - **Certificado atual**   O certificado deve ser atual. Não é possível usar um certificado expirado ou revogado para criar uma confiança de federação.

  - **Uso avançado de chave**   O certificado deve incluir o tipo de uso avançado de chave (EKU) **Autenticação de Cliente (1.3.6.1.5.5.7.3.2)**. Esse tipo de uso é feito para provar sua identidade a um computador remoto. Se você usar o EAC ou o Shell para gerar uma solicitação de certificado, esse tipo de uso será incluído por padrão.


> [!NOTE]  
> Como o certificado não é usado para autenticação, ele não tem nenhum requisito de nome do requerente ou nome alternativo do requerente. Você pode usar um certificado com um nome de assunto que é o mesmo do nome de host, do nome de domínio ou de qualquer outro nome.



Voltar ao início

## Fazer a transição para um novo certificado

O certificado usado para criar a confiança de federação é designado como o certificado atual. Entretanto, pode ser preciso instalar e usar um novo certificado para a confiança de federação periodicamente. Por exemplo, poderá haver a necessidade de usar um novo certificado se o certificado atual expirar ou para atender a um novo requisito comercial ou de segurança. Para garantir uma transição perfeita para um novo certificado, você precisa instalar o novo certificado no seu servidor Exchange 2013 e configurar a confiança de federação para designá-la como o próximo certificado. O Exchange 2013 automaticamente distribui o novo certificado a outros servidores Exchange 2013 na organização. Dependendo de sua topologia do Active Directory, a distribuição do certificado pode levar algum tempo. Você pode verificar o status do certificado, usando o cmdlet [Test-FederationTrustCertificate](https://technet.microsoft.com/pt-br/library/dd335228\(v=exchg.150\)) no Shell.

Depois de verificar o status de distribuição do certificado, você pode configurar a confiança para usar o novo certificado. Após a troca de certificados, o certificado atual é designado como o certificado anterior e o novo certificado é designado como o certificado atual. O novo certificado é publicado para o sistema de autenticação AD do Azure, e todos os tokens novos trocados com o sistema de autenticação AD do Azure criptografados usando o novo certificado.


> [!NOTE]  
> Esse processo de transição de certificado é usado apenas pela federação. Se você usar o mesmo certificado para outros recursos do Exchange 2013 que exijam certificados, será preciso levar os requisitos de recursos em consideração ao planejar a aquisição, a instalação ou a transição para um novo certificado.



Voltar ao início

## Considerações de firewall para Federação

Os recursos de Federação exigem que os servidores de Caixa de Correio e Acesso para Cliente na sua organização tenham acesso de saída para a Internet via HTTPS. Você deve permitir o acesso HTTPS de saída (porta 443 para TCP) para todos os servidores de Caixa de Correio e Acesso para Cliente do Exchange 2013 na organização.

Para uma organização externa acessar as informações de disponibilidade da sua organização, é preciso publicar um servidor de Acesso para Cliente na Internet. Isso requer acesso HTTPS de entrada da Internet para o servidor de Acesso para Cliente. Os servidores de Acesso para Cliente nos sites do Active Directory que não tenham um servidor de Acesso para Cliente publicado na Internet podem usar os servidores de Acesso para Cliente em outros sites do Active Directory que possam ser acessados da Internet. Os servidores de Acesso para Cliente que não são publicados na Internet devem ter a URL externa do diretório virtual de serviços da Web definida com a URL que é visível para organizações externas.

[Voltar ao início](sharing-exchange-2013-help.md)

