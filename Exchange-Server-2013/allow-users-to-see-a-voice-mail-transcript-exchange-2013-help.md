---
title: 'Permitir que os usuários vejam uma transcrição do correio de voz: Exchange 2013 Help'
TOCTitle: Permitir que os usuários vejam uma transcrição do correio de voz
ms:assetid: c5192e05-905c-440f-beec-1f697edc15b3
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Ff629381(v=EXCHG.150)
ms:contentKeyID: 51407909
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Permitir que os usuários vejam uma transcrição do correio de voz

 

_**Aplica-se a:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Tópico modificado em:**2016-12-09_

Visualização da caixa postal é um recurso que está disponível para os usuários que receberem suas mensagens de voz da Unificação de mensagens (UM). Visualização da caixa postal aprimora a funcionalidade de caixa postal Unificação de MENSAGENS existente, fornecendo uma versão de texto de gravações de áudio. O texto da caixa postal é exibido em mensagens de email dentro de MicrosoftOutlook Web App, Outlook 2010 e versões posteriores e em outros programas de email com suporte. Para obter mais informações, consulte [As tecnologias de fala da Microsoft](http://go.microsoft.com/fwlink/p/?linkid=187348).

## Os usuários precisam usar um programa de email específica?

Não. Visualização da caixa postal é incluída no texto do corpo da mensagem de qualquer programa de email, incluindo programas móveis. Embora os usuários podem usar outros programas de email para receber mensagens de voz, Outlook e Outlook Web App fornecem uma experiência melhor. Por exemplo, em Outlook 2010 e versões posteriores, quando uma palavra específica é clicada no texto de visualização da caixa postal, a reprodução de áudio da mensagem de voz será iniciado tocar ao mesmo que o word. Isso é útil para ouvir uma parte específica de uma mensagem de voz.

## Os usuários podem pesquisar mensagens de voz específica?

Sim. Palavras e frases no texto visualização da caixa postal são automaticamente indexados para que mensagens de voz serão exibidas nos resultados da pesquisa. Em Outlook 2010 e versões posteriores ou no Outlook Web App, os usuários também podem usar caixa **Anotações de áudio** adicionar texto sobre uma mensagem de voz. Essas notas também são incluídas nas pesquisas, para facilitar a localizar uma mensagem.

## Por que esse recurso é chamado "Visualização da caixa postal"?

É importante definir expectativas dos usuários corretamente. Visualização da caixa postal não necessariamente produza texto que é o mesmo o que os chamadores dizem em suas mensagens de voz. Na verdade, é geralmente inadequado de alguma maneira. Para chamá-lo a transcrição seria sugerir um resultado mais perfeito que geralmente pode ser obtido. Visualização sugere que o leitor deve ser capaz de entender a essência do conteúdo voz, que é o recurso real do recurso mais próxima.

## O que torna o texto de visualização da caixa postal mais ou menos precisos?

A precisão do texto visualização da caixa postal depende por vários fatores e em alguns casos, esses fatores não podem ser controlados. No entanto, o texto de visualização da caixa postal é provavelmente mais precisas quando:

  - O chamador deixar uma mensagem de voz simples que não inclui termos gíria, jargão técnico, ou incomuns palavras ou frases.

  - O chamador usa um idioma facilmente reconhecido e traduzido pelo sistema de caixa postal. Geralmente, as mensagens de voz deixadas por chamadores que não falam rápido ou suave demais e que não têm sotaques fortes produzirão sentenças e frases mais exatas.

  - A mensagem de voz é livre de ruídos de fundo, o eco e o áudio não descartar check-out.

## Quais idiomas podem ser usados com a visualização da caixa postal?

O texto de visualização de correio de voz está disponível nos seguintes idiomas:

  - Inglês (EUA) (en-US)

  - Inglês (Canadá) (en-CA)

  - Francês (França) (fr-FR)

  - Italiano (it-IT)

  - Polônia (pl-PL)

  - Português (Portugal) (pt-PT)

  - Espanhol (Espanha) (es-ES)

Se você tiver um local ou implantação híbrida da Unificação de MENSAGENS, você pode baixar os pacotes de idiomas de Unificação de MENSAGENS do [Centro de Download da Microsoft](https://go.microsoft.com/fwlink/?linkid=266542).

Se você tiver um local ou implantação híbrida, depois de instalar um pacote de idioma de Unificação de MENSAGENS, os planos de discagem e atendedores automáticos pode ser configurada para usar o idioma escolhido. Para clientes online, você não precisa instalar os pacotes de idiomas de Unificação de MENSAGENS. Muitas empresas possuem apenas um plano de discagem de UM. Unificação de MENSAGENS tentará criar uma visualização da caixa postal no idioma de plano de discagem padrão, mas somente será aprovada se o idioma padrão oferece suporte à visualização da caixa postal. Um plano de discagem UM só pode ser configurado para criar voz visualizações de email em um idioma por vez.

Para configurar a Unificação de MENSAGENS para fornecer voz visualizações de email em um idioma diferente en-US, siga estas etapas:

1.  Verificar se a visualização da caixa postal é suportada no idioma que deseja usar.

2.  Se você tiver um local ou implantação híbrida, baixe e instale o pacote de idiomas de Unificação de MENSAGENS apropriado. Baixando e instalando o pacote de idiomas não configuram o idioma de padrão de plano de discagem.

3.  Configure o plano de discagem com o idioma que será usado para visualização da caixa postal. Para obter mais informações, consulte [Definir o idioma padrão em um plano de discagem](set-the-default-language-on-a-dial-plan-exchange-2013-help.md).

Como visualização da caixa postal exibe o texto nos idiomas suportados depende do tipo de mensagem de voz que será enviada. Existem dois tipos:

  - **Mensagens de voz que são registradas quando um usuário não atende seu telefone**
    
    Para essas mensagens, o idioma usado para visualização da caixa postal é determinado pelo idioma falado e se há suporte para o idioma do chamador. Por exemplo, se um chamador deixar uma mensagem de voz em italiano, o texto de visualização da caixa postal aparecerão em italiano se italiano tiver sido configurado no plano de discagem. No entanto, se um chamador deixar uma mensagem em japonês, nenhum texto de visualização da caixa postal será incluído com a mensagem porque japonês não está disponível.

  - **Mensagens de voz que são enviadas para por um usuário do Outlook Voice Access**
    
    Para mensagens enviadas por um usuário de acesso de voz Outlook, o idioma que é usado para visualização da caixa postal é controlado pelo administrador do correio de voz. Assim, o texto de visualização da caixa postal será no mesmo idioma como o sistema de caixa postal. No entanto, se um chamador falando de um idioma que não é suportado para visualização da caixa postal usa Outlook Voice Access para deixar uma mensagem, nenhum texto de visualização da caixa postal será incluído com a mensagem. Para saber mais sobre Outlook Voice Access, consulte [Configurando o Outlook Voice Access](setting-up-outlook-voice-access-exchange-2013-help.md).

## Unificação de MENSAGENS sabe quando uma visualização da caixa postal não estiverem corretas?

O nível de confiança é determinado para cada visualização da caixa postal incluída com uma mensagem de voz. O sistema de caixa postal mede o quão bem os sons na gravação coincidem com as palavras, números e frases. Se forem encontradas correspondências facilmente, o nível de confiança é alto. Um nível mais alto de confiança é geralmente associado uma maior precisão.

Se o nível de confiança é determinado ser menor que um determinado valor, a frase de **Visualização da caixa postal (confiança é baixa)** é incluída acima do texto de visualização da caixa postal. Se o nível de confiança for baixo, é provável que o texto de visualização da caixa postal não serão exatos.

Unificação de mensagens usa reconhecimento automático de fala (ASR) para calcular seu confiança na visualização, mas não tem como determinar quais palavras estão erradas e que estão corretas.

No entanto, UM tente Saiba como melhorar a precisão de seus visualizações de correio de voz. Por exemplo, ele tenta corresponder o número de telefone do chamador (se fornecido) com contatos pessoais do usuário e o catálogo de endereços da sua organização ou os contatos de redes sociais. Se UM localizar uma coincidência, ele incluirá o nome do chamador, juntamente com suas listas padrão de nomes e palavras, ao executar ASR a gravação de voz.

## Visualização da caixa postal pode ser usada se ele não estiver totalmente preciso?

Usuários podem ter uma melhor experiência com a visualização da caixa postal, se eles não tentarem ler a visualização muito cuidadosamente, palavra por palavra. Em vez disso, elas devem procurar por nomes, números de telefone e frases, como "Retornar chamada" ou "Preciso falar" que podem fornecer dicas sobre o propósito da chamada.

Visualização da caixa postal não é esperada para dita mensagens exatamente, mas ela pode ajudar os usuários a responder perguntas como as seguintes:

  - Esta mensagem de voz está relacionada ao meu trabalho?

  - Esta mensagem de voz é importante para mim?

  - O chamador deixar um número? É diferente do quaisquer números que eu tiver listado para eles?

  - O chamador considere essa mensagem de voz de urgente?

  - Deve etapa fora de uma reunião para retorno de chamada essa pessoa?

  - Era esperado um uma chamada para confirmar a minha solicitação. Esta é a chamada de confirmação?

## Visualização da caixa postal pode ser ativada ou desativado

Sim. Se você tiver habilitado a visualização da caixa postal, os usuários podem ativá-lo ou desativar usando Outlook 2010 ou uma versão posterior ou Outlook Web App. No entanto, o idioma do plano de discagem deve oferecer suporte a visualização da caixa postal e o pacote de idiomas de Unificação de MENSAGENS para o idioma deve ser instalado.

Embora configurações de visualização da caixa postal são as mesmas, se um usuário estiver usando Outlook 2010 ou uma versão posterior ou Outlook Web App, eles vai acessá-las de forma diferente:

**Outlook Web App**

Para acessar as configurações de visualização da caixa postal no Outlook Web App, os usuários clique em **configurações** \> **telefone** \> **caixa postal**. Na página **caixa postal**, as configurações estão disponíveis em **visualização da caixa postal**.

Por padrão, as duas opções de visualização da caixa postal estão disponíveis quando um usuário está habilitado para Unificação de mensagens. Se UM plano de discagem está configurado para usar um pacote de idiomas de Unificação de MENSAGENS que oferece suporte à visualização da caixa postal, Unificação de mensagens criará voz visualizações de email para usuários quando:

  - Um chamador deixar uma mensagem de voz, porque ele não atender o telefone dela.

  - Um usuário habilitado entra no Outlook Voice Access e registra uma mensagem de voz para um ou mais destinatários.

Quando deixa um chamador uma mensagem de voz e **incluir o texto de visualização às mensagens de voz que eu recebo** for selecionado, Unificação de mensagens criará uma visualização da caixa postal na mensagem de email, anexe o arquivo de áudio e enviá-la à caixa de correio do destinatário. Talvez você queira desabilitar essa opção se o idioma que está configurado no plano de discagem não inclui o suporte de visualização da caixa postal e você não quer que as visualizações de email de voz nas mensagens de caixa postal.

Quando os usuários fazem logon Outlook Voice Access e eles enviam uma mensagem de voz para outro usuário, querem limpar a caixa de seleção **incluir texto de visualização com mensagens de voz enviadas por meio do Outlook Voice Access**. Por exemplo, eles talvez queira fazer isso se eles podem enviar mensagens de voz em um idioma que não oferece suporte a visualização da caixa postal ou se eles não quiserem incluir a visualização da caixa postal com a mensagem de voz, porque ele é muito longo.

