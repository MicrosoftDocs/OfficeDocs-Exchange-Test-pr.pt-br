---
title: 'O protocolo de transporte de email simples está atualmente installed_SMTPSvcInstalled: Exchange 2013 Help'
TOCTitle: O protocolo de transporte de email simples está atualmente installed_SMTPSvcInstalled
ms:assetid: f786a93c-876d-4f4e-adb6-4dfea3d820d1
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/ms.exch.setupreadiness.smtpsvcinstalled(v=EXCHG.150)
ms:contentKeyID: 50487038
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# O protocolo de transporte de email simples está atualmente installed\_SMTPSvcInstalled

 

_**Aplica-se a:**Exchange Server_

_**Tópico modificado em:**2012-06-05_

O conteúdo neste tópico não foi atualizado para o Microsoft Exchange Server 2013. Mesmo assim, ele ainda pode se aplicar ao Exchange 2013. Se você ainda precisar de ajuda, verifique os recursos da comunidade, abaixo.

Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), ou [Proteção do Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=285351).

Instalação do Microsoft® Exchange Server 2007 não pode continuar porque o serviço do Microsoft Windows Server™ 2003 Simple Mail Transfer Protocol (SMTP) está instalado neste computador.

Instalação do Microsoft Exchange requer que o serviço SMTP não ser instalado nos servidores que são usados para o Exchange 2007.

Para resolver esse problema, desinstale o serviço SMTP e execute novamente o programa de instalação do Microsoft Exchange.

Desinstalar o serviço SMTP usando Adicionar ou remover um componente do Windows no painel de controle

1.  No menu **Iniciar**, clique em **Painel de controle**.

2.  Clique duas vezes em **Adicionar ou Remover Programas**.

3.  Clique em **Adicionar/remover componentes do Windows**.

4.  Na lista de **componentes**, marque a caixa de seleção **Servidor de aplicativos** e clique em **detalhes**.

5.  Selecione o **Gerenciador de serviços de informações da Internet** e, em seguida, clique em **detalhes**.

6.  Selecione o **Serviço SMTP** e, em seguida, clique para desmarcar a caixa de seleção.

7.  Clique em **OK** duas vezes para retornar à lista de **componentes** e clique em **Avançar**.

8.  Clique em **Concluir** quando o serviço SMTP é desinstalado.

