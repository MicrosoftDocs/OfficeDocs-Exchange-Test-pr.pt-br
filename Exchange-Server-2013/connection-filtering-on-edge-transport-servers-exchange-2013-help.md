---
title: 'Servidores de transporte de borda de filtragem de Conexão: Exchange 2013 Help'
TOCTitle: Nos servidores de transporte de borda de filtragem de Conexão
ms:assetid: b513755c-5d3e-44fa-a6cb-771d48b544ac
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Bb124320(v=EXCHG.150)
ms:contentKeyID: 60829937
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Nos servidores de transporte de borda de filtragem de Conexão

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2015-03-09_

Filtragem de conexão é um recurso antispam do Microsoft Exchange Server 2013 que permite ou bloqueia emails de acordo com a origem da mensagem. A filtragem de conexão é feita pelo agente Filtragem de Conexão, que está disponível somente em servidores de Transporte de Borda. O agente Filtragem de Conexão considera o endereço IP do servidor de email conectado para determinar a ação (se houver) a ser executada em uma mensagem de entrada.

Por padrão, o agente Filtragem de Conexão é o primeiro agente antispam a avaliar uma mensagem de entrada em um servidor de Transporte de Borda. O endereço IP de origem da conexão SMTP é verificado nos endereços IP permitidos e bloqueados. Se o endereço IP de origem for especificamente permitido, a mensagem será enviada para os destinatários da sua organização sem ser processada por outros agentes antispam. Se o endereço IP de origem for especificamente bloqueado, a conexão SMTP será eliminada. Se o endereço IP de origem não for especificamente permitido ou bloqueado, a mensagem passará pelos demais agentes antispam do servidor de Transporte de Borda.

A filtragem de conexão compara o endereço IP do servidor de email de origem com os valores da lista de IPs Permitidos, da lista de IPs Bloqueados e com os provedores de listas de IPs permitidos e bloqueados. Você precisa configurar pelo menos um desses quatro repositórios de dados de endereços IP para que a filtragem de conexão funcione. Se não especificar qualquer dado de endereço IP, será preciso desabilitar o agente Filtragem de Conexão. Para obter mais informações, consulte [Gerenciar nos servidores de transporte de borda de filtragem de Conexão](manage-connection-filtering-on-edge-transport-servers-exchange-2013-help.md).

**Sumário**

IP Block list

IP Allow list

IP Block List providers

IP Allow List providers

Test IP Block List providers and IP Allow List providers

Configure connection filtering on Edge Transport servers that aren't directly connected to the Internet

## Lista de IPs Bloqueados

A lista de IPs Bloqueados contém os endereços IP de servidores de email que você quer bloquear. Atualize manualmente os endereços IP da lista de IPs Bloqueados. Você pode adicionar cada endereço IP ou intervalos de endereços IP. E pode especificar uma data e hora de expiração que defina por quanto tempo a entrada de endereço IP ficará bloqueada. Quando a data e hora da expiração for atingida, a entrada de endereço IP da lista de IPs Bloqueados será desabilitada.

Se o agente Filtragem de Conexão encontrar o endereço IP de origem na lista de IPs Bloqueados, a conexão SMTP será eliminada depois que todos os cabeçalhos **RCPT TO** (destinatários de envelope) da mensagem forem processados.

Endereços IP também podem ser adicionados automaticamente à lista de IPs Bloqueados pelo recurso Reputação de Remetente do agente Análise de Protocolo. Para obter mais informações, consulte [Reputação do remetente e o agente de análise de protocolo](sender-reputation-and-the-protocol-analysis-agent-exchange-2013-help.md).

## Lista de IPs Permitidos

A lista de IPs Permitidos contém os endereços IP de servidores de email que você quer definir como fontes confiáveis de email. Os emails vindos dos servidores de email que você especificar na lista de IPs Permitidos serão liberados do processamento por outros agentes antispam do Exchange.

Atualize manualmente os endereços IP da lista de IPs Permitidos. Você pode adicionar cada endereço IP ou intervalos de endereços IP. E especifique uma data e hora de expiração que defina por quanto tempo a entrada de endereço IP será permitida. Quando a data e hora da expiração for atingida, a entrada de endereço IP da lista de IPs Permitidos será desabilitada.

Voltar ao início

## Provedores de Lista de IPs Bloqueados

Os provedores de lista de IPs Bloqueados são normalmente chamados de *listas de bloqueio em tempo real* ou RBLs. Os provedores de lista de IPs Bloqueados compilam listas de endereços IP de servidor de email que envia spam. Muitos provedores de lista de IPs Bloqueados também compilam listas de endereços IP de servidores de email que podem ser usados para spam. Incluem, por exemplo, servidores de email configurados para provedores de serviço de Internet de retransmissão aberta (ISPs), que atribuem endereços IP dinâmicos, e ISPs que permitem tráfego de servidor de email SMTP de contas dial-up.

Quando você configura a filtragem de conexão para usar um provedor de lista de IPs Bloqueados, o agente Filtragem de Conexão compara os endereços IP do servidor de email de conexão com a lista de endereços IP do provedor de lista de IPs Bloqueados. Se houver correspondência, a mensagem não será permitida na sua organização. Você pode configurar a filtragem de conexão para usar vários provedores de lista de IPs Bloqueados e atribuir diferentes valores de prioridade a cada provedor.

O agente Filtragem de Conexão verifica o endereço IP de origem na lista de IPs Permitidos e na lista de IPs Bloqueados. Se o endereço IP não estiver em nenhuma das listas, o agente Filtragem de Conexão consultará o provedor de lista de IPs Bloqueados, de acordo com o valor de prioridade atribuído. Se o endereço IP estiver em um provedor de lista de IPs Bloqueados, o servidor de Transporte de Borda aguardará e processará o cabeçalho **RCPT TO**, responderá ao servidor de email emissor com um erro `SMTP 550` e encerrará a conexão. A conexão não é imediatamente eliminada para que a tentativa de conexão seja registrada e porque você pode especificar destinatários liberados de bloqueio nas mensagens por qualquer provedor de lista de IPs Bloqueados.

Se o endereço IP não for definido em nenhum dos provedores de lista de IPs Bloqueados, o agente Filtragem de Conexão transmitirá a mensagem para o próximo agente de transporte no servidor de Transporte de Borda.

Em cada provedor de lista de IPs Bloqueados, você pode personalizar o erro `SMTP 550` retornado ao remetente quando uma mensagem é bloqueada. Você deve identificar o provedor de lista de IPs Bloqueados que definiu a fonte da mensagem como spam. Se um servidor de email de origem legítima for identificado incorretamente como fonte de spam, o administrador poderá entrar em contato com o provedor da lista de IPs Bloqueados, que tomará as medidas necessárias para remover o servidor de email do provedor de lista de IPs Bloqueados.

Os provedores de lista de IPs Bloqueados podem retornar códigos diferentes para identificar por que um endereço IP consta em suas listas. A maioria dos provedores de lista de IPs Bloqueados retorna tipos de dados bitmask ou de valor absoluto. Nesses tipos de dados, o provedor de lista de IPs Bloqueados pode usar diversos valores para classificar o endereço IP por tipo de ameaça.

Há questões a considerar quando os provedores de lista de IPs Bloqueados são utilizados:

  - Interrupções ou atrasos no serviço de provedor de lista de IPs Bloqueados podem causar atrasos no processamento de mensagens no servidor de Transporte de Borda. Você deve sempre selecionar provedores de lista de IPs Bloqueados.

  - Servidores de origem que você sabe que são legítimos podem ser incorretamente identificados como fontes de spam. Por exemplo, o servidor de email pode ser inadvertidamente configurado para agir como retransmissão aberta. Você deve sempre selecionar provedores de lista de IPs Bloqueados que forneçam procedimentos claros para avaliação e remoção dos serviços.

Voltar ao início

## Exemplos de bitmask e valores absolutos

Essa seção mostra um exemplo dos códigos de status retornados pela maioria dos provedores de Lista de Bloqueios. Para detalhes sobre os códigos de status retornados pelo provedor, consulte a documentação do provedor específico.

Para tipos de dados bitmask, o serviço de provedor de Lista de IPs Bloqueados retorna o código de status 127.0.0.*x*, onde o inteiro *x* é um dos valores listados na tabela a seguir.

### Códigos de valores e status para tipos de dados bitmask

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Valor</th>
<th>Código de status</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>1</p></td>
<td><p>O endereço IP está numa Lista de IPs Bloqueados.</p></td>
</tr>
<tr class="even">
<td><p>2</p></td>
<td><p>O servidor SMTP está configurado para atuar como uma retransmissão aberta.</p></td>
</tr>
<tr class="odd">
<td><p>4</p></td>
<td><p>O endereço IP oferece suporte a um endereço IP de dial-up.</p></td>
</tr>
</tbody>
</table>


Para tipos de valores absolutos, o provedor de lista de IPs Bloqueados retorna respostas explícitas que definem por que o endereço IP figura em suas listas de bloqueio. A tabela a seguir mostra alguns exemplos de valores absolutos e respostas explícitas.

### Códigos de valores e status para tipos de dados de valor absoluto

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Valor</th>
<th>Resposta explícita</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>127.0.0.2</p></td>
<td><p>O endereço IP é uma fonte de spam direta.</p></td>
</tr>
<tr class="even">
<td><p>127.0.0.4</p></td>
<td><p>O endereço IP envia emails em massa.</p></td>
</tr>
<tr class="odd">
<td><p>127.0.0.5</p></td>
<td><p>O servidor remoto que está enviando a mensagem é conhecido por oferecer suporte a retransmissões abertas de vários estágios.</p></td>
</tr>
</tbody>
</table>


Voltar ao início

## Provedores de Lista de IPs Permitidos

Provedores de lista de IPs Permitidos também são conhecidos como *listas seguras* ou *listas brancas*. Os provedores de lista de IPs Permitidos são configurados exatamente como os provedores de lista de IPs Bloqueados, mas os resultados são opostos: eles definem endereços IP de servidores de email que definitivamente não estão associados a atividades de spam. Se o endereço IP do servidor de email de conexão figurar em um provedor de lista de IPs Permitidos, a mensagem ficará liberada do processamento por outros agentes antispam do Exchange. Por esse motivo, os provedores de lista de IPs Bloqueados são usados com muito mais frequência do que os provedores de lista de IPs Permitidos. Seja cuidadoso ao selecionar provedores de lista de IPs Permitidos.

Voltar ao início

## Testar os provedores de lista de IPs Bloqueados e de IPs Permitidos

Depois de configurar a filtragem de conexão para usar um provedor de lista de IPs Bloqueados ou de IPs Permitidos, você poderá fazer testes para verificar se os provedores estão funcionando corretamente. A maioria dos provedores fornece endereços IP que você pode usar para testar seus serviços. Ao testar um provedor, o agente Filtragem de Conexão emite uma consulta DNS que deve resultar em uma resposta específica do provedor. Para obter mais informações sobre como testar os endereços IP com um serviço de provedor de lista de IPs Bloqueados ou de IPs Permitidos, consulte [Gerenciar nos servidores de transporte de borda de filtragem de Conexão](manage-connection-filtering-on-edge-transport-servers-exchange-2013-help.md).

Voltar ao início

## Configurar a filtragem de conexão em servidores de Transporte de Borda que não estejam diretamente conectados à Internet

Você pode usar a filtragem de conexão em servidores de Transporte de Borda que não recebam emails diretamente da Internet. Nesse cenário, o servidor de Transporte de Borda está usando outro servidor de email, que recebe e processa as mensagens diretamente da Internet. Por exemplo, a sua organização pode enviar tráfego de emails por um servidor, serviço ou aplicativo antispam antes de as mensagens chegarem ao servidor de Transporte de Borda. Nesse cenário, o agente Filtragem de Conexão precisa extrair o endereço IP de origem correto da mensagem. Para fazer isso, o agente Filtragem de Conexão precisa analisar os valores do campo de cabeçalho **Received** e comparar esses valores aos endereços IP conhecidos do servidor de email que fica entre o servidor de Transporte de Borda e a Internet.

Cada servidor de email que aceite e transmita uma mensagem SMTP no caminho de entrega adiciona seu próprio campo de cabeçalho **Received** ao cabeçalho da mensagem. O cabeçalho **Received** contém, geralmente, o nome de domínio e o endereço IP do servidor de email que processou a mensagem.

Se o servidor de Transporte de Borda não aceitar mensagens diretamente da Internet, você precisará usar o parâmetro *InternalSMTPServers* no cmdlet **Set-TransportConfig** em um servidor de Caixa de Correio do Exchange 2013 para identificar o endereço IP do servidor de email que fica entre o servidor de Transporte de Borda e a Internet. Os dados de endereço IP são replicados nos servidores de Transporte de Borda pelo EdgeSync. Quando são recebidas mensagens pelo servidor de Transporte de Borda, o agente Filtragem de Conexão considera que um endereço IP em um campo de cabeçalho **Received** não corresponde a um valor especificado pelo parâmetro *InternalSMTPServers*, que é o endereço IP de origem que precisa ser verificado. Portanto, você precisa especificar todos os servidores SMTP internos para que a filtragem de conexão funcione corretamente.

Voltar ao início

