---
title: 'Saudações e prompts de idiomas de Unificação de MENSAGENS: Exchange 2013 Help'
TOCTitle: Saudações e prompts de idiomas de Unificação de MENSAGENS
ms:assetid: d48df962-9669-420b-838f-44bfe1012e2f
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Bb124728(v=EXCHG.150)
ms:contentKeyID: 50486714
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Saudações e prompts de idiomas de Unificação de MENSAGENS

 

_**Aplica-se a:**Exchange Server 2013, Exchange Server 2016_

_**Tópico modificado em:**2016-12-09_

Você pode instalar e configurar os pacotes de idiomas para oferecer suporte a vários idiomas em ambientes de Unificação de mensagens (UM).

Os pacotes de idioma de UM permitem aos chamadores e usuários do Outlook Voice Access interagir com o sistema de caixa postal em vários idiomas. Depois de instalar um idioma adicional em um servidor de Caixa de Correio, os chamadores e os usuários do Outlook Voice Access poderão ouvir as mensagens de email e interagir com o sistema de caixa postal nesse idioma.

Há vários componentes principais que se baseiam nos pacotes de idiomas de Unificação de MENSAGENS para permitir que usuários e os chamadores efetivamente interagir com o Unified Messaging em vários idiomas. Cada pacote de idiomas de Unificação de MENSAGENS inclui um mecanismo de fala (TTS), o pré-gravado solicita e suporte para reconhecimento automático de fala (ASR) e a visualização da caixa postal de um idioma específico. Este tópico discute os pacotes de idiomas de Unificação de MENSAGENS, os componentes de Unificação de MENSAGENS que usam os pacotes de idiomas de Unificação de MENSAGENS e pacotes de idiomas do como UM — depois que eles instalados — pode ser usado para configurar planos de discagem de Unificação de MENSAGENS e atendedores automáticos para usar outros idiomas.

Exchange Pacotes de idioma do Unified Messaging são específicos da versão e específicos de plataforma. Desde o Exchange Server 2007, têm sido várias versões de pacotes de idiomas de Unificação de MENSAGENS, incluindo a versão RTM do Exchange 2007, Exchange 2007 SP1, SP2 e SP3, a versão RTM do Exchange Server 2010, Exchange 2010 SP1 e SP2 e Exchange 2013. Para algumas dessas versões, downloads de 32 bits e 64 bits estão disponíveis, mas para outras versões downloads de 64 bits só estão disponíveis.

É muito importante que você instale a versão correta e a plataforma dos pacotes de idioma de Unificação de MENSAGENS em um servidor de caixa de correio. Não instale pacotes de idiomas de Unificação de MENSAGENS em um servidor de caixa de correio que está executando uma versão anterior do Exchange ou que foi projetada para uma plataforma de 32 bits.

**Sumário**

Visão geral dos pacotes de idiomas de Unificação de MENSAGENS

Recursos e componentes de idioma de Unificação de MENSAGENS

Visualização da caixa postal

Idiomas do Unified Messaging

Pacotes de idioma do Unified Messaging

Idiomas de plano de discagem de UM

Idiomas de Atendedor de automático de Unificação de MENSAGENS

Processo de seleção de idioma do cliente

## Visão geral dos pacotes de idiomas de Unificação de MENSAGENS

Pacotes de idioma do Unified Messaging permitem que um servidor de caixa de correio para falar idiomas adicionais aos chamadores e reconhecer outros idiomas quando os chamadores usam ASR ou mensagens de voz são transcrita. Pacotes de idioma de Unificação de MENSAGENS contenham:

  - Avisar pré-gravado no idioma do pacote de idiomas de Unificação de MENSAGENS. Por exemplo, "depois do tom, por favor, registre sua mensagem. Quando terminar a gravação, desligar, ou pressione a tecla \# para obter mais opções."

  - Arquivos de gramática no idioma do pacote de idiomas de Unificação de MENSAGENS que são usados por um servidor de caixa de correio para pesquisar os nomes de dado usuários no diretório.

  - Conversão de texto em fala (TTS) para que conteúdo (email, calendário, informações de contato, etc.) pode ser lidas aos chamadores no idioma do pacote de idiomas de Unificação de MENSAGENS.

  - Suporte para reconhecimento automático de fala, que permite que os chamadores interagir com a Unificação de MENSAGENS usando a interface de usuário de voz (VUI) no idioma do pacote de idiomas de Unificação de MENSAGENS.

  - Suporte para visualização da caixa postal, que permite aos usuários ler a transcrição da voz mensagens de email em um idioma específico de dentro de um cliente de email com suporte, como Outlook ou Outlook Web App.

Pacotes de idiomas de Unificação de MENSAGENS incluem pré-gravado prompts, suporte de conversão de TTS para um idioma específico e em alguns casos, o suporte para ASR. Em ambientes de vários idiomas, você talvez seja necessário instalar pacotes de idiomas de Unificação de MENSAGENS adicionais, pois alguns chamadores preferem ser solicitado em outro idioma ou porque recebem email em mais de um idioma. Você deve instalar vários pacotes de idiomas de Unificação de MENSAGENS para oferecer suporte a capacidade do servidor de caixa de correio para ler uma mensagem de email que contém mais de um idioma, pois o sistema de conversão de TTS deve ser instruído o idioma a ser selecione baseada no texto da mensagem a ser lido. Se o pacote de idiomas de Unificação de mensagens não tenha sido instalado, a mensagem de email será ilógico e incoerentes, quando ele é lido volta para o usuário. Instalando o pacote de idioma apropriado habilita o mecanismo TTS ler itens de email e calendário ao usuário Outlook Voice Access usando o idioma correto e também fornece prompts de pré-gravado específicos de idioma para a Unificação de mensagens. Em alguns casos, também podem oferecer suporte a ASR.


> [!TIP]
> O mecanismo de TTS converte o texto em fala, mas ele não converte fala ao texto. Habilitado os usuários podem enviar uma mensagem de email que tenha um arquivo de voz anexado para outro usuário. No entanto, eles não podem criar e enviar uma mensagem de email baseado em texto para outro usuário.



Ao instalar um pacote de idiomas, o programa de instalação faz o seguinte:

1.  Cópias solicita que o idioma que serão usadas para configurar UM planos de discagem e atendedores automáticos.

2.  Permite que o mecanismo TTS ler mensagens quando os usuários do Voice Access Outlook acessam suas caixas de entrada.

3.  Habilita a ASR para planos de discagem de Unificação de MENSAGENS habilitado para fala e atendedores automáticos de para o idioma instalado.

4.  Permite a visualização da caixa postal para clientes em outros idiomas.

Você pode adicionar os pacotes de idiomas de Unificação de MENSAGENS usando o comando **Setup.exe** ou executando o programa de instalação do *\<UMLanguagePack\>*.exe depois de baixar o pacote de idiomas de Unificação de MENSAGENS do [Exchange Server 2013 UM pacotes de idiomas](https://go.microsoft.com/fwlink/p/?linkid=266542). No entanto, você precisará usar o comando Setup.exe para remover um pacote de idiomas de Unificação de MENSAGENS. Não há nenhum cmdlet do Shell de gerenciamento de Exchange que você pode usar para adicionar ou remover idiomas de um servidor de caixa de correio. Para obter mais informações sobre como instalar um pacote de idiomas de Unificação de MENSAGENS, consulte [Instalar um pacote de idiomas para UM](install-a-um-language-pack-exchange-2013-help.md). Para obter mais informações sobre como remover um pacote de idiomas de Unificação de MENSAGENS, consulte [Remover um pacote de idiomas de Unificação de mensagens](remove-a-um-language-pack-exchange-2013-help.md).


> [!TIP]
> Por padrão, quando você instala um servidor de caixa de correio, o pacote de idiomas inglês dos Estados Unidos (en-US) é instalado. Ele não pode ser removido, a menos que você remova o servidor de caixa de correio do computador.



Voltar ao início

A tabela a seguir lista os pacotes de idiomas de Unificação de mensagens que estão atualmente disponíveis. Ele também lista o nome do arquivo de instalação para cada pacote de idiomas de Unificação de MENSAGENS e a identificação da cultura do idioma de Unificação de MENSAGENS.

### Nomes de arquivo instalação do pacote de idioma Unificação de MENSAGENS e IDs de cultura

<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>Idioma</th>
<th>País/Região</th>
<th>Identificação da cultura</th>
<th>Nome do arquivo de instalação</th>
<th>Disponibilidade</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Catalão</p></td>
<td><p>Espanha</p></td>
<td><p>ca-ES</p></td>
<td><p>UMLanguagePack. CA-ES</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=266542">Disponível para download</a></p></td>
</tr>
<tr class="even">
<td><p>Chinês (Hong Kong)</p></td>
<td><p>China</p></td>
<td><p>zh-HK</p></td>
<td><p>UMLanguagePack. zh-HK</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=266542">Disponível para download</a></p></td>
</tr>
<tr class="odd">
<td><p>Chinês (simplificado)</p></td>
<td><p>China</p></td>
<td><p>zh-CHS</p></td>
<td><p>UMLanguagePack.zh-CN</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=266542">Disponível para download</a></p></td>
</tr>
<tr class="even">
<td><p>Chinês (tradicional)</p></td>
<td><p>Taiwan</p></td>
<td><p>zh-TW</p></td>
<td><p>UMLanguagePack.zh-TW</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=266542">Disponível para download</a></p></td>
</tr>
<tr class="odd">
<td><p>Dinamarquês</p></td>
<td><p>Dinamarca</p></td>
<td><p>da-DK</p></td>
<td><p>UMLanguagePack.da-DK</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=266542">Disponível para download</a></p></td>
</tr>
<tr class="even">
<td><p>Holandês</p></td>
<td><p>Países Baixos</p></td>
<td><p>nl-NL</p></td>
<td><p>UMLanguagePack.nl-NL</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=266542">Disponível para download</a></p></td>
</tr>
<tr class="odd">
<td><p>Inglês</p></td>
<td><p>Austrália</p></td>
<td><p>en-AU</p></td>
<td><p>UMLanguagePack.en-AU</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=266542">Disponível para download</a></p></td>
</tr>
<tr class="even">
<td><p>Inglês</p></td>
<td><p>Canadá</p></td>
<td><p>en-CA</p></td>
<td><p>UMLanguagePack. en-CA</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=266542">Disponível para download</a></p></td>
</tr>
<tr class="odd">
<td><p>Inglês</p></td>
<td><p>Índia</p></td>
<td><p>en-IN</p></td>
<td><p>UMLanguagePack. en-IN</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=266542">Disponível para download</a></p></td>
</tr>
<tr class="even">
<td><p>Inglês</p></td>
<td><p>Reino Unido</p></td>
<td><p>en-GB</p></td>
<td><p>UMLanguagePack.en-GB</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=266542">Disponível para download</a></p></td>
</tr>
<tr class="odd">
<td><p>Inglês</p></td>
<td><p>Estados Unidos</p></td>
<td><p>en-US</p></td>
<td><p>Incluído com a instalação de um servidor de caixa de correio</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=266542">Disponível para download</a></p></td>
</tr>
<tr class="even">
<td><p>Finlandês</p></td>
<td><p>Finlândia</p></td>
<td><p>Fi-Fl</p></td>
<td><p>UMLanguagePack.fi-Fl</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=266542">Disponível para download</a></p></td>
</tr>
<tr class="odd">
<td><p>Francês</p></td>
<td><p>Canadá</p></td>
<td><p>fr-CA</p></td>
<td><p>UMLanguagePack.fr-CA</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=266542">Disponível para download</a></p></td>
</tr>
<tr class="even">
<td><p>Francês</p></td>
<td><p>França</p></td>
<td><p>fr-FR</p></td>
<td><p>UMLanguagePack.fr-FR</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=266542">Disponível para download</a></p></td>
</tr>
<tr class="odd">
<td><p>Alemão</p></td>
<td><p>Alemanha</p></td>
<td><p>de-DE</p></td>
<td><p>UMLanguagePack.de-DE</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=266542">Disponível para download</a></p></td>
</tr>
<tr class="even">
<td><p>Italiano</p></td>
<td><p>Itália</p></td>
<td><p>it-IT</p></td>
<td><p>UMLanguagePack.it-IT</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=266542">Disponível para download</a></p></td>
</tr>
<tr class="odd">
<td><p>Japonês</p></td>
<td><p>Japão</p></td>
<td><p>ja-JP</p></td>
<td><p>UMLanguagePack.ja-JP</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=266542">Disponível para download</a></p></td>
</tr>
<tr class="even">
<td><p>Coreano</p></td>
<td><p>Coreano</p></td>
<td><p>ko-KR</p></td>
<td><p>UMLanguagePack.ko-KR</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=266542">Disponível para download</a></p></td>
</tr>
<tr class="odd">
<td><p>Norueguês (Bokmål)</p></td>
<td><p>Noruega</p></td>
<td><p>nb-NO</p></td>
<td><p>UMLanguagePack.nb-NO</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=266542">Disponível para download</a></p></td>
</tr>
<tr class="even">
<td><p>Polonês</p></td>
<td><p>Polônia</p></td>
<td><p>pl-PL</p></td>
<td><p>UMLanguagePack.pl-PL</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=266542">Disponível para download</a></p></td>
</tr>
<tr class="odd">
<td><p>Português</p></td>
<td><p>Brasil</p></td>
<td><p>pt-BR</p></td>
<td><p>UMLanguagePack.pt-BR</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=266542">Disponível para download</a></p></td>
</tr>
<tr class="even">
<td><p>Português</p></td>
<td><p>Portugal</p></td>
<td><p>pt-PT</p></td>
<td><p>UMLanguagePack.pt-PT</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=266542">Disponível para download</a></p></td>
</tr>
<tr class="odd">
<td><p>Russo</p></td>
<td><p>Rússia</p></td>
<td><p>ru-RU</p></td>
<td><p>UMLanguagePack. RU-RU</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=266542">Disponível para download</a></p></td>
</tr>
<tr class="even">
<td><p>Espanhol</p></td>
<td><p>Espanha</p></td>
<td><p>es-ES</p></td>
<td><p>UMLanguagePack.es-ES</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=266542">Disponível para download</a></p></td>
</tr>
<tr class="odd">
<td><p>Espanhol</p></td>
<td><p>México</p></td>
<td><p>es-MX</p></td>
<td><p>UMLanguagePack.es-MX</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=266542">Disponível para download</a></p></td>
</tr>
<tr class="even">
<td><p>Sueco</p></td>
<td><p>Suécia</p></td>
<td><p>sv-SE</p></td>
<td><p>UMLanguagePack.sv-SE</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=266542">Disponível para download</a></p></td>
</tr>
</tbody>
</table>


Voltar ao início

## Recursos e componentes de idioma de Unificação de MENSAGENS

Há vários componentes-chave e recursos na Unificação de mensagens que permitem que os usuários e os chamadores para interagir com um sistema de correio de voz de vários idiomas. Para esses componentes e recursos para funcionar corretamente e permitir que os chamadores interagir com o sistema em vários idiomas, os pacotes de idiomas de Unificação de MENSAGENS devem ser instalados corretamente em um servidor de caixa de correio.

## Prompts pré-gravado

A função de servidor de caixa de correio é instalada com um conjunto de arquivos de prompt de áudio do padrão. Esses arquivos de áudio contêm as gravações para menus do Voice Access Outlook, saudação da caixa postal e números que são usados pelo Exchange Unificação de mensagens. Os arquivos de áudio são tocados por um servidor de caixa de correio para chamadores de entrada, internos e externos. Muitos dos arquivos de áudio são prompts padrão que fornecem as informações que eles precisam para percorrer o TUI e a Interface de usuário de voz (VUI) dos usuários da Interface de usuário de telefone (TUI) e Outlook Voice Access. Os prompts estão localizados em \<*Program Files*\> \\Microsoft\\Exchange Server\\V15\\UnifiedMessaging\\Prompts\\ \< idioma \>. Os prompts usados pelo servidor de caixa de correio para ajudar os chamadores para percorrer os menus não devem ser substituídos ou alterados.

Quando um pacote de idioma de Unificação de MENSAGENS adicional é instalado, os prompts pré-gravado para esse idioma também serão instalados. Depois que um pacote de idiomas de Unificação de MENSAGENS estiver instalado, os prompts pré-gravado para esse idioma podem ser usados por planos de discagem de Unificação de MENSAGENS e atendedores automáticos.

## Idiomas TTS

A Unificação de mensagens depende de um mecanismo de fala (TTS). Funcionalidade TTS é fornecida pelo Microsoft serviço Speech Server. O mecanismo de TTS lê e converte o texto escrito em saída audível que pode ser ouvida por um chamador. O mecanismo de TTS lê e converte os seguintes itens na caixa de correio de um usuário:

  - Nomes de assuntos e corpos de mensagem de email e caixa postal

  - Nomes, assuntos, locais e corpos de calendário

  - Nomes de contato pessoais

  - Saudação da caixa postal dos usuários padrão


> [!TIP]
> Depois que um usuário tiver gravado saudação da personalizadas de caixa postal, a versão TTS das saudações de voz não são mais usados.



## Reconhecimento Automático de Fala

Além de TTS, suporte de ASR está incluído na Unificação de mensagens. Funcionalidade de ASR é fornecida pelo Microsoft serviço Speech Server. ASR permite que os chamadores usar comandos de voz para percorrer os menus e interagir com os itens de suas caixas de correio individuais, incluindo mensagens, contatos pessoais e calendário. Suporte de ASR está incluído com cada pacote de idiomas.

Voltar ao início

## Visualização de Caixa Postal

Pacotes de idioma de Unificação de MENSAGENS também oferecem suporte para visualização da caixa postal, que permite que os usuários selecionem rapidamente suas mensagens de voz lendo suas transcrições de dentro de um cliente de email com suporte, como Outlook ou Outlook Web App.

Quando um chamador deixa uma mensagem de voz para um usuário habilitado para Unificação de MENSAGENS, o arquivo de mensagem de voz e uma transcrição da mensagem de voz são colocados no corpo da mensagem de voz que é enviada à caixa de correio do usuário.

Todos os pacotes de idiomas da UM são arquivos únicos que podem ser baixados. Esses pacotes de idioma incluem os prompts pré-gravados, arquivos de gramática, Conversão de Texto em Fala (TTS) e ASR. No entanto, nem todos os pacotes de idioma da UM contêm suporte à Visualização de Caixa Postal.

Os seguintes pacotes de idioma da UM contêm suporte a todos os componentes e recursos, inclusive à Visualização de Caixa Postal:

  - Inglês (EUA) - (en-US)

  - Inglês (Canadá) (en-CA)

  - Francês (França) - (fr-FR)

  - Italiano - (it-IT)

  - Polônia (pl-PL)

  - Português (Portugal) (pt-PT)

  - Espanhol (Espanha) (es-ES)

Por padrão, depois de instalar o servidor de caixa de correio, o servidor enviará voz visualizações de email para usuários habilitados se um pacote de idiomas de Unificação de MENSAGENS com suporte é instalado.

Há Unified Messaging visualização da caixa postal parceiros que oferecem suporte a transcrição avançada para o recurso de visualização da caixa postal. Esses parceiros empregam pessoas para corrigir as transcrições de correio de voz que foram criadas usando a ASR. Cada parceiro de visualização da caixa postal deve atender a um conjunto de requisitos para ser certificados para interoperar com a Unificação de mensagens.

Se você achar que as visualizações de correio de voz enviado para seus usuários não são precisos o suficiente, você pode contatar um dos parceiros visualização da caixa postal certificados listados na página [Microsoft identifique para Unificação de mensagens](https://go.microsoft.com/fwlink/p/?linkid=261951) e sign up com eles a um custo adicional.

Você pode baixar os pacotes de idiomas de Unificação de MENSAGENS do [Centro de Download da Microsoft](https://go.microsoft.com/fwlink/p/?linkid=266542). Para obter informações detalhadas, consulte [Instalar um pacote de idiomas para UM](install-a-um-language-pack-exchange-2013-help.md).

## Idiomas do Unified Messaging

Para permitir que os chamadores usar os vários recursos de idioma encontrados na Unificação de mensagens, você deve primeiro instalar um pacote de idiomas de Unificação de MENSAGENS. Em seguida, você tem a opção configurar outros componentes de Unificação de MENSAGENS.

  - Instale o pacote de idioma de Unificação de MENSAGENS nos servidores de caixa de correio em sua organização.

  - Se for necessário, configure o idioma padrão para um plano de discagem de UM. Isso permite que os usuários do Voice Access Outlook associados a UM novo idioma de uso de plano de discagem quando acessarem suas caixas de correio. No entanto, os usuários ainda podem configurar sua configuração de idioma nas opções de Outlook Web App.

  - Se você precisar permitir que vários idiomas em atendedores automáticos, defina a configuração de idioma em um atendedor automático. Por padrão, um atendedor automático usa o idioma de plano de discagem de Unificação de MENSAGENS. No entanto, você pode alterar essa configuração e permitir que os chamadores não autenticados para se conectar à sua organização e para percorrer os menus do atendedor automático no idioma que você especificou do atendedor automático.

## Pacotes de idioma do Unified Messaging

Instalar um pacote de idioma de Unificação de MENSAGENS em um servidor de caixa de correio usando Setup.exe. Depois de instalar o novo pacote de idioma, o idioma associado com o pacote de idiomas será adicionado à lista de idiomas disponíveis que você pode usar. Você pode visualizar os idiomas que tem sido instalados usando o cmdlet [Get-UMService](https://technet.microsoft.com/pt-br/library/jj552407\(v=exchg.150\)) em Exchange Management Shell.

Quando você instala o idioma UM pacote, os arquivos que são usados pelo mecanismo de TTS e os prompts pré-gravado para o idioma escolhido são copiados e disponibilizados para usuários que se conectam ao sistema de correio de voz. Você pode baixar os pacotes de idiomas de Unificação de MENSAGENS do [Centro de Download da Microsoft](https://go.microsoft.com/fwlink/p/?linkid=266542). Para obter informações detalhadas, consulte [Instalar um pacote de idiomas para UM](install-a-um-language-pack-exchange-2013-help.md).

## Idiomas de plano de discagem de UM

Cada plano de discagem UM é criado contém uma configuração de idioma padrão. A configuração de idioma de plano de discagem de Unificação de MENSAGENS é necessária porque a Unificação de mensagens pode precisar usar conversão de TTS ou reproduzir um prompt de áudio padrão para Outlook usuários Voice Access quando acessarem suas caixas de correio. Você não precisará selecionar um idioma de plano de discagem padrão.

Quando você instala o inglês do Exchange, US será o idioma padrão e a opção de idioma disponíveis somente para seu plano de discagem. Após instalar um pacote de idiomas de Unificação de MENSAGENS em um servidor de caixa de correio, o idioma associado com o pacote de idiomas será listado como uma opção disponível ao configurar o idioma padrão para o plano de discagem.

O idioma padrão é importante para os chamadores. Quando um usuário de acesso de voz Outlook chama sistema de correio de voz, o idioma usado baseia-se a configuração de idioma no Outlook Web App que foi definido quando o usuário conectado primeiro ao suas caixas de correio. A Unificação de mensagens compara o idioma definido no Outlook Web App à lista de idiomas disponíveis no plano de discagem ao qual o usuário está associado. Se não houver nenhuma correspondência adequada, o idioma de plano de discagem de Unificação de MENSAGENS padrão será usado. Por exemplo, se você tiver um plano de discagem que contém apenas os usuários da França, convém alterar a configuração de idioma padrão no plano de discagem para francês.

## Idiomas de Atendedor de automático de Unificação de MENSAGENS

Por padrão, como atendedores automáticos são associados um plano de discagem de Unificação de MENSAGENS quando são criados, eles usam a configuração de idioma padrão do associado UM plano de discagem. No entanto, essa configuração pode ser alterada após a criação do atendedor automático.

A configuração de idioma atendedor automático Unificação de MENSAGENS é necessária porque a Unificação de mensagens pode precisar usar conversão de TTS ou reproduzir um prompt de áudio padrão para um chamador. A Unificação de mensagens não verifica se o idioma de prompts personalizados para o atendedor automático corresponde a configuração de idioma no atendedor automático. No entanto, como uma prática recomendada, certifique-se de que a configuração de idioma do atendedor automático corresponde ao idioma dos prompts personalizados. Caso contrário, o chamador pode ouvir a mudança do sistema de um idioma para outro.

Também é útil se você precisar atendentes automáticos de específicas do idioma diferente da várias para os chamadores poder alterar a configuração de idioma do atendedor automático Unificação de MENSAGENS.

## Processo de seleção de idioma do cliente

Pacotes de idiomas de Unificação de MENSAGENS permitem que os chamadores e Outlook usuários com acesso de voz interagir com o sistema de Unificação de mensagens em vários idiomas. Depois de instalar pacotes de idioma adicionais em um servidor de caixa de correio, os chamadores e usuários do Voice Access Outlook podem ouvir mensagens de email e interagir com o sistema de caixa postal e Outlook Web App usuários e os usuários que estejam usando Outlook 2010 ou uma versão posterior podem exibir a transcrição de uma mensagem de voz usando a visualização da caixa postal em um idioma específico.

Para oferecer suporte a um idioma específico, uma linguagem de cliente UM pacote para que o idioma deve ser instalado em cada servidor de caixa de correio.

Em alguns casos, se um pacote de idiomas de Unificação de MENSAGENS para um idioma específico não tiver sido instalado e não estiver disponível, um idioma de fallback do cliente pode ser usado. Idiomas de cliente UM fallback estão disponíveis para ser usado no lugar de alguns idiomas, mas, para outros idiomas, o idioma de fallback não está disponível. Se não há um pacote de idiomas de Unificação de MENSAGENS instalado para um idioma específico, e nenhum idioma de fallback está disponível para esse idioma, en-US (inglês americano) serão usado.

A tabela a seguir inclui uma lista de idiomas do cliente e os idiomas de fallback que são usados quando um pacote de idiomas de Unificação de MENSAGENS específico não foi instalado em um servidor de caixa de correio.

### Idiomas de fallback de cliente para Unificação de MENSAGENS

<table style="width:100%;">
<colgroup>
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
</colgroup>
<thead>
<tr class="header">
<th>Idioma</th>
<th>País/Região</th>
<th>Identificação da cultura</th>
<th>Primeiro idioma escolhido, se instalado</th>
<th>Segundo idioma escolhido, se instalado</th>
<th>Terceiro idioma escolhido, se instalado</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Catalão</p></td>
<td><p>Espanha</p></td>
<td><p>ca-ES</p></td>
<td><p>ca-ES</p></td>
<td><p>en-US</p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Chinês (Hong Kong)</p></td>
<td><p>China</p></td>
<td><p>zh-HK</p></td>
<td><p>zh-HK</p></td>
<td><p>zh-CN</p></td>
<td><p>zh-TW</p></td>
</tr>
<tr class="odd">
<td><p>Chinês (simplificado)</p></td>
<td><p>China</p></td>
<td><p>zh-CN</p></td>
<td><p>zh-CN</p></td>
<td><p>zh-HK</p></td>
<td><p>zh-TW</p></td>
</tr>
<tr class="even">
<td><p>Chinês (tradicional)</p></td>
<td><p>Taiwan</p></td>
<td><p>zh-TW</p></td>
<td><p>zh-TW</p></td>
<td><p>zh-HK</p></td>
<td><p>zh-CN</p></td>
</tr>
<tr class="odd">
<td><p>Dinamarquês</p></td>
<td><p>Dinamarca</p></td>
<td><p>da-DK</p></td>
<td><p>da-DK</p></td>
<td><p>en-US</p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Holandês</p></td>
<td><p>Países Baixos</p></td>
<td><p>nl-NL</p></td>
<td><p>nl-NL</p></td>
<td><p>en-US</p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Inglês</p></td>
<td><p>Austrália</p></td>
<td><p>en-AU</p></td>
<td><p>en-AU</p></td>
<td><p>en-US</p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Inglês</p></td>
<td><p>Canadá</p></td>
<td><p>en-CA</p></td>
<td><p>en-CA</p></td>
<td><p>en-US</p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Inglês</p></td>
<td><p>Índia</p></td>
<td><p>en-IN</p></td>
<td><p>en-IN</p></td>
<td><p>en-US</p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Inglês</p></td>
<td><p>Reino Unido</p></td>
<td><p>en-GB</p></td>
<td><p>en-GB</p></td>
<td><p>en-US</p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Inglês</p></td>
<td><p>Estados Unidos</p></td>
<td><p>en-US</p></td>
<td><p>en-US</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Finlandês</p></td>
<td><p>Finlândia</p></td>
<td><p>fi-FL</p></td>
<td><p>fi-FL</p></td>
<td><p>en-US</p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Francês</p></td>
<td><p>Canadá</p></td>
<td><p>fr-CA</p></td>
<td><p>fr-CA</p></td>
<td><p>fr-FR</p></td>
<td><p>en-US</p></td>
</tr>
<tr class="even">
<td><p>Francês</p></td>
<td><p>França</p></td>
<td><p>fr-FR</p></td>
<td><p>fr-FR</p></td>
<td><p>fr-CA</p></td>
<td><p>en-US</p></td>
</tr>
<tr class="odd">
<td><p>Alemão</p></td>
<td><p>Alemanha</p></td>
<td><p>de-DE</p></td>
<td><p>de-DE</p></td>
<td><p>en-US</p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Italiano</p></td>
<td><p>Itália</p></td>
<td><p>it-IT</p></td>
<td><p>it-IT</p></td>
<td><p>en-US</p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Japonês</p></td>
<td><p>Japão</p></td>
<td><p>ja-JP</p></td>
<td><p>ja-JP</p></td>
<td><p>en-US</p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Coreano</p></td>
<td><p>Coréia</p></td>
<td><p>ko-KR</p></td>
<td><p>ko-KR</p></td>
<td><p>en-US</p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Norueguês (Bokmål)</p></td>
<td><p>Noruega</p></td>
<td><p>nb-NO</p></td>
<td><p>nb-NO</p></td>
<td><p>en-US</p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Polonês</p></td>
<td><p>Polônia</p></td>
<td><p>pl-PL</p></td>
<td><p>pl-PL</p></td>
<td><p>en-US</p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Português</p></td>
<td><p>Brasil</p></td>
<td><p>pt-BR</p></td>
<td><p>pt-BR</p></td>
<td><p>pt-PT</p></td>
<td><p>en-US</p></td>
</tr>
<tr class="even">
<td><p>Português</p></td>
<td><p>Portugal</p></td>
<td><p>pt-PT</p></td>
<td><p>pt-PT</p></td>
<td><p>pt-BR</p></td>
<td><p>en-US</p></td>
</tr>
<tr class="odd">
<td><p>Russo</p></td>
<td><p>Rússia</p></td>
<td><p>ru-RU</p></td>
<td><p>ru-RU</p></td>
<td><p>en-US</p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Espanhol</p></td>
<td><p>Espanha</p></td>
<td><p>es-ES</p></td>
<td><p>es-ES</p></td>
<td><p>es-MX</p></td>
<td><p>en-US</p></td>
</tr>
<tr class="odd">
<td><p>Espanhol</p></td>
<td><p>México</p></td>
<td><p>es-MX</p></td>
<td><p>es-MX</p></td>
<td><p>es-ES</p></td>
<td><p>en-US</p></td>
</tr>
<tr class="even">
<td><p>Sueco</p></td>
<td><p>Suécia</p></td>
<td><p>sv-SE</p></td>
<td><p>sv-SE</p></td>
<td><p>en-US</p></td>
<td><p></p></td>
</tr>
</tbody>
</table>


Voltar ao início

