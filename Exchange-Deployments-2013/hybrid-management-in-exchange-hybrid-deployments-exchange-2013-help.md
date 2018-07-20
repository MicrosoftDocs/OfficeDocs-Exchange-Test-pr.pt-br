﻿---
title: 'Gerenciamento híbrido em implantações híbridas do Exchange: Exchange 2013 Help'
TOCTitle: Gerenciamento híbrido em implantações híbridas do Exchange
ms:assetid: 233f9f34-3ff5-47e1-a9e8-3244ee868d6e
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/JJ659048(v=EXCHG.150)
ms:contentKeyID: 50487107
ms.date: 01/10/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Gerenciamento híbrido em implantações híbridas do Exchange

 

_<strong>Aplica-se a:</strong>Exchange Server 2013, Exchange Server 2016_

_<strong>Tópico modificado em:</strong>2016-12-09_

Ao instalar um servidor Exchange, as ferramentas de gerenciamento do Exchange são automaticamente instaladas no servidor. Você usará as seguintes ferramentas para configurar e gerenciar as organizações local do Exchange e do Exchange Online:

  - **Centro de administração do Exchange**   O EAC é um console de gerenciamento baseado na web que permite a facilidade de uso e é ideal para implantações locais, online, ou híbridas do Exchange. O EAC substitui o EMC (Console de Gerenciamento do Exchange) e o ECP (Painel de Controle do Exchange), que eram as interfaces usadas para gerenciar o Exchange Server 2010.

  - **Shell de Gerenciamento do Exchange**   O Shell de Gerenciamento do Exchange é uma interface de linha de comando baseada no Windows PowerShell.

## O centro de administração do Exchange

O EAC permite que você realize diversas tarefas de implantação e tarefas administrativas mais comuns no dia a dia em servidores locais do Exchange e na organização do Exchange Online. Ele é instalado por padrão em cada servidor Exchange 2013 ou mais recente. Além disso, como é um console de gerenciamento com base na Web, você também pode acessá-lo usando um navegador da Web em outros computadores em sua rede ou pela Internet usando a URL de diretório virtual do ECP.

É possível acessar a organização do Exchange Online no EAC selecionando a guia de navegação entre locais do Office 365. A navegação entre locais permite que você alterne facilmente entre suas organizações do Exchange Online e suas organizações locais do Exchange. Se você configurou uma implantação híbrida, selecionar a guia do Office 365 permite que você gerencie a organização do Exchange Online e objetos de destinatário. Se você não possui uma organização do Exchange Online, selecionar o link do Office 365 o levará diretamente para a página de inscrição do Office 365.

Para saber mais sobre o EAC, consulte [Centro de administração do Exchange no Exchange 2013](https://technet.microsoft.com/pt-br/library/jj150562\(v=exchg.150\)).

## O Shell de Gerenciamento do Exchange

O Shell de Gerenciamento do Exchange permite a execução de qualquer tarefa realizada pelo EAC, bem como de algumas tarefas adicionais executáveis apenas no Shell de Gerenciamento do Exchange. O Shell de Gerenciamento do Exchange é uma coleção de scripts e cmdlets do Windows PowerShell que são instalados no computador quando as ferramentas de gerenciamento do Exchange são instaladas. Esses scripts e cmdlets são carregados apenas na abertura do Shell de Gerenciamento do Exchange usando o ícone do Shell de Gerenciamento do Exchange. Se o Windows PowerShell for aberto diretamente, os scripts e cmdlets do Exchange não serão carregados e não poderão gerenciar a organização local.


> [!TIP]
> É possível criar uma conexão manual do Windows PowerShell com a organização local, semelhante à forma como você se conecta manualmente à organização do Exchange Online abaixo. Contudo, recomendamos fortemente o uso do ícone do Shell de Gerenciamento do Exchange para abrir o Shell de Gerenciamento do Exchange e gerenciar os servidores do Exchange locais.



Quando você abre o Shell de Gerenciamento do Exchange usando o ícone do Shell de Gerenciamento do Exchange em um computador com as ferramentas de gerenciamento instaladas, é possível gerenciar a organização local. Contudo, não é possível gerenciar a organização do Exchange Online se o Shell de Gerenciamento do Exchange for aberto usando esse ícone. O motivo disso é que, ao abrir o Shell de Gerenciamento do Exchange usando o ícone do Shell de Gerenciamento do Exchange, é estabelecida uma conexão automática com o servidor local do Exchange.

Se você deseja gerenciar a organização do Exchange Online usando o Windows PowerShell, será necessário abrir o Windows PowerShell diretamente, e não via ícone do Shell de Gerenciamento do Exchange. Ao abrir o Windows PowerShell, é possível especificar manualmente onde você deseja se conectar. Ao criar uma conexão manual, você especifica uma conta de administrador na organização locatária do Office 365 e depois executa um comando para criar uma conexão. Ao estabelecer a conexão, os cmdlets do Exchange autorizados para execução estarão disponíveis. Saiba mais em [Uso do Windows PowerShell](http://go.microsoft.com/fwlink/p/?linkid=209660).

Caso não esteja familiarizado com o Shell de Gerenciamento do Exchange e deseje conhecer os princípios básicos de funcionamento do Shell de Gerenciamento do Exchange, sintaxes de comando e muito mais, consulte [Usando o PowerShell com o Exchange 2013 (Shell de gerenciamento do Exchange)](https://technet.microsoft.com/pt-br/library/bb123778\(v=exchg.150\)).

