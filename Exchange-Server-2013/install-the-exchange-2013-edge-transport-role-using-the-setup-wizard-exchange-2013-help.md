---
title: 'Instalar a função de Transporte de Borda do Exchange 2013 usando o Assistente para Configuração: Exchange 2013 Help'
TOCTitle: Instalar a função de Transporte de Borda do Exchange 2013 usando o Assistente para Configuração
ms:assetid: b8e51b0b-201e-4c64-92c8-3ac0db04b6e2
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Dn635117(v=EXCHG.150)
ms:contentKeyID: 61203510
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Instalar a função de Transporte de Borda do Exchange 2013 usando o Assistente para Configuração

 

_**Aplica-se a:**Exchange Server, Exchange Server 2013_

_**Tópico modificado em:**2014-06-19_

Este tópico explica como usar o assistente de instalação do Microsoft Exchange Server 2013 para instalar a função de servidor de Transporte de Borda do Exchange 2013 em um computador. A função de Transporte de Borda está disponível com o Exchange 2013 Service Pack 1 (SP1) ou posterior. Para obter mais informações sobre o planejamento e a implantação do Exchange 2013, consulte [Planejamento e implantação](planning-and-deployment-for-exchange-2013-installation-instructions.md).

Recomendamos que a função Transporte de Borda seja instalada na rede de perímetro fora da floresta interna Active Directory da sua organização. Mesmo sendo possível instalar a função de servidor Transporte de Borda em um computador que faz parte de um domínio, isso irá habilitar apenas o gerenciamento de domínio de recursos e configurações Windows. A função de Transporte de Borda por si só não usa propriamente Active Directory. Em vez disso, ela usa o recurso Active Directory Lightweight Directory Services (AD LDS) Windows para armazenar a configuração e informações sobre o destinatário. Para obter mais informações sobre a função de Transporte de Borda, consulte [Servidores de Transporte de Borda](edge-transport-servers-exchange-2013-help.md).

Se deseja instalar as funções do Acesso para Cliente ou Caixa de Correio do Exchange 2013 em um computador, consulte [Instalar o Exchange 2013 usando o Assistente para Configuração](install-exchange-2013-using-the-setup-wizard-exchange-2013-help.md). A função Transporte de Borda não pode ser instalada no mesmo computador que tiver as funções de servidor de Caixa de Correio e Acesso para Cliente instaladas.


> [!TIP]
> Você já ouviu falar do Assistente de Implantação do Exchange Server? É uma ferramenta online gratuita que ajuda a implantar rapidamente o Exchange 2013 em sua organização. Ele faz algumas perguntas e cria uma lista de verificação de implantação personalizada para você. Se você quiser saber mais sobre ele, consulte <A href="exchange-server-deployment-assistant-exchange-2013-help.md">Assistente de implantação do Exchange Server</A>.



Para obter informações sobre tarefas a serem concluídas após a instalação, consulte [Tarefas de pós-instalação do Exchange 2013](exchange-2013-post-installation-tasks-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: 40 minutos

  - Certifique-se de ter lido as notas de versão antes de instalar o Exchange 2013. Para obter mais informações, consulte [Notas de versão do Exchange 2013](release-notes-for-exchange-2013-exchange-2013-help.md).

  - O computador no qual instalar o Exchange 2013 deve ter um sistema operacional compatível (como Windows Server 2008 R2 com Service Pack 1 (SP1), Windows Server 2012 R2, ou Windows Server 2012), ter espaço em disco suficiente e atender a outros requisitos. Para obter informações sobre os requisitos do sistema, consulte [Requisitos de sistema do Exchange 2013](exchange-2013-system-requirements-exchange-2013-help.md).

  - Para executar a instalação do Exchange 2013, você deve instalar o .NET Framework 4.5, Management Framework Windows da Microsoft, e outros software necessários. Para conhecer os pré-requisitos de todas as funções de servidor, consulte [Pré-requisitos do Exchange 2013](exchange-2013-prerequisites-exchange-2013-help.md).

  - Você precisa configurar o sufixo DNS primário do computador. Por exemplo, se o nome do domínio totalmente qualificado do seu computador for edge.contoso.com, o sufixo do DNS do computador será contoso.com. Para obter mais informações, consulte [Sufixo DNS primário estiver faltando](primary-dns-suffix-is-missing-exchange-2013-help.md).

  - Os servidores de Transporte de Hub Exchange 2007 e Exchange 2010 precisam de atualização antes de você criar uma Assinatura do EdgeSync entre eles e um servidor de Transporte de Borda Exchange 2013. Se você não instalar esta atualização, a assinatura do EdgeSync não funcionará corretamente. Para obter mais informações, consulte a seção dos "Cenários de coexistência suportados" [Requisitos de sistema do Exchange 2013](exchange-2013-system-requirements-exchange-2013-help.md).

  - Certifique-se de que sua conta faça parte do grupo local de Administradores no computador em que você está instalando a função Transporte de Borda.

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!WARNING]
> Depois de instalar o Exchange em um servidor, não altere o nome do servidor. Não há suporte para renomear o servidor após a instalação de uma função de servidor Exchange.



## Instalar o Exchange Server 2013


> [!TIP]
> Para baixar a versão mais recente do Exchange 2013, consulte <A href="updates-for-exchange-2013-exchange-2013-help.md">Atualizações para o Exchange 2013</A>.



1.  Faça logon no computador em que deseja instalar o Exchange 2013.

2.  Navegue até o local de rede dos arquivos de instalação do Exchange 2013.

3.  Inicie a Instalação do Exchange 2013 clicando duas vezes em `Setup.exe`
    

    > [!IMPORTANT]
    > Se o Controle de Acesso de Usuário (UAC) estiver habilitado, você deverá clicar com o botão direito do mouse em <CODE>Setup.exe</CODE> e selecionar <STRONG>Executar como administrador</STRONG>.



4.  Na página **Verificar se há atualizações?**, escolha se deseja que a Instalação se conecte à Internet e baixe as atualizações de produto e de segurança para o Exchange 2013. Se você selecionar **Conectar-se à Internet e verificar se há atualizações**, a Instalação baixará as atualizações e as aplicará antes de continuar. Caso selecione **Não verificar atualizações agora**, você poderá baixar e instalar as atualizações manualmente mais tarde. Recomendamos que você baixe e instale as atualizações agora. Clique em **Avançar** para continuar.

5.  
    
    A página **Introdução** inicia o processo de instalação do Exchange na sua organização. Ela o guiará pela instalação. Vários links para conteúdo útil de implantação estão listados. Recomendamos que você visite esses links antes de continuar a instalação. Clique em **Avançar** para continuar.

6.  
    
    Na página **Contrato de Licença**, leia os termos de licença do software. Se concordar com os termos, selecione **Aceito os termos do contrato de licença** e clique em **Avançar**.

7.  
    
    Na página **Configurações recomendadas**, selecione se deseja usar as configurações recomendadas. Caso selecione **Usar configurações recomendadas**, o Exchange enviará automaticamente relatórios de erros e informações à Microsoft sobre o hardware do seu computador e como você usa o Exchange. Se você selecionar **Não usar as configurações recomendadas**, essas configurações permanecerão desabilitadas, mas você poderá habilitá-las a qualquer momento após o término da Instalação. Para obter mais informações sobre essas configurações e como as informações enviadas à Microsoft são usadas, clique em **?**.

8.  
    
    Na página **Seleção de Função de Servidor**, selecione **Transporte de Borda**. Lembre-se de que não é possível adicionar as funções de servidor de Caixa de Correio ou de Acesso para Cliente a um computador que tenha a função de Transporte de Borda instalada. As ferramentas de gerenciamento serão instaladas automaticamente se você instalar qualquer função de servidor.
    
    Selecione **Instalar automaticamente as funções e os recursos do Windows Server necessários para instalar o Exchange Server** para que o assistente de Instalação instale os pré-requisitos necessários do Windows. Talvez seja necessário reiniciar o computador para concluir a instalação de alguns recursos do Windows. Se você não selecionar essa opção, deverá instalar os recursos do Windows manualmente.
    

    > [!TIP]
    > Esta opção instala apenas os recursos do Windows necessários para o Exchange. Deverá instalar outros pré-requisitos manualmente. Para obter mais informações, consulte <A href="exchange-2013-prerequisites-exchange-2013-help.md">Pré-requisitos do Exchange 2013</A>.

    
    Clique em **Avançar** para continuar.

9.  Na página **Espaço de Instalação e Localização**, aceite a localização de instalação padrão ou clique em **Procurar** para escolher uma nova localização. Verifique se você possui espaço em disco suficiente na localização em que deseja instalar o Exchange. Clique em **Avançar** para continuar.

10. 
    
    Na página **Verificações de Preparação**, exiba o status para determinar se as verificações de pré-requisitos de função de servidor e da organização foram concluídas com êxito. Se essas verificações não forem concluídas com êxito, será necessário resolver todos os erros relatados antes de instalar o Exchange 2013. Não é necessário sair da Instalação durante a resolução de alguns dos erros de pré-requisitos. Após resolver um erro informado, clique em **Voltar** e em **Avançar** para executar a verificação de pré-requisito novamente. Lembre-se de rever também todos os avisos relatados. Se todas as verificações de preparação tiverem sido concluídas com sucesso, clique em **Avançar** para instalar o Exchange 2013.

11. 
    
    Na página **Conclusão**, clique em **Concluir**.

12. Reinicie o computador após a conclusão do Exchange 2013.

13. Conclua sua implantação executando as tarefas fornecidas no [Tarefas de pós-instalação do Exchange 2013](exchange-2013-post-installation-tasks-exchange-2013-help.md).

## Como saber se funcionou?

Para verificar se instalou com sucesso o Exchange 2013, consulte [Verificar uma instalação do Exchange 2013](verify-an-exchange-2013-installation-exchange-2013-help.md).

Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), ou [Proteção do Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=285351).

Você encontrou o que você está procurando? Por favor, separe um minuto do seu tempo para [enviar seus comentários para nós](mailto:exsetuphelpfeedback@microsoft.com?subject=exchange%202013%20setup%20help%20feedback) sobre as informações que você estava esperando encontrar.

