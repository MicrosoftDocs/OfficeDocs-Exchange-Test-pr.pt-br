---
title: 'Diretório de retirada e repetição: Exchange 2013 Help'
TOCTitle: Diretório de retirada e repetição
ms:assetid: ae191700-953f-411c-906f-dc90feec3d5a
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Bb124230(v=EXCHG.150)
ms:contentKeyID: 50486388
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Diretório de retirada e repetição

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2016-12-09_

Por padrão, os diretórios de retirada e repetição existem em cada servidor de caixa de correio do Microsoft Exchange Server 2013 ou o servidor de transporte de borda. Formatados corretamente os arquivos de mensagens de email que você copie para a retirada ou diretórios de repetição são enviados para entrega. O diretório de retirada é usado pelos administradores de teste de fluxo de email ou pelos aplicativos que devem criar e enviar suas próprias mensagens. O diretório de reprodução recebe mensagens de servidores de gateway externo e também pode ser usado para reenviar mensagens que os administradores exportam das filas dos servidores do Exchange.

**Sumário**

Anatomia de um arquivo de mensagem de email

Como os diretórios de retirada e repetição processam

Requisitos do arquivo de mensagem de diretório de retirada

Modificações de cabeçalho de mensagem do diretório de retirada

Requisitos do arquivo de mensagem de diretório de repetição

Modificações de cabeçalho de mensagem de diretório de repetição

Falhas no processamento de mensagens de diretório de retirada e repetição

Considerações de segurança para os diretórios de retirada e repetição

Permissões para os diretórios de retirada e repetição

## Anatomia de um arquivo de mensagens de email

Uma mensagem de email SMTP padrão consiste em um *envelope de mensagem* e a mensagem de conteúdo. Envelope da mensagem contém informações necessárias para transmissão e como entregar a mensagem. O conteúdo da mensagem contém campos de cabeçalho de mensagem (chamados coletivamente o *cabeçalho da mensagem*) e o corpo da mensagem. Envelope da mensagem é descrito no RFC 2821 e o cabeçalho da mensagem é descrito na RFC 2822.

Quando um remetente escreve uma mensagem de email e o envia para entrega, a mensagem contém as informações básicas necessários para cumprir os padrões de SMTP, um remetente, um destinatário, a data e hora em que a mensagem foi composta, uma linha de assunto opcional e corpo de uma mensagem opcional. Essa informação está contida na própria mensagem e, por definição, está contida no cabeçalho da mensagem.

Servidor de mensagens do remetente gera um envelope de mensagem para a mensagem usando as informações de remetente e destinatário encontradas no cabeçalho da mensagem e transmite a mensagem para a Internet para entrega ao servidor de mensagens do destinatário. Nunca, destinatários veem o envelope da mensagem, porque ele é gerado pelo processo de transmissão de mensagens e não é realmente uma parte da mensagem.

Cada servidor envolvidos na transmissão da mensagem pode ter inserido campos de cabeçalho de mensagem relacionados a função do servidor no fornecimento campos de cabeçalho de mensagem ou outra mensagem de aplicativo específico no cabeçalho da mensagem. Quando o destinatário abrir a mensagem usando um cliente de email, o cliente de email exibe algumas das informações mais relevantes do cabeçalho da mensagem, como o remetente, os destinatários e o assunto em conjunto com o corpo da mensagem.

Voltar ao início

## Como os diretórios de retirada e repetição processam

Em Exchange 2013, o local padrão do diretório de retirada é `%ExchangeInstallPath%TransportRoles\Pickup`. O local padrão do diretório de repetição é `%ExchangeInstallPath%TransportRoles\Replay`. Um arquivo de mensagem. eml formatada corretamente copiado para o diretório de retirada ou repetição é processado para envio nas etapas a seguir:

1.  Os diretórios de retirada e repetição são verificados para novos arquivos de mensagem a cada cinco segundos. Você não pode modificar esse intervalo de sondagem. Você pode ajustar a taxa de processamento, usando o parâmetro *PickupDirectoryMaxMessagesPerMinute* no cmdlet **Set-TransportService** de arquivo de mensagem. Este parâmetro afeta o diretório de retirada e o diretório de repetição. O valor padrão é de 100 mensagens por minuto. Arquivos que não podem ser abertos são deixados no diretório de retirada e são reavaliados no próximo intervalo de sondagem.

2.  Colocar em arquivos de mensagens no diretório de retirada, como o tamanho máximo do cabeçalho e o número máximo de destinatários, os limites são verificados. Por padrão, o tamanho de cabeçalho máximo é de 64 kilobytes (KB) e o número máximo de destinatários é 100. Você pode alterar esses limites usando o cmdlet **Set-TransportService** . Essas configurações afetam apenas o diretório de retirada.

3.  O arquivo é renomeado de. eml de *\<filename\>*<span></span>para *\<filename\>*<span></span>TMP. Se o arquivo. tmp *\<filename\>*<span></span>já existir, o arquivo é renomeado como *\<filename\>\<datetime\>*<span></span>TMP. Se o arquivo renomeando falhar, será gerado um erro de log de eventos e o próximo arquivo continua o processo de retirada.

4.  Depois que o arquivo. tmp com êxito é convertido em uma mensagem de email, um comando **delete on close** é emitido para o arquivo. tmp. O arquivo. tmp aparece permaneça no diretório de retirada, mas o arquivo não pode ser aberto.

5.  Depois que a mensagem na fila com êxito para entrega, é emitido um comando de **close** e o arquivo. tmp é excluído do diretório de retirada. Se a exclusão falhar, é gerado um erro de log de eventos. Se o serviço de transporte do Microsoft Exchange é reiniciado quando há arquivos. tmp no diretório de retirada, todos os arquivos. tmp renomeados como arquivos. eml e são reprocessados. Isso pode implicar para duplicar a transmissão de mensagens.

Voltar ao início

## Requisitos do arquivo de mensagem de diretório de retirada

Um arquivo de mensagem copiado para o diretório de retirada deve atender aos seguintes requisitos para entrega bem-sucedida:

  - O arquivo de mensagem deve ser um arquivo de texto que seja compatível com o formato básico de mensagem SMTP. Há suporte para os campos de cabeçalho de mensagem MIME e conteúdo.

  - O arquivo de mensagem deve ter uma extensão de nome de arquivo. eml.

  - Endereço de email pelo menos um deve existir nos campos de cabeçalho de mensagem `Sender` ou `From` no cabeçalho da mensagem. Se um endereço de email único existir nos campos `Sender` tanto o `From` , o endereço de email no campo `From` é usado como o remetente da mensagem no envelope da mensagem.

  - Endereço de email apenas um pode existir no campo `Sender` . Vários endereços de email não são permitidos. O campo `Sender` é opcional se apenas um endereço de email existe no campo `From` .

  - Vários endereços de email são permitidos no campo `From` , mas um único endereço de email também deve existir no campo `Sender` . O endereço no campo `Sender` , em seguida, é usado como o remetente da mensagem no envelope da mensagem.

  - Endereço de email pelo menos um deve existir nos campos `To`, `Cc`ou `Bcc` .

  - Uma linha em branco deve existir entre o cabeçalho da mensagem e o corpo da mensagem.

Este exemplo mostra uma mensagem de texto simples que usa a formatação aceitável para o diretório de retirada.

    To: mary@contoso.com
    From: bob@fabrikam.com
    Subject: Message subject
    
    This is the body of the message.

Também há suporte para o conteúdo MIME nos arquivos de mensagem do diretório de retirada. MIME define uma ampla variedade de conteúdo da mensagem que inclui os idiomas que não podem ser representados em outro conteúdo multimídia, HTML e texto ASCII de 7 bits. Uma descrição completa dos MIME e seus requisitos está além do escopo deste tópico. Este exemplo mostra uma mensagem MIME simple que usa aceitável de formatação para o diretório de retirada.

    To: mary@contoso.com
    From: bob@fabrikam.com
    Subject: Message subject
    MIME-Version: 1.0
    Content-Type: text/html; charset="iso-8859-1"
    Content-Transfer-Encoding: 7bit
    
    <HTML><BODY>
    <TABLE>
    <TR><TD>cell 1</TD><TD>cell 2</TD></TR>
    <TR><TD>cell 3</TD><TD>cell 4</TD></TR>
    </TABLE>

    </BODY></HTML>

Voltar ao início

## Modificações de cabeçalho de mensagem do diretório de retirada

O diretório de retirada remove qualquer um dos seguintes campos de cabeçalho de mensagem do cabeçalho da mensagem:

  - `Received`

  - `Resent-*`

  - `Bcc`
    

    > [!NOTE]
    > Qualquer email endereços encontrados no cabeçalho da mensagem opcional <CODE>Bcc</CODE> campos no cabeçalho da mensagem são processados corretamente. Depois que os destinatários <CODE>Bcc</CODE> são promovidos para destinatários de envelope da mensagem invisível, eles são removidos do cabeçalho da mensagem para proteger sua identidade. Se uma mensagem contiver somente os destinatários <CODE>Bcc</CODE> , o valor de <STRONG>Undisclosed Recipients</STRONG> é adicionado ao campo <CODE>To</CODE> no cabeçalho da mensagem.



O diretório de retirada adiciona seu próprio campo de cabeçalho de `Received` a uma mensagem como parte do processo de envio de mensagem. No campo de cabeçalho de `Received` é aplicado no seguinte formato.

    Received: from localhost by Pickup with Microsoft SMTP Server id <ExchangeServerVersion><datetime>

O diretório de retirada modifica os seguintes campos de cabeçalho de mensagem se eles estão ausentes ou incorretos:

  - **Id da mensagem**   Se o campo `Message-Id` está ausente ou vazia, o diretório de retirada adiciona um campo de Id da mensagem usando o formato *\<GUID\>*@*\<defaultdomain\>*.

  - **Data**   Se o campo de `Date` for ausentes ou incorretos, o diretório de retirada adiciona a data e hora da processamento pelo diretório de recebimento de mensagens.

Voltar ao início

## Requisitos do arquivo de mensagem de diretório de repetição

O diretório de reprodução é usado para reenviar mensagens do Exchange exportadas e receber mensagens de servidores de gateway externo. Essas mensagens já estiverem formatadas para o diretório de repetição. Não há necessidade de pouca ou nenhuma para administradores ou aplicativos para compor e enviar novos arquivos de mensagem usando o diretório de reprodução. O diretório de retirada deve ser usado para criar e enviar novos arquivos de mensagem.

As mensagens do diretório de repetição fazer um uso extensivo dos *Cabeçalhos X*. Cabeçalhos X são campos de cabeçalho de mensagem definidas pelo usuário, não oficiais que existem no cabeçalho da mensagem. X-cabeçalhos não são especificamente mencionados na RFC 2822, mas o uso de um campo de cabeçalho de mensagem indefinido começando com "X-" tornou-se uma maneira aceita adicionar campos de cabeçalho de mensagem não oficiais a uma mensagem. Os cabeçalhos de X específicas do Exchange usados nos arquivos de mensagem em que a repetição do diretório realmente pode definir informações de entrega que normalmente existe no envelope da mensagem. Esse recurso é necessário para preservar as informações da mensagem original quando você usa o diretório de reprodução para processar mensagens exportadas de outro servidor Exchange.

Um arquivo de mensagem copiado para o diretório de repetição deve atender aos seguintes requisitos para entrega bem-sucedida:

  - O arquivo de mensagem deve ser um arquivo de texto que seja compatível com o formato básico de mensagem SMTP. Há suporte para os campos de cabeçalho de mensagem MIME e conteúdo.

  - O arquivo de mensagem deve ter uma extensão de nome de arquivo. eml.

  - Cabeçalhos X devem ocorrer antes de todos os campos de cabeçalho regular.

  - Uma linha em branco deve existir entre os campos de cabeçalho e corpo da mensagem.

Os cabeçalhos de X descritos na lista a seguir são exigidos por mensagens no diretório de reprodução:

  - **X-remetente**   Este cabeçalho X substitui o requisito de campo de cabeçalho de mensagem `From` em uma mensagem SMTP típica. Deve existir um campo `X-Sender` que contém um endereço de email. O diretório de reprodução ignora o campo de cabeçalho de mensagem `From` se ele estiver presente, embora o cliente de email do destinatário exibe o valor do campo de cabeçalho de mensagem `From` como o remetente da mensagem. Outros parâmetros geralmente existirem no campo `X-Sender` , conforme mostrado no exemplo a seguir.
    
    ```powershell
X-Sender: <bob@fabrikam.com> BODY=7bit RET=HDRS ENVID=12345ABCD auth=<someAuth>
```
    

    > [!NOTE]
    > Esses parâmetros são valores de envelope de mensagem que normalmente são gerados pelo servidor de envio. Talvez você veja parâmetros semelhantes a esta nos arquivos de mensagem exportado.<BR><CODE>RET</CODE> Especifica se a mensagem inteira ou apenas os cabeçalhos devem ser retornados ao remetente se a mensagem não pode ser entregue. <CODE>RET</CODE> pode ter um valor de <CODE>HDRS</CODE> ou <CODE>FULL</CODE>. <CODE>ENVID</CODE> é um identificador de envelope de mensagem. <CODE>BODY</CODE> Especifica a codificação de texto da mensagem. <CODE>auth</CODE> Especifica um mecanismo de autenticação para o servidor de mensagens, conforme descrito em RFC 2554.



  - **Receptor de X**   Este cabeçalho X substitui o requisito de campo de cabeçalho de mensagem do `To` em uma mensagem SMTP típica. Pelo menos um campo `X-Receiver` que contém um endereço de email deve existir. Vários campos `X-Receiver` são permitidos para vários destinatários. O diretório de reprodução ignora os campos de cabeçalho de mensagem `To` se estiver presentes, embora o cliente de email do destinatário exibe os valores dos campos de cabeçalho de mensagem `To` como os destinatários da mensagem. Outros parâmetros opcionais podem existir nos campos `X-Receiver` , conforme mostrado no exemplo a seguir.
    
    ```powershell
X-Receiver: <mary@contoso.com> NOTIFY=NEVER ORcpt=mary@contoso.com
```
    

    > [!NOTE]
    > Esses parâmetros são valores de envelope de mensagem que normalmente são gerados pelo servidor de envio. Talvez você veja parâmetros semelhantes a esta nos arquivos de mensagem exportado. Esses parâmetros estão relacionados às mensagens de notificação (DSN) de status de entrega conforme descrito em RFC 1891.<BR><CODE>NOTIFY</CODE> pode ter um valor de <CODE>NEVER</CODE>, <CODE>DELAY</CODE>ou <CODE>FAILURE</CODE>. <CODE>ORcpt</CODE> preserva o destinatário original da mensagem.



Os cabeçalhos de X descritos na lista a seguir são opcionais para arquivos de mensagens no diretório de reprodução:

  - **X-CreatedBy**   Usado para a funcionalidade de firewall de cabeçalho. Se este cabeçalho X existir, ele não deve estar em branco. Se o campo `X-CreatedBy` não existir, ele é adicionado com um valor de **Unspecified**. Normalmente, o valor desse campo é **MSExchange15**, mas ele também pode conter o de definir em um conector de envio, tais como do tipo de espaço de endereçamento não SMTP **Notes**.

  - **X-EndOfInjectedXHeaders**   Tamanho em bytes de todos os cabeçalhos X presente. Este cabeçalho X pode ser usado como um marcador para indicar o último cabeçalho X antes de iniciar os campos de cabeçalho da mensagem normal.

  - **X-ExtendedMessageProps**   Propriedades de mensagem estendido para a mensagem.

  - **X-HeloDomain**   String de domínio HELO/EHLO apresentado durante a conversação de protocolo SMTP inicial.

  - **X-fonte**   Usado pelo Visualizador de filas na coluna **MessageSourceName**. Se o valor deste cabeçalho X não for especificado, o valor de **Replay** é usado. Outros valores possíveis para este cabeçalho X são **Smtp Receive Connector** e **Smtp Send Connector**.

  - **X-SourceIPAddress**   Endereço IP do servidor de envio. Esse campo é `0.0.0.0` se nenhum endereço IP for especificado.

Este exemplo mostra uma mensagem de texto simples que usa a formatação aceitável para o diretório de repetição.

```powershell
X-Receiver: <mary@contoso.com> NOTIFY=NEVER ORcpt=mary@contoso.com
```
    X-Sender: <bob@fabrikam.com> BODY=7bit ENVID=12345AB auth=<someAuth>
    Subject: Optional message subject
    
    This is the body of the message.

Também há suporte para o conteúdo MIME nos arquivos de mensagem do diretório de repetição. MIME define uma ampla variedade de conteúdo da mensagem que inclui os idiomas que não podem ser representados em outro conteúdo multimídia, HTML e texto ASCII de 7 bits. Uma descrição completa dos MIME e seus requisitos está além do escopo deste tópico. Este exemplo mostra uma mensagem MIME simple que usa aceitável de formatação para o diretório de repetição.

```powershell
X-Receiver: <mary@contoso.com> NOTIFY=NEVER ORcpt=mary@contoso.com
```
    X-Sender: <bob@fabrikam.com> BODY=7bit ENVID=12345ABCD auth=<someAuth>
    To: mary@contoso.com
    From: bob@fabrikam.com
    Subject: Optional message subject
    MIME-Version: 1.0
    Content-Type: text/html; charset="iso-8859-1"
    Content-Transfer-Encoding: 7bit
    
    <HTML><BODY>
    <TABLE>
    <TR><TD>cell 1</TD><TD>cell 2</TD></TR>
    <TR><TD>cell 3</TD><TD>cell 4</TD></TR>
    </TABLE>

    </BODY></HTML>

Voltar ao início

## Modificações de cabeçalho de mensagem de diretório de repetição

Do diretório de repetição exclui campo de cabeçalho da mensagem de `Bcc` no arquivo de mensagens.

O diretório de reprodução adiciona seu próprio campo de cabeçalho de mensagem `Received` a uma mensagem como parte do processo de envio de mensagem. O campo de cabeçalho de mensagem recebido é aplicado no seguinte formato.

    Received: from <ReceivingServerName> by Replay with <ExchangeServerVersion><DateTime>

O diretório de reprodução modifica os seguintes campos de cabeçalho de mensagem no cabeçalho da mensagem:

  - **ID da mensagem**   Se esse campo de cabeçalho de mensagem está ausente ou vazia, o diretório de reprodução adiciona um campo de cabeçalho de mensagem Message-ID usando o formato *\<GUID\>*@*\<defaultdomain\>*.

  - **Data**   Se esse campo de cabeçalho de mensagem estiver faltando ou mal formados, o diretório de reprodução adiciona o campo de cabeçalho de mensagem de data usando a data e hora da mensagem processamento pelo diretório de repetição.

Voltar ao início

## Falhas no processamento de mensagens de diretório de retirada e repetição

Não pode ser filas com êxito um arquivo de mensagens copiado para os diretórios de retirada ou repetição para entrega. Categorias de falha de envio de mensagem a seguir podem ocorrer:

  - **Falhas de entrega**   Um arquivo de mensagem formatada corretamente em conjunto com um remetente válido que não pode ser enviado com êxito para entrega gera um relatório de falha na entrega (NDR). As violações de restrição do diretório de conteúdo ou retirada mal formados mensagem também pode causar um NDR. Quando uma NDR é gerada durante o processamento de mensagem, o arquivo de mensagem original é anexado à mensagem NDR e o arquivo de mensagem é excluído do diretório de retirada ou do diretório de repetição.
    

    > [!NOTE]
    > Uma mensagem formatada corretamente enviada pelo pipeline de transporte posteriormente perceba uma falha de entrega e a ser retornada ao remetente com uma NDR. Esse tipo de falha pode ser causado por questões de transmissão não relacionadas aos diretórios de retirada ou repetição, como falhas do servidor de mensagens ou routing falhas ao longo do caminho de entrega da mensagem.



  - **Badmail**   Uma mensagem classificada como *badmail* tem problemas sérios que impedem que os diretórios de retirada ou repetição enviando a mensagem para entrega. A outra condição que faz com que o badmail é quando a mensagem está formatada corretamente, mas os destinatários são inválidos e uma mensagem de notificação de falha NA não pode ser enviada ao remetente, porque o remetente não é válido.
    
    Arquivos de mensagens determinados como badmail são deixados nos diretórios de retirada ou repetição e renomeados das. eml de *\<filename\>*<span></span>para *\<filename\>*<span></span>bad. Se o arquivo de bad *\<filename\>*<span></span>já existir, o arquivo é renomeado para *\<filename\>\<datetime\>*<span></span>bad. Se os diretórios de retirada ou repetição existir badmail, será gerado um erro de log de eventos, mas as mesmas mensagens badmail não geram erros de log de eventos repetidos.
    

    > [!NOTE]
    > Sempre redação e salvar arquivos de mensagens em um local diferente antes de copiá-los para o diretório de retirada para entrega. O diretório de retirada sonda para novas mensagens a cada cinco segundos. Portanto, se você tentar redação e salvar os arquivos de mensagens no diretório de retirada próprio, o diretório de retirada pode tentar processar os arquivos de mensagens antes de finalizar redigi-los.



Voltar ao início

## Considerações de segurança para os diretórios de retirada e repetição

A lista a seguir descreve as preocupações de segurança que são comuns para o diretório de retirada e o diretório de reprodução:

  - Qualquer verificação de segurança configuradas em um conector de recebimento, como recursos anti-spam, antimalware, a filtragem de remetente ou ações, a filtragem por destinatário não é executadas em mensagens enviadas por meio do diretório de retirada ou do diretório de repetição.

  - Um diretório de retirada comprometido ou o diretório de repetição pode atuar como uma retransmissão aberta. Isso permite que mensagens sejam reenviadas ou *retransmitidos* usando um servidor diferente para mascarar a origem real das mensagens.

A lista a seguir descreve as preocupações de segurança adicionais que se aplicam ao diretório de reprodução:

  - Os cabeçalhos de X usados pelo diretório de repetição permitem a criação manual de envelope da mensagem. As informações dos campos `X-Sender` e `X-Receiver` podem ser completamente diferentes dos campos de cabeçalho de mensagem `To` ou `From` exibidos por clientes de email. Geralmente, tal uma representação de um remetente e um domínio é chamada *falsificação*. Um *email falsificado* é uma mensagem de email que tenha um endereço de envio que foi modificado para que ele apareça como se ele for originada de um remetente que não seja o remetente real da mensagem.

  - Se o campo `X-CreatedBy` tem o valor de **MSExchange15**, o destino será considerado confiável e firewall de cabeçalho não será aplicada. *Firewall de cabeçalho* é uma maneira para o Exchange preservar cabeçalhos X em mensagens transmitidas entre os servidores Exchange confiáveis ou para remover potencialmente revelar X cabeçalhos de mensagens transmitidas para destinos não confiáveis fora da organização do Exchange. Esses cabeçalhos X podem ser usados para compartilhar informações do Exchange, como o nível de confiança de spam (SCL), assinatura de mensagens ou autorizado de criptografia entre servidores Exchange. Revelar essas informações a fontes não autorizadas poderia representar um risco de segurança. Para obter mais informações sobre o firewall de cabeçalho, consulte [Understanding Firewall de cabeçalho](https://go.microsoft.com/fwlink/?linkid=268394).

Maior segurança deve ser aplicada para o diretório de repetição devido aos riscos de segurança adicionais associados com o diretório de repetição. Usuários ou aplicativos que devem gerar e enviar mensagens podem ter acesso ao diretório de retirada, mas não deveria precisam de acesso para o diretório de repetição.

O diretório de retirada e o do diretório de repetição são habilitados por padrão em todos os servidores de caixa de correio e transporte de borda. Se o diretório de retirada ou do diretório de repetição não é necessária em um servidor de caixa de correio específico ou um servidor de transporte de borda em sua organização, você pode desabilitar o diretório de retirada ou do diretório de repetição nesse servidor, definindo o caminho do diretório de retirada ou caminho do diretório de reprodução para o valor `$null`. Para obter mais informações, consulte [Configurar o diretório de retirada e o diretório de repetição](configure-the-pickup-directory-and-the-replay-directory-exchange-2013-help.md).

Voltar ao início

## Permissões para os diretórios de retirada e repetição

As seguintes permissões são necessárias sobre os diretórios de retirada e repetição:

  - Administrador: Controle total

  - Sistema: Controle Total

  - Serviço de rede: Ler, gravar e excluir arquivos e subpastas

Por padrão, o serviço transporte do Microsoft Exchange usa as credenciais de segurança da conta de usuário de serviço de rede para gerenciar o local e as permissões dos diretórios de retirada e repetição. A conta de serviço de rede requer essas permissões no diretório de retirada para que podem ser abertos arquivos. eml, renomeado para. tmp e excluído ou renomeado para bad se a mensagem é classificada como badmail.

Você pode mover o local desses diretórios usando os parâmetros *PickupDirectoryPath* e *ReplayDirectoryPath* no cmdlet **Set-TransportService** . Com êxito, alterar o local do diretório de retirada depende os direitos concedidos à conta de serviço de rede em que os novos locais de diretório, e se a novos diretórios já existirem. Se a pasta não existir, e a conta de serviço de rede possui os direitos necessários para criar pastas e aplicar permissões no novo local, o diretório é criado e as permissões corretas são aplicadas a ele. Se já existir um novo diretório, as permissões de pasta não são verificadas. Sempre que você move os locais de diretório usando o parâmetro *PickupDirectoryPath* ou *ReplayDirectoryPath* com o cmdlet **Set-TransportService** , sempre verifique se que o novo diretório existe e se o novo diretório tem as permissões corretas aplicadas a ela.

Voltar ao início

