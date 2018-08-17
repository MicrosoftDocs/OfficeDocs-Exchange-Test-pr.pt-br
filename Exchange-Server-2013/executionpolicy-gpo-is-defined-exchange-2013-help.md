---
title: 'O GPO ExecutionPolicy está definido: Exchange 2013 Help'
TOCTitle: O GPO ExecutionPolicy está definido
ms:assetid: 63de83e2-9a6b-4f57-85b9-df445bea18dd
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/ms.exch.setupreadiness.powershellexecutionpolicycheckset(v=EXCHG.150)
ms:contentKeyID: 61203504
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# O GPO ExecutionPolicy está definido

 

_**Aplica-se a:** Exchange Server_

_**Tópico modificado em:** 2016-12-15_

A Instalação do Microsoft Exchange Server 2013 não pode continuar porque detectou que o Objeto de Política de Grupo (GPO) **ExecutionPolicy** define uma ou ambas das seguintes políticas:

  - **MachinePolicy**

  - **UserPolicy**

Não importa como as políticas foram definidas. O importante é que elas foram definidas.

Quando você executa a Instalação do Exchange 2013, o Exchange para e desabilita o serviço Instrumentação de Gerenciamento do Windows (WMI). Quando uma dessas políticas for definida, será necessário ter o serviço WMI habilitado para a execução de um script do Windows PowerShell. Se as políticas estiverem definidas e se o serviço WMI estiver parado, a Instalação falhará e o servidor ficará em um estado inconsistente.

Para permitir que a Instalação continue, você precisa remover temporariamente qualquer definição de **MachinePolicy** ou de **UserPolicy** do GPO **ExecutionPolicy**.

Para obter informações sobre como remover qualquer definição de **MachinePolicy** ou de **UserPolicy** no **ExecutionPolicy** GPO, consulte o [artigo da Base de dados de Conhecimento KB981474](https://go.microsoft.com/fwlink/?linkid=3052&kbid=981474).


> [!NOTE]
> Mesmo que este artigo da Base de Dados de Conhecimento tenha sido escrito para o Exchange 2010, ele também se aplica às atualizações cumulativas e aos service packs do Exchange 2013.



Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), ou [Proteção do Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=285351).

Você encontrou o que você está procurando? Por favor, separe um minuto do seu tempo para [enviar seus comentários para nós](mailto:exsetuphelpfeedback@microsoft.com?subject=exchange%202013%20setup%20help%20feedback) sobre as informações que você estava esperando encontrar.

