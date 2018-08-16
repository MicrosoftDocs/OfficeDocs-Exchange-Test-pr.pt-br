---
title: 'Serviço de Publicação na World Wide Web desabilitado ou ausente'
TOCTitle: O serviço de publicação na World Wide Web estiver desabilitada ou missing_ShouldReRunSetupForW3SVC
ms:assetid: f1815a6d-d16b-4271-9fab-84087465529e
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/ms.exch.setupreadiness.shouldrerunsetupforw3svc(v=EXCHG.150)
ms:contentKeyID: 50486979
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# O serviço de publicação na World Wide Web estiver desabilitada ou missing\_ShouldReRunSetupForW3SVC

 

_**Aplica-se a:** Exchange Server_

_**Tópico modificado em:** 2012-06-05_

O conteúdo neste tópico não foi atualizado para o Microsoft Exchange Server 2013. Mesmo assim, ele ainda pode se aplicar ao Exchange 2013. Se você ainda precisar de ajuda, verifique os recursos da comunidade, abaixo.

Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), ou [Proteção do Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=285351).

Instalação do Microsoft® Exchange Server 2007 não pode continuar porque ao tentar instalar a função de servidor de caixa de correio ou de acesso para cliente encontrada que o serviço de publicação na World Wide Web estiver desabilitado ou não instalado neste computador.

Instalação do Exchange 2007 exige que o computador que você está instalando o Microsoft Exchange para que o serviço de publicação na World Wide Web instalado e definido como algo diferente de desabilitado.

Para resolver esse problema, verifique se o serviço de publicação na World Wide Web é instalado e não está desabilitado no computador local e, em seguida, execute novamente a instalação do Microsoft Exchange.

Para verificar se o serviço de publicação na World Wide Web é instalado e não desabilitado

1.  Clique com o botão **Meu computador** na área de trabalho e, em seguida, clique em **Gerenciar**.

2.  Expanda o nó **serviços e aplicativos** e, em seguida, clique no nó de **Serviços**.

3.  No painel direito, localize o **Serviço de publicação na World Wide Web**.
    
    Se o **Serviço de publicação na World Wide Web** não é exibido na lista de serviços instalados, siga as etapas no procedimento abaixo para instalá-lo.

4.  Se o **Serviço de publicação na World Wide Web** é exibida, mas tem um status que não seja **iniciado**, continue com as etapas abaixo para iniciá-lo.

5.  Clique com o botão o **Serviço de publicação na World Wide Web** e, em seguida, clique em **Propriedades**.

6.  Verifique se o **Tipo de inicialização** é **automático** e o **status do serviço** está definido como **iniciado**.

7.  Clique em **Aplicar** e em **OK**.

Para instalar o serviço de publicação na World Wide Web

1.  No menu **Iniciar**, selecione **configurações**, **Painel de controle** e clique em **Adicionar ou remover programas**

2.  Clique em **Adicionar/remover componentes do Windows**.

3.  Na lista de **componentes**, marque a caixa de seleção **Servidor de aplicativos** e, em seguida, clique em **detalhes**.

4.  Selecione o **Gerenciador de serviços de informações da Internet** e, em seguida, clique em **detalhes**.

5.  Selecione **Serviço World Wide Web** e, em seguida, marque a caixa de seleção.

6.  Clique em **OK** duas vezes para retornar à lista de **componentes** e clique em **Avançar**.

7.  Clique em **Concluir** quando o serviço do IIS está instalado.

