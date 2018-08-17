---
title: 'DSNs e notificações de falha na entrega no Exchange 2013: Exchange 2013 Help'
TOCTitle: DSNs e notificações de falha na entrega no Exchange 2013
ms:assetid: 8e91de84-76fa-49b2-898c-c5eface76560
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Bb232118(v=EXCHG.150)
ms:contentKeyID: 50486138
ms.date: 01/10/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# DSNs e notificações de falha na entrega no Exchange 2013

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2016-12-09_


> [!NOTE]
> Se precisar de ajuda com notificações de falha na entrega no Office 365 ou no Exchange Online, confira <A href="https://go.microsoft.com/fwlink/p/?linkid=524931">Notificações de falha na entrega de email no Office 365</A>.



Quando há um problema na entrega de uma mensagem, o Exchange Server 2013 envia uma notificação de status de entrega (DSN) para o remetente da mensagem. Essas mensagens geradas pelo sistema também são conhecidas como mensagens de devolução e contêm um código de erro, detalhes técnicos sobre o problema e, às vezes, as etapas de solução de problemas para o remetente da mensagem. As mensagens de Notificação de Falha na Entrega (NDR) são um tipo comum de notificação de status. Este tópico para administradores de email descreve causas prováveis e soluções para os vários códigos de status de NDR. Ele também mostra como ler e interpretar mensagens de NDR.

**Sumário**

Códigos de status avançados comuns

Seções da notificação de falha na entrega

Exemplos de mensagens de notificação de falha na entrega

## Códigos de status avançados comuns

A tabela a seguir contém uma lista dos códigos de status avançados retornados em notificações de falha na entrega para as falhas mais comuns de entrega de mensagem.


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Código de status avançado</th>
<th>Descrição</th>
<th>Causa possível</th>
<th>Additional information</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>4.3.1</p></td>
<td><p><code>Insufficient system resources</code></p></td>
<td><p>Ocorreu um erro de memória insuficiente. Um problema de recurso, como um disco cheio, pode causar esse problema.</p>
<p>Em vez de um erro de disco cheio, talvez um erro de memória insuficiente seja exibido.</p></td>
<td><p>Verifique se o servidor do Exchange tem armazenamento em disco suficiente.</p></td>
</tr>
<tr class="even">
<td><p>4.3.2</p></td>
<td><p><code>System not accepting network messages</code></p></td>
<td><p>Essa notificação de falha na entrega é gerada quando uma fila está congelada.</p></td>
<td><p>Você pode resolver essa condição descongelando a fila.</p></td>
</tr>
<tr class="odd">
<td><p>4.4.1</p></td>
<td><p><code>Connection timed out</code></p></td>
<td><p>O servidor de destino não está respondendo. Condições de rede transitórias podem causar esse erro. O servidor do Exchange tenta automaticamente se conectar ao servidor novamente e entregar a mensagem. Se a entrega falhar após várias tentativas, uma notificação de falha na entrega com um código de falha permanente é gerada.</p></td>
<td><p>Monitore a situação. Esse pode ser um problema transitório que será solucionado automaticamente.</p></td>
</tr>
<tr class="even">
<td><p>4.4.2</p></td>
<td><p><code>Connection dropped</code></p></td>
<td><p>Uma conexão foi perdida entre os servidores. Condições de rede transitória ou um servidor que está tendo problemas podem causar esse erro. O servidor remetente tentará entregar a mensagem por um período de tempo específico e gerará relatórios de status adicionais.</p></td>
<td><p>Monitora a situação enquanto o servidor tenta entregar novamente. Esse pode ser um problema transitório que será solucionado automaticamente.</p>
<p>Essa situação pode também ocorrer quanto o limite de tamanho da mensagem para a conexão for atingido, ou se a taxa de envio de mensagens para o endereço IP cliente exceder o limite configurado.</p></td>
</tr>
<tr class="odd">
<td><p>4.4.7</p></td>
<td><p><code>Message expired</code></p></td>
<td><p>A mensagem na fila expirou. O servidor de envio tentou retransmitir ou entregar a mensagem, mas a ação não foi concluída antes de ocorrer a expiração da mensagem. Essa mensagem pode também indicar que o limite do cabeçalho da mensagem foi atingido em um servidor remoto ou algum outro tempo limite de protocolo ocorreu ao se comunicar com o servidor remoto.</p></td>
<td><p>Essa mensagem geralmente indica um problema no servidor de recebimento. Verifique a validade do endereço de destinatário e determine se o servidor de recebimento está configurado corretamente para receber mensagens.</p>
<p>Talvez seja preciso reduzir o número de destinatários no cabeçalho da mensagem para o host do qual você está recebendo esse erro. Se você enviar a mensagem outra vez, ela será colocada na fila novamente. Se o servidor de recebimento estiver disponível, a mensagem será entregue.</p></td>
</tr>
<tr class="even">
<td><p>5.0.0</p></td>
<td><p><code>HELO / EHLO requires domain address</code></p></td>
<td><p>Essa situação é uma falha permanente. Causas possíveis:</p>
<ul>
<li><p>Não há roteador para o espaço de endereço fornecido; por exemplo, um conector SMTP está configurado, mas esse endereço não corresponde.</p></li>
<li><p>O DNS retornou um host autoritativo que não foi encontrado para o domínio.</p></li>
<li><p>Ocorreu um erro SMTP.</p></li>
</ul></td>
<td><p>Entre algumas das resoluções possíveis:</p>
<ul>
<li><p>Em um ou mais conectores SMTP, adicione um valor de asterisco (<strong>*</strong>) como o espaço de endereço SMTP.</p></li>
<li><p>Verifique se o DNS está funcionando.</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>5.1.0</p></td>
<td><p><code>Sender denied</code></p></td>
<td><p>Essa notificação de falha na entrega é causada por uma falha geral (falha de endereço incorreto). Um endereço de email ou outro atributo não pôde ser encontrado nos Serviços de Domínio do Active Directory. As entradas de contato sem o atributo <strong>targetAddress</strong> podem causar esse problema. Outra causa possível pode ser que o atributo <strong>homeMDB</strong> de um usuário não pôde ser determinado. O atributo <strong>homeMDB</strong> corresponde ao servidor Exchange no qual a caixa de correio do usuário reside.</p>
<p>Outra causa comum dessa notificação de falha na entrega é quando você usa o Microsoft Outlook para salvar a mensagem de email como um arquivo e alguém abriu a mensagem offline e respondeu à mensagem. A propriedade da mensagem só preserva o atributo <strong>legacyExchangeDN</strong> quando o Outlook entrega a mensagem e, portanto, a pesquisa pode falhar.</p></td>
<td><p>Ou o endereço do destinatário está formatado incorretamente, ou o destinatário não pode ser resolvido corretamente. A primeira etapa do processo de resolução do erro é verificar o endereço do destinatário e enviar a mensagem novamente.</p></td>
</tr>
<tr class="even">
<td><p>5.1.1</p></td>
<td><p><code>Bad destination mailbox address</code></p></td>
<td><p>Essa falha pode ser causada pelas seguintes condições:</p>
<ul>
<li><p>O endereço de email do destinatário foi digitado incorretamente pelo remetente.</p></li>
<li><p>Não existe um destinatário no sistema de email de destino.</p></li>
<li><p>A caixa de correio do destinatário foi movida e o cache do destinatário do Outlook no computador do remetente não foi atualizado.</p></li>
<li><p>Existe um nome de domínio (DN) legado inválido para o Serviço de Domínio do Active Directory da caixa de correio do destinatário.</p></li>
</ul></td>
<td><p>Esse erro normalmente ocorre quando o remetente da mensagem digita o endereço de email do destinatário de forma incorreta. O remetente deve verificar o endereço de email do destinatário e enviar a mensagem novamente. Esse erro também pode ocorrer caso o endereço de email do destinatário estivesse correto anteriormente, mas tenha sido alterado ou removido do sistema de emails de destino.</p>
<p>Se o remetente da mensagem estiver na mesma organização do Exchange que o destinatário e a caixa de correio ainda existir, determine se a caixa de correio do destinatário foi relocada para um novo servidor de emails. Se for esse o problema, o Outlook poderá não ter atualizado corretamente o cache de destinatários. Instrua o remetente a remover o endereço do destinatário do cache de destinatários do Outlook e a criar uma nova mensagem. O reenvio da mensagem original resultará na mesma falha.</p>
<p>Outros problemas podem causar este erro, como um nome diferenciado (DN) legado inválido nos Serviços de Domínio do Active Directory. Examine e corrija o antigo DN da caixa de correio do destinatário. Em seguida, instrua o remetente a remover o endereço do destinatário do cache de destinatários do Outlook e a criar uma nova mensagem. O reenvio da mensagem original resultará na mesma falha.</p></td>
</tr>
<tr class="odd">
<td><p>5.1.2</p></td>
<td><p><code>Invalid X.400 address</code></p></td>
<td><p>O destinatário tem um endereço não SMTP que não corresponde a um destino. O endereço não parece ser local, e não há conectores configurados com os espaços de endereço que contêm o endereço do destinatário.</p></td>
<td><p>Verifique se o endereço do destinatário foi inserido corretamente. Se o endereço do destinatário estiver em um sistema de email não SMTP ao qual você deseja especificamente fornecer a entrega de mensagens, você precisará adicionar o tipo apropriado de conector à sua topologia e configurá-lo para fornecer serviço ao sistema de email do destinatário.</p></td>
</tr>
<tr class="even">
<td><p>5.1.3</p></td>
<td><p><code>Invalid recipient address</code></p></td>
<td><p>Essa mensagem indica que o endereço do destinatário é exibido incorretamente na mensagem.</p></td>
<td><p>Ou o endereço do destinatário está formatado incorretamente ou o endereço do destinatário não pode ser resolvido corretamente. A primeira etapa do processo de resolução do erro é verificar o endereço do destinatário e enviar a mensagem novamente.</p>
<p>Além disso, examine a diretiva de destinatário SMTP e garanta que cada domínio de email para o qual você deseja aceitar mensagens seja exibido corretamente.</p></td>
</tr>
<tr class="odd">
<td><p>5.1.4</p></td>
<td><p><code>Destination mailbox address ambiguous</code></p></td>
<td><p>Dois ou mais destinatários na organização do Exchange possuem o mesmo endereço.</p></td>
<td><p>Esse erro normalmente ocorre por causa de um erro de configuração nos Serviços de Domínio do Active Directory. Possivelmente, por causa de problemas de replicação, dois objetos de destinatário nos Serviços de Domínio do Active Directory possuem o mesmo endereço SMTP ou endereço Exchange Server (EX).</p></td>
</tr>
<tr class="even">
<td><p>5.1.7</p></td>
<td><p><code>Invalid address</code></p></td>
<td><p>O remetente tem um endereço SMTP ausente ou malformado, o atributo <strong>mail</strong> no serviço de diretório. O item de mensagens não pode ser entregue sem um atributo <strong>mail</strong> válido.</p></td>
<td><p>Verifique a estrutura de diretório do remetente e determine se o atributo <strong>mail</strong> existe.</p></td>
</tr>
<tr class="odd">
<td><p>5.2.1</p></td>
<td><p><code>Mailbox cannot be accessed</code></p></td>
<td><p>A caixa de correio não pode ser acessada. A caixa de correio pode ficar offline, desabilitada ou a mensagem foi colocada em quarentena por uma regra.</p></td>
<td><p>Verifique se o banco de dados de destinatário está online, a caixa de correio do destinatário está desabilitada ou a mensagem foi colocada em quarentena.</p></td>
</tr>
<tr class="even">
<td><p>5.2.2</p></td>
<td><p><code>Mailbox full</code></p></td>
<td><p>A caixa de correio do destinatário excedeu sua cota de repositório e não pode mais aceitar novas mensagens.</p></td>
<td><p>Esse erro ocorre quando a caixa de correio do destinatário excedeu sua cota de repositório. O destinatário deve reduzir o tamanho da caixa de correio, ou o administrador deve aumentar a cota de repositório para que a entrega possa ser feita com êxito.</p></td>
</tr>
<tr class="odd">
<td><p>5.2.3</p></td>
<td><p><code>Message too large</code></p></td>
<td><p>A mensagem é muito grande e a cota local foi excedida. Por exemplo, um usuário do Exchange remoto pode ter uma restrição no tamanho máximo de uma mensagem de entrada.</p></td>
<td><p>Envie a mensagem novamente sem anexos ou defina o limite do lado do servidor ou do lado do cliente que permita um limite de tamanho de mensagem maior.</p></td>
</tr>
<tr class="even">
<td><p>5.2.4</p></td>
<td><p><code>Mailing list expansion problem</code></p></td>
<td><p>O destinatário é uma lista de distribuição dinâmica configurada incorretamente. Ou a cadeia de caracteres de filtro ou o DN base da lista de distribuição dinâmica é inválido.</p></td>
<td><p>Defina o nível de log de eventos do categorizador pelo menos no nível mínimo e envie outra mensagem para a lista de distribuição dinâmica. Verifique o log de eventos do aplicativo para um evento 6025 ou um evento 6026 detalhando qual atributo está configurado incorretamente no objeto da lista de distribuição dinâmica.</p></td>
</tr>
<tr class="odd">
<td><p>5.3.3</p></td>
<td><p><code>Unrecognized command</code></p></td>
<td><p>Quando o servidor remoto do Exchange atinge a capacidade de seu repositório em disco para conter mensagens, ele pode responder com essa notificação de falha na entrega. Esse erro geralmente ocorre quando o servidor remetente está enviando mensagens com um comando ESMTP BDAT. Esse erro também indica um possível erro de protocolo SMTP.</p></td>
<td><p>Verifique se o servidor remoto tem capacidade de repositório suficiente para conter mensagens. Verifique o log do SMTP.</p></td>
</tr>
<tr class="even">
<td><p>5.3.4</p></td>
<td><p><code>Message too big for system</code></p></td>
<td><p>A mensagem excede um limite de tamanho configurado em um banco de dados de transporte ou de caixa de correio e não pode ser aceita. Essa falha pode ser gerada tanto pelo sistema de envio de emails quanto pelo sistema de email do destinatário.</p></td>
<td><p>Esse erro ocorre quando o tamanho da mensagem enviada pelo remetente excede o tamanho máximo permitido para mensagens ao passar por um componente de transporte ou um banco de dados de caixa de correio. O remetente deve reduzir o tamanho da mensagem para que ela seja entregue com êxito. Para saber mais sobre como configurar os limites de tamanho de mensagens, veja <a href="message-size-limits-exchange-2013-help.md">Limites de tamanhos de mensagens</a>.</p></td>
</tr>
<tr class="odd">
<td><p>5.3.5</p></td>
<td><p><code>System incorrectly configured</code></p></td>
<td><p>Uma situação de loop de email foi detectada, o que significa que o servidor está configurado para enviar mensagens em loop de volta para si mesmo.</p></td>
<td><p>Verifique se há loops na configuração dos conectores do servidor e garanta que cada conector está definido por uma porta de entrada exclusiva. Se houver vários servidores virtuais, certifique-se de que nenhum está definido como &quot;Todos Não Atribuídos&quot;.</p></td>
</tr>
<tr class="even">
<td><p>5.4.4</p></td>
<td><p><code>Invalid arguments</code></p></td>
<td><p>Essa notificação de falha na entrega ocorre se não houver roteador para entrega de mensagens, ou se o categorizador não puder determinar o destino do próximo salto.</p></td>
<td><p>Verifique se o nome de domínio especificado é válido e se um registro MX (servidor de mensagens) existe.</p></td>
</tr>
<tr class="odd">
<td><p>5.4.6</p></td>
<td><p><code>Routing loop detected</code></p></td>
<td><p>Um erro de configuração causou um loop de email. Por padrão, após 20 iterações de um loop de email, o Exchange interrompe o loop e gera uma notificação de falha na entrega para o remetente da mensagem.</p></td>
<td><p>Esse erro ocorre quando a entrega de uma mensagem gera outra mensagem em resposta. Essa mensagem então gera uma terceira mensagem, e o processo se repete, criando um loop. Para ajudar a proteger contra o esgotamento de recursos do sistema, o Exchange interrompe o loop de email após 20 iterações. Loops de email geralmente são criados por causa de um erro de configuração no servidor de envio de emails, no servidor de recebimento de emails, ou em ambos. Verifique a configuração das regras da caixa de correio do destinatário e do remetente para determinar se o encaminhamento automático de mensagens está habilitado.</p></td>
</tr>
<tr class="even">
<td><p>5.5.2</p></td>
<td><p><code>Send hello first</code></p></td>
<td><p>Um erro SMTP genérico ocorre quando comandos SMTP são enviados fora de sequência. Por exemplo, um servidor tenta enviar um comando AUTH (autorização) antes de se identificar com um comando EHLO.</p>
<p>É possível que esse erro possa também ocorrer quando o disco do sistema está cheio.</p></td>
<td><p>Veja o Log de SMTP ou um rastreamento Netmon e verifique se há repositório em disco adequado e memória virtual disponível.</p></td>
</tr>
<tr class="odd">
<td><p>5.5.3</p></td>
<td><p><code>Too many recipients</code></p></td>
<td><p>O total combinado de destinatários nas linhas Para, Cc e Bcc da mensagem excede o número total de destinatários permitidos para uma única mensagem.</p></td>
<td><p>Este erro ocorre quando o remetente incluiu destinatários demais na mensagem. O remetente deve reduzir o número de endereços de destinatários na mensagem, ou o número máximo de destinatários deve ser aumentado para permitir que a mensagem seja entregue.</p></td>
</tr>
<tr class="even">
<td><p>5.5.4</p></td>
<td><p><code>Invalid domain name</code></p></td>
<td><p>A mensagem contém um remetente inválido ou um formato de endereço de destinatário incorreto.</p>
<p>Uma causa possível é que o formato de endereço do destinatário pode conter caracteres que não estão em conformidade com padrões da Internet.</p></td>
<td><p>Verifique o endereço do destinatário em busca de caracteres não padrão.</p></td>
</tr>
<tr class="odd">
<td><p>5.5.6</p></td>
<td><p><code>Invalid message content</code></p></td>
<td><p>Essa mensagem indica um possível erro de protocolo.</p></td>
<td><p>Verifique se há possíveis falhas no Log de Eventos.</p></td>
</tr>
<tr class="even">
<td><p>5.7.1</p></td>
<td><p><code>Delivery not authorized</code></p></td>
<td><p>O remetente da mensagem não tem permissão para enviar mensagens ao destinatário.</p></td>
<td><p>Esse erro ocorre quando o remetente tenta enviar uma mensagem a um destinatário, mas não tem autorização para isso. Isso ocorre frequentemente quando um remetente tenta enviar mensagens a um grupo de distribuição que foi configurado para aceitar mensagens apenas de membros desse grupo de distribuição ou de outros remetentes autorizados. O remetente deve solicitar permissão para enviar mensagens ao destinatário.</p>
<p>Esse erro também poderá ocorrer se uma regra de transporte do Exchange rejeitar uma mensagem porque a mensagem possui as condições configuradas na regra de transporte.</p></td>
</tr>
<tr class="odd">
<td><p>5.7.1</p></td>
<td><p><code>Unable to relay</code></p></td>
<td><p>O sistema de envio de email não tem permissão para enviar uma mensagem a um sistema de email que não seja o destino final da mensagem.</p></td>
<td><p>Esse erro ocorre quando o sistema de envio de emails tenta enviar uma mensagem anônima para um sistema de recebimento de email, e esse sistema não aceita mensagens para o domínio ou domínios especificados em um ou mais dos destinatários. A seguir, alguns dos motivos mais comuns desse erro:</p>
<ul>
<li><p>Um terceiro tenta usar um sistema de recebimento de emails para enviar spam, e a tentativa é rejeitada. Pela natureza do spam, o endereço de email do remetente pode ter sido forjado e a notificação de falha na entrega resultante poderá ter sido enviada ao endereço de email do remetente, que não sabe de nada. É difícil evitar essa situação.</p></li>
<li><p>Um registro MX para um domínio aponta para um sistema de recebimento de emails em que o domínio não é aceito. O administrador responsável pelo nome de domínio específico deve corrigir o registro MX ou configurar o sistema de recebimento de emails para aceitar mensagens enviadas a esse domínio, ou ambas as opções.</p></li>
<li><p>Um sistema de envio de emails ou um cliente que deve usar o sistema de recebimento de emails para retransmitir mensagens não possui as permissões corretas para fazer isso.</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>5.7.1</p></td>
<td><p><code>Client was not authenticated</code></p></td>
<td><p>O sistema de envio de emails não fez a autenticação com o sistema de recebimento de emails. O sistema de recebimento de emails exige autenticação antes do envio da mensagem.</p></td>
<td><p>Este erro ocorre quando o servidor de recebimento precisa ser autenticado antes do envio da mensagem, e o sistema de envio de emails não foi autenticado com o sistema de recebimento de emails. O administrador do sistema de envio de emails deve configurar esse sistema para que faça autenticação com o sistema de recebimento de emails para que a entrega seja feita com êxito. Esse erro também poderá ocorrer se você tentar aceitar mensagens anônimas da Internet usando um servidor de Caixa de Correio que não tenha sido configurado para isso.</p></td>
</tr>
<tr class="odd">
<td><p>5.7.3</p></td>
<td><p><code>Not Authorized</code></p></td>
<td><p>O remetente proibiu a reatribuição ao destinatário alternativo.</p></td>
<td><p> </p></td>
</tr>
</tbody>
</table>


Voltar ao início

## Seções da notificação de falha na entrega

No Exchange 2013, as notificações de falha na entrega foram projetadas para fácil leitura e entendimento de usuários finais e administradores. As informações exibidas em uma notificação de falha na entrega são separadas nestas duas áreas:

  - Uma seção de informações do usuário

  - Uma seção de informações do administrador

As informações em cada seção se destinam aos leitores dessa seção. A seção de informações do usuário aparece primeiro e contém comentários para ajudar o usuário a entender, em termos não-técnicos, por que a entrega da mensagem falhou. A seção **Informações de diagnóstico para administradores** oferece informações técnicas mais detalhadas, como cabeçalhos da mensagem original, que ajudam os administradores de email a solucionar um problema de entrega. A figura a seguir mostra a seção de informações ao usuário e a seção **Informações de diagnóstico para administradores** de uma notificação de falha na entrega.

**Seções da notificação de falha na entrega**

![Notificação de falha na entrega mostrando Informações de Diagnóstico do Usuário e do Administrador](images/Bb232118.96245455-5fb9-4669-a931-5563ddd3ab35(EXCHG.150).png "Notificação de falha na entrega mostrando Informações de Diagnóstico do Usuário e do Administrador")

## Seção de informações ao usuário

A seção de informações do usuário de uma notificação de falha na entrega gerada pelo Exchange contém informações que você deseja comunicar a um usuário final que enviou uma mensagem que voltou posteriormente com uma notificação de falha na entrega. O texto exibido nesta seção é inserido pelo servidor do Exchange que gerou a notificação de falha na entrega.

O texto na seção de informações ao usuário foi criado para ajudar o usuário final a determinar por que a mensagem foi rejeitada e como reenviá-la com êxito, caso seja necessário. Quando aplicável, o FQDN (nome de domínio totalmente qualificado) do servidor que rejeitou a mensagem é incluído na seção de informações ao usuário. Se ocorrer falha na entrega para mais de um destinatário, o endereço de email de cada destinatário será listado e o motivo da falha será incluído no espaço abaixo do endereço de email do destinatário.

Você pode modificar o texto na seção de informações ao usuário usando o cmdlet **New-SystemMessage**. Ao criar uma mensagem personalizada, você pode fornecer informações específicas para usuários finais, como o número de telefone para entrar em contato com o departamento de suporte ou um hiperlink para os próprios usuários executarem procedimentos de suporte.

Voltar ao início

## Informações de diagnóstico para administradores

A seção **Informações de diagnóstico para administradores** contém informações mais detalhadas sobre o erro específico que ocorreu durante a entrega da mensagem, o servidor que gerou a notificação de falha na entrega e o servidor que rejeitou a mensagem. Os campos a seguir estão presentes na maioria das notificações de falha na entrega e são visíveis na figura "Seções da notificação de falha na entrega" apresentada anteriormente neste tópico:

  - **Servidor gerador**   O servidor gerador é o servidor SMTP que criou a notificação de falha na entrega. O servidor gerador adota o código de status avançado que será explicado posteriormente neste tópico. Esse código cria uma notificação de falha na entrega de fácil leitura. Se não houver um servidor remoto listado abaixo do endereço de email do remetente, na seção **Informações de diagnóstico para administradores**, o servidor gerador será também o servidor que rejeitou o email original. Se ocorrer falha na entrega da mensagem quando a mensagem for enviada para outro destinatário na organização do Exchange, normalmente o mesmo servidor rejeitará a mensagem original e gerará a notificação de falha na entrega.

  - **Destinatário rejeitado**   O destinatário rejeitado é o endereço de email do destinatário para o qual a entrega da mensagem original falhou. Se a entrega para mais de um destinatário tiver falhado, o endereço de email de cada destinatário será listado aqui. O campo de destinatário rejeitado também contém os seguintes subcampos para cada endereço de email listado:
    
      - **Servidor remoto**   O campo de servidor remoto contém o FQDN do servidor que rejeita a entrega da mensagem durante a conversa SMTP. O campo de servidor remoto só é preenchido quando houve tentativa de entrega em um servidor remoto e essa tentativa foi rejeitada antes de o servidor de recebimento reconhecer com êxito a mensagem depois que o corpo da mensagem foi enviado. Se a mensagem original for reconhecida com êxito pelo servidor de recebimento e for rejeitada por causa de restrições de conteúdo, por exemplo, o campo de servidor remoto não será preenchido.
    
      - **Código de status avançado**   É o código retornado pelo servidor que rejeitou a mensagem original. O código de status avançado indica por que a mensagem original foi rejeitada. Esse código não é reescrito pelo Exchange, mas é usado para determinar que texto deve ser exibido na seção de informações ao usuário. Os códigos de status avançado que você provavelmente encontrará estão listados em "Códigos de status avançado comuns", posteriormente neste tópico. Para obter uma lista detalhada de códigos de status avançado, confira RFC 3463.
    
      - **Resposta SMTP**   A resposta SMTP é o texto legível pela máquina retornado pelo servidor que rejeitou a mensagem original. A resposta SMTP normalmente contém uma cadeia de caracteres curta que fornece uma explicação do código de status avançado que também é retornado. A resposta SMTP não é reescrita pelo Exchange. Além disso, essa resposta é apresentada sempre no formato US-ASCII.

  - **Cabeçalhos da mensagem original**   A seção de cabeçalhos da mensagem original contém os cabeçalhos da mensagem rejeitada. Esses cabeçalhos podem fornecer informações de diagnóstico úteis, como informações que podem ajudar a determinar o caminho percorrido pela mensagem antes de ser rejeitada ou se o campo **Para** corresponde ao endereço de email especificado no campo de destinatário rejeitado.

Voltar ao início

## Exemplos de mensagens de notificação de falha na entrega

As seções a seguir fornecem exemplos de duas maneiras que as mensagens de notificação de falha na entrega podem ser geradas:

  - Pelo mesmo servidor

  - Por servidores diferentes

## NDR gerada e mensagem original rejeitada pelo mesmo servidor

O exemplo a seguir mostra o que acontece quando uma organização de email remota aceita a entrega de um email através de um servidor de Transporte de Borda e, em seguida, rejeita a mensagem devido à restrição de políticas na caixa de correio do destinatário. Nesse caso, o remetente não tem permissão para enviar mensagens ao destinatário. Servidores de Transporte de Borda não realizam a validação de tamanho de mensagem, de modo que o servidor de Transporte de Borda nesse exemplo aceite a mensagem porque ela tem um endereço de destinatário válido e não viola nenhuma outra restrição de conteúdo. Como a organização de email remota aceita a mensagem inteira, inclusive o conteúdo da mensagem, ela é responsável por rejeitar a mensagem e gerar a mensagem de notificação de falha na entrega a ser enviada ao remetente.

**NDR gerada e mensagem rejeitada pelo mesmo servidor**

![Notificação de falha na entrega mostrando o mesmo servidor para geração e rejeição](images/Bb232118.c9a7cd2d-f35f-4d77-8225-c29585fa3ccd(EXCHG.150).gif "Notificação de falha na entrega mostrando o mesmo servidor para geração e rejeição")

Além disso, as mensagens rejeitadas ao serem enviadas a destinatários que fazem parte da mesma organização local do Exchange são normalmente rejeitadas pelo mesmo servidor de email que gera a mensagem de NDR. As mensagens enviadas a destinatários locais podem ser rejeitadas por diversos motivos, como caixas de correio com cota excedida, falta de autorização para enviar mensagens ao endereço do destinatário ou falhas de hardware que resultam em perda de conectividade por um longo período com outros servidores da organização.

Em ambas as situações, nenhum servidor remoto é incluído sob o endereço de email dos destinatários listados na mensagem de notificação de falha na entrega.

Voltar ao início

## Notificação de falha na entrega gerada e mensagem original rejeitada por servidores diferentes

O exemplo a seguir mostra o que acontece quando uma organização de email remota rejeita a entrega de um email antes de aceitá-lo. Nesse exemplo, o servidor remoto rejeita a mensagem e retorna um código de status avançado para o servidor de envio local, porque o destinatário especificado não existe. A rejeição acontece antes de o servidor de recebimento reconhecer a mensagem. Como o servidor de recebimento não reconhece com êxito a mensagem, ele não é responsável pela mensagem. Portanto, o servidor de envio local gera a mensagem de notificação de falha na entrega e a envia ao remetente da mensagem original.

**Notificação de falha na entrega gerada e mensagem rejeitada por servidores diferentes**

![Notificação de falha na entrega mostrando servidores de geração/envio diferentes](images/Bb232118.adfb8d5a-9c1d-4cd9-8a71-ce14224434f8(EXCHG.150).gif "Notificação de falha na entrega mostrando servidores de geração/envio diferentes")

Voltar ao início

## Consulte também


[Notificações de falha na entrega de email no Office 365](https://go.microsoft.com/fwlink/p/?linkid=524931)

