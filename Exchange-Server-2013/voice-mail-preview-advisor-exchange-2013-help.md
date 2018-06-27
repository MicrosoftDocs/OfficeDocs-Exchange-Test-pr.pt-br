---
title: 'Supervisor de visualização de correio de voz: Exchange 2013 Help'
TOCTitle: Supervisor de visualização de correio de voz
ms:assetid: 0957dd54-df6d-4b50-9db5-4757f548b899
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Ee364730(v=EXCHG.150)
ms:contentKeyID: 51407834
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Supervisor de visualização de correio de voz

 

_**Aplica-se a:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Tópico modificado em:**2016-12-09_

A Unificação de Mensagens do Exchange Microsoft inclui um recurso chamado Visualização da caixa postal. Esse recurso usa o ASR (Reconhecimento Automático de Fala) para adicionar uma versão em texto do arquivo de áudio da caixa postal em mensagens na caixa postal. O ASR não é totalmente preciso, especialmente quando é usado para gravar áudio em um telefonema com vozes desconhecidas e ruídos. Algumas organizações exigem transcrições de mensagens de voz sem erros (ou quase sem erros). O Programa de parceiros de Visualização da caixa postal ajudará tais organizações a atenderem a essas exigências.

A Visualização da caixa postal usa as [tecnologias de fala da Microsoft](http://go.microsoft.com/fwlink/p/?linkid=187348) para prover uma versão em texto de registros de áudio. O texto da caixa postal é exibido nas mensagens de email dentro do MicrosoftOutlook Web App, Outlook 2010 ou de versões mais recentes, e outros programas de email.

Por padrão, quando você habilita um usuário para UM em uma implantação local ou híbrida, as visualizações de caixa postal serão enviadas se houver um pacote de idiomas da UM suportado instalado. Quando você habilita um usuário para UM no Exchange Online, todos os pacotes de idioma da UM são instalados. No entanto, a Visualização de caixa postal não é suportada em todos os idiomas instalados.

Há parceiros de Visualização da Caixa Postal que oferecem suporte avançado a transcrições e serviços para o recurso de Visualização da Caixa Postal. Esses parceiros empregam pessoas para corrigir as transcrições da caixa postal que foram criadas usando-se o ASR. Cada parceiro de Visualização de Caixa Postal deve cumprir um conjunto de requisitos, para ser certificado a interoperar com a UM do Exchange.

Se achar que as visualizações de correio de voz é enviada para os usuários não são precisos o suficiente, você pode contatar um dos parceiros visualização da caixa postal certificados listados na [Microsoft identifique](https://go.microsoft.com/fwlink/p/?linkid=281966) e sign up com eles a um custo adicional.

**Sumário**

Visão geral

Exchange Unified Messaging Voice Mail Partner program

Voice Mail Preview partners certified for Exchange Unified Messaging

Configuring Voice Mail Preview partners

VoIP or media gateways and IP PBX support

## Visão geral

Quando a Unificação de Mensagens registra o áudio de uma mensagem da caixa postal, ele usa o ASR para criar o texto da visualização da caixa postal a partir do arquivo de áudio e, então, envia a mensagem de voz completa para o usuário. Para cada mensagem de voz criada, a Unificação de Mensagens determina um nível de confiança para a visualização da caixa postal incluída na mensagem. Ela mede o quanto os sons na gravação correspondem às palavras, números e frases na mensagem. Se o sistema localiza facilmente essas correspondências, o nível de confiança será alto. O nível alto de confiança geralmente é associado a uma maior exatidão.

A exatidão do texto na visualização da caixa postal depende de diversos fatores que nem sempre podem ser controlados. Contudo, é provável que o texto seja mais exato quando:

  - A mensagem de voz deixada é simples e o chamador não usa gírias, jargões técnicos ou palavras ou frases incomuns.

  - O chamador usa um idioma facilmente reconhecido e traduzido pelo sistema de caixa postal. Geralmente, as mensagens de voz deixadas por chamadores que não falam rápido ou suave demais e que não têm sotaques fortes produzirão sentenças e frases mais exatas.

  - Não há ruídos de fundo nem ecos na mensagem de voz e o áudio não é interrompido.

A maioria dos clientes que usam a Unificação de Mensagens descobre que as visualizações da caixa postal são suficientemente exatas para seus usuários. No entanto, quando o ASR é aplicado em gravações feitas ao telefone por vozes desconhecidas e com ruídos de fundo, o texto de visualização da caixa postal não é completamente exato. Se o nível de confiança for consistentemente baixo ou se as visualizações da caixa postal que foram recebidas estiverem pouco exatas, é possível aumentar a exatidão dessas visualizações recebidas pelo usuário da seguinte maneira:

  - Assine um serviço de transcrição de voz oferecido por um parceiro de Visualização de caixa postal.

  - Depois de se inscrever em um parceiro de Visualização de caixa postal, defina o parceiro para trabalhar com UM. Para obter mais informações sobre como configurar a UM para um parceiro de Visualização de caixa postal, consulte [Configurar serviços de parceiros de visualização da caixa postal para usuários](configure-voice-mail-preview-partner-services-for-users-exchange-2013-help.md).

Quando você se inscreve em um parceiro de Visualização de caixa postal, os servidores do Exchange em sua organização redirecionam as mensagens da voz com o arquivo de áudio anexado para o parceiro de Visualização de caixa postal, em vez de gerar o texto da visualização de caixa postal para mensagens de voz e enviá-lo à caixa postal do usuário A mensagem de email com o texto da visualização de caixa postal produzido pelo parceiro de Visualização de caixa postal é enviada aos servidores do Exchange em sua organização para ser entregue à caixa de correio do destinatário.


> [!IMPORTANT]
> Recomendamos que todos os clientes que planejam implantar a Unificação de mensagens obtenham a assistência de um especialista de Unificação de MENSAGENS. Um especialista de Unificação de MENSAGENS o ajuda a garantir que haja uma transição suave para Unificação de MENSAGENS de um sistema de correio de voz herdado. Realizando uma nova implantação ou atualizando um sistema de correio de voz herdado exige conhecimento significativo sobre gateways VoIP, IP PBXs, PBXs controladores de borda de sessão (SBCs) e a Unificação de mensagens. Para obter mais informações sobre como entrar em contato com um especialista de Unificação de MENSAGENS, consulte o <A href="http://go.microsoft.com/fwlink/p/?linkid=262708">Microsoft Exchange Server 2013 Unified Messaging (UM) especialistas</A> ou <A href="https://go.microsoft.com/fwlink/p/?linkid=261951">Microsoft identifique para Unificação de mensagens</A>.



Voltar ao início

## Programa de parceiros da caixa postal da Unificação de Mensagens do Exchange

Para se tornar um parceiro certificado de Visualização de caixa de correio que interopera com a UM do Exchange, o parceiro deve implementar os requisitos contidos na Especificação de interoperabilidade de Visualização de caixa postal, e a solução do parceiro deve ser certificada por um fornecedor de certificação independente. Se você está interessado em certificar seu serviço de transcrição para trabalhar com a UM do Exchange, envie uma solicitação para [Parceiros de Visualização de caixa postal para a Unificação de Mensagens do Exchange](mailto:vmppp@microsoft.com).

## Parceiros de Visualização de caixa postal certificados para a Unificação de Mensagens do Exchange

Se você já implantou Unificação de mensagens em sua organização, e você está procurando por um parceiro certificado de visualização da caixa postal fornecer serviços de suporte de transcrição, consulte [Microsoft identifique](https://go.microsoft.com/fwlink/p/?linkid=281966). Esses fornecedores de software foram certificadas como interoperável com o UM do Exchange.

## Configuração dos parceiros de Visualização de caixa postal

Após a configuração da UM, ela encaminha as mensagens de voz com o áudio para um parceiro dedicado de Visualização de caixa postal que, por sua vez, recebe o arquivo de áudio e cria o texto de visualização de caixa postal. No entanto, para permitir que os usuários recebam a visualização de caixa postal com suas mensagens de voz em sua caixa de correio, é necessário configurar uma política de caixa de correio da UM, associar os usuários a essa política e confirmar com os usuários se eles recebem visualizações de caixa postal em suas mensagens de voz no Outlook 2010, ou em uma versão mais recente, ou no Outlook Web App. Para obter mais informações sobre como configurar a UM para um parceiro de Visualização de caixa postal, consulte [Configurar serviços de parceiros de visualização da caixa postal para usuários](configure-voice-mail-preview-partner-services-for-users-exchange-2013-help.md).

## Suporte para VoIP ou gateways de mídia e PBX IP

Configurar os gateways VoIP e os PBX IPs de sua organização é uma tarefa de difícil implantação que deve ser concluída de forma correta para que se possa implantar com êxito a Unificação de Mensagens com um parceiro de Visualização de caixa postal. Para informações que possam auxiliá-lo na configuração de seus gateways VoIP e PBX IPs, e para as informações mais atualizadas sobre como configurá-los, consulte [Supervisor de telefonia para o Exchange 2013](telephony-advisor-for-exchange-2013-exchange-2013-help.md) ou [Notas de configuração para gateways VoIP com suporte, IP PBXs e PBXs](configuration-notes-for-supported-voip-gateways-ip-pbxs-and-pbxs-exchange-2013-help.md).

Teste de interoperabilidade de UM do Exchange com gateways VoIP foi integrada com Microsoft programa de interoperabilidade aberta do Unified Communications. Para obter mais informações, consulte [Microsoft Unified Communications programa de interoperabilidade aberta](https://go.microsoft.com/fwlink/p/?linkid=132071).

Voltar ao início

