---
title: 'Implantar o Exchange 2013 em uma topologia entre florestas: Exchange 2013 Help'
TOCTitle: Implantar o Exchange 2013 em uma topologia entre florestas
ms:assetid: 65be650f-d435-4f60-9ff0-5cb88a726abb
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Aa998597(v=EXCHG.150)
ms:contentKeyID: 51407867
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Implantar o Exchange 2013 em uma topologia entre florestas

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2016-12-09_

Este tópico explica como implantar um topologia entre florestas no Exchange 2013 usando o Microsoft Forefront Identity Manager 2010 R2 SP1. Para implantar o Exchange 2013 em uma topologia entre florestas, você deve primeiro instalar o Exchange 2013 em cada floresta, e então conectar as florestas para que os usuários possam ver os dados de disponibilidade e endereço entre as florestas.

A figura a seguir ilustra a sincronização do usuário entre duas florestas do Exchange 2013 .

**Exemplo de sincronização do Exchange 2013 entre florestas**

![Exemplo de várias florestas do Exchange 2010](images/Aa998597.df0ba5dd-cb96-4542-98bd-2a425defe317(EXCHG.150).gif "Exemplo de várias florestas do Exchange 2010")

Este tópico *não* descreve como implantar o Exchange 2013 em uma topologia de floresta dedicada (ou floresta de recurso) do Exchange . Para mais informações sobre como implantar o Exchange 2013 em uma topologia de floresta de recurso, veja [Implantar o Exchange 2013 em uma topologia de floresta de recursos do Exchange](deploy-exchange-2013-in-an-exchange-resource-forest-topology-exchange-2013-help.md).

## O que você precisa saber antes de começar?

Para realizar o procedimento a seguir no Exchange 2013, confirme o seguinte:

  - Você configurou corretamente o DNS (Sistema de Nome de Domínio) para a resolução de nomes entre florestas da organização. Para verificar se o DNS está configurado corretamente, use a ferramenta de ping para testar a conectividade em cada floresta pelas demais florestas de sua organização e pelo servidor no qual você executará o agente GAL Sync.

  - O agente de gerenciamento (MA) da GALSync se comunica com a floresta do Exchange 2013 usando o RTM do PowerShell do Windows . Verifique se o Windows PowerShell v1.0 não está instalado neste computador. Para isso, acesse o Painel de Controle e clique em Programas e Recursos.

  - Certifique-se de que o Gerenciamento Remoto do Windows não tenha sido instalado pelo Windows Update.

  - Instale o Windows PowerShell e o Gerenciamento Remoto do Windows. Para detalhes, veja o artigo 968930 da Base de Conhecimento da Microsoft, [Pacote Windows Management Framework Core (Windows PowerShell 2.0 e WinRM 2.0)](http://go.microsoft.com/fwlink/p/?linkid=3052&kbid=968930).

  - Baixe o Forefront Identity Manager 2010 R2 SP1. Consulte o [Download do Microsoft Forefront Identity Manager 2010 R2 SP1](https://go.microsoft.com/fwlink/p/?linkid=279868).

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>.



## Implantar o Exchange 2013 em uma topologia entre florestas com o Forefront Identity Manager 2010 R2 SP1

1.  Em cada floresta, instale o Exchange 2013 separadamente. Para instalar Exchange 2013, realize as mesmas etapas que você faria se você estivesse instalando o Exchange 2013 em uma topologia de floresta única. Para obter etapas detalhadas, consulte um dos seguintes tópicos:
    
      - [Implantar uma nova instalação do Exchange 2013](deploy-a-new-installation-of-exchange-2013-exchange-2013-help.md)
    
      - [Instalar o Exchange 2013 usando o Assistente para Configuração](install-exchange-2013-using-the-setup-wizard-exchange-2013-help.md)
        

        > [!NOTE]
        > Este tópico pressupõe que você não possui um existente Exchange 2007 ou Exchange 2010 topologia. Se você tiver uma topologia existente do Exchange e você deseja atualizar, consulte <A href="upgrade-from-exchange-2010-to-exchange-2013-exchange-2013-help.md">Atualizar do Exchange 2010 para o Exchange 2013</A> ou <A href="upgrade-from-exchange-2007-to-exchange-2013-exchange-2013-help.md">Atualização do Exchange 2007 para o Exchange 2013</A>.



2.  Em cada floresta, use os Usuários e Computadores do Active Directory para criar um contêiner no qual o FIM 2010 R2 SP1 criará contatos para cada caixa de correio de outra floresta. Recomendamos que você coloque o nome desse contêiner de **FromFIM**. Para criar o contêiner, escolha o domínio no qual você deseja criar o contêiner, clique com o botão direito no domínio, selecione **Novo** \> **Unidade Organizacional**. Em **Novo Objeto - Unidade Organizacional**, digite **FromFIM**, e depois clique em **OK**.

3.  Crie um agente de gerenciamento da GALSync para cada floresta usando o Forefront Identify Manager. Isto permite que você sincronize os usuários em cada floresta e crie uma GAL comum. Para as etapas detalhadas, veja os seguintes recursos:
    
      - [Configurando a sincronização de lista (GAL) de endereços Global com o Forefront Identity Manager (FIM) 2010](https://go.microsoft.com/fwlink/p/?linkid=279869)
    
      - [Trabalhar com os agentes de gerenciamento](https://go.microsoft.com/fwlink/p/?linkid=279870)
    
      - [O Forefront Identity Manager 2010 R2 Documentation Roadmap](https://go.microsoft.com/fwlink/p/?linkid=279871)
    

    > [!IMPORTANT]
    > Enquanto os recursos discutem Exchange 2010, Exchange 2013 é suportado para o FIM 2010 R2 SP1. Certifique-se de que você configura <STRONG>extensões</STRONG> no FIM 2010 R2 SP1 para Exchange 2013.

    
    1.  Na página **Configurar Extensões** , em **Configurar nome(s) para exibição da partição**, ao lado de **Configurar para**, selecione **Exchange 2013**. Você verá o campo **URI do Exchange 2013 RPS** . Digite a URI de um servidor de Acesso para Cliente do Exchange 2013 para ter certeza de que a conexão remota do PowerShell está funcionando. A **URI do Exchange 2013 RPS** deve estar no seguinte formato: http://CAS\_Server\_FQDN/Powershell. Clique em **OK**.
        

        > [!NOTE]
        > Certifique-se de que as credenciais de administrador usads para conectar-se à floresta do Exchange 2013 também podem fazer conexões remotas do PowerShell para aquela floresta.<BR>A figura a seguir mostra como selecionar a configuração para o Exchange 2013.

        
        **Configurar o Agente de Gerenciamento da GalSync para o Exchange 2013**
        
        ![Provisionamento do Agente de Gerenciamento do Exchange 2010](images/Aa998597.8f403cda-e5e4-4edf-887f-c1ed46cee3f5(EXCHG.150).gif "Provisionamento do Agente de Gerenciamento do Exchange 2010")  

4.  Crie um conector de envio SMTP em cada uma das florestas. Para conhecer etapas detalhadas, consulte [Configurar um conector de envio entre florestas](configure-a-cross-forest-send-connector-exchange-2013-help.md).

5.  Em cada floresta, habilite o serviço de Disponibilidade para que os usuários de cada floresta possam exibir dados de disponibilidade sobre os usuários da outra floresta. Para obter mais informações, consulte [Serviço de disponibilidade no Exchange 2013](availability-service-in-exchange-2013-exchange-2013-help.md).

6.  Se você deseja que o email seja recolocado em qualquer floresta na sua organização, você deve configurar um domínio naquela floresta como um domínio autoritativo. Para conhecer etapas detalhadas, consulte [Configurar o Exchange para aceitar emails de vários domínios autoritativos](configure-exchange-to-accept-mail-for-multiple-authoritative-domains-exchange-2013-help.md).

