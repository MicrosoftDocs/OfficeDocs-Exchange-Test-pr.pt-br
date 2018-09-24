---
title: 'Exibir ou configurar diretórios virtuais do Outlook Web App'
TOCTitle: Exibir ou configurar diretórios virtuais do Outlook Web App
ms:assetid: 90babcf6-4486-4e01-9819-6d3ca4ed756c
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Dd298140(v=EXCHG.150)
ms:contentKeyID: 50486180
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Exibir ou configurar diretórios virtuais do Outlook Web App

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2013-08-12_

Você pode usar o EAC ou o Shell para exibir ou configurar as propriedades de um diretório virtual do Outlook Web App.


> [!WARNING]
> No Exchange Online, os administradores não podem exibir ou configurar diretórios virtuais do Outlook Web App.



Se usar o Shell para visualizar as propriedades de um diretório virtual do Outlook Web App, as informações retornadas serão um subconjunto das informações disponíveis. Por exemplo, se você usar o cmdlet **Get-OWAVirtualDirectory** para visualizar as propriedades, o Exchange retornará as seguintes informações:

  - Nome do diretório virtual

  - Nome do servidor

  - Exchange Versão do servidor do

Você também pode recuperar informações de determinado diretório virtual em um servidor específico usando os parâmetros disponíveis. Para obter mais informações sobre os parâmetros do cmdlet **Get-OWAVirtualDirectory**, consulte [Get-OwaVirtualDirectory](https://technet.microsoft.com/pt-br/library/aa998588\(v=exchg.150\)).

Se você usar o EAC para exibir as propriedades de um diretório virtual do Outlook Web App, poderá exibir a maioria das propriedades do diretório virtual que está visualizando.

## O que você precisa saber antes de começar?

  - Tempo estimado para concluir cada procedimento: 10 minutos.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Diretórios virtuais do Outlook Web App", no tópico [Permissões de dispositivos móveis e clientes](clients-and-mobile-devices-permissions-exchange-2013-help.md).

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>..



## O que você deseja fazer?

## Usar o EAC para exibir ou configurar as propriedades de diretório virtual do Outlook Web App

1.  No EAC, clique em **Servidores** \> **Diretórios Virtuais**.
    
    Você pode usar as listas suspensas para selecionar o servidor e o tipo de diretório virtual. Por padrão, todos os servidores e diretórios virtuais são exibidos.

2.  No painel de resultados, clique para selecionar o diretório virtual que você deseja exibir ou editar e clique em **Editar**.

3.      
    Na guia **Geral**, você pode exibir as propriedades do site padrão do Outlook Web App e especificar uma URL externa e uma interna. Visualize ou selecione as seguintes opções:
    
      - **Servidor**   (Somente leitura.) **Servidor** exibe o nome do servidor que hospeda o diretório virtual do Outlook Web App.
    
      - **Versão**   (Somente leitura.) **Versão** exibe a versão do servidor Exchange no qual o diretório virtual está.
    
      - **Site**   (Somente leitura.) **Site** exibe o nome do site.
    
      - **Versão do Outlook Web App**   (somente leitura). **Versão do Outlook Web App** exibe a versão do servidor Exchange.
    
      - **Modificado**   (Somente leitura.) **Modificado** exibe a data e hora da última modificação do diretório virtual.
    
      - **URL interna**   Nesta caixa de texto, especifique a URL usada para acessar este site de uma rede interna. Uma URL interna é configurada automaticamente durante a Instalação do Exchange 2013. A configuração padrão da URL interna de um servidor voltado ou não para a Internet é https://\<Nome do computador\>/owa.
    
      - **URL externa**   Nesta caixa de texto, especifique a URL usada para acessar o site a partir da Internet. Por padrão, a **URL Externa** fica em branco. Para servidores de Acesso para Cliente voltados para a Internet, a **URL Externa** deve ser definida com o valor publicado no DNS referente a esse site do Active Directory. Para servidores Exchange 2013 que não têm presença na Internet, a configuração **URL externa** deve permanecer em branco.

4.      
    Na guia **Autenticação**, especifique os métodos de autenticação, o formato de entrada e o domínio de entrada.
    
      - **Use um ou mais métodos de autenticação padrão**   Selecione essa opção para usar um ou mais dos seguintes métodos de autenticação padrão:
        
        **Autenticação Integrada do Windows**   Este método exige que os usuários tenham um nome de conta de usuário e uma senha do Windows Server 2008 ou do Windows Server 2012 válidos para acessar informações. Os nomes e as senhas da conta dos usuários não são solicitados. Ao invés disso, o servidor negocia com os pacotes de segurança do Windows que estão instalados no computador cliente. A autenticação integrada do Windows habilita o servidor a autenticar usuários sem solicitar informações a eles e sem transmitir informações que não sejam criptografadas pela rede. Para que esse método funcione, o computador cliente deve ser membro do mesmo domínio dos servidores que estão executando o Exchange ou de um domínio que seja de confiança do domínio em que o servidor do Exchange se encontra.
        
        **Autenticação digest para servidores de domínio do Windows**   Esse método transmite senhas pela rede como um valor hash para segurança adicional. A autenticação Resumida pode ser usada apenas em domínios do Windows Server 2008 e do Windows Server 2012 para usuários que tenham uma conta armazenada no Active Directory. Para obter mais informações sobre a autenticação Digest, consulte a documentação do Windows Server.
        
        **Autenticação básica (a senha é enviada como texto não criptografado)**   Esse método é um mecanismo de autenticação simples definido pela especificação HTTP, que codifica o nome de logon e a senha de um usuário antes que suas credenciais sejam enviadas ao servidor. Para verificar se a senha está o mais protegida possível, você deve usar criptografia SSL (Secure Sockets Layer) entre computadores cliente e o servidor em que a função de servidor Acesso para Cliente esteja instalada.
    
      - **Usar autenticação baseada em formulários**   A autenticação baseada em formulários fornece segurança aprimorada para diretórios virtuais do Outlook Web App. A autenticação baseada em formulários cria uma página de entrada para o Outlook Web App. Você pode configurar o tipo de prompt de entrada usado pela autenticação baseada em formulários. Por exemplo, você pode configurar a autenticação baseada em formulários para exigir que os usuários forneçam informações sobre o domínio e o nome de usuário, no formato domínio\\nome do usuário na página de entrada do Outlook Web App.
        

        > [!IMPORTANT]
        > A autenticação baseada em formulários não fornece um canal seguro, a menos que a SSL tenha sido habilitada.

        
        Selecione uma destas opções:
        
        **Domínio\\nome de usuário**   Exige que o usuário informe o domínio e o nome de usuário no formato domínio\\nome de usuário. Por exemplo, para um usuário chamado Kweku no domínio Contoso, o logon seria contoso\\kweku.
        
        **Nome UPN** Se o formato de entrada do nome UPN é especificado, a caixa **Nome de Usuário** na página de entrada do Outlook Web App instrui os usuários a inserir o endereço de email; por exemplo, kweku@contoso.com. Se o UPN do usuário não é idêntico ao endereço de email, o usuário não consegue acessar o Outlook Web App usando o prompt de entrada **PrincipalName**. Recomendamos que você use o prompt de entrada **PrincipalName** somente se os UPNs dos usuários corresponderem aos endereços de email.
        
        **Apenas nome de usuário** O usuário informa apenas seu nome de usuário, sem o nome de domínio, como, por exemplo, Kweku. Se você usar o prompt de entrada **Apenas nome de usuário** para autenticação baseada em formulários, deverá especificar também a propriedade **Domínio de Logon**. A propriedade **Domínio de Logon** determina o domínio padrão a ser usado quando um usuário tenta fazer logon no Outlook Web App. Por exemplo, se o domínio padrão for Contoso, e um usuário de domínio chamado Kweku fizer logon no Outlook Web App, apenas Kweku deve ser inserido como o nome de usuário. O servidor usará o domínio padrão Contoso. Se o usuário não for um membro do domínio Contoso, o domínio e o nome do usuário devem ser inseridos.

5.      
    Na guia **Recursos**, especifique os recursos que você deseja habilitar ou desabilitar para usuários do Outlook Web App em um diretório virtual.
    

    > [!NOTE]
    > As configurações de recursos para usuários individuais substituem as configurações do diretório virtual. É possível alterar as configurações de segmentação de cada usuário usando o cmdlet <STRONG>Set-CASMailbox</STRONG> ou usando as diretivas de caixa de correio do Outlook Web App. Para mais informações, consulte <A href="https://docs.microsoft.com/pt-br/exchange/clients-and-mobile-in-exchange-online/outlook-on-the-web/outlook-web-app-mailbox-policies">Diretivas de caixa de correio do Outlook Web App</A>.

    
    Use as caixas de seleção para habilitar ou desabilitar recursos. Por padrão, são exibidos os recursos mais comuns. Para ver todos os recursos que podem ser habilitados ou desabilitados, clique em **Mais opções**.
    

    > [!NOTE]
    > A opção para habilitar ou desabilitar a versão padrão do Outlook Web App usando a caixa de seleção <STRONG>Cliente Premium</STRONG> foi substituída e será removida das configurações. A versão padrão do Outlook Web App está sempre habilitada.



6.      
    Na guia **Acesso a arquivos**, use as caixas de seleção para configurar as opções de acesso a arquivos e exibição dos usuários. O acesso aos arquivos permite que os usuários abram ou visualizem o conteúdo de arquivos anexos a um email.
    
    O acesso aos arquivos pode ser controlado com base em se o usuário entrou no sistema em um computador público ou privado. A opção para que os usuários selecionem acesso a computadores particulares ou acesso a computadores públicos está disponível apenas quando você usa autenticação baseada em formulários. Todas as outras formas de padrão de autenticação para acesso de computador particular.
    
      - **Acesso direto a arquivos**   Marque essa caixa de seleção se quiser habilitar acesso direto aos arquivos. O acesso direto aos arquivos permite que os usuários abram arquivos anexados a emails.
    
      - **Exibição de Documentos WebReady**   Marque essa caixa de seleção, se você quiser que os documentos suportados sejam convertidos para HTML e exibidos em um navegador da Web.
    
      - **Forçar Exibição de Documento WebReady quando um conversor estiver disponível**   Marque esta caixa de seleção, se você quiser forçar que documentos sejam convertidos para HTML e exibidos em um navegador da Web antes de que os usuários possam abri-los no aplicativo de exibição. Os documentos só poderão ser abertos no aplicativo de exibição se o acesso direto aos arquivos estiver habilitado.

7.  Clique em **Salvar** para atualizar a política.

## Usar o Shell para configurar as propriedades do diretório virtual do Outlook Web App

Este exemplo habilita a autenticação baseada em formulários no diretório virtual padrão do Outlook Web App do servidor Contoso.

    set-OwaVirtualDirectory -Identity "Contoso\owa (default web site)" -FormsAuthentication $true

Para obter mais informações sobre sintaxe e parâmetros, consulte [Set-OwaVirtualDirectory](https://technet.microsoft.com/pt-br/library/bb123515\(v=exchg.150\)).

## Usar o Shell para visualizar as propriedades do diretório virtual do Outlook Web App

Este exemplo permite a exibição das propriedades de todos os diretórios virtuais do Outlook Web App em todos os sites de IIS (Serviços de Informações da Internet) em todos os computadores que tenham a função de servidor de Acesso para Cliente instalada em uma organização do Exchange.

```powershell
Get-OWAVirtualDirectory
```

Este exemplo permite a exibição das propriedades de um diretório virtual do Outlook Web App no site de IIS padrão no servidor Exchange local.

    Get-OWAVirtualDirectory -identity "<Exchange Server Name>\owa (default web site)"

Este exemplo permite a exibição das propriedades de todos os diretórios virtuais do Outlook Web App em um site de IIS em um servidor Exchange específico.

```powershell
Get-OWAVirtualDirectory -server <Exchange Server Name>
```

Este exemplo permite a exibição dos valores das propriedades de cada diretório virtual do Outlook Web App em todos os sites de IIS em todos os servidores de Acesso para Cliente em uma organização do Exchange.

```powershell
Get-OWAVirtualDirectory | format-list
```

Para obter mais informações sobre sintaxe e parâmetros, consulte [Get-OwaVirtualDirectory](https://technet.microsoft.com/pt-br/library/aa998588\(v=exchg.150\)).

## Como saber se funcionou?

Para confirmar se você teve êxito ao editar um diretório virtual do Outlook Web App:

1.  No EAC, clique em **Servidores** \> **Diretórios Virtuais** e escolha um diretório virtual específico do Outlook Web App.

2.  Clique no botão **Editar** para exibir as propriedades do diretório virtual.

3.  Clique em **Salvar** ou **Cancelar**, para fechar a página de Propriedades.

