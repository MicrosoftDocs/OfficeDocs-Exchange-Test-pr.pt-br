---
title: 'Configurar as pastas públicas herdadas nas quais as caixas de correio dos usuários estão em servidores do Exchange 2013: Exchange 2013 Help'
TOCTitle: Configurar as pastas públicas herdadas nas quais as caixas de correio dos usuários estão em servidores do Exchange 2013
ms:assetid: 1d5ca19e-696e-4054-a634-15dd34d952b7
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Dn690134(v=EXCHG.150)
ms:contentKeyID: 62281152
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configurar as pastas públicas herdadas nas quais as caixas de correio dos usuários estão em servidores do Exchange 2013

 

_**Aplica-se a:** Exchange Server 2013, Exchange Server 2016_

_**Tópico modificado em:** 2017-03-27_

Como permitir que os usuários do Exchange 2013 ou Exchange 2016 como acesso Exchange 2010 ou pastas públicas anteriores (também conhecido como pastas de públicas herdadas).

## O que você precisa saber antes de começar?

Usuários cujas caixas postais estão no Exchange Server 2013 ou Exchange Server 2016 não conseguirá acessar pastas públicas herdadas do Outlook Web App, Outlook na web ou o Outlook para Mac. As etapas neste artigo funcionam para o Exchange 2013 e Exchange 2016.


> [!NOTE]
> 2016 do Outlook para usuários do Mac podem acessar pastas públicas herdadas após seguir as etapas neste artigo. Se os clientes na sua organização usarem 2016 do Outlook para Mac, certifique-se de que eles tenham instalado a atualização de abril de 2016. Caso contrário, os usuários não poderão acessar pastas públicas em uma coexistência ou topologia híbrida. Para obter mais informações, consulte <A href="https://docs.microsoft.com/pt-br/exchange/collaboration-exo/public-folders/access-public-folders-with-outlook-2016-for-mac">Acesso a pastas públicas com 2016 do Outlook para Mac</A>.



## Etapa 1: tornar as pastas públicas do Exchange 2010 detectáveis

1.  Se suas pastas públicas no Exchange 2010 ou posteriores servidores, você precisará instalar a função de servidor acesso para cliente em todos os servidores de caixa de correio que tem um banco de dados de pasta pública. Isso permite que o serviço Microsoft Exchange RpcClientAccess estar em execução, que permite que todos os clientes acessar pastas públicas. A função de acesso para cliente não é necessária para servidores de pasta pública do Exchange 2007 e esta etapa não é necessária. Para obter mais informações, consulte [instalar o Exchange Server 2010](install-exchange-2013-using-the-setup-wizard-exchange-2013-help.md).
    

    > [!NOTE]
    > Esse servidor não precisa ser parte do balanceamento de carga de acesso para cliente. Para obter mais informações, consulte <A href="https://technet.microsoft.com/en-us/library/ff625247(v=exchg.141).aspx">balanceamento de carga de Understanding no Exchange 2010</A>.



2.  Crie um banco de dados de caixa de correio vazio em cada servidor de pasta pública.
    
    Para o Exchange 2010, execute o seguinte comando. Este comando exclui o banco de dados de caixa de correio do balanceador de carga de provisionamento de caixa de correio. Isso evita que novas caixas de correio sejam automaticamente adicionadas a esse banco de dados.
    
    ```powershell
    New-MailboxDatabase -Server <PFServerName_with_CASRole> -Name <NewMDBforPFs> -IsExcludedFromProvisioning $true 
    ```
    
    Para o Exchange 2007, execute o seguinte comando:
    
    ```powershell
    New-MailboxDatabase -StorageGroup "<PFServerName>\StorageGroup>" -Name <NewMDBforPFs>
    ```
    

    > [!NOTE]
    > Recomendamos que a única caixa de correio que você adicionar a esse banco de dados seja a caixa de correio de proxy que você criará na etapa 3. Nenhuma outra caixa de correio deve ser criada nesse banco de dados de caixa de correio.



3.  Crie uma caixa de correio de proxy no novo banco de dados de caixa de correio e oculte a caixa de correio do catálogo de endereços. O SMTP desta caixa de correio será devolvido pela Descoberta Automática como o SMTP *DefaultPublicFolderMailbox*, de modo que, ao resolver esse SMTP, o cliente possa acessar o servidor Exchange herdado para acesso à pasta pública.
    
    ```powershell
    New-Mailbox -Name <PFMailbox1> -Database <NewMDBforPFs> 
    ```
    
    ```powershell
    Set-Mailbox -Identity <PFMailbox1> -HiddenFromAddressListsEnabled $true
    ```

4.  Para o Exchange 2010, habilite a Descoberta Automática para retornar as caixas de correio de pasta pública de proxy. Esta etapa não é necessária para o Exchange 2007.
    
    ```powershell
    Set-MailboxDatabase <NewMDBforPFs> -RPCClientAccessServer <PFServerName_with_CASRole>
    ```

5.  Repita as etapas anteriores para cada servidor de pasta pública em sua organização.

## Etapa 2: configurar as caixas de correio de usuário para acessar as pastas públicas herdadas

A etapa final deste procedimento é configurar as caixas de correio de usuário para permitir o acesso a pastas públicas locais herdadas.

Permita que os usuários locais do Exchange Server 2013 acessem as pastas públicas herdadas. Você apontará para todas as caixas de correio de pasta pública de proxy que criou na [Step 2: Make remote public folders discoverable](https://docs.microsoft.com/pt-br/exchange/collaboration-exo/public-folders/set-up-legacy-hybrid-public-folders). Execute o seguinte comando a partir de um servidor do Exchange 2013 com a CU5 ou a atualização mais recente.

```powershell
Set-OrganizationConfig -PublicFoldersEnabled Remote -RemotePublicFolderMailboxes ProxyMailbox1,ProxyMailbox2,ProxyMailbox3
```


> [!NOTE]
> Você deve esperar a conclusão da sincronização do ActiveDirectory para ver as alterações. Esse processo pode levar várias horas.



## Como saber se funcionou?

Faça logon no Outlook para um usuário cuja caixa de correio esteja em um Exchange Server 2013 CU5 ou superior e execute os seguintes testes de pasta pública:

1.  Verifique se o cliente do Outlook está executando.

2.  Mantenha a tecla CTRL pressionada e clique com o botão direito do mouse no ícone do Outlook na área de notificação do lado direito da barra de tarefas do Windows.

3.  Selecione **Testar a Configuração Automática de Email...**

4.  Certifique-se de que a ferramenta Testar a Configuração Automática de Email retorne as seguintes informações na guia XML:
    
      - \<PublicFolderInformation\>
    
      - \<SmtpAddress\>\<Endereço SMTP para caixa de correio de pasta pública\</SmtpAddress\>
    
      - \</PublicFolderInformation\>

5.  No cliente do Outlook, execute as seguintes tarefas:
    
      - Exiba a hierarquia da pastas públicas.
    
      - Verifique as permissões.
    
      - Crie e exclua pastas públicas.
    
      - Publique conteúdo e exclua conteúdo de uma pasta pública.

