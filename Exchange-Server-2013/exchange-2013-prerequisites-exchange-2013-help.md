---
title: 'Pré-requisitos do Exchange 2013: Exchange 2013 Help'
TOCTitle: Pré-requisitos do Exchange 2013
ms:assetid: e21cf744-7813-48b3-9293-5cecd89a6c25
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Bb691354(v=EXCHG.150)
ms:contentKeyID: 50486884
ms.date: 01/10/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Pré-requisitos do Exchange 2013

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2017-03-20_

Este tópico apresenta as etapas para instalar os pré-requisitos de sistema operacional Windows Server 2012 R2, Windows Server 2012 e Windows Server 2008 R2 com Service Pack 1 (SP1) necessários para as funções de servidor de Caixa de Correio e Acesso para Cliente do Microsoft Exchange 2013. Ele também apresenta os pré-requisitos necessários para a instalação das ferramentas de gerenciamento do Exchange 2013 nos computadores cliente com Windows 8, Windows 8.1 e Windows 7.

  - O que você precisa saber antes de começar?

  - Preparação do Active Directory

  - Pré-requisitos do Windows Server 2012 R2 e Windows Server 2012
    
      - Funções de servidor de Caixa de Correio ou de Acesso para Cliente
    
      - Função de servidor Transporte de Borda

  - Pré-requisitos do Windows Server 2008 R2 SP1
    
      - Funções de servidor de Caixa de Correio ou de Acesso para Cliente
    
      - Função de servidor Transporte de Borda

  - Pré-requisitos do Windows 7 (somente as ferramentas de administração)

  - Pré-requisitos do Windows 8 e Windows 8.1 (somente as ferramentas de administração)

## O que você precisa saber antes de começar?

  - As informações deste tópico se aplicam ao Service Pack 1 e a versões posteriores do Exchange 2013.

  - A função de servidor de Transporte de Borda está disponível a partir do Exchange 2013 SP1.

  - Certifique-se de que o nível funcional da sua floresta seja no mínimo Windows Server 2003, e que o mestre de esquema esteja executando o Windows Server 2003 com Service Pack 2 ou posterior. Para obter mais informações sobre o nível funcional do Windows, consulte [Gerenciando Domínios e Florestas](https://go.microsoft.com/fwlink/p/?linkid=137037).

  - A opção de instalação completa do Windows Server 2012 R2, Windows Server 2012 e Windows Server 2008 R2 SP1 deve ser usada para todos os servidores que executam funções de servidor ou ferramentas de gerenciamento do Exchange 2013.

  - Você deve primeiro ingressar o computador na floresta e no domínio do Active Directory internos apropriados.

  - Alguns pré-requisitos exigem que você reinicie o servidor para concluir a instalação.

  - Instale as atualizações do Windows mais recentes no seu computador. Para mais informações, consulte [Lista de verificação de segurança de implantação](deployment-security-checklist-exchange-2013-help.md).
    

    > [!NOTE]
    > Se estiver instalando a função de servidor de Caixa de Correio e quiser que o servidor seja membro de um grupo de disponibilidade de banco de dados (DAG), você deverá executar o Windows Server 2012 R2 Standard ou Datacenter Edition, Windows Server 2012 Standard ou Datacenter Edition ou o Windows Server 2008 R2 SP1 Enterprise Edition O Windows Server 2008 R2 SP 1 Standard Edition não oferece suporte aos recursos necessários para DAGs.<BR>Não é possível atualizar o Exchange&nbsp;estiver instalado no servidor.<BR>Para atualizar para o Microsoft Unified Communications Managed API (UCMA) 4.0, você deve, primeiro, desinstalar todas as versões do UCMA instaladas anteriormente, usando <STRONG>Adicionar/Remover programas</STRONG>.




> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>.



## Preparação do Active Directory

O computador que deseja usar para preparar o Active Directory para Exchange 2013 tem pré-requisitos específicos que devem ser atendidos.

Instale os seguintes softwares, na ordem demonstrada, no computador que serão usados para preparar o Active Directory:

1.  [.NET Framework 4.6.2](https://go.microsoft.com/fwlink/p/?linkid=808659)

2.  [Windows Management Framework 4.0](https://go.microsoft.com/fwlink/p/?linkid=390234) (incluído no Windows Server 2012 R2)

Após ter instalado o software listado acima, execute as seguintes etapas para instalar o Remote Tools Administration Pack. Após a instalação do Remote Tools Administration Pack, você conseguirá usar o computador para preparar o Active Directory. Para obter mais informações sobre como preparar o Active Directory, consulte [Preparar o Active Directory e domínios](prepare-active-directory-and-domains-exchange-2013-help.md).

1.  Abra o Windows PowerShell.

2.  Instale o Remote Tools Administration Pack.
    
      - Em um computador com Windows Server 2012 R2 ou Windows Server 2012, execute o seguinte comando.
        
            Install-WindowsFeature RSAT-ADDS
    
      - Em um computador com Windows Server 2008 R2 SP1, execute o seguinte comando.
        
            Add-WindowsFeature RSAT-ADDS

## Pré-requisitos do Windows Server 2012 R2 e Windows Server 2012

Os pré-requisitos necessários para instalar o Exchange 2013 e um computador com Windows Server 2012 R2 ou Windows Server 2012 depende de quais funções do Exchange você deseja instalar. Leia a seção abaixo correspondente às funções que você deseja instalar.

## Funções de servidor de Caixa de Correio ou de Acesso para Cliente

Siga as instruções desta seção para instalar os pré-requisitos nos computadores com Windows Server 2012 R2 ou Windows Server 2012 nos quais você deseja fazer uma das seguintes ações:

  - Instalar apenas a função de servidor de Caixa de Correio em um computador.

  - Instalar apenas a função de servidor de Acesso para Cliente em um computador.

  - Instalar as funções de servidor de Caixa de Correio e Acesso para Cliente no mesmo computador.

Faça o seguinte para instalar as funções e os recursos de Windows necessários:

1.  Abra o Windows PowerShell.

2.  Execute o seguinte comando para instalar os componentes necessários do Windows.
    
        Install-WindowsFeature AS-HTTP-Activation, Desktop-Experience, NET-Framework-45-Features, RPC-over-HTTP-proxy, RSAT-Clustering, RSAT-Clustering-CmdInterface, RSAT-Clustering-Mgmt, RSAT-Clustering-PowerShell, Web-Mgmt-Console, WAS-Process-Model, Web-Asp-Net45, Web-Basic-Auth, Web-Client-Auth, Web-Digest-Auth, Web-Dir-Browsing, Web-Dyn-Compression, Web-Http-Errors, Web-Http-Logging, Web-Http-Redirect, Web-Http-Tracing, Web-ISAPI-Ext, Web-ISAPI-Filter, Web-Lgcy-Mgmt-Console, Web-Metabase, Web-Mgmt-Console, Web-Mgmt-Service, Web-Net-Ext45, Web-Request-Monitor, Web-Server, Web-Stat-Compression, Web-Static-Content, Web-Windows-Auth, Web-WMI, Windows-Identity-Foundation, RSAT-ADDS

Após ter instalado as funções e os recursos de sistema operacional, instale os seguintes softwares na ordem mostrada:

1.  [.NET Framework 4.6.2](https://go.microsoft.com/fwlink/p/?linkid=808659)
    

    > [!IMPORTANT]
    > O Exchange 2013 CU16 e versões posteriores <STRONG>requerem</STRONG> o .NET Framework 4.6.2. Atualize os servidores para o .NET Framework 4.6.2 antes de instalar o Exchange 2013 CU16. Caso contrário, você receberá uma mensagem de erro. Se instalou o .NET Framework 4.5.2 em servidores Exchange, atualize os servidores para o Exchange 2013 CU15 antes de instalar o .NET Framework 4.6.2.



2.  [Windows Management Framework 4.0](https://go.microsoft.com/fwlink/p/?linkid=390234) (incluído no Windows Server 2012 R2)

3.  [Microsoft Unified Communications Managed API 4.0, Core Runtime 64 bits](https://go.microsoft.com/fwlink/p/?linkid=258269)

## Função de servidor Transporte de Borda

Siga as instruções desta seção para instalar os pré-requisitos nos computadores com Windows Server 2012 R2 ou Windows Server 2012 em que você deseja instalar a função de servidor de Transporte de Borda em um computador.

Faça o seguinte para instalar as funções e os recursos de Windows necessários:

1.  Abra o Windows PowerShell.

2.  Execute o seguinte comando para instalar os componentes necessários do Windows.
    
        Install-WindowsFeature ADLDS

Instale a versão do Microsoft .NET Framework que corresponde à versão do Exchange 2013 que você está instalando:

1.  [.NET Framework 4.6.2](https://go.microsoft.com/fwlink/p/?linkid=808659)
    

    > [!IMPORTANT]
    > O Exchange 2013 CU16 e versões posteriores <STRONG>requerem</STRONG> o .NET Framework 4.6.2. Atualize os servidores para o .NET Framework 4.6.2 antes de instalar o Exchange 2013 CU16. Caso contrário, você receberá uma mensagem de erro. Se instalou o .NET Framework 4.5.2 em servidores Exchange, atualize os servidores para o Exchange 2013 CU15 antes de instalar o .NET Framework 4.6.2.



2.  [Windows Management Framework 4.0](https://go.microsoft.com/fwlink/p/?linkid=390234) (incluído no Windows Server 2012 R2)

## Pré-requisitos do Windows Server 2008 R2 SP1

Os pré-requisitos necessários para instalar o Exchange 2013 e um computador com Windows Server 2008 R2 SP1 depende de quais funções do Exchange você deseja instalar. Leia a seção abaixo correspondente às funções que você deseja instalar.

## Funções de servidor de Caixa de Correio ou de Acesso para Cliente

Siga as instruções desta seção para instalar os pré-requisitos nos computadores Windows Server 2008 R2 SP1 em que deseja fazer um dos seguintes:

  - Instalar apenas a função de servidor de Caixa de Correio em um computador.

  - Instalar apenas a função de servidor de Acesso para Cliente em um computador.

  - Instalar as funções de servidor de Caixa de Correio e Acesso para Cliente no mesmo computador.

Faça o seguinte para instalar as funções e os recursos de Windows necessários:

1.  Abra o Windows PowerShell.

2.  Execute o seguinte comando para carregar o módulo Gerenciador de Servidores.
    
        Import-Module ServerManager

3.  Execute o seguinte comando para instalar os componentes necessários do Windows.
    
        Add-WindowsFeature Desktop-Experience, NET-Framework, NET-HTTP-Activation, RPC-over-HTTP-proxy, RSAT-Clustering, RSAT-Web-Server, WAS-Process-Model, Web-Asp-Net, Web-Basic-Auth, Web-Client-Auth, Web-Digest-Auth, Web-Dir-Browsing, Web-Dyn-Compression, Web-Http-Errors, Web-Http-Logging, Web-Http-Redirect, Web-Http-Tracing, Web-ISAPI-Ext, Web-ISAPI-Filter, Web-Lgcy-Mgmt-Console, Web-Metabase, Web-Mgmt-Console, Web-Mgmt-Service, Web-Net-Ext, Web-Request-Monitor, Web-Server, Web-Stat-Compression, Web-Static-Content, Web-Windows-Auth, Web-WMI, RSAT-ADDS

Após ter instalado as funções e os recursos de sistema operacional, instale os seguintes softwares na ordem mostrada:

1.  [.NET Framework 4.6.2](https://go.microsoft.com/fwlink/p/?linkid=808659)
    

    > [!IMPORTANT]
    > O Exchange 2013 CU16 e versões posteriores <STRONG>requerem</STRONG> o .NET Framework 4.6.2. Atualize os servidores para o .NET Framework 4.6.2 antes de instalar o Exchange 2013 CU16. Caso contrário, você receberá uma mensagem de erro. Se instalou o .NET Framework 4.5.2 em servidores Exchange, atualize os servidores para o Exchange 2013 CU15 antes de instalar o .NET Framework 4.6.2.



2.  [Windows Management Framework 4.0](https://go.microsoft.com/fwlink/p/?linkid=390234)

3.  [Microsoft Unified Communications Managed API 4.0, Core Runtime 64 bits](https://go.microsoft.com/fwlink/p/?linkid=258269)

4.  [Artigo KB974405 da Base de Dados de Conhecimento Microsoft (Windows Identity Foundation)](http://go.microsoft.com/fwlink/?linkid=3052&kbid=974405)

5.  [Artigo KB2619234 da Base de Dados de Conhecimento Microsoft (Um hotfix está disponível para permitir que o Cookie/GUID da associação que é usado por RPC sobre HTTP para ser usado na camada de RPC no Windows 7 e no Windows Server 2008 R2)](http://go.microsoft.com/fwlink/?linkid=3052&kbid=2619234)

6.  [Artigo KB2533623 da Base de Dados de Conhecimento Microsoft (Comunicado de Segurança da Microsoft: Carregamento da biblioteca insegura pode permitir a execução de código remoto)](http://go.microsoft.com/fwlink/?linkid=3052&kbid=2533623)
    

    > [!NOTE]
    > Esse hotfix já poderá ter sido instalado caso você tenha configurado o Windows Update para instalar atualizações de segurança no seu computador.



## Função de servidor Transporte de Borda

Siga as instruções desta seção para instalar os pré-requisitos nos computadores com Windows Server 2008 R2 SP1 em que você deseja instalar a função de servidor de Transporte de Borda em um computador.

Faça o seguinte para instalar as funções e os recursos de Windows necessários:

1.  Abra o Windows PowerShell.

2.  Execute o seguinte comando para carregar o módulo Gerenciador de Servidores.
    
        Import-Module ServerManager

3.  Execute o seguinte comando para instalar os componentes necessários do Windows.
    
        Add-WindowsFeature NET-Framework, ADLDS

Após ter instalado as funções e os recursos de sistema operacional, instale os seguintes softwares na ordem mostrada:

1.  [.NET Framework 4.6.2](https://go.microsoft.com/fwlink/p/?linkid=808659)
    

    > [!IMPORTANT]
    > O Exchange 2013 CU16 e versões posteriores <STRONG>requerem</STRONG> o .NET Framework 4.6.2. Atualize os servidores para o .NET Framework 4.6.2 antes de instalar o Exchange 2013 CU16. Caso contrário, você receberá uma mensagem de erro. Se instalou o .NET Framework 4.5.2 em servidores Exchange, atualize os servidores para o Exchange 2013 CU15 antes de instalar o .NET Framework 4.6.2.



2.  [Windows Management Framework 4.0](https://go.microsoft.com/fwlink/p/?linkid=390234)

3.  [Microsoft Unified Communications Managed API 4.0, Core Runtime 64 bits](https://go.microsoft.com/fwlink/p/?linkid=258269)

## Pré-requisitos do Windows 7 (somente as ferramentas de administração)

Siga as instruções desta seção para instalar os pré-requisitos nos computadores Windows Server 7 64 bits associados a um domínio em que deseja instalar as ferramentas de gerenciamento do Exchange:

1.  Abra o **Painel de Controle** e selecione **Programas**.

2.  Clique em **Ligar ou desligar os recursos do Windows**.

3.  Navegue até **Serviços de Informações da Internet** \> **Ferramentas de Gerenciamento da Web** \> **Compatibilidade com Gerenciamento do IIS 6**.

4.  Marque a caixa de seleção para **Console de Gerenciamento do IIS 6** e clique em **OK**.

Após ter instalado os recursos de sistema operacional, instale os seguintes softwares na ordem mostrada:

1.  [.NET Framework 4.6.2](https://go.microsoft.com/fwlink/p/?linkid=808659)

2.  [Windows Management Framework 4.0](https://go.microsoft.com/fwlink/p/?linkid=390234)

3.  [Artigo KB974405 da Base de Dados de Conhecimento Microsoft (Windows Identity Foundation)](http://go.microsoft.com/fwlink/?linkid=3052&kbid=974405)

## Pré-requisitos do Windows 8 e Windows 8.1 (somente as ferramentas de administração)

[.NET Framework 4.6.2](https://go.microsoft.com/fwlink/p/?linkid=808659)

