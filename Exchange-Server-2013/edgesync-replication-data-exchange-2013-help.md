---
title: 'Dados de replicação do EdgeSync: Exchange 2013 Help'
TOCTitle: Dados de replicação do EdgeSync
ms:assetid: c7dd137d-7ed4-4f16-9895-f354c449cf9b
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Bb232177(v=EXCHG.150)
ms:contentKeyID: 61183355
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Dados de replicação do EdgeSync

 

_**Aplica-se a:**Exchange Server 2013_

_**Tópico modificado em:**2015-03-09_

Quando você implanta um servidor de Transporte de Borda, ele não tem acesso ao Active Directory. Para realizar as tarefas de agregação de lista segura e pesquisa de destinatário, bem como para implementar a segurança de domínio usando a autenticação TLS mútua, o servidor de Transporte de Borda exige dados que estão no Active Directory. Esses dados são replicados para o servidor de Transporte de Borda usando o processo do EdgeSync e o servidor de Transporte de Borda armazena todas as informações replicadas nos Active Directory Lightweight Directory Services (AD LDS).

Este tópico se concentra nos dados replicados do Active Directory para os serviços AD LDS em um servidor de Transporte de Borda inscrito em um site do Active Directory. Para saber mais sobre o processo do EdgeSync e sobre as Inscrições de Borda, consulte [Inscrições de Borda](edge-subscriptions-exchange-2013-help.md).

Há quatro tipos de dados replicados para os serviços AD LDS e usados pelo servidor de Transporte de Borda:

Edge Subscription information

Configuration information

Recipient information

Topology information

## Informações de Inscrição de Borda

O Exchange 2013 estende os esquemas do Active Directory e do AD LDS para fornecer os atributos do objeto **ms-Exch-ExchangeServer** para representar os dados necessários ao controle do processo de sincronização do EdgeSync. Esses atributos oferecem três funções ao EdgeSync:

  - Manutenção e provisionamento automáticos das credenciais usadas para ajudar a proteger a conexão LDAP entre um servidor de Caixa de Correio e um servidor de Transporte de Borda.

  - Arbitram o processo de bloqueio e concessão de sincronização, garantindo que apenas um servidor por vez tentará a sincronização com um único servidor de Transporte de Borda. Para obter mais informações sobre o processo de bloqueio e concessão, consulte [Inscrições de Borda](edge-subscriptions-exchange-2013-help.md).

  - Otimizam o processo de sincronização do EdgeSync para manter um registro do status de sincronização atual. A facilidade em exibir o status de sincronização ajuda a evitar o excesso de sincronização manual.

A tabela a seguir lista as extensões de esquema específicas de Inscrições de Borda. Os valores designados para esses atributos são mantidos pela Inscrição de Borda e pelo processo de sincronização do EdgeSync. Eles não se destinam à edição manual.

### Extensões de esquema de Inscrição de Borda

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Nome do atributo</th>
<th>Descrição</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>ms-Exch-Server-EKPK-Public-Key</strong></p></td>
<td><p>A chave pública atual do certificado que está sendo usado pelo servidor. Esse valor é armazenado pelos servidores de Transporte de Borda e de Caixa de Correio. A chave pública destina-se a criptografar as credenciais usadas para autenticar o servidor durante a comunicação LDAP e SMTP.</p></td>
</tr>
<tr class="even">
<td><p><strong>ms-Exch-EdgeSync-Credential</strong></p></td>
<td><p>A lista de credenciais que o processo de sincronização EdgeSync usa para estabelecer uma sessão LDAP autenticada nos serviços AD LDS. Nos servidores de Caixa de Correio, esse atributo contém apenas as credenciais que o servidor de Caixa de Correio usa para autenticar-se nos servidores de Transporte de Borda inscritos. Nos servidores de Transporte de Borda, esse atributo contém as credenciais de cada servidor de Caixa de Correio no site inscrito do Active Directory que participa do processo de sincronização do EdgeSync. Esse atributo só está presente nos servidores de Caixa de Correio que executam o processo de sincronização do EdgeSync e nos servidores de Transporte de Borda inscritos.</p></td>
</tr>
<tr class="odd">
<td><p><strong>ms-Exch-Edge-Sync-Lease</strong></p></td>
<td><p>Usado para arbitrar entre servidores de Caixa de Correio quando mais de um deles tenta replicar para o mesmo servidor de Transporte de Borda.</p></td>
</tr>
<tr class="even">
<td><p><strong>ms-Exch-Edge-Sync-Status</strong></p></td>
<td><p>Só está presente nos serviços AD LDS do objeto de servidor de Transporte de Borda. Esse atributo rastreia o status de replicação para uma instância dos serviços AD LDS e inclui informações sobre replicação.</p></td>
</tr>
</tbody>
</table>


Voltar ao início

## Informações de configuração

Ao inscrever um servidor de Transporte de Borda na organização, você pode gerenciar, de dentro da organização, os objetos de configuração que são comuns ao servidor de Transporte de Borda e à organização do Exchange. Essas alterações serão replicadas para o servidor de Transporte de Borda usando o serviço de sincronização do EdgeSync. Esse processo ajuda a manter uma configuração consistente em todos os servidores envolvidos no processamento de mensagens.

Um subconjunto dos dados de configuração para a organização do Exchange também deve ser mantido no servidor de Transporte de Borda. Durante o processo de sincronização do EdgeSync, os dados de configuração dos quais o servidor de Transporte de Borda precisa são gravados na partição de configuração dos serviços AD LDS. Os dados de configuração gravados nos serviços AD LDS incluem o seguinte:

  - **Servidores de Caixa de Correio**   O nome de domínio totalmente qualificado (FQDN) de cada servidor de Caixa de Correio no site inscrito do Active Directory é disponibilizado para o repositório local dos serviços AD LDS no servidor de Transporte de Borda. Essas informações são usadas para obter uma lista de servidores de host inteligente para o conector de envio de entrada.

  - **Domínios aceitos**   Todos os domínios de retransmissão internos e externos autoritativos, configurados para a organização do Exchange, são gravados nos serviços AD LDS. Os domínios aceitos estando disponíveis ao servidor de Transporte de Borda permitem que a organização do Exchange execute a filtragem de domínios e rejeite o tráfego SMTP inválido na organização o mais rápido possível. Para obter mais informações sobre domínios aceitos, consulte [Domínios aceitos](accepted-domains-exchange-2013-help.md).

  - **Classificações de mensagem**   Se classificações de mensagem estiverem disponíveis no servidor de Transporte de Borda, agentes de transporte e conversão de conteúdo poderão agir de acordo com as classificações de mensagem na rede de perímetro. Por exemplo, o agente de Filtragem de Anexo pode aplicar a classificação Anexo Removido ao remover um anexo. Por essa razão, um texto informativo será exibido a um usuário do Microsoft Outlook ou do Outlook Web App para informar ao destinatário o que ocorreu. Os agentes que são desenvolvidos para serem usados por aplicativos de terceiros podem usar as classificações de mensagem de maneira semelhante.

  - **Domínios remotos**   Todas as entradas de domínio remoto configuradas para a organização do Exchange são gravadas nos serviços AD LDS. As entradas de domínio remoto controlam as configurações de mensagem de ausência temporária e de formato de mensagem para um domínio remoto. Para obter mais informações sobre domínios remotos, consulte [Domínios remotos](remote-domains-exchange-2013-help.md).

  - **Conectores de envio**   Por padrão, os conectores de Envio exigidos para habilitar todo o fluxo de mensagens entre a organização do Exchange e a Internet são criados automaticamente. Todos os Conectores de Envio existentes no servidor de Transporte de Borda são excluídos. Para configurar conectores de Envio adicionais, configure o conector de Envio na organização do Exchange e selecione a Inscrição de Borda como o servidor de origem do conector. Para obter mais informações, consulte [Inscrições de Borda](edge-subscriptions-exchange-2013-help.md).

  - **Servidores SMTP internos**   O valor do atributo *InternalSMTPServers* é armazenado no objeto **TransportConfig** para a organização do Exchange e o servidor de Transporte de Borda local. Durante o processo de sincronização do EdgeSync, o valor que é armazenado no objeto do servidor de Transporte de Borda local é substituído pelo valor que é armazenado nesse objeto para a organização do Exchange. Esse atributo especifica uma lista de endereços IP ou intervalos de endereços IP de servidores SMTP internos que devem ser ignorados pelo recurso de ID de remetente e de filtragem de conexão.

  - **Listas Seguras do Domínio**   Os atributos *TLSReceiveDomainSecureList* e *TLSSendDomainSecureList* são armazenados no objeto **TransportConfig** para a organização do Exchange e o servidor de Transporte de Borda local. Durante o processo de sincronização do EdgeSync, o valor que é armazenado no objeto do servidor de Transporte de Borda local é substituído pelo valor que é armazenado nesse objeto para a organização do Exchange. Esses atributos especificam a lista de domínios remotos configurados para autenticação TLS mútua.

Voltar ao início

## Informações de destinatário

As informações de destinatário replicadas para os serviços AD LDS incluem apenas um subconjunto dos atributos de destinatário. Somente os dados que o servidor de Transporte de Borda precisa para executar determinadas tarefas antispam são replicados. As informações de destinatário replicadas para os serviços AD LDS incluem o seguinte:

  - **Destinatários**   A lista de destinatários da organização do Exchange é replicada para os serviços AD LDS. Cada destinatário é identificado pela GUID atribuída a ele no Active Directory. Se você configurar uma conta de destinatário para recusar o recebimento de emails de fora da organização, o destinatário não será replicado para os serviços AD LDS. Se a caixa de correio de um destinatário for desabilitada ou excluída, ela não será replicada para os serviços AD LDS.

  - **Endereços de proxy**   Todos os endereços de proxy atribuídos a cada destinatário são replicados para os serviços AD LDS como dados hash. Esse é um hash unidirecional que usa o Secure Hash Algorithm (SHA)-256. O SHA-256 gera uma compilação de mensagem de 256 bits dos dados originais. O repositório de endereços de proxy como dados hash ajuda a proteger essas informações, no caso de comprometimento do servidor de Transporte de Borda ou dos serviços AD LDS. Os endereços de proxy são consultados quando o servidor de Transporte de Borda executa a tarefa antispam de pesquisa de destinatário.

  - **Lista de Remetentes Seguros, Lista de Remetentes Bloqueados e Lista de Destinatários Seguros**   As listas de Remetentes Seguros, Remetentes Bloqueados e Destinatários Seguros que são definidas na instância do Outlook de cada destinatário são agregadas e replicadas para os serviços AD LDS. Essas definições ficam no repositório de caixa de correio no qual reside a caixa de correio do destinatário. Uma coleção de lista segura do usuário do Outlook é formada pelos dados combinados da Lista de Remetentes Seguros, da Lista de Destinatários Seguros, da Lista de Remetentes Bloqueados e dos contatos externos do usuário. A disponibilidade dos dados da coleção de lista segura nos serviços AD LDS permite que o servidor de Transporte de Borda faça triagem dos remetentes de modo apropriado, reduzindo a sobrecarga operacional envolvida na filtragem de emails. Essas informações são enviadas como dados específicos.
    

    > [!IMPORTANT]
    > Embora os dados de destinatário seguro sejam armazenados no Outlook e possam ser agregados à coleção de lista segura na instância dos serviços AD LDS no servidor de Transporte de Borda, a funcionalidade de filtragem de conteúdo não atua nos dados de destinatário seguro.



  - **Configurações de antispam por destinatário**   Com o uso do cmdlet **Set-Mailbox**, você pode atribuir configurações de limite de antispam por destinatário que sejam diferentes das configurações de antispam de toda a organização. Se você definir as configurações de antispam por destinatário, elas substituirão as configurações de toda a organização. Com a replicação dessas configurações para os serviços AD LDS, as configurações por destinatário poderão ser consideradas antes da retransmissão da mensagem para a organização do Exchange. Essas informações são enviadas como dados hash.

Voltar ao início

## Informações de topologia

As informações de topologia incluem a notificação de servidores de Transporte de Borda recém-inscritos ou Inscrições de Borda removidas. Esses dados são atualizados a cada cinco minutos.

Voltar ao início

