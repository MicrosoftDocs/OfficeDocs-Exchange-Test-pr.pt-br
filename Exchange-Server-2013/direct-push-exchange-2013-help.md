---
title: 'Direct Push: Exchange 2013 Help'
TOCTitle: Direct Push
ms:assetid: 373c1629-3d4b-4828-b014-9e103de4ef25
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Aa997252(v=EXCHG.150)
ms:contentKeyID: 50485337
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Direct Push

 

_**Aplica-se a:** Exchange Online, Exchange Server 2013_

_**Tópico modificado em:** 2012-07-11_

Direct Push é um recurso que está incorporado ao Microsoft Exchange Server 2013. O Direct Push mantém um dispositivo móvel sincronizado em uma conexão de rede sem fio ou de celular. Ele avisa ao dispositivo móvel quando há conteúdo novo pronto para ser sincronizado.

**Conteúdo**

Visão geral

Direct Push topology

Configuring Direct Push to work through your firewall

## Visão geral

Para o Direct Push funcionar, o dispositivo móvel deve ser compatível com o Direct Push. Esses dispositivos incluem os seguintes:

  - Todas as versões do Windows Phone

  - Celulares produzidos por licenciados do Microsoft Exchange ActiveSync e que tenham sido projetados especificamente para serem compatíveis com Direct Push

Por padrão, o Direct Push é habilitado no Exchange 2013. Dispositivos móveis que oferecem suporte a Direct Push emitem uma solicitação HTTPS de longa duração para o servidor Microsoft Exchange. O servidor do Exchange monitorará a atividade na caixa de correio do usuário e enviará uma resposta para o dispositivo móvel se houver alterações, como itens novos ou alterados de email, calendário, contatos ou tarefas. Se ocorrerem alterações dentro do tempo de vida da solicitação HTTPS, o servidor Exchange emitirá uma resposta para o dispositivo que informa a ocorrência dessas alterações e o dispositivo deverá iniciar a sincronização com o servidor Exchange. Em seguida, o dispositivo emite essa solicitação para o servidor. Quando a sincronização é concluída, uma nova solicitação HTTPS de longa duração é gerada para iniciar o processo novamente. Isso garante que itens de email, calendário, contatos e tarefas sejam entregues rapidamente para o dispositivo móvel e que o dispositivo esteja sempre sincronizado com o servidor Exchange.

## Topologia de Direct Push

O Direct Push opera da seguinte maneira:

1.  Um dispositivo móvel configurado para sincronização com um servidor Exchange 2013 emite uma solicitação HTTPS para o servidor. Essa solicitação é conhecida como PING. A solicitação faz com que o servidor notifique o dispositivo se algum item for alterado nos próximos 15 minutos em alguma pasta configurada para sincronização. Caso contrário, o servidor deverá retornar uma mensagem HTTP 200 OK. Em seguida, o dispositivo móvel entra no modo de espera. O tempo de vida de 15 minutos é conhecido como *intervalo de pulsação*.

2.  Se nenhum item for alterado em 15 minutos, o servidor retornará uma resposta HTTP 200 OK. O dispositivo móvel recebe essa resposta, retoma a atividade (conhecida como *ativação*) e emite sua solicitação novamente. Isso reinicia o processo.

3.  Se alguns itens forem alterados ou novos itens forem recebidos dentro do intervalo de pulsação de 15 minutos, o servidor enviará uma resposta que informa ao dispositivo móvel se há um item novo ou alterado e fornece o nome da pasta em que o item novo ou alterado reside. Depois que o dispositivo móvel receber essa resposta, ele emitirá uma solicitação de sincronização para a pasta que tem os itens novos ou alterados. Quando a sincronização for concluída, o dispositivo móvel emitirá uma nova solicitação de PING e o processo inteiro se inicia novamente.

O Direct Push depende de condições de rede que ofereçam suporte a uma solicitação HTTPS de longa duração. Se a rede da operadora do dispositivo móvel ou do firewall não aceitar solicitações HTTPS de longa duração, a solicitação HTTPS será parada. As etapas a seguir descrevem como o Direct Push opera quando a rede da operadora do dispositivo móvel tem um valor de tempo limite de 13 minutos.

1.  Um dispositivo móvel emite uma solicitação HTTPS para o servidor. A solicitação faz com que o servidor notifique o dispositivo se algum item for alterado nos próximos 15 minutos em alguma pasta configurada para sincronização. Caso contrário, o servidor deverá retornar uma mensagem HTTP 200 OK. Em seguida, o dispositivo móvel entra no modo de espera.

2.  Se o servidor não responder após 15 minutos, o dispositivo móvel será ativado e concluirá que o tempo limite da conexão com o servidor foi esgotado pela rede. O dispositivo emite novamente a solicitação HTTPS, mas dessa vez usa um intervalo de pulsação de 8 minutos.

3.  Após 8 minutos, o servidor envia uma mensagem HTTP 200 OK. Em seguida, o dispositivo tenta obter uma conexão mais longa emitindo uma nova solicitação HTTPS para o servidor que tiver um intervalo de pulsação de 12 minutos.

4.  Após 4 minutos, uma nova mensagem de email é recebida e o servidor responde enviando uma solicitação HTTPS que faz com que o dispositivo seja sincronizado. O dispositivo é sincronizado e emite novamente a solicitação HTTPS com uma pulsação de 12 minutos.

5.  Após 12 minutos, se não houver itens novos ou alterados, o servidor responderá enviando uma mensagem HTTP 200 OK. O dispositivo é ativado e conclui que as condições da rede aceitarão um intervalo de pulsação de 12 minutos. Em seguida, o dispositivo tenta obter uma conexão mais longa emitindo novamente uma solicitação HTTPS com um intervalo de pulsação de 16 minutos.

6.  Após 16 minutos, nenhuma resposta é recebida do servidor. O dispositivo é ativado e conclui que as condições da rede não podem aceitar um intervalo de pulsação de 16 minutos. Como essa falha ocorreu imediatamente depois que o dispositivo tentou aumentar o intervalo de pulsação, ele conclui que o intervalo de pulsação atingiu seu limite máximo. Em seguida, o dispositivo emite uma solicitação HTTPS com um intervalo de pulsação de 12 minutos, pois esse foi o último intervalo de pulsação bem-sucedido.

O dispositivo móvel tenta usar o intervalo de pulsação mais longo ao qual a rede oferece suporte. Isso prolonga a vida útil da bateria no dispositivo e reduz quantos dados são transferidos na rede. As operadoras de celular podem especificar um valor de pulsação máximo, mínimo e inicial nas configurações de Registro do dispositivo móvel.

## Configurar o Direct Push para funcionar através do firewall

Para o Direct Push funcionar pelo firewall, você deve abrir a porta TCP 443. Essa porta é obrigatória para o protocolo SSL (Secure Sockets Layer) e deve permanecer aberta entre a Internet e o servidor de Acesso do Cliente.

Além de abrir portas no firewall, para obter desempenho ideal do Direct Push, você deve aumentar o valor de tempo limite no firewall do padrão de 15 para 30 minutos. A duração máxima da solicitação HTTPS é determinada pelas seguintes configurações:

  - O tempo limite máximo definido nos firewalls que controlam o tráfego da Internet para o servidor de Acesso do Cliente

  - Os valores de tempo limite de firewall são definidos pelo provedor de serviços móveis

