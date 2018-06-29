---
title: 'Novos recursos de caixa postal: Exchange 2013 Help'
TOCTitle: Novos recursos de caixa postal
ms:assetid: 89faaa97-3485-4704-a56c-d13632f01e2a
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/JJ649002(v=EXCHG.150)
ms:contentKeyID: 50486110
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Novos recursos de caixa postal

 

_**Aplica-se a:**Exchange Server 2013, Exchange Server 2016_

_**Tópico modificado em:**2016-12-09_

Unificação de mensagens (UM) no Microsoft Exchange Server 2013 inclui o mesmo conjunto como Exchange 2010 e Exchange 2007, com algumas melhorias e mudanças de arquitetura de recursos. No entanto, Unificação de mensagens não mais é uma função de servidor separado. Agora é um componente dos recursos relacionadas à voz oferecidas em Exchange 2013.

## Alterações na arquitetura de voz

Arquitetura de voz em Exchange 2013 é diferente do que era em Exchange 2010 e Exchange 2007. Nas versões anteriores de UM do Exchange, todos os componentes para Unificação de mensagens foram incluídos em um servidor que tinha a função de servidor de Unificação de MENSAGENS instalada. Em Exchange 2013, os componentes de Unificação de mensagens são divididos entre um servidor de acesso para cliente que executa o serviço Microsoft Exchange Unified Messaging roteador de chamada e um servidor de caixa de correio executando o serviço de Unificação de mensagens do Microsoft Exchange. Maioria das funcionalidades, incluindo os serviços e os processos de trabalho para Unificação de mensagens, está localizado em cada servidor de caixa de correio. O servidor de acesso para cliente, executando o Microsoft Exchange Unified Messaging serviço roteador de chamadas, chamadas de entrada de proxies para o servidor de caixa de correio. Para obter detalhes, consulte [Mudanças de arquitetura de voz](voice-architecture-changes-exchange-2013-help.md).

## Suporte a IPv6

Protocolo IP versão 6 (IPv6) é a versão mais recente do protocolo da Internet (IP). IPv6 destina-se a corrigir muitas das deficiências IPv4, qual foi a versão anterior do IP. Assim como Exchange 2010 fez, servidores de acesso para cliente e caixa de correio Exchange 2013 mais suportam total redes IPv6. Para obter informações detalhadas, consulte [Suporte a IPv6 na Unificação de mensagens](ipv6-support-in-unified-messaging-exchange-2013-help.md).

## Suporte para API 4.0 UCMA

Desde o Exchange 2010 Service Pack 1 (SP1), a função Unificação de mensagens tem se baseavam em v 2.0 Unified Communications Managed API (UCMA) para a sinalização e mídia. Portanto, o UCMA 2.0 era um pré-requisito para a instalação UM Exchange 2010. UCMA 2.0 é baixado separadamente e implantados manualmente pelos administradores nos servidores de UM executando Exchange 2010 SP1 ou versão posterior.

No entanto, UCMA 2.0 tem várias limitações. Muitos dessas deficiências são corrigidos por UCMA 4.0, que é necessária para Exchange 2013. Agora que o servidor de Unificação de MENSAGENS não mais é uma função de servidor separado, é os servidores de acesso para cliente e caixa de correio que exigem o UCMA 4.0.

UCMA 4.0 oferece suporte a novos recursos na Unificação de mensagens, como usando a mesma versão do mecanismo de fala para texto em fala (TTS) e o reconhecimento automático de fala (ASR). A plataforma que é usada para Exchange 2013, .NET 4.0, inclui um arquivo único instalador e permite manter a compatibilidade com os servidores de Unificação de MENSAGENS Exchange 2010 e Exchange 2007.

No Exchange 2010 SP2 e SP1, UCMA 2.0 instalação é necessária antes de instalar o service pack em um servidor de Unificação de mensagens.

Usando o UCMA 4.0 oferece vários benefícios:

  - Ele incorpora patches e hotfixes.

  - Suporte a IPv6.

  - Implantação do UCMA 4.0 foi automatizada e simplificada.

  - Instalação do UCMA 4.0 inclui todos os pré-requisitos para Exchange 2013.

  - UCMA 4.0 fornece mais precisas traduções de mecanismo de fala e suporte de plataforma de voz mais escalonável em vários produtos.


> [!TIP]
> UCMA 4.0 é instalado quando você está instalando Exchange 2013. Para obter detalhes sobre os requisitos de instalação e 4.0 UCMA, consulte <A href="exchange-2013-prerequisites-exchange-2013-help.md">Pré-requisitos do Exchange 2013</A>. Para atualizar para a versão mais recente do UCMA, desinstale qualquer versão anterior do UCMA instaladas usando Adicionar ou remover programas.



## Aprimoramentos para visualização da caixa postal

Alguns aprimoramentos aos serviços de fala são incluídos em Exchange Server 2013 Unificação de MENSAGENS por meio do 11.0 do mecanismo de fala e UCMA 4.0. Houve aprimoramentos no suporte para vários idiomas, principais serviços de voz e geração de gramática. Exchange Server 2013 UM também inclui vários aprimoramentos para serviços de transcrição que são entregues aos usuários finais e aumento da confiança e a precisão para visualização da caixa postal. Para obter informações detalhadas, consulte [Melhorias da caixa postal preview](voice-mail-preview-enhancements-exchange-2013-help.md).

## Suporte de ID de chamador avançada

Nas versões anteriores do Exchange Unified Messaging, um servidor de Unificação de MENSAGENS que recebeu uma chamada usado o ID de chamador para pesquisar a identidade possível da parte chamada. Esta pesquisa estendida por Active Directory e contatos pessoais de Unificação de MENSAGENS do usuário armazenados em suas caixas de correio.

No passado, os usuários às vezes foram frustrados por causa de falha do sistema de correio de voz para identificar o Exchange ou os contatos pessoais de sua ID do chamador. Até agora, somente a pasta de contato padrão na caixa de correio do Exchange do usuário foi usada para a pesquisa. Mas Exchange Server 2013 usuários provavelmente terá contatos agregados de redes sociais externas ou contatos que eles adicionados às pastas exclusivas ao organizar seus contatos. No Exchange 2013, UM estende o escopo da pesquisa para incluir o usuário do outro Exchange e pastas de contatos pessoais que foram criadas manualmente. Exchange 2013 também oferece suporte à agregação de contatos de redes sociais externas, fornece inteligência para vincular a vários contatos que se referem a mesma pessoa e usa esses dados para apresentar os modos de exibição centrados em pessoa (ao invés centrados em contato). Isso significa que os contatos que estão agregados de redes sociais externas podem ser colocados na pasta contato armazenados na caixa de correio do usuário no Microsoft Outlook Web App e Outlook. Esses contatos agora também podem ser adicionados para as pastas de contato adicionais que os usuários criam.

Pesquisa de ID de chamador é integrada com agregação de contato, para que ele pesquisará os entre contatos externos. A propriedade **PersonID** , onde apresentar e definida como um valor que não seja Null, melhora a experiência do usuário para resolução de identificação do chamador com suprimindo correspondências duplicadas para contatos que estão associados a mesma pessoa. Como a propriedade o PersonID é o mesmo em ambos os resultados, UM o trata como uma correspondência para um único contato.

## Aprimoramentos para a plataforma de fala e reconhecimento de fala

Exchange Server 2013 Unificação de MENSAGENS introduz algumas melhorias para a plataforma de fala e reconhecimento de fala, incluindo o seguinte:

  - As melhorias e precisão aprimorado para visualização da caixa postal.

  - Suporte para a [plataforma do Microsoft Speech – Runtime (versão 11.0)](https://go.microsoft.com/fwlink/p/?linkid=253196).

  - Geração de gramática de fala usando a caixa de correio do sistema para uma organização.

Unificação de mensagens do Exchange usa gramáticas fala estáticas e dinâmicas para reconhecer comandos, nomes dos contatos da lista de endereços global (GAL) e nomes de contatos pessoais em caixa de correio do usuário. Hoje, em Exchange Server 2013, cada servidor de caixa de correio executando o serviço de Unificação de mensagens do Microsoft Exchange gera gramáticas para todos os idiomas de Unificação de MENSAGENS instaladas nele e armazenando-as em diretórios. Cada servidor de caixa de correio armazena cada gramática possível, qual ele gera com base no número de planos de discagem, atendedores automáticos e os idiomas de Unificação de MENSAGENS que estão instalados.

Arquivos de gramática são usados pela Unificação de MENSAGENS para permitir que os chamadores usar a fala para localizar usuários em sua organização. Os arquivos são atualizados a cada 24 horas pelo Assistente de caixa de correio. O comando GGG.exe Exchange 2007 e Exchange 2010 possibilitada atualizar manualmente os arquivos de gramática sem esperar que a atualização agendada. Em Exchange Server 2013, escalabilidade de geração de gramática ASR de lidar com problemas para Unificação de MENSAGENS, a fala a geração de gramática da GAL não são mais acontece no servidor com a função de servidor Unificação de mensagens está instalada. Em vez disso, ele acontece periodicamente usando o Assistente de caixa de correio, no servidor de caixa de correio executando o serviço de Unificação de mensagens do Microsoft Exchange que hospeda as caixas de correio de arbitragem da organização. O arquivo de gramática de fala GAL é armazenado na caixa de correio de arbitragem para uma organização e posteriormente baixado para todos os servidores de caixa de correio na organização do Exchange. Por padrão, o Assistente de caixa de correio é executado a cada 24 horas. Você pode ajustar a frequência usando o cmdlet **Set-MailboxServer** .

## Atualizações do cmdlet

Para Exchange 2013, vários cmdlets de Unificação de MENSAGENS serem levados de Exchange 2010. No entanto, houve alterações em alguns desses cmdlets e novos cmdlets foram adicionados para a nova funcionalidade. Para obter informações detalhadas, consulte [Atualizações de cmdlet do Unified Messaging](unified-messaging-cmdlet-updates-exchange-2013-help.md).

