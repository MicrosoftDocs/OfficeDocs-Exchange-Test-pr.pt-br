---
title: 'Tocar no Telefone: Exchange 2013 Help'
TOCTitle: Tocar no Telefone
ms:assetid: 511e4950-340a-48cc-a020-35d11e76b993
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Dn205136(v=EXCHG.150)
ms:contentKeyID: 54651940
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Tocar no Telefone

 

_**Aplica-se a:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Tópico modificado em:**2013-04-25_

Depois que uma mensagem de voz chega, os usuários podem optar entre ouvir essa mensagem usando os alto-falantes ou os fones de ouvido do computador e ouvi-la usando o recurso Tocar no Telefone. O recurso Tocar no Telefone é incluído no Microsoft Outlook e o Outlook Web App, e as configurações de Tocar no Telefone estão disponíveis na seção **Tocar no telefone** em opções de **Correio de voz**. Este tópico discute como um usuário habilitado para UM pode usar o recurso Tocar no Telefone.

## O que é Tocar no Telefone?

O recurso Tocar no Telefone permite que usuários habilitados para UM reproduzam mensagens de voz pelo telefone. Se um usuário habilitado para UM ocupar uma baia no escritório, estiver usando um computador público ou um computador que não esteja habilitado para multimídia ou estiver ouvindo uma mensagem de voz confidencial, talvez ele não queira ou não possa ouvir uma mensagem de voz usando os alto-falantes do computador. Como alternativa, o usuário pode reproduzir a mensagem de voz usando qualquer telefone, incluindo telefones residenciais, comerciais ou celulares. Para revisar as configurações de Tocar no Telefone, no Outlook, vá para **Arquivo** \> **Informações** \> **Gerenciar caixa postal**. Se você clicar no botão **Gerenciar caixa postal** entrará automaticamente no Outlook Web App, ou você pode entrar no Outlook Web App usando um navegador da web. No Outlook Web App, vá para **Opções** \> **Telefone** \> **Correio de Voz** \> seção **Tocar no Telefone**, na página **Correio de Voz**.

Quando o usuário clica na opção da barra de ferramentas Tocar no Telefone, no formulário de mensagem de voz, a caixa de diálogo **Tocar no Telefone** aparece. A caixa **Tocar no Telefone** fornece os controles para a seleção ou inclusão do número de telefone a ser usado para tocar uma mensagem de voz, iniciar e encerrar a chamada, bem como uma mensagem de status para monitorar a chamada. Se o usuário está vinculado a um plano de discagem de URI do SIP, seu endereço SIP aparecerá na caixa **Discar**. Se o usuário está vinculado a um plano de discagem E.164, seu número E.164 completo aparecerá na caixa **Discar**.


> [!TIP]
> Apenas uma mensagem de voz pode ser tocada de cada vez. Se o usuário tentar iniciar uma segunda chamada Tocar no Telefone enquanto uma chamada anterior ainda estiver em andamento, será exibida uma mensagem de erro.



## Lista de números de telefone usados mais recentemente

Os usuários podem ver uma lista dos números de telefone que eles usaram mais recentemente na caixa **Discar**. O número de telefone especificado na seção **Tocar no Telefone** é sempre exibido como a entrada superior e é selecionado automaticamente para o usuário como o número principal. Os usuários podem usar o menu suspenso para selecionar outros números de telefone para discar, em vez do telefone configurado como o número principal.


> [!TIP]
> Para habilitar os usuários que estão usando o recurso Tocar no Telefone para discar um número de telefone externo sem um código de acesso a linha externa (por exemplo, 425-555-1234, em vez de 9-425-555-1234), configure regras de discagem para país/região em um plano de discagem do UM que incluam a seguinte linha: grupo1, 9xxxxxxxxxx, 91xxxxxxxxxx. Uma vez configuradas as regras de discagem para país/região, adicione essa lista à política de caixa de correio de UM.



## Botões de Tocar no Telefone

A caixa de diálogo **Tocar no Telefone** fornece aos usuários as opções **Discar** e **Desligar**. Quando a caixa de diálogo **Tocar no Telefone** for aberta pela primeira vez, o botão **Discar** estará habilitado e o botão **Desligar**, desabilitado. Depois que você fizer uma chamada, o botão **Discar** será desabilitado até o encerramento da chamada. Para encerrar a chamada, clique no botão **Desligar** ou desligue o telefone fisicamente. Fechar a caixa de diálogo **Tocar no Telefone** usando o botão **Fechar** encerra uma chamada, caso exista alguma em andamento. A opção **Tocar no Telefone** e outras opções também estão disponíveis na visualização **Painel de leitura** no Outlook. Se você abre a mensagem de correio de voz numa janela separada, o botão **Tocar no Telefone** está na barra de ferramentas.

## Seção Assunto, Enviado e Status

A seção inferior da caixa de diálogo **Tocar no Telefone** exibe o assunto da mensagem de voz, a data e a hora de envio e uma mensagem que exibe o estado atual da chamada. Todos os erros específicos da operação Tocar no Telefone são exibidos para o usuário nessa seção da caixa de diálogo **Tocar no Telefone**.

## Validação de número de telefone

O recurso Tocar no Telefone só executa validação simples em sua entrada na caixa de diálogo **Tocar no Telefone**. Tocar no Telefone não valida números de telefone. Se um número de telefone não for válido, a Unificação de Mensagens retornará um código de erro significativo para o usuário.

