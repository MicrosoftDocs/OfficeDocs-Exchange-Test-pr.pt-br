---
title: 'Codecs de áudio: Exchange 2013 Help'
TOCTitle: Codecs de áudio
ms:assetid: 6c39d65c-c2d3-4128-aae9-8596602819c3
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Aa998670(v=EXCHG.150)
ms:contentKeyID: 54651973
ms.date: 01/10/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Codecs de áudio

 

_**Aplica-se a:**Exchange Server 2013, Exchange Server 2016_

_**Tópico modificado em:**2016-12-09_

Na Unificação de Mensagens (UM), um codec de áudio é usado para armazenar mensagens de caixa postal. Outro codec é usado entre um gateway VoIP ou Central Privada de Comutação Telefônica (PBX) e o servidor de Caixa de Correio executando o serviço de Unificação de Mensagens do Microsoft Exchange ou o servidor de Acesso para Cliente executando o serviço de Roteador de Chamadas da Unificação de Mensagens do Microsoft Exchange. A Unificação de Mensagens pode usar qualquer dos quatro codecs a seguir para criar e armazenar mensagens de voz:

  - MP3 (padrão)

  - Windows Media Audio (WMA)

  - Group System Mobile (GSM) 06.10

  - G.711 Pulse Code Modulation (PCM) Linear


> [!WARNING]
> Os codecs G.711 (PCMA e PCMU) e o G.723.1 são codecs de VoIP usados entre um gateway de VoIP e os servidores de Caixa de Correio e de Acesso para Cliente.



Parte do planejamento da sua UM envolve escolher o codec de áudio certo com base nas necessidades e requisitos de sua organização. Este tópico discute os codecs de áudio que a UM pode usar e você usá-lo para ajudar você a planejar a implantação da sua UM.

## Codecs

O termo *codec* é uma combinação das palavras "codificação" e "decodificação" e é usado com dados de áudio digitais. Um codec é um programa de software que transforma dados digitais em formato de arquivo de áudio ou formato de streaming de áudio. Codecs são usados para converter um sinal de voz analógico em uma versão digital do sinal de voz. Os codecs podem variar em questões como qualidade do som, largura de banda necessária para usá-los e requisitos de sistema necessários para a codificação.

Dois tipos de codec são usados na Unificação de Mensagens:

  - O codec usado entre o gateway VoIP, IP PBX ou PBX com SIP habilitado e os servidores de Caixa de Correio e Acesso para Cliente ou entre um gateway VoIP e um PBX.

  - O codec era usado para codificar e armazenar mensagens de voz para usuários.

Quando você usa um telefone comum em uma Rede Telefônica Pública Comutada (PSTN), a sua voz é transportada em formato analógico pela linha de telefone. Mas com VoIP, sua voz é convertida em sinais digitais. Esse processo de conversão é conhecido como codificação. A codificação é realizada por um codec. Depois que a voz digitalizada alcançar seu destino, ela deverá ser decodificada de volta ao seu formato analógico original para que a pessoa na outra extremidade da chamada possa ouvir e compreender o chamador.

## Codec VoIP

Na UM, três tipos de codecs podem ser usados entre os gateways VoIP ou IP PBXs e os servidores de Caixa de Correio e Acesso para Cliente

  - G.711 µ-law

  - G.711 A-law

  - G.723.1

G.711 é um padrão que foi desenvolvido para uso com codecs de áudio. Há dois algoritmos principais definidos no padrão para G.711: o algoritmo µ-law, usado na América do Norte e no Japão, e o algoritmo A-law, usado na Europa e em outros países/regiões. O codec de áudio G.723.1 é mais usado em aplicativos VoIP e exige uma licença para ser usado. O G.723.1 tipo de codec de alta qualidade com alta compressão

Um servidor de Caixa de Correio ou Acesso para Cliente e um gateway VoIP ou IP PBX suportados podem ambos oferecer os codecs G.711 e G.723.1. Por padrão, o primeiro codec a ser usado é o G.723.1. Se quiser usar outro codec em vez do G.723.1, entre os servidores de Acesso para Cliente e Caixa de Correio e o gateway VoIP ou o PBX IP, recomendamos que você altere a configuração no gateway VoIP ou no PBX IP. A tabela a seguir resume alguns codecs VoIP comuns.

### Codecs VoIP

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Codec VoIP</th>
<th>Largura de banda (Kbps)</th>
<th>Descrição</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>G.711</p></td>
<td><p>64</p></td>
<td><p>Este codec exige pouco processamento. Ele precisa de pelo menos 128 kbps (quilobits por segundo) para comunicação bidirecional.</p></td>
</tr>
<tr class="even">
<td><p>G.723.1</p></td>
<td><p>5.3/6.3</p></td>
<td><p>Este codec oferece alta compressão com alta qualidade de áudio. Ele exige mais processamento do que o codec G.711. O codec G.723.1 usa largura de banda reduzida mas oferece baixa qualidade de áudio.</p></td>
</tr>
</tbody>
</table>


## Codec de armazenamento de menssagem de voz da UM

Os planos de discagem de Unificação de Mensagens são essenciais para a operação da UM. Por padrão, quando você cria um plano de discagem de UM, o plano de discagem de UM usa o codec de áudio de MP3 para criar e armazenar mensagens de voz. Entretanto, após ter criado o plano de discagem da UM, você pode configurá-lo para usar os codecs de áudio WMA, GSM 06.10 ou G.711 PCM Linear.

Cada codec de áudio apresenta vantagens e desvantagens. O codec de áudio de MP3 foi escolhido como o codec de áudio padrão devido às suas propriedades de compressão e qualidade de som. Os codecs de áudio GSM 06.10 e G.711 PCM Linear foram incluídos como opções disponíveis por causa de sua capacidade de oferecer suporte a outros tipos de sistemas de mensagens.

Ao planejar a UM, você deve equilibrar o tamanho e a qualidade relativa do arquivo de áudio que será criado para mensagens de voz. Em geral, quanto mais alta a taxa de bits de um arquivo de áudio, melhor será a qualidade. Você deve considerar também se o arquivo de áudio está compactado. A tabela a seguir exibe a taxa de bits da amostra (bit/seg) e as propriedades de compressão para cada codec de áudio na UM.

### Codecs de armazenamento de mensagens de voz de UM padrão

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Codec de armazenamento de mensagens de voz</th>
<th>Bits</th>
<th>Arquivo compactado?</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>MP3</p></td>
<td><p>16 bits</p></td>
<td><p>Sim</p></td>
</tr>
<tr class="even">
<td><p>WMA</p></td>
<td><p>16 bits</p></td>
<td><p>Sim</p></td>
</tr>
<tr class="odd">
<td><p>G.711 PCM</p></td>
<td><p>16 bits</p></td>
<td><p>Não</p></td>
</tr>
<tr class="even">
<td><p>GSM 06.10</p></td>
<td><p>8 bits</p></td>
<td><p>Sim</p></td>
</tr>
</tbody>
</table>


Na UM, o tipo de arquivo criado para uma menssagem de voz depende do codec de áudio que é usado para criar um arquivo de áudio de mensagem de voz. O codec de áudio de MP3 cria arquivos de áudio .mp3, o codec de áudio de WMA cria arquivos de áudio .wma e os codecs de áudio GSM 06.10 e G.711 PCM Linear criam arquivos de áudio .wav. Todos esses arquivos de áudio são enviados junto com uma mensagem de email ao destinatário da mensagem de voz.

Normalmente, mas não sempre, a codificação e a decodificação dos dados digitais também envolve compactação ou descompactação. A compactação de áudio é uma forma de compactação de dados que reduz o tamanho dos arquivos de dados de áudio. O algoritmo de compactação de áudio usado pelo codec de áudio compacta os arquivos de áudio .wma ou .wav. Na UM, o tipo de algoritmo de compressão de áudio usado é baseado no tipo de codec de áudio escolhido nas propriedades do plano de discagem de UM. Depois que o arquivo de áudio é criado e compactado, ele é anexado à mensagem de voz.

Algumas vezes, as informações dos dados digitais são perdidas durante a compactação e descompactação. Quanto maior a compactação usada para compactar o arquivo de áudio, maior será a perda de informações durante a conversão. No entanto, será usado menos espaço em disco porque o tamanho do arquivo de áudio será reduzido. Por outro lado, quanto menor a compactação, menor a perda de informações. No entanto, será usado mais espaço em disco devido ao aumento de tamanho de cada arquivo de áudio.

Banda larga RTAudio ou áudio de alta fidelidade para gravar mensagens de voz está também disponível como um codec de áudio. Entretanto, o áudio de alta fidelidade que usa RTAudio é disponibilizado apenas após você ter integrado com sucesso a Unificação de Menssagens com o [Servidor Microsoft Lync](https://go.microsoft.com/fwlink/p/?linkid=202010). Para habilitar o RTAudio como o codec de transferência, banda larga ou estreita, o plano de discagem de UM deve ser configurado como um plano de discagem do tipo URI do protocolo SIP e você deve configurar o codec de atendimento de chamada no plano de discagem para MP3 ou WMA para habilitar o áudio em banda larga (16Khz).


> [!IMPORTANT]
> O RTAudio não está disponível em ambientes onde o Servidor Lync não estiver implantado. Isto se deve ao fato de que em ambientes que não integram o Servidor Lync, o plano de discagem será definido para Extensão de Telefone ou E.164 e não para SIP URI.



Há dois fluxos de mídia para cada chamada de entrada: entrada para um servidor de Acesso para Cliente e saída para um servidor de Caixa de Correio. Quando o tipo de plano de discagem é configurado para SIP URI e o codec de atendimento de chamada é configurado para MP3 ou WMA, um servidor de Acesso para Cliente tenta escolher o codec VoIP de RTAudio para o fluxo de mídia de entrada. Se a negociação for bem sucedida, o codec RTAudio para o fluxo de entrada será usado para chamadas de atendimento de chamadas ou chamadas originadas de um cliente ou servidor Lync.


> [!TIP]
> Chamadas realizadas usando o recurso Tocar no Telefone não usarão o codec RTAudio. O fluxo de entrada de chamadas realizadas usando o recurso Tocar no Telefone usará o codec G.711 ou G.723.1.



Quando o codec RTAudio é usado, a mensagem de voz que é gravada será gravada com alta fidelidade e será armazenada como um arquivo de áudio que possui uma extensão .mp3 ou .wma dependendo de como o plano de discagem estiver configurado. Quando a mensagem de voz é tocada para o usuário no Outlook ou no Outlook Web App eles ouvirão a mensagem de voz com áudio de alta fidelidade. Se a negociação for malsucedida, o codec G.711 ou G.723.1 será usado. Os codecs G.711 e G.723.1 são codecs de banda estreita. Quando são usados como codec VoIP, a mensagem de voz é gravada e armazenada como um arquivo de áudio de banda estreita que possui uma extensão .mp3 ou .wma.

O fluxo de mídia de saída sempre será negociado usando o codec G.711 ou G.723.1. Isso significa que os chamadores sempre ouvirão áudio de banda estreita pelo telefone. Isto também se aplica a situações nas quais uma chamada é feita usando o Servidor Microsoft Lync 2010 ou posterior.

O formato de áudio e o codec que os servidores de Caixa de Correio usam para armazenar o áudio em mensagens de voz dependem não apenas do codec do áudio que é configurado no plano de discagem, mas também da taxa de bits do áudio que a UM negocia com um par SIP. Se o seu ambiente inclui o Servidor Lync ou terminais SIP, um servidor de Caixa de Correio também negocia o codec de áudio para usar um par SIP. Por exemplo, quando o RTAudio de banda larga é negociado como o codec de transferência, um servidor de Caixa de Correio usará então o formato MP3 ou WMA 9.2 de 32 Kbps ao criar menssagens de voz, depdendendo da configuração do plano de discagem. A tabela a seguir mostra a relação entre o codec de áudio de armazenamento de mensagem de voz e o codec de áudio de transmissão ou VoIP usado.

### Relação entre o codec de áudio de armazenamento e o codec de áudio de transmissão ou VoIP

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Codec de áudio configurado em um plano de discagem da UM</th>
<th>Codec de transmissão ou VoIP (banda estreita) - G.723, G.711 ou RTAudio (8 KHz)</th>
<th>Codec de transmissão ou VoIP (banda ampla) - RTAudio (16 KHz)</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>G0.711</p></td>
<td><p>G0.711</p></td>
<td><p>Não se aplica. Um servidor de Caixa de Correio ou de Acesso para Cliente não negocia áudio de banda larga se o plano de discagem estiver definido para G.711.</p></td>
</tr>
<tr class="even">
<td><p>WMA</p></td>
<td><p>WMA 9 Voice</p></td>
<td><p>WMA 9.2</p></td>
</tr>
<tr class="odd">
<td><p>GSM</p></td>
<td><p>GSM 6.10</p></td>
<td><p>Não se aplica. Uma Caixa de Correio ou Acesso para Cliente não negocia áudio de banda larga se o plano de discagem estiver configurado para GSM.</p></td>
</tr>
<tr class="even">
<td><p>MP3</p></td>
<td><p>MP3 (16 Kbps)</p></td>
<td><p>MP3 (32 Kbps)</p></td>
</tr>
</tbody>
</table>


Codecs

## Dimensionamento da mensagem de UM.

Você pode configurar a Unificação de Mensagens para usar um destes quatro codecs de áudio para criar mensagens de voz: MP3, WMA, GSM 06.10 e G.711 PCM Linear. Por padrão, o formato MP3 é selecionado.

O codec de áudio WMA é sempre armazenado no formato Windows Media, e o anexo é um arquivo que tem uma extensão de nome de arquivo .wma. Arquivos de áudio codificados com o codec de áudio GSM ou G.711 PCM Linear são sempre armazenados em formato RIFF/WAV, e o anexo é um arquivo que tem uma extensão de nome de arquivo .wav.

O tamanho das mensagens de voz de UM dependem do tamanho do anexo que contém os dados de voz. Por sua vez, o tamanho do anexo depende dos seguintes fatores:

  - A duração da gravação da mensagem de voz

  - O codec de áudio usado

  - O formato de armazenamento do arquivo de áudio

A figura a seguir mostra como o tamanho do arquivo de áudio depende da duração da gravação da mensagem de voz para os três codecs de áudio que você pode usar na UM.


> [!TIP]
> Nesta figura, a duração média de uma mensagem de voz de atendimento de chamadas é de aproximadamente 30 segundos.



**Tamanho do arquivo de áudio**

![UM\_Message\_Sizing](images/Aa998670.76ca4891-450f-4ffd-9493-aac8d0d23a5d(EXCHG.150).gif "UM_Message_Sizing")

## MP3

Por padrão, o formato MP3 está selecionado e é o formato de arquivo de áudio padrão para mensagens de caixa postal. O formato MP3 é um formato de arquivo de áudio comum usado para reduzir significativamente o tamanho do arquivo de áudio e é mais usado por dispositivos de áudio pessoais ou players de MP3. MP3 é um tipo de codec de áudio que funciona em várias plataformas e é usado para compatibilidade com muitos dispositivos e telefones celulares, assim como diversos sistemas operacionais de computador.

## WMA

WMA é o codec de áudio com maior taxa de compactação dos três tipos de codec. A compactação é de aproximadamente 11.000 bytes para cada 10 segundos de áudio. Entretanto, o formato do arquivo .wma tem uma seção de cabeçalho muito maior do que o formato de arquivo .wav. A seção de cabeçalho do arquivo .wma é de aproximadamente 7 quilobytes (KB), embora a seção de cabeçalho do arquivo .wav seja de menos de 100 bytes. Embora as gravações de áudio WMA sejam gravadas por mais de 15 segundos, ficam menores do que as gravações de áudio GSM. Portanto, para os menores arquivos de áudio, mas de alta qualidade, use o codec de áudio WMA.


> [!TIP]
> Se usar notificações por push na implantação local do OWA para Dispositivos, você não poderá usar o formato WMA. OWA para Dispositivos dá suporte apenas ao formato de arquivo MP3.



## G.711 PCM Linear

O codec de áudio G.711 PCM Linear cria arquivos de áudio .wav que não são compactados. Por essa razão, os arquivos de áudio .wav do G.711 PCM Linear ocupam mais espaço, seja qual for a duração, quando comparados com os codecs de áudio GSM e WMA. Arquivos de áudio G.711 PCM Linear .wav ocupam um pouco mais de 160.000 bytes para cada 10 segundos de áudio. Os arquivos de áudio .wav do G.711 PCM Linear possuem a maior qualidade de áudio dos três codecs de áudio usados pela UM. Entretanto, a qualidade dos arquivos de áudio semelhantes criados usando os codecs de áudio WMA e GSM é aceitável para a maioria dos usuários que ouvem as mensagens de voz.

## GSM

O codec de áudio GSM cria arquivos de áudio .wav que são compactados. Arquivos de áudio GSM .wav ocupam um pouco mais de 16.000 bytes para cada 10 segundos de áudio. Entretanto, GSM cria um arquivo de áudio maior do que o arquivo de áudio criado pelo codec de áudio WMA. Por essa razão, ao considerar a qualidade da mensagem de voz e o tamanho, talvez essa não seja a melhor opção.

Codecs

