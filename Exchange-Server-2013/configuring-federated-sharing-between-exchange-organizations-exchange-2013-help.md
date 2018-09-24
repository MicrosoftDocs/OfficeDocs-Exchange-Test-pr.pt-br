---
title: 'Configurando o compartilhamento federado entre organizações do Exchange'
TOCTitle: Configurando o compartilhamento federado entre organizações do Exchange
ms:assetid: 94e31454-b027-4757-b52f-d3c2ead6d916
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/JJ657473(v=EXCHG.150)
ms:contentKeyID: 50486154
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configurando o compartilhamento federado entre organizações do Exchange

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2016-12-09_

Com o compartilhamento federado, os usuários em sua organização do Exchange no local podem compartilhar informações de calendário de disponibilidade com os destinatários em outras organizações do Exchange também configuradas para compartilhamento federado. O compartilhamento de disponibilidade pode ser habilitado entre duas organizações executando o Exchange 2013 e também entre organizações com uma implantação mista do Exchange. Para saber mais sobre compartilhamento federado, consulte [Compartilhamento](sharing-exchange-2013-help.md).

Este tópico oferece um resumo das exigências e etapas de configuração necessárias para habilitar o compartilhamento de disponibilidade entre tipos diferentes das seguintes implantações comuns do Exchange:

  - Duas organizações do Exchange 2013.

  - Uma organização do Exchange 2013 e uma organização do Exchange 2010 SP2.

  - Uma organização do Exchange 2007 (ou uma organização mista Exchange 2007 e do Exchange 2010 SP2) e uma organização do Exchange 2013.

  - Uma organização do Exchange 2003 (ou uma organização mista Exchange 2003 e do Exchange 2010 SP2) e uma organização do Exchange 2013.

Para outras tarefas de gerenciamento relacionadas a compartilhamento federado, consulte [Procedimentos de Federação](federation-procedures-exchange-2013-help.md).


> [!IMPORTANT]
> Esse recurso do Exchange Server 2013 não é totalmente compatível com o Office 365 operado pelo 21Vianet na China e pode haver algumas limitações de recurso. Para saber mais, confira o artigo <A href="https://go.microsoft.com/fwlink/?linkid=313640">Saiba mais sobre o Office 365 operado pelo 21Vianet</A>.



## O que você precisa saber antes de começar?

  - Tempo estimado para concluir cada procedimento: 2 horas.

  - Os procedimentos neste tópico exigem permissões específicas. Consulte cada procedimento para ver informações sobre permissões.

  - Antes de seguir os procedimentos deste tópico, confirme se você entendeu as limitações associadas ao compartilhamento de informações de disponibilidade nas organizações do Exchange. Para detalhes, consulte [Limitations of free/busy sharing](sharing-exchange-2013-help.md).

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

## O que você deseja fazer?

## Configurar compartilhamento de disponibilidade entre organizações do Exchange 2013

Conclua as etapas em [Configurar o compartilhamento federado](configure-federated-sharing-exchange-2013-help.md) para ambas as organizações.

## Configurar compartilhamento de disponibilidade entre organizações do Exchange 2013 e do Exchange 2010 SP2

  - Configurar compartilhamento federado para a organização do Exchange 2013. Siga as instruções em [Configurar o compartilhamento federado](configure-federated-sharing-exchange-2013-help.md).

  - Configure delegação federada (nome anterior para compartilhamento federado) para a organização do Exchange 2010 SP2. Conclua as etapas em [Configure federated delegação](https://go.microsoft.com/fwlink/p/?linkid=268410).

## Configurar o compartilhamento de disponibilidade entre organizações do Exchange 2013 e Exchange 2007

  - Configurar compartilhamento federado para a organização do Exchange 2013. Siga as instruções em [Configurar o compartilhamento federado](configure-federated-sharing-exchange-2013-help.md).ção do Active Directoryde
    1.  **Adicionar um servidor Exchange 2010 SP2**
        
        Um servidor Exchange 2010 SP2 com a função de servidor acesso para cliente deve ser instalado na organização do Exchange 2007. Se você tiver servidores Exchange 2010 existentes, eles devem ser atualizados para o Exchange 2010 SP2. Para obter informações sobre como instalar o Exchange 2010 em uma organização do Exchange 2007, consulte [Exchange 2007 - mapa de planejamento para atualização e coexistência](https://go.microsoft.com/fwlink/p/?linkid=268411).
    
    2.  **Configurar delegação federada**
        
        Configure delegação federada para a organização do Exchange 2007. Em um servidor Exchange 2010 SP2 na organização do Exchange 2007, conclua as etapas em [Configure federated delegação](https://go.microsoft.com/fwlink/p/?linkid=268410).
    
    3.  **Configurar sincronização do Active Directory**
        
        A sincronização do Active Directory deve ser configurada para todos os usuários que precisarem compartilhar informações de disponibilidade entre as organizações. Você pode configurar manualmente a sincronização do Active Directory ou usar um serviço automatizado de sincronização do Active Directory. Para configurar a sincronização do Active Directory, consulte as etapas abaixo:
        
          - **Pré-requisitos** Verifique se sua organização atende aos requisitos para instalação da sincronização do Active Directory.
            
            Para saber mais, consulte preparar para a sincronização do Active Directoryde [https://go.microsoft.com/fwlink/p/?LinkId=247302](https://go.microsoft.com/fwlink/p/?linkid=247302)
        
          - **Plano** Noções básicas sobre a Ferramenta de Sincronização de Diretórios do Microsoft Online Services e roteiro de instalação.
            
            Para saber mais, consulte [Sincronização do Active Directory: Roteiro](http://go.microsoft.com/fwlink/p/?linkid=203007)
        
          - **Instalação e Configuração** Configurar a sincronização do Active Directory entre sua organização local e organização de serviço inquilina do Office 365.
            
            Para saber mais, consulte [instalar e atualizar a ferramenta de sincronização de diretórios do Microsoft Online Services](https://go.microsoft.com/fwlink/p/?linkid=247303)
    
    4.  **Criar um espaço de endereçamento de disponibilidade**
        
        Crie um espaço de endereçamento de disponibilidade para a organização do Exchange 2013 remoto que direcione as solicitações de disponibilidade dos usuários de caixa de correio do Exchange 2007 para o servidor de Acesso para Cliente do Exchange 2010 SP2 na organização do Exchange 2007. Essa configuração permite que as solicitações de disponibilidade de usuários feitas pelos usuários do Exchange 2007 na organização do Exchange 2013 remoto sejam encaminhadas por proxy pelo servidor de Acesso para Cliente do Exchange 2010 na organização do Exchange 2007. O servidor de Acesso para Cliente do Exchange 2010 na organização do Exchange 2007 usa a confiança de federação e a relação de organização para enviar solicitações de disponibilidade para o ponto de extremidade de disponibilidade de floresta da organização do Exchange 2013 remoto.
        
        Para configurar o espaço de endereçamento de disponibilidade, no servidor de Acesso para Cliente do Exchange 2010 na organização do Exchange 2007, execute este comando no Shell de Gerenciamento do Exchange:
        
            Add-AvailabilityAddressSpace -AccessMethod InternalProxy -ProxyUrl https://<Exchange 2010 CAS server name>/ews/exchange.asmx -ForestName <SMTP domain of the remote Exchange organization> -UseServiceAccount $True
        
        Para detalhadas sobre sintaxe e informações de parâmetro, consulte Add-AvailabilityAddressSpacede [](https://go.microsoft.com/fwlink/p/?linkid=268413)

## Configurar o compartilhamento de disponibilidade entre organizações do Exchange 2013 e Exchange 2003

  - Configurar compartilhamento federado para a organização do Exchange 2013. Siga as instruções em [Configurar o compartilhamento federado](configure-federated-sharing-exchange-2013-help.md).

  - Siga estas instruções na organização do Exchange 2003:
    
    1.  **Adicionar o servidor do Exchange 2010 SP2**.
        
        Um servidor Exchange 2010 SP2 com a função de servidor acesso para cliente deve ser instalado na organização do Exchange 2003. Se você tiver servidores Exchange 2010 existentes, eles devem ser atualizados para o Exchange 2010 SP2. Para obter informações sobre como instalar o Exchange 2010 em uma organização do Exchange 2003, consulte [Exchange 2003 – mapa de planejamento para atualização e coexistência](https://go.microsoft.com/fwlink/?linkid=268414).
        

        > [!WARNING]
        > Para que o compartilhamento de disponibilidade funcione corretamente entre organizações do Exchange 2013 e Exchange 2003, a pasta pública <STRONG>OU=EXTERNAL (FYDIBOHF25SPDLT)</STRONG> deve existir na hierarquia de pastas públicas. Essa pasta será criada automaticamente no servidor de Caixa de Correio do Exchange 2010 na organização do Exchange 2003 apenas se você selecionar a opção de criar pastas públicas como parte da definição das configurações de cliente para suporte ao Outlook 2003 durante a instalação do Exchange 2010. Além disso, essa opção é apresentada durante o processo de instalação apenas se o servidor de Caixa de Correio do Exchange 2010 for o primeiro servidor de Caixa de Correio instalado na organização. Se a pasta pública <STRONG>OU=EXTERNAL (FYDIBOHF25SPDLT)</STRONG> não tiver sido criada durante a instalação, você terá que criá-la manualmente. Para ver detalhes sobre como criar essa pasta pública, consulte <A href="http://go.microsoft.com/fwlink/p/?linkid=3052&kbid=2555008">Como solucionar problemas de disponibilidade ao usar a federação do Exchange no Microsoft Office 365 para ambientes corporativos</A>.

    
    2.  **Configurar delegação federada**.
        
        Configure delegação federada para a organização do Exchange 2003. Em um servidor Exchange 2010 SP2 na organização do Exchange 2003, conclua as etapas em [Configure federated delegação](https://go.microsoft.com/fwlink/p/?linkid=268410).
    
    3.  **Configure a sincronização do Active Directory**.
        
        Sincronização do Active Directory deve ser configurada para todos os usuários que precisam compartilhar informações de disponibilidade entre as organizações. Você pode configurar a sincronização do Active Directory manualmente ou usar um serviço de sincronização do Active Directory automatizado. Para saber mais sobre a sincronização do Active Directory, consulte [Forefront Identity Management](https://go.microsoft.com/fwlink/?linkid=294645).
        
          - **Pré-requisitos** Verifique se sua organização atende aos requisitos para instalação da sincronização do Active Directory.
            
            Para saber mais, consulte preparar para a sincronização do Active Directoryde [https://go.microsoft.com/fwlink/p/?linkid=247302](https://go.microsoft.com/fwlink/p/?linkid=247302)
        
          - **Plano** Noções básicas sobre a Ferramenta de Sincronização de Diretórios do Microsoft Online Services e roteiro de instalação.
            
            Para saber mais, consulte [Sincronização do Active Directory: Roteiro](http://go.microsoft.com/fwlink/p/?linkid=203007)
        
          - **Instalação e Configuração** Configurar a sincronização do Active Directory entre sua organização local e organização de serviço inquilina do Office 365.
            
            Para saber mais, consulte [instalar e atualizar a ferramenta de sincronização de diretórios do Microsoft Online Services](https://go.microsoft.com/fwlink/p/?linkid=247303)
    
    4.  **Configure pastas públicas para compartilhamento de disponibilidade em sua organização do Exchange 2003.**
        
        Conclua as seguintes etapas em um servidor Exchange 2003:
        
          - No Gerenciador do Sistema do Exchange, navegue na árvore do console até **Grupos Administrativos** \> **Primeiro Grupo Administrativo** \> **Servidores**.
        
          - Selecione seu servidor do Exchange 2003 e navegue até **Primeiro Grupo de Armazenamento** \> **Repositório da Pasta Pública** \> **Pastas Públicas** \> **Disponibilidade do Schedule+**.
        
          - No painel de ação, selecione a pasta **UO=EXTERNO (FYDIBOHF25SPDLT)** para o **Primeiro grupo administrativo**.
        
          - Clique com o botão direito na pasta **OU=EXTERNO (FYDIBOHF25SPDLT)** e, em seguida, clique em **Propriedades**.
        
          - Em **Propriedades UO=EXTERNO (FYDIBOHF25SPDLT)**, selecione a guia **Replicação**.
        
          - Para replicar a pasta **OU=EXTERNAL (FYDIBOHF25SPDLT)** para o servidor de Acesso para Cliente/Caixa de Correio do Exchange 2010, clique em **Adicionar**.
        
          - Em **Selecionar um Repositório de Pasta Pública**, selecione o **Banco de Dados de Pasta Pública** do servidor de Acesso para Cliente/Caixa de Correio do Exchange 2010 e clique em **OK**.
            

            > [!NOTE]
            > Por padrão, o Exchange usa a agenda de replicação definida no banco de dados de pasta pública.

        
          - Clique em **OK** para fechar **Propriedades UO=EXTERNO (FYDIBOHF25SPDLT)** and salve as alterações.
        
          - Complete os mesmos procedimentos acima para a pasta **OU=Grupo Administrativo do Exchange (FYDIBOHF23SPDLT)**.
            

            > [!WARNING]
            > Dependendo do tamanho das pastas públicas, a replicação pode levar várias horas para ser concluída.

        
          - Depois que as pastas públicas **OU=EXTERNO (FYDIBOHF25SPDLT)** e **OU=Grupo Administrativo do Exchange (FYDIBOHF23SPDLT)** forem replicadas para o servidor de Acesso para Cliente/Caixa de Correio do Exchange 2010, você terá que remover as réplicas dessas pastas públicas no servidor do Exchange 2003.
    
    5.  **Modificar o parâmetro LegacyExchangeDN**
        
        Modifique o parâmetro *LegacyExchangeDN* em todos os objetos habilitados para email na organização do Exchange 2003 que referenciem a organização remota do Exchange 2013. Mude o valor da unidade organizacional (OU) existente do objeto habilitado para email para **Externo (FYDIBOHF25SPDLT)**. Por exemplo, **LegacyExchangeDN=/o=Primeira Organização/ou=Externo (FYDIBOHF25SPDLT)/cn=Recipients/cn=User Name**.
        
        Para modificar objetos habilitados para email na organização do Exchange 2003, você pode usar a [ferramenta Active Directory Service Interfaces Editor (Editor ADSI)](https://go.microsoft.com/fwlink/?linkid=294644) ou o [Microsoft Exchange Server LegacyDN Utility](http://go.microsoft.com/fwlink/?linkid=294643).

