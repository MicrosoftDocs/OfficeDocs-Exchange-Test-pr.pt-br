---
title: 'Componente de extensibilidade do .NET IIS 7 é required_LonghornIIS7NetExt: Exchange 2013 Help'
TOCTitle: Componente de extensibilidade do .NET IIS 7 é required_LonghornIIS7NetExt
ms:assetid: 8b481626-b68a-4fba-b66e-a02c03856bfd
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/ms.exch.setupreadiness.longhorniis7netext(v=EXCHG.150)
ms:contentKeyID: 50486115
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Componente de extensibilidade do .NET IIS 7 é required\_LonghornIIS7NetExt

 

_**Aplica-se a:** Exchange Server_

_**Tópico modificado em:** 2012-06-05_

O conteúdo neste tópico não foi atualizado para o Microsoft Exchange Server 2013. Mesmo assim, ele ainda pode se aplicar ao Exchange 2013. Se você ainda precisar de ajuda, verifique os recursos da comunidade, abaixo.

Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), ou [Proteção do Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=285351).

Microsoft®A instalação do Exchange Server 2010 não pode continuar porque o componente de extensibilidade do .NET do servidor de informações da Internet (IIS) 7 necessário não está instalado no servidor de destino.

Para que Exchange 2010 possa usar o Windows PowerShell remoto, o componente de extensibilidade do .NET IIS 7 deve ser instalado no servidor de destino.

Para resolver esse erro, use o Gerenciador de servidores para instalar o componente de extensibilidade do .NET IIS 7 neste servidor e, em seguida, execute novamente a instalação do Exchange 2010.

Instalar o componente de extensibilidade do .NET IIS 7 no Windows Server 2008 ou no Windows Server 2008 R2, usando a ferramenta Gerenciador de servidores

1.  Clique em **Iniciar**, clique em **Ferramentas administrativas** e em seguida **Gerenciador de servidores**.

2.  No painel de navegação esquerdo, expanda **Funções**, clique com o botão direito do mouse em **Servidor Web (IIS)** e selecione **Adicionar Serviços de Função**.

3.  No painel **Selecionar Serviços de função**, role para baixo até o **Desenvolvimento de aplicativos**.

4.  Marque a caixa de seleção em **Extensibilidade do .NET**.

5.  Clique em **Avançar**, no painel **Selecionar Serviços de função** e clique em **instalar**, no painel **Confirmar seleções de instalações**.

6.  Clique em **Fechar** para sair do assistente Adicionar serviços de função.

