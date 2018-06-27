---
title: 'Configurar a codificação de transferência de conteúdo: Exchange 2013 Help'
TOCTitle: Configurar a codificação de transferência de conteúdo
ms:assetid: c4922362-18d4-42f7-9189-9076720eb1d8
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Gg144562(v=EXCHG.150)
ms:contentKeyID: 50486576
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configurar a codificação de transferência de conteúdo

 

_**Aplica-se a:**Exchange Online, Exchange Server 2013_

_**Tópico modificado em:**2015-03-09_

*Codificação de transferência de conteúdo* define os métodos de codificação para transformar dados de mensagem de email binário em formato de texto sem formatação a US-ASCII. Essa transformação permite a mensagem se desloque em servidores mais antigos da mensagens SMTP que suportam somente as mensagens em texto US-ASCII. Codificação de transferência de conteúdo é definida no RFC 2045. A método de codificação de transferência é armazenada no campo de cabeçalho **Codificação de transferência de conteúdo** da mensagem. No Microsoft Exchange Server 2013, os seguintes métodos de codificação de transferência de conteúdo estão disponíveis:

  - **7 bits**   Esse valor indica que os dados de corpo da mensagem já estão no formato texto sem formatação ASCII conosco e nenhuma codificação de mensagem tiver sido estabelecida à mensagem.

  - **Quoted-printable (QP)**   Este método de codificação usa caracteres US-ASCII imprimíveis para codificar os dados de corpo da mensagem. Se o texto da mensagem original é principalmente o texto US-ASCII, a codificação QP oferece resultados de relativamente legíveis e compacto. Por padrão, Exchange 2013 usa QP para codificação dados binários de mensagem.

  - **Base64**   Este método de codificação baseia-se principalmente na privacidade avançada padrão de email (PEM) definido no RFC 1421. A codificação Base64 usa 64 caracteres alfabeto preenchimento caracteres definidos pela PEM de saída e de método de codificação para codificar os dados de corpo da mensagem. A codificação Base64 cria um previsível aumento no tamanho da mensagem e é ideal para dados binários e texto de não-US-ASCII.

Configure a método usando o parâmetro *ByteEncoderTypeFor7BitCharsets* nos cmdlets **Set-OrganizationConfig** e **Set-RemoteDomain** de codificação de transferência. As configurações de codificação de transferência de conteúdo que você configure com **Set-OrganizationConfig** se aplicam a todas as mensagens na organização do Exchange. As configurações de codificação de transferência de conteúdo que você configure com **Set-RemoteDomain** aplicam-se somente a mensagem enviada para destinatários externos no domínio remoto.

A tabela a seguir lista os valores que você pode usar para definir a método de codificação de transferência.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Parâmetro em <strong>Set-OrganizationConfig</strong></th>
<th>Parâmetro em <strong>Set-RemoteDomain</strong></th>
<th>Descrição</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>0</p></td>
<td><p><code>Use7Bit</code></p></td>
<td><p>Use sempre a codificação de 7 bits para HTML e texto sem formatação. Este é o valor padrão.</p></td>
</tr>
<tr class="even">
<td><p>1</p></td>
<td><p><code>UseQP</code></p></td>
<td><p>Use sempre a codificação QP para HTML e texto sem formatação.</p></td>
</tr>
<tr class="odd">
<td><p>2</p></td>
<td><p><code>UseBase64</code></p></td>
<td><p>Use sempre a codificação Base64 para HTML e texto sem formatação.</p></td>
</tr>
<tr class="even">
<td><p>5</p></td>
<td><p><code>UseQPHtmlDetectTextPlain</code></p></td>
<td><p>Use a codificação QP para HTML e texto sem formatação, a menos que a quebra de linha estiver habilitada em texto sem formatação. Se a quebra de linha estiver habilitada, use a codificação de 7 bits para texto sem formatação.</p></td>
</tr>
<tr class="odd">
<td><p>6</p></td>
<td><p><code>UseBase64HtmlDetectTextPlain</code></p></td>
<td><p>Use a codificação Base64 para HTML e texto sem formatação, a menos que a quebra de linha estiver habilitada em texto sem formatação. Se a quebra de linha é habilitada em texto sem formatação, use a codificação Base64 para HTML e usar a codificação de 7 bits texto sem formatação.</p></td>
</tr>
<tr class="even">
<td><p>13</p></td>
<td><p><code>UseQPHtml7BitTextPlain</code></p></td>
<td><p>Use sempre a codificação QP para HTML. Sempre use a codificação de 7 bits para texto sem formatação.</p></td>
</tr>
<tr class="odd">
<td><p>14</p></td>
<td><p><code>UseBase64Html7BitTextPlain</code></p></td>
<td><p>Use sempre a codificação Base64 para HTML. Sempre use a codificação de 7 bits para texto sem formatação.</p></td>
</tr>
</tbody>
</table>


Para obter mais detalhes sobre o campo de cabeçalho de **Codificação de transferência de conteúdo**, consulte a seção "Noções básicas sobre a estrutura das mensagens de email" [Conversão de conteúdo](content-conversion-exchange-2013-help.md).

Para obter mais informações sobre domínios remotos, consulte [Domínios remotos](remote-domains-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: 15 minutos

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Serviço de transporte" no tópico [Permissões de fluxo de email](mail-flow-permissions-exchange-2013-help.md).

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>.



## O que você deseja fazer?

## Use o Shell para configurar a método para a organização de codificação de transferência de conteúdo

Para configurar a método para a organização de codificação de transferência de conteúdo, execute o seguinte comando:

    Set-OrganizationConfig -ByteEncoderTypeFor7BitCharsets <Integer>

Por exemplo, para definir a método de Base64 de codificação de transferência de conteúdo, execute o seguinte comando:

    Set-OrganizationConfig -ByteEncoderTypeFor7BitCharsets 2

## Use o Shell para configurar a método para um domínio remoto de codificação de transferência de conteúdo

Para configurar a método de codificação para todos os destinatários em um domínio remoto de transferência de conteúdo, execute o seguinte comando:

    Set-RemoteDomain -ByteEncoderTypeFor7BitCharsets <Value>

Por exemplo, para definir a método de Base64 de codificação de transferência de conteúdo, execute o seguinte comando:

    Set- RemoteDomain -ByteEncoderTypeFor7BitCharsets UseBase64

## Como saber se funcionou?

Para verificar se você configurou com êxito o método de codificação de transferência de conteúdo, faça o seguinte:

1.  Envie uma mensagem de teste que contenha uma mistura de texto US-ASCII e dados binários ou texto não-US-ASCII para uma conta de teste interno ou externo. Use uma conta interna para testar as configurações da organização e uma conta externa no domínio remoto para testar as configurações de domínio remoto.

2.  Em um cliente de email, exiba o campo de cabeçalho **Content-Transfer-Encoding** na mensagem e verifique se o método que foi utilizado na mensagem de codificação de transferência de conteúdo corresponde o método que você configurou.

