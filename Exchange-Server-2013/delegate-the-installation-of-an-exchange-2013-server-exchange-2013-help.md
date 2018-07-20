---
title: 'Delegar a instalação de um servidor Exchange 2013: Exchange 2013 Help'
TOCTitle: Delegar a instalação de um servidor Exchange 2013
ms:assetid: f2fc8680-0c7c-4a29-b8f5-d77404fec280
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Bb201741(v=EXCHG.150)
ms:contentKeyID: 62614007
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Delegar a instalação de um servidor Exchange 2013

 

_**Aplica-se a:** Exchange Online, Exchange Server, Exchange Server 2013_

_**Tópico modificado em:** 2014-07-31_

Exchange Server 2013 permite delegar a instalação dos servidores Exchange para pessoas que não são membros do grupo de função de gerenciamento de organização da Exchange 2013. Isso geralmente é útil em grandes empresas onde as pessoas que instalar e configurar os servidores não são as mesmas pessoas que gerenciam os serviços, como Exchange. Se isso SOA como algo que você deseja fazer, este tópico é para você.

Normalmente, quando Exchange for instalado, as pessoas instalá-lo precisam ser membros do grupo de função [Gerenciamento da Organização](organization-management-exchange-2013-help.md) . Isso ocorre porque as alterações são feitas Active Directory quando Exchange está instalado, e apenas administradores Exchange, que são membros do grupo de funções de gerenciamento da organização, poderá fazer essas alterações. A lista a seguir mostra as alterações são feitas:

  - Um objeto de servidor é criado na partição de configuração **CN=Servers,CN=Exchange Administrative Group (FYDIBOHF23SPDLT),CN=Administrative Groups,CN=\<Organization Name\>,CN=Microsoft Exchange,CN=Services,CN=Configuration,DC=\<Root Domain\>** .

  - As seguintes entradas de controle de acesso (ACEs) são adicionadas ao objeto servidor dentro da partição de configuração para o grupo de função de instalação delegada:
    
      - Controle total sobre o objeto de servidor e seus objetos filhos
    
      - Negar a entrada de controle de acesso para a enviar como direito estendido
    
      - Negar a entrada de controle de acesso para a receber como direito estendido
    
      - Negar permissões CreateChild e DeleteChild para Exchange objetos de armazenamento de pasta pública
    

    > [!TIP]
    > Pastas públicas são administradas em um nível organizacional; Portanto, a criação e a exclusão de armazenamentos de pasta pública é restrito aos administradores Exchange.



  - A conta de computador Active Directory para o servidor é adicionada ao grupo de servidores Exchange.

  - O servidor é adicionado como um servidor provisionado no Exchange Admin Center.

Em grandes empresas, as pessoas que instalar e configurar novos servidores geralmente não são administradores Exchange. Para habilitá-los instalar o Exchange, um administrador Exchange pode *provisionar* o servidor em Active Directory. Quando um servidor é provisionado, todas as alterações necessárias para o novo servidor Exchange funcione são feitas em Active Directory separadamente da instalação real do Exchange em um computador. Um administrador Exchange pode provisionar um novo servidor em Active Directory horas ou até mesmo dias antes Exchange está instalado no novo computador. Após um servidor tenha sido provisionado, a pessoa que realizou as necessidades de instalação somente para ser um membro do grupo de função [Configuração Delegada](delegated-setup-exchange-2013-help.md) para instalar o Exchange. O grupo de função de instalação delegada só permite que os membros instalar servidores provisionados.

Lembre-se do seguinte ao pensar usando delegada a instalação:

  - Pelo menos um servidor de Exchange 2013 deve já estar instalado antes de você pode delegar a instalação dos servidores adicionais. A pessoa que instala o primeiro servidor precisa ser um administrador Exchange. Para obter mais informações, confira [Lista de verificação: Executar uma nova instalação do Exchange 2013](checklist-perform-a-new-installation-of-exchange-2013-exchange-2013-help.md).

  - Um usuário delegado não é possível desinstalar um servidor Exchange. Para desinstalar um servidor Exchange, você precisa ser um administrador Exchange.

## Como faço para provisionar um servidor Exchange 2013?

Para provisionar um servidor para Exchange, você precisa usar Exchange 2013 Setup Command-line. Se você não familiarizados com Windows Prompt de comando, não se preocupe. Este tópico o orienta exatamente o que você precisa fazer. Antes de começar, aqui estão algumas coisas em mente:

  - Você precisa ser um membro do grupo de funções de gerenciamento da organização para provisionar um servidor.

  - Você deve ter a versão mais recente do Exchange 2013. Você pode obter o link de download do [Atualizações para o Exchange 2013](updates-for-exchange-2013-exchange-2013-help.md).

O comando que você precisa usar para provisionar o servidor depende se você estiver executando a instalação do computador que você está provisionamento ou se você estiver executando a partir de outro computador. Escolha o comando nas etapas a seguir faz a correspondência de onde você está executando a instalação:

1.  Pressione a tecla Windows + R para abrir a janela **Executar**.

2.  Em **Abrir**, digite**cmd.exe**e pressione Enter para abrir um **Prompt de comando do Windows**.

3.  Altere os diretórios para onde você baixou e expandida a Exchange 2013 instalar arquivos. Se os arquivos de instalação estão localizados em `C:\Downloads\Exchange 2013`, use o seguinte comando.
    
        CD "C:\Downloads\Exchange 2013"

4.  Escolha o comando que faz a correspondência de onde você está executando a instalação:
    
      - **Se você estiver executando a instalação no computador que está sendo provisionado**, execute o seguinte comando:
        
            Setup.exe /NewProvisionedServer /IAcceptExchangeServerLicenseTerms
    
      - **Se você estiver executando a instalação em outro computador**, execute o seguinte comando:
        
            Setup.exe /NewProvisionedServer:<ComputerName> /IAcceptExchangeServerLicenseTerms

5.  Depois que você configurar o servidor, você precisará certificar-se de que você tenha adicionado os usuários que devem ser capazes de instalar Exchange nos servidores provisionados para o grupo de função de instalação delegada. Para ver como adicionar usuários a um grupo de funções, consulte [Add members to a role group](manage-role-group-members-exchange-2013-help.md).

Quando você terminar estas etapas, o computador estará pronto para Exchange a serem instalados. Exchange 2013 pode ser instalado em um servidor provisionado usando as etapas descritas em [Instalar o Exchange 2013 usando o Assistente para Configuração](install-exchange-2013-using-the-setup-wizard-exchange-2013-help.md).

## Como saber se funcionou?

Para certificar-se de que o servidor foi provisionado corretamente para Exchange, você pode fazer o seguinte:

1.  Vá para **Iniciar** \> **Ferramentas administrativas** e, em seguida, open **e computadores do Active Directory Users**.

2.  Selecione os **Grupos de segurança do Microsoft Exchange**, clique duas vezes em **Servidores Exchange** e selecione a guia **membros**.

3.  Na guia **membros**, verifique se o servidor que você acabou de ser provisionado está listado como membro do grupo de segurança.

Se o seu servidor está listado como um membro do grupo de segurança de servidores Exchange, foi provisionado corretamente. Alguém que seja membro do grupo de função de instalação delegada agora pode instalar Exchange nesse servidor.

Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), ou [Proteção do Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=285351).

Você encontrou o que você está procurando? Por favor, separe um minuto do seu tempo para [enviar seus comentários para nós](mailto:exsetuphelpfeedback@microsoft.com?subject=exchange%202013%20setup%20help%20feedback) sobre as informações que você estava esperando encontrar.

