---
title: 'Instalar o Exchange 2013 usando o modo autônomo: Exchange 2013 Help'
TOCTitle: Instalar o Exchange 2013 usando o modo autônomo
ms:assetid: 386465e9-41da-4e26-9816-b3b69be1f8bf
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Aa997281(v=EXCHG.150)
ms:contentKeyID: 50485379
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Instalar o Exchange 2013 usando o modo autônomo

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2014-06-19_

Para executar uma instalação autônoma, você deve instalar o Microsoft Exchange Server 2013 pelo prompt de comando. Para obter mais informações sobre o planejamento e a implantação do Exchange 2013, consulte [Planejamento e implantação](planning-and-deployment-for-exchange-2013-installation-instructions.md).

Recomendamos que a função Transporte de Borda seja instalada na rede de perímetro fora da floresta interna Active Directory da sua organização. Mesmo sendo possível instalar a função de servidor Transporte de Borda em um computador que faz parte de um domínio, isso irá habilitar apenas o gerenciamento de domínio de recursos e configurações Windows. A função de Transporte de Borda por si só não usa propriamente Active Directory. Em vez disso, ela usa o recurso Active Directory Lightweight Directory Services (AD LDS) Windows para armazenar a configuração e informações sobre o destinatário. Para obter mais informações sobre a função de Transporte de Borda, consulte [Servidores de Transporte de Borda](edge-transport-servers-exchange-2013-help.md).


> [!TIP]
> Você já ouviu falar do Assistente de Implantação do Exchange Server? É uma ferramenta online gratuita que ajuda a implantar rapidamente o Exchange 2013 em sua organização. Ele faz algumas perguntas e cria uma lista de verificação de implantação personalizada para você. Se você quiser saber mais sobre ele, consulte <A href="exchange-server-deployment-assistant-exchange-2013-help.md">Assistente de implantação do Exchange Server</A>.




> [!TIP]
> Depois de instalar qualquer função de servidor em um computador executando o Exchange 2013, não será possível usar o assistente de Instalação do Exchange 2013&nbsp;para adicionar outras funções de servidor ao computador. Se você quiser adicionar mais funções de servidor a um computador, use Adicionar ou Remover Programas no Painel de Controle ou Setup.exe na janela de prompt de comando.<BR>A função Transporte de Borda não pode ser instalada no mesmo computador que tiver as funções de servidor de Caixa de Correio e Acesso para Cliente instaladas.



Para obter informações sobre tarefas a serem concluídas após a instalação, consulte [Tarefas de pós-instalação do Exchange 2013](exchange-2013-post-installation-tasks-exchange-2013-help.md).

## O que você precisa saber antes de começar?

As informações a seguir se aplicam a todas as funções de servidor do Exchange 2013.

  - Certifique-se de ter lido as notas de versão antes de instalar o Exchange 2013. Para mais informações, consulte [Notas de versão do Exchange 2013](release-notes-for-exchange-2013-exchange-2013-help.md).

  - O computador em que você instalou o Exchange 2013 deve ter um sistema operacional com suporte (tal como Windows Server 2008 R2 com Service Pack 1 (SP1), Windows Server 2012 R2 ou Windows Server 2012), ter espaço em disco suficiente e atender a outros requisitos. Para obter informações sobre os requisitos do sistema, consulte [Requisitos de sistema do Exchange 2013](exchange-2013-system-requirements-exchange-2013-help.md).

  - Para executar a instalação do Exchange 2013, você deve instalar o .NET Framework 4.5, Management Framework Windows da Microsoft, e outros software necessários. Para conhecer os pré-requisitos de todas as funções de servidor, consulte [Pré-requisitos do Exchange 2013](exchange-2013-prerequisites-exchange-2013-help.md).

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!WARNING]
> Depois de instalar o Exchange em um servidor, não altere o nome do servidor. Não há suporte para renomear o servidor após a instalação de uma função de servidor Exchange.



As informações a seguir se aplicam às funções do servidor Caixa de Correio e Acesso para Cliente do Exchange 2013.

  - Tempo estimado para conclusão: 60 minutos

  - Cada organização precisa de, no mínimo, um servidor de Acesso para Cliente e um servidor de Caixa de Correio na floresta do Active Directory. Além disso, todo site do Active Directory que contenha um servidor de Caixa de Correio também deve conter um servidor de Acesso para Cliente, pelo menos. Se você estiver separando suas funções de servidor, recomendamos instalar primeiro a função de servidor Caixa de Correio.

  - O computador em que você instalou o Exchange 2013 deve pertencer a um domínio Active Directory.

  - Certifique-se de que a conta que você usa tenha sido delegada a associação ao grupo Administradores do Esquema, se você não tiver preparado anteriormente o esquema do Active Directory. Se você estiver instalando o primeiro servidor do Exchange 2013 da organização, a conta usada deverá ser associada ao grupo Administradores de Empresas. Se já tiver preparado o esquema e não estiver instalando o primeiro servidor do Exchange 2013 da organização, você deverá usar uma conta associada ao grupo de função de Gerenciamento da Organização do Exchange 2013.
    
    Os administradores que são membros do grupo de função de Instalação Delegada podem implantar servidores do Exchange 2013 que tenham sido previamente configurados por um membro do grupo de função de Gerenciamento da Organização.

As informações a seguir se aplicam à função de servidor de Transporte de Borda do Exchange 2013.

  - Tempo estimado para conclusão: 40 minutos

  - A função Transporte de Borda está disponível com o Exchange 2013 SP1 ou posterior.

  - Você precisa configurar o sufixo DNS primário do computador. Por exemplo, se o nome do domínio totalmente qualificado do seu computador for edge.contoso.com, o sufixo DNS do computador será contoso.com. Para obter mais informações, consulte [Sufixo DNS primário estiver faltando](primary-dns-suffix-is-missing-exchange-2013-help.md).

  - Os servidores de Transporte de Hub Exchange 2007 e Exchange 2010 precisam de atualização antes de você criar uma Assinatura do EdgeSync entre eles e um servidor de Transporte de Borda Exchange 2013. Se você não instalar esta atualização, a assinatura do EdgeSync não funcionará corretamente. Para obter mais informações, consulte a seção dos "Cenários de coexistência suportados" [Requisitos de sistema do Exchange 2013](exchange-2013-system-requirements-exchange-2013-help.md).

  - Certifique-se de que sua conta faça parte do grupo local de Administradores no computador em que você está instalando a função Transporte de Borda.

## Use o Setup.exe para instalar o Exchange 2013 no modo autônomo


> [!TIP]
> Para baixar a versão mais recente do Exchange 2013, consulte <A href="updates-for-exchange-2013-exchange-2013-help.md">Atualizações para o Exchange 2013</A>.



1.  Faça logon no computador em que você deseja instalar o Exchange 2013.

2.  Navegue até o local de rede dos arquivos de instalação do Exchange 2013.

3.  No prompt de comando, execute o comando aplicável para a sua organização.
    

    > [!IMPORTANT]
    > Se o Controle de Acesso de Usuário (UAC) estiver habilitado, você deverá executar o <CODE>Setup.exe</CODE> em um prompt de comando elevado.

    
        Setup.exe [/Mode:<setup mode>] [/IAcceptExchangeServerLicenseTerms]
        [/Roles:<server roles to install>] [/InstallWindowsComponents] 
        [/OrganizationName:<name for the new Exchange organization>] 
        [/TargetDir:<target directory>] [/SourceDir:<source directory>]
        [/UpdatesDir:<directory from which to install updates>] 
        [/DomainController:<FQDN of domain controller>] [/DisableAMFiltering]
        [/AnswerFile:<filename>] [/DoNotStartTransport] 
        [/EnableErrorReporting] [/CustomerFeedbackEnabled:<True | False>] 
        [/AddUmLanguagePack:<UM language pack name>] 
        [/RemoveUmLanguagePack:<UM language pack name>] 
        [/NewProvisionedServer:<server>] [/RemoveProvisionedServer:<server>] 
        [/MdbName:<mailbox database name>] [/DbFilePath:<Edb file path>] 
        [/LogFolderPath:<log folder path>] [/ActiveDirectorySplitPermissions:<True | False>]
        [/TenantOrganizationConfig:<path>]

4.  Os arquivos de instalação são copiados localmente para o computador em que você está instalando o Exchange 2013.

5.  A instalação verifica os pré-requisitos, incluindo todos os pré-requisitos específicos para as funções de servidor que você está instalando. Se você não tiver atendido a todos os pré-requisitos, a Instalação falhará e retornará uma mensagem de erro explicando o motivo da falha. Se você atendeu a todos os pré-requisitos, o programa de Instalação instalará o Exchange 2013.

6.  Reinicie o computador após a conclusão do Exchange 2013.

7.  Conclua sua implantação executando as tarefas fornecidas no [Tarefas de pós-instalação do Exchange 2013](exchange-2013-post-installation-tasks-exchange-2013-help.md).

## Exemplos

A seguir, são exibidos exemplos do uso do Setup.exe:

  - **Setup.exe /mode:Install /role:ClientAccess,Mailbox /OrganizationName:MyOrg /IAcceptExchangeServerLicenseTerms**
    
    Este comando cria uma organização do Exchange 2013 no Active Directory chamada MyOrg, instala a função de servidor de Acesso para Cliente, a função de servidor de Caixa de Correio e as ferramentas de gerenciamento e também aceita os termos de licenciamento do Exchange 2013.

  - **Setup.exe /mode:Install /role:ClientAccess,Mailbox /TargetDir:"C:\\Exchange Server" /IAcceptExchangeServerLicenseTerms**
    
    Este comando instala a função de servidor de Acesso para Cliente, a função de servidor de Caixa de Correio e as ferramentas de gerenciamento no diretório "C:\\Exchange Server". Esse comando considera que uma organização do Exchange 2013 já foi preparada.

  - **Setup.exe /mode:Install /r:CA,MB /IAcceptExchangeServerLicenseTerms**
    
    Este comando instala a função de servidor de Acesso para Cliente, a função de servidor de Caixa de Correio e as ferramentas de gerenciamento no local de instalação padrão.

  - **Setup.exe /mode:Install /r:EdgeTransport /IAcceptExchangeServerLicenseTerms**
    
    Este comando instala a função de servidor Transporte de Borda e as ferramentas de gerenciamento no local de instalação padrão.

  - **Setup.exe /mode:Install /r:ET /IAcceptExchangeServerLicenseTerms**
    
    Este comando instala a função de servidor Transporte de Borda e as ferramentas de gerenciamento no local de instalação padrão.

  - **Setup.exe /mode:Uninstall /IAcceptExchangeServerLicenseTerms**
    
    Este comando remove completamente o Exchange 2013 do servidor e remove a configuração do Exchange deste servidor do Active Directory.

  - **Setup.exe /PrepareAD /on:"My Org" /IAcceptExchangeServerLicenseTerms**
    
    Este comando cria uma organização do Exchange chamada My Org e prepara o Active Directory para o Exchange 2013.

  - **C:\\ExchangeServer\\bin\\Setup.exe /m:Install /r:ClientAccess /SourceDir:d:\\amd64 /IAcceptExchangeServerLicenseTerms**
    
    Este comando adiciona a função de servidor de Acesso para Cliente a um servidor do Exchange 2013 existente, usando D:\\amd64 como o diretório de origem.

  - **Setup.exe /role:ClientAccess,Mailbox /UpdatesDir:"C:\\ExchangeServer\\New Patches" /IAcceptExchangeServerLicenseTerms**
    
    Este comando atualiza o ExchangeServer.msi com patches do diretório especificado e depois instala a função de servidor de Acesso para Cliente, a função de servidor de Caixa de Correio e as ferramentas de gerenciamento. Se um pacote de idiomas estiver incluído neste diretório, ele também será instalado.

  - **Setup.exe /mode:Install /role:ClientAccess,Mailbox /DomainController:DC01 /IAcceptExchangeServerLicenseTerms**
    
    Este comando usa o controlador de domínio DC01 para consultar e fazer alterações no Active Directory enquanto instala a função de servidor de Acesso para Cliente, a função de servidor de Caixa de Correio e as ferramentas de gerenciamento.

  - **Setup.exe /mode:Install /role:ClientAccess /AnswerFile:c:\\ExchangeConfig.txt /IAcceptExchangeServerLicenseTerms**
    
    Este comando instala a função de servidor de Acesso para Cliente usando as configurações no arquivo ExchangeConfig.txt.

  - **Setup.exe /rprs:Exchange03 /IAcceptExchangeServerLicenseTerms**
    
    Este comando remove o objeto Exchange03 do Active Directory.

  - **Setup.exe /AddUmLanguagePack:ko-KR /IAcceptExchangeServerLicenseTerms**
    
    Este comando instala o pacote de idioma de Unificação de Mensagens coreano do diretório %ExchangeSourceDir%\\ServerRoles\\UnifiedMessaging.

## Como saber se funcionou?

Para verificar se instalou com sucesso o Exchange 2013, consulte [Verificar uma instalação do Exchange 2013](verify-an-exchange-2013-installation-exchange-2013-help.md).

Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), ou [Proteção do Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=285351).

Você encontrou o que você está procurando? Por favor, separe um minuto do seu tempo para [enviar seus comentários para nós](mailto:exsetuphelpfeedback@microsoft.com?subject=exchange%202013%20setup%20help%20feedback) sobre as informações que você estava esperando encontrar.

