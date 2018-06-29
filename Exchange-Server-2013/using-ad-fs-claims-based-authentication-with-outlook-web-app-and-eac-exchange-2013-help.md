---
title: 'Usar autenticação baseada em declarações do AD FS com o Outlook Web App e o EAC: Exchange 2013 Help'
TOCTitle: Usar autenticação baseada em declarações do AD FS com o Outlook Web App e o EAC
ms:assetid: 919a9bfb-c6df-490a-b2c4-51796b0f0596
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Dn635116(v=EXCHG.150)
ms:contentKeyID: 61203508
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Usar autenticação baseada em declarações do AD FS com o Outlook Web App e o EAC

 

_**Aplica-se a:**Exchange Server 2013 SP1_

_**Tópico modificado em:**2017-04-14_

**Resumo**:

Para implantações de Service Pack 1 (SP1) do local Exchange 2013, instalando e configurando Active Directory serviços de Federação (AD FS) significam que agora você pode usar a autenticação baseada em declarações do AD FS para se conectar ao Outlook Web App e o EAC. É possível integrar o AD FS e autenticação baseada em declarações com Exchange 2013 SP1. Usando a autenticação baseada em declarações substitui os métodos de autenticação tradicional, incluindo o seguinte:

  - autenticação

  - Autenticação de formulários

  - Autenticação resumida

  - Autenticação básica

  - Autenticação de certificados de cliente

A autenticação é o processo de confirmação da identidade de um usuário. A autenticação valida que o usuário é quem ele afirma ser. A identidade baseada em declarações é uma outra abordagem de autenticação. A autenticação baseada em declarações remove o gerenciamento de autenticação do aplicativo (nesse caso, do Outlook Web App e do EAC) para facilitar o gerenciamento de contas por meio da centralização da autenticação. O Outlook Web App e o EAC não são responsáveis pela autenticação de usuários, nem pelo armazenamento de contas e senhas de usuários, pela pesquisa de detalhes de identidade de usuários ou pela integração com outros sistemas de identidade. A centralização da autenticação facilita a atualização para métodos de autenticação no futuro.


> [!TIP]
> O OWA para dispositivos não é compatível com a autenticação baseada em declarações.



Há várias versões do AD FS que podem ser usado, conforme resumido pela tabela a seguir.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>versão Windows Server</th>
<th>Instalação</th>
<th>Versão do AD FS</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>R2</p></td>
<td><p><strong>Baixe e instale</strong> o AD FS 2.0, um complemento do componente do Windows.</p></td>
<td><p>AD FS 2.0</p></td>
</tr>
<tr class="even">
<td><p>Windows Server 2012</p></td>
<td><p>Instale a função de servidor <strong>interna</strong> do AD FS.</p></td>
<td><p>AD FS 2.1</p></td>
</tr>
<tr class="odd">
<td><p>R2</p></td>
<td><p>Instale a função de servidor <strong>interna</strong> do AD FS.</p></td>
<td><p>AD FS 3.0</p></td>
</tr>
</tbody>
</table>


As tarefas que serão realizadas aqui são baseadas em Windows Server 2012 R2 que inclui o serviço de função do AD FS.

**Visão geral das etapas obrigatórias**

Step 1 - Review the certificate requirements for AD FS

Step 2 - Install and configure Active Directory Federation Services (AD FS)

Etapa 3: criar uma terceira parte confiável e regras de declaração personalizado para Outlook Web App e o EAC

Etapa 4 - instalar o serviço de função do Proxy de aplicativo Web (opcional)

Etapa 5 - configurar o serviço de função do Proxy de aplicativo Web (opcional)

Etapa 6 - Publicar Outlook Web App e o EAC usando o Proxy de aplicativo da Web (opcional)

Etapa 7 - configurar o Exchange 2013 para usar a autenticação do AD FS

Etapa 8 - autenticação de habilitar o AD FS nos diretórios virtuais do OWA e do ECP

Etapa 9 - reiniciar ou reciclar os serviços de informações da Internet (IIS)

Etapa 10 - testar as declarações do AD FS para Outlook Web App e o EAC

Additional information you might want to know

## O que eu preciso saber antes de começar?

  - No mínimo, é preciso instalar servidores Windows Server 2012 R2 separados: um como controlador de domínio, que usa o AD DS (Serviços de Domínio do Active Directory), um servidor do Exchange 2013, um servidor Proxy de Aplicativo Web e um servidor AD FS (Serviços de Federação do Active Directory). Verifique se todas as atualizações estão instaladas.

  - Instale o AD DS em uma quantidade adequada de servidores do Windows Server 2012 R2 da organização. Também é possível usar as **Notificações** no **Gerenciador de servidores** \> **Painel** para **Promover este servidor a um controlador de domínio**.

  - Instale a quantidade adequada de servidores de Acesso para Cliente e de Caixa de Correio para sua organização. Verifique se todas as atualizações estão instaladas, incluindo o SP1, em todos os servidores do Exchange 2013 da sua organização. Para baixar o SP1, consulte [Atualizações para o Exchange 2013](updates-for-exchange-2013-exchange-2013-help.md).

  - Para implantar o Proxy de Aplicativo da Web em um servidor é necessário ter permissões de administrador local. Implante o AD FS em um servidor que executa o Windows Server 2012 R2 em sua organização antes de implantar o Proxy de Aplicativo da Web.

  - Instale e configure a função do AD FS e crie objetos de confiança de terceiros confiável e regras de declaração no Windows Server 2012 R2. Para fazer isso, é preciso entrar com uma conta de usuário que seja membro dos Administradores de Domínio, Administradores Corporativos e do grupo Administradores Locais.

  - Para determinar as permissões necessárias para o Exchange 2013, consulte [Permissões de recurso](feature-permissions-exchange-2013-help.md).

  - É necessário receber permissões para gerenciar o Outlook Web App. Para ver as permissões necessárias, consulte a entrada "Permissões do Outlook Web App" no tópico [Permissões de dispositivos móveis e clientes](clients-and-mobile-devices-permissions-exchange-2013-help.md).

  - É necessário receber permissões para gerenciar o EAC. Para ver as permissões necessárias, consulte a entrada "Conectividade do Centro de Administração do Exchange" no tópico [Permissões de infraestrutura do Exchange e do Shell](exchange-and-shell-infrastructure-permissions-exchange-2013-help.md).

  - É provável que você só consiga usar o Shell para realizar alguns procedimentos. Para saber como abrir o Shell na organização local do Exchange, consulte [Abra o shell.](https://technet.microsoft.com/pt-br/library/dd638134\(v=exchg.150\)).

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>.



## Etapa 1: analise os requisitos de certificado para o AD FS

Os certificados desempenham um papel fundamental na proteção das comunicações entre os servidores do Exchange 2013 SP1, clientes da Web como o Outlook Web App e o EAC, servidores do Windows Server 2012 R2, incluindo os servidores de Serviços de Federação do Active Directory (AD FS) e os servidores Proxy de Aplicativo da Web. Os requisitos para certificados variam dependendo de você configurar um servidor do AD FS, Proxy do AD FS ou um servidor Proxy de Aplicativo da Web. Os certificados usados para serviços do AD FS, incluindo certificados SSL e de autenticação de token, devem ser importados para dentro do repositório de Autoridades de Certificação Confiáveis em todos os servidores do Exchange, AD FS e Proxy de Aplicativo da Web. A impressão digital importada para o certificado também é usada nos servidores do Exchange 2013 SP1 quando você usa o cmdlet [Set-OrganizationConfig](https://technet.microsoft.com/pt-br/library/aa997443\(v=exchg.150\)).

Em qualquer design do AD FS, vários certificados devem ser usados para proteger a comunicação entre usuários nos servidores da Internet e o AD FS. Cada servidor de federação deve ter um certificado de comunicação de serviço ou o certificado da camada de soquete seguro (SSL) e um certificado de assinatura de token antes de servidores do AD FS, Active Directory controladores de domínio, e os servidores de Exchange 2013 podem se comunicar e autentica. Dependendo de suas necessidades de orçamento e segurança, considere cuidadosamente quais dos seus certificados serão obtidas por um público autoridade de certificação ou uma autoridade de certificação corporativa. Se você deseja instalar e configurar uma raiz corporativa ou a autoridade de certificação subordinada, você pode usar Active Directory certificado AD CS (serviços). Se você deseja saber mais sobre o AD CS, consulte [Visão geral do Active Directory certificado serviços](https://go.microsoft.com/fwlink/?linkid=392697).

Apesar do AD FS não exigir que os certificados sejam emitidos por uma autoridade de certificação, o certificado SSL (que também é usado por padrão como um certificado de comunicações do serviço) deve ser de confiança do clientes do AD FS. Não recomendamos o uso de certificados autoassinados. Os servidores de federação usam um certificado SSL para proteger o tráfego dos serviços da Web para comunicações SSL com os clientes da Web e com os proxies de servidores de federação. Como o certificado SSL deve ser confiável para os computadores clientes, recomendamos usar um certificado assinado por uma autoridade de certificação de confiança. Todos os certificados selecionados devem ter uma chave privada correspondente. Depois de receber um certificado de uma autoridade de certificação (corporativa ou pública), certifique-se de que todos os certificados sejam importados para o repositório de Autoridades de Certificação Confiáveis em todos os servidores. Importe os certificados para o repositório com o snap-in **Certificados** do MMC ou distribua os certificados usando os Serviços de Certificados do Active Directory. É importante que, se o certificado importado expirar, você importe manualmente outro certificado válido.


> [!IMPORTANT]
> Se você estiver usando o certificado de autenticação de token autoassinado a partir do AD FS, é necessário importar este certificado para o repositório de Autoridades de Certificação Confiáveis em todos os servidores do Exchange 2013. Se o certificado de autenticação de token autoassinado não estiver sendo usado e o Proxy de Aplicativo Web for implantado, será necessário atualizar a chave pública na configuração do Proxy de Aplicativo da Web e todos os objetos de confiança de terceiros confiáveis do AD FS.



Ao configurar o Exchange 2013 SP1, o AD FS e o Proxy de Aplicativo da Web, siga estas recomendações para certificados:

  - **Servidores de Caixa de Correio**   Os certificados usados em servidores de Caixa de Correio são certificados autoassinados criados enquanto o Exchange 2013 é instalado. Como os clientes se conectam a um servidor de Caixa de Correio do Exchange 2013 por meio de um servidor de Acesso para Cliente do Exchange 2013, os únicos certificados que precisam ser gerenciados são os dos servidores de Acesso para Cliente.

  - **Servidores de Acesso para Cliente**   É exigido um certificado SSL usado para comunicações de serviço. Se seu certificado SSL já incluir o FQDN que você está usando para configurar o ponto de extremidade do objeto de confiança de terceiros confiável, não serão exigidos certificados adicionais.

  - **AD FS**   O AD FS exige de dois tipos de certificados:
    
      - O certificado SSL usado para comunicações de serviço
        
          - Nome da entidade: **adfs.contoso.com** (nome da implantação do AD FS)
        
          - Nome Alternativo da Entidade (SAN): Nenhum
    
      - Certificado de assinatura de tokens
        
          - Nome da entidade: **tokensigning.contoso.com**
        
          - Nome Alternativo da Entidade (SAN): Nenhum
        

        > [!TIP]
        > Ao substituir o certificado de autenticação de token no AD FS, todos os objetos de confiança de terceiros confiáveis devem ser atualizados para o uso no novo certificado de autenticação de token.



  - **Proxy de Aplicativo da Web**
    
      - O certificado SSL usado para comunicações de serviço
        
          - Nome da entidade: **owa.contoso.com**
        
          - Nome Alternativo da Entidade (SAN): Nenhum
        

        > [!TIP]
        > Se a URL Externa do Proxy de Aplicativo da Web for idêntica à sua URL interna, reutilize o certificado SSL do Exchange aqui.

    
      - Certificado SSL do Proxy do AD FS
        
          - Nome da entidade: **adfs.contoso.com** (nome da implantação do AD FS)
        
          - Nome Alternativo da Entidade (SAN): Nenhum
    
      - Certificado de autenticação de token: será copiado automaticamente a partir do AD FS como parte das etapas abaixo. Se esse certificado for usado, ele deve ser de confiança dos servidores do Exchange 2013 de sua organização.

Consulte a seção de requisitos de certificado no [Examinar os requisitos para implantar o AD FS](https://go.microsoft.com/fwlink/?linkid=392699) para obter mais informações sobre certificados.


> [!TIP]
> Um certificado de criptografia SSL ainda será necessário para o Outlook Web App e para o EAC, mesmo que você já tenha um certificado SSL para o AD FS. O certificado SSL é usado nos diretórios virtuais do OWA e do ECP.



## Etapa 2: instalar e configurar os Serviços de Federação do Active Directory (AD FS)

O AD FS no Windows Server 2012 R2 oferece recursos seguros e simplificados de federação de identidade e signon único (SSO) da Web. O AD FS inclui um serviço de federação que permite autenticações SSO da Web com base no navegador, de vários fatores e com base em declarações. O AD FS simplifica o acesso a sistemas e aplicativos usando um mecanismo de autorização de acesso com base em declarações para manter a segurança do aplicativo.

Para instalar o AD FS no Windows Server 2012 R2:

1.  Abra o **Gerenciador de Servidor** na tela **Bem-vindo** ou o **Gerenciador de Servidor** na barra de tarefas na área de trabalho. Clique em **Adicionar Funções e Recursos** no menu **Gerenciar**.

2.  Na página **Antes de começar**, clique em **Seguinte**.

3.  Na página **Selecionar o Tipo de Instalação**, clique em **Instalação baseada em função ou recurso** e, em seguida, clique em **Seguinte**.

4.  Na página **Selecionar Servidor de Destino**, clique em **Selecionar um servidor no pool de servidores**, verifique se o computador local está selecionado e clique em **Seguinte**.

5.  Na página **Selecionar funções de servidor**, clique em **Serviços de Federação do Active Directory** e em **Seguinte**.
    
    Na página **Selecionar Recursos**, clique em **Seguinte**. Os pré-requisitos ou recursos obrigatórios já estão selecionados para você. Não é necessário selecionar outros recursos.

6.  Na página **Serviço de Federação do Active Directory (AD FS)**, clique em **Seguinte**.

7.  Na página **Confirmar Seleções de Instalação**, marque **Reiniciar cada servidor de destino automaticamente, se necessário** e clique em **Instalar**.
    

    > [!TIP]
    > Não feche o assistente durante o processo de instalação.



Depois de instalar os servidores necessários da AD FS e gerar os certificados necessários, você deve configurar o AD FS e depois testar se o AD FS está funcionando corretamente. Você também pode usar a lista de verificação aqui para ajudá-lo na instalação e configuração do AD FS: [lista de verificação: configuração de servidor de Federação um](https://go.microsoft.com/fwlink/?linkid=392700).

Para configurar os Serviços de Federação do Active Directory:

1.  Na página **Processo de Instalação**, na janela abaixo de **Serviços de Federação do Active Directory**, clique em **Configurar o serviço de federação neste servidor**. O Assistente de Configuração do Serviço de Federação do Active Directory é exibido.

2.  Na página **Bem-vindo**, clique em **Criar o primeiro servidor de federação em um farm de servidores de federação** e, em seguida, clique em **Seguinte**.

3.  Na página **Conectar ao AD DS**, especifique uma conta com direitos de administrador de domínio para o domínio do Active Directory correto ao qual esse computador está conectado e, em seguida, clique em **Seguinte**. Se precisar selecionar um usuário diferente, clique em **Alterar**.

4.  Na página **Especificar Propriedades do Serviço**, faça o seguinte e clique em **Seguinte**:
    
      - Importe o certificado SSL que você obtido anteriormente da AD CS ou uma autoridade de certificação pública. Esse certificado é o certificado de autenticação de serviço necessários. Navegue até o local do seu certificado SSL. Para obter detalhes sobre como criar e importar certificados SSL, consulte [Certificados de servidor](https://go.microsoft.com/fwlink/?linkid=392703).
    
      - Insira um nome para seu serviço de federação; por exemplo, digite **adfs.contoso.com**.
    
      - Para oferecer um nome de exibição ao serviço de federação, digite o nome da sua organização. Por exemplo, **Contoso, Ltd.**.

5.  Na página **Especificar Conta de Serviço**, selecione **Usar uma Conta de Serviço Gerenciado de grupo ou de conta de usuário de domínio existente** e, em seguida, especifique a conta GMSA (FsGmsa) criada ao gerar o controlador de domínio. Inclua a senha da conta e clique em **Seguinte**.
    

    > [!TIP]
    > A Conta de Serviço Gerenciado Globalmente (GMSA) é uma conta que deve ser criada ao configurar o controlador de domínio. A conta GMSA é necessária durante a instalação e configuração do AD FS. Se ainda não tiver criado esta conta, execute o seguinte comando do Windows PowerShell. Ele criará a conta para o domínio contoso.com e para o servidor AD FS:



6.  execute o seguinte comando.
    
        Add-KdsRootKey -EffectiveTime (Get-Date).AddHours(-10)

7.  Este exemplo cria uma nova conta GMSA denominada FsGmsa para o serviço de Federação chamado adfs.contoso.com. O nome do serviço de Federação é o valor que é visível aos clientes.
    
        New-ADServiceAccount FsGmsa -DNSHostName adfs.contoso.com -ServicePrincipalNames http/adfs.contoso.com

8.  Na página **Especificar Banco de Dados de Configuração**, selecione **Criar um banco de dados neste servidor que utiliza o Banco de Dados Interno do Windows** e, em seguida, clique em **Seguinte**.

9.  Na página **Analisar Opções**, verifique suas seleções de configuração. Você pode optar por usar o botão **Exibir script** para automatizar instalações adicionais do AD FS. Clique em **Seguinte**.

10. Na página **Verificações de Pré-requisitos**, veja se todas as verificações se pré-requisitos foram concluídas com êxito e, em seguida, clique em **Configurar**.

11. Na página **Progresso da Instalação**, verifique se tudo está instalado corretamente e clique em **Fechar**.

12. Na página **Resultados**, analise os resultados, verifique se a configuração foi concluída com êxito e, em seguida, clique em **As próximas etapas são necessárias para concluir a implantação do serviço de federação**.

Os seguintes comandos do PowerShell Windows fazem a mesma coisa que as etapas anteriores.

    Import-Module ADFS

    Install-AdfsFarm -CertificateThumbprint 0E0C205D252002D535F6D32026B6AB074FB840E7 -FederationServiceDisplayName "Contoso Corporation" -FederationServiceName adfs.contoso.com -GroupServiceAccountIdentifier "contoso\FSgmsa`$"

Para obter detalhes e a sintaxe, consulte [Install-AdfsFarm](https://go.microsoft.com/fwlink/?linkid=392704).

Para verificar a instalação: No servidor do AD FS, abra o navegador da Web e navegue até a URL dos metadados de federação. Por exemplo, **https://adfs.contoso.com/federationmetadata/2007-06/federationmetadata.xml**.

## Etapa 3: criar uma terceira parte confiável e regras de declaração personalizado para Outlook Web App e o EAC

Para obter todos os aplicativos e serviços que você deseja publicar por meio do Proxy de aplicativo Web, você deve configurar uma terceira parte confiável no servidor AD FS. Para implantações com vários sites de Active Directory que usam os namespaces separados, uma terceira parte confiável para Outlook Web App e o EAC deve ser adicionado para cada namespace.

O EAC usa o diretório virtual do ECP. Exiba ou defina definições para o EAC usando o [Get-EcpVirtualDirectory](https://technet.microsoft.com/pt-br/library/dd351058\(v=exchg.150\)) e os cmdlets [Set-EcpVirtualDirectory](https://technet.microsoft.com/pt-br/library/dd297991\(v=exchg.150\)). Para acessar o EAC, use um navegador da Web e vá para **http://server1.contoso.com/ecp**.


> [!TIP]
> A inclusão da barra à direita <STRONG>/</STRONG> nos exemplos URL mostrada abaixo é intencional. É importante garantir que o AD FS confianças de parceiros e a <STRONG>são idênticos do Exchange audiência URI</STRONG>. Isso significa que o AD FS terceira confiança de terceiros e Exchange audiência URI deve <STRONG>ter</STRONG> ou <STRONG>ambos emitem</STRONG> trilha barras em suas URLs. Os exemplos desta seção contêm à direita <STRONG>/</STRONG> após qualquer url que terminem com "owa" (/owa/) ou "ecp" (/ecp/).



No Outlook Web App, para criar objetos de confiança de terceiros confiáveis usando o snap-in de Gerenciamento do AD FS no Windows Server 2012 R2:

1.  Em **Gerenciador de Servidor**, clique em **Ferramentas** e, em seguida, selecione **Gerenciamento do AD FS**.

2.  No **snap-in do AD FS**, em **AD FS\\Relações de Confiança**, clique com o botão direito do mouse em **Objeto de Confiança de Terceira Parte Confiável** e, em seguida, clique em **Adicionar Objeto de Confiança de Terceiros Confiáveis** para abrir o assistente **Adicionar Objeto de Confiança de Terceiros Confiáveis**.

3.  Na página **Bem-vindo**, clique em **Iniciar**.

4.  Na página **Selecionar Fonte de Dados**, clique em **Inserir dados sobre a confiança de terceiros confiáveis manualmente** e em **Seguinte**.

5.  Na página **Especificar nome para exibição**, na caixa **Nome para exibição**, digite o **Outlook Web App**e, em seguida, em **notas**, digite uma descrição para esta terceira parte confiável (por exemplo, **Isso é uma relação de confiança para https://mail.contoso.com/owa/**) e Clique em **Avançar**.

6.  Na página **Escolher Perfil**, clique em **Perfil do AD FS** e, em seguida, clique em **Seguinte**.

7.  Na página **Configurar Certificado**, clique em **Seguinte**.

8.  Na página **Configurar URL**, clique em **Habilitar suporte para o protocolo WS-Federation Passive** e, em seguida, em **URL do protocolo WS-Federation Passive terceira parte confiável**, **tipo https://mail.contoso.com/owa/**e clique em Avançar de .

9.  Na página **Configurar Identificadores**, especifique um ou mais identificadores para a confiança de terceiros confiáveis, clique em **Adicionar** para adicioná-los à lista e, em seguida, clique em **Seguinte**.

10. Na página **Configurar a Autenticação Multifator Agora?**, selecione **Definir as configurações da autenticação multifator para esta terceira parte confiável**.

11. Na página **Configurar Autenticação Multifator**, verifique se **Não quero definir as configurações da autenticação multifator para este objeto de confiança de terceira parte confiável dessa vez** está selecionado e clique em **Seguinte**.

12. Na página **Escolher Regras de Autorização de Emissão**, selecione **Permitir que todos os usuários acessem esta confiança de terceiros confiáveis** e clique em **Seguinte**.

13. Na página **Pronto para Adicionar Confiança**, analise as configurações e clique em **Seguinte** para salvar as informações da confiança de terceiros confiáveis.

14. Na página **Terminar**, verifique se **Abrir a caixa de diálogo Editar Regras de Declaração para este objeto de confiança de terceiros confiáveis depois que o assistente fechar** não está selecionado e clique em **Fechar**.

Para criar um objeto de confiança de terceiros confiáveis para o EAC, siga estas etapas novamente e crie um segundo objeto de confiança de terceiros confiáveis, mas, em vez de usar **Outlook Web App** como o nome de exibição, insira **EAC**. Em descrição, insira **This is a trust for the Exchange Admin Center** e a **URL do Protocolo Passivo da Federação do WS da Confiança de Terceiros Confiáveis** é **https://mail.contoso.com/ecp**.

No modelo de identidade baseada em declarações, a função dos Serviços de Federação do Active Directory (AD FS) como serviço de federação é emitir um token contendo um conjunto de declarações. As regras de declaração regem as decisões com relação às declarações emitidas pelo AD FS. As regras de declaração e todos os dados de configuração de servidores são armazenados no banco de dados de configuração do AD FS.

É necessário que você crie duas regras de declaração:

  - SID de usuário

  - UPN

Para adicionar as regras de declarações exigidas:

1.  Em **Gerenciador de Servidor**, clique em **Ferramentas** e em **Gerenciamento do AD FS**.

2.  Na árvore de console, em **AD FS\\Relações de Confiança**, clique em **Confianças do Provedor de Declarações** ou em **Confianças de Terceiros Confiáveis** e, em seguida, clique no objeto de confiança de terceiros confiáveis do Outlook Web App.

3.  Na janela **Confianças de Terceiros Confiáveis**, clique com o botão direito do mouse na relação de confiança do Outlook Web App e, em seguida, clique em **Editar Regras de Declaração**.

4.  Na janela **Editar Regras de Declaração**, na guia **Regras de Transformação de Emissão**, clique em **Adicionar Regra** para iniciar o Assistente para Adicionar Regra de Declaração de Transformação.

5.  Na página **Selecionar Modelo de Regras**, em **Modelo de regra de declaração**, selecione **Enviar Declarações Usando uma Regra Personalizada** na lista e clique em **Seguinte**.

6.  Na página **Configurar Regra**, na etapa **Escolher Tipo de Regra**, em **Nome da regra de declaração**, insira o nome da regra de declaração. Use um nome descritivo para a regra de declaração, por exemplo, **ActiveDirectoryUserSID**. Em **Regra Personalizada**, insira a seguinte sintaxe de linguagem das regras de declaração para esta regra:
    
        c:[Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsaccountname", Issuer == "AD AUTHORITY"] => issue(store = "Active Directory", types = ("http://schemas.microsoft.com/ws/2008/06/identity/claims/primarysid"), query = ";objectSID;{0}", param = c.Value);

7.  Na página **Configurar Regra**, clique em **Terminar**.

8.  Na janela **Editar Regras de Declaração**, na guia **Regras de Transformação de Emissão**, clique em **Adicionar Regra** para iniciar o Assistente para Adicionar Regra de Declaração de Transformação.

9.  Na página **Selecionar Modelo de Regras**, em **Modelo de regra de declaração**, selecione **Enviar Declarações Usando uma Regra Personalizada** na lista e clique em **Seguinte**.

10. Na página **Configurar Regra**, na etapa **Escolher Tipo de Regra**, em **Nome da regra de declaração**, insira o nome da regra de declaração. Use um nome descritivo para a regra de declaração, por exemplo, **ActiveDirectoryUPN**. Em **Regra Personalizada**, insira a seguinte sintaxe de linguagem das regras de declaração para esta regra:
    
        c:[Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsaccountname", Issuer == "AD AUTHORITY"] => issue(store = "Active Directory", types = ("http://schemas.xmlsoap.org/ws/2005/05/identity/claims/upn"), query = ";userPrincipalName;{0}", param = c.Value);

11. Clique em **Finalizar**.

12. Na janela **Editar Regras de Declaração**, clique em **Aplicar** e em **OK**.

13. Repita as etapas de 3 a 12 deste procedimento para a EAT terceira confiança de terceiros.

Como alternativa, você pode criar relações de confiança de terceiros retransmissão e regras de declaração usando Windows PowerShell:

1.  Crie os arquivos .txt: IssuanceAuthorizationRules.txt e IssuanceTransformRules.txt.

2.  Importe o conteúdo dos arquivos para duas variáveis.

3.  Execute os dois cmdlets a seguir para criar os objetos de confiança de terceiros confiáveis. Neste exemplo, também serão configuradas regras de declaração.

**O arquivo IssuanceAuthorizationRules.txt contém:**

    @RuleTemplate = "AllowAllAuthzRule" => issue(Type = "http://schemas.microsoft.com/authorization/claims/permit", Value = "true");

**O arquivo IssuanceTransformRules.txt contém:**

    @RuleName = "ActiveDirectoryUserSID" c:[Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsaccountname", Issuer == "AD AUTHORITY"] => issue(store = "Active Directory", types = ("http://schemas.microsoft.com/ws/2008/06/identity/claims/primarysid"), query = ";objectSID;{0}", param = c.Value); 
    
    @RuleName = "ActiveDirectoryUPN" c:[Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsaccountname", Issuer == "AD AUTHORITY"] => issue(store = "Active Directory", types = ("http://schemas.xmlsoap.org/ws/2005/05/identity/claims/upn"), query = ";userPrincipalName;{0}", param = c.Value);

**Execute os seguintes comandos:**

    [string]$IssuanceAuthorizationRules=Get-Content -Path C:\IssuanceAuthorizationRules.txt
    
    [string]$IssuanceTransformRules=Get-Content -Path c:\IssuanceTransformRules.txt
    
    Add-ADFSRelyingPartyTrust -Name "Outlook Web App" -Enabled $true -Notes "This is a trust for https://mail.contoso.com/owa/" -WSFedEndpoint https://mail.contoso.com/owa/ -Identifier https://mail.contoso.com/owa/ -IssuanceTransformRules $IssuanceTransformRules -IssuanceAuthorizationRules $IssuanceAuthorizationRules
    
    Add-ADFSRelyingPartyTrust -Name "Exchange Admin Center (EAC)" -Enabled $true -Notes "This is a trust for https://mail.contoso.com/ecp/" -WSFedEndpoint https://mail.contoso.com/ecp/ -Identifier https://mail.contoso.com/ecp/ -IssuanceTransformRules $IssuanceTransformRules -IssuanceAuthorizationRules $IssuanceAuthorizationRules

## Etapa 4: instalar o serviço de função do Proxy de aplicativo Web (opcional)


> [!TIP]
> Etapa 4, etapa 5 e 6 etapa são para os usuários que deseja publicar o OWA do Exchange e do ECP usando o Proxy de aplicativo Web e que desejam ter o Proxy de aplicativo Web executem a autenticação do AD FS. No entanto, publicação Exchange com o Proxy de aplicativo Web não será necessária, portanto você pode ignorar a etapa 7, se você não usar o Proxy de aplicativo Web e quiser que o Exchange para realizar a autenticação do AD FS em si.



Proxy de aplicativo Web é um novo serviço de função de acesso remoto no Windows Server 2012 R2. Proxy de aplicativo Web fornece a funcionalidade de proxy reverso para aplicativos da web dentro de sua rede corporativa permitir que os usuários em muitos dispositivos para acessá-las de fora da rede corporativa. Proxy de aplicativo Web preauthenticates acesso aos aplicativos web usando Active Directory serviços de Federação (AD FS) e também funciona como um proxy do AD FS. Embora o Proxy de aplicativo Web não é necessária, é recomendável quando o AD FS está acessível para clientes externos. No entanto, o acesso offline no Outlook Web App não é suportado ao usar a autenticação do AD FS por meio do Proxy de aplicativo Web. Você pode encontrar mais informações sobre como integrar o Proxy de aplicativo Web, conferindo [Instalando e configurando o Proxy de aplicativo Web para publicação de aplicativos internos](https://go.microsoft.com/fwlink/?linkid=392705)


> [!WARNING]
> Não é possível instalar o Proxy de Aplicativo da Web no mesmo servidor em que o AD FS está instalado.



Para implantar o Proxy de Aplicativo da Web, é necessário instalar a função de servidor de Acesso Remoto com a função de serviço do Proxy de Aplicativo da Web em um servidor que atuará como o servidor do Proxy de Aplicativo da Web. Para instalar o serviço de função do Proxy de Aplicativo da Web:

1.  No servidor do Proxy de Aplicativo da Web, em **Gerenciador de Servidor**, clique em **Gerenciar** e, em seguida, em **Adicionar Funções e Recursos**.

2.  No Assistente para Adicionar Funções e Recursos, clique três vezes em **Seguinte** para ir para a página **Funções de Servidor**.

3.  Na página **Funções de Servidor**, selecione **Acesso Remoto** na lista e, em seguida, clique em **Seguinte**.

4.  Na página **Recursos**, clique em **Seguinte**.

5.  Na página **Acesso Remoto**, leia as informações e depois clique em **Seguinte**.

6.  Na página **Serviços de Função**, selecione **Proxy de Aplicativo da Web**. Em seguida, na janela **Assistente para Adicionar Funções e Recursos**, clique em **Adicionar Recursos** e em **Seguinte**.

7.  Na janela **Confirmação**, clique em **Instalar**. Você também pode marcar **Reiniciar o servidor de destino automaticamente, se necessário**.

8.  Na caixa de diálogo **Progresso da Instalação**, verifique se a instalação foi concluída com êxito e clique em **Fechar**.

O cmdlet Windows PowerShell a seguir faz o mesmo que as etapas anteriores.

    Install-WindowsFeature Web-Application-Proxy -IncludeManagementTools

## Etapa 5: configurar o serviço de função do Proxy de aplicativo Web (opcional)

É necessário configurar o Proxy de Aplicativo da Web para se conectar ao servidor do AD FS. Repita este procedimento para todos os servidores que você deseja implantar como servidores de Proxy de Aplicativo da Web.

Para configurar o serviço de função de Aplicativo da Web:

1.  No servidor de Proxy de Aplicativo da Web, em **Gerenciador de Servidor**, clique em **Ferramentas** e em **Gerenciamento de Acesso Remoto**.

2.  No painel **Configuração**, clique em **Proxy de Aplicativo da Web**.

3.  No console **Gerenciamento de Acesso Remoto**, no painel central, clique em **Executar o assistente de configuração do Proxy de Aplicativo da Web**.

4.  No Assistente de configuração do Proxy de Aplicativo da Web, na caixa de diálogo **Bem-vindo**, clique em **Seguinte**.

5.  Na página **Servidor de Federação**, realize os seguintes procedimentos e clique em **Seguinte**:
    
      - Na caixa **Nome do serviço de federação**, insira o nome de domínio totalmente qualificado (FQDN) do servidor do AD FS. Por exemplo, **adfs.contoso.com**.
    
      - Nas caixas **Nome de usuário** e **Senha**, digite as credenciais da conta de administrador local nos servidores do AD FS.

6.  Na caixa de diálogo **Certificado de Proxy do AD FS**, na lista de certificados atualmente instalada no servidor de Proxy de Aplicativo da Web, selecione o certificado a ser usado pelo Proxy de Aplicativo da Web para a funcionalidade de proxy do AD FS e, em seguida, clique em **Seguinte**. O certificado escolhido aqui deve ser aquele cuja entidade é o nome do Serviço de Federação. Por exemplo, **adfs.contoso.com**.

7.  Na caixa de diálogo **Confirmação**, analise as configurações. Caso seja necessário, copie o cmdlet do Windows PowerShell para automatizar as instalações adicionais. Clique em **Configurar**.

8.  Na caixa de diálogo **Resultados**, verifique se a configuração foi concluída com êxito e clique em **Fechar**.

O cmdlet Windows PowerShell a seguir faz o mesmo que as etapas anteriores.

    Install-WebApplicationProxy -CertificateThumprint 1a2b3c4d5e6f1a2b3c4d5e6f1a2b3c4d5e6f1a2b -FederationServiceName adfs.contoso.com

## Etapa 6: publicar o Outlook Web App e o EAC usando o Proxy de aplicativo da Web (opcional)

Na etapa 3, você criou declarações retransmissão de confiança de terceiros para Outlook Web App e o EAC e agora você precisa publicar ambos os aplicativos. Mas antes de fazer isso, verificar se uma terceira parte confiável para que eles foi criado e verificar se você tem um certificado no servidor Proxy de aplicativo Web que é adequado para Outlook Web App e o EAC. Para todos os AD FS pontos de extremidade que você precisa para serem publicados pelo Proxy do aplicativo Web, no console de gerenciamento do AD FS, você deve definir o ponto de extremidade para ser **Habilitado para Proxy**.

Siga estas etapas para publicar o Outlook Web App usando o Proxy de Aplicativo da Web. Repita estas etapas para o EAC. Quando publicar no EAC, será necessário alterar o nome, a URL externa, o certificado externo e a URL de backend.

Para publicar o Outlook Web App e o EAC usando o Proxy de Aplicativo da Web:

1.  No servidor do Proxy de Aplicativo da Web, no console de **Gerenciamento de Acesso Remoto**, no painel **Navegação**, clique em **Proxy de Aplicativo da Web** e, em seguida, no painel **Tarefas**, clique em **Publicar**.

2.  No Assistente para publicar novos aplicativos, na página **Bem-vindo**, clique em **Seguinte**.

3.  Na página **Pré-autenticação**, clique em **Serviços de Federação do Active Directory (AD FS)** e em **Seguinte**.

4.  Na página **Confiança de Terceiros Confiáveis**, na lista de confianças de terceiros confiáveis, selecione a confiança de terceiros confiáveis para o aplicativo que você deseja publicar e, em seguida, clique em **Seguinte**.

5.  Na página **Configurações de Publicação**, realize os seguintes procedimentos e clique em **Seguinte**:
    
    1.  Na caixa **Nome**, insira um nome amigável para o aplicativo. Este nome só é usado na lista de aplicativos publicados no **Console de Gerenciamento de Acesso Remoto**. Use **OWA** e **EAC** como nomes.
    
    2.  Na caixa **URL externa**, insira a URL externa para esse aplicativo — por exemplo, **https://external.contoso.com/owa/** para Outlook Web App e **https://external.contoso.com/ecp/** para EAC.
    
    3.  Na lista **Certificado externo**, selecione um certificado cujo nome de entidade corresponda ao nome do host da URL externa.
    
    4.  Na caixa **URL do servidor de back-end**, insira a URL do servidor back-end. Observe que esse valor é inserido automaticamente quando você insere a URL externa e alterá-lo somente se a URL do servidor back-end é diferente — por exemplo, **https://mail.contoso.com/owa/** para Outlook Web App e **https://mail.contoso.com/ecp/** para EAC.
    

    > [!TIP]
    > O Proxy de Aplicativo da Web pode traduzir nomes de hosts em URLs, mas não consegue traduzir caminhos. Portanto, é possível inserir nomes de hosts diferentes, mas é necessário que o mesmo caminho seja inserido. Por exemplo, você pode inserir uma URL externa <EM>https://external.contoso.com/app1/</EM> e uma URL de servidor backend <EM>https://mail.contoso.com/app1/</EM>. Porém, não é possível inserir uma URL externa <EM>https://external.contoso.com/app1/</EM> e uma URL de servidor backend <EM>https://mail.contoso.com/internal-app1/</EM>.



6.  Na página **Confirmação**, analise as configurações e clique em **Publicar**. Copie o comando do Windows PowerShell para configurar outros aplicativos publicados.

7.  Na página **Resultados**, certifique-se de que o aplicativo tenha sido publicado com êxito e clique em **Fechar**.

A seguir, o cmdlet do Windows PowerShell realiza as mesmas tarefas que o procedimento anterior do Outlook Web App.

    Add-WebApplicationProxyApplication -BackendServerUrl 'https://mail.contoso.com/owa/' -ExternalCertificateThumbprint 'E9D5F6CDEA243E6E62090B96EC6DE873AF821983' -ExternalUrl 'https://external.contoso.com/owa/' -Name 'OWA' -ExternalPreAuthentication ADFS -ADFSRelyingPartyName 'Outlook Web App'

A seguir, o cmdlet do Windows PowerShell realiza as mesmas tarefas que o procedimento anterior do EAC.

    Add-WebApplicationProxyApplication -BackendServerUrl 'https://mail.contoso.com/ecp/' -ExternalCertificateThumbprint 'E9D5F6CDEA243E6E62090B96EC6DE873AF821983' -ExternalUrl 'https://external.contoso.com/ecp/' -Name 'EAC' -ExternalPreAuthentication ADFS -ADFSRelyingPartyName 'Exchange Admin Center'

Após concluir essas etapas, Proxy de aplicativo Web irá realizar a autenticação do AD FS para clientes do Outlook Web App e o EAC e também aparecerá proxy as conexões com o Exchange em nome deles. Você não precisa configurar o Exchange em si para autenticação do AD FS, portanto, prossiga para a etapa 10 para testar sua configuração.

## Etapa 7 – configurar o Exchange 2013 para usar a autenticação do AD FS

Ao configurar o AD FS que será usado para a autenticação baseada em declarações com o Outlook Web App e o EAC no Exchange 2013, habilite o AD FS para sua organização do Exchange. Use o cmdlet [Set-OrganizationConfig](https://technet.microsoft.com/pt-br/library/aa997443\(v=exchg.150\)) para definir as configurações do AD FS para sua organização:

  - Defina o emissor do AD FS como **https://adfs.contoso.com/adfs/ls/**.

  - Defina os URIs do AD FS como **https://mail.contoso.com/owa/** e **https://mail.contoso.com/ecp/**.

  - Encontre o impressão digital do certificado de assinatura usando Windows PowerShell no servidor AD FS e inserindo `Get-ADFSCertificate -CertificateType "Token-signing"`de token do AD FS. Em seguida, atribua a assinatura de token impressão digital do certificado que você encontrou. Se o certificado de assinatura de token do AD FS tiver expirado, a impressão digital do novo certificado de assinatura de token do AD FS deve ser atualizada, usando o cmdlet [Set-OrganizationConfig](https://technet.microsoft.com/pt-br/library/aa997443\(v=exchg.150\)) .

Execute os seguintes comandos no Shell de gerenciamento do Exchange.

    $uris = @(" https://mail.contoso.com/owa/","https://mail.contoso.com/ecp/")
    Set-OrganizationConfig -AdfsIssuer "https://adfs.contoso.com/adfs/ls/" -AdfsAudienceUris $uris -AdfsSignCertificateThumbprint "88970C64278A15D642934DC2961D9CCA5E28DA6B"


> [!TIP]
> O parâmetro <EM>-AdfsEncryptCertificateThumbprint</EM> não é compatível com estes cenários.



Para obter detalhes e sintaxe, consulte [Set-OrganizationConfig](https://technet.microsoft.com/pt-br/library/aa997443\(v=exchg.150\)) e [Get-ADFSCertificate](https://go.microsoft.com/fwlink/?linkid=392706).

## Etapa 8 – autenticação de habilitar o AD FS nos diretórios virtuais do OWA e do ECP

Para os diretórios virtuais do OWA e do ECP, habilite a autenticação do AD FS como o único método de autenticação e desabilite todas as outras formas de autenticação.


> [!WARNING]
> Configure o diretório virtual do ECP antes de configurar o diretório virtual do OWA.



Configure o diretório virtual do ECP usando o Shell de gerenciamento do Exchange. Na janela do Shell, execute o seguinte comando.

    Get-EcpVirtualDirectory | Set-EcpVirtualDirectory -AdfsAuthentication $true -BasicAuthentication $false -DigestAuthentication $false -FormsAuthentication $false -WindowsAuthentication $false

Configure o diretório virtual OWA usando o Shell de gerenciamento do Exchange. Na janela do Shell, execute o seguinte comando.

    Get-OwaVirtualDirectory | Set-OwaVirtualDirectory -AdfsAuthentication $true -BasicAuthentication $false -DigestAuthentication $false -FormsAuthentication $false -WindowsAuthentication $false -OAuthAuthentication $false


> [!TIP]
> Os comandos anteriores do Shell de gerenciamento do Exchange configure os diretórios virtuais do OWA e do ECP em cada servidor de acesso para cliente em sua organização. Se você não quiser aplicar essas configurações para todos os servidores de acesso para cliente, use o parâmetro <EM>-Identity</EM> e especifique o servidor de acesso para cliente. É provável que você desejará aplicar estas configurações somente para os servidores de acesso para cliente em sua organização que estão na Internet opostas.



Para obter detalhes e saber sobre a sintaxe, consulte [Get-OwaVirtualDirectory](https://technet.microsoft.com/pt-br/library/aa998588\(v=exchg.150\)) e [Set-OwaVirtualDirectory](https://technet.microsoft.com/pt-br/library/bb123515\(v=exchg.150\)) ou [Get-EcpVirtualDirectory](https://technet.microsoft.com/pt-br/library/dd351058\(v=exchg.150\)) e [Set-EcpVirtualDirectory](https://technet.microsoft.com/pt-br/library/dd297991\(v=exchg.150\)).

## Etapa 9: reiniciar ou reciclar os serviços de informações da Internet (IIS)

Depois de concluir todas as etapas necessárias, incluindo as alterações nos diretórios virtuais do Exchange, será necessário reiniciar os Serviços de Informações da Internet. Para fazer isso, use um dos seguintes métodos:

  - Usando o Windows PowerShell:
    
        Restart-Service W3SVC,WAS -noforce

  - Usando uma linha de comando: Clique em **Iniciar** e em **Executar**, digite `IISReset /noforce` e clique em **OK**.

  - Usando o Gerenciador dos Serviços de Informações da Internet (IIS): Em **Gerenciador de Servidor** \> **IIS**, clique em **Ferramentas** e, em seguida, em **Gerenciador dos Serviços de Informações da Internet (IIS)**. Na janela **Gerenciador dos Serviços de Informações da Internet (IIS)**, no painel de ações em **Gerenciar Servidor**, clique em **Reiniciar**.

## Etapa 10 - testar as declarações do AD FS para Outlook Web App e o EAC

Para testar as declarações do AD FS para o Outlook Web App:

  - No navegador da web, entrar no Outlook Web App — por exemplo, **https://mail.contoso.com/owa**

  - Na janela do navegador, se você receber um erro de certificado, basta prosseguir para o site do Outlook Web App. Você deve ser redirecionado para o ADFS página de entrada ou o ADFS solicitar credenciais.

  - Digite seu nome de usuário (domínio \\ usuário) e a senha e clique em **entrar**.

Outlook Web App será carregado na janela.

Para testar as declarações do AD FS para o EAC:

1.  No navegador da Web, acesse **https://mail.contoso.com/ecp**.

2.  Na janela do navegador, se você receber um erro de certificado, basta prosseguir para o site do ECP. Você deve ser redirecionado para o ADFS página de entrada ou o ADFS solicitar credenciais.

3.  Digite seu nome de usuário (domínio \\ usuário) e a senha e clique em **entrar**.

4.  O EAC deve carregar na janela.

## Mais informações que podem lhe interessar

**Autenticação de vários fatores**

Para implantações do Exchange 2013 SP1 no local, implantar e configurar os Serviços de Federação do Active Directory (AD FS) 2.0 usando declarações significa que o Outlook Web App e o EAC no Exchange 2013 SP1 são compatíveis com os métodos de autenticação de vários fatores, como autenticação baseada em certificados, tokens de autenticação ou de segurança e autenticação por impressão digital. A autenticação de dois fatores geralmente é confundida com outras formar de autenticação. A autenticação de vários fatores exige o uso de dois ou três fatores de autenticação. Esses fatores são:

  - Algo que apenas o usuário saiba (por exemplo: a senha, o PIN ou um padrão)

  - Algo que o usuário possua (por exemplo: um cartão de banco, um token de segurança, um cartão inteligente ou um celular)

  - Algo que o usuário seja (por exemplo: uma característica biométrica, como uma impressão digital)

Para obter detalhes sobre a autenticação multifator Windows Server 2012 R2, consulte [Visão geral: gerenciar o risco com adicionais a autenticação multifator para aplicativos confidenciais](https://go.microsoft.com/fwlink/?linkid=392707) e [guia passo a passo: gerenciar o risco com Adicionais a autenticação multifator para aplicativos confidenciais](https://go.microsoft.com/fwlink/?linkid=392708).

O Windows Server 2012 o serviço de função R2 AD FS, o serviço de Federação funciona como um serviço de token de segurança, fornece os tokens de segurança que são usados com declarações e fornece a capacidade de suportar a autenticação multifator. O serviço de Federação emite tokens baseados nas credenciais que são apresentadas. Depois que o repositório de conta verifica as credenciais do usuário, as declarações para o usuário são geradas de acordo com as regras da política de confiança e são adicionadas a um token de segurança que é emitido para o cliente. Para obter mais informações sobre declarações, consulte [Noções básicas sobre declarações](https://go.microsoft.com/fwlink/?linkid=392709).

**Co existente com outras versões do Exchange**

É possível usar a autenticação do AD FS para o Outlook Web App e a EAT quando você tiver mais de uma versão do Exchange implantado em sua organização. Este cenário só há suporte para implantações do Exchange 2010 e Exchange 2013 e apenas se todos os clientes estiverem se conectando através dos servidores de Exchange 2013 **e** esses servidores Exchange 2013 tiverem sido configurados para autenticação do AD FS.

Usuários com uma caixa de correio em um servidor do Exchange 2010 podem acessar suas caixas de correio por meio de um servidor Exchange 2013 configurado para autenticação do AD FS. A conexão do cliente inicial para o servidor Exchange 2013 usará a autenticação do AD FS. No entanto, a conexão intermediadas por proxy para o servidor do Exchange 2010, usará Kerberos. Não há um meio com suporte para configurar o Exchange Server 2010 para direcionar a autenticação do AD FS.

