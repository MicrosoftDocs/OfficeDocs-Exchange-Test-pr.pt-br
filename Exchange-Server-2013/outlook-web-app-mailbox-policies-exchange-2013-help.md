---
title: 'Diretivas de caixa de correio do Outlook Web App: Exchange 2013 Help'
TOCTitle: Diretivas de caixa de correio do Outlook Web App
ms:assetid: 213b8b7a-1c29-49ee-8c98-d0364ddf4f9d
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Dd335142(v=EXCHG.150)
ms:contentKeyID: 50485102
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Diretivas de caixa de correio do Outlook Web App

 

_**Aplica-se a:** Exchange Online, Exchange Server 2013_

_**Tópico modificado em:** 2012-10-05_

Use as diretivas de caixa de correio do MicrosoftOutlook Web App para criar políticas em nível de organização para gerenciar o acesso a recursos no Outlook Web App.

**Sumário**

Outlook Web App mailbox policies

Creating or deleting Outlook Web App mailbox policies

Configuring Outlook Web App mailbox policies

Applying Outlook Web App mailbox policies

## Diretivas de caixa de correio do Outlook Web App

No Exchange 2013, você pode criar várias diretivas de caixa de correio do Outlook Web App e aplicá-las a caixas de correio individuais. Quando uma diretiva de caixa de correio do Outlook Web App for aplicada a uma caixa de correio, as configurações do diretório virtual serão ignoradas.

Os recursos do Outlook Web App também podem ser gerenciados através da configuração de diretórios virtuais do Outlook Web App. As configurações de diretório virtual serão usadas para qualquer caixa de correio à qual uma política de caixa de correio não tenha sido aplicada.

## Criar ou excluir políticas de caixa de correio do Outlook Web App

Uma política padrão de caixa de correio do Outlook Web App é criada automaticamente quando o Exchange é instalado. Por padrão, todas as opções são habilitadas na diretiva de caixa de correio padrão do Outlook Web App. Você pode criar quantas diretivas de caixa de correio do Outlook Web App forem necessárias para atender às necessidades de sua organização.


> [!NOTE]
> A política padrão de caixa de correio do Outlook Web App não será automaticamente aplicada a qualquer caixa de correio.



Para obter informações sobre como criar e remover políticas de caixa de correio, consulte [Criar uma política de caixa de correio do Outlook Web App](create-an-outlook-web-app-mailbox-policy-exchange-2013-help.md) e [Remover uma política de caixa de correio do Outlook Web App do Exchange](remove-an-outlook-web-app-mailbox-policy-from-exchange-exchange-2013-help.md).

## Configurar diretivas de caixa de correio do Outlook Web App

A política padrão de caixa de correio do Outlook Web App tem todas as opções habilitadas por padrão. Para obter informações sobre como configurar políticas de caixa de correio do Outlook Web App, consulte [Exibir ou configurar as propriedades de diretiva de caixa de correio do Outlook Web App](view-or-configure-outlook-web-app-mailbox-policy-properties-exchange-2013-help.md).

## Aplicar políticas de caixa de correio do Outlook Web App

Apenas uma diretiva de caixa de correio do Outlook Web App pode ser aplicada a uma caixa de correio.

Se não houver nenhuma diretiva de caixa de correio do Outlook Web App aplicada a uma caixa de correio, as configurações definidas em um diretório virtual serão aplicadas.

Uma diretiva de caixa de correio do Outlook Web App pode ser aplicada a uma caixa de correio usando o EAC (Centro de Administração do Exchange) para modificar uma caixa de correio existente ou usando o Shell e o cmdlet [Set-CASMailbox](https://technet.microsoft.com/pt-br/library/bb125264\(v=exchg.150\)) para aplicar uma política de caixa de correio. Para mais informações, consulte [Aplicar ou remover uma diretiva de caixa de correio do Outlook Web App em uma caixa de correio](apply-or-remove-an-outlook-web-app-mailbox-policy-on-a-mailbox-exchange-2013-help.md).

