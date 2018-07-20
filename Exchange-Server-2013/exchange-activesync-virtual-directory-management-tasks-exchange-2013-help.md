---
title: 'Tarefas de gerenciamento de diretório virtual do Exchange ActiveSync: Exchange 2013 Help'
TOCTitle: Tarefas de gerenciamento de diretório virtual do Exchange ActiveSync
ms:assetid: f0b339b7-e184-4392-a133-20523183459d
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Bb125170(v=EXCHG.150)
ms:contentKeyID: 50486972
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Tarefas de gerenciamento de diretório virtual do Exchange ActiveSync

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2012-10-05_

Você pode gerenciar várias das configurações do aplicativo Exchange ActiveSync no Exchange Server 2013 através do diretório virtual do Exchange ActiveSync. Um diretório virtual é usado pelos serviços de informações da Internet (IIS) para permitir o acesso a um aplicativo web, como Exchange ActiveSync. Algumas das configurações do diretório virtual que você pode gerenciar para Exchange ActiveSync incluem relatórios, segurança e autenticação.

## Configurações do diretório virtual do Exchange ActiveSync

Você pode modificar as propriedades e configurações no diretório virtual Exchange ActiveSync a seguir:

  - **InternalURL** O InternalURL é a URL que os clientes internos podem usar para acessar o diretório virtual. Geralmente, é o formato https://servername/Microsoft-Server-ActiveSync. Por exemplo, se o nome NetBIOS do servidor for Sequoia, o InternalURL seria https://sequoia/Microsoft-Server-ActiveSync.

  - **ExternalURL** O ExternalURL é a URL que os clientes externos podem usar para acessar o diretório virtual. Essa URL deve ser acessível a partir de fora da rede interna. Por exemplo, seu ExternalURL poderia ser https://www.contoso.com/.

  - **Configurações de autenticação** Os dois métodos de autenticação que você pode configurar para o diretório virtual do Exchange ActiveSync são autenticação básica e autenticação de certificado de cliente.

