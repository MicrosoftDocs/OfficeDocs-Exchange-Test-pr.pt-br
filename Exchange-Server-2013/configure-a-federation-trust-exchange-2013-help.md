---
title: 'Configurar uma confiança de Federação: Exchange 2013 Help'
TOCTitle: Configurar uma confiança de Federação
ms:assetid: 7c2b539f-faed-4374-8578-9f329ca628db
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/JJ657462(v=EXCHG.150)
ms:contentKeyID: 50485987
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configurar uma confiança de Federação

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2017-07-26_

Uma relação de confiança de Federação estabelece uma relação de confiança entre uma organização do Microsoft Exchange 2013 e o sistema de autenticação Azure Active Directory. Configurando uma relação de confiança de federação, você pode configurar o compartilhamento federado com outras organizações federadas do Exchange para compartilhar informações de disponibilidade de calendário entre destinatários. Compartilhamento federado pode ser configurado entre duas organizações federadas Exchange 2013 ou entre uma organização federada Exchange 2013 e organizações federadas Exchange 2010. Você também pode definir o compartilhamento com uma organização do Office 365.


> [!TIP]
> Criar uma confiança de federação é uma das várias etapas da configuração do compartilhamento federado em sua organização do Exchange. Para examinar todas as etapas, consulte <A href="configure-federated-sharing-exchange-2013-help.md">Configurar o compartilhamento federado</A>.



Para tarefas de gerenciamento adicionais relacionadas à dederação, consulte [Procedimentos de Federação](federation-procedures-exchange-2013-help.md).


> [!IMPORTANT]
> Esse recurso do Exchange Server 2013 não é totalmente compatível com o Office 365 operado pelo 21Vianet na China e pode haver algumas limitações de recurso. Para saber mais, confira o artigo <A href="https://go.microsoft.com/fwlink/?linkid=313640">Saiba mais sobre o Office 365 operado pelo 21Vianet</A>.



## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: 30 minutos.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada de permissões de "Certificados e federação" no tópico [Permissões de infraestrutura do Exchange e do Shell](exchange-and-shell-infrastructure-permissions-exchange-2013-help.md) .

  - O domínio utilizado para estabelecer uma confiança de federação deve ser determinado a partir da Internet. Isso requer que o domínio seja registrado em um registrador de domínios e que a zona DNS do domínio seja hospedada em um servidor DNS acessível pela Internet. Se a organização recebe emails da Internet no domínio, você já possui os requisitos necessários.

  - Você precisará adicionar um registro em TXT para seu DNS público. Reveja os requisitos para adicionar um registro TXT com a organização que hospeda seus registros DNS públicos.

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

  - Ambas as organizações de Exchange em uma relação de compartilhamento federada devem usar o mesmo sistema de autenticação AD do Azure para seus confianças de Federação. Esse requisito se aplica ao configurar o compartilhamento federado entre duas organizações do local Exchange ou entre uma organização de Exchange local e uma organização Exchange hospedados pelo [Office 365](https://go.microsoft.com/fwlink/?linkid=392576).

  - Quando você cria uma relação de confiança de federação com o sistema de autenticação AD do Azure para sua organização Exchange 2013, a relação de confiança de Federação usará a instância comercial do sistema de autenticação AD do Azure. No entanto, outras organizações federadas do Exchange com versões anteriores do Exchange e relações de confiança de Federação existentes podem estar usando a instância comercial ou do consumidor do sistema de autenticação AD do Azure.
    
    As seguintes organizações Exchange usam a instância comercial do sistema de autenticação AD do Azure por padrão:
    
      - organizações do Exchange 2013, usando o assistente para **Habilitar a confiança de federação** e certificados autoassinados para uma confiança de federação.
    
      - Exchange 2010 SP1 ou posteriores organizações usando o Assistente de **Nova relação de confiança de Federação** e certificados autoassinados para uma confiança de Federação.
    
      - Organizações do Exchange hospedadas pelo Office 365, como o Exchange Online.
    
    As seguintes organizações Exchange usam a instância de consumidor do sistema de autenticação AD do Azure por padrão:
    
      - Versão Release to manufacturing (RTM) das organizações Exchange 2010 usando certificados emitidos por autoridades de certificação de terceiros.
    
    É recomendável que todas as organizações Exchange usam a instância comercial do sistema de autenticação AD do Azure para confianças de Federação. Antes de configurar o compartilhamento federado entre as duas organizações do Exchange, você precisará verificar qual instância de sistema de autenticação AD do Azure cada organização Exchange você está usando para qualquer confianças de Federação existente. Para determinar qual instância de sistema de autenticação AD do Azure uma organização Exchange você está usando para uma confiança de Federação existente, execute o seguinte comando no Shell.
    
        Get-FederationInformation -DomainName <hosted Exchange domain namespace>
    
    A instância de empresa retorna um valor de `<uri:federation:MicrosoftOnline>` para o parâmetro *TokenIssuerURIs*.
    
    A instância de consumidor retorna um valor de `<uri:WindowsLiveID>` para o parâmetro *TokenIssuerURIs*.
    
    Para configurar o compartilhamento federado com uma organização Exchange que tem uma confiança de Federação existente que está usando a instância comercial do sistema de autenticação AD do Azure, siga as etapas neste tópico. Estas etapas são você só precisa realizar para criar relações de confiança de federação que podem ser usadas para habilitar o compartilhamento federado entre duas organizações Exchange 2013 ou entre uma organização Exchange 2013 e uma organização Exchange 2010 que já está usando o instância comercial do sistema de autenticação AD do Azure.
    
    Para configurar o compartilhamento federado entre sua organização Exchange 2013 e uma organização de Exchange que tem uma confiança de Federação existente que está usando a instância de consumidor do sistema de autenticação AD do Azure, a organização do Exchange usando a instância de consumidor deve instalar o Exchange 2010 SP2 ou posterior, ou atualizar para o Exchange 2013. Se você decidir instalar o Exchange 2010 SP2 ou posterior, use o Assistente de **Nova relação de confiança de Federação** para remover e recriar os domínios federados existentes e relações de confiança de Federação. Quando as relações de confiança de Federação são recriadas, a instância comercial do sistema de autenticação AD do Azure será usada.

## Usar o EMC para criar e configurar uma confiança de federação

1.  Em um servidor Exchange 2013 na organização local, navegue até **Organização** \> **Compartilhamento**.

2.  Clique em **Permitir**, para iniciar o assistente para **Habilitar a confiança de federação**.

3.  Depois que o assistente for concluído, clique em **Fechar**.

4.  Na seção **Confiança de Federação** da guia **Compartilhamento**, clique em **Modificar**.

5.  Em **Domínios Habilitados para Compartilhamento**, próximo a **Passo 1**, clique em **Procurar**.

6.  Em **Selecionar Domínios Aceitos**, selecione o domínio compartilhado principal da lista e clique em **OK**.
    

    > [!TIP]
    > O domínio que você selecionar será usado para configurar a OrgID para a confiança de federação. Para mais informações sobre a OrgID, consulte <A href="federation-exchange-2013-help.md">Federação</A>.



7.  Anote a prova de domínio federado é gerada para o domínio compartilhado principal. Você usará essa cadeia de caracteres para criar um registro TXT no seu servidor DNS público.
    

    > [!IMPORTANT]
    > A prova de domínio federado é uma cadeia de caracteres alfanuméricos. Para evitar erros de entrada, recomendamos que você copie a cadeia de caracteres no EAC e colá-lo em um editor de texto como o bloco de notas. Você pode copiá-lo a partir do editor de texto na área de transferência e cole-o no campo de <STRONG>texto</STRONG> ao criar o registro TXT. Se o registro TXT é criado utilizando um incorretas federados sequência de prova de domínio, o sistema de autenticação AD do Azure não conseguirá verificar prova de propriedade de domínio e não será possível adicioná-lo ao identificador da organização federada.



8.  Na **etapa 2**, clique em **Adicionar**![Ícone Adicionar](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Ícone Adicionar") para adicionar domínios adicionais à confiança federada para endereços de email que será usado pelos usuários em sua organização que exigem recursos de compartilhamento federados. Por exemplo, se você tiver usuários que usam um subdomínio no seu endereço de email como sales.contoso.com, seria adicionar o domínio sales.contoso.com à confiança de Federação.
    

    > [!TIP]
    > Uma cadeia de caracteres de prova de domínio federado será criada para cada domínio adicional selecionado. Você deverá criar registros TXT separados no seu DNS público para cada domínio adicional.



9.  Usando as cadeias de caracteres de prova de domínio federado para cada domínio, crie registros TXT para cada um desses domínios no seu servidor de DNS público. Dependendo do agendamento de atualização do seu host DNS público, a replicação de alterações de DNS podem levar 15 minutos ou mais.

10. Depois que os registros TXT forem criados e replicados, clique em **Atualizar**.

## Usar o Shell para criar e configurar uma confiança de federação

1.  Execute este comando para criar um identificador de chave de assunto exclusivo para o certificado de confiança de Federação:
    
        $ski = [System.Guid]::NewGuid().ToString("N")

2.  Use esta sintaxe para criar um certificado autoassinado para a confiança de Federação:
    
        New-ExchangeCertificate -FriendlyName "<Descriptive Name>" -DomainName <domain> -Services Federation -KeySize 2048 -PrivateKeyExportable $true -SubjectKeyIdentifier $ski
    
    Este exemplo cria um certificado autoassinado para a confiança de federação com o sistema de autenticação AD do Azure. O certificado usa o valor de nome amigável Exchange Federated Sharing e o valor de domínio é recuperado na variável de ambiente **USERDNSDOMAIN** .
    
        New-ExchangeCertificate -FriendlyName "Exchange Federated Sharing" -DomainName $env:USERDNSDOMAIN -Services Federation -KeySize 2048 -PrivateKeyExportable $true -SubjectKeyIdentifier $ski

3.  Para criar a relação de confiança de Federação e implantar automaticamente o certificado autoassinado que você criou na etapa anterior para os servidores de Exchange em sua organização, use esta sintaxe:
    
        Get-ExchangeCertificate | ?{$_.FriendlyName -eq "<FriendlyName>"} | New-FederationTrust -Name "<Descriptive Name>"
    
    Este exemplo cria a confiança de Federação chamada autenticação do Azure AD e implanta o certificado autoassinado denominado Exchange Federated Sharing.
    
        Get-ExchangeCertificate | ?{$_.FriendlyName -eq "Exchange Federated Sharing"} | New-FederationTrust -Name "Azure AD Authentication"

4.  Use esta sintaxe para retornar a prova de propriedade de domínio registro TXT que é necessário para qualquer domínio que você vai configurar para a confiança de Federação.
    
        Get-FederatedDomainProof -DomainName <domain>
    
    Este exemplo retorna a prova de propriedade de domínio registro TXT que é necessário para o domínio compartilhado principal de contoso.com.
    
        Get-FederatedDomainProof -DomainName contoso.com
    
    **Observações**:
    
      - Cada domínio ou subdomínio que está configurado para a confiança de Federação requer uma prova de propriedade do domínio registro TXT, portanto, talvez seja necessário executar este comando várias vezes usando valores de diferentes *DomainName* .
    
      - Recomendamos que você copie a cadeia de caracteres de prova de domínio clicando duas vezes no Shell, selecionando **marca**, selecionando o valor de **prova** e pressionando Enter para que possa usá-lo ao criar o registro TXT. Se você criar o registro TXT com uma cadeia de caracteres de prova de domínio federado incorreto, o sistema de autenticação AD do Azure não foi possível verificar sua propriedade do domínio e não será possível adicioná-lo ao identificador da organização federada.

5.  Usando as informações da etapa anterior, crie registros TXT no seu servidor DNS público em cada domínio que será incluído na relação de confiança de Federação. Dependendo o agendamento de atualização do seu host DNS público, replicação das alterações DNS pode levar 15 minutos ou mais. Continue depois de confirmar que os novos registros TXT estão disponíveis.

6.  Execute este comando para recuperar os metadados e o certificado de AD do Azure:
    
        Set-FederationTrust -RefreshMetadata -Identity "Azure AD authentication"

7.  Use esta sintaxe para configurar o domínio compartilhado principal para a confiança de federação que você criou na etapa 3. O domínio que você especificar será usado para configurar o identificador da organização (OrgID) para a confiança de Federação. Para obter mais informações sobre o OrgID, consulte [o identificador de organização federada](federation-exchange-2013-help.md).
    
        Set-FederatedOrganizationIdentifier -DelegationFederationTrust "<Federation Trust Name>" -AccountNamespace <Accepted Domain> -Enabled $true
    
    Este exemplo configura o domínio aceito contoso.com como o principal shared domínio para a confiança de Federação denominado autenticação do Azure AD.
    
        Set-FederatedOrganizationIdentifier -DelegationFederationTrust "Azure AD authentication" -AccountNamespace contoso.com -Enabled $true

8.  Para adicionar outros domínios à confiança de federação, use esta sintaxe:
    
        Add-FederatedDomain -DomainName <AdditionalDomain>
    
    Este exemplo adiciona o subdomínio sales.contoso.com à confiança federada, porque os usuários com endereços de email no domínio sales.contoso.com exigem recursos de compartilhamento federados.
    
        Add-FederatedDomain -DomainName sales.contoso.com
    
    Lembre-se de que qualquer domínio ou subdomínio que você adicionar a confiança de Federação requer uma prova de propriedade do domínio registro TXT,

Para detalhadas sobre sintaxe e informações de parâmetro, consulte [New-ExchangeCertificate](https://technet.microsoft.com/pt-br/library/aa998327\(v=exchg.150\)), [New-FederationTrust](https://technet.microsoft.com/pt-br/library/dd351047\(v=exchg.150\)), [Get-FederatedDomainProof](https://technet.microsoft.com/pt-br/library/ff717833\(v=exchg.150\)), [Set-FederationTrust](https://technet.microsoft.com/pt-br/library/dd298034\(v=exchg.150\)), [Set-FederatedOrganizationIdentifier](https://technet.microsoft.com/pt-br/library/dd351037\(v=exchg.150\))e [Add-FederatedDomain](https://technet.microsoft.com/pt-br/library/dd351208\(v=exchg.150\)).

## Como saber se funcionou?

A conclusão com êxito dos assistentes **Habilitar confiança de federação** e **Domínios Habilitados para Compartilhamento** será sua primeira indicação que a confiança de federação foi configurada como o esperado.

Para verificar com mais profundidade se você criou e configurou a confiança de federação com êxito, faça o seguinte:

1.  Execute o seguinte comando do Shell para verificar as informações de confiança de federação.
    
        Get-FederationTrust | Format-List

2.  Substitua *\<PrimarySharedDomain\>* seu domínio compartilhado principal e execute o seguinte comando Shell para verificar se as informações de federação podem ser recuperadas da sua organização.
    
        Get-FederationInformation -DomainName <PrimarySharedDomain>

Para obter informações detalhadas sobre sintaxe e parâmetros, consulte [Get-FederationTrust](https://technet.microsoft.com/pt-br/library/dd351262\(v=exchg.150\)) e [Get-FederationInformation](https://technet.microsoft.com/pt-br/library/dd351221\(v=exchg.150\)).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>.


