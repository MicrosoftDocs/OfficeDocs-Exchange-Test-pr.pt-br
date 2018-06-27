---
title: 'Dispositivos móveis: Exchange 2013 Help'
TOCTitle: Dispositivos móveis
ms:assetid: 93a949e7-b3ef-43ea-ae0c-6698826fc8d2
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Bb232129(v=EXCHG.150)
ms:contentKeyID: 50486142
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Dispositivos móveis

 

_**Aplica-se a:**Exchange Server 2013_

_**Tópico modificado em:**2012-09-24_

Dispositivos móveis que estão habilitados paraExchange ActiveSync de Microsoft permitem que os usuários acessar a maioria dos seus dados de caixa de correio Microsoft Exchange a qualquer momento, em qualquer lugar. Há muitos diferentes celulares e dispositivos habilitados para Exchange ActiveSync. Eles incluem Windows telefones, Nokia celulares, telefones Android e tablets e o Apple iPhone, iPod e iPad.

Embora telefone e dispositivos móveis do telefone não suportam Exchange ActiveSync, na maioria dos documentação de Exchange ActiveSync, usamos o termo de *dispositivo móvel*. A menos que o recurso ou recursos estamos discutindo exigem um sinal de telefone celular, como notificação de mensagem SMS, o termo dispositivo móvel se aplica aos telefones móveis e outros dispositivos móveis, como tablets.

## Exchange ActiveSync

Exchange ActiveSync é um protocolo de comunicação que permite o acesso móvel, dinamicamente, como mensagens, dados de agendamento, contatos e tarefas de email. Exchange ActiveSync estão disponíveis em telefones Windows e telefones de terceiros que são habilitados para Exchange ActiveSync.

Exchange ActiveSync oferece a tecnologia Direct Push. O Direct Push usa uma conexão HTTPS criptografada que tenha estabelecido e mantido entre o dispositivo móvel e o servidor push novas mensagens de email e outros Exchange dados ao telefone.

Para usar o Direct Push com MicrosoftExchange Server 2013, os usuários devem ter um dispositivo móvel que tenha projetado para suportar o Direct Push.

## Recursos do Exchange ActiveSync

Exchange ActiveSync fornece acesso a diversos recursos que permitem que você aplicar políticas de segurança em dispositivos móveis. Usando Exchange 2013, você pode configurar várias políticas de caixa de correio de dispositivo móvel e controlar quais dispositivos móveis podem sincronizar com seu servidor Exchange. Exchange ActiveSync permite que você envie um comando de apagamento remoto do dispositivo que apaga todos os dados de um dispositivo móvel, caso esse dispositivo móvel for perdido ou roubado. Os usuários também podem iniciar um apagamento remoto de dispositivo de Outlook Web App.

Exchange ActiveSync permite que os usuários gerar uma senha de recuperação. Essa senha de recuperação é salvo no dispositivo móvel e é usada quando um usuário esquecer sua senha. O usuário gera a senha de recuperação ao mesmo tempo que eles geram o PIN ou a senha do dispositivo. Essa senha de recuperação pode ser usada para desbloquear o dispositivo móvel. Imediatamente após essa senha de recuperação for usada, o usuário precisará criar um novo PIN.

## POP3 e IMAP4

Se seu dispositivo móvel não é compatível com o Exchange ActiveSync ou o conjunto de recursos avançados que fornece o Exchange ActiveSync não é necessário, você pode usar o POP3 ou IMAP4 para acessar o email no seu dispositivo móvel. Para obter mais informações sobre o acesso à sua caixa de correio POP3 e IMAP4, consulte [POP3 e IMAP4 no Exchange Server 2013](pop3-and-imap4-in-exchange-server-2013-exchange-2013-help.md).

