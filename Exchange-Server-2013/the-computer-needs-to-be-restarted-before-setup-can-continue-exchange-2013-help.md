---
title: 'O computador deve ser reiniciado antes que a Configuração possa continuar: Exchange 2013 Help'
TOCTitle: O computador deve ser reiniciado antes que a Configuração possa continuar
ms:assetid: d5c73280-4e54-473a-b328-9673af11e2c0
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/ms.exch.setupreadiness.rebootpending(v=EXCHG.150)
ms:contentKeyID: 50486735
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# O computador deve ser reiniciado antes que a Configuração possa continuar

 

_**Aplica-se a:**Exchange Server_

_**Tópico modificado em:**2016-12-09_

Microsoft Exchange Server 2013 a instalação não pode continuar porque detectou que o computador local que precisa ser reiniciado para concluir a instalação de outros programas ou atualizações do Windows.

## Por que isso está acontecendo?

Quando programas e atualizações do Windows são instalados, eles fazem alterações nos arquivos que são armazenados em seu computador. Às vezes, durante a instalação, um programa ou atualização do Windows precisa fazer uma alteração em um arquivo que está sendo usado. Quando isso acontece, você precisa reiniciar o computador antes que outros programas, como o Exchange 2013, possam ser instalados. A Configuração do Exchange exige que todas as outras instalações estejam concluídas para poder verificar se todos os pré-requisitos necessários para funcionar corretamente foram instalados.

Às vezes, a instalação de um programa anterior ou uma atualização do Windows pode não ser concluída com êxito. Quando isso acontece, alterações que fazem o Windows e outros programas pensar que é necessário reiniciar podem ser deixadas para trás. Infelizmente, como a instalação que falha nunca limpa essas alterações, a instalação de atualizações do Windows e outros programas pode ser bloqueada. Se isso acontecer, você continuará a ver esse erro toda vez que executar a Configuração do Exchange.

## Como faço para corrigi-lo?

Na maioria dos casos, você só precisa reiniciar o computador para se livrar desse erro. No entanto, há momentos em que você poderá receber esse erro novamente mesmo que já tenha reiniciado o computador. Isso pode acontecer quando a instalação de um programa ou atualização do Windows precisar fazer outras alterações e essas alterações também exigirem que o computador seja reiniciado. Se você vir esse erro após reiniciar o computador, tente reiniciá-lo novamente.

Se você reiniciar o computador mais de duas ou três vezes e ainda vir esse erro, tente reinstalar todos os programas ou atualizações do Windows que você instalou recentemente. Isso pode permitir que uma instalação que falhou seja concluída com êxito.

Se, depois de reiniciar seu computador e reinstalar todos os programas recentes ou Windows atualizações, você *ainda* receber esse erro, é recomendável que você entre em contato com suporte da Microsoft. Eles vai ajudá-lo a encontrar a razão por que Windows e outros programas pensa que seu computador precisa ser reiniciado. Para contatar o suporte da Microsoft, vá para o [suporte para o Microsoft Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=525940).


> [!WARNING]
> Embora pareça tentador, é altamente recomendável que você não tente resolver esse problema excluindo ou alterando manualmente as chaves ou valores no Registro do Windows. Essa ação pode corrigir esse problema momentaneamente, mas pode provocar problemas no futuro. Isso é especialmente importante se a instalação que falhou tiver sido uma Atualização do Windows.


