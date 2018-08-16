---
title: 'Filtragem de destinatário nos servidores de Transporte de Borda'
TOCTitle: Filtragem de destinatário nos servidores de Transporte de Borda
ms:assetid: 994eefd9-3903-41e6-a882-1e333d6d2d18
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Bb123891(v=EXCHG.150)
ms:contentKeyID: 50486243
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Filtragem de destinatário nos servidores de Transporte de Borda

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2014-05-07_

Filtragem de destinatário é um recurso antispam no Microsoft Exchange Server 2013 que se baseia no cabeçalho RCPT TO SMTP para determinar que ação, se houver, deve ser tomada em uma mensagem de entrada. A Filtragem de destinatário é executada pelo agente de Filtro de Destinatários.

O agente Filtro de Destinatários bloqueia mensagens de acordo com as características do destinatário desejado na organização. O agente do Filtro de Destinatário pode ajudar a impedir a aceitação de mensagens nos cenários a seguir:

  - **Destinatários inexistentes**   Você pode impedir a entrega a destinatários que não estejam no catálogo de endereços da organização. Por exemplo, você poderá interromper o envio para nomes de contas freqüentemente mal usados, como administrator@contoso.com ou support@contoso.com.

  - **Listas de distribuição restrita**   Você pode impedir a entrega de emails da Internet a listas de distribuição que deveriam ser usadas apenas por usuários internos.

  - **Caixas de correio que nunca devem receber mensagens da Internet**   Você pode impedir a entrega de emails da Internet a uma caixa de correio ou alias específico que é geralmente usado dentro da organização, como Assistência Técnica.

O agente Filtro de Destinatário atua nos destinatários armazenados em uma ou em ambas as fontes de dados a seguir:

  - **Lista de Bloqueio de Destinatários**   Uma lista de destinatários, definida pelo administrador, que nunca devem receber mensagens da internet.

  - **Pesquisa de Destinatário**   Consulta o Active Directory para verificar se o destinatário existe na organização. Em um servidor de Transporte de Borda, a Pesquisa de Destinatário requer acesso às informações do Active Directory proporcionadas pelo EdgeSync para a instância local dos Active Directory Lightweight Directory Services (AD LDS).

Quando você habilita o agente do Filtro de Destinatário, uma das ações a seguir é tomada nas mensagens de saída de acordo com as características dos destinatários. Esses destinatários estão indicados pelo cabeçalho RCPT TO.

  - Se a mensagem de entrada contiver um destinatário que esteja na lista de Bloqueios de Destinatários, o servidor Exchange enviará um erro de sessão SMTP `550 5.1.1 User unknown` ao servidor de envio.

  - Se a mensagem de entrada contiver um destinatário que não corresponda a nenhum destinatário na Pesquisa de Destinatários, o servidor Exchange enviará um erro de sessão SMTP `550 5.1.1 User unknown` ao servidor de envio.

  - Se o destinatário não estiver na lista de Bloqueios de Destinatários e estiver na Pesquisa de Destinatário, o servidor Exchange enviará uma resposta SMTP `250 2.1.5 Recipient OK` para o servidor de envio, e o próximo agente antispam na cadeia processará a mensagem.

**Conteúdo**

Configuring recipient lookup

Tarpitting functionality

Multiple namespaces

## Configurando a pesquisa de destinatário

Uma das maneiras mais eficazes de reduzir spam é validar destinatários antes de aceitar mensagens de entrada da Internet. Você habilita o bloqueio de mensagens enviadas a destinatários que não existem na organização do Exchange e o bloqueio de destinatários específicos usando o cmdlet **Set-RecipientFilterConfig** no Shell de Gerenciamento do Exchange. Para obter mais informações, consulte [Gerenciar filtragem por destinatário nos servidores de transporte de borda](manage-recipient-filtering-on-edge-transport-servers-exchange-2013-help.md).

Se você tem um servidor de Transporte de Borda instalado na sua rede de perímetro, o ideal é configurar a instância dos serviços AD LDS executada no servidor de Transporte de Borda para que sincronize com o Active Directory. Por padrão, o AD LDS é instalado e configurado no servidor de Transporte de Borda. No entanto, você deve configurar os serviços AD LDS para que se comuniquem com um servidor de catálogo global unido por domínio do Active Directory, inscrevendo o servidor de Transporte de Borda na sua organização. Para obter mais informações, consulte [Usar um Exchange 2010 ou o servidor de transporte de borda 2007 no Exchange 2013](use-an-exchange-2010-or-2007-edge-transport-server-in-exchange-2013-exchange-2013-help.md).

Voltar ao início

## Funcionalidade de tarpitting

A funcionalidade Pesquisa de Destinatário permite que o servidor de envio determine se um endereço de email é válido ou inválido. Conforme mencionado anteriormente, quando o destinatário de uma mensagem de entrada for um destinatário conhecido, o servidor Exchange envia de volta uma resposta SMTP `250 2.1.5 Recipient OK` ao servidor de envio. Essa funcionalidade fornece um ambiente ideal para um ataque de colheita de diretório.

Um *ataque de coleta de diretório* é uma tentativa de coletar endereços de email válidos de uma organização específica, para que os endereços de email possam ser adicionados a um banco de dados de spam. Como o rendimento de todo spam se baseia em tentar fazer as pessoas abrirem mensagens de email, endereços conhecidos como ativos são uma mercadoria pela qual usuários mal-intencionados, ou *spammers*, pagam. Como o protocolo SMTP fornece comentários sobre remetentes conhecidos e remetentes desconhecidos, um spammer pode escrever um programa automatizado que usa nomes comuns ou termos de dicionário para construir endereços de email para um domínio específico. O programa coleta todas as mensagens de email que retornem uma resposta SMTP `250 2.1.5 Recipient OK` e descarta todos os endereços de email que retornem um erro de sessão SMTP `550 5.1.1 User unknown`. O spammer pode, então, vender os endereços de email válidos ou usá-los como destinatários para mensagens não solicitadas.

Para combater ataques de colheita de diretório, o Exchange 2013 inclui a funcionalidade de tarpitting. *Tarpitting* é a prática de retardar artificialmente as respostas do servidor para padrões de comunicação SMTP específicos que indiquem altos volumes de spam ou outras mensagens indesejadas. O objetivo do tarpitting é reduzir o processo de comunicação desse tráfego de email para que o custo de envio de spam aumente para a pessoa ou organização que está enviando o spam. O tarpitting torna os ataques de colheita de diretório dispendiosos demais para serem automatizados de forma eficaz.

Se o tarpitting não estiver configurado, o servidor Exchange retornará imediatamente o erro de sessão SMTP `550 5.1.1 User unknown` para o remetente quando um destinatário não for localizado na Pesquisa de Destinatário. Por outro lado, se o tarpitting estiver configurado, o SMTP aguardará um número de segundos especificado antes de retornar o erro `550 5.1.1 User unknown`. Essa pausa na sessão SMTP torna a automação do ataque de colheita de diretório mais difícil e menos rentável para o spammer. Por padrão, o tarpitting está configurado para 5 segundos nos conectores de recebimento.

Para configurar o atraso em que o SMTP retorna o erro `550 5.1.1 User unknown`, você define o intervalo do tarpitting usando o parâmetro *TarpitInterval* no cmdlet **Set-ReceiveConnector**. A sintaxe é:

    Set-ReceiveConnector <Receive Connector> -TarpitInterval <00:00:00 to 00:10:00>

O valor padrão é `00:00:05` ou 5 segundos. O nome do conector padrão de Recebimento em um servidor de Transporte de Borda é `Default internal receive connector <server name>`.

Tome cuidado se decidir alterar o valor de tarpitting. Um intervalo demasiadamente longo poderá interromper o fluxo normal de mensagens, enquanto um intervalo breve demais poderá não ser tão eficaz no impedimento de um ataque de colheita do diretório. Se você alterar o intervalo de tarpitting, faça isso em incrementos menores e verifique os resultados. Por exemplo, se cinco segundos não forem suficientes, tente alterar o intervalo para 10 segundos.

Voltar ao início

## Vários namespaces

O agente do filtro de destinatário realiza pesquisas do destinatários somente para domínios autoritativos. Se sua organização aceita e repassa mensagens em nome de outro domínio que está configurado como um domínio de retransmissão interna ou externa, o agente Filtro de Destinatários não realiza pesquisa de destinatário em destinatários nestes domínios. No entanto, se um destinatário estiver especificado na lista de Bloqueios de Destinatários, o destinatário ainda será bloqueado pelo agente Filtro de Destinatário.

Observe que você também pode configurar localmente domínios aceitos em um servidor de Transporte de Borda. Se o domínio for configurado como um domínio de retransmissão interna ou externa, o agente Filtro de Destinatários no servidor de Transporte de Borda não realiza uma pesquisa de destinatários em destinatários nestes domínios.

Voltar ao início

