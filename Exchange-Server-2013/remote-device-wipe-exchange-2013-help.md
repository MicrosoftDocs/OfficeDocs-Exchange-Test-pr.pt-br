---
title: 'Apagamento remoto de dispositivo: Exchange 2013 Help'
TOCTitle: Apagamento remoto de dispositivo
ms:assetid: cd615210-cd8a-48de-b3e3-8f9ec39ca380
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Bb124591(v=EXCHG.150)
ms:contentKeyID: 50486656
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Apagamento remoto de dispositivo

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2012-09-19_

Telefones celulares, tablets e outros dispositivos podem armazenar dados corporativos confidenciais e fornecer acesso a muitos recursos corporativos. Se um dispositivo móvel é perdido ou roubado, esses dados podem ser comprometidos. Por meio de políticas de caixa de correio do dispositivo móvel do Exchange Microsoft, você pode adicionar um requisito de senha nos seus dispositivos móveis. Isso requer que os usuários insiram uma senha para acessar seus dispositivos móveis. Recomendamos que, além de exigir uma senha de dispositivo, você configurar seus dispositivos móveis para solicitar uma senha automaticamente após um período de inatividade. A combinação de uma senha de dispositivo e o bloqueio de inatividade fornece segurança reforçada para seus dados corporativos.

Além desses recursos, Exchange Server 2013 fornece um recurso de apagamento remoto do dispositivo. Você pode emitir um comando de apagamento remoto do dispositivo de Exchange Management Shell ou o Centro de administração do Exchange (EAC). Os usuários podem emitir seu próprio dispositivo remoto apagamento comandos da interface do usuário MicrosoftOutlook Web App.

O recurso de apagamento remoto do dispositivo também inclui uma função de confirmação que grava um carimbo de hora nos dados de estado de sincronização da caixa de correio do usuário. Esse carimbo de data é exibido na Outlook Web App e na caixa de diálogo de propriedades por telefone celular do usuário no EAC.


> [!IMPORTANT]
> Apagamento remoto de dispositivo pode redefinir um telefone celular para a condição de padrão de fábrica. Embora o protocolo de apagamento remoto do dispositivo como implementada no Exchange 2013 requer apenas a exclusão de dados corporativos pessoais, todos os fabricantes de dispositivos móveis atual interpretam o comando como um que apaga todos os dados no telefone. Muitos sistemas operacionais de dispositivo móvel também apagar todos os dados em qualquer placa de armazenamento que está inserida no dispositivo móvel. Se você estiver executando um apagamento remoto de dispositivo em um telefone móvel em sua posse e deseja manter os dados no cartão de armazenamento, recomendamos a remoção da placa de armazenamento antes de você iniciar o apagamento remoto de dispositivo.




> [!WARNING]
> Após a ocorrência de apagamento remoto de dispositivo, a recuperação de dados é muito difícil. No entanto, nenhum processo de remoção de dados deixa um dispositivo móvel tão livre de dados residuais como quando ele é novo. Recuperação de dados de um dispositivo móvel ainda pode ser possível usando ferramentas sofisticadas.



## Apagamento remoto de dispositivo versus apagamento do dispositivo local

Apagamento do dispositivo local ocorre quando um dispositivo móvel se apaga sem que a solicitação provenientes do servidor. Se sua organização tiver implementado políticas de caixa de correio de dispositivo móvel que especificam um número máximo de tentativas malsucedidas de senha e esse máximo for excedido, o dispositivo móvel executa um apagamento do dispositivo local. O resultado de uma limpeza de dispositivo local é o mesmo de apagamento remoto de dispositivo. O dispositivo é retornado ao seu condição padrão de fábrica. Quando um dispositivo móvel realiza um apagamento do dispositivo local, nenhuma confirmação será enviada para o servidor Exchange.

