---
title: 'Redundância de sombra: Exchange 2013 Help'
TOCTitle: Redundância de sombra
ms:assetid: a40dbe61-2a18-48a8-b2e0-4e81a6678d11
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Dd351027(v=EXCHG.150)
ms:contentKeyID: 50486294
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Redundância de sombra

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2015-03-09_

Redundância de sombra foi introduzida no Microsoft Exchange Server 2010 para fornecer cópias redundantes de mensagens antes que eles estiver entregue às caixas de correio. No Exchange 2010, redundância de sombra atrasada exclusão de uma mensagem do banco de dados de transporte em um servidor de transporte até que o servidor verificado o próximo salto no caminho de entrega da mensagem concluída entrega. Se o próximo salto falhou antes de relatar uma entrega bem-sucedida volta para o servidor de transporte, o servidor de transporte reenviado a mensagem para esse próximo salto. servidores Exchange 2010 usado o verbo XSHADOW para anunciar seu suporte de redundância de sombra. Se um servidor SMTP não oferecer suporte a redundância de sombra, Exchange 2010 usado atrasada com base em um intervalo de tempo configurado no conector de recebimento de fazer uma cópia redundante da mensagem de confirmação.

A melhoria principal para redundância de sombra no Microsoft Exchange Server 2013 é que o servidor de transporte agora faz uma cópia redundante de qualquer mensagem recebida antes que ele reconhece com êxito recebendo a mensagem de volta ao servidor de envio. Suporte do servidor de envio ou falta de suporte para redundância de sombra não importa. Isso ajuda a garantir que todas as mensagens no pipeline de transporte Exchange 2013 sejam feitas redundantes enquanto eles estão em trânsito. Se Exchange 2013 determina que a mensagem original foi perdida em trânsito, cópia redundante da mensagem é entregue novamente.

**Sumário**

Componentes de redundância de sombra

Requisitos de redundância de sombra

Redundância de sombra é habilitada por padrão

Como as mensagens na sombra são criadas

Tempos limite de SMTP

Como as mensagens na sombra são mantidas

Processamento após uma interrupção de mensagem

## Componentes de redundância de sombra

A tabela a seguir descreve os componentes de redundância de sombra. Esses termos são usados em todo o tópico.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Termo</th>
<th>Descrição</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Servidor de transporte</p></td>
<td><p>Um servidor do Exchange que tem filas de mensagens e é responsável pelo roteamento de mensagens. Exchange 2013, um servidor de transporte é um servidor de caixa de correio (serviço de transporte no servidor de caixa de correio).</p></td>
</tr>
<tr class="even">
<td><p>Banco de dados de transporte</p></td>
<td><p>O mensagem fila banco de dados em um servidor de transporte Exchange 2013. Filas de sombra e Safety Net também são armazenados no banco de dados de transporte.</p></td>
</tr>
<tr class="odd">
<td><p>Limite de alta disponibilidade de transporte</p></td>
<td><p>Um grupo de disponibilidade da banco de dados (DAG) em ambientes de DAG, ou um site do Active Directory em ambientes não são DAG. Quando uma mensagem é recebida em um servidor de transporte no limite de alta disponibilidade de transporte, o Exchange tenta manter 2 cópias redundantes da mensagem nos servidores de transporte dentro dos limites. Quando uma mensagem deixa o limite de alta disponibilidade de transporte, o Exchange deixará de manter cópias redundantes da mensagem.</p></td>
</tr>
<tr class="even">
<td><p>Mensagem principal</p></td>
<td><p>A mensagem foi enviada pelo pipeline de transporte para entrega.</p></td>
</tr>
<tr class="odd">
<td><p>Mensagem de sombra</p></td>
<td><p>Cópia redundante da mensagem que o servidor de sombra mantém até que ele confirma que a mensagem principal com êxito foi processada pelo servidor primário.</p></td>
</tr>
<tr class="even">
<td><p>Servidor primário</p></td>
<td><p>O servidor de transporte que está processando a mensagem principal.</p></td>
</tr>
<tr class="odd">
<td><p>Servidor de sombra</p></td>
<td><p>O servidor de transporte que contém a mensagem de sombra para o servidor primário. Um servidor de transporte pode ser o servidor primário para algumas mensagens e o servidor de sombra para outras mensagens simultaneamente.</p></td>
</tr>
<tr class="even">
<td><p>Fila de sombra</p></td>
<td><p>A fila de entrega onde o servidor de sombra armazena mensagens na sombra. Para mensagens com vários destinatários, cada próximo salto para a mensagem principal exige filas de sombra separado.</p></td>
</tr>
<tr class="odd">
<td><p>Status de descarte</p></td>
<td><p>As informações de que um servidor de transporte mantém para mensagens na sombra que indicam a mensagem principal foi processadas com êxito.</p></td>
</tr>
<tr class="even">
<td><p>Notificação de descarte</p></td>
<td><p>A resposta um servidor de sombra recebe de um servidor primário, que indica que uma mensagem de sombra está pronta para ser descartada.</p></td>
</tr>
<tr class="odd">
<td><p>Rede de Segurança</p></td>
<td><p>A versão aprimorada de Exchange 2013 do transporte dumpster. As mensagens que são processadas com êxito ou entregue a um destinatário de caixa de correio pelo serviço de transporte em um servidor de caixa de correio são movidas para a rede de segurança. Para obter mais informações, consulte <a href="safety-net-exchange-2013-help.md">Rede de Segurança</a>.</p></td>
</tr>
<tr class="even">
<td><p>Gerenciador de redundância de sombra</p></td>
<td><p>O componente de transporte que gerencia a redundância de sombra.</p></td>
</tr>
<tr class="odd">
<td><p>Pulsação</p></td>
<td><p>O processo que permite que os servidores primários e servidores de sombra para verificar a disponibilidade de umas às outras.</p></td>
</tr>
</tbody>
</table>


Voltar ao início

## Requisitos de redundância de sombra

Embora possa parecer óbvia, redundância de sombra requer vários servidores de caixa de correio Exchange 2013. O servidor de caixa de correio pode ser servidores autônomos, ou os servidores de caixa de correio e servidores de acesso para cliente instalados no mesmo computador.

  - Se o servidor de caixa de correio não for membro de um DAG, os outros servidores de caixa de correio devem estar no site do Active Directory local.

  - Se o servidor de caixa de correio for membro de um DAG, os outros servidores de caixa de correio devem pertencer ao mesmo DAG. Os outros servidores de caixa de correio que pertencem ao DAG podem ser no site do Active Directory local ou em um site remoto do Active Directory. Se o DAG abranger vários sites do Active Directory, redundância de sombra prefere criando uma cópia redundante da mensagem em um site remoto do Active Directory para resiliência de site.

Estas são as situações em que a redundância de sombra não pode proteger mensagens em trânsito:

  - Em ambientes de servidor do Exchange único.

  - Em DAGs sob provisionado.

  - Durante a falha simultânea de dois ou mais servidores de transporte envolvidos na redundância de sombra de uma mensagem.

Voltar ao início

## Redundância de sombra é habilitada por padrão

Por padrão, redundância de sombra está habilitada globalmente no serviço de transporte em todos os servidores de caixa de correio usando o parâmetro *ShadowRedundancyEnabled* no cmdlet **Set-TransportConfig** . Por padrão, se o serviço de transporte em um servidor de caixa de correio não é possível criar uma cópia redundante de uma mensagem, a mensagem não será rejeitada. No entanto, você pode configurar Exchange 2013 para rejeitar uma mensagem se uma cópia redundante da mensagem não é criada usando-se o parâmetro *RejectMessageOnShadowFailure* no cmdlet **Set-TransportConfig** . A mensagem será rejeitada com falha transitória, mas o servidor de envio pode transmitir a mensagem novamente. O código de resposta SMTP é `451 4.4.0 Message failed to be made redundant.` , você deve configurar Exchange 2013 para rejeitar mensagens que não puderem ser tornadas redundantes somente quando a sua organização tiver vários servidores de caixa de correio Exchange 2013 disponíveis.

A tabela a seguir descreve os parâmetros que permitem a redundância de sombra.

### Parâmetros que permitem a redundância de sombra

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Parâmetro</th>
<th>Valor padrão</th>
<th>Descrição</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>ShadowRedundancyEnabled</em> em <strong>Set-TransportConfig</strong></p></td>
<td><p><code>$true</code></p></td>
<td><ul>
<li><p><code>$true</code> permite que a redundância de sombra em todos os servidores de transporte na organização.</p></li>
<li><p><code>$false</code> desabilita a redundância de sombra em todos os servidores de transporte na organização.</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p><em>RejectMessageOnShadowFailure</em> em <strong>Set-TransportConfig</strong></p></td>
<td><p><code>$false</code></p></td>
<td><ul>
<li><p><code>$false</code>   Quando uma cópia de sombra da mensagem não pode ser criada, a mensagem principal é aceita qualquer forma pelos servidores de transporte na organização. Essas mensagens não são persistentes forma redundante enquanto eles estão em trânsito.</p></li>
<li><p><code>$true</code>   Nenhuma mensagem é aceito ou confirmada por qualquer servidor de transporte na organização até que uma cópia de sombra da mensagem foi criada com êxito. Se uma cópia de sombra da mensagem não pode ser criada, a mensagem principal será rejeitada com um erro transitório. Todas as mensagens da organização são mantidas forma redundante enquanto eles estão em trânsito.</p>
<p>Você deve definir esse valor como <code>$true</code> somente se você tiver vários servidores de caixa de correio Exchange 2013 em um site do Active Directory ou DAG, onde uma cópia de sombra da mensagem pode ser criada.</p></li>
</ul>
<p>Esse parâmetro é significativo apenas quando <em>ShadowRedundancyEnabled</em> é <code>$true</code>.</p></td>
</tr>
</tbody>
</table>


Voltar ao início

## Como as mensagens na sombra são criadas

O principal objetivo do redundância de sombra é sempre têm duas cópias de uma mensagem em um limite de alta disponibilidade de transporte, enquanto a mensagem estiver em trânsito. Quando e onde a cópia redundante da mensagem é criada depende do local de origem a mensagem e onde a mensagem será. Há três fatores determinantes principais:

  - Mensagens recebidas de fora de um limite de alta disponibilidade de transporte.

  - Mensagens enviadas de fora de um limite de alta disponibilidade de transporte.

  - Mensagens recebidas do serviço de envio de transporte de caixa de correio de um servidor de caixa de correio dentro dos limites de alta disponibilidade de transporte.

Um *limite de alta disponibilidade de transporte* é um destes procedimentos:

  - Um DAG, para servidores de caixa de correio que são membros de um DAG. Isso inclui um DAG que abrange vários sites do Active Directory.

  - Um site do Active Directory para servidores de caixa de correio que não pertencem a um DAG.

Redundância de sombra nunca rastreia mensagens na sombra em um limite de alta disponibilidade de transporte. Quando uma mensagem cruza o limite de alta disponibilidade de transporte, redundância de sombra inicia ou reinicia. Isso reduz o tráfego de manutenção de mensagem de sombra e impede reenvios de mensagem de sombra ocorra através da fronteira de alta disponibilidade de transporte. Exchange 2010 Servidores de transporte de Hub são um caso especial e são abordadas neste tópico.

## Mensagens recebidas de fora de um limite de alta disponibilidade de transporte

Quando o serviço de transporte em um servidor de caixa de correio Exchange 2013 recebe uma mensagem de fora do limite de alta disponibilidade de transporte, o servidor de caixa de correio não está preocupado com o suporte ou falta de suporte para redundância de sombra pelo servidor de envio. Redundância de sombra está habilitada, desde que o servidor caixa de correio que recebe a mensagem faz uma cópia redundante da mensagem em outro servidor de caixa de correio dentro dos limites de alta disponibilidade de transporte antes de confirmar o recebimento da mensagem de volta ao servidor de envio. Aqui está um exemplo de como funciona o processo:

![Criação de mensagem de sombra](images/Dd351027.a97d383b-6ae4-458d-af3a-1ac0a41cd52b(EXCHG.150).gif "Criação de mensagem de sombra")

1.  Um servidor SMTP transmite uma mensagem para o serviço de transporte em um servidor de caixa de correio. O servidor de caixa de correio é o servidor primário e a mensagem é a principal.

2.  Enquanto a sessão SMTP original com o servidor SMTP ainda estiver ativa, o serviço de transporte no servidor primário abre uma nova sessão SMTP simultânea com o serviço de transporte em um servidor diferente da caixa de correio na organização para criar uma cópia redundante da mensagem.
    
      - Se o servidor primário for um membro de um DAG, o servidor primário se conecta a um servidor de caixa de correio diferente no mesmo DAG. Se o DAG abranger vários sites do Active Directory, um servidor de caixa de correio em um site diferente do Active Directory é preferido por padrão. Essa configuração é controlada pelo parâmetro *ShadowMessagePreference* no cmdlet **Set-TransportService** . O valor padrão é `PreferRemote`, mas você pode alterá-lo para `RemoteOnly` ou `LocalOnly`.
    
      - Se o servidor primário não for membro de um DAG, o servidor primário conecta-se para um servidor de caixa de correio diferente no mesmo Site do Active Directory, independentemente do valor do parâmetro *ShadowMessagePreference* .

3.  O servidor primário transmite uma cópia da mensagem para o serviço de transporte em outro servidor de caixa de correio e o serviço de transporte no servidor de caixa de correio reconhece que a cópia da mensagem foi criada com êxito. A cópia da mensagem é a mensagem de sombra e o servidor de caixa de correio que contém a ele é o servidor de sombra para o servidor primário. A mensagem existe em uma fila de sombra no servidor de sombra.

4.  Depois que o servidor primário recebe a confirmação do servidor de sombra, o servidor primário confirma o recebimento da mensagem principal para o servidor SMTP original na sessão SMTP original e a sessão SMTP está fechada.

## Mensagens enviadas fora de um limite de alta disponibilidade de transporte

Quando um servidor de transporte de Exchange 2013 transmite uma mensagem de fora do limite de alta disponibilidade de transporte e o servidor SMTP no outro lado reconhece o êxito no recebimento da mensagem, o servidor de transporte move a mensagem em Safety Net. Nenhum reenvio da mensagem da Safety Net pode ocorrer depois que a mensagem principal foram transmitida com êxito através da fronteira de alta disponibilidade de transporte. Para obter mais informações sobre a rede de segurança, consulte [Rede de Segurança](safety-net-exchange-2013-help.md).

## Mensagens transmitidas dentro de um limite de alta disponibilidade de transporte

Roteamento de mensagens é otimizado Exchange 2013 para que quando o destino final estiver em um site do Active Directory ou DAG, vários saltos entre o serviço de transporte nos servidores de caixa de correio no site do Active Directory ou DAG não são geralmente necessários. Depois que a mensagem é aceita pelo serviço de transporte em um servidor de caixa de correio no site do DAG ou do Active Directory que contém o destino final da mensagem, o próximo salto para a mensagem é normalmente o destino final em si. Objetivo da redundância de sombra de manter duas cópias de uma mensagem em trânsito seja cumprido quando uma cópia de sombra da mensagem não existe em qualquer lugar dentro do site do Active Directory ou DAG. Normalmente, apenas situações de failover em um DAG que exigem o cmdlet **Redirect-Message** para esvaziar as filas de espera ativas em um servidor de caixa de correio exigiria vários saltos dentro dos limites de alta disponibilidade de transporte mesmo.

## Redundância de sombra com servidores de transporte de Hub do Exchange 2010 no mesmo site do Active Directory

Quando um servidor de transporte de Hub Exchange 2010 transmite uma mensagem para um servidor de caixa de correio Exchange 2013 no mesmo site do Active Directory, o servidor de transporte de Hub Exchange 2010 anuncia o suporte para redundância de sombra usando o comando XSHADOW, mas o servidor de caixa de correio não anuncia o suporte para redundância de sombra. Isso impede que o servidor de transporte de Hub Exchange 2010 criando uma cópia de sombra da mensagem em um servidor de caixa de correio Exchange 2013.

Quando o serviço de transporte em um servidor de caixa de correio Exchange 2013 transmite uma mensagem para um Exchange 2010 transporte de Hub no mesmo site do Active Directory, o servidor de caixa de correio Exchange 2013 sombreia a mensagem para o servidor de transporte de Hub Exchange 2010. Depois que o servidor de caixa de correio Exchange 2013 recebe a confirmação do servidor de transporte de Hub Exchange 2010 que a mensagem foi recebida com êxito, o servidor de caixa de correio Exchange 2013 move a mensagem com êxito processada em Safety Net. No entanto, as mensagens com êxito processadas armazenadas em Safety Net por Exchange 2013 caixa de correio nunca são reenviadas para os servidores de transporte de Hub Exchange 2010.

Voltar ao início

## Tempos limite de SMTP

Durante a tentativa de fazer uma cópia redundante da mensagem, a conexão SMTP entre o servidor de envio SMTP e o servidor primário ou a sessão SMTP entre o servidor primário e o servidor de sombra poderia timeout. Conectores de recebimento e ter um parâmetro *ConnectionInactivityTimeOut* quando dados realmente sendo transmitidos no conector de conectores de envio. Receber conectores também tem um parâmetro de absoluta *ConnectionTimeOut* .

Se qualquer um do tempo limite de sessões de SMTP antes da cópia de sombra da mensagem é criada e confirmada com êxito, o resultado é controlado pelo parâmetro *RejectMessageOnShadowFailure* no cmdlet **Set-TransportConfig** . Por padrão, o valor desse parâmetro é `$false`, que significa que a mensagem principal é aceita sem uma cópia de sombra que está sendo criada. Se o valor desse parâmetro for `$true` a principal mensagem será rejeitada com o erro transitório `451 4.4.0`.

Se a cópia de sombra de uma mensagem foi criada com êxito, mas a sessão SMTP entre o servidor de envio SMTP e o servidor primário expire, o servidor primário aceita e processa a mensagem principal. Servidor SMTP de envio proporcionará novamente a mensagem não confirmada, mas a detecção de mensagem duplicada impedirá que os usuários de caixa de correio do Exchange de ver as mensagens duplicadas. Quando o servidor de envio SMTP reenvia a mensagem, o servidor primário criará outra cópia de sombra da mensagem. Não há nenhuma relação entre as mensagens na sombra criadas durante reenvios mensagem pelo servidor SMTP de envio.

A tabela a seguir descreve os parâmetros que controlam a criação de mensagens na sombra

### Parâmetros de criação de mensagem de sombra

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Origem</th>
<th>Valor padrão</th>
<th>Descrição</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>ShadowMessagePreferenceSetting</em> em <strong>Set-TransportConfig</strong></p></td>
<td><p><code>PreferRemote</code></p></td>
<td><ul>
<li><p><code>PreferRemote</code>   Tente fazer uma cópia de sombra da mensagem em um servidor de caixa de correio em um site diferente do Active Directory. Se a operação falhar, tente fazer uma cópia de sombra da mensagem em um servidor no site do Active Directory local.</p></li>
<li><p><code>LocalOnly</code>   Uma cópia de sombra da mensagem deve ser feita somente em um servidor de transporte no site do Active Directory local.</p></li>
<li><p><code>RemoteOnly</code>: uma cópia de sombra da mensagem deve ser feita somente em um servidor de transporte em um site diferente do Active Directory.</p></li>
</ul>
<p>Esse parâmetro é significativo apenas quando o servidor primário que está tentando fazer uma cópia de sombra da mensagem for um servidor de caixa de correio que seja membro de um DAG que abrange vários sites do Active Directory.</p></td>
</tr>
<tr class="even">
<td><p><em>MaxRetriesForRemoteSiteShadow</em> em <strong>Set-TransportConfig</strong></p></td>
<td><p>4</p></td>
<td><p>Este parâmetro é usado quando o servidor de caixa de correio é um membro de um DAG que abrange vários sites do Active Directory.</p>
<ul>
<li><p>Se <em>ShadowMessagePreferenceSetting</em> for definido como <code>PreferRemote</code>, primeiro o servidor de caixa de correio tenta criar uma cópia de sombra da mensagem em outro servidor de caixa de correio em um site do Active directory remoto até o número de vezes especificado pelo <em>MaxRetriesForRemoteSiteShadow</em>. Se isso falhar, o servidor de caixa de correio tenta criar uma cópia de sombra da mensagem em um servidor de caixa de correio diferente no site do Active Directory local até o número de vezes especificado pelo <em>MaxRetriesForLocalSiteShadow</em>.</p></li>
<li><p>Se <em>ShadowMessagePreferenceSetting</em> for definido como <code>RemoteOnly</code>, o servidor de caixa de correio apenas tenta criar uma cópia de sombra da mensagem em um servidor de caixa de correio em um site do Active Directory remoto até o número de vezes especificado pelo <em>MaxRetriesForRemoteSiteShadow</em>.</p></li>
<li><p>O cmdlet</p></li>
</ul>
<p>Quando uma cópia de sombra da mensagem não pode ser criada com êxito:</p>
<ul>
<li><p>Se <em>RejectMessageOnShadowFailure</em> for <code>$true</code>, a mensagem principal será rejeitada com um erro transitório.</p></li>
<li><p>Se <em>RejectMessageOnShadowFailure</em> for <code>$false</code>, a mensagem principal é aceita qualquer forma, mas não é mantida de forma redundante.</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p><em>MaxRetriesForLocalSiteShadow</em> em <strong>Set-TransportConfig</strong></p></td>
<td><p>2</p></td>
<td><p>Este parâmetro é usado nas seguintes circunstâncias:</p>
<ul>
<li><p>Se o servidor de caixa de correio é um membro de um DAG que abrange vários sites do Active Directory.</p>
<ol>
<li><p>Se <em>ShadowMessagePreferenceSetting</em> for definido como <code>PreferRemote</code>, primeiro o servidor de caixa de correio tenta criar uma cópia de sombra da mensagem em outro servidor de caixa de correio em um site do Active directory remoto até o número de vezes especificado pelo <em>MaxRetriesForRemoteSiteShadow</em>. Se isso falhar, o servidor de caixa de correio tenta criar uma cópia de sombra da mensagem em um servidor de caixa de correio diferente no site do Active Directory local até o número de vezes especificado pelo <em>MaxRetriesForLocalSiteShadow</em>.</p></li>
<li><p>Se <em>ShadowMessagePreferenceSetting</em> for definido como <code>LocalOnly</code>, o servidor de caixa de correio apenas tenta criar uma cópia de sombra da mensagem em um servidor de caixa de correio diferente no site do Active Directory local até o número de vezes especificado pelo <em>MaxRetriesForLocalSiteShadow</em>.</p></li>
</ol></li>
<li><p>Se o servidor de caixa de correio não for membro de um DAG, ou se o servidor de caixa de correio é um membro de um DAG que está em um site do Active Directory, o servidor de caixa de correio apenas tenta criar uma cópia de sombra da mensagem em um servidor de caixa de correio diferente no site do Active Directory local até o número de vezes especificado pelo <em>MaxRetriesForLocalSiteShadow</em>.</p></li>
</ul>
<p>Quando uma cópia de sombra da mensagem não pode ser criada com êxito:</p>
<ul>
<li><p>Se <em>RejectMessageOnShadowFailure</em> for <code>$true</code>, a mensagem principal será rejeitada com um erro transitório.</p></li>
<li><p>Se <em>RejectMessageOnShadowFailure</em> for <code>$false</code>, a mensagem principal é aceita qualquer forma, mas não é mantida de forma redundante.</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p><em>ConnectionInactivityTimeout</em> em <strong>Set-ReceiveConnector</strong></p></td>
<td><p>5 minutos no serviço de transporte em servidores de caixa de correio</p>
<p>5 minutos no serviço Front End Transport em servidores de acesso para cliente.</p>
<p>1 minuto em servidores de transporte de borda.</p></td>
<td><p>Este parâmetro especifica o tempo máximo que uma conexão de SMTP aberta com um servidor de origem de mensagens pode permanecer inativa antes que a conexão é fechada. O valor desse parâmetro deve ser menor que o valor especificado pelo parâmetro <em>ConnectionTimeout</em> .</p></td>
</tr>
<tr class="odd">
<td><p><em>ConnectionTimeout</em> em <strong>Set-ReceiveConnector</strong></p></td>
<td><p>10 minutos no serviço de transporte em servidores de caixa de correio</p>
<p>10 minutos no serviço Front End Transport em servidores de acesso para cliente.</p>
<p>5 minutos nos servidores de transporte de borda.</p></td>
<td><p>Este parâmetro especifica o tempo máximo que uma conexão de SMTP com uma fonte de servidor de mensagens pode permanecer aberta, mesmo se o servidor de mensagens de origem está transmitindo dados. O valor desse parâmetro deve ser maior que o valor especificado pelo parâmetro <em>ConnectionInactivityTimeout</em> .</p></td>
</tr>
<tr class="even">
<td><p><em>ConnectionInactivityTimeOut</em> em <strong>Set-SendConnector</strong></p></td>
<td><p>10 minutos</p></td>
<td><p>Este parâmetro especifica o tempo máximo que uma conexão de SMTP aberta com um servidor de destino de mensagens pode permanecer inativa antes que a conexão é fechada.</p></td>
</tr>
</tbody>
</table>


Voltar ao início

## Como as mensagens na sombra são mantidas

Depois que uma mensagem de sombra foi criada com êxito, o trabalho de redundância de sombra somente apenas tiver começado. O servidor primário e o servidor de sombra necessário permanecer em contato com uns aos outros para rastrear o progresso da mensagem.

Quando o servidor primário com êxito transmite a mensagem para o próximo salto e o próximo salto confirma o recebimento da mensagem, o servidor primário atualiza o *status de descarte* da mensagem como entrega completa. O status de descarte é basicamente uma mensagem que contenha da lista de mensagens que estão sendo monitorados. Uma mensagem entregue com êxito não precisa ser mantidos em uma fila de sombra, portanto, depois que o servidor de sombra sabe o servidor primário tem transmitidas com êxito a mensagem para o próximo salto, o servidor de sombra move a mensagem de sombra da fila de sombra para Safety Net.

O servidor de sombra determina o status de descarte das mensagens em suas filas de sombra sombra consultando o servidor primário. Se o servidor de sombra abre uma sessão SMTP com o servidor primário por qualquer motivo, incluindo a transmissão de outras mensagens não relacionadas, o servidor de sombra emite o comando **XQDISCARD** para determinar o status de descarte das mensagens principais. Se o servidor de sombra ainda não abriu uma sessão SMTP com o servidor primário após um intervalo de tempo pré-configurada, o servidor de sombra será abrir uma sessão SMTP com o servidor primário e execute o comando **XQDISCARD** . O intervalo de tempo é controlado pelo parâmetro *ShadowHeartbeatFrequentcy* no cmdlet **Set-TransportConfig** . O valor padrão é 2 minutos. Após a sombra server abre uma sessão SMTP com o servidor primário, o servidor primário responde com o *descarte notificações* para mensagens que se aplicam ao consultar o servidor de sombra. Em Exchange 2013, as notificações de descarte são armazenadas em disco, não na memória. Portanto, se o serviço de transporte do Microsoft Exchange for reiniciado, as notificações de descarte são persistentes. Depois que o serviço for reiniciado, o servidor principal ainda sabe sobre as mensagens processada com êxito e essa informação é disponível para o servidor de sombra.

A comunicação SMTP entre o servidor de sombra e o servidor primário é usada como a *pulsação* que determina a disponibilidade dos servidores. Se o servidor de sombra não é possível abrir uma sessão SMTP com o servidor primário após um intervalo de tempo pré-configurado ou se o banco de dados de transporte do servidor primário tiver uma ID de banco de dados diferente, o servidor de sombra eleva próprio como o servidor primário, eleva as mensagens na sombra como mensagens principais e transmite as mensagens para o próximo salto. O intervalo de tempo é controlado pelo parâmetro *ShadowResubmitTimeSpan* no cmdlet **Set-TransportConfig** . O valor padrão é 3 horas.

*Gerenciador de redundância de sombra* é o principal componente de um servidor de transporte de Exchange 2013 que é responsável pelo gerenciamento de redundância de sombra. Gerenciador de redundância de sombra é responsável por manter as informações para todas as mensagens principais que um servidor está processando a seguir:

  - O servidor de sombra para cada mensagem principal que estão sendo processada.

  - O status de descarte sejam enviadas aos servidores de sombra.

Gerente de redundância de sombra é responsável pelas seguintes informações sobre todas as mensagens de sombra que um servidor de sombra possui em suas filas de sombra:

  - Manter a lista de servidores primários para cada mensagem de sombra.

  - Comparando o original ID de banco de dados e a ID de banco de dados atual do banco de dados de fila em que a cópia principal da mensagem está armazenada.

  - Verificando a disponibilidade de cada servidor primário para o qual uma mensagem de sombra está na fila.

  - Notificações de descarte de processamento de servidores primários.

  - Remover as mensagens na sombra das filas sombra afinal esperado notificações de descarte são recebidas.

  - Decidindo quando o servidor de sombra deve assumir a propriedade de mensagens na sombra, tornando-se um servidor primário.

  - Bifurcations do acompanhamento de mensagens e outras mensagens de efeitos colaterais, como notificações de status de entrega (DSNs) e relatórios de diário para verificar a que cópia redundante da mensagem não lançada até que todas as bifurcações da mensagem são totalmente processadas.

A tabela a seguir descreve os parâmetros que controlam como as mensagens na sombra são mantidas.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Parâmetro</th>
<th>Valor padrão</th>
<th>Descrição</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>ShadowHeartbeatFrequency</em> em <strong>Set-TransportConfig</strong></p></td>
<td><p>2 minutos</p></td>
<td><p>A quantidade máxima de tempo que um servidor de sombra aguarda antes de abrir uma conexão de SMTP para o servidor primário para verificar o status de descarte de mensagens.</p></td>
</tr>
<tr class="even">
<td><p><em>ShadowResubmitTimeSpan</em> em <strong>Set-TransportConfig</strong></p></td>
<td><p>3 horas</p></td>
<td><p>Quanto tempo um servidor espera antes de decidir se um servidor principal falha e assume a propriedade de mensagens na sombra na fila de sombra para o servidor principal que está inacessível.</p></td>
</tr>
<tr class="odd">
<td><p><em>ShadowMessageAutoDiscardInterval</em> em <strong>Set-TransportConfig</strong></p></td>
<td><p>2 dias</p></td>
<td><p>Como um servidor de long mantém eventos de descarte de mensagens entregues com êxito. Filas de um servidor primário descartam eventos até consultado pelo servidor de sombra. No entanto, se o servidor de sombra não consultar o servidor primário para a duração especificada neste parâmetro, o servidor primário exclui os eventos de descarte na fila.</p></td>
</tr>
<tr class="even">
<td><p><em>SafetyNetHoldTime</em> em <strong>Set-TransportConfig</strong></p></td>
<td><p>2 dias</p></td>
<td><p>Quanto tempo as mensagens processadas com êxito são mantidas no Safety Net. Mensagens na sombra não confirmados eventualmente expiram da Safety Net após a soma de <em>SafetyNetHoldTime</em> e <em>MessageExpirationTimeout</em> em <strong>Set-TransportService</strong>.</p></td>
</tr>
<tr class="odd">
<td><p><em>MessageExpirationTimeout</em> em <strong>Set-TransportService</strong></p></td>
<td><p>2 dias</p></td>
<td><p>Quanto tempo uma mensagem pode permanecer em uma fila antes que ela expire.</p></td>
</tr>
</tbody>
</table>


Voltar ao início

## Processamento após uma interrupção de mensagem

Redundância de sombra minimiza a perda de mensagem devido a interrupções do servidor. Quando um servidor de transporte vem online novamente após uma interrupção, há dois cenários:

  - **O servidor for colocado online novamente com um novo banco de dados de transporte**   Neste cenário, o banco de dados de transporte é irrecuperável devido à falha de hardware ou corrupção de dados. Nesse caso, pois o servidor de transporte terá uma nova ID de banco de dados, ele será ser reconhecido como uma nova rota pelos outros servidores de transporte na organização. Isso também se aplica à situação em que um servidor não pôde ser recuperado e um novo servidor foi provisionado como um substituto.

  - **O servidor for colocado online novamente com o mesmo banco de dados de transporte**   Neste cenário, o servidor de transporte específica de não falhará, mas estava offline tempo suficiente para que o servidor de sombra para assumir a propriedade das mensagens e reenviá-los. Por exemplo, uma falha de placa de rede ou uma longa manutenção no servidor causaria neste cenário.

A tabela a seguir resume como a redundância de sombra reage a esses dois cenários. Para manter a clareza, suponha que o servidor que tinha uma interrupção é chamado Mailbox01.

### Processamento em cenários de recuperação de mensagens

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Cenário de recuperação</th>
<th>Medidas tomadas</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Mailbox01 vem online novamente com um novo banco de dados.</p></td>
<td><p>Quando Mailbox01 ficar indisponível, cada servidor que tem sombra mensagens em fila para Mailbox01 será assumem a propriedade dessas mensagens e reenviá-los. As mensagens, em seguida, obtém entregues aos seus destinos.</p>
<p>O atraso máximo para mensagens é o valor do parâmetro <em>ShadowHeartbeatFrequency</em> no cmdlet <strong>Set-TransportConfig</strong> . O valor padrão é 2 minutos.</p></td>
</tr>
<tr class="even">
<td><p>Mailbox01 vem online novamente com o mesmo banco de dados.</p></td>
<td><p>Após Mailbox01 for colocado online novamente, fornecerão as mensagens em suas filas, que já foram entregues pelos servidores que armazenam cópias de sombra de mensagens para Mailbox01. Isso resultará na entrega duplicada dessas mensagens. Usuários de caixa de correio do Exchange não verá mensagens duplicadas devido à detecção de mensagem duplicados. No entanto, os destinatários em sistemas de mensagens do Exchange não podem receber duplicadas cópias de mensagens.</p>
<p>O atraso máximo para mensagens é o valor do parâmetro <em>ShadowResubmitTimeSpan</em> no cmdlet <strong>Set-TransportConfig</strong> . O valor padrão é 3 horas.</p></td>
</tr>
</tbody>
</table>


Voltar ao início

