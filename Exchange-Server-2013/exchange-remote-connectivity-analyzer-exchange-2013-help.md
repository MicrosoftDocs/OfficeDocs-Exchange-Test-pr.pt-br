---
title: 'Analisador de Conectividade Remota do Exchange: Exchange 2013 Help'
TOCTitle: Analisador de Conectividade Remota do Exchange
ms:assetid: dd26698e-d00c-47f5-a7aa-c3894fe86c75
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Ff701693(v=EXCHG.150)
ms:contentKeyID: 50486787
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Analisador de Conectividade Remota do Exchange

 

_**Aplica-se a:**Exchange Server 2013_

_**Tópico modificado em:**2014-09-22_

O Analisador de Conectividade Remota (ExRCA) do MicrosoftExchange ajuda a garantir que a conectividade dos servidores do Exchange seja configurada corretamente. Se você tiver problemas, esse recurso também ajudará a localizar e corrigir esses problemas. O site do ExRCA pode executar testes para verificar o MicrosoftExchange ActiveSync, os Serviços Web do Exchange, o MicrosoftOutlook e a conectividade de email da Internet.

## Testes do Analisador de Conectividade Remota

Você pode realizar vários testes com o ExRCA. Os testes a seguir funcionam no Exchange 2007 e em versões posteriores:

  - Exchange ActiveSync

  - Serviços Web do Exchange

  - Outlook

  - Email de Internet

## Testes do Exchange ActiveSync

Você pode fazer os seguintes testes do Exchange ActiveSync:

  - **Exchange ActiveSync:** esse teste simula as etapas que um dispositivo móvel utiliza para se conectar ao servidor do Exchange usando o Exchange ActiveSync.

  - **Descoberta automática do Exchange ActiveSync:** esse teste realiza as etapas que um dispositivo do Exchange ActiveSync usa para obter configurações do serviço de Descoberta Automática.

## Testes de conectividade dos Serviços Web do Exchange

Os testes de serviços Web Exchange verificam as configurações para muitos dos Exchange serviços da Web. Você pode executar os seguintes testes do Exchange serviços Web:

  - **Sincronização, Notificação, Disponibilidade e Respostas Automáticas:** esses testes verificam muitas das tarefas básicas dos Serviços Web do Exchange para confirmar se estão funcionando. Isso é bastante útil para os administradores de TI que querem solucionar problemas de acesso externo usando o Entourage EWS ou outros clientes dos Serviços Web.

  - **Acesso à Conta de Serviço (Desenvolvedores):** esse teste verifica a capacidade de uma conta de serviço para acessar uma caixa de correio específica, criar e excluir itens dela e acessá-la via representação do Exchange. Esse teste é usado principalmente por desenvolvedores de aplicativos para testar a capacidade de acessar caixas de correio com credenciais alternativas.

## Testes de conectividade do Microsoft Office Outlook

Você pode fazer os seguintes testes de conectividade do Outlook:

  - **Outlook em Qualquer Lugar (RPC sobre HTTP):** esse teste acompanha as etapas utilizadas pelo Outlook para se conectar via Outlook em Qualquer Lugar (RPC sobre HTTP).

  - **Descoberta Automática do Outlook:** esse teste acompanha as etapas utilizadas pelo Outlook para obter as configurações do serviço de Descoberta Automática. Esse teste não se conecta de verdade a uma caixa de correio.

## Testes de email de Internet

Você pode fazer os seguintes testes de email da Internet:

  - **Email SMTP** **de Entrada:** esse teste acompanha as etapas utilizadas por um servidor de email da Internet para enviar email SMTP de entrada para o seu domínio.

  - **Email SMTP de Saída:** esse teste verifica seu endereço IP de saída para detectar certos requisitos. Isso inclui verificações de DNS Reverso, ID do Remetente e RBL.

  - **Email POP:** esse teste acompanha as etapas utilizadas por um cliente de email para se conectar a uma caixa de correio usando POP3.

  - **Email IMAP:** esse teste acompanha as etapas utilizadas por um cliente de email para se conectar a uma caixa de correio usando IMAP.

