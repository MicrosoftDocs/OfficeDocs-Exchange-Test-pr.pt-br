---
title: 'Gerenciar uma confiança de Federação: Exchange 2013 Help'
TOCTitle: Gerenciar uma confiança de Federação
ms:assetid: 0439839f-2052-4bc9-9d30-aa6e7d51b733
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/JJ673036(v=EXCHG.150)
ms:contentKeyID: 50484885
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Gerenciar uma confiança de Federação

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2015-01-01_

Uma relação de confiança de Federação estabelece uma relação de confiança entre uma organização do Microsoft Exchange 2013 e o sistema de autenticação Azure Active Directory e oferece suporte a compartilhamento federado com outras organizações federadas do Exchange. Normalmente, você não deve ter que gerenciar ou modificar a confiança de Federação após sua criação. No entanto, pode haver circunstâncias que exigem a adição ou remoção de domínios federados ou redefinindo o domínio usado para configurar o identificador da organização (OrgID) para a confiança de Federação.


> [!TIP]
> A modificação de uma confiança de federação existente, especialmente no domínio compartilhado principal usado para definir o OrgID, pode interromper o compartilhamento federado entre as organizações do Exchange federadas ou para implantações híbridas com organizações do Office 365.



Para tarefas de gerenciamento adicionais relacionadas à Federação, consulte [Procedimentos de Federação](federation-procedures-exchange-2013-help.md).


> [!IMPORTANT]
> Esse recurso do Exchange Server 2013 não é totalmente compatível com o Office 365 operado pelo 21Vianet na China e pode haver algumas limitações de recurso. Para saber mais, confira o artigo <A href="https://go.microsoft.com/fwlink/?linkid=313640">Saiba mais sobre o Office 365 operado pelo 21Vianet</A>.



## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: 30 minutos.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada de permissões de *Federation and certificates* no tópico [Permissões de infraestrutura do Exchange e do Shell](exchange-and-shell-infrastructure-permissions-exchange-2013-help.md).

  - Você precisará adicionar um registro TXT ao seu DNS público para cada novo domínio federado adicionado à confiança de federação. Reveja os requisitos para adicionar um registro TXT com a organização que hospeda seus registros DNS públicos.

  - Para as finalidades deste tópico, uma confiança de federação existente foi definida com as seguintes configurações:
    
      - **Contoso.com** é o principal domínio compartilhado para a confiança de federação. (Esse domínio não será alterado.)
    
      - Os domínios federados **service.contoso.com** e **sales.contoso.com** estão incluídos na confiança de federação existente.
    
      - **Marketing.contoso.com** é um domínio aceito na organização do Exchange.

  - Este tópico também cobre outras tarefas de gerenciamento de federação, como exibição e gerenciamento de certificados usados para a confiança de federação e exibição de informações dos parâmetros de confiança de federação no Shell.

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

## O que você deseja fazer?

## Usar o EAC para gerenciar uma confiança de federação

1.  Em um servidor Exchange 2013 na organização local, navegue até **Organização** \> **Compartilhamento**.

2.  Na seção **Confiança de federação**, clique em **Modificar**.

3.  Em **Domínios habilitados para compartilhamento**, ignore a **Etapa 1** porque o domínio de compartilhamento principal não está mudando.

4.  Na **Etapa 2**, selecione o domínio **service.contoso.com** e depois clique em **Remover**![ícone Remover](images/JJ657492.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "ícone Remover") para remover o domínio da confiança federada.

5.  Na **Etapa 2**, clique em **Adicionar**![Ícone Adicionar](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Ícone Adicionar").

6.  Em **Selecionar Domínios Aceitos**, selecione **marketing.contoso.com** na lista de domínios aceitos e depois clique em **OK** para adicionar o domínio à confiança federada.
    

    > [!IMPORTANT]
    > Uma cadeia de caracteres de comprovação de domínio federada será criada para o domínio <STRONG>marketing.contoso.com</STRONG>. Você deve criar um registro TXT separado no seu DNS público para este domínio.



7.  Usando a cadeia de caracteres de comprovação de domínio federada para o domínio **marketing.contoso.com**, crie um registro de TXT no seu servidor DNS público. Dependendo do agendamento de atualização do seu host DNS público, a replicação de alterações de DNS podem levar 15 minutos ou mais.

8.  Após o registro TXT ser criado e replicado, clique em **Atualizar**.

## Usar o Shell para gerenciar uma confiança de federação

1.  Este exemplo remove o domínio service.contoso.com da federação de confiança.
    
    ```powershell
    Remove-FederatedDomain -DomainName service.contoso.com
    ```

2.  Este exemplo adiciona o domínio marketing.contoso.com à confiança de federação.
    
    ```powershell
    Add-FederatedDomain -DomainName marketing.contoso.com
    ```

Para obter informações detalhadas sobre sintaxe e parâmetros, consulte [Remove-FederatedDomain](https://technet.microsoft.com/pt-br/library/dd298128\(v=exchg.150\)) e [Add-FederatedDomain](https://technet.microsoft.com/pt-br/library/dd351208\(v=exchg.150\)).

Execute os seguintes comandos do Shell para gerenciar outros aspectos de uma confiança de federação:

1.  **Exibir o OrgID federado e domínios federados**
    
    Esse exemplo exibe o OrgID federado e informações relacionadas da organização do Exchange, incluindo domínios federados e status.
    
    ```powershell
    Get-FederatedOrganizationIdentifier
    ```

2.  **Exibir certificados de confiança de federação**
    
    Este exemplo exibe os certificados anteriores, atuais e futuros usados pela confiança de federação "Autenticação do Azure AD".
    
    ```powershell
    Get-FederationTrust "Azure AD authentication" | Select Org*certificate
    ```

3.  **Verificar o status dos certificados de federação**
    
    Este exemplo exibe o status de certificados de federação em todos os servidores de Caixa de Correio e Acesso para Cliente.
    
    ```powershell
    Test-FederationTrustCertificate
    ```

4.  **Configurar a confiança de federação para usar um certificado como o próximo certificado**
    
    Este exemplo configura a confiança de federação "Autenticação do Azure AD" para usar o certificado com a miniatura fornecida como o próximo certificado. Depois que o certificado for implantado em todos os servidores do Exchange na organização,você poder usar a opção *PublishCertificate* para configurar a confiança de federação para usar esse certificado como o atual.
    
    ```powershell
    Set-FederationTrust "Azure AD authentication" -Thumbprint AC00F35CBA8359953F4126E0984B5CCAFA2F4F17
    ```

5.  **Configurar a confiança de federação para usar o próximo certificado como o certificado atual**
    
    Este exemplo configura a autenticação do Azure AD de confiança de federação para usar o próximo certificado como o certificado atual e publicá-lo para o sistema de autenticação AD do Azure.
    
    ```powershell
    Set-FederationTrust "Azure AD authentication" -PublishFederationCertificate
    ```
    

    > [!WARNING]
    > Antes de configurar a confiança de federação para usar o certificado seguinte como o atual, verifique se o certificado foi implantado em todos os servidores do Exchange em sua organização. Use o cmdlet <A href="https://technet.microsoft.com/pt-br/library/dd335228(v=exchg.150)">Test-FederationTrustCertificate</A> para verificar o status de implantação do certificado.



6.  **Atualizar os metadados de Federação e o certificado do sistema de autenticação do AD do Azure**
    
    Este exemplo atualiza os metadados de Federação e o certificado do sistema de autenticação AD do Azure para a autenticação de Azure AD de confiança de Federação.
    
    ```powershell
    Set-FederationTrust "Azure AD authentication" -RefreshMetadata
    ```

Para obter informações detalhadas sobre sintaxes e parâmetros, consulte os seguintes tópicos:

  - [Get-FederatedOrganizationIdentifier](https://technet.microsoft.com/pt-br/library/dd298149\(v=exchg.150\))

  - [Get-FederationTrust](https://technet.microsoft.com/pt-br/library/dd351262\(v=exchg.150\))

  - [Test-FederationTrustCertificate](https://technet.microsoft.com/pt-br/library/dd335228\(v=exchg.150\))

  - [Set-FederationTrust](https://technet.microsoft.com/pt-br/library/dd298034\(v=exchg.150\))

## Como saber se funcionou?

A conclusão bem-sucedida do assistente **Domínios habilitados para compartilhamento** é a primeira indicação de que você configurou a confiança de federação conforme o esperado.

Para verificar o sucesso, execute o seguinte procedimento:

1.  Execute o seguinte comando do Shell para verificar as informações de confiança de federação.
    
    ```powershell
    Get-FederationTrust | format-list
    ```

2.  Execute o comando do Shell para verificar se as informações de federação podem ser recuperadas da sua organização. Por exemplo, verifique se os domínios sales.contoso.com e marketing.contoso.com são retornados no parâmetro *DomainNames*.
    
    ```powershell
    Get-FederationInformation -DomainName <your primary sharing domain>
    ```


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>.


