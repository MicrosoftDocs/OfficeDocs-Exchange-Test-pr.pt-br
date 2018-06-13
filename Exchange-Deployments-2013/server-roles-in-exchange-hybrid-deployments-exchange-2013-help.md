---
title: 'Funções de servidor em implantações híbridas do Exchange: Exchange 2013 Help'
TOCTitle: Funções de servidor em implantações híbridas do Exchange
ms:assetid: 7a7eaf17-d2b0-4d62-90a2-45a0d2faca54
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/JJ659051(v=EXCHG.150)
ms:contentKeyID: 50487113
ms.date: 01/10/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Funções de servidor em implantações híbridas do Exchange

 

_**Aplica-se a:**Exchange Server 2013, Exchange Server 2016_

_**Tópico modificado em:**2016-12-09_

Você pode configurar as implantações híbridas com base no Exchange 2013 e no Exchange 2016. As funções que precisam ser configuradas para oferecer suporte a uma implantação híbrida dependem da versão do Exchange que você está usando.

## Implantação híbrida do Exchange 2016

Ao configurar uma implantação híbrida em uma organização do Exchange 2016, não é necessário instalar servidores do Exchange adicionais em sua organização do Exchange existente. Os seus servidores de Caixa de Correio coordenam as comunicações entre sua organização do Exchange 2016 existente e a organização do Exchange Online. Essa comunicação inclui o transporte de mensagens e os recursos de mensagens entre a organização local e a organização do Exchange Online. É altamente recomendada a instalação de mais de um servidor do Exchange em sua organização no local para ajudar a aumentar a confiabilidade e a disponibilidade dos recursos de implantação híbrida.

O Exchange 2016 tem apenas uma função de servidor necessária, a função de Caixa de Correio. Além de hospedar as caixas de correio locais do destinatário, a função de Caixa de Correio executa todas as funções necessárias para oferecer suporte a uma implantação híbrida com o Exchange Online. Isso inclui gerenciar mensagens de email seguras entre as organizações locais e do Exchange Online, bem como regras de transporte, políticas de registro no diário e entregas de mensagem para caixas de correio do usuário em uma implantação híbrida. Todos os recursos de relação da organização e conectividade do cliente, como o compartilhamento de disponibilidade, também são gerenciados pelo servidor da Caixa de Correio.

Saiba mais sobre o planejamento de capacidade do Exchange 2016 em [Dimensionamento de implantações do Exchange 2016](http://go.microsoft.com/fwlink/p/?linkid=301990).

## Implantação híbrida do Exchange 2013

Ao configurar uma implantação híbrida em uma organização do Exchange 2013, não é necessário instalar servidores do Exchange adicionais em sua organização do Exchange existente. Seus servidores de Acesso para Cliente e de Caixa de Correio coordenam as comunicações entre sua organização do Exchange 2013 existente e a organização do Exchange Online. Essa comunicação inclui o transporte de mensagens e os recursos de mensagens entre a organização local e a organização do Exchange Online. É altamente recomendada a instalação de mais de um servidor do Exchange em sua organização no local para ajudar a aumentar a confiabilidade e a disponibilidade dos recursos de implantação híbrida.

Eis uma rápida visão geral das funções de servidor do Exchange 2013 em uma implantação híbrida:

  - **Função de servidor acesso para cliente**   A função de servidor de Acesso para Cliente continua a fornecer basicamente a mesma funcionalidade fornecida por servidores de Acesso para Cliente na organização do Exchange 2013 com poucas adições necessárias para suportar a implantação híbrida. O servidor de Acesso para Cliente também gerencia todas as mensagens de email seguras enviadas entre as organizações locais e do Exchange Online, bem como regras de transporte, políticas de registro no diário e entregas de mensagem para caixas de correio do usuário em uma implantação híbrida. Por padrão, um conector dedicado de Recepção é configurado no servidor de Acesso para Cliente para suportar transporte seguro de email híbrido. Toda a conectividade do cliente, incluindo o acesso para cliente do Outlook, o Outlook Web App e o Outlook em Qualquer Lugar, passa pela função de servidor Acesso para Cliente. Os recursos de relacionamento da organização entre as organizações locais e as organizações do Exchange Online, como compartilhamento de disponibilidade, também são tratados pela função de servidor de Acesso para Cliente.
    
    Saiba mais em [Servidor de Acesso para Cliente](https://technet.microsoft.com/pt-br/library/dd298114\(v=exchg.150\)).

  - **Função servidor de Caixa de Correio**   A função servidor de Caixa de Correio hospeda as caixas de correio de destinatário locais e se comunica com a organização do Exchange Online por proxy por meio do servidor de Acesso para Cliente local. Por padrão, um conector dedicado de Envio é configurado no servidor de Acesso para Cliente para suportar transporte seguro de email híbrido.
    
    Saiba mais em [Servidor de Caixa de Correio](https://technet.microsoft.com/pt-br/library/jj150491\(v=exchg.150\)).

Dependendo da configuração de implantação híbrida que deseja, um servidor do Exchange 2013 exige uma ou ambas as funções de servidor para serem instaladas nele:

  - **Servidor do Exchange único**   Se você escolher instalar um único servidor do Exchange em sua organização local, você precisará instalar as funções de servidor de Acesso para Cliente e de Caixa de Correio no servidor único.

  - **Mais de um servidor do Exchange**   Se você escolher instalar mais de um servidor do Exchange em sua organização local, você pode instalar as funções de servidor em servidores separados em sua organização local. Por exemplo, você pode instalar um servidor do Exchange que possui as funções de Caixa de Correio e de Acesso para Cliente instaladas e também instalar outro servidor do Exchange que possui apenas a função de servidor de Acesso para Cliente instalada. No entanto, a prática recomendada e a configuração de servidor recomendada é instalar os servidores de Acesso para Cliente e de Caixa d Correio em *cada* servidor implantado em sua organização local.

Saiba mais sobre o planejamento de capacidade do Exchange 2013 em [Noções Básicas Sobre Várias Configurações de Função de Servidor no Planejamento da Capacidade](http://go.microsoft.com/fwlink/?linkid=266576).

## Funcionalidade do Exchange Server em implantações híbridas

Servidores Exchange oferecem várias funções importantes para a sua organização local em uma implantação híbrida:

  - **Federação**   Os servidores do Exchange permitem criar uma confiança de federação para sua organização local com o Microsoft Federation Gateway. O Microsoft Federation Gateway é um serviço gratuito baseado na nuvem oferecido pela Microsoft, atuando como agente de confiança entre a organização local e a organização do Office 365. A federação é requisito para a criação de um relacionamento de organização entre a organização local e a organização do Exchange Online.
    
    Saiba mais em [Federação](https://technet.microsoft.com/pt-br/library/dd335047\(v=exchg.150\)).

  - **Relacionamentos de organização**   Servidores do Exchange 2013 com a função de Acesso para Cliente e servidores do Exchange 2016 com a função de Caixa de Correio permitem a criação das relações da organização entre as organizações local e do Exchange Online. As relações da organização são necessários para muitos outros serviços em uma implantação híbrida, incluindo compartilhamento de informações de disponibilidade de calendário, acompanhamento de mensagens e movimentações de caixa de correio entre a organização local e a organização do Exchange Online.
    
    Saiba mais em [Compartilhamento](https://technet.microsoft.com/pt-br/library/dd638083\(v=exchg.150\)).

  - **Transporte de mensagem**   Servidores do Exchange com funções de servidor de Acesso para Cliente e Caixa de Correio são responsáveis pelo transporte de mensagens em uma implantação híbrida. Usando conectores de Envio e Recebimento, eles servem como ponto de extremidade de conexão para mensagens externas de entrada e também oferecem a entrega de mensagens de saída para a Internet e a organização do Exchange Online.
    
    Saiba mais em [Opções de transporte em implantações híbridas do Exchange](transport-options-in-exchange-hybrid-deployments-exchange-2013-help.md).

  - **Segurança de transporte de mensagens**   Servidores do Exchange com a função de servidor de Acesso para Cliente e de Caixa de Correio ajudam a proteger a comunicação de mensagens entre a organização local e a organização do Exchange Online usando a funcionalidade de Segurança de Domínio no Exchange. A segurança pode ser aumentada usando autenticação de segurança de camada de transporte mútua e criptografia para comunicações de mensagens.
    
    Saiba mais em [Noções básicas sobre segurança de domínio](http://go.microsoft.com/fwlink/p/?linkid=266581).

  - **Outlook na Web (conhecido como Outlook Web App no Exchange 2013)**   Servidores do Exchange 2013 com a função de Acesso para Cliente e servidores do Exchange 2016 com a função de Caixa de Correio dão suporte à configuração de um único ponto de extremidade de URL para conexões externas para caixas de correio local e do Exchange Online. Para caixas de correio locais, os servidores de Exchange são configurados para solicitações do Outlook na Web de serviço. Para caixas de correio da organização do Exchange Online, os servidores de Exchange são configurados para exibir automaticamente um link para o ponto de extremidade do Outlook na Web na organização do Exchange Online.
    
    Saiba mais em [Outlook Web App](https://technet.microsoft.com/pt-br/library/jj657718\(v=exchg.150\)).

