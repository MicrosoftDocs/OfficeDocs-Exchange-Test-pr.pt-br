---
title: 'Required_DomainPrepRequired de preparação do domínio: Exchange 2013 Help'
TOCTitle: Required_DomainPrepRequired de preparação do domínio
ms:assetid: f6feae6f-7404-4b1f-887f-ed63c26a6bcd
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/ms.exch.setupreadiness.domainpreprequired(v=EXCHG.150)
ms:contentKeyID: 50487035
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Required\_DomainPrepRequired de preparação do domínio

 

_**Aplica-se a:**Exchange Server_

_**Tópico modificado em:**2016-12-09_

O conteúdo neste tópico não foi atualizado para o Microsoft Exchange Server 2013. Mesmo assim, ele ainda pode se aplicar ao Exchange 2013. Se você ainda precisar de ajuda, verifique os recursos da comunidade, abaixo.

Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), ou [Proteção do Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=285351).

Instalação do Microsoft Exchange Server 2007 não pode continuar porque houve falha na tentativa de instalar a função de servidor.

A instalação do Microsoft Exchange requer que o domínio local ser preparado para o Exchange Server 2007 para que determinadas funções de servidor podem ser instaladas.

Preparação do domínio para o Exchange Server 2007 consiste das seguintes tarefas:

  - Configurando permissões no contêiner do domínio para os servidores do Exchange, administradores de organização do Exchange, os usuários autenticados e administradores de caixa de correio do Exchange.

  - Criando o contêiner objetos do sistema do Microsoft Exchange, se não existir e permissões de configuração deste contêiner para os servidores do Exchange, administradores de organização do Exchange e usuários autenticados.

  - Criar um novo grupo global de domínio no domínio atual chamado servidores de domínio de instalação do Exchange.

  - Adicionando o grupo de servidores de domínio de instalação do Exchange para o USG de servidores do Exchange no domínio raiz.

Para resolver esse problema, execute **setup /PrepareDomain** para preparar o domínio local e tente novamente o servidor de instalação da função.

Para obter mais informações sobre como executar o processo de PrepareDomain, consulte "Como para preparar e domínios do Active Directory" ([https://go.microsoft.com/fwlink/?LinkId=78453](https://go.microsoft.com/fwlink/?linkid=78453)).

