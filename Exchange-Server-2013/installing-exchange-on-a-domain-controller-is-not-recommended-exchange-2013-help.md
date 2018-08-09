---
title: 'Instalar o Exchange em um controlador de domínio não é recomendado'
TOCTitle: Instalando o Exchange em um controlador de domínio não é recomendado
ms:assetid: 48922de2-a68c-4092-96a5-d38c8e5f49f5
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/ms.exch.setupreadiness.warninginstallexchangerolesondomaincontroller(v=EXCHG.150)
ms:contentKeyID: 50485475
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Instalando o Exchange em um controlador de domínio não é recomendado

 

_**Aplica-se a:** Exchange Server_

_**Tópico modificado em:** 2013-03-22_

A Configuração do Microsoft Exchange Server 2013 detectou que o computador em que você está tentando instalar o Exchange 2013 está em um controlador de domínio do Active Directory. Instalar o Exchange 2013 em um controlador de domínio não é recomendado.

Se você instalar o Exchange 2013 em um controlador de domínio, esteja atento para os seguintes problemas:

  - Configurar o Exchange 2013 para divisão de permissões do Active Directory não é suportado.

  - O grupo de segurança universal do Sub-sistema de Confiança do Exchange (USG) é adicionado ao grupo de Administradores de Domínio quando o Exchange é instalado em um controlador de domínio. Quando isso ocorre, todos os servidores Exchange no domínio recebem direitos de administrador para esse domínio.

  - Exchange Server e Active Directory são aplicativos que utilizam muitos recursos. Há implicações de desempenho a serem consideradas quando ambos estiverem sendo executados no mesmo computador.

  - Você deve se certificar de que o Exchange 2013 do controlador de domínio esteja instalado em um servidor de catálogo global.

  - Os serviços do Exchange podem não se iniciar corretamente quando o controlador de domínio também for um servidor de catálogo global.

  - O desligamento do sistema será consideravelmente mais longo se os serviços do Exchange não forem parados antes de se desligar ou reiniciar o servidor.

  - Rebaixar um controlador de domínio para um servidor membro não é suportado.

  - Não há suporte para a execução do Exchange 2013 em um nó de cluster que também seja um controlador de domínio do Active Directory.

Recomendamos que você instale o Exchange 2013 em um servidor membro.

Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), ou [Proteção do Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=285351).

Você encontrou o que você está procurando? Por favor, separe um minuto do seu tempo para [enviar seus comentários para nós](mailto:exsetuphelpfeedback@microsoft.com?subject=exchange%202013%20setup%20help%20feedback) sobre as informações que você estava esperando encontrar.

