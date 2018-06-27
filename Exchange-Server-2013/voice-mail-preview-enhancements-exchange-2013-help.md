---
title: 'Melhorias da caixa postal preview: Exchange 2013 Help'
TOCTitle: Melhorias da caixa postal preview
ms:assetid: 1fcccec1-4edc-40b8-948c-111647d7d770
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/JJ150501(v=EXCHG.150)
ms:contentKeyID: 50485093
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Melhorias da caixa postal preview

 

_**Aplica-se a:**Exchange Server 2013, Exchange Server 2016_

_**Tópico modificado em:**2012-07-05_

Visualização da Caixa Postal é um recurso disponível a usuários que recebem suas mensagens de caixa postal de Unificação de Mensagens (UM) do Exchange Server 2010 ou do Exchange Server 2013. Visualização da Caixa Postal aprimora a funcionalidade de caixa postal de UM, fornecendo uma versão em texto de gravações de áudio. O texto da caixa postal é mostrada em um email dentro do Microsoft Office Outlook Web App, Outlook 2010 e outros programas de email.

## Aperfeiçoamentos da Visualização de Caixa Postal

No Exchange 2013, a UM inclui vários aperfeiçoamentos para a interface de usuário para clientes Outlook Web App e Outlook e aperfeiçoamentos para aumentar a confiança e a precisão da Visualização da Caixa Postal. Além disso, alguns aperfeiçoamentos dos serviços relacionados à fala são oferecidos através da Microsoft Speech Platform (Versão 11.0) e Unified Communications Managed API (UCMA) 4.0, para aperfeiçoar a geração de gramática e o suporte ao idioma.

A Unificação de Mensagens apresenta o recurso de Visualização da Caixa Postal no Exchange 2010. A Visualização da Caixa Postal usa reconhecimento de fala automático (ASR) para adicionar uma versão em texto de um arquivo de áudio de caixa postal para uma mensagem de voz. O ASR não é totalmente preciso, especialmente quando é usado para gravar áudio em um telefonema que inclua vozes desconhecidas e ruídos.

Algumas organizações exigem transcrições de mensagens de caixa postal sem erros ou quase sem erros para alguns usuários, se não todos. O Programa de Parceiros de Visualização da Caixa Postal ajuda essas organizações a atenderem a essas exigências. O Programa de Parceiros de Visualização da Caixa Postal foi feito para o Exchange 2010 aperfeiçoar os resultados da Visualização da Caixa Postal, mas ele não foi usados pelos clientes do Exchange 2010 por causa dos custos e das despesas operacionais. Para cuidar desses problemas, o Exchange 2013 inclui estes aperfeiçoamentos para a Visualização da Caixa Postal:

  - **Normalização de áudio aperfeiçoada**   A normalização de áudio é o processo de aumentar (ou diminuir) uniformemente a amplitude de todo um sinal de áudio, de forma que a amplitude de pico resultante corresponda a um destino especificado ou à norma. A UM normaliza o registro de áudio, antes de compactá-lo e enviá-lo para o usuário.

  - **Reconhecimento de fala aperfeiçoado**   Reunindo mensagens de caixa postal (somente se os clientes do Exchange escolherem compartilhar essa informação), os resultados das visualizações de caixa postal podem ser usados para adicionar palavras e frases ao mecanismo de fala. Isso é feito definindo-se o parâmetro *VoiceMailAnalysisEnabled* para `$true`, usando-se o cmdlet **Set-UMMailbox**, ou definindo-se o parâmetro *AllowVoiceMailAnalysis* para `$true`, no cmdlet **Set-UMMailboxPolicy**. Além disso, a UM do Exchange 2013 usa as informações com mais eficiência de threads de email criados por um usuário com o Outlook Voice Access. Isso incluir informações (país, cidade, companhia) sobre o participante (Active Directory ou contato pessoal) e o número de telefone do Outlook Voice Access.

  - **Confiança da Visualização da Caixa Postal**   A pontuação de confiança é o número atribuído pela Unificação de Mensagens que está diretamente relacionado à precisão geral da transcrição. Os cálculos de confiança que são usados pelo UM foram ajustados para serem mais precisos e representarem a precisão real de uma mensagem transcrita.

  - **Filtragem** Palavras ofensivas são detectadas e filtradas, e os resultados são armazenados no cache e na caixa de correio do usuário.

  - **Ocultar a visualização em texto**   Se a pontuação de confiança de uma visualização de caixa postal estiver abaixo de um determinado limite, o texto da Visualização da Caixa Postal será oculto. Se o texto ficar oculto, a mensagem de voz irá incluir texto informando que a confiança da caixa postal era muito baixa para os resultados serem mostrados.

  - **Desempenho da transcrição**   A Visualização da Caixa Postal é uma operação que faz uso intenso da CPU, exigindo aproximadamente duas vezes o tempo necessário para processar um arquivo de áudio. Se gerar o texto de Visualização da Caixa Postal demorar muito, a limitação da CPU para de processar a visualização. No Exchange 2010, a UM não tentava transcrever qualquer mensagem de voz que tivesse mais que 75 segundos. No Exchange 2013, toda a mensagem de voz é transcrita, mas o texto da mensagem não é incluído, se tiver mais de 75 segundos.

  - **Esquemas de cores**   Por causa da confusão sobre as cores que eram usadas para distinguir entre confianças baixa, média e alta de uma Visualização de Caixa Postal, o esquema de cores foi removido do Exchange 2013 para o Outlook Web App e o Outlook.

