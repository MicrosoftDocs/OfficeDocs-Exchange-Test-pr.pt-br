---
title: 'Configurar Recursos do Cliente de Caixa Postal: Exchange 2013 Help'
TOCTitle: Configurar Recursos do Cliente de Caixa Postal
ms:assetid: 5e661cfd-d34e-4caa-91a5-967bbecb75eb
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/JJ673529(v=EXCHG.150)
ms:contentKeyID: 50556208
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configurar Recursos do Cliente de Caixa Postal

 

_**Aplica-se a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Tópico modificado em:** 2013-02-20_

Este tópico descreve os recursos do cliente que permitem que usuários habilitados para a Unificação de Mensagens (UM) do Exchange acessem o email e as mensagens de caixa postal em sua caixa de correio. Esses recursos permitem oferecer aos usuários acesso simplificado a email e caixa postal em uma experiência geral aprimorada para os usuários.

**Sumário**

Voice mail client support

Outlook Voice Access

Forwarding calls

Voice Mail Preview

Receiving faxes

## Suporte a cliente de caixa postal

**Clientes do Exchange ActiveSync**   O protocolo do Microsoft Exchange ActiveSync é usado para conectar clientes móveis, como os encontrados em dispositivos móveis com Internet, para uma caixa de correio do Exchange. Os usuários podem usar dispositivos móveis para acessar sua caixa de correio e exibir mensagens de email, exibir e alterar informações de calendário e contato e escutar suas mensagens de caixa postal. Eles podem também sincronizar email, caixa postal, itens de calendário e informações de contato com outros dispositivos.

**Integração com Outlook**   O Microsoft Outlook permite que os usuários acessem sua caixa postal do Exchange e vejam mensagens de email em sua Caixa de Entrada e escutem as mensagens de voz usando o Microsoft Windows Media Player, que está incorporado às mensagens de email. Utilizando um cliente de email suportado, os usuários ganham recursos adicionais, como a funcionalidade Tocar no Telefone.

**Integração com Outlook Web App**   O Microsoft Outlook Web App oferece aos usuários um conjunto de ferramentas e interfaces de UM que podem ser comparadas com um cliente de email com recursos completos, como o Outlook. Com o Outlook Web App, os usuários podem acessar suas caixas de correio do Exchange usando um navegador da Web compatível. Assim como o Outlook, o Outlook Web App fornece o Windows Media Player integrado em mensagens de email para que os usuários possam ouvir as mensagens de voz e permite que os usuários tenham acesso a outros recursos, como Tocar no Telefone.

## Outlook Voice Access

Na UM do Exchange, um usuário habilitado para UM pode fazer uma chamada para um número de telefone interno ou externo configurado para um plano de discagem da UM para acessar sua caixa de correio e usar o sistema de menu do Outlook Voice Access. Usando esse menu, os usuários habilitados para UM podem ler email, ouvir mensagens de voz, interagir com o calendário do Outlook, acessar seus contatos pessoais e executar tarefas como configurar o PIN do Outlook Voice Access ou gravar saudações para caixa postal. Para detalhes, consulte [Configurando o Outlook Voice Access](https://docs.microsoft.com/pt-br/exchange/voice-mail-unified-messaging/set-up-client-voice-mail-features/set-up-outlook-voice-access).

## Encaminhando chamadas

Um usuário habilitado para UM pode criar e configurar regras de atendimento de chamadas utilizando o Outlook ou o Outlook Web App. As regras de atendimento de chamadas permitem que os usuários controlem como as chamadas recebidas devem ser tratadas. As regras são aplicadas às chamadas recebidas de um modo parecido à forma como as regras de Caixa de Entrada são aplicadas a mensagens de email recebidas e são armazenadas junto com outras configurações de voz na caixa de correio do usuário. Até nove regras de atendimento de chamadas podem ser configuradas para cada caixa de correio habilitada para UM. Essas regras são independentes das regras de Caixa de Entrada e não utilizam parte da cota de armazenamento das regras de Caixa de Entrada do usuário. Para detalhes, consulte [Permitir usuários de email encaminhar chamadas de voz](https://docs.microsoft.com/pt-br/exchange/voice-mail-unified-messaging/set-up-client-voice-mail-features/allow-voice-mail-users-to-forward-calls).

## Visualização de Caixa Postal

Visualização da Caixa Postal é um recurso disponível a usuários que recebem suas mensagens de caixa postal do sistema de caixa postal de UM. Visualização da Caixa Postal aprimora a experiência de caixa postal, fornecendo uma versão em texto de gravações de áudio. Para obter detalhes, consulte [Permitir que os usuários vejam uma transcrição do correio de voz](allow-users-to-see-a-voice-mail-transcript-exchange-2013-help.md).

## Recebendo faxes

A UM encaminha chamadas de fax recebidas de um usuário habilitado para UM a uma solução parceira de fax dedicada, que estabelece a chamada de fax com o remetente e recebe o fax em nome do usuário. Para que os usuários habilitados para UM possam receber mensagens de fax em sua caixa de correio, você deve fazer o seguinte:

  - Habilitar o recebimento de faxes no plano de discagem de UM vinculado aos usuários definindo o parâmetro *FaxEnabled* como `$true`.

  - Habilitar o recebimento de faxes no plano de discagem de UM vinculado aos usuários definindo o parâmetro *Allowfax* como `$true`.

  - Habilitar o recebimento de faxes pelos usuários definindo o parâmetro *FaxEnabled* como `$true`.

  - Definir a URI do servidor de fax parceiro para permitir o recebimento de faxes.

  - Configurar a autenticação entre o servidor de Caixa de Correio e o servidor parceiro de fax.

