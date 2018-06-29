---
title: 'Novidades do Exchange 2013: Exchange 2013 Help'
TOCTitle: Novidades do Exchange 2013
ms:assetid: 97501135-2149-4590-8373-98e638ac8eb1
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/JJ150540(v=EXCHG.150)
ms:contentKeyID: 50486176
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Novidades do Exchange 2013

 

_**Aplica-se a:**Exchange Server 2013_

_**Tópico modificado em:**2016-12-09_

Faça check-out de todos os recursos mais recentes no Exchange 2013.

O Microsoft Exchange Server 2013 apresenta um conjunto novo e sofisticado de tecnologias, recursos e serviços para a linha de produtos do Exchange Server. Sua meta é dar suporte às pessoas e às organizações à medida que seus hábitos de trabalho evoluem de um foco na comunicação para um foco na colaboração. Ao mesmo tempo, o Exchange Server 2013 ajuda a baixar o custo total de propriedade, independentemente de você implantar o Exchange 2013 localmente ou provisionar suas caixas de correio na nuvem. Novos recursos e funcionalidade no Exchange 2013 foram criados para:

  - **Dar suporte a uma força de trabalho de várias gerações**   Promover a integração social e facilitar a localização de pessoas é importante para os usuários. A *Pesquisa Inteligente* aprende com o comportamento de comunicação e colaboração dos usuários para aprimorar e priorizar os resultados da pesquisa no Exchange. Além disso, com o Exchange 2013, os usuários podem mesclar contatos de várias fontes para fornecer uma visão única de uma pessoa, vinculando informações de contato extraídas de vários locais.

  - **Proporcionar uma experiência envolvente**   O Microsoft Outlook 2013 e o Microsoft Outlook Web App têm uma nova aparência. O Outlook Web App apresenta uma ênfase em uma interface do usuário simplificada que também oferece suporte ao uso de toque, aprimorando a experiência de uso do Exchange em dispositivos móveis.

  - **Integrar com SharePoint e Lync**   O Exchange 2013 oferece maior integração com o Microsoft SharePoint 2013 e o Microsoft Lync 2013 por meio de caixas de correio de site e Descoberta Eletrônica In-loco. Juntos, esses produtos oferecem um conjunto de recursos que possibilitam cenários como Descoberta eletrônica empresarial e colaboração usando caixas de correio de site.

  - **Ajuda a atender a expansão das necessidades de conformidade**    Conformidade e Descoberta Eletrônica representam um desafio para muitas organizações. ajuda você a encontrar e pesquisar dados não apenas no Exchange, mas na sua organização. Com pesquisa e indexação aprimoradas, você pode pesquisar no Exchange 2013, no Lync 2013, no SharePoint 2013 e nos servidores de arquivos do Windows. Além disso, a prevenção de perda de dados (DLP) pode ajudar a manter sua organização protegida contra usuários que enviam informações confidenciais acidentalmente para pessoas não autorizadas. A DLP ajuda a identificar, monitorar e proteger dados confidenciais por meio de uma profunda análise de conteúdo.

  - **Fornecer uma solução resiliente**   O Exchange 2013 foi criado com base na arquitetura do Exchange Server 2010 e foi reprojetado para proporcionar simplicidade de escala, utilização de hardware e isolamento de falhas.

Para obter informações sobre as alterações feitas no Exchange Server 2013 RTM, consulte [Atualizações para o Exchange 2013](updates-for-exchange-2013-exchange-2013-help.md).

Veja as seguintes seções para obter mais informações sobre as novidades no Exchange 2013:

Exchange admin center

Exchange 2013 architecture

Configuração

Messaging policy and compliance

Anti-malware protection

Mail flow

Destinatários

Sharing and collaboration

Integration with SharePoint and Lync

Clients and mobile

Unified Messaging

Batch mailbox moves

[Alta disponibilidade e resiliência de site](high-availability-and-site-resilience-exchange-2013-help.md)

Exchange workload management


> [!TIP]
> Para obter informações sobre recursos de versões anteriores do Exchange que foram removidos, descontinuados ou substituídos no Exchange Server 2013, consulte <A href="what-s-discontinued-in-exchange-2013-exchange-2013-help.md">O que será descontinuado no Exchange 2013</A>. Além disso, você pode ter interesse em <A href="release-notes-for-exchange-2013-exchange-2013-help.md">Notas de versão do Exchange 2013</A>.



## Centro de Administração do Exchange

O Exchange 2013 fornece um console de gerenciamento unificado que facilita o uso e é otimizado para o gerenciamento de implantações híbridas, no local ou online. O *centro de administração do Exchange* (EAC) no Exchange 2013 substitui o Console de Gerenciamento do Exchange (EMC) do Exchange 2010 e o Painel de Controle do Exchange (ECP). Porém, \&quot;ECP\&quot; ainda é o nome do diretório virtual usado pelo EAC. Alguns recursos do EAC:

  - **Modo de exibição de lista**   O modo de exibição de lista do EAC foi projetado para remover as principais limitações que existiam no ECP. O ECP era limitado a exibir até 500 objetos e, para exibir objetos que não estavam listados no painel de detalhes, você precisava usar pesquisas e filtros para encontrar esses objetivos específicos. No Exchange 2013, o limite de exibição de dentro do modo de exibição em lista do EAC é de, aproximadamente, 20.000 objetos. Depois que o EAC retorna os resultados, o cliente do EAC executa a pesquisa e a classificação, o que aumenta muito o desempenho em comparação com o ECP no Exchange 2010. Além disso, acrescentou-se a paginação, para você poder paginar os resultados. Você também pode configurar o tamanho da página e exportar para um arquivo .csv.

  - **Adicionar/remover colunas para o modo de exibição de lista do Destinatário**   Você pode escolher quais colunas exibir e, com cookies locais, salvar seus modos de exibição de lista personalizados em cada computador que utilizar para acessar o EAC.

  - **Proteger o diretório virtual do ECP**   Você pode particionar o acesso da Internet e de intranets de dentro do diretório virtual do IIS do ECP, para permitir ou bloquear recursos de gerenciamento. Com esse recurso, você pode permitir ou negar acesso a usuários tentando acessar o EAC da Internet fora do seu ambiente organizacional, ao mesmo tempo em que permite o acesso às opções do Outlook Web App do usuário final.

  - **Gerenciamento de Pasta Pública**   No Exchange 2010 e no Exchange 2007, as pastas públicas eram gerenciadas através do console de administração de Pasta Pública. As pastas públicas agora estão no EAC, e você não precisa de uma ferramenta separada, para gerenciá-las.

  - **Notificações**   No Exchange 2013, o EAC agora tem um visualizador de Notificações, para que você possa exibir o status os processos de longa duração e, se preferir, receber uma notificação via email, quando o processo terminar.

  - **Editor de Usuário do Controle de Acesso Baseado em Função (RBAC)**   No Exchange 2010, você podia usar o Editor de Usuário do RBAC na Caixa de Ferramentas do Exchange para adicionar usuários a grupos de funções de gerenciamento. No Exchange 2013, a funcionalidade do Editor de Usuário do RBAC agora está no EAC, e você não precisa de uma ferramenta separada para gerenciar o RBAC.

  - **Ferramentas de Unificação de Mensagens**   No Exchange 2010, você podia usar as ferramentas Estatísticas de Chamada e Logs de Chamada do Usuário para ajudar a fornecer estatísticas de UM e informações sobre chamadas específicas de um usuário habilitado para UM. No Exchange 2013, as ferramentas Estatísticas de Chamada e Logs de Chamada do Usuário agora estão no EAC, e você não precisa de uma ferramenta separada para gerenciá-las.

  - **Melhorias dos grupos**   O EAC (Centro de Administração do Exchange) agora pode exibir até 10.000 destinatários na janela **GruposSelecionar Membros**. Por padrão, até 500 destinatários são retornados quando você abre a janela **Selecionar Membros**, porém, você pode optar por listar até 10.000 destinatários clicando em **Obter Todos os Resultados**, sob a lista de destinatários. Agora, nós damos suporte à busca em mais de 500 destinatários por meio da barra de rolagem, e também acrescentamos recursos de pesquisa aprimorados para habilitar a filtragem dos destinatários exibidos na lista. Você pode filtrar por:
    
      - cidade
    
      - empresa
    
      - país/região
    
      - departamento
    
      - escritório
    
      - título

Para mais informações, consulte [Centro de administração do Exchange no Exchange 2013](exchange-admin-center-in-exchange-2013-exchange-2013-help.md).

## Arquitetura do Exchange 2013

As versões anteriores do Exchange foram otimizadas e arquitetadas com certas restrições tecnológicas que existiam naquele momento. Por exemplo, durante o desenvolvimento do Exchange 2007, uma das principais restrições era o desempenho da CPU. Para aliviar essa restrição, o Exchange 2007 foi dividido em diferentes funções de servidor que permitiam realizar o dimensionamento por meio da separação de servidores. No entanto, as funções de servidor no Exchange 2007 e Exchange 2010 foram fortemente aglutinadas. A aglutinação das funções teve seus lados negativos, incluindo dependência de versão, geoafinidade (exigindo todas as funções de um site específico), afinidade de sessão (exigindo balanceamento de carga de hardware de camada 7 de alto custo) e complexidade de namespace.

Atualmente, o poder de processamento da CPU tem um custo bem menor e não é mais um fator de restrição. Com essa restrição eliminada, a meta principal de design do Exchange 2013 passou a ser simplicidade de escala, utilização de hardware e isolamento de falha. Com o Exchange 2013, reduzimos o número de funções de servidor para três: a função de servidor de Acesso para Cliente, de Caixa de Correio e de Transporte de Borda.

O servidor de Caixa de correio inclui todos os componentes de servidor tradicionais encontrados no Exchange 2010: os protocolos de Acesso para Cliente, o serviço de Transporte, os bancos de dados de Caixa de Correio e a Unificação de Mensagens. O servidor de Caixa de Correio lida com toda a atividade das caixas de correio ativas nesse servidor. O servidor de Acesso para Cliente fornece autenticação, redirecionamento limitado e serviços de proxy. O servidor de Acesso para Cliente em si não faz nenhuma renderização de dados. O servidor de Acesso para Cliente é um servidor fino e sem monitoração de estado. Nunca há nada na fila ou armazenado no servidor de Acesso para Cliente. O servidor de Acesso para Cliente oferece todos os protocolos de acesso para cliente comuns: HTTP, POP e IMAP e SMTP.

Com essa nova arquitetura, o servidor de Acesso para Cliente e o servidor de Caixa de Correio se tornaram \&quot;flexivelmente combinados\&quot;. Todo o processamento e a atividade de uma caixa de correio específica ocorre no servidor de Caixa de Correio que hospeda a cópia de banco de dados ativa em que a caixa de correio reside. Toda a transformação e toda a renderização de dados são executadas localmente na cópia de banco de dados ativa, eliminando preocupações de compatibilidade de versão entre o servidor de Acesso para Cliente e o servidor de Caixa de Correio.

Com o Exchange 2013 Service Pack 1, reintroduzimos a função de servidor de Transporte de Borda. A função de Transporte de Borda geralmente é implantada em sua rede de perímetro, fora da floresta interna do Active Directory, e é projetada para minimizar a superfície de ataque de sua implantação do Exchange. Ao manipular todo o fluxo de email voltado para a Internet, a função também adiciona camadas adicionais de segurança e proteção de mensagens contra spam e vírus e pode aplicar regras de transporte para controlar o fluxo de mensagem. Para saber mais sobre a função de servidor de Transporte de Borda, confira [Servidores de Transporte de Borda](edge-transport-servers-exchange-2013-help.md).

A arquitetura do Exchange 2013 fornece os seguintes benefícios:

  - **Flexibilidade de atualização de versão** Não há mais requisitos de atualização rígidos. Um servidor de Acesso para Cliente pode ser atualizado de maneira independente e em qualquer ordem em relação ao servidor de Caixa de Correio.

  - **Indiferença de sessão**   Com o Exchange 2010, a afinidade de sessão para a função de servidor de Acesso para Cliente era solicitada para vários protocolos. No Exchange 2013, os componentes de acesso para cliente e caixa de correio residem no mesmo servidor de Caixa de Correio. Como o servidor de Acesso para Cliente simplesmente faz a intermediação de todas as conexões de um usuário com um servidor de Caixa de Correio específico, nenhuma afinidade de sessão é necessária nos servidores de Acesso para Cliente. Isso permite que conexões de entrada com servidores de Acesso para Cliente sejam balanceadas por meio do uso de técnicas fornecidas por tecnologia de balanceamento de carga, como menor conexão ou round robin.

  - **Simplicidade de implantação**   Com o design com resiliência de site do Exchange 2010, você precisava de até oito namespaces diferentes: dois namespaces IP, dois para fallback do Outlook Web App, um para Descoberta Automática, dois para Acesso para Cliente RPC e um para SMTP. Um namespace herdado também era necessário se você atualizasse do Exchange 2003 ou do Exchange 2007. Com o Exchange 2013, o número mínimo de namespaces cai para dois. Se estiver coexistindo com o Exchange 2007, você precisará ainda criar um nome de host herdado, mas se estiver coexistindo com o Exchange 2010 ou estiver instalando uma nova organização do Exchange 2013, o número mínimo de namespaces necessários será dois: um para protocolos de cliente e outro para Descoberta Automática. Você também pode precisar de um namespace SMTP.

Como resultado dessas alterações na arquitetura, houve algumas alterações na conectividade do cliente. Em primeiro lugar, RPC não é mais um protocolo de acesso direto com suporte. Isso significa que toda a conectividade do Outlook precisa ocorrer usando RPC por HTTP (também conhecido como Outlook em Qualquer Lugar). À primeira vista, isso pode parecer uma limitação, mas na verdade tem alguns benefícios adicionais. O benefício mais óbvio é que não é necessário ter o serviço de acesso para cliente RPC no servidor de Acesso para Cliente. Isso resulta na redução de dois namespaces que seriam normalmente necessários para uma solução com resiliência de site. Além disso, não há mais nenhuma necessidade de fornecer afinidade para o serviço de acesso para cliente RPC.

Segundo, os clientes do Outlook não se conectam mais ao FQDN de um servidor, como faziam em todas as versões anteriores do Exchange. O Outlook usa a Descoberta Automática para criar um novo ponto de conexão, composto pelo GUID da caixa de correio, pelo símbolo de @ e pela parte de domínio do endereço SMTP principal do usuário. Essa mudança simples resulta na eliminação quase total da mensagem indesejada "Seu administrador fez uma alteração em sua caixa de correio. Reinicie." Somente o Outlook 2007 e versões superiores são compatíveis com o Exchange 2013.

O modelo de alta disponibilidade do componente de caixa de correio não mudou significativamente desde o Exchange 2010. A unidade de alta disponibilidade ainda é o grupo de disponibilidade de banco de dados (DAG). O DAG ainda usa o cluster de failover do Windows Server. A replicação contínua ainda dá suporte à replicação em modo de arquivo e em modo de bloco. No entanto, houve algumas melhorias. Os tempos de failover foram reduzidos devido aos aprimoramentos no código do log de transações e ao ponto de verificação mais profundo nos bancos da dados passivos. O serviço de Repositório do Exchange foi reescrito em código gerenciado (consulte a seção "Repositório Gerenciado" mais adiante neste tópico). Agora, cada banco de dados é executado sob seu próprio processo, permitindo o isolamento de problemas de repositório em um único banco de dados.

## Repositório Gerenciado

No Exchange 2013, *Repositório Gerenciado* é o nome dos processos de Repositório de Informações reescritos recentemente, do Microsoft.Exchange.Store.Service.exe e do Microsoft.Exchange.Store.Worker.exe. O novo Repositório Gerenciado é escrito em C\# e é fortemente integrado com o serviço de Replicação do Microsoft Exchange (MSExchangeRepl.exe) para oferecer maior disponibilidade por meio do aprimoramento na resiliência. Além disso, o Repositório Gerenciado foi desenvolvido para permitir um gerenciamento mais granular do consumo de recursos e análise de causa principal mais rápida por meio de diagnóstico aprimorado.

O Armazenamento Gerenciado trabalha com o serviço Microsoft Exchange Replication para gerenciar bancos de dados da caixa de correio, que continua a usar o Mecanismo de Armazenamento Extensível (ESE) como o mecanismo de banco de dados. inclui alterações significativas no esquema de banco de dados da caixa de correio oferecendo muitas otimizações em relação às versões anteriores do Exchange. Além dessas mudanças, o serviço de Replicação do Microsoft Exchange é responsável por toda a disponibilidade de serviço relacionada aos servidores de Caixa de Correio. As mudanças de arquitetura permitem o failover mais rápido de banco de dados e melhor tratamento de falhas de disco físico.

O Repositório Gerenciado também é integrado ao mecanismo de pesquisa Search Foundation (o mesmo mecanismo de pesquisa usado pelo SharePoint 2013) para fornecer indexação e pesquisa mais robustas em comparação com o Microsoft Search em versões anteriores do Exchange.

Para obter mais informações, consulte [Alta disponibilidade e resiliência de site](high-availability-and-site-resilience-exchange-2013-help.md).

## Gerenciamento de certificados

O gerenciamento de certificados digitais é uma das tarefas relacionadas à segurança mais importantes para a sua organização do Exchange. Garantir que os certificados sejam apropriadamente configurados é essencial para fornecer uma infraestrutura de mensagens segura para a empresa. No Exchange 2010, o Console de Gerenciamento do Exchange era o principal método de gerenciamento de certificados. No Exchange 2013, a funcionalidade de gerenciamento de certificados é fornecida no centro de administração do Exchange, a nova interface do usuário de administrador do Exchange 2013.

O trabalho no Exchange 2013 relacionado aos certificados concentrava-se em minimizar o número de certificados que um Administrador devia gerenciar, minimizar a interação que o Administrador deve ter com certificados e permitindo o gerenciamento de certificados a partir de um local central. Os benefícios resultantes das alterações no gerenciamento de certificados são:

  - O gerenciamento de certificados pode ser feito no servidor de Acesso para Cliente ou no servidor de Caixa de Correio. O servidor de Caixa de Correio tem um certificado autoassinado instalado por padrão. O servidor de Acesso para Cliente confia automaticamente no certificado autoassinado no servidor de Caixa de Correio do Exchange 2013; portanto, os clientes não receberão avisos sobre um certificado autoassinado que não é confiável, contanto que o servidor de Acesso para Cliente do Exchange 2013 tenha um certificado que não seja autoassinado proveniente de uma autoridade de certificação (AC) do Windows ou de um terceiro confiável.

  - Em versões anteriores do Exchange, era difícil ver quando um certificado digital estava se aproximando da expiração. No Exchange 2013, o centro de notificações exibirá avisos quando um certificado armazenado em qualquer servidor do Exchange 2013 estiver prestes a expirar. Os administradores também podem optar por receber essas notificações via email.

Para obter mais informações, consulte [Certificados digitais e SSL](digital-certificates-and-ssl-exchange-2013-help.md).

## Instalação

O Programa de Instalação foi reescrito completamente, de modo a proporcionar mais facilidade na instalação do Exchange 2013, bem como dos pacotes cumulativos de atualizações e das correções de segurança do produto. Aqui estão algumas das melhorias que fizemos:

  - **Instalação sempre atualizada**   Ao executar o assistente de Instalação, você terá a opção de baixar e usar os pacotes cumulativos de atualizações, as correções de segurança e os pacotes de idiomas mais recentes do produto. Essa opção não atualiza apenas os arquivos que serão usados para executar o Exchange; o próprio Programa de Instalação pode ser atualizado. Este design nos permite continuar aprimorando o Programa de Instalação após o lançamento, incluindo e atualizando verificações de preparação conforme os requisitos são atualizados ou alterados.
    
    Se você estiver usando o modo de Instalação autônoma, não será possível baixar atualizações automaticamente. Entretanto, você ainda poderá aproveitar as vantagens de executar a versão mais recente do Programa de Instalação baixando as atualizações mais recentes antecipadamente e usar o parâmetro `/UpdatesDir: <path>` para permitir que o Programa de Instalação se atualize antes de o processo de instalação iniciar.

  - **Verificações de preparação aprimoradas**   As verificações de preparação garantem que seu computador e a organização estejam prontos para o Exchange 2013. Após o fornecimento das informações necessárias ao Programa de Instalação, as verificações de preparação são executadas antes do início da instalação. O novo mecanismo de verificação de preparação agora executa todas as verificações antes de informar a você quais ações precisam ser executadas para que a instalação possa continuar, e faz isso mais rápido do que nunca. Assim como nas versões anteriores do Exchange, você pode instruir a instalação a instalar os recursos do Windows exigidos por ela, para que não seja necessário instalá-los manualmente.

  - **Assistente simplificado e moderno**   Removemos todas as etapas do assistente de Instalação que não são absolutamente necessárias para que você instale o Exchange. O que restou é um assistente fácil de seguir que o orienta pelo processo de instalação uma etapa por vez.

Para mais informações, consulte [Planejamento e implantação](planning-and-deployment-for-exchange-2013-installation-instructions.md).

## Conformidade e política de sistema de mensagens

Existem dois novos recursos de conformidade e política de mensagem no Exchange 2013: Prevenção de perda de dados e o conector Microsoft Rights Management.

*Os recursos de Prevenção de perda de dados* (DLP) ajudam você a proteger os seus dados confidenciais e a informar aos usuários sobre as políticas de conformidade interna. A DLP também pode ajudar a manter a sua organização segura contra usuários que possam equivocadamente enviar informações confidenciais para pessoas não autorizadas. A DLP ajuda a identificar, monitorar e proteger dados confidenciais por meio de uma profunda análise de conteúdo. O Exchange 2013 oferece políticas de DLP integradas com base em padrões regulamentares, como informações de identificação pessoal e padrões de segurança de dados PCI (Payment Card Industry), contando com capacidade de extensão para suporte a outras políticas importantes para a sua empresa. Além disso, as novas Dicas de Política do Outlook 2013 informam os usuários sobre violações de política antes do envio de dados confidenciais.

O conector Microsoft Rights Management (RMS connector) é um aplicativo opcional que ajuda você a melhor a proteção dos dados do seu servidor Exchange 2013 conectando-se aos serviços do Microsoft Rights Management na nuvem. Ao instalar o conector RMS, ele oferece proteção contínua dos dados durante o tempo de vida das informações e como estes serviços são personalizáveis, você pode definir o nível de proteção de que você precisa. Por exemplo, você pode limitar o acesso a mensagem de email para usuários específicos ou definir direitos somente de leitura para certas mensagens.

Para saber mais sobre estes recursos consulte:

[Prevenção de perda de dados](technical-overview-of-dlp-data-loss-prevention-in-exchange.md)

[Conector Rights Management](https://go.microsoft.com/fwlink/p/?linkid=330432)

## Arquivamento In-loco, retenção e Descoberta Eletrônica

O Exchange 2013 inclui os seguintes aprimoramentos no Arquivamento In-loco, na retenção e na Descoberta Eletrônica para ajudar a sua organização a atender às suas necessidades de conformidade:

  - **Bloqueio In-loco**   Bloqueio In-loco é um novo modelo de bloqueio unificado que permite cumprir os requisitos de retenção legais nos seguintes cenários:
    
      - Preservar os resultados da consulta (bloqueio baseado em consulta), possibilitando imutabilidade com escopo em todas as caixas de correio.
    
      - Inserir um bloqueio baseado em tempo para atender aos requisitos de retenção (por exemplo, reter todos os itens de uma caixa de correio por sete anos, um cenário que exigia o uso de Recuperação de Item Único/Retenção de Item Excluído no Exchange 2010).
    
      - Colocar uma caixa de correio em bloqueio indefinido (similar à retenção de litígio no Exchange 2010).
    
      - Colocar um usuário em vários bloqueios para atender a diferentes requisitos de cada caso.

  - **Descoberta Eletrônica In-loco**   A Descoberta Eletrônica In-loco permite que usuários autorizados pesquisem dados de caixa de correio em todas as caixas de correio e todos os Arquivamentos In-loco em uma organização do Exchange 2013, além de copiar mensagens para uma caixa de correio de descoberta para análise. No Exchange 2013, a Descoberta Eletrônica In-loco foi aprimorada para permitir que os gerentes de descoberta realizem pesquisas e bloqueios mais eficientes. Esses aprimoramentos incluem:
    
      - A **pesquisa federada** permite pesquisar e preservar dados em vários repositórios de dados. Com o Exchange 2013, você pode realizar pesquisas de Descoberta Eletrônica In-loco no Exchange, no SharePoint 2013 e no Lync 2013. Você pode usar o Centro de Descoberta Eletrônica no SharePoint 2013 para realizar pesquisa de Descoberta Eletrônica In-loco e bloqueios.
    
      - **O Bloqueio In-loco baseado em consulta** permite que você salve os resultados da consulta, possibilitando imutabilidade com escopo em todas as caixas de correio.
    
      - **Exportar resultados da pesquisa** Os Gerentes de Descoberta podem exportar conteúdo de caixa de correio para um arquivo .pst a partir do Console de Descoberta Eletrônica do SharePoint 2013. Os cmdlets de solicitação de exportação de caixa de correio não são mais necessários para exportar uma caixa de correio para um arquivo .pst.
    
      - **Estatísticas de palavra-chave**   As estatísticas de pesquisa são oferecidas por termo de pesquisa. Isso permite que um Gerente de Descoberta tome decisões inteligentes rapidamente sobre como refinar ainda mais a consulta de pesquisa para fornecer resultados melhores. Os resultados da pesquisa de Descoberta Eletrônica são classificados por relevância.
    
      - **Sintaxe KQL**   Os Gerenciadores de Descoberta podem usar a sintaxe KQL (Keyword Query Language) em consultas de pesquisa. A KQL é similar à Sintaxe de Consulta Avançada (AQS) usada para pesquisas de descoberta no Exchange 2010.
    
      - **Assistente de Bloqueio e Descoberta Eletrônica In-loco**   Os Gerentes de Descoberta podem usar o novo assistente de Bloqueio e Descoberta Eletrônica In-loco para realizar operações de descoberta eletrônica e bloqueio.
        

        > [!TIP]
        > Se o SharePoint 2013 não estiver disponível, um subconjunto da funcionalidade de Descoberta Eletrônica estará disponível no centro de administração do Exchange.



  - **Pesquisar nas caixas de correio principais e de arquivo morto no Outlook Web App**   Os usuários podem pesquisar em suas caixas de correio principais e de arquivo morto no Outlook Web App. Não são mais necessárias duas pesquisas separadas.

  - **Arquivar o conteúdo do Lync**   O Exchange 2013 oferece suporte ao arquivamento do conteúdo do Lync 2013 na caixa de correio do usuário. Você pode bloquear o conteúdo do Lync usando o Bloqueio In-loco e usar a Descoberta Eletrônica In-loco para pesquisar o conteúdo do Lync arquivado no Exchange.

  - **Políticas de retenção**   As políticas de retenção ajudam a sua organização a reduzir os riscos associados a email e outras comunicações e também atendem aos requisitos de retenção de email. As políticas de retenção incluem os seguintes aprimoramentos:
    
      - **Suporte para marcas de retenção de Calendário e Tarefas**   Você pode criar marcas de política de retenção para as pastas Calendário e Tarefas padrão para expirar itens nessas pastas. Os itens nessas pastas também são movidos para o arquivo morto do usuário com base nas configurações da política de arquivamento aplicadas à caixa de correio.
    
      - **Capacidade aprimorada de reter itens por um período específico**   Você pode usar a política de retenção e um Bloqueio In-loco com base em tempo para impor a retenção de itens por um período definido.

Para mais informações, consulte [Conformidade e política de sistema de mensagens](messaging-policy-and-compliance-exchange-2013-help.md).

## Regras de transporte

As regras de transporte no Exchange Server 2013 são uma continuação dos recursos que estão disponíveis no Exchange Server 2010. No entanto, várias melhorias foram feitas nas regras de transporte do Exchange 2013. A mudança mais importante é o suporte para prevenção de perda de dados (DLP). Há também novos predicados e ações, monitoramento aprimorado e algumas alterações de arquitetura.

Para obter informações detalhadas, consulte [Novidades sobre regras de transporte](what-s-new-for-transport-rules-exchange-2013-help.md).

## Gerenciamento de Direitos de Informação

Gerenciamento de direitos de informação (IRM) é compatível com o modo criptográfico 2, um modo de criptografia do Active Directory Rights Management Services (AD RMS) que oferece suporte à criptografia forte, permitindo que você use teclas de 2048 bits RSA e teclas de 256 bits para SHA-1. Além disso, o modo 2 permite que você use o algoritmo de hash SHA-2. Para obter mais informações sobre modos criptográficos no AD RMS, consulte [Modos criptográficos do AD RMS](https://go.microsoft.com/fwlink/p/?linkid=263219).

## Auditoria

O Exchange 2013 inclui os seguintes aprimoramentos para auditoria:

  - **Relatórios de auditoria**   O EAC inclui a funcionalidade de auditoria para que você possa executar relatórios ou exportar entradas do log de auditoria de caixa de correio e o log de auditoria do administrador. O log de auditoria de caixa de correio registra sempre que uma caixa de correio é acessada por alguém diferente da pessoa que possui a caixa de correio. Isso pode ajudá-lo a determinar quem acessou a caixa de correio e o que a pessoa fez. O log de auditoria do administrador grava qualquer ação, com base em um cmdlet do Shell de Gerenciamento do Exchange, executada por um administrador. Isso pode ajudá-lo a solucionar problemas de configuração ou identificar a causa de problemas relacionados à segurança ou à conformidade. Para mais informações, consulte [Relatórios de auditoria do Exchange](exchange-auditing-reports-exchange-2013-help.md).

  - **Exibindo o log de auditoria do administrador**   Em vez de exportar o log de auditoria do administrador, cujo recebimento via mensagem de email pode demorar até 24 horas, você pode exibir as entradas de log de auditoria do administrador no EAC. Para isso, acesse **Gerenciamento de Conformidade** \> **Auditoria** e clique em **Exibir o log de auditoria do administrador**. Serão exibidas até 1.000 entradas em várias páginas. Para restringir a pesquisa, especifique um intervalo de datas. Para saber mais, veja [Exibir o log de auditoria do administrador](view-the-administrator-audit-log-exchange-2013-help.md).

## Proteção antimalware

Os recursos de filtragem de malware integrados do Exchange 2013 ajudam a proteger a sua rede contra software mal-intencionado transferido por mensagens de email. Todas as mensagens enviadas ou recebidas pelo seu servidor Exchange são verificadas para detecção de malware (vírus e spyware). Se algum malware for detectado, a mensagem será excluída. Notificações também podem ser enviadas a remetentes ou administradores quando uma mensagem infectada é excluída e não é entregue. Você também pode optar por substituir anexos infectados por mensagens padrão ou personalizadas que notificam os destinatários sobre a detecção de malware.

Para obter mais informações sobre proteção contra malware, consulte [Proteção antimalware](anti-malware-protection-exchange-2013-help.md).

## Fluxo de mensagens

O modo como as mensagens fluem por uma organização e o que ocorre com elas mudou bastante no Exchange 2013. A seguir, uma breve visão geral das mudanças:

  - **Pipeline de transporte**   O pipeline de transporte no Exchange 2013 é agora composto por vários serviços diferentes: serviço de Transporte de Front-End em servidores de Acesso para Cliente, serviço de Transporte em servidores de Caixa de Correio e serviço de Transporte de Caixa de Correio em servidores de Caixa de Correio. Para mais informações, consulte [Fluxo de mensagens](mail-flow-exchange-2013-help.md).

  - **Roteamento**   O roteamento de email no Exchange 2013 reconhece os limites de DAG e também os limites de site do Active Directory. Além disso, o roteamento de email foi aprimorado para colocar em fila as mensagens mais diretamente para destinatários internos. Para mais informações, consulte [Roteamento de mensagens](mail-routing-exchange-2013-help.md).

  - **Conectores**   O tamanho máximo padrão da mensagem para um conector de Envio ou um conector de Recebimento, conforme especificado pelo parâmetro *MaxMessageSize*, aumentou de 10 MB para 25 MB. Para obter mais informações sobre como definir parâmetros em um conector, consulte [Set-SendConnector](https://technet.microsoft.com/pt-br/library/aa998294\(v=exchg.150\)) e [Set-ReceiveConnector](https://technet.microsoft.com/pt-br/library/bb125140\(v=exchg.150\)).
    
    Você pode definir um conector de Envio no serviço de Transporte de um servidor de Caixa de Correio para rotear o email de saída através de um servidor de Transporte de Front End no site do Active Directory local, por meio do parâmetro *FrontEndProxyEnabled* do cmdlet **Set-SendConnector**, consolidando dessa forma a maneira como o email é roteado do serviço de Transporte.

  - **Transporte de Borda**   Opcionalmente, você pode instalar um servidor de Transporte de Borda na rede de perímetro para reduzir a superfície de ataque e fornecer segurança e proteção às mensagens. Para saber mais, confira [Servidores de Transporte de Borda](edge-transport-servers-exchange-2013-help.md).

## Destinatários

Esta seção descreve os aprimoramentos para o gerenciamento de destinatários no Exchange 2013:

  - **Política de nome de grupo**   Os administradores podem agora usar o EAC para criar uma *política de nome de grupo*, que permite padronizar e gerenciar os nomes de grupos de distribuição criados por usuários em sua organização. Você pode exigir que um prefixo e um sufixo específicos sejam adicionados ao nome de um grupo de distribuição quando ele for criado, bem como impedir que palavras específicas sejam usadas. Esse recurso ajuda a minimizar o uso de palavras inadequadas em nomes de grupos.
    
    Para mais informações, consulte [Criar um diretiva de nomeação de grupo de distribuição](create-a-distribution-group-naming-policy-exchange-2013-help.md).

  - **Controle de mensagens**   Os administradores podem também usar o EAC para acompanhar informações de entrega de mensagens de email enviadas ou recebidas por qualquer usuário na organização. É necessário apenas selecionar uma caixa de correio e procurar mensagens enviadas ou recebidas por um usuário diferente. É possível refinar a pesquisa procurando palavras específicas na linha de assunto. A notificação de entrega resultante acompanha a mensagem por todo o processo de entrega e especifica se ela foi entregue com êxito, se a entrega está pendente ou se não foi entregue.
    
    Para mais informações, consulte [Acompanhar mensagens com notificações de entrega](track-messages-with-delivery-reports-exchange-2013-help.md).

## Compartilhamento e colaboração

Esta seção descreve os aprimoramentos de compartilhamento e colaboração no Exchange 2013.

  - **Pastas públicas**   As pastas públicas agora aproveitam as vantagens das tecnologias existentes de alta disponibilidade e armazenamento do repositório de caixa de correio. A hierarquia de pasta pública usa caixas de correio designadas especialmente para armazenar o conteúdo da pasta pública e a hierarquia. Esse novo design também significa que não há mais um banco de dados de pasta pública. A replicação de pasta pública agora usa o modelo de replicação contínua. A alta disponibilidade da hierarquia e das caixas de correio de conteúdo é fornecida pelo grupo de disponibilidade de banco de dados (DAG). Com esse design, estamos mudando de um modelo de replicação multimestre para um modelo de replicação com um único mestre.
    
    Agora, os usuários do Outlook Web App da organização têm a capacidade de adicionar ou remover pastas públicas dos Favoritos. Anteriormente, isso só podia ser feito no Outlook.
    
    Para mais informações, consulte [Pastas públicas](public-folders-exchange-2013-help.md).

  - **Caixas de correio de site**   Emails e documentos são tradicionalmente mantidos em dois repositórios de dados exclusivos e separados. A maioria das equipes normalmente colabora usando os dois meios. O desafio é que emails e documentos são acessados com o uso de clientes diferentes, o que geralmente resulta em uma redução da produtividade do usuário e em uma degradação na experiência de uso.
    
    A *caixa de correio de site* é um conceito novo no Exchange 2013 que tenta resolver esses problemas. As caixas de correio de site melhoram a colaboração e a produtividade do usuário, permitindo acesso aos documentos em um site do SharePoint e a mensagens de email no Outlook 2013, usando a mesma interface de cliente. Uma caixa de correio de site é composta funcionalmente pela associação ao site do SharePoint (proprietários e membros), armazenamento compartilhado através de uma caixa de correio do Exchange para emails e um site do SharePoint para documentos, e uma interface de gerenciamento que lida com as necessidades de provisionamento e ciclo de vida.
    
    Para mais informações, consulte [Caixas de correio locais](site-mailboxes-exchange-2013-help.md).

  - **Caixas de correio compartilhadas**   Nas versões anteriores do Exchange, a criação de uma caixa de correio compartilhada era um processo em várias etapas que exigia o uso do Shell de Gerenciamento do Exchange para definir as permissões de representante. No Exchange 2013, agora você pode criar uma caixa de correio compartilhada em uma única etapa, usando o centro de administração do Exchange. No EAC, vá para **Destinatários** \> **Caixas de correio compartilhadas** para criar uma caixa de correio compartilhada. A caixa de correio compartilhada agora é um tipo de destinatário; portanto, você pode pesquisar facilmente suas caixas de correio compartilhadas na interface do usuário ou usando o Shell.
    
    Para mais informações, consulte [Caixas de correio compartilhadas](shared-mailboxes-exchange-2013-help.md).

## Integração com o SharePoint e o Lync

O Exchange 2013 oferece uma maior integração com o SharePoint 2013 e o Lync 2013. Os benefícios dessa integração aprimorada incluem:

  - O Exchange 2013 se integra ao SharePoint 2013 para permitir que os usuários colaborem de modo mais eficiente usando as caixas de correio de site.

  - O Lync Server 2013 pode arquivar conteúdo no Exchange 2013 e usar o Exchange 2013 como um repositório de contato.

  - Os Gerentes de Descoberta podem realizar pesquisas de Bloqueio e Descoberta Eletrônica In-loco nos dados do SharePoint 2013, do Exchange 2013 e do Lync 2013.

  - A autenticação OAuth permite que aplicativos de parceiros autentiquem como um serviço ou representem usuários onde necessário.

Para mais informações, consulte [Integração com o SharePoint e o Lync](integration-with-sharepoint-and-lync-exchange-2013-help.md).

## Clientes e dispositivos móveis

A interface do usuário do Outlook Web App é nova e otimizada para tablets e smartphones, bem como para desktops e notebooks. Os novos recursos incluem aplicativos para Outlook, que permitem que os usuários e os administradores ampliem os recursos do Outlook Web App; vinculação de contato, que é a capacidade dos usuários de adicionar contatos de suas contas do LinkedIn; e atualizações na aparência e nos recursos do calendário.

Para mais informações, consulte [Novidades do Outlook Web App no Exchange 2013](what-s-new-for-outlook-web-app-in-exchange-2013-exchange-2013-help.md).

## Unificação de Mensagens

A Unificação de Mensagens no Exchange 2013 contém essencialmente os mesmos recursos de caixa postal incluídos no Exchange 2010. Contudo, algumas funções e alguns recursos novos e aprimorados foram adicionados aos recursos existentes. O mais importante é que as mudanças de arquitetura na Unificação de Mensagens do Exchange 2013 resultaram na divisão de componentes, serviços e funções que estavam incluídos na função de servidor de Unificação de Mensagens no Exchange 2010 entre as funções de servidor de Acesso para Cliente e de Caixa de Correio do Exchange 2013.

Para mais detalhes, consulte [What's new para Unificação de mensagens no Exchange 2013](what-s-new-for-unified-messaging-in-exchange-2013-exchange-2013-help.md).

## Movimentações de caixa de correio em lote

O Exchange 2013 introduz o conceito de movimentações em lote. A nova arquitetura de movimentação é construída com base nas movimentações do serviço de Replicação de Caixa de Correio (MRS), com capacidade de gerenciamento aperfeiçoada. A nova arquitetura de movimentação em lote apresenta os seguintes aprimoramentos:

  - Capacidade de mover várias caixas de correio em grandes lotes.

  - Notificação por email durante movimentação com emissão de relatórios.

  - Repetição automática e priorização automática de movimentações.

  - Caixas de correio de arquivo morto principais e pessoais podem ser movidas juntas ou separadamente.

  - Opção de finalizar a solicitação de movimentação manual, permitindo que você revise a movimentação antes de concluí-la.

  - Sincronizações incrementais periódicas para migrar as alterações.

Para saber mais, confira [Gerenciar movimentações de local](manage-on-premises-moves-exchange-2013-help.md).

## Alta disponibilidade e resiliência de site

O Exchange 2013 usa DAGs e cópias de banco de dados de caixa de correio, além de outros recursos, como recuperação de itens únicos, políticas de retenção e cópias de banco de dados com atraso, para fornecer alta disponibilidade, resiliência de site e proteção de dados nativos do Exchange. A plataforma de alta disponibilidade, o Repositório de Informações do Exchange e o Mecanismo de Armazenamento Extensível (ESE) foram aprimorados para oferecer maior disponibilidade, gerenciamento mais fácil e reduzir custos. Esses aprimoramentos incluem:

  - **Disponibilidade gerenciada**   Com a disponibilidade gerenciada, o monitoramento interno e os recursos orientados à recuperação estão totalmente integrados para ajudar a impedir falhas, restaurar serviços proativamente e iniciar failovers de servidor automaticamente ou alertar administradores para tomarem uma providência. O foco está no monitoramento e no gerenciamento da experiência do usuário final em vez de apenas no servidor e no tempo de operação de componentes, para ajudar a manter o serviço continuamente disponível.

  - **Repositório Gerenciado**   Repositório Gerenciado é o nome dos processos de Repositório de Informações reescritos recentemente no Exchange 2013. O novo Repositório Gerenciado é escrito em C\# e possui alta integração com o serviço de Replicação do Microsoft Exchange (MSExchangeRepl.exe) para oferecer disponibilidade maior por meio de resiliência aprimorada.

  - **Suporte para vários bancos de dados por disco**   O Exchange 2013 inclui aprimoramentos que possibilitam o suporte para vários bancos de dados (combinações de cópias ativas e passivas) no mesmo disco, utilizando, assim, discos maiores em termos de capacidade e IOPS da forma mais eficiente possível.

  - **Nova propagação automática**   Permite que você restaure rapidamente a redundância de banco de dados após uma falha de disco. Se um disco falhar, a cópia de banco de dados armazenada nesse disco será copiada da cópia de banco de dados ativa para um disco reserva no mesmo servidor. Se várias cópias de banco de dados forem armazenadas no disco com falha, todas elas poderão ser automaticamente propagadas em um disco reserva. Isso permite propagações mais rápidas, visto que os bancos de dados ativos provavelmente estão em vários servidores, e os dados são copiados em paralelo.

  - **Recuperação automática de falhas de armazenamento**   Este recurso dá continuidade à inovação introduzida no Exchange 2010 para permitir que o sistema se recupere de falhas que afetam a resiliência ou a redundância. Além dos comportamentos de verificação de bugs do Exchange 2010, o Exchange 2013 inclui comportamentos de recuperação adicionais para tempos de E/S longos e consumo de memória excessivo pelo MSExchangeRepl.exe, bem como em casos graves em que o sistema esteja em um estado tão comprometido que threads não possam ser agendados.

  - **Aprimoramentos de cópias com retardamento**   As cópias com retardamento podem agora administrar a si próprias até um determinado limite, desprezando o log automaticamente. As cópias com retardamento desprezarão automaticamente os arquivos de log em uma variedade de situações, como cenários de restauração de uma única página e pouco espaço em disco. Se o sistema detectar que a correção de páginas é necessária para uma cópia com retardamento, os logs serão automaticamente reproduzidos na cópia com retardamento para a correção das páginas. As cópias com retardamento chamarão esse recurso de reprodução automática quando um limite de pouco espaço em disco for atingido e quando a cópia com retardamento tiver sido detectada como a única disponível para um período específico. Além disso, as cópias com retardamento podem utilizar a Rede de Segurança, tornando a recuperação ou a ativação mais fácil. *Rede Segura* é uma funcionalidade aprimorada no Exchange 2013 com base no dumpster de transporte do Exchange 2010.

  - **Aprimoramentos no alerta de cópia única**   O alerta de cópia única introduzido no Exchange 2010 não é mais um script agendado separado. Ele está agora integrado aos componentes de disponibilidade gerenciados no sistema e é uma função nativa no Exchange.

  - **Configuração automática da rede do DAG**   As redes dos DAGs podem ser automaticamente configuradas pelo sistema com base nas definições de configuração. Além das opções de configuração manual, os DAGs podem também fazer a distinção entre as redes MAPI e de replicação e configurar as redes do DAG automaticamente.

Para obter mais informações sobre esses recursos, consulte [Alta disponibilidade e resiliência de site](high-availability-and-site-resilience-exchange-2013-help.md) e [Alterações na alta disponibilidade e resilência de site em relação às versões anteriores](changes-to-high-availability-and-site-resilience-over-previous-versions-exchange-2013-help.md).

## Gerenciamento de carga de trabalho do Exchange

Uma carga de trabalho do Exchange é um recurso, protocolo ou serviço do servidor Exchange que foi explicitamente definido para as finalidades de gerenciamento de recursos do sistema do Exchange. Cada carga de trabalho do Exchange consome recursos do sistema, como CPU, operações de banco de dados de caixa de correio ou solicitações do Active Directory para executar solicitações do usuário ou trabalho em segundo plano. Os exemplos de cargas de trabalho do Exchange incluem Outlook Web App, Exchange ActiveSync, migração de caixa de correio e assistentes de caixa de correio.

Existem duas maneiras de gerenciar cargas de trabalho do Exchange no Exchange 2013:

  - **Monitorar a integridade dos recursos do sistema**    O gerenciamento de cargas de trabalho com base na integridade dos recursos de sistema é novo no Exchange 2013.

  - **Controlar como os recursos são consumidos por usuários individuais**   O controle de como os recursos são consumidos por usuários individuais era possível no Exchange 2010 (no qual é chamado de limitação de usuário), e esse recurso foi expandido para o Exchange 2013.

Para obter mais informações sobre esses recursos, consulte [Gerenciamento de carga de trabalho do Exchange](exchange-workload-management-exchange-2013-help.md).

