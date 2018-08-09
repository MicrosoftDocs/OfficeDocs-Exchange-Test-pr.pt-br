---
title: 'Componentes de compatibilidade do IIS 6 não instalados: Exchange 2013 Help'
TOCTitle: Componentes de compatibilidade do IIS 6 não installed_LonghornIIS6MgmtConsoleNotInstalled
ms:assetid: 8358eafb-def7-4b8d-8fe1-623bc5a0e20e
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/ms.exch.setupreadiness.longhorniis6mgmtconsolenotinstalled(v=EXCHG.150)
ms:contentKeyID: 50486014
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Componentes de compatibilidade do IIS 6 não installed\_LonghornIIS6MgmtConsoleNotInstalled

 

_**Aplica-se a:** Exchange Server_

_**Tópico modificado em:** 2012-06-05_

O conteúdo neste tópico não foi atualizado para o Microsoft Exchange Server 2013. Mesmo assim, ele ainda pode se aplicar ao Exchange 2013. Se você ainda precisar de ajuda, verifique os recursos da comunidade, abaixo.

Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), ou [Proteção do Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=285351).

Microsoft®A instalação do Exchange Server 2007 não pode continuar ao tentar instalar a função de servidor acesso para cliente do servidor, a função de servidor de caixa de correio ou as ferramentas do Exchange 2007 administrativos nos seguintes sistemas operacionais Windows:

  - Windows Server 2008 R2

  - Windows Server 2008

  - Windows 7 (somente para ferramentas administrativas)

  - Windows Vista (somente para ferramentas administrativas)

Esse problema ocorre porque o componente de compatibilidade de Metabase do servidor de informações da Internet (IIS) 6 e o Console de gerenciamento do IIS 6 não estão instalados.

A instalação do Exchange 2007 requer que o computador em que você está instalando a função de servidor acesso para cliente do Exchange 2007, a função de servidor de caixa de correio ou as ferramentas do Exchange 2007 administrativos tem os componentes de compatibilidade de Metabase do IIS 6 e o Console de gerenciamento do IIS 6 instalada.

Para resolver esse problema, instale o componente de compatibilidade de Metabase do IIS 6 no computador de destino e, em seguida, execute novamente o programa de instalação do Microsoft Exchange.

Instalar os componentes de compatibilidade de gerenciamento do IIS 6.0 no Windows Server 2008 R2 ou no Windows Server usando a ferramenta Gerenciador de servidores

1.  Clique em **Iniciar**, clique em **Ferramentas Administrativas** e em **Gerenciador do Servidor**.

2.  No painel de navegação, expanda **funções**, clique com o botão **Servidor Web (IIS)** e clique em **Adicionar serviços de função**.

3.  No painel **Selecionar Serviços de função**, role para baixo até a **Compatibilidade com gerenciamento do IIS 6**.

4.  Clique para marcar as caixas de seleção de **Compatibilidade de Metabase do IIS 6**, **Compatibilidade com WMI do IIS 6** e **O Console de gerenciamento do IIS 6**.

5.  No painel **Selecionar Serviços de função**, clique em **Avançar**.

6.  No painel **Confirmar seleções**, clique em **instalar**.

7.  Clique em **Fechar** para sair do assistente Adicionar serviços de função.

Instalar os componentes de compatibilidade do IIS 6.0 de gerenciamento no Windows 7 ou no Windows Vista, no painel de controle

1.  Clique em **Iniciar**, clique em **Painel de controle**, clique em **programas e recursos** e clique em **Ativar recursos do Windows ativada ou desativada**.

2.  Abra o **Internet Information Services**.

3.  Abra as **Ferramentas de gerenciamento da Web**.

4.  Abra **a compatibilidade do IIS 6.0 de gerenciamento**.

5.  Clique para marcar as caixas de seleção do **Console de gerenciamento do IIS 6**, **Compatibilidade com WMI do IIS 6** e **compatibilidade de configuração do IIS 6 e Metabase do IIS 6**.

6.  Clique em **OK**.

