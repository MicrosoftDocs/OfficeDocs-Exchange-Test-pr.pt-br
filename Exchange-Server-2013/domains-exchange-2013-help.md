---
title: 'Domínios: Exchange 2013 Help'
TOCTitle: Domínios
ms:assetid: 11748c2d-2e32-43a4-b77d-e0c17db6200b
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/JJ673041(v=EXCHG.150)
ms:contentKeyID: 50485044
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Domínios

 

_**Aplica-se a:**Exchange Server 2013, Office 365_

_**Tópico modificado em:**2012-10-11_

Os domínios representam namespaces SMTP para os quais os diretórios de email e caixas de correio são configurados. Ao configurar os domínios que interagem com a sua organização do Microsoft Exchange Server 2013, você pode configurar como os emails enviados e recebidos por diversos domínios são processados pelo Exchange.

## Domínios aceitos

Um domínio aceito é qualquer namespace SMTP no qual sua organização do Exchange envia ou recebe emails. Domínios aceitos incluem aqueles domínios nos quais a organização do Exchange é autoritativa, assim como domínios de retransmissão interna e externa. Uma organização do Exchange é autoritativa quando controla a entrega de mensagens para destinatários no domínio aceito. Domínios aceitos também incluem domínios nos quais a organização do Exchange recebe emails e, em seguida, os retransmite para um servidor de email fora da organização.

Para obter mais informações sobre domínios aceitos, consulte [Domínios aceitos](accepted-domains-exchange-2013-help.md).

## Domínios remotos

No Exchange 2013, você cria entradas de domínios remotos para definir as configurações de transferência de mensagens entre sua organização do Exchange e domínios fora da sua organização. Quando você cria uma entrada de domínio remoto, pode controlar os tipos de mensagens enviadas para esse domínio. Você pode também aplicar diretivas de formato de mensagens e conjuntos de caracteres aceitáveis a mensagens enviadas de usuários em sua organização para o domínio remoto.

As configurações para domínios remotos são definições de configuração global para sua organização do Exchange. As configurações de domínio remoto são aplicadas às mensagens durante a categorização. Quando a resolução do destinatário ocorre, é feita a correspondência do domínio do destinatário com os domínios remotos configurados. Se uma configuração do domínio remoto impedir que um determinado tipo de mensagem seja enviado aos destinatários desse domínio, a mensagem será excluída. Se você especificar um determinado formato de mensagem para o domínio remoto, o conteúdo e os cabeçalhos da mensagem serão modificados. As configurações se aplicam a todas as mensagens processadas pela organização do Exchange.

Para obter mais informações sobre domínios remotos, consulte [Domínios remotos](remote-domains-exchange-2013-help.md).

