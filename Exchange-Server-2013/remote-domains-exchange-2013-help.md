---
title: 'Domínios remotos: Exchange 2013 Help'
TOCTitle: Domínios remotos
ms:assetid: 10fb7d62-4d78-40a3-82db-d62bcd27ba42
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Aa996309(v=EXCHG.150)
ms:contentKeyID: 50485038
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Domínios remotos

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2015-04-07_

Você pode criar entradas de domínio remoto para definir as configurações para transferência de mensagens entre a organização do Microsoft Exchange Server 2013 e os domínios fora de sua floresta do serviço de diretório do Exchange. Quando você cria uma entrada de domínio remoto, pode controlar os tipos de mensagens enviadas para esse domínio. Você pode também aplicar diretivas de formato de mensagens e conjuntos de caracteres aceitáveis a mensagens enviadas de usuários em sua organização para o domínio remoto. As configurações para domínios remotos são definições de configuração global para a organização do Exchange.

As configurações de domínio remoto são aplicadas a mensagens durante a categorização no serviço de Transporte, em servidores de Caixa de Correio. Quando a resolução do destinatário ocorre, é feita a correspondência do domínio do destinatário com os domínios remotos configurados. Se uma configuração do domínio remoto impedir que um determinado tipo de mensagem seja enviado aos destinatários desse domínio, a mensagem será excluída. Se você especificar um determinado formato de mensagem para o domínio remoto, o conteúdo e os cabeçalhos da mensagem serão modificados. As configurações se aplicam a todas as mensagens processadas pela organização do Exchange.


> [!NOTE]
> Se você configurar as definições da mensagem por usuário, as definições por usuário substituirão a configuração organizacional.



Por padrão, há uma entrada de domínio remoto única. O espaço de endereçamento do domínio é configurado como um asterisco (\*). Isso representa todos os domínios. Se você não criar entradas de domínio remoto adicionais, todas as mensagens enviadas para todos os destinatários em todos os domínios remotos terão as mesmas configurações aplicadas a elas.

Ao configurar os domínios remotos, você pode impedir que certos tipos de mensagens sejam enviados para esse domínio. Essas mensagens incluem mensagens de ausência temporária, mensagens de resposta automática, notificações de falha na entrega e notificações de encaminhamento de reunião. Se você possui um ambiente de várias florestas, pode desejar permitir o envio desses tipos de mensagens para esses domínios. Entretanto, se tiver identificado o domínio originário do spam, pode preferir bloquear o envio daqueles tipos de mensagens para esses domínios remotos.

**Conteúdo**

Message format

Automatic replies settings

Controlling NDR information

## Formato de mensagem

Você pode especificar o formato da mensagem e o conjunto de caracteres a ser usado em emails enviadao a domínios remotos. Essas configurações podem ser úteis para garantir que emails enviados pelos remetentes em seu domínio para o domínio remoto sejam compatíveis com o sistema de email do destinatário. Por exemplo, se você souber que o sistema de mensagens do domínio remoto é o Exchange, poderá especificar que a formatação Rich Text (RTF) do Exchange seja sempre usada. Para obter mais informações, consulte [Conversão de conteúdo](content-conversion-exchange-2013-help.md).

## Configurações de respostas automáticas

No Exchange 2013, os usuários podem especificar respostas automáticas diferentes para destinatários internos e externos. Mais do que isso, os tipos de respostas automáticas disponíveis na sua organização também dependem da versão do Microsoft Outlook em uso.

No Exchange 2013, existem dois tipos de respostas automáticas:

  - **Externa**   Suportada pelo Exchange 2013 e pelo Exchange 2010. Somente pode ser definida pelo Outlook 2010 ou pelo Office Outlook 2007 ou usando-se o Microsoft Office Outlook Web App.

  - **Interna**   Suportada pelo Exchange 2013 e pelo Exchange 2010. Somente pode ser definida pelo Outlook 2010 ou pelo Outlook 2007 ou usando-se o Outlook Web App.

A tabela a seguir descreve várias combinações de cliente e servidor e os tipos de respostas automáticas que podem ser usadas em cada cenário.

**Suporte a cliente e servidor para respostas automáticas**


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Versão do Cliente</th>
<th>Versão do Exchange</th>
<th>Respostas automáticas com suporte</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Outlook 2010 ou Outlook 2007</p></td>
<td><p>Exchange 2013 Exchange 2010 Exchange 2007</p></td>
<td><p>Interna, Externa</p></td>
</tr>
<tr class="even">
<td><p>Outlook Web App</p></td>
<td><p>Exchange 2013 Exchange 2010 Exchange 2007</p></td>
<td><p>Interna, Externa</p></td>
</tr>
</tbody>
</table>


## Controlarinformações de NRD

Conforme mencionado no início deste tópico, é possível impedir que notificações de falha na entrega sejam enviadas para um domínio remoto. Ao bloquear o envio de NDRs para um domínio remoto, você pode impedir que as informações contidas na NDR deixem sua organização, limitando o conhecimento que um usuário mal intencionado possa obter sobre sua organização. No entanto, isso também impede que remetentes legítimos recebam notificações de falha na entrega, causando confusão e perda de produtividade.

O Exchange 2013 oferece um controle mais minucioso sobre o conteúdo de uma notificação de falha na entrega destinada a um domínio remoto. Com o Exchange 2013, você pode permitir NDRs para domínios remotos, ao mesmo tempo em que remove informações de diagnóstico. Dessa maneira você pode impedir que informações sobre sua implantação do Exchange deixem sua organização sem deixar de oferecer notificações de falha na entrega aos remetentes externos.

Esse recurso é controlado com o novo parâmetro *NDRDiagnosticInfoEnabled* do cmdlet **Set-RemoteDomain**. Como essa definição é configurável para cada domínio remoto, você pode ter definições diferentes de acordo com suas necessidades. Você pode, por exemplo, optar por remover as informações de diagnóstico da notificação de falha na entrega para o domínio remoto padrão, mas permitir informações completas de diagnóstico na notificação para os domínios remotos que representem seus parceiros.

Para mais informações sobre essa nova configuração, consulte [Set-RemoteDomain](https://technet.microsoft.com/pt-br/library/aa997857\(v=exchg.150\)).

