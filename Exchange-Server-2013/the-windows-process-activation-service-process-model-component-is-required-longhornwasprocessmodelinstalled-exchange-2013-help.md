---
title: 'O serviço de ativação de processos do Windows - o componente de modelo de processo é required_LonghornWASProcessModelInstalled: Exchange 2013 Help'
TOCTitle: O serviço de ativação de processos do Windows - o componente de modelo de processo é required_LonghornWASProcessModelInstalled
ms:assetid: 8cc13dbb-4921-4c07-8602-d26613d7730a
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/ms.exch.setupreadiness.longhornwasprocessmodelinstalled(v=EXCHG.150)
ms:contentKeyID: 50486084
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# O serviço de ativação de processos do Windows - o componente de modelo de processo é required\_LonghornWASProcessModelInstalled

 

_**Aplica-se a:**Exchange Server_

_**Tópico modificado em:**2015-04-07_

O conteúdo neste tópico não foi atualizado para o Microsoft Exchange Server 2013. Mesmo assim, ele ainda pode se aplicar ao Exchange 2013. Se você ainda precisar de ajuda, verifique os recursos da comunidade, abaixo.

Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), ou [Proteção do Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=285351).

instalação Exchange Server 2010 não pode continuar a instalação no Windows Server 2008-computador Windows Server 2008 R2 ou porque o serviço de ativação de processos do Windows - o recurso de modelo de processo não está instalado no servidor.

O serviço de ativação de processos do Windows generaliza o modelo de processo do Internet Information Services (IIS), removendo a dependência no HTTP. Todos os recursos do IIS que estavam anteriormente disponível apenas a aplicativos HTTP agora estão disponíveis para aplicativos que hospedam os serviços do Windows Communication Foundation (WCF), usando protocolos não HTTP. O IIS 7.0 também usa o serviço de ativação de processos do Windows para ativação baseada em mensagem sobre HTTP.

O modelo de processo hospeda serviços Web e WCF. Introduzido no IIS 6.0, o modelo de processo é uma nova arquitetura que recursos proteção rápida contra falha, monitoramento da integridade e reciclagem.

Para resolver esse problema, instale o serviço de ativação de processos do Windows - recurso de modelo de processo nesse servidor e, em seguida, execute novamente a instalação do Exchange 2010.

Instalar o serviço de ativação de processos do Windows - recurso de modelo de processo usando a ferramenta Gerenciador de servidores

1.  Clique em **Iniciar**, clique em **Ferramentas administrativas** e em seguida **Gerenciador de servidores**.

2.  No painel de navegação esquerdo, clique com o botão **recursos** e, em seguida, clique em **Adicionar recursos**.

3.  No painel **Selecionar recursos**, role para baixo até o **Serviço de ativação de processos do Windows**.

4.  Marque as caixas de seleção de **Modelo de processo**.

5.  Clique em **Avançar**, no painel **Selecionar recursos** e clique em **instalar**, no painel **Confirmar seleções de instalações**.

6.  Clique em **Fechar** para sair do assistente Adicionar serviços de função.

