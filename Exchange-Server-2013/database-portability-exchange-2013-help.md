---
title: 'Portabilidade do banco de dados: Exchange 2013 Help'
TOCTitle: Portabilidade do banco de dados
ms:assetid: 387b727a-ce51-4910-b5c4-613c693fa5bd
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Dd876873(v=EXCHG.150)
ms:contentKeyID: 51407851
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Portabilidade do banco de dados

 

_**Aplica-se a:**Exchange Server 2013_

_**Tópico modificado em:**2017-01-30_

A portabilidade de banco de dados é um recurso que permite que um banco de dados de caixas de correio do Microsoft Exchange Server 2013 possa ser movido ou montado em qualquer outro servidor de Caixas de Correio na mesma organização que esteja executando o Exchange 2013 com bancos de dados de mesma versão de esquema de banco de dados. Os bancos de dados de caixas de correio de versões anteriores do Exchange não podem ser movidos para um servidor de caixas de correio que esteja executando o Exchange 2013. Usando a portabilidade de banco de dados, a confiabilidade é aprimorada pela remoção de diversas etapas manuais suscetíveis a erros dos processos de recuperação. Além disso, essa portabilidade reduz os tempos de recuperação gerais de vários cenários de falha.

Ao usar a portabilidade do banco de dados para recuperar um banco de dados de caixa de correio, a versão do sistema operacional e a versão do Exchange Server nos servidores do Exchange de origem e destino devem ser o mesmo. Por exemplo, se uma banco de dados de caixa de correio do Exchange 2013 foi montado anteriormente em um servidor executando o Windows Server 2012, portabilidade do banco de dados só funcionará quando for migrar o banco de dados para um servidor executando o Windows Server 2012 e o Exchange 2013 também.

Para obter informações sobre como executar uma recuperação de banco de dados com o recurso de portabilidade do banco de dados, consulte [Mover um banco de dados de caixa de correio usando a portabilidade de banco de dados](move-a-mailbox-database-using-database-portability-exchange-2013-help.md).

