---
title: 'Desinstalar os Pacotes de Idioma da Unificação de Mensagens'
TOCTitle: Desinstalar o Unified Messaging Packs_AdditionalUMLangPackExists de idioma
ms:assetid: 3a7e2621-0553-44f5-8029-c72fea25af3c
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/ms.exch.setupreadiness.additionalumlangpackexists(v=EXCHG.150)
ms:contentKeyID: 50485396
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Desinstalar o Unified Messaging Packs\_AdditionalUMLangPackExists de idioma

 

_**Aplica-se a:** Exchange Server_

_**Tópico modificado em:** 2016-12-09_

O conteúdo neste tópico não foi atualizado para o Microsoft Exchange Server 2013. Mesmo assim, ele ainda pode se aplicar ao Exchange 2013. Se você ainda precisar de ajuda, verifique os recursos da comunidade, abaixo.

Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), ou [Proteção do Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=285351).

Instalação do Microsoft Exchange Server 2007 não pode continuar porque houve falha na atualização a função de servidor Unificação de mensagens.

Configuração do Exchange requer que todos os Unified Messaging server role pacotes de idioma, exceto o pacote de idioma inglês dos EUA, ser desinstalados antes de continuar a atualização de função de servidor Unificação de mensagens.

Pacotes de idiomas de mensagens (UM) unificada que estão incluídos com o Exchange 2007 contêm pré-gravado prompts, suporte à conversão de texto em fala (TTS) para um determinado idioma.

Pacotes de idiomas de Unificação de MENSAGENS do Exchange 2007 permitem que os chamadores e usuários do Outlook Voice Access interagir com o sistema de Unificação de mensagens em vários idiomas.

Os pacotes de idiomas não - inglês dos EUA existente precisam ser desinstalada para que podem ser instalados novos pacotes de idiomas.

Para resolver esse problema, desinstale todos Unificação de mensagens server role pacotes de idiomas, exceto o pacote de idioma inglês dos EUA e, em seguida, execute novamente a instalação do Exchange 2007.

Para obter mais informações sobre como desinstalar os pacotes de idiomas de função de servidor Unificação de mensagens, consulte [como remover um Unified Messaging pacote de idiomas de um servidor de Unificação de mensagens](https://go.microsoft.com/fwlink/?linkid=85973) na documentação do produto Exchange 2007.

