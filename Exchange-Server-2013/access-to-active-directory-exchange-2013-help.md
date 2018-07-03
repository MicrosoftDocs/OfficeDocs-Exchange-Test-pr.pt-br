---
title: 'Acesso ao Active Directory: Exchange 2013 Help'
TOCTitle: Acesso ao Active Directory
ms:assetid: 61080b45-8bce-4c23-b744-ed264d5f0b7d
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Aa998561(v=EXCHG.150)
ms:contentKeyID: 50485718
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Acesso ao Active Directory

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2016-12-09_

O Microsoft Exchange Server 2013 armazena todas as informações de destinatários e configurações no banco de dados de serviço de diretório do Active Directory. Quando um computador que está executando o Exchange 2013 precisa de informações sobre destinatários e sobre a configuração da organização do Exchange, ele deve consultar o Active Directory para acessar as informações. Os servidores do Active Directory devem estar disponíveis para que o Exchange 2013 funcione corretamente.

Este tópico explica como o Exchange 2013 armazena e recupera informações no Active Directory para que você possa planejar o acesso ao Active Directory. Este tópico também discute os problemas de que você deve estar ciente caso tente recuperar objetos excluídos do Exchange 2013 Active Directory.

## Informações do Exchange armazenadas no Active Directory

O banco de dados do Active Directory armazena informações em três tipos de partições lógicas descritas nas seguintes seções:

  - Partição de esquema

  - Partição de configuração

  - Partição de domínio

## Partição de esquema

A partição de esquema armazena os dois tipos de informações a seguir:

  - As **classes de esquema** definem todos os tipos de objetos que podem ser criados e armazenados no Active Directory.

  - Os **atributos de esquema** definem todas as propriedades que podem ser usadas para descrever os objetos armazenados no Active Directory.

Quando você instala a primeira função de servidor do Exchange 2013 na floresta ou executa o processo de preparação do Active Directory, o processo de preparação do Active Directory adiciona muitas classes e atributos ao esquema do Active Directory. As classes adicionadas ao esquema são usadas para criar objetos específicos do Exchange, como agentes e conectores. Os atributos adicionados ao esquema são usados para configurar os objetos específicos do Exchange e os usuários e os grupos habilitados para email. Esses atributos incluem propriedades, como as configurações do Microsoft Office Outlook Web Access e as configurações de Unificação de Mensagens (UM) do Microsoft Exchange. Cada controlador de domínio e servidor de catálogo global da floresta contém uma réplica completa da partição de esquema.

Para obter mais informações sobre modificações de esquema no Exchange 2013, consulte [Alterações de esquema do Active Directory no Exchange 2013](exchange-2013-active-directory-schema-changes-exchange-2013-help.md).

## Partição de configuração

A partição de configuração armazena informações sobre a configuração de toda a floresta. Essas informações incluem a configuração de sites do Active Directory, configurações globais do Exchange, configurações de transporte e diretivas de caixa de correio. Cada tipo de informação de configuração é armazenado em um contêiner na partição de configuração. As informações de configuração do Exchange são armazenadas em uma subpasta no contêiner de serviços da partição de configuração. As informações armazenadas nesse contêiner incluem:

  - Listas de endereços

  - Diretivas de caixas de correio do catálogo de endereços

  - Grupos administrativos

  - Configurações de acesso para cliente

  - Conexões

  - Configurações de caixa de correio móveis

  - Configurações globais

  - Configurações de monitoramento

  - Diretivas do sistema

  - Contêiner de políticas de retenção

  - Configurações de transporte

Cada controlador de domínio e servidor de catálogo global da floresta contém uma réplica completa da partição de configuração.

## Partição de domínio

A partição de domínio armazena informações em contêineres padrão e em unidades organizacionais criadas pelo administrador do Active Directory. Esses contêineres armazenam os objetos específicos do domínio. Esses dados incluem objetos do sistema Exchange e informações sobre computadores, usuários e grupos desse domínio. Quando o Exchange 2013 é instalado, o Exchange atualiza os objetos dessa partição para aceitar a funcionalidade do Exchange. Essa funcionalidade afeta o modo como as informações do destinatário são armazenadas e acessadas.

Cada controlador de domínio contém uma réplica completa da partição do domínio para o qual ele está autorizado. Cada servidor de catálogo global da floresta contém um subconjunto das informações de cada partição de domínio da floresta.

## Como o Exchange 2013 acessa informações no Active Directory

O Exchange 2013 usa uma API do Active Directory para acessar as informações armazenadas no Active Directory. O serviço de Topologia do Microsoft ExchangeActive Directory é executado em todas as funções de servidor do Exchange 2013. Esse serviço lê informações em todas as partições do Active Directory. Os dados recuperados são armazenados em cache e usados pelos servidores do Exchange 2013 para descobrir o site do Active Directory de todos os serviços do Exchange na organização.

Para obter mais informações sobre topologia e descoberta de serviços, consulte [Planejar o uso de sites do Active Directory para roteamento de email](planning-to-use-active-directory-sites-for-routing-mail-exchange-2013-help.md).

O Exchange 2013 é um aplicativo de reconhecimento de sites do Active Directory que prefere se comunicar com os servidores de diretório localizados no mesmo site do servidor Exchange para otimizar o tráfego de rede. Cada função de servidor organizacional do Exchange 2013 deve se comunicar com o Active Directory para recuperar informações sobre destinatários e sobre as demais funções de servidor do Exchange 2013. Os dados obtidos por cada função de servidor são descritos nas seções a seguir.

Por padrão, sempre que um servidor Exchange 2013 for iniciado, ele se liga a um controlador de domínio e um servidor de catálogo global selecionados aleatoriamente em seu próprio site. Você pode visualizar os servidores de diretório selecionados usando o cmdlet **Get-ExchangeServer** no Shell de Gerenciamento do Exchange. Também é possível usar o cmdlet **Set-ExchangeServer** para configurar uma lista estática de controladores de domínio ao qual um servidor Exchange 2013 deve se ligar ou uma lista de controladores de domínio que devem ser excluídos.


> [!IMPORTANT]
> Um controlador de domínio do Windows Server 2008 pode ser configurado como um servidor de diretório somente leitura. Essa configuração é útil quando você deseja implantar um controlador de domínio ou um servidor de catálogo global em um site remoto para fins de autenticação e de autorização, mas não deseja permitir que os administradores desse site gravem alterações no Active Directory. Entretanto, não é possível implantar um servidor do Exchange 2013 em qualquer site que contenha apenas servidores de diretório somente leitura.



## Função de servidor Caixa de Correio

A função de servidor de Caixa de Correio armazena informações de configuração sobre usuários e repositórios de caixa de correio no Active Directory. Além disso, para o Exchange 2013, o servidor de Caixa de Correio inclui todos os componentes de servidor tradicionais encontrados no Exchange 2010: os protocolos de Acesso para Cliente ,o serviço de Transporte, os bancos de dados de Caixa de Correio e a Unificação de Mensagens. O servidor de Caixa de Correio lida com toda a atividade das caixas de correio ativas nesse servidor.

## Função de servidor de acesso para cliente

No Exchange 2013, o servidor de Acesso para Cliente fornece autenticação, redirecionamento limitado e serviços de proxy. O próprio servidor de Acesso para Cliente não faz nenhum processamento de dados. O servidor de Acesso para Cliente é um servidor fino e sem monitoração de estado. Nunca há nada na fila ou armazenado no servidor de Acesso para Cliente. O servidor de Acesso para Cliente oferece todos os protocolos de acesso para cliente comuns: HTTP, POP e IMAP e SMTP.

## Recuperação de objetos excluídos do Exchange

Active Directory A Lixeira ajuda a minimizar o tempo de inatividade do serviço de diretório, melhorando a capacidade de preservar e recuperar objetos excluídos do Active Directory sem restaurar dados do Active Directory dos backups, reiniciando o Active Directory Domain Services (AD DS) ou reinicializando os controles de domínio.

A coisa mais importante a entender sobre a recuperação de objetos excluídos do Exchange relacionados ao Active Directory é que os objetos do Exchange não existem isoladamente. Por exemplo, quando você habilita para email um usuário, várias diretivas e vários links diferentes são calculados para o usuário com base na configuração atual do Exchange. Dois problemas que podem surgir quando você restaurar um objeto de destinatário ou uma configuração excluída do Exchange são:

  - **Colisões**   Alguns atributos do Exchange devem ser exclusivos em uma floresta. Por exemplo, os endereços proxy (de email) não devem ser os mesmos para dois usuários diferentes. O Active Directory não aplica exclusividade de endereço proxy (as ferramentas administrativas do Exchange verificam a exclusividade). As diretivas de endereço de email do Exchange também resolvem automaticamente possíveis conflitos na atribuição de endereços proxy com base em regras determinísticas. Por isso, é possível restaurar um objeto de usuário do Exchange e, como resultado, criar uma colisão com endereços proxy ou outros atributos que devem ser exclusivos.

  - **Erros de Configuração**   O Exchange automatizou as regras que atribuem várias diretivas ou configurações. Se você excluir um destinatário e alterar as regras ou as diretivas, a restauração de um objeto de usuário do Exchange poderá resultar em um usuário sendo atribuído à diretiva incorreta (ou até mesmo a uma diretiva que não existe mais).

As seguintes diretrizes o ajudarão a minimizar problemas ou questões quando você recuperar objetos excluídos relacionados ao Exchange:

  - Se você tiver excluído um objeto de configuração do Exchange usando as ferramentas de gerenciamento do Exchange, não restaure o objeto. Em vez disso, crie novamente o objeto usando as ferramentas de gerenciamento do Exchange (centro de administração do Exchange ou Shell de Gerenciamento do Exchange).

  - Se você tiver excluído um objeto de configuração do Exchange sem usar as ferramentas de gerenciamento do Exchange, recupere o objeto quanto antes. Quanto mais alterações administrativas e de configuração tiverem sido feitas no sistema desde a exclusão, maior será a probabilidade de a restauração dos objetos resultar em configuração incorreta.

  - Se você recuperar destinatários excluídos do Exchange (contatos, usuários ou grupos de distribuição), monitore de perto as colisões e os erros relacionados aos objetos recuperados. Se as diretivas do Exchange ou outra configuração relacionada a destinatários puderem ter sido modificadas desde a exclusão, reaplique as diretivas atuais aos destinatários restaurados para garantir que eles sejam configurados corretamente.

## Para obter mais informações

[Active Directory Recycle Bin de guia passo a passo](https://go.microsoft.com/fwlink/p/?linkid=178720)

[Introdução ao aprimoramentos de centro administrativo do Active Directory (nível 100)](https://go.microsoft.com/fwlink/p/?linkid=267641)

[Avançadas de gerenciamento do AD DS usando o Active Directory Administrative Center (nível 200)](https://go.microsoft.com/fwlink/p/?linkid=267642)

