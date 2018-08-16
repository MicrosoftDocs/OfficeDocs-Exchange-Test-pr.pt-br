---
title: 'O computador local é um controlador de domínio de um domínio filho'
TOCTitle: O computador local é um controlador de domínio de um domain_LocalComputerIsDCInChildDomain filho
ms:assetid: 7db1dcc0-d953-41b8-b081-2a47a70950c4
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/ms.exch.setupreadiness.localcomputerisdcinchilddomain(v=EXCHG.150)
ms:contentKeyID: 50486022
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# O computador local é um controlador de domínio de um domain\_LocalComputerIsDCInChildDomain filho

 

_**Aplica-se a:** Exchange Server_

_**Tópico modificado em:** 2012-06-05_

O conteúdo neste tópico não foi atualizado para o Microsoft Exchange Server 2013. Mesmo assim, ele ainda pode se aplicar ao Exchange 2013. Se você ainda precisar de ajuda, verifique os recursos da comunidade, abaixo.

Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), ou [Proteção do Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=285351).

Instalação do Microsoft® Exchange Server 2007 não pode continuar porque o computador local é um controlador de domínio para um domínio filho.

Instalação do Exchange 2007 não será instalado em um controlador de domínio para um domínio filho, a menos que o controlador de domínio é um servidor de catálogo global.

Para resolver esse problema, promova o controlador de domínio para um servidor de catálogo global ou instalar o Exchange 2007 em um controlador de domínio não, um servidor membro, no domínio filho e, em seguida, execute novamente o programa de instalação do Microsoft Exchange.

Para corrigir esse aviso, tornando o Exchange server em um servidor de catálogo global

1.  No controlador de domínio, clique em **Iniciar**, aponte para **programas**, clique em **Ferramentas administrativas** e, em seguida, clique em **serviços e Sites do Active Directory**.

2.  Na árvore de console, clique duas vezes em **Sites**, duas vezes no nome do site e, em seguida, clique duas vezes em **servidores**.

3.  Clique duas vezes no controlador de domínio de destino.

4.  No painel de resultados, clique com o botão **Configurações NTDS** e, em seguida, clique em **Propriedades**.

5.  Na guia **Geral**, clique para marcar a caixa de seleção de **Catálogo Global**.

6.  Reinicie o controlador de domínio.

