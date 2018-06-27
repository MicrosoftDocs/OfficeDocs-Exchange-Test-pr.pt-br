---
title: 'Resolução de destinatário: Exchange 2013 Help'
TOCTitle: Resolução de destinatário
ms:assetid: 09deda5a-d405-45b1-a3ff-fefd3d76cdea
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Bb430743(v=EXCHG.150)
ms:contentKeyID: 52058785
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Resolução de destinatário

 

_**Aplica-se a:**Exchange Server 2013_

_**Tópico modificado em:**2016-03-17_

*Resolução de destinatário* é o processo de expansão e resolver todos os destinatários de uma mensagem. O ato de resolver os destinatários corresponde a um destinatário para o objeto do Active Directory correspondente na organização do Microsoft Exchange. O ato de expandir os destinatários expande todos os grupos de distribuição em uma lista de destinatários individuais. Resolução de destinatário permite que os limites de mensagem e destinatários alternativos a serem aplicadas corretamente para cada destinatário.

Em uma organização do Microsoft Exchange Server 2013, resolução de destinatário é realizada pelo categorizador no serviço de transporte em servidores de caixa de correio. Categorização em cada mensagem acontece depois que uma mensagem que acabou de chegar é colocada na fila de envio. Resolução de destinatário, além de roteamento e conversão de conteúdo é executada na mensagem antes que a mensagem é colocada em uma fila de entrega. Categorizador executa a resolução de destinatário antes de rotear. O componente do categorizador que é responsável por destinatário resolução frequentemente é chamado para o *resolvedor*.

**Sumário**

Resolução de nível superior

Expansão

Bifurcação e controlando a expansão de destinatário

Diagnósticos de resolução de destinatário

## Resolução de nível superior

*Resolução de nível superior* é o primeiro estágio da resolução do destinatário. Resolução de nível superior associa cada destinatário em uma mensagem de entrada para um objeto de destinatário correspondente no Active Directory. Durante a solução de nível superior, o categorizador cria uma lista que contém o remetente e os endereços de email do destinatário inicial, não expandidos que existirem dentro da mensagem. Categorizador usa essa lista de endereços de email para consultar o Active Directory para localizar quaisquer objetos habilitados para email que têm a correspondência de atributos de endereço de email. Quando uma correspondência for encontrada, as propriedades de correspondência de objetos do Active Directory são armazenados em cache para uso posterior. Qualquer restrição de mensagem do remetente também é impostas.

## Endereços de email do destinatário

Resolução de nível superior começa com uma mensagem e a lista inicial, não expandida de destinatários para o *envelope da mensagem*. Envelope da mensagem contém os comandos que são usados para transmitir mensagens entre os servidores de mensagens SMTP. Endereço de email do remetente está contido no comando **MAIL FROM:** . Endereço de email de cada destinatário está contido em um comando separado **RCPT TO:** . O remetente do envelope e o destinatários de envelope geralmente criados a partir do remetente e destinatários dos campos de cabeçalho `To:`, `From:`, `Cc:`e `Bcc:` no cabeçalho da mensagem. No entanto, isso não é sempre true. Os campos de cabeçalho `To:`, `From:`, `Cc:`e `Bcc:` em uma mensagem são facilmente falsificados e podem não corresponder ao remetente real ou endereços de email do destinatário que foram usados para transmitir a mensagem.

## Endereços de email encapsulado

Endereços de email SMTP padrão siga as especificações do RFC 2821 e RFC 2822, como chris@contoso.com, por exemplo. No entanto, um endereço de email também pode ser um endereço de email não SMTP encapsulado dentro de um endereço SMTP válido. O Exchange oferece suporte a endereços encapsulados que usam o método de encapsulamento de endereço de encapsulado de conector de email da Internet (IMCEA).

Esse método de encapsulamento requer a codificação de quaisquer caracteres inválidos nos endereços de email SMTP. Caracteres alfanuméricos, o sinal de igual (=) e o hífen (-) não exigem a codificação. Outros caracteres usam a seguinte sintaxe de codificação:

  - Uma barra (/) foi substituída por um caractere de sublinhado (\_).

  - Outros caracteres US-ASCII são substituídos por um sinal de adição (+) e os dois dígitos do seu valor ASCII são escritos em hexadecimal. Por exemplo, o caractere de espaço tem o valor codificado `+20`.

O método de encapsulamento IMCEA usa a seguinte sintaxe: `IMCEA<Type>-<address>@<domain>`

O espaço reservado \<*Type*\> identifica o tipo de endereçamento não SMTP, por exemplo `EX`, `X400`ou `FAX`.


> [!TIP]
> Embora <CODE>SMTP</CODE> e <CODE>X500</CODE> são valores válidos teoricamente para &lt;<EM>Type</EM>&gt;, resolução de destinatário do Exchange rejeita todos os endereços IMCEA codificado que usam qualquer um desses tipos.



Espaço reservado \<*address*\> é o endereço original codificado. O espaço reservado \<*domain*\> representa o domínio SMTP que é usado para encapsular o endereçamento não SMTP, por exemplo, contoso.com

Com o método de encapsulamento IMCEA, endereços são unencapsulated somente quando o domínio corresponde o domínio autoritativo da padrão na organização do Exchange. Para obter mais informações sobre domínios aceitos, consulte [Domínios aceitos](accepted-domains-exchange-2013-help.md).

O comprimento máximo para um endereço de email SMTP no Exchange é 571 caracteres. Esse limite inclui o seguinte:

  - 315 caracteres para a parte do nome do endereço

  - 255 caracteres para o nome de domínio

  - O sinal de arroba (@) caractere que separa a parte do nome do endereço do nome de domínio

Observe que Exchange não dá suporte a mensagens que são codificadas com o método de encapsulamento IMCEA quando a parte do nome do endereço excede 315 caracteres, mesmo se o endereço de email completo é menor que 571 caracteres.

## Resolução de endereço

Para cada mensagem, o endereço de email do remetente e todos os endereços de email do destinatário são adicionados a uma lista que tiver usado para consultar o Active Directory. Todos os endereços encapsulados são unencapsulated antes que são adicionados à lista de endereços de email. A consulta do Active Directory é realizada em até 20 endereços de email por vez. Se a consulta do Active Directory encontra quaisquer erros transitórios, a mensagem é retornada para a fila de envio e adiada para a hora em que é especificada pela chave *ResolverRetryInterval* em `%ExchangeInstallPath%Bin\EdgeTransport.exe.config` aplicativo arquivo de configuração XML que tenha associado ao serviço de transporte do Microsoft Exchange. O valor padrão é 30 minutos.

A tabela a seguir descreve os objetos de destinatário são encontrados no Active Directory. Para obter mais informações sobre tipos de destinatário do Exchange, consulte [Destinatários](recipients-exchange-2013-help.md).

### Objetos de destinatário no Active Directory

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Tipo de destinatário do Active Directory</th>
<th>Descrição</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>DistributionGroup</p></td>
<td><p>Qualquer objeto de grupo habilitado para email. Os tipos de objeto do grupo de distribuição são:</p>
<ul>
<li><p><strong>MailUniversalDistributionGroup</strong>   Um objeto de grupo de distribuição universal</p></li>
<li><p><strong>MailUniversalSecurityGroup</strong>   Um objeto (USG) do grupo de segurança universal que tenha um endereço de email</p></li>
<li><p><strong>MailNonUniversalGroup</strong>   Um objeto de grupo de segurança local ou de um objeto de grupo de segurança global que tenha um endereço de email</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>DynamicDistributionGroup</p></td>
<td><p>Um objeto que tem a classe do Active Directory <strong>msExchDynamicDistributionList</strong>. Para obter mais informações, consulte <a href="manage-dynamic-distribution-groups-exchange-2013-help.md">Gerenciar grupos dinâmicos de distribuição</a>.</p></td>
</tr>
<tr class="odd">
<td><p>Caixa de Correio</p></td>
<td><p>Um objeto de usuário que tenha um endereço de email e um parâmetro definido <em>Database</em></p></td>
</tr>
<tr class="even">
<td><p>MailUser</p></td>
<td><p>Um objeto de usuário que tenha um endereço de email sem um parâmetro definido <em>Database</em> . Para obter mais informações, consulte <a href="manage-mail-users-exchange-2013-help.md">Gerenciar usuários de email</a>.</p></td>
</tr>
<tr class="odd">
<td><p>MailContact</p></td>
<td><p>Um objeto de contato que possui um endereço de email. Normalmente, um contato de email é usado para destinatários fora da organização do Exchange. Um contato de email também é usado em ambientes do Exchange entre florestas. Para obter mais informações, consulte <a href="manage-mail-contacts-exchange-2013-help.md">Gerenciar contatos de email</a>.</p></td>
</tr>
<tr class="even">
<td><p>MailPublicFolder</p></td>
<td><p>Um objeto de pasta pública que tenha um endereço de email.</p></td>
</tr>
<tr class="odd">
<td><p>MicrosoftExchangeRecipient</p></td>
<td><p>Um objeto que tem a classe do Active Directory <strong>msExchExchangeServerRecipient</strong>. Para obter mais informações sobre o objeto de destinatário do Microsoft Exchange, consulte <a href="recipients-exchange-2013-help.md">Destinatários</a>.</p></td>
</tr>
<tr class="even">
<td><p>SystemAttendantMailbox</p></td>
<td><p>Um objeto que tem a classe do Active Directory <strong>exchangeAdminService</strong>. Deve haver apenas um correio Atendedor do sistema na organização do Exchange.</p></td>
</tr>
<tr class="odd">
<td><p>SystemMailbox</p></td>
<td><p>Um objeto de usuário que tenha um endereço de email e que esteja localizado no contêiner objetos do sistema do Microsoft Exchange. Deve haver uma caixa de correio do sistema para cada banco de dados de caixa de correio na organização do Exchange.</p></td>
</tr>
</tbody>
</table>


Um objeto que contém as propriedades críticas ausentes ou incorretos é classificado pela consulta do Active Directory como um objeto inválido. Por exemplo, um objeto de grupo dinâmico de distribuição sem um endereço de email é considerado inválido. As mensagens enviadas a destinatários que são classificados como objetos inválidos geram um relatório de falha na entrega (NDR).

Para cada endereço de email, uma única consulta inicial é executada para todas as propriedades de destinatário possíveis, como os identificadores de destinatário, tipo de destinatário, limites de mensagem, endereços de email e destinatários alternativos. As propriedades aplicáveis para o destinatário são armazenados em cache para uso posterior. Resolução de destinatário classifica os destinatários com base nas semelhanças em como os destinatários forem resolvidos e semelhança de propriedades de destinatário do aplicáveis.

O filtro LDAP que será usado para resolução de endereço está descrito a seguir:

  - Para o tipo de endereço de email **EX** , o filtro LDAP baseia-se no atributo do Active Directory **legacyExchangeDN** do destinatário ou o destinatário **proxyAddresses** atributo do Active Directory. O atributo do Active Directory **legacyExchangeDN** tem precedência.

  - Para todos os outros tipos de endereços do email, o atributo do Active Directory de destinatário **proxyAddresses** é usado como o filtro LDAP.

Se o endereço de email que é usado na mensagem não coincidir com o endereço SMTP principal do objeto do Active Directory correspondente, categorizador reconfigure o endereço de email na mensagem para coincidir com o endereço SMTP principal. O endereço de email original será salva na entrada `ORCPT=` no comando **RCPT TO:** no envelope da mensagem.

## Restrições de remetente da mensagem

O tamanho que é usado para a restrição de tamanho de mensagem do remetente é o valor do **X-MS-Exchange-organização-OriginalSize:** campo de cabeçalho no cabeçalho da mensagem. Exchange usa esse campo de cabeçalho para registrar o tamanho da mensagem original da mensagem quando ele inserido a organização do Exchange. Sempre que a mensagem será comparada os limites de tamanho de mensagem especificado, o valor mais baixo do tamanho da mensagem atual ou o cabeçalho de tamanho da mensagem original é usado. O tamanho da mensagem pode alterar devido à conversão de conteúdo, codificação e processamento de agente. Se esse campo de cabeçalho não existir, ele é criado usando-se o valor de tamanho de mensagem atual. Se a mensagem for muito grande, uma NDR é gerado e processamento de mensagens adicionais é interrompido.

O limite de destinatário do remetente só é imposto no serviço de transporte no primeiro servidor de caixa de correio que processa a mensagem. A contagem de destinatários de envelope de mensagem original, não-expandida é comparada com o limite de destinatário do remetente. A contagem de destinatários de envelope de mensagem original, não-expandida é usada para evitar os problemas de entrega de mensagem parcial ocorreram no Microsoft Exchange Server 2003 quando as listas de distribuição aninhados usado servidores expansão remoto.

O remetente da mensagem e todos os destinatários são marcados como resolvidos por carimbo uma propriedade estendida na mensagem. Esta propriedade estendida permite a mensagem para ignorar a resolução de nível superior se a mensagem deve passar resolução de destinatário novamente. Uma mensagem pode ter atravessar resolução de destinatário novamente, porque o serviço de transporte do Microsoft Exchange reiniciado.

Voltar ao início

## Expansão

Expansão ocorre após a resolução de nível superior. Expansão completamente expande níveis aninhados de destinatários para destinatários individuais. Expansão pode exigir várias viagens durante o processo de expansão para expandir todos os destinatários. Nem todos os destinatários precisam ser expandido. No entanto, todos os destinatários devem passar o processo de expansão. O processo de expansão também impõe restrições de destinatário de mensagem para todos os tipos de destinatários.

A lista a seguir descreve os tipos de destinatários que exigem a expansão:

  - **Grupos de distribuição e grupos dinâmicos de distribuição**   Grupos de distribuição são expandidos com base em **memberOf** propriedade do Active Directory. Grupos dinâmicos de distribuição são expandidos usando a definição de consulta do Active Directory. Se o parâmetro *ExpansionServer* estiver definido no grupo, o grupo não está expandido pelo servidor atual. O grupo de distribuição é encaminhado para o servidor especificado para expansão.
    

    > [!TIP]
    > Se você selecionar um servidor de transporte específica em sua organização, como o servidor de expansão, o uso do grupo de distribuição se torna depende da disponibilidade do servidor de expansão. Se o servidor de expansão não estiver disponível, todas as mensagens enviadas para o grupo de distribuição não podem ser entregue. Se você planeja usar servidores específicos de expansão para seus grupos de distribuição, para reduzir o risco de interrupção do serviço, você deve considerar a implementação de soluções de alta disponibilidade para esses servidores.



  - **Destinatários alternativos**   O parâmetro *ForwardingAddress* pode ser definido em caixas de correio e pastas públicas habilitadas para email. O parâmetro *ForwardingAddress* redireciona todas as mensagens para o destinatário alternativo especificado. Isso é conhecido como um *encaminhadas destinatário*. Quando um endereço de entrega alternativo for especificado no parâmetro *ForwardingAddress* e o parâmetro *DeliverToMailboxAndForward* é definido como `$true`, a mensagem é entregue ao destinatário original e o destinatário alternativo. Isso é conhecido como *entregues e encaminhadas destinatário*.

  - **Cadeias de contato**   *Entre em contato com a cadeia* é um usuário de email ou contato de email que tenha o parâmetro *ExternalEmailAddress* definido como o endereço de email do destinatário outro na organização do Exchange.

## Detecção de loops de destinatário

Como a distribuição cadeias de contatos, alternativos destinatários e grupos são expandidas, categorizador procura *loops de destinatário*. Um loop de destinatário é um problema de configuração de destinatário que faz com que a entrega da mensagem para os mesmos destinatários em um círculo infinito. A lista a seguir descreve os diferentes tipos de loops de destinatário:

  - **Loop de destinatário inofensiva**   Um loop de destinatário inofensivo resulta na entrega de mensagem bem-sucedida. A lista a seguir descreve os dois cenários quando ocorrerem inofensivas loops de destinatário:
    
      - Quando dois grupos de distribuição contenham um outro como membros.
    
      - Quando as caixas de correio ou pastas públicas habilitadas para email são definidas para entregar e encaminhar uns aos outros. Isso acontece quando o parâmetro *DeliverToMailboxAndForward* de ambos os destinatários é definido como `$true` e o parâmetro *ForwardingAddress* é definido para um outro.
    
    Quando for detectado um loop de destinatário inofensivo, a mensagem é entregue ao destinatário, mas nenhum tentativas adicionais são feitas para entregar a mensagem ao destinatário mesmo.

  - **Executar um loop destinatário quebrado**   Um loop de destinatário desfeito não pode resultar em entrega de mensagem bem-sucedida. Um exemplo de um loop de destinatário quebrado é quando caixas de correio ou pastas públicas habilitadas para email tem o parâmetro *ForwardingAddress* definido como entre si. Quando o categorizador detecta um loop de destinatário quebrado, interrompe a atividade de expansão para o destinatário atual e uma NDR é gerado para o destinatário.

Detecção de loops destinatários não impede a entrega da mensagem duplicados. Por exemplo, C do grupo de distribuição observarão a entrega da mensagem duplicados se as seguintes condições forem verdadeiras:

  - Grupo de distribuição B e C do grupo de distribuição são membros do grupo de distribuição A.

  - Grupo de distribuição C também é membro do B. de grupo de distribuição

## Redirecionamento de relatório de entrega para grupos de distribuição

Quando um grupo de distribuição é expandido, o tipo de mensagem é verificado para determinar se ele é uma mensagem de relatório de entrega. Se a mensagem for um relatório de entrega, as configurações de redirecionamento do grupo de distribuição são verificadas para determinar se o redirecionamento do relatório de entrega é necessário. Convém suprimir os relatórios de entrega porque os relatórios de entrega divulgar informações indesejadas sobre sua associação e o grupo de distribuição.

A lista a seguir descreve as configurações de redirecionamento de relatório de entrega que estão disponíveis para grupos de distribuição e grupos dinâmicos de distribuição:

  - **ReportToManagerEnabled**   Esse parâmetro permite que os relatórios de entrega sejam enviadas para o gerente do grupo de distribuição. Valores válidos são `$true` ou `$false`. O valor padrão é `$false`. Para um grupo de distribuição, o gerente é controlado pelo parâmetro *ManagedBy* no cmdlet **Set-Group** . Para um grupo dinâmico de distribuição, o gerente é controlado pelo parâmetro *ManagedBy* no cmdlet **Set-DynamicDistributionGroup** .

  - **ReportToOriginatorEnabled**   Esse parâmetro permite que os relatórios de entrega sejam enviadas para o remetente das mensagens de email enviadas para este grupo de distribuição. Valores válidos são `$true` ou `$false`. O valor padrão é `$true`.
    

    > [!TIP]
    > Os valores do parâmetro <EM>ReportToManagerEnabled</EM> e <EM>ReportToOriginatorEnabled</EM> não podem ser <CODE>$true</CODE>. Se um parâmetro for definido como <CODE>$true</CODE>, o outro deve ser definido como <CODE>$false</CODE>. Os valores dos dois parâmetros podem ser <CODE>$false</CODE>. Suprime o redirecionamento de todos os de todas as mensagens de relatório de entrega.



A lista a seguir descreve as mensagens de relatório de entrega disponíveis:

  - **Confirmação de entrega (DR)**   Este relatório confirma que uma mensagem foi entregue ao destinatário pretendido.

  - **Notificação de status de entrega (DSN)**   Este relatório descreve o resultado de uma tentativa de enviar uma mensagem. Para obter mais informações sobre mensagens DSN, consulte [DSNs e notificações de falha na entrega no Exchange 2013](dsns-and-ndrs-in-exchange-2013-exchange-2013-help.md).

  - **Notificação de disposição de mensagem (MDN)**   Este relatório descreve o status de uma mensagem após ter sido entregue com êxito para um destinatário. Uma notificação de leitura (RN) e uma notificação de leitura não (NRN) são exemplos de uma mensagem de MDN. Mensagens MDN são definidas na RFC 2298 e são controladas pelo campo de cabeçalho **Disposition-Notification-To:** no cabeçalho da mensagem. Configurações de MDN que usam o campo de cabeçalho `Disposition-Notification-To:` são compatíveis com muitos servidores de mensagem diferente. Configurações de MDN também podem ser definidas usando propriedades MAPI no Microsoft Outlook e Exchange.

  - **Relatório de não-entrega (NDR)**   Este relatório indica o remetente da mensagem que a mensagem não pôde ser entregue aos destinatários especificados.

  - **Notificação de leitura não (NRN)**   Este relatório indica que uma mensagem foi excluída antes que ele foi lido.

  - **Ausência temporária (OOF)**   Este relatório indica que o destinatário não responde às mensagens de email. As datas de ausência temporária acrônimo volta para o Microsoft original onde a notificação correspondente era chamada de "sem facility." do sistema de mensagens

  - **Notificação de leitura (RN)**   Este relatório indica que uma mensagem foi lido.

  - **Relatório de cancelamento**   Este relatório indica o status de uma solicitação de cancelamento para um destinatário específico. Uma solicitação de cancelamento é quando um remetente tenta recuperar uma mensagem enviada usando o Outlook.

Quando uma mensagem de relatório de entrega é enviada a um grupo de distribuição, as configurações a seguir causam a mensagem de relatório a ser excluído:

  - Redirecionamento de relatório não está definido. Como alternativa, o redirecionamento de relatório é definido como o remetente da mensagem.

  - Redirecionamento de relatório é definido como o gerente do grupo de distribuição e a mensagem de relatório de entrega não é uma NDR.

Quando uma mensagem de relatório de entrega é enviada a um grupo de distribuição, a mensagem de relatório de entrega pode ser entregue ao gerente do grupo de distribuição. Isso acontece quando o redirecionamento de relatório é definido como o gerente do grupo de distribuição e a mensagem de relatório é um NDR.

Quando uma mensagem que não é uma mensagem de relatório de entrega é enviada a um grupo de distribuição, a mensagem é entregue para os membros do grupo de distribuição. As configurações de solicitação do relatório estão resumidas na lista a seguir:

  - Se o redirecionamento do relatório estiver definido como o remetente da mensagem, as configurações de solicitação de relatório não são modificadas.

  - Se o redirecionamento de relatório não estiver definido, todas as configurações de solicitação de relatório são suprimidas. A entrada `NOTIFY=NEVER` é adicionada à **RCPT TO:** para cada destinatário no envelope da mensagem.

  - Se o redirecionamento de relatório é definido como o gerente do grupo de distribuição, todas as configurações de solicitação de relatório são suprimidas exceto mensagens NDR que são enviadas para o gerente do grupo de distribuição.

## Restrições de mensagens nos destinatários

O processo de expansão também impõe restrições de qualquer mensagem que estiverem configuradas para destinatários. Essas restrições podem ser configuradas individualmente para cada destinatário ou empresariais para todos os servidores de transporte de Hub na organização do Exchange. A tabela a seguir descreve as restrições de mensagem que estão configuradas para destinatários.

### Restrições de mensagens nos destinatários

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
<th>Descrição</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>Set-DistributionGroup</strong></p>
<p><strong>Set-DynamicDistributionGroup</strong></p>
<p><strong>Set-Mailbox</strong></p>
<p><strong>Set-MailContact</strong></p>
<p><strong>Set-MailPublicFolder</strong></p>
<p><strong>Set-MailUser</strong></p>
<p><strong>Set-TransportConfig</strong></p></td>
<td><p><em>MaxReceiveSize</em></p></td>
<td><p>O parâmetro <em>MaxReceiveSize</em> Especifica o tamanho que é usado para as restrições de mensagem que estão configuradas para destinatários é o valor do campo de cabeçalho <strong>X-MS-Exchange-Organization-OriginalSize:</strong> no cabeçalho da mensagem. Exchange usa esse campo de cabeçalho para registrar o tamanho da mensagem original da mensagem quando ele inserido a organização do Exchange. Sempre que a mensagem será comparada os limites de tamanho de mensagem especificado, o valor mais baixo do tamanho da mensagem atual ou o cabeçalho de tamanho da mensagem original é usado. O tamanho da mensagem pode alterar devido à conversão de conteúdo, codificação e processamento de agente. Se esse campo de cabeçalho não existir, ele é criado usando-se o valor de tamanho de mensagem atual. Se a mensagem for muito grande, uma NDR é gerado e processamento de mensagens adicionais é interrompido.</p></td>
</tr>
<tr class="even">
<td><p><strong>Set-DistributionGroup</strong></p>
<p><strong>Set-DynamicDistributionGroup</strong></p>
<p><strong>Set-Mailbox</strong></p>
<p><strong>Set-MailContact</strong></p>
<p><strong>Set-MailPublicFolder</strong></p>
<p><strong>Set-MailUser</strong></p></td>
<td><p><em>RequireSenderAuthenticationEnabled</em></p></td>
<td><p>O parâmetro <em>RequireSenderAuthenticationEnabled</em> requer que todas as mensagens que são enviadas ao destinatário são provenientes de remetentes autenticados. Quando o valor desse parâmetro é definido como <code>$true</code>, mensagens de remetentes não-autenticados são rejeitadas. Todos os remetentes que enviam mensagens para as caixas de correio do sistema e Atendedor do sistema devem ser autenticados.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Set-DistributionGroup</strong></p>
<p><strong>Set-DynamicDistributionGroup</strong></p>
<p><strong>Set-Mailbox</strong></p>
<p><strong>Set-MailContact</strong></p>
<p><strong>Set-MailPublicFolder</strong></p>
<p><strong>Set-MailUser</strong></p></td>
<td><p><em>AcceptMessagesOnlyFromSendersOrMembers</em></p>
<p><em>RejectMessagesFromSendersOrMembers</em></p></td>
<td><p>O parâmetro <em>AcceptMessagesOnlyFromSendersOrMembers</em> Especifica os remetentes ou grupos de distribuição cujos membros têm permissão para enviar mensagens ao destinatário. Observe que esse parâmetro combina a funcionalidade dos parâmetros <em>AcceptMessagesOnlyFrom</em> e <em>AcceptMessagesOnlyFromDLMembers</em> mais antigos.</p>
<p>O parâmetro <em>RejectMessagesFromSendersOrMembers</em> Especifica os remetentes ou grupos de distribuição cujos membros não têm permissão para enviar mensagens ao destinatário. Observe que esse parâmetro combina a funcionalidade dos parâmetros <em>RejectMessagesFrom</em> e <em>RejectMessagesFromDLMembers</em> mais antigos.</p>
<p>Categorizador verifica a permissão de destinatário em dois passos. A primeira passagem determina se o remetente está presente no parâmetro <em>AcceptOnlyMessagesFromSendersOrMembers</em> ou <em>RejectMessagesFromSendersOrMembers</em> . Se o remetente não foi encontrado em qualquer um dos parâmetros, os grupos de distribuição nesses parâmetros ficam totalmente expandidos. Essa expansão completa dos grupos de distribuição pode levar algum tempo. Recomendamos que você minimizar a profundidade de grupos de distribuição aninhados nesses parâmetros.</p></td>
</tr>
</tbody>
</table>


Certos tipos de mensagens que são enviadas por remetentes autenticados estão isentos de restrições. A lista a seguir descreve as mensagens que são isentas de restrições de destinatário:

  - **Todas as mensagens que são enviadas pelo destinatário do Microsoft Exchange**   Essas mensagens incluem mensagens DSN, relatórios de diário, mensagens de cota e outras mensagens geradas pelo sistema que são enviadas para remetentes de mensagem interna. Para obter mais informações sobre o destinatário da Microsoft, consulte [Destinatários](recipients-exchange-2013-help.md).

  - **Todas as mensagens que são enviadas pelo endereço postmaster externo**   Essas mensagens incluem mensagens DSN e outras mensagens geradas pelo sistema que são enviadas para os remetentes das mensagens externas. Para obter mais informações sobre o endereço do postmaster externo, consulte [Configurar o endereço do postmaster externo](configure-the-external-postmaster-address-exchange-2013-help.md).

Determinados tipos de mensagens são bloqueados quando eles são enviados da organização do Exchange para domínios externos. As configurações são controladas pelos seguintes parâmetros no cmdlet **Set-RemoteDomain** :

  - *AllowedOOFType*

  - *AutoForwardEnabled*

  - *AutoReplyEnabled*

  - *DeliveryReportEnabled*

  - *NDREnabled*

Para obter mais informações, consulte [Domínios remotos](remote-domains-exchange-2013-help.md).

Voltar ao início

## Bifurcação e controlando a expansão de destinatário

Porque a lista completa dos destinatários da mensagem for expandida e resolvida com a resolução de destinatário, há ocasiões quando diferentes cópias da mesma mensagem devem ser criadas. Essas ocasiões são descritas pelos seguintes cenários:

  - **Quando os destinatários da mensagem exigem configurações diferentes de mensagens**   Propriedades de mensagem, como ler confirmações podem precisar ser habilitados para alguns destinatários e bloqueados para outros destinatários. Criar uma nova versão da mensagem que tem propriedades ligeiramente diferentes que a mensagem original é chamada *bifurcação*.

  - **Para limitar o número de destinatários do envelope em uma única mensagem**   O processo de expansão de destinatário pode gerar milhares de destinatários individuais quando os grupos de distribuição grandes são expandidos. No Exchange, ao invés de criar uma única cópia da mensagem que tem milhares de destinatários do envelope, várias cópias da mesma mensagem que tem um número limitado de destinatários do envelope são criadas.

## Bifurcação

Resolução de destinatário bifurca uma mensagem se as seguintes condições forem verdadeiras:

  - Quando o remetente da mensagem em **MAIL FROM:**, no envelope da mensagem, é atualizado. Um exemplo é quando o parâmetro *ReportToManagerEnabled* em um grupo de distribuição tem um valor de `$true`.

  - Quando as mensagens de resposta automática, como DSNs, OOF mensagens e relatórios de cancelamento devem ser suprimidos.

  - Quando os destinatários alternativos são expandidos.

  - Quando um campo de cabeçalho de **Resent-From:** deve ser adicionado ao cabeçalho da mensagem. Reenviadas cabeçalho campos são campos de cabeçalho informativos que podem ser usados para determinar se uma mensagem foi encaminhada por um usuário. Reenviadas cabeçalho campos são usados para que a mensagem é exibida para o destinatário como se ele foi enviado diretamente pelo remetente original. O destinatário pode exibir o cabeçalho da mensagem para descobrir quem encaminhou a mensagem. Reenviadas cabeçalho campos são definidos na seção 3.6.6 da RFC 2822.

  - Quando o histórico da expansão do grupo de distribuição deve ser transmitido.

## Controlando a expansão de destinatário

Quando o número de destinatários expandidos for muito grande, o categorizador divide a mensagem em várias cópias. Isso é feito para reduzir o uso de recursos do sistema durante a expansão da mensagem. O número máximo de destinatários do envelope em uma mensagem é controlado pela chave *ExpansionSizeLimit* no arquivo de configuração do aplicativo `%ExchangeInstallPath%Bin\EdgeTransport.exe.config` . O valor padrão é 1000.


> [!WARNING]
> Recomendamos que você não modifique o valor da chave <EM>ExpansionSizeLimit</EM> em um servidor de transporte do Exchange em um ambiente de produção.



Voltar ao início

## Diagnósticos de resolução de destinatário

Informações de diagnósticos e relatórios para resolução de destinatário são fornecidas pelo contadores de desempenho e entradas de log de rastreamento de mensagens. Essas fontes podem ajudá-lo a identificar e diagnosticar problemas de resolução de destinatário.

## Contadores de desempenho de resolução de destinatário

A tabela a seguir descreve os contadores de desempenho que estão disponíveis para resolução de destinatário.

### Contadores de desempenho de resolução de destinatário

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Nome do contador</th>
<th>Nome de exibição</th>
<th>Descrição</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>AmbiguousRecipientsTotal</p></td>
<td><p>Destinatários ambíguos</p></td>
<td><p>Este é o número total de destinatários ambíguos detectados durante a resolução de destinatário. Destinatários ambíguos são diferentes destinatários que possuem atributos do Active Directory <strong>legacyExchangeDN</strong> correspondentes ou atributos do Active Directory <strong>proxyAddresses</strong> correspondentes.</p></td>
</tr>
<tr class="even">
<td><p>AmbiguousSendersTotal</p></td>
<td><p>Remetentes ambíguos</p></td>
<td><p>Esse é o número de remetentes ambíguos detectados durante a resolução de destinatário. Remetentes ambíguos são diferentes remetentes que possuem atributos do Active Directory <strong>legacyExchangeDN</strong> correspondentes ou atributos do Active Directory <strong>proxyAddresses</strong> correspondentes.</p></td>
</tr>
<tr class="odd">
<td><p>FailedRecipientsTotal</p></td>
<td><p>Destinatários com falha</p></td>
<td><p>Esse é o número de destinatários com falha que foram detectados durante a resolução de destinatário.</p></td>
</tr>
<tr class="even">
<td><p>LoopRecipientsTotal</p></td>
<td><p>Destinatários de loop</p></td>
<td><p>Esse é o número de destinatários que falharam resolução de destinatário por causa de loops de destinatário.</p></td>
</tr>
<tr class="odd">
<td><p>MessagesChippedTotal</p></td>
<td><p>Mensagens processadas</p></td>
<td><p>Este é o número total de cópias da mesma mensagem que foram criados durante a resolução de destinatário para controlar o número de destinatários do envelope em uma única mensagem. No Exchange, esse processo é conhecido como <em>chipping</em>.</p></td>
</tr>
<tr class="even">
<td><p>MessagesCreatedTotal</p></td>
<td><p>Mensagens criadas</p></td>
<td><p>Esse é o número de mensagens que foram criados durante a resolução de destinatário.</p></td>
</tr>
<tr class="odd">
<td><p>MessagesRetriedTotal</p></td>
<td><p>Mensagens repetidas</p></td>
<td><p>Esse é o número de mensagens que foram agendadas para repetição durante a resolução de destinatário.</p></td>
</tr>
<tr class="even">
<td><p>UnresolvedOrgRecipientsTotal</p></td>
<td><p>Destinatários da Org. não resolvidos</p></td>
<td><p>Esse é o número de destinatários de um domínio autoritativo não resolvidos que foram detectados durante a resolução de destinatário.</p></td>
</tr>
<tr class="odd">
<td><p>UnresolvedOrgSendersTotal</p></td>
<td><p>Remetentes da Org. não resolvidos</p></td>
<td><p>Esse é o número de remetentes não resolvidos de um domínio autoritativo detectados durante a resolução de destinatário.</p></td>
</tr>
</tbody>
</table>


## Eventos de resolução de destinatário no log de acompanhamento de mensagens

A tabela a seguir descreve os eventos de resolução de destinatário que são gravados no log de acompanhamento de mensagens.

### Eventos de resolução de destinatário no log de acompanhamento de mensagens

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Evento de rastreamento de mensagem</th>
<th>Descrição</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>EXPANDA</p></td>
<td><p>Esse evento indica que um grupo de distribuição expandido.</p></td>
</tr>
<tr class="even">
<td><p>REDIRECIONAR</p></td>
<td><p>Esse evento indica que uma mensagem enviada para um destinatário de caixa de correio ou um destinatário habilitado para email de pasta pública foi redirecionada para um destinatário alternativo conforme especificado pelo parâmetro <em>ForwardingAddress</em> .</p></td>
</tr>
<tr class="odd">
<td><p>RESOLVER</p></td>
<td><p>Esse evento indica que um endereço de email do destinatário foi alterado para o endereço de email SMTP principal do objeto de destinatário correspondente do Active Directory.</p></td>
</tr>
<tr class="even">
<td><p>TRANSFERIR</p></td>
<td><p>Esse evento indica que bifurcação de mensagem ou chipping ocorreu.</p></td>
</tr>
</tbody>
</table>


Para obter mais informações sobre o rastreamento de mensagens, consulte [Controle de mensagens](message-tracking-exchange-2013-help.md).

