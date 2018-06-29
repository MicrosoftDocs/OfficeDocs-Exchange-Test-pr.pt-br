---
title: 'Conversão de conteúdo: Exchange 2013 Help'
TOCTitle: Conversão de conteúdo
ms:assetid: bc367eb3-0306-4da9-9a84-4341caef77af
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Bb232174(v=EXCHG.150)
ms:contentKeyID: 50486500
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Conversão de conteúdo

 

_**Aplica-se a:**Exchange Server 2013_

_**Tópico modificado em:**2016-12-09_

*Conversão de conteúdo* é o processo de formatação corretamente uma mensagem para cada destinatário. A decisão de realizar a conversão de conteúdo em uma mensagem depende do destino e o formato da mensagem que estão sendo processada. No Microsoft Exchange Server 2013, há dois tipos diferentes de conversão de conteúdo:

  - **Conversão de mensagem para destinatários externos**   Esse tipo de conversão de conteúdo inclui as opções de conversão de TNEF Transport Neutral Encapsulation Format () e as opções para destinatários externos de codificação de mensagem. Mensagens enviadas a destinatários dentro da organização do Exchange não exigem esse tipo de conversão de conteúdo. Esse tipo de conversão de conteúdo é manipulado pelo categorizador no serviço de transporte no servidor de caixa de correio. Categorização em cada mensagem acontece depois que uma mensagem que acabou de chegar é colocada na fila de envio. Além de resolução de destinatário e resolução de roteamento, a conversão de conteúdo é executado na mensagem antes que a mensagem é colocada em uma fila de entrega. Se uma única mensagem contiver vários destinatários, o categorizador determina a codificação apropriado para cada destinatário da mensagem. Rastreamento de conversão de conteúdo não captura quaisquer falhas de conversão de conteúdo que o categorizador encontra à medida que ele converte as mensagens enviadas a destinatários externos.

  - **Conversão MAPI para destinatários internos**   Esse tipo de conversão de conteúdo é manipulado pelo serviço de transporte de caixa de correio. O serviço de transporte de caixa de correio existe nos servidores de caixa de correio para transmitir mensagens entre os bancos de dados de caixa de correio no servidor local e o serviço de transporte em servidores de caixa de correio. Especificamente, o serviço de envio de transporte de caixa de correio transmite mensagens de saída do remetente para serviço de transporte em um servidor de caixa de correio. O serviço de entrega de transporte de caixa de correio transmite mensagens do serviço de transporte em um servidor de caixa de correio para a caixa de entrada do destinatário. O serviço de envio de transporte de caixa de correio converte todas as mensagens enviadas de MAPI e o serviço de entrega de transporte de caixa de correio converte todas as mensagens recebidas em MAPI. Rastreamento de conversão de conteúdo captura essas falhas de conversão de MAPI. Para obter mais informações, consulte [Rastreamento de conversão de conteúdo](content-conversion-tracing-exchange-2013-help.md).

Este tópico explica as opções de conversão de mensagem para destinatários externos.

**Sumário**

Formatos de mensagem do Exchange e Outlook

Opções de conversão de conteúdo para destinatários externos

Noções básicas sobre a estrutura das mensagens de email

## Formatos de mensagens do Exchange e Outlook

A lista a seguir descreve os formatos de mensagem básica disponíveis no Exchange e o Microsoft Outlook:

  - **Texto sem formatação**   Uma mensagem de texto sem formatação usa apenas US-ASCII texto conforme descrito em RFC 2822. A mensagem não pode conter diferentes fontes ou outra formatação de texto. Dois formatos a seguir podem ser usados para uma mensagem de texto não criptografado:
    
      - Os cabeçalhos de mensagem e o corpo da mensagem são compostas de texto US-ASCII. Anexos devem ser codificados usando *Uuencode*. UUENCODE representa a codificação Unix-to-Unix e define um algoritmo de codificação para armazenar os anexos binários utilizando caracteres de texto US-ASCII no corpo de uma mensagem de email.
    
      - A mensagem é codificado em MIME com um valor de tipo de conteúdo de texto/simples e um valor de codificação de transferência de conteúdo de bit 7 para as partes de texto de uma mensagem com várias partes. Quaisquer anexos de mensagens são codificados usando a codificação Quoted-printable ou Base64. Por padrão, quando você redigir e envia uma mensagem de texto sem formatação no Outlook, a mensagem é codificado em MIME com um valor de tipo de conteúdo de texto/simples.

  - **HTML**   Uma mensagem HTML aceita formatação de texto, imagens de plano de fundo, tabelas, marcadores e outros elementos gráficos. Por definição, uma mensagem formatado em HTML deve ser codificado em MIME para preservar a formatação de elementos.

  - **Formato rich text (RTF)**   O RTF aceita formatação de texto e outros elementos gráficos. RTF é sinônimo de TNEF. Arquivos RTF e TNEF podem ser usado forma intercambiável. O formato de mensagem rich text é completamente diferente do formato de documento de rich text disponível no Microsoft Word.
    
    Somente o Outlook e alguns outros clientes de email MAPI entendem as mensagens RTF.

  - **TNEF**   O Transport Neutral Encapsulation Format é um formato de específicas da Microsoft para encapsular propriedades de mensagem MAPI. Uma mensagem TNEF contém uma versão de texto sem formatação da mensagem e um anexo que empacota versão formatada da mensagem original. Normalmente, esse anexo é denominado Winmail. O anexo Winmail. dat inclui as seguintes informações:
    
      - Versão formatada original da mensagem, incluindo, por exemplo, fontes, tamanhos de texto e cores de texto
    
      - Objetos OLE, incluindo, por exemplo, incorporado imagens ou documentos incorporados do Microsoft Office
    
      - Recursos especiais do Outlook, incluindo, por exemplo, formulários personalizados, botões de votação ou solicitações de reunião
    
      - Anexos de mensagem regular que estavam na mensagem original
    
    A mensagem de texto sem formatação resultante pode ser representada nos seguintes formatos:
    
      - Mensagem RFC 2822 compatível com composta apenas a texto US-ASCII com um anexo Winmail. dat codificado em Uuencode
    
      - Mensagem com várias partes codificado em MIME que tem um anexo Winmail. dat
    
    Um cliente de email compatível com MAPI que entenda totalmente o TNEF, como o Outlook, processa os anexos Winmail. dat e exibe o conteúdo da mensagem original sem precisar exibir os anexos Winmail. Um cliente de email que não entende TNEF pode apresentar uma mensagem TNEF em qualquer uma das seguintes maneiras:
    
      - A versão de texto sem formatação da mensagem é exibida e a mensagem contém um anexo com o nome Winmail.dat, Win.dat ou algum outro nome genérico como Att*nnnnn*.dat ou Att*nnnnn*.eml onde o espaço reservado *nnnnn* representa um número aleatório.
    
      - A versão do texto sem formatação da mensagem é exibida. O anexo TNEF é ignorado ou removido. O resultado é uma mensagem de texto sem formatação.
    
      - Servidores que entendem TNEF de mensagens podem ser configurado para remover anexos TNEF de mensagens de entrada. O resultado é uma mensagem de texto sem formatação. Além disso, alguns clientes de email como o Microsoft Outlook Express talvez não entende o TNEF, mas reconhecer e ignorar anexos TNEF. O resultado é uma mensagem de texto sem formatação.
    
    Existem utilitários de terceiros que podem ajudar a converter os anexos Winmail.dat
    
    TNEF é compreendido por todas as versões do Exchange desde Exchange Server versão 5.5.

  - **Resumo Transport Neutral Encapsulation Format (STNEF)**   STNEF é equivalente ao TNEF. No entanto, as mensagens STNEF são codificadas diferente mensagens TNEF. Especificamente, mensagens STNEF são sempre codificado em MIME e sempre têm um valor de codificação de transferência de conteúdo de binário. Portanto, não há nenhuma representação em texto sem formatação da mensagem e houver um anexo Winmail. dat distinto, contido no corpo da mensagem. Toda a mensagem é representada por meio de apenas dados binários. Mensagens que têm um valor de codificação de transferência de conteúdo de binário só podem ser transferidas entre os servidores de mensagens SMTP que suportam e anunciam o BINARYMIME e SMTP REUNIR as extensões, como definido no RFC 3030. As mensagens sempre são transferidas entre SMTP messaging utilizando-se o comando BDAT, em vez do comando de DADOS padrão.
    
    STNEF é compreendido por todas as versões do Exchange desde Exchange 2000. STNEF será usado automaticamente para todas as mensagens transferidas entre os servidores do Exchange na organização desde o modo nativo Exchange Server 2003.
    
    Exchange nunca envia mensagens STNEF a destinatários externos. Mensagens TNEF só podem ser enviadas para destinatários fora da organização do Exchange.

Voltar ao início

## Opções de conversão de conteúdo para destinatários externos

As opções de conversão de conteúdo que podem ser definidos em uma organização do Exchange para destinatários externos podem ser descritas nas seguintes categorias:

  - **Opções de conversão de TNEF**   Essas opções de conversão especificam se TNEF deve ser preservada ou removida das mensagens que deixam a organização do Exchange.

  - **Opções de codificação de mensagem**   Essas opções especificam as opções de codificação de mensagem, como MIME e conjuntos de caracteres não MIME, a codificação de mensagem e formatos de anexo.

Estas opções de codificação e de conversão são independentes uma da outra. Por exemplo, se mensagens TNEF podem deixar a organização do Exchange não relacionada à configurações de codificação MIME ou configurações de codificação de texto não criptografado dessas mensagens.

Você pode especificar o conversão de conteúdo em vários níveis da organização do Exchange, conforme descrito na lista a seguir:

  - **Configurações de domínio remoto**   Domínios remotos definem as configurações para transferências de mensagem de saída entre a organização do Exchange e os domínios externos.. Mesmo se você não criar entradas de domínio remoto para domínios específicos, há um domínio remoto predefinido denominado padrão que se aplica a todos os espaços de endereço remoto (\*).

  - **Configurações de contato de email e usuário de email**   Usuários de email e contatos de email são semelhantes, pois ambos têm endereços de email externo e contêm informações sobre pessoas de fora da organização do Exchange. A principal diferença é que os usuários de email têm contas que podem ser usadas para fazer logon nos recursos de acesso e o domínio do Active Directory na organização.

  - **Configurações do Outlook**   No Outlook, você pode definir a mensagem formatação e codificação opções descritas na lista a seguir:
    
      - **Formato da mensagem**   Você pode definir o formato de mensagem padrão para todas as mensagens. Você pode substituir o formato padrão da mensagem ao escrever uma mensagem específica.
    
      - **Formato da mensagem de Internet**   Você pode controlar se as mensagens TNEF serão enviadas aos destinatários de remotos ou convertidos primeiro em um formato mais compatível. Você também pode especificar várias opções de codificação de mensagem para mensagens enviadas a destinatários remotos. Essas configurações não se aplicam às mensagens enviadas aos destinatários na organização do Exchange.
    
      - **Formato de mensagem de destinatário da Internet**   Você pode controlar se mensagens TNEF enviadas a destinatários específicos ou convertidos primeiro em um formato mais compatível. Você pode definir opções de conversão para contatos específicos na sua pasta de contatos e você pode substituir as opções de conversão para um destinatário específico no campo para, Cc ou Cco fields como redigir uma mensagem. Essas opções de conversão não estão disponíveis para os destinatários na organização do Exchange.
    
      - **Opções de codificação de mensagem de destinatário da Internet**   Você pode controlar o MIME ou opções de codificação para contatos específicos em sua pasta de contatos e você podem substituir a conversão em texto sem formatação opções para um destinatário específico em para, Cc ou Cco, em campos como redigir uma mensagem. Essas opções de conversão não estão disponíveis para os destinatários na organização do Exchange.
    
      - **Opções Internacionais**   Você pode controlar os conjuntos de caracteres que são usados em mensagens.

## Opções de conversão de TNEF

Você pode especificar as opções de conversão de TNEF nos seguintes níveis:

  - Configurações de domínio remoto

  - Configurações de contato de email e usuário de email

  - Configurações do Outlook, incluindo:
    
      - Formato de mensagem
    
      - Formato de mensagem da Internet
    
      - Formato de mensagem de destinatário da Internet

## Opções de codificação de mensagem

Você pode especificar as opções nos seguintes níveis de codificação de mensagem:

  - Configurações de domínio remoto

  - Configurações de contato de email e usuário de email

  - Configurações do Outlook, incluindo:
    
      - Formato de mensagem
    
      - Mensagem da Internet
    
      - Formato de mensagem de destinatário da Internet
    
      - Opções de codificação de conjunto de caracteres de mensagem

Para obter informações detalhadas, consulte [Opções de codificação de mensagem](message-encoding-options-exchange-2013-help.md).

Voltar ao início

## Noções básicas sobre a estrutura das mensagens de email

Para entender melhor as opções de conversão de conteúdo para destinatários externos, você precisa compreender a estrutura das mensagens de email. Uma mensagem SMTP é baseada em texto sem formatação de US-ASCII de 7 bits de redigir e enviar mensagens de email. Uma mensagem SMTP padrão consiste nos seguintes elementos:

  - **Envelope da mensagem**   Envelope da mensagem é definido no RFC 2821. Envelope da mensagem contém as informações necessárias para transmitir e entregar a mensagem. Os destinatários veem nunca o envelope da mensagem, porque ele é gerado pelo processo de transmissão de mensagens e não é realmente uma parte do conteúdo da mensagem.

  - **Conteúdo da mensagem**   O conteúdo da mensagem é definido no RFC 2822. O conteúdo da mensagem consiste nos seguintes elementos:
    
      - **Cabeçalho da mensagem**   O cabeçalho da mensagem é uma coleção de campos de cabeçalho. Campos de cabeçalho consistem em nome de um campo, seguido por um caractere de dois-pontos (:), seguido de um corpo de campo e encerradas por um retorno de carro/linha feed combinação de caracteres (CR LF).
        
        Um nome de campo deve ser composto de caracteres de texto US-ASCII imprimíveis, exceto o caractere de dois-pontos (:). Especificamente, os caracteres ASCII que possuem valores de 33 por meio de 57 e 59 por meio de 126 são permitidos.
        
        O corpo de um campo pode ser composto de quaisquer caracteres US-ASCII, exceto o caractere de retorno de carro (CR) e a caractere (LF) de avanço de linha. No entanto, o corpo de um campo pode conter a combinação de caracteres CR/LF quando usado no *cabeçalho dobra*. Dobra de cabeçalho é a separação de um corpo de campo único cabeçalho em várias linhas, conforme descrito na seção 2.2.3 do RFC 2822. Outros requisitos de sintaxe do corpo de campo são descritos nas seções 3 e 4 do RFC 2822.
    
      - **Corpo da mensagem**   O corpo da mensagem é uma coleção de linhas de caracteres de texto US-ASCII que aparece após o cabeçalho da mensagem. O cabeçalho da mensagem e o corpo da mensagem são separados por uma linha em branco que termine com a combinação de caracteres CR/LF. Corpo da mensagem é opcional. Qualquer linha de texto no corpo da mensagem deve ser menor do que 998 caracteres. Os caracteres CR e LF só podem aparecer juntos indicar o final de uma linha.

Quando as mensagens SMTP contêm os elementos que não são de texto US-ASCII sem formatação, a mensagem deve ser codificada para preservar a esses elementos. O padrão de MIME define um método de codificação de conteúdo em mensagens que não seja texto. MIME permite texto em outros conjuntos de caracteres, anexos sem texto, corpos de mensagem com várias partes e campos de cabeçalho em outros conjuntos de caracteres. MIME é definido no RFC 2045, RFC 2046, 2047 RFC, RFC 2048 e RFC 2077. MIME define uma coleção de campos de cabeçalho que especifica os atributos de mensagem adicionais. A tabela a seguir descreve alguns campos de cabeçalho MIME importantes.

### Campos de cabeçalho MIME importantes

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Nome do campo de cabeçalho</th>
<th>Valor padrão</th>
<th>Descrição</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Versão de MIME</p></td>
<td><p>1.0</p></td>
<td><p>Este campo de cabeçalho é o primeiro campo de cabeçalho MIME que aparece em uma mensagem no formato MIME. Esse campo de cabeçalho aparece após os outros campos do cabeçalho de RFC 2822 padrão, mas antes de quaisquer outros campos de cabeçalho MIME. Clientes de email MIME reconhecimento usam esse campo de cabeçalho para identificar uma mensagem MIME codificada. Quando este campo de cabeçalho estiver ausente, os clientes de email MIME reconhecimento identificam a mensagem como texto sem formatação.</p></td>
</tr>
<tr class="even">
<td><p>Tipo de conteúdo</p></td>
<td><p>texto/simples</p></td>
<td><p>Esse campo de cabeçalho identifica o tipo de mídia do conteúdo da mensagem, conforme descrito em RFC 2046. Um tipo de mídia consiste em um tipo, um subtipo e um ou mais parâmetros opcionais, como um parâmetro de <em>charset=</em> que define a codificação de caracteres MIME. Tipos que começam com &quot;x-&quot; não são padrão. Os subtipos que começam com &quot;vnd.&quot; são específicas de fornecedor. O Internet Assigned Numbers Authority (IANA) mantém uma lista de tipos de mídia registrados. Para obter mais informações, consulte <a href="https://www.iana.org/assignments/media-types/">Tipos de mídia MIME</a>.</p>
<p>O tipo de mídia <em>com várias partes</em> permite várias partes de mensagem na mesma mensagem usando seções definidas por diferentes tipos de mídia. Alguns valores de campo de tipo de conteúdo incluem texto/simples, texto/html, com diversas partes/resumida e com diversas partes/alternativa.</p></td>
</tr>
<tr class="odd">
<td><p>Codificação de transferência de conteúdo</p></td>
<td><p>7bit</p></td>
<td><p>Este campo de cabeçalho pode descrevem as seguintes informações sobre uma mensagem:</p>
<ul>
<li><p>O algoritmo de codificação usado para transformar qualquer texto de não-US-ASCII ou dados binários que existe no corpo da mensagem.</p></li>
<li><p>Um indicador que descreve a condição atual do corpo da mensagem.</p></li>
</ul>
<p>Pode haver vários valores do campo de cabeçalho codificação de transferência de conteúdo de uma mensagem MIME. Quando o campo de cabeçalho de codificação de transferência de conteúdo for exibida no cabeçalho da mensagem, ela se aplica a todo o corpo da mensagem. Quando o campo de cabeçalho de codificação de transferência de conteúdo aparece em uma das partes de uma mensagem com várias partes, ele se aplica somente a parte da mensagem.</p>
<p>Quando um algoritmo de codificação é aplicado aos dados do corpo da mensagem, os dados de corpo da mensagem são transformados em texto US-ASCII sem formatação. Essa transformação permite a mensagem se desloque em servidores mais antigos da mensagens SMTP que suportam somente as mensagens em texto US-ASCII. Os valores de campo de cabeçalho de codificação de transferência de conteúdo que indicam que um algoritmo de codificação usado no corpo da mensagem são:</p>
<ul>
<li><p><strong>Quoted-printable</strong>   Esse algoritmo de codificação usa caracteres US-ASCII imprimíveis para codificar os dados de corpo da mensagem. Se o texto da mensagem original é principalmente o texto US-ASCII, codificação Quoted-printable oferece resultados de relativamente legíveis e compacto. Todos os caracteres de texto US-ASCII imprimíveis, exceto o caractere de sinal de igual (=) podem ser representados sem codificação.</p></li>
<li><p><strong>Base64</strong>   Esse algoritmo de codificação baseia-se principalmente na privacidade avançada padrão de email (PEM) definido no RFC 1421. A codificação Base64 usa 64 caracteres alfabeto a codificação de caracteres definidos pela PEM de preenchimento de saída e de algoritmo para codificar os dados de corpo da mensagem. Normalmente, uma mensagem de codificação Base64 é 33% maior do que a mensagem original. A codificação Base64 cria um previsível aumento no tamanho da mensagem e é ideal para dados binários e texto de não-US-ASCII.</p></li>
</ul>
<p>Normalmente, você não verá vários algoritmos de codificação usados na mesma mensagem.</p>
<p>Quando nenhum algoritmo de codificação tiver sido usado no corpo da mensagem, o campo de cabeçalho de codificação de transferência de conteúdo meramente identifica a condição de dados do corpo da mensagem atual. Os seguintes valores de campo de cabeçalho de codificação de transferência de conteúdo indicam que nenhuma algoritmos de codificação foram usados no corpo da mensagem:</p>
<ul>
<li><p><strong>7 bits</strong> esse valor indica que os dados de corpo da mensagem já estão no formato RFC 2822. Especificamente, isso significa que as seguintes condições devem ser verdadeiras:</p>
<ul>
<li><p>Todas as linhas de texto devem ser menor que 998 caracteres de comprimento.</p></li>
<li><p>Todos os caracteres devem ser texto US-ASCII que possuem valores de caracteres de 1 a 127.</p></li>
<li><p>Os caracteres CR e LF só podem ser usados juntos para indicar o final de uma linha de texto.</p></li>
</ul>
<p>O corpo da mensagem inteira pode ser 7 bits ou parte do corpo da mensagem em uma mensagem com diversas partes pode não estar 7 bits. Se a mensagem com diversas partes contém outras partes que possuem quaisquer dados binários ou texto não-US-ASCII, que parte da mensagem deve ser codificada usando os algoritmos de codificação Quoted-printable ou Base64.</p>
<p>Mensagens que têm corpos de 7 bits podem viajar entre servidores de mensagens SMTP usando o comando de DADOS padrão.</p></li>
<li><p><strong>8 bits</strong> esse valor indica que os dados de corpo da mensagem contém caracteres não-US-ASCII. Especificamente, isso significa que as seguintes condições devem ser verdadeiras:</p>
<ul>
<li><p>Todas as linhas de texto devem ser menor que 998 caracteres de comprimento.</p></li>
<li><p>Um ou mais caracteres no corpo da mensagem têm valores maiores que 127.</p></li>
<li><p>Os caracteres CR e LF só podem ser usados juntos para indicar o final de uma linha de texto.</p></li>
</ul>
<p>O corpo da mensagem inteira pode ser 8 bits ou parte do corpo da mensagem em uma mensagem com diversas partes pode não estar 8 bits. Se a mensagem com diversas partes contém outras partes que tenham dados binários, a parte da mensagem deve ser codificada usando os algoritmos de codificação Quoted-printable ou Base64.</p>
<p>Mensagens que têm corpos de 8 bits só podem se encaminhar entre os servidores de mensagens SMTP que suportam a extensão de SMTP 8BITMIME conforme definido no RFC 1652, como servidores que executam Exchange 2000 Server ou versões mais recentes. Especificamente, isso significa que as seguintes condições devem ser verdadeiras:</p>
<ul>
<li><p>A palavra-chave 8BITMIME deve ser anunciada na resposta EHLO do servidor.</p></li>
<li><p>Mensagens ainda são transferidas usando o comando de DADOS padrão do SMTP. No entanto, o CORPO = 8BITMIME parâmetro deve ser adicionado ao final do comando MAIL FROM.</p></li>
</ul></li>
<li><p><strong>Binário</strong>   Esse valor indica que o corpo da mensagem contém dados binários ou texto não-US-ASCII. Especificamente, isso significa que as seguintes condições são verdadeiras:</p>
<ul>
<li><p>Qualquer sequência de caracteres é permitida.</p></li>
<li><p>Não há nenhuma limitação de comprimento de linha.</p></li>
<li><p>Elementos de mensagem binária não exigem a codificação.</p></li>
</ul>
<p>Mensagens que têm corpos binários só podem se encaminhar entre os servidores de mensagens SMTP que suportam a extensão BINARYMIME SMTP, como definido no RFC 3030, como servidores que executam Exchange 2000 Server ou versões mais recentes. Especificamente, isso significa que as seguintes condições devem ser verdadeiras:</p>
<ul>
<li><p>A palavra-chave BINARYMIME deve ser anunciada na resposta EHLO do servidor.</p></li>
<li><p>A extensão BINARYMIME SMTP só pode ser usada com a extensão de FRAGMENTAÇÃO SMTP. <em>Chunking</em> permite corpos de mensagem grande que sejam enviadas em várias partes menores. Reunir também é definida em RFC 3030. A palavra-chave CHUNKING também deve ser anunciada na resposta EHLO do servidor.</p></li>
<li><p>Mensagens são transferidas usando o comando BDAT, em vez do comando de DADOS padrão.</p></li>
<li><p>O parâmetro <em>BODY=BINARYMIME</em> deve ser adicionado ao final do comando MAIL FROM quando a mensagem tiver um corpo da mensagem.</p></li>
</ul></li>
</ul>
<p>Os valores de bit 7, 8 bits e binário nunca coexistir na mesma mensagem com várias partes. Os valores são mutuamente exclusivos. Os valores de Base64 ou Quoted-printable podem aparecer em um bit 7 ou o corpo da mensagem com várias partes de 8 bits, mas nunca no corpo da mensagem de binários. Se um corpo de mensagem com várias partes contiver diferentes partes compostas de 7 bits e de conteúdo de 8 bits, toda a mensagem é classificada como 8 bits. Se um corpo de mensagem com várias partes contiver compostas de 7 bits, 8 bits e conteúdo binário de diferentes partes, toda a mensagem é classificada como binário.</p></td>
</tr>
<tr class="even">
<td><p>Disposição de conteúdo</p></td>
<td><p>Attachment</p></td>
<td><p>Este campo de cabeçalho instrui um cliente de email habilitados em MIME em como ele deve exibir um arquivo anexado e está descrito em RFC 2183. Os valores desse campo podem estar embutida ou anexo. Quando o valor desse campo é embutida, o anexo é exibido no corpo da mensagem. Quando o valor desse campo é um anexo, o arquivo anexado aparece como um anexo regular separado do corpo da mensagem. Outros parâmetros estão disponíveis quando o valor é um anexo, como nome de arquivo, data de criação e tamanho.</p></td>
</tr>
</tbody>
</table>


Voltar ao início

