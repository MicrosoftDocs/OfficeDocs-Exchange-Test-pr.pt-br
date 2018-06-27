---
title: 'políticas de caixa de correio de UM: Exchange 2013 Help'
TOCTitle: políticas de caixa de correio de UM
ms:assetid: dfae629e-ee89-4494-a3ed-9655b67eb87e
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Bb124909(v=EXCHG.150)
ms:contentKeyID: 50556300
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# políticas de caixa de correio de UM

 

_**Aplica-se a:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Tópico modificado em:**2012-11-15_

Políticas de caixa de correio Unificação de mensagens (UM) são necessárias quando você habilita usuários para Unificação de mensagens. Criar políticas de caixa de correio de Unificação de mensagens para aplicar um conjunto comum de políticas ou configurações de segurança para um conjunto de caixas de correio dos usuários do correio de voz. UM políticas de caixa de correio são usadas para especificar configurações de Unificação de mensagens, como o seguinte:

  - Diretivas de PIN

  - Restrições de discagem

  - Outras propriedades de política de caixa de correio de Unificação de mensagens gerais

Por exemplo, você pode criar uma política de caixa de correio de Unificação de mensagens para aumentar o nível de segurança PIN, reduzindo o número máximo de falhas de entrada para um grupo específico de usuários habilitados para UM, como executivos.

## políticas de caixa de correio de UM

Pelo menos uma diretiva de caixa de correio de Unificação de mensagens deve ter sido criada antes de poder habilitar usuários para Unificação de mensagens. Você pode criar diretivas de caixa de correio de Unificação de mensagens adicionais para aplicar um conjunto comum de configurações de grupos de usuários.

Você pode criar políticas de caixa de correio de Unificação de mensagens usando o Shell de gerenciamento do Exchange ou o Centro de administração do Exchange (EAC). Por padrão, uma única política de caixa de correio de Unificação de mensagens é criada sempre que você criar um plano de discagem de UM. A nova diretiva de caixa de correio de Unificação de mensagens é automaticamente associada a UM plano de discagem e parte do nome do plano de discagem está incluído no nome de exibição da diretiva de caixa de correio de Unificação de mensagens. Você pode editar essa diretiva de caixa de correio de Unificação de mensagens padrão.

Vários usuários habilitados para UM podem ser vinculados a uma única política de caixa de correio de Unificação de mensagens. No entanto, a caixa de correio para cada usuário habilitado deve ser vinculada a uma única política de caixa de correio de Unificação de mensagens. Esse recurso permite controlar as configurações de segurança PIN, como o número mínimo de dígitos de um PIN ou o número máximo de tentativas de entrada para os usuários habilitados para Unificação de mensagens que estão associados a diretiva de caixa de correio de Unificação de mensagens. Você também pode controlar configurações de mensagem de texto ou restrições de discagem para as caixas de correio mesmas habilitado.

