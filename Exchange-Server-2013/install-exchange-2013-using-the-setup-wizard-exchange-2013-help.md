---
title: 'Instalar o Exchange 2013 usando o Assistente para Configuração: Exchange 2013 Help'
TOCTitle: Instalar o Exchange 2013 usando o Assistente para Configuração
ms:assetid: da690d47-3384-4430-a69e-0cd4d3bf80a7
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Bb124778(v=EXCHG.150)
ms:contentKeyID: 50486772
ms.date: 01/10/2018
mtps_version: v=EXCHG.150
f1_keywords:
- Microsoft.Exchange.Management.ExSetupUI.SetupWizardForm.IntroductionPage
ms.translationtype: HT
---

# Instalar o Exchange 2013 usando o Assistente para Configuração

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2014-06-19_

Este tópico explica como usar o assistente de instalação do Microsoft Exchange Server 2013 para instalar as funções de Caixa de Correio e Acesso para Cliente do Exchange 2013 em um computador. Para obter mais informações sobre o planejamento e a implantação do Exchange 2013, consulte [Planejamento e implantação](planning-and-deployment-for-exchange-2013-installation-instructions.md).

Se desejar instalar a função de Transporte de Borda do Exchange 2013 em um computador, consulte [Instalar a função de Transporte de Borda do Exchange 2013 usando o Assistente para Configuração](install-the-exchange-2013-edge-transport-role-using-the-setup-wizard-exchange-2013-help.md). A função Transporte de Borda não pode ser instalada no mesmo computador que tiver as funções de servidor de Caixa de Correio e Acesso para Cliente instaladas.


> [!TIP]
> Você já ouviu falar do Assistente de Implantação do Exchange Server? É uma ferramenta online gratuita que ajuda a implantar rapidamente o Exchange 2013 em sua organização. Ele faz algumas perguntas e cria uma lista de verificação de implantação personalizada para você. Se você quiser saber mais sobre ele, consulte <A href="exchange-server-deployment-assistant-exchange-2013-help.md">Assistente de implantação do Exchange Server</A>.




> [!TIP]
> Depois de instalar qualquer função de servidor em um computador executando o Exchange 2013, não será possível usar o assistente de Instalação do Exchange 2013&nbsp;para adicionar outras funções de servidor ao computador. Se você quiser adicionar mais funções de servidor a um computador, use Adicionar ou Remover Programas no Painel de Controle ou Setup.exe na janela de prompt de comando.



Para obter informações sobre tarefas a serem concluídas após a instalação, consulte [Tarefas de pós-instalação do Exchange 2013](exchange-2013-post-installation-tasks-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: 60 minutos

  - Certifique-se de ter lido as notas de versão antes de instalar o Exchange 2013. Para mais informações, consulte [Notas de versão do Exchange 2013](release-notes-for-exchange-2013-exchange-2013-help.md).

  - Cada organização precisa de, no mínimo, um servidor de Acesso para Cliente e um servidor de Caixa de Correio na floresta do Active Directory. Além disso, todo site do Active Directory que contenha um servidor de Caixa de Correio também deve conter um servidor de Acesso para Cliente, pelo menos. Se você estiver separando suas funções de servidor, recomendamos instalar primeiro a função de servidor Caixa de Correio.

  - O computador no qual instalar o Exchange 2013 deve ter um sistema operacional compatível (como Windows Server 2008 R2 com Service Pack 1 (SP1) ou Windows Server 2012), ter espaço em disco suficiente, ser membro de um domínio de Active Directory e atender a outros requisitos. Para obter informações sobre os requisitos do sistema, consulte [Requisitos de sistema do Exchange 2013](exchange-2013-system-requirements-exchange-2013-help.md).

  - Para executar a instalação do Exchange 2013, é necessário instalar o Microsoft .NET Framework 4.5, Windows Management Framework 3.0 e outros softwares necessários. Para conhecer os pré-requisitos de todas as funções de servidor, consulte [Pré-requisitos do Exchange 2013](exchange-2013-prerequisites-exchange-2013-help.md).

  - Certifique-se de que a conta que você usa tenha sido delegada a associação ao grupo Administradores do Esquema, se você não tiver preparado anteriormente o esquema do Active Directory. Se você estiver instalando o primeiro servidor do Exchange 2013 da organização, a conta usada deverá ser associada ao grupo Administradores de Empresas. Se você já tiver preparado o esquema e não estiver instalando o primeiro servidor do Exchange 2013 da organização, deverá usar uma conta associada ao grupo de função de Gerenciamento da Organização do Exchange 2013.
    
    Os administradores que são membros do grupo de função de Instalação Delegada podem implantar servidores do Exchange 2013 que tenham sido previamente configurados por um membro do grupo de função de Gerenciamento da Organização.

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!WARNING]
> Depois de instalar o Exchange em um servidor, não altere o nome do servidor. Não há suporte para renomear o servidor após a instalação de uma função de servidor Exchange.



## Instalar o Exchange Server 2013

Se estiver instalando o primeiro servidor do Exchange 2013 na organização e as etapas de preparação do Active Directory não tiverem sido executadas, a conta usada deverá ser membro do grupo Administradores de Empresas. Se não preparou o Esquema do Active Directory antecipadamente, a conta deverá também ser membro do grupo Administradores de Esquema. Para obter informações sobre como preparar o Active Directory para o Exchange 2013, consulte [Preparar o Active Directory e domínios](prepare-active-directory-and-domains-exchange-2013-help.md). Se já tiver executado as etapas de preparação do Esquema e do Active Directory, a conta usada deve ser membro do grupo de funções de gerenciamento de Instalação Delegada ou do grupo de funções de Gerenciamento da Organização.


> [!TIP]
> Para baixar a versão mais recente do Exchange 2013, consulte <A href="updates-for-exchange-2013-exchange-2013-help.md">Atualizações para o Exchange 2013</A>.



1.  Faça logon no computador no qual deseja instalar o Exchange 2013.

2.  Navegue até o local de rede dos arquivos de instalação do Exchange 2013.

3.  Iniciar a Instalação do Exchange 2013 clicando duas vezes em `Setup.exe`
    

    > [!IMPORTANT]
    > Se o Controle de Acesso de Usuário (UAC) estiver habilitado, você deverá clicar com o botão direito do mouse em <CODE>Setup.exe</CODE> e selecionar <STRONG>Executar como administrador</STRONG>.



4.  Na página **Verificar se há atualizações?**, escolha se deseja que a Configuração se conecte à Internet e baixe as atualizações de produto e de segurança para o Exchange 2013. Se você selecionar **Conectar-se à Internet e verificar se há atualizações**, a Instalação baixará as atualizações e as aplicará antes de continuar. Caso selecione **Não verificar atualizações agora**, você poderá baixar e instalar as atualizações manualmente depois. Recomendamos que você baixe e instale as atualizações agora. Clique em **Avançar** para continuar.

5.  
    
    A página **Introdução** inicia o processo de instalação do Exchange na sua organização. Ela o guiará pela instalação. Vários links para conteúdo útil de implantação estão listados. Recomendamos que você visite esses links antes de continuar a instalação. Clique em **Avançar** para continuar.

6.  
    
    Na página do **Contrato de Licença**, examine os termos da licença do software. Se aceitar os termos, selecione **Aceito os termos do contrato de licença** e clique em **Avançar**.

7.  
    
    Na página **Configurações recomendadas**, selecione se deseja usar as configurações recomendadas. Caso selecione **Usar configurações recomendadas**, o Exchange enviará automaticamente relatórios de erros e informações à Microsoft sobre o hardware do seu computador e como você usa o Exchange. Se você selecionar **Não usar as configurações recomendadas**, essas configurações permanecerão desabilitadas, mas você poderá habilitá-las a qualquer momento após o término da Instalação. Para obter mais informações sobre essas configurações e como as informações enviadas à Microsoft são usadas, clique em **?**.

8.  
    
    Na página **Seleção da Função de Servidor**, escolha se deseja instalar a **função de Caixa de Correio**, a **função de Acesso para Cliente**, ambas as funções ou apenas as **Ferramentas de Gerenciamento** neste computador. Posteriormente, você pode adicionar outras funções de servidor, se optar por não instalá-las durante esta instalação. Uma organização deve ter pelo menos uma função de Caixa de Correio e pelo menos uma função de servidor de Acesso para Cliente instaladas. Elas podem ser instaladas no mesmo computador ou em computadores separados. As ferramentas de gerenciamento serão instaladas automaticamente se você instalar qualquer função de servidor.
    
    Selecione **Instalar automaticamente as funções e os recursos do Windows Server necessários para instalar o Exchange Server** para que o assistente de Instalação instale os pré-requisitos necessários do Windows. Talvez seja necessário reiniciar o computador para concluir a instalação de alguns recursos do Windows. Se você não selecionar essa opção, deverá instalar os recursos do Windows manualmente.
    

    > [!TIP]
    > Esta opção instala apenas os recursos do Windows necessários para o Exchange. Você deve instalar manualmente outros pré-requisitos. Para mais informações, consulte <A href="exchange-2013-prerequisites-exchange-2013-help.md">Pré-requisitos do Exchange 2013</A>.

    
    Clique em **Avançar** para continuar.

9.  Na página **Espaço e local da instalação**, aceite o local de instalação padrão ou clique em **Procurar** para escolher um novo local. Verifique se você tem espaço em disco suficiente disponível no local onde deseja instalar o Exchange. Clique em **Avançar** para continuar.

10. 
    
    Se este for o primeiro servidor Exchange em sua organização, na página **Organização do Exchange**, digite um nome para sua organização do Exchange. O nome da organização do Exchange só pode conter os seguintes caracteres:
    
      - A a Z
    
      - a a z
    
      - 0 a 9
    
      - Espaço (exceto no início ou no final)
    
      - Hífen ou travessão
        

        > [!TIP]
        > O nome da organização não pode conter mais de 64 caracteres. O nome da organização não pode ficar em branco.

    
    Se quiser usar o modelo de permissões de divisão doActive Directory, selecione **Aplicar modelo de segurança de permissões divididas do Active Directory à organização do Exchange**.
    

    > [!WARNING]
    > A maioria das organizações não precisa aplicar o modelo de permissões de divisão do Active Directory. Se precisar separar o gerenciamento das entidades de segurança doActive Directory e da configuração do Exchange, as permissões de divisão do Controle de Acesso Baseado na Função (RBAC) poderão funcionar para você. Para maiores informações, clique em <STRONG>?</STRONG>.

    
    Clique em **Avançar** para continuar.

11. Se estiver instalando a função de Caixa de correio, na página **Configurações de Proteção contra Malware**, escolha se deseja habilitar ou desabilitar a verificação de malware. Se você desabilitar a verificação de malware, ela poderá ser habilitada no futuro. Clique em **Avançar** para continuar.

12. 
    
    Na página **Verificações de Preparação**, exiba o status para determinar se as verificações de pré-requisitos de função de servidor e da organização foram concluídas com êxito. Se ainda não foram concluídas com sucesso, você deve corrigir quaisquer erros reportados antes de instalar o Exchange 2013. Não é preciso sair da instalação para corrigir alguns dos erros de pré-requisitos. Após resolver um erro informado, clique em **Voltar** e em **Avançar** para executar a verificação de pré-requisito novamente. Lembre-se de rever também todos os avisos relatados. Se todas as verificações de preparação tiverem sido concluídas com sucesso, clique em **Avançar** para instalar o Exchange 2013.

13. 
    
    Na página **Conclusão**, clique em **Concluir**.

14. Reinicie o computador depois que o Exchange 2013 terminar.

15. Conclua sua implantação executando as tarefas fornecidas no [Tarefas de pós-instalação do Exchange 2013](exchange-2013-post-installation-tasks-exchange-2013-help.md).

## Como saber se funcionou?

Para verificar se instalou com sucesso o Exchange 2013, consulte [Verificar uma instalação do Exchange 2013](verify-an-exchange-2013-installation-exchange-2013-help.md).

Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), ou [Proteção do Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=285351).

Você encontrou o que você está procurando? Por favor, separe um minuto do seu tempo para [enviar seus comentários para nós](mailto:exsetuphelpfeedback@microsoft.com?subject=exchange%202013%20setup%20help%20feedback) sobre as informações que você estava esperando encontrar.

