---
title: "What's new para Unificação de mensagens no Exchange 2013: Exchange 2013 Help"
TOCTitle: What's new para Unificação de mensagens no Exchange 2013
ms:assetid: a444ef2d-d893-408e-adf9-c9d8a8b07593
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/JJ150545(v=EXCHG.150)
ms:contentKeyID: 50486312
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# What's new para Unificação de mensagens no Exchange 2013

 

_**Aplica-se a:**Exchange Server 2013_

_**Tópico modificado em:**2016-12-09_

No Microsoft Exchange Server 2013, estamos estiver aprimorando a versões anteriores do Exchange apresentando os novos recursos e mudanças de arquitetura. Unified Messaging (UM) em Exchange 2013 inclui o mesmo recurso definido como Exchange 2010 e Exchange 2007, no entanto, Unificação de mensagens não mais é uma função de servidor separadas. Agora é um componente dos recursos relacionadas à voz oferecidas em Exchange 2013.

## Alterações na arquitetura de voz

A arquitetura de Exchange 2013 é diferente do que era em Exchange 2010 e Exchange 2007. Nas versões anteriores de UM do Exchange, todos os componentes para Unificação de mensagens foram incluídos em um servidor que tinha a função de servidor de Unificação de MENSAGENS instalada. Em Exchange 2013, todos os componentes de Unificação de mensagens são divididos entre um servidor de acesso para cliente que executa o serviço Microsoft Exchange Unified Messaging roteador de chamada e um servidor de caixa de correio executando o serviço de Unificação de mensagens do Microsoft Exchange. Toda a funcionalidade, incluindo os serviços e os processos de trabalho para Unificação de mensagens, está localizada em cada servidor de caixa de correio, com exceção do servidor de acesso para cliente que executa o serviço Microsoft Exchange Unified Messaging roteador de chamadas, chamadas de entrada que proxies para o servidor de caixa de correio. Para obter detalhes, consulte [Mudanças de arquitetura de voz](voice-architecture-changes-exchange-2013-help.md).

## Suporte a IPv6

Protocolo IP versão 6 (IPv6) é a versão mais recente do protocolo da Internet. IPv6 destina-se a corrigir muitas das deficiências IPv4, qual foi a versão anterior do IP. Como Exchange 2010, servidores de acesso para cliente e caixa de correio de Exchange 2013 totalmente oferecem suporte a redes IPv6. Para obter informações detalhadas, consulte [Suporte a IPv6 na Unificação de mensagens](ipv6-support-in-unified-messaging-exchange-2013-help.md).

## Suporte para API 4.0 UCMA

Desde o Service Pack 1 para Exchange 2010, a função Unificação de mensagens tem se baseavam em v 2.0 Unified Communications Managed API (UCMA) para a sinalização e mídia. Portanto, o UCMA 2.0 é um pré-requisito para a instalação UM Exchange 2010. UCMA 2.0 é baixado separadamente e implantados manualmente pelos administradores nos servidores de Unificação de mensagens executando Exchange 2010 SP1 ou versão posterior. Para Exchange 2013, UCMA 4.0 é necessário. No entanto, considerando que o servidor de Unificação de MENSAGENS não mais é uma função de servidor separadas no Exchange 2013, agora é os servidores de acesso para cliente e caixa de correio que exigem o UCMA 4.0.

UCMA 4.0 oferece suporte a novos recursos na Unificação de mensagens, como usando a mesma versão do mecanismo de fala para texto em fala (TTS) e o reconhecimento automático de fala (ASR). A plataforma que é usada para Exchange 2013, .NET 4.0, inclui um arquivo único instalador e permite manter a compatibilidade com os servidores de Unificação de MENSAGENS Exchange 2010 e Exchange 2007.

No Exchange 2010 SP2 e SP1, UCMA 2.0 instalação é necessária antes de instalar o service pack em um servidor de Unificação de mensagens. No entanto, o UCMA 2.0 tinham várias limitações. UCMA 4.0 corrige muitas das deficiências. Em Exchange Server 2013, a Unificação de MENSAGENS continua a usar o UCMA. No entanto, a mudança para a versão mais recente do UCMA oferece estes benefícios:

  - A compilação mais recente do UCMA incorpora patches e hotfixes.

  - UCMA requer o .NET 4.0, qual é a plataforma de usado pelo Exchange Server 2013. (UCMA 2.0 não tem suporte para .NET 4.0.)

  - UCMA 4.0 oferece suporte a IPv6.

  - Implantação simplificada e automatizada do UCMA 4.0. Exchange 2013 Instalação realiza uma verificação única do UCMA 4.0.

  - Instalação do UCMA 4.0 inclui todos os pré-requisitos para Exchange 2013.


> [!TIP]
> UCMA 4.0 é instalado quando você está instalando Exchange 2013. Para obter detalhes sobre os requisitos de instalação e 4.0 UCMA, consulte <A href="exchange-2013-prerequisites-exchange-2013-help.md">Pré-requisitos do Exchange 2013</A>. Para atualizar para a versão mais recente do UCMA, desinstale qualquer versão anterior do UCMA instaladas usando Adicionar ou remover programas.



## Aprimoramentos para visualização da caixa postal

Alguns aprimoramentos aos serviços relacionados a fala são oferecidos para Exchange Server 2013 Unificação de MENSAGENS por meio do 11.0 do mecanismo de fala e UCMA 4.0. Aprimoramentos de idioma e de geração de gramática são incluídos. Além disso, Exchange Server 2013 Unificação de MENSAGENS inclui vários aprimoramentos na interface do usuário e melhorias para a confiança e a precisão para visualização da caixa postal. Para obter detalhes, consulte [Melhorias da caixa postal preview](voice-mail-preview-enhancements-exchange-2013-help.md).

## Suporte de ID de chamador avançada

Nas versões anteriores do Exchange Unified Messaging, um servidor de Unificação de MENSAGENS que recebeu uma chamada usado o ID do chamador para tentar procurar a identidade do chamador. Esta pesquisa estendido do Active Directory e contatos pessoais de Unificação de MENSAGENS do usuário armazenados em suas caixas de correio.

Os usuários do Exchange com frequência se incomodar com falhas para identificar Exchange ou os contatos pessoais de sua ID de chamador. Até agora, apenas a pasta de contato padrão em UM do Exchange foi usada para esta pesquisa. Mas Exchange Server 2013 usuários provavelmente terá contatos agregados de redes sociais externas ou contatos em pastas exclusivos que os usuários criados manualmente. Exchange 2013 oferece suporte à agregação de contatos de redes sociais externas, fornece inteligência para vincular a vários contatos fazendo referência à mesma pessoa e usa esses dados para apresentar os modos de exibição centrados em pessoa (ao invés centrados em contato). Os contatos que estão agregados de redes externas são colocados em pastas de contatos junto com quaisquer pastas de contato adicionais que os usuários criados. Os recursos no Exchange 2013 UM estendem o escopo da pesquisa para incluir do usuário outro Exchange e pastas de contatos pessoais que foram criadas manualmente.

Pesquisa de ID de chamador é integrada com agregação de contato, para que ele pesquisará os entre contatos externos. A propriedade o PersonID, onde presente e com um valor não-nulo, melhora a experiência do usuário para resolução de ID do chamador, suprimindo duplicadas corresponde aos contatos que estão associados a mesma pessoa. Como a propriedade o PersonID é o mesmo em ambos os resultados, UM o trata como uma correspondência para um único contato.

## Aprimoramentos para a plataforma de fala e reconhecimento de fala

Exchange Server 2013 Unificação de MENSAGENS introduz algumas melhorias para a plataforma de fala e reconhecimento de fala, incluindo o seguinte:

  - As melhorias e precisão aprimorado para visualização da caixa postal.

  - Suporte para a [plataforma do Microsoft Speech – Runtime (versão 11.0)](https://go.microsoft.com/fwlink/p/?linkid=253196).

  - Geração de gramática de fala usando a caixa de correio do sistema para uma organização.

Unificação de mensagens do Exchange usa o gramáticas fala estáticas e dinâmicas para reconhecer comandos, nomes dos contatos na lista de endereços global e nomes de contatos pessoais na caixa de correio do usuário. Hoje, em Exchange Server 2013, cada servidor de caixa de correio executando o serviço de Unificação de mensagens do Microsoft Exchange gera gramáticas para todos os idiomas de Unificação de MENSAGENS instaladas nele e armazenando-as em diretórios. Cada servidor de caixa de correio armazena cada gramática possível, qual ele gera com base no número de planos de discagem, atendedores automáticos e os idiomas de Unificação de MENSAGENS que estão instalados.

Arquivos de gramática são usados como entradas para o processo de reconhecimento de fala e são gerados periodicamente. O comando GGG.exe Exchange 2007 e Exchange 2010 permitido atualizar manualmente os arquivos de gramática sem esperar que a atualização agendada. Em Exchange Server 2013, para resolver problemas de escalabilidade de geração de gramática ASR para Unificação de MENSAGENS, a GAL gramática de fala geração não são mais acontece no servidor com a função de servidor Unificação de mensagens está instalada. Em vez disso, ele acontece periodicamente usando o Assistente de caixa de correio, no servidor de caixa de correio executando o serviço de Unificação de mensagens do Microsoft Exchange que hospeda as caixas de correio de arbitragem da organização. O arquivo de gramática de fala GAL é armazenado na caixa de correio de arbitragem para uma organização e posteriormente baixado para todos os servidores de caixa de correio na organização do Exchange que. Por padrão, o Assistente de caixa de correio é executado a cada 24 horas. Você pode ajustar a frequência usando o cmdlet **Set-MailboxServer** .

## Atualizações do cmdlet

Para Exchange 2013, vários cmdlets de Unificação de MENSAGENS foi trazidos de Exchange 2010, mas houve alterações em alguns desses cmdlets e novos cmdlets foram adicionados para a nova funcionalidade. Para obter detalhes, consulte [Atualizações de cmdlet do Unified Messaging](unified-messaging-cmdlet-updates-exchange-2013-help.md).

