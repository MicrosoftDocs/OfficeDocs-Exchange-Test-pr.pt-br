---
title: 'Práticas recomendadas para configuração das regras de fluxo de email: Exchange Online Protection Help'
TOCTitle: Práticas recomendadas para configuração das regras de fluxo de email
ms:assetid: abd863c3-c0ce-42f3-9470-a573adc3cbba
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Dn960147(v=EXCHG.150)
ms:contentKeyID: 65211650
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Práticas recomendadas para configuração das regras de fluxo de email

 

_**Aplica-se a:** Exchange Online, Exchange Online Protection, Exchange Server 2013_

_**Tópico modificado em:** 2016-12-09_

Siga estas práticas recomendadas para regras de transporte de Exchange para evitar erros comuns de configuração. Cada links de recomendação para um tópico com um exemplo e instruções passo a passo.

## Testar suas regras

Para certificar-se de que inesperada não ocorre para emails de pessoas e para certificar-se você está cumprindo realmente os negócios, legais ou intenção de conformidade da sua regra, certifique-se de testá-lo completamente. Há muitas opções e regras podem interagir uns com os outros, portanto, é importante para mensagens de teste que você espera que isso coincidirá com a regra tanto não correspondem à regra caso você fez inadvertidamente uma regra muito geral. Para saber a todas as opções para testar regras, consulte [Testar uma regra de fluxo de email](test-a-mail-flow-rule-exchange-2013-help.md).

## A regra de escopo

Verifique se que a regra se aplica somente às mensagens que você quer que ela. Por exemplo:

  - **Restringir uma regra para as mensagens chegam ao ou indo para fora da organização**
    
    Por padrão, uma nova regra se aplica às mensagens que são enviadas ou recebidas por pessoas da sua organização. Isso se desejar que a regra seja aplicada apenas uma maneira, certifique-se de especificá-lo nas condições da regra. Para obter um exemplo, consulte [Cenários comuns de bloqueio de anexo](common-attachment-blocking-scenarios-for-mail-flow-rules-exchange-2013-help.md).

  - **Restringir uma regra baseada em domínio do remetente ou do receptor**
    
    Por padrão, uma nova regra se aplica às mensagens enviadas de ou recebidas em qualquer domínio. Em alguns casos, você deseja que uma regra seja aplicada a todos os domínios, com exceção de um, ou a um domínio. Para obter exemplos, consulte [Criar listas de remetentes bloqueados ou remetente seguro em toda a organização no Office 365](https://technet.microsoft.com/pt-br/library/dn198251\(v=exchg.150\)).

Para obter uma lista completa de todas as condições e exceções que estão disponíveis para regras de transporte, consulte:

  - [Exceções (predicados) e condições de regra de fluxo de email no Exchange Online](https://technet.microsoft.com/pt-br/library/jj919235\(v=exchg.150\))

  - [Condições de regra de transporte (predicados)](mail-flow-rule-conditions-and-exceptions-predicates-in-exchange-2013-exchange-2013-help.md)

  - [Condições de regra de fluxo e email exceções (predicados) no Exchange Online Protection](https://technet.microsoft.com/pt-br/library/jj919234\(v=exchg.150\))

## Saber quando você precisar de duas regras

Às vezes, são necessárias duas regras para fazer o que você deseja. Regras de transporte são processadas na ordem, portanto várias regras podem aplicar a mesma mensagem. Por exemplo, se uma das ações é bloquear a mensagem, e você também tem outra ação que você deseja aplicar, como copiar a mensagem para o gerente do remetente ou alterar o assunto da mensagem de notificação, precisaria duas regras. A primeira regra pode copiar a mensagem para o gerente do remetente e alterar o assunto e a segunda regra pode bloquear a mensagem.

Se você usar as duas regras desta, certifique-se de que as condições sejam idênticas. Para ver exemplos, veja o exemplo 3 no [Cenários comuns de aprovação de mensagem](common-message-approval-scenarios-exchange-2013-help.md), o exemplo 3 em [Cenários comuns de bloqueio de anexo](common-attachment-blocking-scenarios-for-mail-flow-rules-exchange-2013-help.md)e [Avisos de isenção de responsabilidade, assinaturas, rodapés ou cabeçalhos para toda a organização](organization-wide-disclaimers-signatures-footers-or-headers-exchange-online-help.md).

## Não repita uma ação em cada email em uma conversa

A cadeia de email em uma conversa pode incluir muitos mensagens individuais e a ação em cada mensagem do encadeamento de repetição pode ter inconveniente. Por exemplo, se você tiver uma ação como a adição de um aviso de isenção, convém aplicá-la apenas a primeira mensagem no segmento. Em caso afirmativo, adicione uma exceção para mensagens que já inclua o texto de isenção de responsabilidade. Para obter um exemplo, consulte [Avisos de isenção de responsabilidade, assinaturas, rodapés ou cabeçalhos para toda a organização](organization-wide-disclaimers-signatures-footers-or-headers-exchange-online-help.md).

## Saber quando parar o processamento da regra

Em alguns casos, faz sentido para parar o processamento de regra depois que uma regra é correspondida. Por exemplo, se você tiver uma regra para bloquear mensagens com anexos e outro para inserir um aviso de isenção em mensagens que correspondem a um padrão, você provavelmente deve parar regra processamento depois que a mensagem é bloqueada. Não há nenhuma necessidade de uma ação adicional.

Para parar o processamento de regra depois que uma regra for disparada, na regra, marque a caixa de seleção **Parar o processamento de mais regras**.

## Se você tiver muitas palavras-chave ou padrões para corresponder, carregá-los a partir de um arquivo

Por exemplo, talvez você queira impedir a emails que está sendo enviada caso eles contenham uma lista de palavras inaceitáveis ou ruim. Você pode criar um arquivo de texto contendo essas palavras e frases e, em seguida, usar Windows PowerShell para configurar uma regra de transporte que bloqueia as mensagens que usá-los.

O arquivo de texto pode conter expressões regulares para padrões. Essas expressões não diferenciam maiúsculas de minúsculas. As expressões regulares comuns incluem:


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p><strong>Expressão</strong></p></td>
<td><p><strong>Correspondências</strong></p></td>
</tr>
<tr class="even">
<td><p><strong>.</strong></p></td>
<td><p>Qualquer caractere único</p></td>
</tr>
<tr class="odd">
<td><p><strong>*</strong></p></td>
<td><p>Todos os caracteres adicionais</p></td>
</tr>
<tr class="even">
<td><p><strong>\d</strong></p></td>
<td><p>Qualquer dígito decimal</p></td>
</tr>
<tr class="odd">
<td><p>[<em>grupo_de_caracteres</em>]</p></td>
<td><p>Qualquer caractere único em um <em>grupo_de_caracteres</em>.</p></td>
</tr>
</tbody>
</table>


Para obter um exemplo que mostra um arquivo de texto com expressões regulares e os comandos de Windows PowerShellExchange módulo usar, consulte [Usar regras de fluxo de email com base em uma lista de palavras, frases ou padrões de emails de rota](use-mail-flow-rules-to-route-email-based-on-a-list-of-words-phrases-or-patterns-exchange-2013-help.md).

Para saber como especificar os padrões de uso de expressões regulares, consulte [Referência de expressão Regular](https://go.microsoft.com/fwlink/p/?linkid=532394).

