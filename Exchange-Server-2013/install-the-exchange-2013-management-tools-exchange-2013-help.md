---
title: 'Instalar as ferramentas de gerenciamento do Exchange 2013: Exchange 2013 Help'
TOCTitle: Instalar as ferramentas de gerenciamento do Exchange 2013
ms:assetid: 71fcbe4c-783b-4f77-aabb-a21aa7a4ef23
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Bb232090(v=EXCHG.150)
ms:contentKeyID: 50556230
ms.date: 01/10/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Instalar as ferramentas de gerenciamento do Exchange 2013

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2013-01-28_

Com as ferramentas de gerenciamento do Microsoft Exchange Server 2013, é possível configurar e gerenciar remotamente a organização do Exchange. As ferramentas de gerenciamento do Exchange 2013 incluem o Shell de Gerenciamento do Exchange e a Caixa de Ferramentas do Exchange. Este tópico explica como é possível usar tanto o Setup.exe quanto o modo de instalação autônoma para instalar as ferramentas de gerenciamento do Exchange 2013.


> [!TIP]
> Não é preciso executar este procedimento para usar o Centro de Administração do Exchange (EAC) remotamente. O EAC é um console baseado na Web hospedado em computadores com a função de servidor de Acesso para Cliente do Exchange 2013. Para saber mais sobre como acessar o EAC remotamente, confira <A href="exchange-admin-center-in-exchange-2013-exchange-2013-help.md">Centro de administração do Exchange no Exchange 2013</A>.



Para mais informações sobre como gerenciar o Exchange 2013, confira [Centro de administração do Exchange no Exchange 2013](exchange-admin-center-in-exchange-2013-exchange-2013-help.md) e [Usando o PowerShell com o Exchange 2013 (Shell de gerenciamento do Exchange)](https://technet.microsoft.com/pt-br/library/bb123778\(v=exchg.150\)).

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: 10 minutos

  - Certifique-se de ter lido as notas de versão antes de instalar o Exchange 2013. Para mais informações, confira [Notas de versão do Exchange 2013](release-notes-for-exchange-2013-exchange-2013-help.md).

  - O computador em que você instala as ferramentas de gerenciamento deve ter um sistema operacional suportado (como Windows Server 2012 ou Windows 8), ter espaço em disco suficiente, ser membro de um domínio Active Directory e atender a outros requisitos. Para saber mais sobre os requisitos do sistema, confira [Requisitos de sistema do Exchange 2013](exchange-2013-system-requirements-exchange-2013-help.md).

  - Para executar a instalação do Exchange 2013, é necessário instalar o Microsoft .NET Framework 4.5, Windows Management Framework 3.0 e outros softwares necessários. Para conhecer os pré-requisitos de todas as funções de servidor, confira [Pré-requisitos do Exchange 2013](exchange-2013-prerequisites-exchange-2013-help.md).

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>.



## Usar a Instalação para instalar as ferramentas de gerenciamento do Exchange 2013

1.  Faça logon no computador no qual deseja instalar o Exchange 2013.

2.  Navegue até o local de rede dos arquivos de instalação do Exchange 2013.

3.  Iniciar a Instalação do Exchange 2013 clicando duas vezes em `Setup.exe`
    

    > [!IMPORTANT]
    > Se o Controle de Acesso de Usuário (UAC) estiver habilitado, você deverá clicar com o botão direito do mouse em <CODE>Setup.exe</CODE> e selecionar <STRONG>Executar como administrador</STRONG>.



4.  Na página **Verificar se Há Atualizações**, escolha se deseja que a Instalação se conecte à Internet e baixe atualizações de segurança e produtos para o Exchange 2013. Se você selecionar **Conectar-se à Internet e verificar se há atualizações**, a Instalação baixará e aplicará atualizações antes de continuar. Se você selecionar **Não verificar atualizações agora**, poderá baixar e instalar atualizações manualmente mais tarde. Convém baixar e instalar atualizações agora. Clique em **Avançar** para continuar.

5.  
    
    A página **Introdução** inicia o processo de instalação do Exchange na sua organização. Ela o guiará pela instalação. Vários links para conteúdo útil de implantação estão listados. Recomendamos que você visite esses links antes de continuar a instalação. Clique em **Avançar** para continuar.

6.  
    
    Na página **Contrato de Licença**, examine os termos de licença do software. Se você concordar com os termos, selecione **Aceito os termos do contrato de licença** e clique em **Avançar**.

7.  
    
    Na página **Configurações recomendadas**, selecione se deseja usar as configurações recomendadas. Caso selecione **Usar configurações recomendadas**, o Exchange automaticamente enviará relatórios de erros e informações à Microsoft sobre o hardware do seu computador e como você usa o Exchange. Se você selecionar **Não usar as configurações recomendadas**, essas configurações permanecerão desabilitadas, mas você poderá habilitá-las a qualquer momento após o término da Instalação. Para obter mais informações sobre essas configurações e como as informações enviadas à Microsoft são usadas, clique em **?**.

8.  
    
    Na página **Seleção de Função de Servidor**, verifique se a opção **Ferramentas de Gerenciamento** está selecionada.
    
    Selecione **Instalar automaticamente as funções e os recursos do Windows Server necessários para instalar o Exchange Server** para que o assistente de Instalação instale os pré-requisitos necessários do Windows. Talvez seja necessário reiniciar o computador para concluir a instalação de alguns recursos do Windows. Se você não selecionar essa opção, deverá instalar os recursos do Windows manualmente.
    

    > [!TIP]
    > Essa opção instala apenas os recursos do Windows necessários para o Exchange. Você deve instalar manualmente outros pré-requisitos. Para obter mais informações, confira <A href="exchange-2013-prerequisites-exchange-2013-help.md">Pré-requisitos do Exchange 2013</A>.

    
    Clique em **Avançar** para continuar.

9.  Na página **Espaço e local da instalação**, aceite o local de instalação padrão ou clique em **Procurar** para escolher um novo local. Verifique se você tem espaço em disco suficiente disponível no local onde deseja instalar o Exchange. Clique em **Avançar** para continuar.

10. 
    
    Se for a primeira vez que você executa a Instalação do Exchange 2013 em sua organização, na página **Organização do Exchange**, digite um nome para sua organização do Exchange. O nome da organização do Exchange só pode conter os seguintes caracteres:
    
      - A a Z
    
      - a a z
    
      - 0 a 9
    
      - Espaço (exceto no início ou no final)
    
      - Hífen ou travessão
        

        > [!TIP]
        > O nome da organização não pode conter mais de 64 caracteres. O nome da organização não pode ficar em branco.

    
    Se quiser usar o modelo de permissões de divisão do Active Directory, selecione **Aplicar modelo de segurança de permissões divididas do Active Directory à organização do Exchange**.
    

    > [!WARNING]
    > A maioria das organizações não precisa aplicar o modelo de permissões de divisão do Active Directory. Se você precisar de gerenciamento separado das entidades de segurança do Active Directory e da configuração do Exchange, as permissões de divisão do Controle de Acesso Baseado na Função (RBAC) poderão funcionar para você. Para maiores informações, clique em <STRONG>?</STRONG>.

    
    Clique em **Avançar** para continuar.

11. 
    
    Na página **Verificações de Preparação**, exiba o status para determinar se as verificações de pré-requisitos de função de servidor e da organização foram concluídas com êxito. Se essas verificações não forem concluídas com êxito, será necessário resolver todos os erros relatados antes de instalar o Exchange 2013. Você não precisa sair da Instalação durante a resolução de alguns dos erros de pré-requisitos. Após resolver um erro informado, clique em **Voltar** e em **Avançar** para executar a verificação de pré-requisito novamente. Lembre-se de rever também todos os avisos relatados. Se todas as verificações de preparação tiverem sido concluídas com sucesso, clique em **Avançar** para instalar o Exchange 2013.

12. 
    
    Na página **Conclusão**, clique em **Concluir**.

13. Reinicie o computador depois que o Exchange 2013 terminar.

## Usar modo Instalação autônoma para instalar as ferramentas de gerenciamento do Exchange 2013

1.  Faça logon no computador em que deseja instalar as ferramentas de gerenciamento do Exchange 2013.

2.  Navegue até o local de rede dos arquivos de instalação do Exchange 2013.

3.  No prompt de comando, execute o seguinte comando:
    

    > [!IMPORTANT]
    > Se o Controle de Acesso de Usuário (UAC) estiver habilitado, você deverá executar o <CODE>Setup.exe</CODE> em um prompt de comando elevado.

    
        Setup.exe /Role:ManagementTools /IAcceptExchangeServerLicenseTerms

Para saber mais, confira [Instalar o Exchange 2013 usando o modo autônomo](install-exchange-2013-using-unattended-mode-exchange-2013-help.md).

