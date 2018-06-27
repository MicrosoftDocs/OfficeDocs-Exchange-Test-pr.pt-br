---
title: 'Servidor de Caixa de Correio: Exchange 2013 Help'
TOCTitle: Servidor de Caixa de Correio
ms:assetid: 1aacc1c9-c81b-47d4-b222-ee73956cf968
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/JJ150491(v=EXCHG.150)
ms:contentKeyID: 50485132
ms.date: 01/10/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Servidor de Caixa de Correio

 

_**Aplica-se a:**Exchange Server 2013_

_**Tópico modificado em:**2013-02-19_

No Microsoft Exchange Server 2010, a função de servidor Caixa de Correio hospedava os bancos de dados de caixa de correio e de bancos de dados de pasta pública e também fornecia o armazenamento de emails. Agora, no Exchange Server 2013, a função de servidor Caixa de Correio também inclui os protocolos de Acesso para Cliente, serviço de Transporte, bancos de dados de caixa de correio e componentes de Unificação de Mensagem.

No Exchange 2013, a função de servidor Caixa de Correio interage diretamente com o Active Directory, o servidor de Acesso para Cliente e clientes do Outlook no seguinte processo:

  - O servidor de Caixa de Correio usa o LDAP para acessar informações de configuração do destinatário, do servidor e da organização do Active Directory.

  - O servidor de Acesso para Cliente envia solicitações de clientes para o servidor de Caixa de Correio, e retorna dados do servidor de Caixa de Correio para os clientes. O servidor de Acesso para Cliente também acessa arquivos do catálogo de endereços online (OAB) no servidor de Caixa de Correio, através do compartilhamento de arquivos NetBIOS. O servidor de Acesso para Cliente envia mensagens, dados de disponibilidade, configurações de perfil de cliente e dados de OAB entre o cliente e o servidor de Caixa de Correio.

  - Os clientes do Outlook dentro do seu firewall acessam o servidor de Acesso do Cliente para enviar e recuperar mensagens. Os clientes do Outlook fora do firewall podem acessar o servidor de Acesso para Cliente, usando o Outlook em Qualquer Lugar (que usa o componente RPC sobre Proxy HTTP).

  - As caixas de correio de pasta pública são acessíveis via RPC sobre HTTP, independente de o cliente estar fora ou dentro do firewall.

  - O computador apenas de administrador recupera informações de topologia do Active Directory do serviço de Topologia do Microsoft Exchange Active Directory. Ele também recupera informações de políticas de endereço de email e de listas de endereços.

  - O servidor de Acesso para Cliente usa LDAP ou NSPI (Interface de Provedor de Serviço de Nome) para contatar o servidor do Active Directory e recuperar informações do Active Directory de usuários.

**Arquitetura e interação de servidor de Caixa de Correio e Acesso para Cliente**

![Interação de servidor de Acesso para Cliente e Caixa de Correio](images/JJ150491.d14577bf-14f9-40fa-bd49-a92932eb003a(EXCHG.150).gif "Interação de servidor de Acesso para Cliente e Caixa de Correio")

Para mais detalhes, consulte a seção "Arquitetura do Exchange 2013" em [Novidades do Exchange 2013](what-s-new-in-exchange-2013-exchange-2013-help.md).

## Novos recursos de Caixa de Correio

A seguinte lista descreve, resumidamente, alguns dos recursos novos e dos aperfeiçoados na função de Caixa de Correio do Exchange 2013:

  - Evolução do grupo de disponibilidade de banco de dados (DAG) do Exchange 2010:
    
      - O código do log de transações foi retrabalhado para failover rápido, com um ponto de verificação profundo para cópias passivas de bancos de dados.
    
      - Para oferecer suporte à resiliência de site aperfeiçoada, os servidores podem estar em locais diferentes.

  - O Exchange 2013 agora hospeda alguns componentes de Acesso para Cliente, os componentes de Transporte e os componentes de Unificação de Mensagens.

  - O Repositório do Exchange foi reescrito em código gerenciado, para melhorar o desempenho em redução de confiabilidade de E/S adicionais.

  - Cada banco de dados do Exchange 2013 agora é executado sob o seu próprio processo.

  - A Pesquisa Inteligente substituiu a infraestrutura de pesquisa em várias caixas de correio do Exchange 2010.

## Proteção dos servidores de Caixa de Correio

Por padrão, a comunicação HTTP, Microsoft Exchange ActiveSync, POP3 e IMAP4 entre os servidores de Caixa de Correio e outras funções de servidor do Exchange, controladores de domínio e servidores de catálogo global é criptografada. Além disso, certifique-se de que seus servidores de Caixa de Correio não possam ser acessados pela Internet.

## Para obter mais informações

[Unificação de mensagens](unified-messaging-exchange-2013-help.md)

[Fluxo de mensagens](mail-flow-exchange-2013-help.md)

[Alta disponibilidade e resiliência de site](high-availability-and-site-resilience-exchange-2013-help.md)

[Conformidade e política de sistema de mensagens](messaging-policy-and-compliance-exchange-2013-help.md)

[Movimentações de caixa de correio no Exchange 2013](mailbox-moves-in-exchange-2013-exchange-2013-help.md)

[Gerenciar bancos de dados de caixa de correio no Exchange 2013](manage-mailbox-databases-in-exchange-2013-exchange-2013-help.md)

[Conformidade e política de sistema de mensagens](messaging-policy-and-compliance-exchange-2013-help.md)

[Destinatários](recipients-exchange-2013-help.md)

[Colaboração](collaboration-exchange-2013-help.md)

