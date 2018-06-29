---
title: 'Opções de codificação de mensagem: Exchange 2013 Help'
TOCTitle: Opções de codificação de mensagem
ms:assetid: c1d9edbb-d87c-41e5-881b-cd612d83d7e4
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Bb310794(v=EXCHG.150)
ms:contentKeyID: 50486586
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Opções de codificação de mensagem

 

_**Aplica-se a:**Exchange Online, Exchange Server 2013_

_**Tópico modificado em:**2016-12-09_

As opções de codificação de mensagem disponíveis no Exchange especificam características da mensagem, como conjuntos de caracteres MIME e não MIME, codificação binária e formatos de anexos. Você pode especificar opções de codificação de mensagem nos seguintes locais:

  - Configurações de domínio remoto

  - Configurações de contato de email e usuário de email

  - Configurações do Microsoft Outlook
    
      - Formato de mensagem
    
      - Formato de mensagem da Internet
    
      - Formato de mensagem de destinatário da Internet
    
      - Opções de codificação de conjunto de caracteres de mensagem

**Conteúdo**

Message encoding options for messages sent to remote domains

Message encoding options for mail users and mail contacts

Message encoding options available in Outlook

Opções disponíveis no Outlook Web App de codificação de mensagem

Order of precedence for message encoding options

Para obter mais informações

## Opções de codificação de mensagem para mensagens enviadas a domínios remotos

Ao configurar as opções de codificação de mensagens para um domínio remoto, as configurações específicas são aplicadas a todas as mensagens enviadas para o domínio. Para domínios remotos da sua organização, há as seguintes opções de configuração para codificação de mensagens.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p><strong>Configuração</strong></p></td>
<td><p><strong>Disponível no EAC do Exchange Online dedicado</strong></p></td>
<td><p><strong>Disponível no Shell</strong></p></td>
</tr>
<tr class="even">
<td><p><strong>Conjunto de caracteres MIME</strong>   O conjunto de caracteres que você especificar será usado somente para mensagens MIME que não tenham seu próprio conjunto especificado. A definição deste parâmetro não substituirá conjuntos de caracteres já especificados para o email de saída.</p>
<p><strong>Conjunto de caracteres não MIME</strong>   Essa configuração é usada se alguma das seguintes condições for verdadeira:</p>
<ul>
<li><p>Mensagens de entrada de um domínio remoto que estão sem o valor da configuração <em>charset=</em> no tipo de Conteúdo MIME: campo do cabeçalho.</p></li>
<li><p>Mensagens de saída para um domínio remoto que estão sem o valor do conjunto de caracteres MIME.</p></li>
</ul>
<p></p></td>
<td><p>Sim</p></td>
<td><p>Sim</p></td>
</tr>
<tr class="odd">
<td><p><strong>Tipo de conteúdo</strong>   Você pode especificar o tipo de conteúdo para mensagens MIME enviadas a destinatários no domínio remoto. Você pode usar uma das seguintes configurações:</p>
<ul>
<li><p><strong>MimeHtmlText</strong>   Todas as mensagens são convertidas em mensagens MIME que usam formatação HTML, a menos que a mensagem original seja uma mensagem de texto. Se a mensagem original for uma mensagem de texto, a mensagem de saída será uma mensagem MIME que usa formatação de texto. Essa é a configuração-padrão.</p></li>
<li><p><strong>MimeText</strong>   Todas as mensagens são convertidas em mensagens MIME que usam formatação de texto.</p></li>
<li><p><strong>MimeHtml</strong>   Todas as mensagens são convertidas em mensagens MIME que usam formatação HTML.</p></li>
</ul></td>
<td><p>Não</p></td>
<td><p>Sim</p></td>
</tr>
<tr class="even">
<td><p><strong>Tamanho de quebra automática de linha</strong>   Você pode especificar o número máximo de caracteres que podem existir em uma única linha de texto no corpo da mensagem de email. Os aplicativos de cliente de email mais antigos poderão preferir 78 caracteres por linha. Essa opção só será disponibilizada com o Shell.</p>
<p></p></td>
<td><p>Não</p></td>
<td><p>Sim</p></td>
</tr>
</tbody>
</table>


Voltar ao início

## Opções de codificação de mensagens para usuários de email e contatos de email

Ao configurar as opções de codificação de mensagens para um contato de email ou usuário de email, essa opção é aplicada a todas as mensagens enviadas a esse destinatário específico. Para contatos de email e usuários de email em sua organização, você tem as seguintes opções de configuração para a codificação de mensagens:

  - **UsePreferMessageFormat**   Esse parâmetro especifica se as definições de formato da mensagem configuradas para o contato de email substituem as definições globais configuradas para o domínio remoto. Se desabilitar essa configuração, o Exchange irá ignorar outras opções de codificação de mensagem deste destinatário, e a codificação de mensagem será determinada pela configuração do domínio remoto ou pelas configurações definidas pelo remetente da mensagem.

  - **MessageFormat**   Esse parâmetro especifica o formato de mensagem. Você pode especificar Texto ou MIME como o formato de mensagem. O valor dessa configuração é dependente de parâmetro *MessageBodyFormat*. Se o formato de corpo da mensagem for Html ou TextAndHtml, você deve definir o parâmetro como MIME.

  - **MessageBodyFormat**   Esse parâmetro especifica o formato do corpo da mensagem. Você pode especificar Texto, HTML ou TextAndHtml. O valor dessa configuração é dependente de parâmetro *MessageFormat*. Se o formato da mensagem for Texto, você também deve definir esse parâmetro como Texto.

  - **MacAttachmentFormat**   Esse parâmetro especifica o formato de anexo do sistema operacional Apple Macintosh para mensagens. Você pode especificar BinHex, UuEncode, AppleSingle ou AppleDouble. O valor dessa configuração é dependente de parâmetro *MessageFormat*. Se o formato da mensagem estiver definido como Texto, você deve definir esse parâmetro como BinHex ou UuEncode. Se o formato da mensagem estiver definido como MIME, você deve definir esse parâmetro como BinHex, AppleSingle ou AppleDouble.

Você deve usar esses parâmetros no Shell de Gerenciamento do Exchange para definir as opções de codificação de mensagens para usuários de email e contatos de email. Para mais informações, consulte os seguintes tópicos:

  - [Enable-MailContact](https://technet.microsoft.com/pt-br/library/aa996001\(v=exchg.150\))

  - [New-MailContact](https://technet.microsoft.com/pt-br/library/bb124519\(v=exchg.150\))

  - [Set-MailContact](https://technet.microsoft.com/pt-br/library/aa995950\(v=exchg.150\))

  - [Enable-MailUser](https://technet.microsoft.com/pt-br/library/aa996549\(v=exchg.150\))

  - [New-MailUser](https://technet.microsoft.com/pt-br/library/aa996335\(v=exchg.150\))

  - [Set-MailUser](https://technet.microsoft.com/pt-br/library/aa995971\(v=exchg.150\))

Voltar ao início

## Opções de codificação de mensagem disponíveis no Outlook

Como remetente, você pode especificar as opções de codificação de mensagem no Outlook em qualquer uma destas etapas:

  - Configurando o formato de mensagem padrão como texto não criptografado ou HTML.

  - Definindo o formato da mensagem que você está escrevendo como texto não criptografado ou HTML usando a área **Formato** na guia **Opções**.

  - Configurando as opções de codificação de mensagem para mensagens enviadas a todos os destinatários fora da organização do Exchange. Essas opções são chamadas de *Formato de mensagem da Internet*. As opções só se aplicam a destinatários remotos, e não a destinatários na organização do Exchange.

  - Configurando as opções de codificação de mensagem para mensagens enviadas a destinatários específicos fora da organização do Exchange. Essas opções são chamadas de *Formato de mensagem de destinatário da Internet*. As opções só se aplicam a destinatários remotos em sua pasta de Contatos, e não a destinatários na organização do Exchange.

Por padrão, o Outlook utiliza a codificação automática de mensagem de conjuntos de caracteres verificando todo o texto da mensagem de saída a fim de determinar a codificação correta a ser usada na mensagem. Essa configuração é aplicada a mensagens enviadas a destinatários da Internet e a destinatários da organização do Exchange. No entanto, você pode ignorar isso e especificar sua codificação preferida para mensagens de saída.

Voltar ao início

## Opções de codificação de mensagem disponíveis no Outlook Web App

Como remetente, você pode especificar as opções de codificação de mensagem no Outlook Web App em qualquer uma destas etapas:

  - Configurando o formato de mensagem padrão como texto sem formatação ou HTML na seção **Formato de mensagem** da página **Configurações** \>**Opções** \> **Configurações**.

  - Configurando o formato de mensagem durante a elaboração como texto sem formatação ou HTML usando o menu **Mais opções** (…) e selecionando **Alternar para texto sem formatação** ou **Alternar para HTML**.

Voltar ao início

## Ordem de precedência para opções de codificação de mensagem

O Exchange usa a ordem de precedência, conforme descrito na lista a seguir, para determinar as opções de codificação para mensagens de saída que são enviadas aos destinatários fora da organização do Exchange:

1.  Configurações de domínio remoto

2.  Configurações do Outlook ou do Outlook Web App

3.  Configurações de usuário ou contato de email

A lista especifica a ordem de precedência da menor para a maior. Uma configuração feita em um nível superior pode substituir uma configuração feita em um nível inferior.

A tabela a seguir descreve a ordem de precedência da prioridade mais baixa para a prioridade mais alta para opções de codificação do conjunto de caracteres da mensagem.

### Ordem de precedência da prioridade mais baixa para a prioridade mais alta para opções de codificação do conjunto de caracteres da mensagem

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Origem</th>
<th>Parâmetro</th>
<th>Valores</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Usar o EAC ou <strong>Set-RemoteDomain</strong> para configurar a entrada de domínio remoto</p></td>
<td><p><em>CharacterSet</em></p></td>
<td><p>Especificada</p></td>
</tr>
<tr class="even">
<td><p>Usar o EAC ou <strong>Set-RemoteDomain</strong> para configurar a entrada de domínio remoto</p></td>
<td><p><em>NonMimeCharacterSet</em></p></td>
<td><p>Especificada</p></td>
</tr>
<tr class="odd">
<td><p>Configurações do Outlook</p></td>
<td><p>Codificação do conjunto de caracteres da mensagem</p></td>
<td><ul>
<li><p>Seleção automática</p></li>
<li><p>Especificada</p></li>
</ul></td>
</tr>
</tbody>
</table>


Quando você configura o conjunto de caracteres não MIME para um domínio remoto, esse conjunto de caracteres é atribuído aos seguintes tipos de mensagens:

  - Mensagens de saída para um domínio remoto configurado que não contêm um conjunto de caracteres especificado.

  - Mensagens de entrada provenientes de um domínio remoto configurado que não contêm um conjunto de caracteres especificado.

O valor da página de código ANSI do Windows para o servidor de transporte é usado para atribuir um conjunto de caracteres aos seguintes tipos de mensagens:

  - Mensagens internas que não contêm um conjunto de caracteres especificado.

  - Mensagens internas que contêm um conjunto de caracteres especificado, mas não contêm uma página de código do servidor especificado.

Se uma mensagem contiver um conjunto de caracteres especificado, mas inválido, o servidor de transporte tentará substituir o conjunto de caracteres inválido por um conjunto de caracteres válido.

A tabela a seguir descreve a ordem de precedência da prioridade mais baixa para a prioridade mais alta para opções de codificação de mensagem de texto não criptografado.

### Ordem de precedência da prioridade mais baixa para a prioridade mais alta para opções de codificação de mensagem de texto não criptografado

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Origem</th>
<th>Parâmetro</th>
<th>Valores</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>Set-RemoteDomain</strong></p></td>
<td><p><em>LineWrapSize</em></p></td>
<td><ul>
<li><p>De 0 a 132</p></li>
<li><p>ilimitado</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Configurações do Outlook</p></td>
<td><p>Formato de mensagem</p></td>
<td><p>Texto simples</p></td>
</tr>
<tr class="odd">
<td><p>Configurações do Outlook</p></td>
<td><p>Formato de mensagem da Internet</p></td>
<td><p>Opções de texto não criptografado:</p>
<ul>
<li><p>Codificar anexos no formato UuEncode quando você enviar uma mensagem de texto não criptografado</p></li>
<li><p>Quebrar automaticamente a linha de texto em <em>nn</em> caracteres</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Configurações do Outlook</p></td>
<td><p>Formato de mensagem de destinatário da Internet</p></td>
<td><p>Formato de texto não criptografado:</p>
<ul>
<li><p>Codificar anexos no formato de anexo UuEncode</p></li>
<li><p>Usar formato de anexo do Mac BinHex</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p><strong>Set-MailUser</strong></p>
<p><strong>Set-MailContact</strong></p></td>
<td><p><em>UsePreferMessageFormat</em></p></td>
<td><ul>
<li><p><code>$true</code></p></li>
<li><p><code>$false</code></p></li>
</ul>
<p>Se o valor for <code>$false</code> ou se o destinatário não for definido como um usuário de email ou contato de email na organização do Exchange, as configurações do usuário de email ou do contato de email serão ignoradas.</p></td>
</tr>
<tr class="even">
<td><p><strong>Set-MailUser</strong></p>
<p><strong>Set-MailContact</strong></p></td>
<td><p><em>MessageFormat</em></p></td>
<td><p>Texto</p></td>
</tr>
<tr class="odd">
<td><p><strong>Set-MailUser</strong></p>
<p><strong>Set-MailContact</strong></p></td>
<td><p><em>MessageBodyFormat</em></p></td>
<td><p>Texto</p></td>
</tr>
<tr class="even">
<td><p><strong>Set-MailUser</strong></p>
<p><strong>Set-MailContact</strong></p></td>
<td><p><em>MacAttachmentFormat</em></p></td>
<td><ul>
<li><p>BinHex</p></li>
<li><p>UuEncode</p></li>
</ul></td>
</tr>
</tbody>
</table>


A tabela a seguir descreve a ordem de precedência da prioridade mais baixa para a prioridade mais alta para opções de codificação de mensagem MIME.

### Ordem de precedência da prioridade mais baixa para a prioridade mais alta para opções de codificação de mensagem MIME

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Origem</th>
<th>Parâmetro</th>
<th>Valores</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>Set-RemoteDomain</strong></p></td>
<td><p><em>ContentType</em></p></td>
<td><ul>
<li><p><code>MimeHtmlText</code></p></li>
<li><p><code>MimeText</code></p></li>
<li><p><code>MimeHtml</code></p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Configurações do Outlook ou do Outlook Web App</p></td>
<td><p>Formato de mensagem</p></td>
<td><ul>
<li><p>Texto simples</p></li>
<li><p>HTML</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Configurações do Outlook</p></td>
<td><p>Formato de mensagem de destinatário da Internet</p></td>
<td><p>Formato de mensagem MIME</p>
<ul>
<li><p>Texto simples</p></li>
<li><p>Incluir texto simples e HTML</p></li>
<li><p>HTML</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p><strong>Set-MailUser</strong></p>
<p><strong>Set-MailContact</strong></p></td>
<td><p><em>UsePreferMessageFormat</em></p></td>
<td><p><code>$true</code></p>
<p><code>$false</code></p>
<p>Se o valor for <code>$false</code> ou se o destinatário não for definido como um usuário de email ou contato de email na organização do Exchange, as configurações do usuário de email ou do contato de email serão ignoradas.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Set-MailUser</strong></p>
<p><strong>Set-MailContact</strong></p></td>
<td><p><em>MessageFormat</em></p></td>
<td><ul>
<li><p>Texto</p></li>
<li><p>Mime</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p><strong>Set-MailUser</strong></p>
<p><strong>Set-MailContact</strong></p></td>
<td><p><em>MessageBodyFormat</em></p></td>
<td><ul>
<li><p><code>Text</code></p></li>
<li><p><code>Html</code></p></li>
<li><p><code>TextAndHtml</code></p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p><strong>Set-MailUser</strong></p>
<p><strong>Set-MailContact</strong></p></td>
<td><p><em>MacAttachmentFormat</em></p></td>
<td><ul>
<li><p>BinHex</p></li>
<li><p>AppleSingle</p></li>
<li><p>AppleDouble</p></li>
</ul></td>
</tr>
</tbody>
</table>


Voltar ao início

## Para obter mais informações, consulte

[Opções de codificação de mensagem](message-encoding-options-exchange-2013-help.md)

[Opções de conversão de TNEF](tnef-conversion-options-exchange-2013-help.md)

[Domínios remotos](remote-domains-exchange-2013-help.md)

[Domínios remotos no Exchange Online](https://technet.microsoft.com/pt-br/library/jj966211\(v=exchg.150\))

[Gerenciar usuários de email](manage-mail-users-exchange-2013-help.md)

[Gerenciar contatos de email](manage-mail-contacts-exchange-2013-help.md)

[Alterar o formato da mensagem no Outlook](https://go.microsoft.com/fwlink/p/?linkid=397890)

