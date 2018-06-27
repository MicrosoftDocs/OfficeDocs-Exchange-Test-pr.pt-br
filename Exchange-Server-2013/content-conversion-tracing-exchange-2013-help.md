---
title: 'Rastreamento de conversão de conteúdo: Exchange 2013 Help'
TOCTitle: Rastreamento de conversão de conteúdo
ms:assetid: eb9c7df2-9093-49f9-aa4f-044909bd2225
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Bb397226(v=EXCHG.150)
ms:contentKeyID: 50486935
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Rastreamento de conversão de conteúdo

 

_**Aplica-se a:**Exchange Server 2013_

_**Tópico modificado em:**2012-09-25_

Rastreamento de conversão de conteúdo captura falhas na conversão de conteúdo de MAPI que é executada pelo serviço de transporte de caixa de correio em mensagens de entrada e saídas em um servidor de caixa de correio do Microsoft Exchange Server 2013.

O serviço de transporte de caixa de correio em um servidor de caixa de correio é responsável pela conversão de conteúdo de mensagens enviadas de e para destinatários de caixa de correio. Especificamente, o serviço de envio de transporte de caixa de correio converte mensagens de saída dos usuários de caixa de correio de MAPI como MIME. O serviço de entrega de transporte de caixa de correio converte mensagens de entrada para os usuários de caixa de correio de MIME para MAPI. Rastreamento de conversão de conteúdo é responsável por capturar essas falhas de conversão de MAPI.

Categorizador no serviço de transporte em um servidor de caixa de correio é responsável pela conversão de conteúdo de todas as mensagens enviadas a destinatários externos. Rastreamento de conversão de conteúdo não captura quaisquer falhas de conversão de conteúdo que o categorizador no serviço de transporte encontra à medida que ele converte as mensagens enviadas a destinatários externos.

**Sumário**

Configurar o rastreamento de conversão de conteúdo

Conversão de conteúdo como rastreamento funciona

Considerações para rastreamento de conversão de conteúdo

## Configurar o rastreamento de conversão de conteúdo

Rastreamento de conversão de conteúdo é controlado pelos seguintes parâmetros nos cmdlets **Set-TransportService** e **Set-MailboxTransportService** no Shell de gerenciamento do Exchange:

  - *ContentConversionTracingEnabled*   Este parâmetro habilita ou desabilita o rastreamento de conversão de conteúdo no serviço de transporte no servidor de caixa de correio ou no serviço de transporte de caixa de correio no servidor de caixa de correio. Valores válidos para este parâmetro são `$true` e `$false`. O valor padrão é `$false`. Se sua organização do Exchange contém vários servidores de caixa de correio, você deve ativar o rastreamento de conversão de conteúdo em cada servidor de caixa de correio.

  - *PipelineTracingPath*   Embora esse parâmetro está associado com o rastreamento de pipeline, também especifica o local da raiz dos arquivos de conversão de conteúdo de rastreamento. O local padrão no serviço de transporte é `%ExchangeInstallPath%TransportRoles\Logs\Hub\PipelineTracing`. O local padrão no serviço de transporte de caixa de correio é `%ExchangeInstallPath%TransportRoles\Logs\Mailbox\PipelineTracing`. O caminho deve ser local para o computador do Exchange.

Conversão de conteúdo cria uma pasta denominada `ContentConversionTracing` no caminho especificado pelo parâmetro *PipelineTracingPath* . Na pasta `ContentConversionTracing` , conversão de conteúdo cria duas subpastas: `InboundFailures` e `OutboundFailures`. A pasta `InboundFailures` contém as informações de falhas de conversão do conteúdo da mensagem de entrada. A pasta `OutboundFailures` contém as informações de falhas de conversão do conteúdo da mensagem de saída.

O tamanho máximo para todos os arquivos na pasta `InboundFailures` ou a pasta `OutboundFailures` é 128 megabytes (MB). Rastreamento de conversão de conteúdo não usa o log circular para remover arquivos antigos baseados na idade ou tamanho dos arquivos. Assim que o tamanho máximo de uma pasta for atingido, rastreamento de conversão de conteúdo interrompe gravando informações para a pasta. Se você quiser verificar se os limites de tamanho máximo de pasta não são excedidos, você pode criar uma tarefa agendada que periodicamente move os arquivos de conversão de conteúdo de rastreamento para um local diferente.

As permissões necessárias nas pastas e subpastas usadas no rastreamento de conversão de conteúdo são os seguintes:

  - Administradores: Controle Total

  - Serviço de Rede: Controle Total

  - Sistema: Controle Total


> [!WARNING]
> Rastreamento de conversão de conteúdo copia todo o conteúdo das mensagens de email. Para evitar a divulgação indesejada de informações confidenciais, você precisará definir permissões de segurança apropriadas no local da conversão conteúdo os arquivos de rastreamento.



Voltar ao início

## Conversão de conteúdo como rastreamento funciona

Quando a conversão de conteúdo de uma mensagem de entrada falhar, uma notificação de status de entrega (DSN) que tem o código de status 5.6.0 é enviada ao remetente da mensagem. Se o rastreamento de conversão de conteúdo estiver habilitado, as informações de falha são registradas no momento em que o 5.6.0 mensagem DSN é gerada. Cada erro de conversão de conteúdo gera dois arquivos separados.

Um erro de conversão de conteúdo que ocorre quando uma mensagem de entrada é convertida de MIME em MAPI gera os dois arquivos a seguintes na pasta InboundFailures:

  - **. eml de \< GUID \>**   Esse arquivo contém a mensagem com falha em formato de texto.

  - **txt \< GUID \>**   Este arquivo contém a descrição da exceção, resultados de conversão, opções de conversão e limites de tamanho de mensagem impostos em todas as mensagens pelo serviço de transporte de caixa de correio.

Um erro de conversão de conteúdo que ocorre quando uma mensagem de saída é convertida de MAPI como MIME gera os dois arquivos a seguintes na pasta OutboundFailures:

  - **. msg de \< GUID \>**   Esse arquivo contém a mensagem de falha no formato de mensagem do Microsoft Outlook.

  - **txt \< GUID \>**   Este arquivo contém a descrição da exceção, resultados de conversão, opções de conversão e limites de tamanho de mensagem impostos em todas as mensagens pelo driver do repositório.

O espaço reservado \<*GUID*\> é o mesmo em ambos os nomes de arquivo. Cada erro de conversão de conteúdo gera um GUID diferente que é usado nos nomes de arquivo dos arquivos de texto e mensagem correspondente. Um exemplo de um GUID que é usado nos nomes de arquivo é `038b930e-61fd-4bfd-b9b4-0374c18b73f7`.

Voltar ao início

## Considerações para rastreamento de conversão de conteúdo

Você pode deixar o rastreamento de conversão de conteúdo habilitado para monitoramento proativo. Ou então, você pode ativar o rastreamento de conversão de conteúdo solucionar problemas de um evento de falha específicas. Você geralmente pode reproduzir falhas de conversão de conteúdo de entrada solicitando o destinatário do 5.6.0 mensagem DSN para reenviar a mensagem original.

Falhas de conversão de conteúdo de entrada são os mais comuns. Alguns dos motivos para erros de entrada de conversão de conteúdo incluem o seguinte:

  - **Violações de limites de tamanho de mensagem**   Esses limites de tamanho de mensagem são impostas pelo serviço de transporte de caixa de correio para ajudar a impedir ataques negação de serviço (DoS). Esses limites de mensagem estão listados no arquivo. txt \<*GUID*\>. Esses limites de mensagem incluem o seguinte:
    
      - **MaxMimeTextHeaderLength**   Esse limite Especifica o número máximo de caracteres de texto que pode ser usado em um cabeçalho MIME. O valor é 2000.
    
      - **MaxMimeSubjectLength**   Esse limite Especifica o número máximo de caracteres de texto que pode ser usado na linha de assunto. O valor é 255.
    
      - **Mtamanho**   Esse limite Especifica o tamanho máximo da mensagem. O valor é a 2147483647 bytes.
    
      - **MaxMimeRecipients**   Esse limite Especifica o número total de destinatários permitido em para, Cc e Cco campos. O valor é 12288.
    
      - **MaxRecipientPropertyLength**   Esse limite Especifica o número máximo de caracteres de texto que pode ser usado em uma descrição de destinatário. O valor é 1.000.
    
      - **MaxBodyPartsTotal**   Esse limite Especifica o número máximo de partes de mensagem que pode ser usado em uma mensagem de várias partes MIME. O valor é 250.
    
      - **MaxEmbeddedMessageDepth**   Esse limite Especifica o número máximo de mensagens encaminhadas que podem existir em uma mensagem. O valor é 30.
    
    Para obter mais informações sobre limites de tamanho de mensagem configurável usada no serviço de transporte em servidores de caixa de correio ou em servidores de transporte de borda, consulte [Limites de tamanhos de mensagens](message-size-limits-exchange-2013-help.md).

  - **Falha ao converter uma mensagem de entrada iCalendar para uma solicitação de reunião**   RFC 2445 define iCalendar como um padrão para a troca de dados do calendário. Causas específicas de falha de conversão incluem o seguinte:
    
      - Uso incorreto do iCalendar pelo agente de envio.
    
      - Construções do iCalendar que não sejam suportadas pelo esquema de calendário do Outlook ou do Exchange.
    
    Falhas de conversão do iCalendar não resultam no remetente receber uma 5.6.0 mensagem DSN. Em vez disso, a mensagem é entregue com um arquivo. ICS anexado que contém o corpo da mensagem iCalendar.

  - **Falhas causadas por mensagens MIME formatadas incorretamente**   Emails comerciais não solicitadas ou mensagens de spam podem ter formatação erros no cabeçalho da mensagem, como aspas não coincidentes nas descrições de destinatário. Um número muito menor de falhas causadas por mensagens MIME formatadas incorretamente é considerado bugs.

Falhas de conversão de conteúdo de saída são muito menos comuns que as falhas de entrada. Quando ocorrem falhas de saída, eles são geralmente causados por erros no código ou corrompido o conteúdo da mensagem.

Voltar ao início

