---
title: 'Opções de conversão de TNEF: Exchange 2013 Help'
TOCTitle: Opções de conversão de TNEF
ms:assetid: 989a62fc-4bc1-448f-90c8-7c7b56fe1084
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Bb310786(v=EXCHG.150)
ms:contentKeyID: 52058479
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Opções de conversão de TNEF

 

_**Aplica-se a:** Exchange Online, Exchange Server 2013_

_**Tópico modificado em:** 2015-03-09_

Você pode especificar se o TNEF Transport Neutral Encapsulation Format () devem ser preservadas ou removida das mensagens que saem da organização Exchange. TNEF, também conhecido como Outlook Rich Text Format ou Exchange Rich Text Format, é um Microsoft-formato específico para encapsular propriedades de mensagem MAPI. Todas as versões do MicrosoftOutlook entenda totalmente o TNEF. Outlook Web App converte TNEF em MAPI e exibe as mensagens formatadas. No entanto, outros clientes de email que não entendem TNEF normalmente exibem TNEF mensagens formatadas como texto sem formatação mensagens com anexos Winmail. dat ou Win.dat.

**Sumário**

Opções de conversão de TNEF para domínios remotos

Opções de conversão de TNEF para usuários de email e contatos de email

Opções de conversão de TNEF no Outlook

Ordem de precedência para opções de conversão de TNEF

## Opções de conversão de TNEF para domínios remotos

Quando você configura as opções de conversão de TNEF para um domínio remoto, essas opções de conversão TNEF são aplicadas a todas as mensagens enviadas ao domínio.

  - Para o Exchange Online dedicado, você deve usar o Centro de administração do Exchange (EAC) para definir opções de conversão de TNEF para um domínio remoto no **fluxo de emails** \> **domínios remotos** \> **Editar** (![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição")) \> **Exchange usar rich text format**.

  - Para Exchange Online e Exchange 2013, use o parâmetro *TnefEnabled* no cmdlet **Set-RemoteDomain** para definir opções de conversão de TNEF para um domínio remoto.

Para domínios remotos em sua organização, você tem as seguintes opções de configuração para conversão de TNEF:


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Configuração</th>
<th>No EAC</th>
<th>No Shell</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Use o TNEF para todas as mensagens enviadas para o domínio remoto.</p></td>
<td><p><strong>Always</strong></p></td>
<td><p><code>$true</code></p></td>
</tr>
<tr class="even">
<td><p>Nunca use o TNEF para todas as mensagens enviadas para o domínio remoto.</p></td>
<td><p><strong>Never</strong></p></td>
<td><p><code>$false</code></p></td>
</tr>
<tr class="odd">
<td><p>Mensagens TNEF especificamente não são permitidas ou impedidas para destinatários no domínio remoto. Se as mensagens TNEF serão enviadas aos destinatários no domínio remoto dependem da definição específica no contato de email ou o usuário de email ou a configuração especificada pelo remetente no Outlook. Este é o valor padrão.</p></td>
<td><p><strong>Siga as configurações do usuário</strong></p></td>
<td><p><code>$null</code> (em branco)</p></td>
</tr>
</tbody>
</table>


Para obter mais informações sobre domínios remotos, consulte [Domínios remotos](remote-domains-exchange-2013-help.md) ou [Domínios remotos no Exchange Online](https://technet.microsoft.com/pt-br/library/jj966211\(v=exchg.150\)).

Voltar ao início

## Opções de conversão de TNEF para usuários de email e contatos de email

Quando você configura as opções de conversão de TNEF para um contato de email ou de um usuário de email, essas opções de conversão TNEF são aplicadas a todas as mensagens enviadas para que o destinatário específico. Você pode usar o parâmetro *UseMapiRichTextFormat* nos cmdlets de **Set-MailUser** e **Set-MailContact** para configurar as opções de conversão de TNEF para usuários de email e contatos de email.

Para usuários de email e contatos de email na sua organização, você tem as seguintes opções de configuração para conversão de TNEF:

  - **Sempre**   TNEF é usada para todas as mensagens enviadas ao destinatário. O valor correspondente para o parâmetro *UseMapiRichTextFormat* é `Always`.

  - **Nunca**   TNEF nunca é usada para todas as mensagens enviadas ao destinatário. O valor correspondente para o parâmetro *UseMapiRichTextFormat* é `Never`.

  - **Usar as configurações padrão**   Mensagens TNEF especificamente não são permitidas ou impedidas para o contato de email ou de usuário de email. Se as mensagens TNEF são enviadas ao destinatário dependem na configuração específica para o domínio remoto correspondente ou a configuração especificada pelo remetente no Outlook. O valor correspondente para o parâmetro *UseMapiRichTextFormat* é `UseDefaultSettings`. Esta é a configuração padrão.

Voltar ao início

## Opções de conversão de TNEF no Outlook

Remetentes podem controlar as opções de conversão de mensagem TNEF padrão para mensagens TNEF enviadas a todos os destinatários fora da organização do Exchange. Essas opções são chamadas de opções de *formato de mensagem da Internet* . As opções se aplicam somente aos destinatários remotos e não aos destinatários na organização do Exchange.


> [!NOTE]
> As opções seguintes definem como mensagens contendo o rich text do Outlook são manipuladas quando enviadas para destinatários externos. Se você estiver usando o formato da mensagem for HTML ou texto sem formatação, essas configurações não se aplicam.



Você tem as seguintes opções de conversão de TNEF no Outlook:

  - **Converter em formato HTML**   Esta é a opção padrão. Quaisquer mensagens TNEF enviadas aos destinatários remotos são convertidas em HTML. Qualquer formatação na mensagem bastante deve se parecer com a mensagem original. Mensagens HTML codificado em MIME são compatíveis com muitos, mas nem todos os clientes de email.

  - **Converter em formato de texto sem formatação**   Quaisquer mensagens TNEF enviadas aos destinatários remotos são convertidas em texto sem formatação. Qualquer formatação na mensagem será perdida.

  - **Enviar usando o formato Rich Text do Outlook**   Quaisquer mensagens TNEF enviadas aos destinatários remotos permanecem mensagens TNEF.

Você pode configurar essas opções nos seguintes locais no Outlook:

  - **Outlook 2010 ou Outlook 2013** **Arquivo** \> **Opções** \> **email** \> **formato da mensagem**.   

  - **O Outlook 2007** **Ferramentas** \> **Opções** \> **formato de email** \> **formato da Internet**.   

Remetentes também podem controlar as opções de conversão de mensagem TNEF padrão para mensagens TNEF enviadas a destinatários específicos fora da organização do Exchange. Essas opções são chamadas de opções de *formato de mensagem de destinatário da Internet* . As opções se aplicam somente aos destinatários remotos armazenados na sua pasta de contatos e não aos destinatários na organização do Exchange. Você tem as seguintes opções de conversão de TNEF para destinatários remotos na pasta de contatos:

  - **Permitir que o Outlook decida o melhor formato de envio**   Esta é a configuração padrão. Essa configuração força o Outlook a fim de usar a opção de conversão de TNEF que é especificada pelo formato de Internet padrão. Os valores possíveis são **Converter em formato HTML**, **Converter em formato de texto sem formatação** ou **Enviar usando o formato Rich Text do Outlook**. Portanto, a mensagem TNEF pode ser deixada como TNEF, convertida em HTML ou convertida em texto sem formatação. Se você quiser certificar-se de que a mensagem TNEF permanece TNEF para o destinatário, você deve alterar essa configuração de **Permitir que o Outlook decida o melhor formato de envio** para **Enviar em formato Rich Text do Outlook**.

  - **Apenas texto sem formatação de envio**   Quaisquer mensagens TNEF enviadas ao destinatário são convertidas em texto sem formatação. Qualquer formatação na mensagem será perdida.

  - **Enviar em formato Rich Text do Outlook**   Quaisquer mensagens TNEF enviadas aos destinatários remotos permanecem mensagens TNEF.

Você pode configurar essas opções de um contato nos seguintes locais no Outlook:

  - **Outlook 2010 ou Outlook 2013**   Abrir o cartão de visita, clique duas vezes o endereço de email, clique no ícone **Exibir mais opções para interagir com esta pessoa** e selecione **Propriedades do Outlook**. Na caixa de diálogo **Propriedades de email**, selecione o **formato da Internet**.

  - **O Outlook 2007**   Abrir o cartão de visita, clique duas vezes no campo de **email** e selecione o **formato da Internet**.

Voltar ao início

## Ordem de precedência para opções de conversão de TNEF

Exchange usa a ordem de precedência conforme descrito na lista a seguir para determinar as opções de conversão de TNEF das mensagens de saída enviadas aos destinatários fora da organização do Exchange:

1.  Configurações de domínio remoto

2.  Configurações de usuário ou contato de email

3.  Configurações do Outlook

A lista especifica a ordem de precedência da maior para o menor. A configuração de TNEF no domínio remoto substitui as configurações de TNEF no usuário de email, contato de email ou no Outlook. Por exemplo, suponhamos que você enviar uma mensagem de Rich Text do Outlook, mas o destinatário está em um domínio em que a configuração de domínio remoto não permite especificamente mensagens formatadas em TNEF. A mensagem recebida pelo destinatário será texto sem formatação ou HTML, mas não o TNEF.

Além disso, o Exchange nunca envia mensagens de resumo Transport Neutral codificação formato STNEF () para destinatários externos. Mensagens TNEF só podem ser enviadas para destinatários fora da organização do Exchange.

Voltar ao início

