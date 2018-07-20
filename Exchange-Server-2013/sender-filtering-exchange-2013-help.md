---
title: 'Filtragem por remetente: Exchange 2013 Help'
TOCTitle: Filtragem por remetente
ms:assetid: b833f864-ff10-46a0-a653-28fb9ba30896
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Bb124354(v=EXCHG.150)
ms:contentKeyID: 50486470
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Filtragem por remetente

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2012-10-12_

Filtragem de remetente se baseia em MAIL FROM: cabeçalho SMTP para determinar qual ação, se houver, para receber uma mensagem de email de entrada. Filtragem de remetente é fornecido pelo agente de filtro de remetente.

O agente de filtro de remetente funciona em mensagens de remetentes específicos fora da organização. Os administradores manter uma lista de remetentes que são bloqueados e enviar mensagens para a organização. Como administrador, você pode bloquear remetentes único (por exemplo, kim@contoso.com), toda a domínios (contoso.com), ou domínios e todos os subdomínios (\*. contoso.com). Você também pode configurar a ação que o agente do filtro de remetente deve ser tomadas quando uma mensagem que tenha um remetente bloqueado é encontrada. Você pode configurar as seguintes ações:

  - O agente Filtro de remetente rejeita a solicitação de SMTP com um erro de sessão SMTP `554 5.1.0 Sender Denied` e fecha a conexão.

  - O agente Filtro de remetente aceita a mensagem e atualiza a mensagem para indicar que a mensagem foi enviada de um remetente bloqueado. Porque a mensagem foi enviada de um remetente bloqueado e está marcado como tal, o agente Filtro de conteúdo usará essas informações ao calcular o nível de confiança de spam (SCL).

Você pode designar remetentes bloqueados e define como o agente do filtro de remetente deve agir em mensagens de remetentes bloqueados. Para obter mais informações sobre como configurar o agente Filtro de remetente, consulte [Gerenciar filtragem de remetente](manage-sender-filtering-exchange-2013-help.md).


> [!IMPORTANT]
> MAIL FROM: Cabeçalhos de SMTP podem ser falsificados. Portanto, você não deve confiar em somente o agente do filtro de remetente. Use o agente de filtro de remetente e o agente de ID de remetente juntos. Endereço IP de origem do servidor de envio usa o agente de ID de remetente para verificar se o domínio no MAIL FROM: cabeçalho SMTP corresponde ao domínio que está registrado. Para obter mais informações sobre o agente de ID do remetente, consulte <A href="sender-id-exchange-2013-help.md">ID de remetente</A>.



## Usando o agente de filtro de remetente para bloquear mensagens

Quando o agente do filtro de remetente está habilitado em um servidor Exchange, blocos de filtragem de remetente entrada mensagens que vêm da Internet, mas não são autenticadas. Essas mensagens são tratadas como mensagens externas. Você pode desabilitar o agente de filtro de remetente nas configurações do computador individual. Para obter mais informações, consulte [Gerenciar filtragem de remetente](manage-sender-filtering-exchange-2013-help.md).

Quando você habilita o agente de filtro de remetente em um servidor do Exchange, os filtros de agente de filtro de remetente todas as mensagens que vêm por meio de todos os conectores de recebimento no computador. Conforme observado anteriormente neste tópico, somente as mensagens que vêm de fontes externas são filtradas. *Fontes externas* são definidos como fontes de não-autenticados. Estas são consideradas anônimos fontes de Internet.

Como prática recomendada, você não deve filtrar mensagens de email a partir de parceiros confiáveis ou dentro da organização. Quando você executa pelos filtros antispam, sempre há uma chance de que os filtros detectará falsos positivos. Você deve configurar agentes antispam para ser executado somente em mensagens de fontes potencialmente não confiáveis e desconhecidas. Isso reduzirá a chance que pelos filtros antispam serão mishandle mensagens legítimas. Você pode habilitar e desabilitar o agente de filtro de remetente seja executado em mensagens de qualquer origem. Para obter mais informações, consulte [Gerenciar filtragem de remetente](manage-sender-filtering-exchange-2013-help.md).

Você pode configurar o agente de filtro de remetente para bloquear mensagens de entrada que não especificam um remetente e o domínio em MAIL FROM: cabeçalho SMTP. Você pode usar esse recurso a prevenir ataques de relatório de falha na entrega (NDR) no servidor Exchange. Mais legítimas mensagens de SMTP provenientes de servidores SMTP que fornecem um remetente e o domínio no MAIL FROM: comando SMTP.

## Especificação da ação de bloqueio

Após especificar domínios e remetentes bloqueados, especifique como deseja que o agente de filtro de remetente agir em mensagens de remetentes bloqueados e domínios. Recomendamos que você rejeitar as mensagens. Quando você usa o agente Filtro de remetente para bloquear os endereços de email e domínios especificados por um administrador do Exchange, a chance de falsos positivos é relativamente menor do que quando você usar outros agentes antispam. Por exemplo, o agente Filtro de conteúdo é um agente anti-spam que depende de muitas variáveis diferentes para determinar se uma mensagem é spam.

Há apenas dois cenários nos quais as mensagens legítimas poderão ser rejeitadas pelo agente de filtro por remetente:

  - Se você vir a digitar um nome de domínio ou endereço de email, o remetente errado poderão ser bloqueado.

  - Se um nome de domínio está registrado para uma empresa legítima depois de adicionar o domínio à sua lista de remetentes bloqueados, involuntariamente bloqueará mensagens legítimas.

Em qualquer um desses casos, talvez ainda seja adequado para rejeitar as mensagens.

