---
title: 'POP3 e IMAP4 no Exchange Server 2013: Exchange 2013 Help'
TOCTitle: POP3 e IMAP4
ms:assetid: a7dc91ee-2919-4db3-ae9c-cd665d2e09ea
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/JJ657728(v=EXCHG.150)
ms:contentKeyID: 50486305
ms.date: 01/10/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# POP3 e IMAP4 no Exchange Server 2013

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2016-08-16_

Saiba mais sobre as diferenças entre os protocolos POP3 e IMAP4 no Exchange Server 2013 e como configurar opções para acessar caixas de correio do Exchange 2013 de vários programas de email.

Por padrão, POP3 e IMAP4 estão desabilitados no Exchange Server 2013. Para dar suporte a clientes POP3 que ainda dependem desses protocolos, você precisa iniciar dois serviços POP3: o serviço POP3 do Microsoft Exchange e o serviço de Back-end do Microsoft Exchange POP3. Para dar suporte a clientes IMAP4 que ainda dependem desses protocolos, você precisa iniciar dois serviços IMAP4: o serviço IMAP4 do Microsoft Exchange e o serviço de Back-end do Microsoft Exchange IMAP4.

Para obter instruções detalhadas sobre como habilitar os serviços POP3 e IMAP4, consulte [Habilitar POP3 no Exchange 2013](enable-pop3-in-exchange-2013-exchange-2013-help.md) e [Habilitar IMAP4 no Exchange 2013](enable-imap4-in-exchange-2013-exchange-2013-help.md).

Por padrão, os usuários com caixas de correio em computadores que executam o Exchange 2013 podem acessar suas caixas de correio usando o Outlook ou o Outlook Web App, Exchange ActiveSync, ou o Voice Access do Outlook. O Outlook, Outlook Web App e o Voice Access do Outlook permitem que seus usuários de email usem o abrangente conjunto de recursos que estão disponíveis para usuários com caixas de correio em servidores do Exchange 2016.

**Sumário**

Visão geral da funcionalidade de POP3 e IMAP4

Conectividade entre sites POP3 e IMAP4

Usando contas não padrão com POP3 e IMAP4

Noções básicas sobre diferenças entre POP3 e IMAP4

Opções de envio e recebimento para aplicativos de email POP3 e IMAP4

Aplicativos POP3 e IMAP4

Definições do usuário para configurar o acesso POP3 ou IMAP4 às suas caixas de correio do Exchange 2013

## Visão geral da funcionalidade de POP3 e IMAP4

Esta seção descreve as funcionalidades POP3 e IMAP4 para Exchange 2013.

Os protocolos POP3 e IMAP4 têm os seguintes benefícios e limitações:

  - **POP3**   Projetado para oferecer suporte ao processamento de emails offline. Com POP3, as mensagens de email são removidas do servidor e armazenadas no cliente POP3 local, a menos que o cliente tenha sido configurado para deixar emails no servidor. Isso coloca o gerenciamento dos dados e a responsabilidade pela segurança nas mãos do usuário. POP3 não oferece recursos de colaboração avançados, como calendário, contatos e tarefas.

  - **IMAP4**   Oferece acesso online e offline, mas, assim como o POP3, o IMAP4 não oferece recursos de colaboração avançados, como calendário, contatos e tarefas.

Os aplicativos de email POP3 e IMAP4 não utilizam POP3 e IMAP4 para enviar mensagens ao servidor de email. Eles dependem do protocolo SMTP para enviar mensagens. O conector de recebimento de envio de emails de aplicativos de clientes que usam POP3 ou IMAP4 é criado automaticamente na instalação do Exchange. Para saber mais sobre conectores, veja [Conectores de recebimento](receive-connectors-exchange-2013-help.md).


> [!TIP]
> Sempre que um usuário usa um programa de email baseado em POP ou IMAP para abrir emails do Office 365, existe a possibilidade de haver um atraso de vários segundos. O atraso é causado pelo servidor proxy, que gera um salto adicional para autenticação. Esse servidor proxy primeiro analisa o servidor de pod atribuído (servidor de Acesso para Cliente) e depois faz a autenticação com base nisso.



## Conectividade entre sites POP3 e IMAP4

Em versões anteriores do Exchange, era necessário executar uma etapa de configuração manual para permitir que seus clientes POP3 e IMAP4 se conectassem aos seus emails a partir de um site na organização quando a caixa de correio estivesse localizada em um site diferente da organização. Por padrão, o Exchange 2013 automaticamente estabelece conexão via proxy de um servidor de Acesso para Cliente em um site para o servidor correto.

## Usar contas não padrão com POP3 e IMAP4

Não é possível usar a conta Anônimo ou Convidado para entrar em uma caixa de correio do Exchange 2016 por meio de POP3 ou IMAP4. As contas anônimas são proibidas devido às vulnerabilidades de segurança presentes quando contas não padrão para acesso POP3 e IMAP4 são usadas. Além disso, você não pode se conectar à caixa de correio de Administrador por meio de POP3 ou IMAP4. Esta limitação foi incluída intencionalmente no Exchange 2013, para aprimorar a segurança da caixa de correio do Administrador. Para acessar a caixa de correio do Administrador, use o Outlook ou o Outlook Web App.

## Compreender as diferenças entre POP3 e IMAP4

**POP3** O POP3 é um protocolo de email da Internet utilizado com frequência. Por padrão, quando os aplicativos de email que usam POP3 baixam mensagens de email em um computador cliente, essas mensagens baixadas são removidas do servidor. Quando uma cópia do email do usuário não é guardada no servidor de emails, o usuário não consegue acessar as mesmas mensagens através de outros computadores. No entanto, alguns aplicativos de email que usam POP3 podem ser configurados para manter cópias de suas mensagens no servidor, de forma que você possa acessar as mesmas mensagens a partir de outro computador. Os aplicativos de email que usam POP3 podem ser usados somente para baixar mensagens do servidor de email para uma única pasta (normalmente a Caixa de Entrada) no computador cliente. O protocolo POP3 não sincroniza várias pastas no servidor de email com várias pastas do computador cliente.

**IMAP4** Os aplicativos cliente de email que usam IMAP4 são mais flexíveis e geralmente oferecem mais recursos do que os aplicativos cliente de email que usam POP3. Por padrão, quando aplicativos de email que usam IMAP4 baixam mensagens para o computador cliente, uma cópia das mensagens baixadas é mantida no servidor. Como uma cópia da mensagem do usuário é guardada no servidor de emails, o usuário pode acessar as mesmas mensagens a partir de outros computadores. Com o email IMAP4, o usuário pode acessar e criar várias pastas de email no servidor. Dessa forma, os usuários podem acessar qualquer mensagem do servidor a partir de computadores em vários locais. Por exemplo, a maioria dos aplicativos de email IMAP4 pode ser configurada para manter uma cópia dos itens enviados no servidor, de forma que o usuário possa acessar esses itens em qualquer outro computador. O IMAP4 oferece suporte a outros recursos que não têm suporte na maioria dos aplicativos IMAP4. Por exemplo, alguns aplicativos IMAP4 contêm um recurso que permite ao usuário exibir somente os cabeçalhos das mensagens de email no servidor, ou seja, o remetente e o assunto, e depois baixar somente as mensagens que desejar ler. O IMAP4 também não é compatível com o acesso à pasta pública.


> [!TIP]
> Clientes IMAP4 e POP3 tem acesso limitado às informações do calendário do Exchange. Para obter mais informações, consulte <A href="configure-calendar-options-for-pop3-exchange-2013-help.md">Configurar opções de calendário para POP3</A> e <A href="configure-calendar-options-for-imap4-exchange-2013-help.md">Configurar opções de calendário para o IMAP4</A>.



## Opções de envio e recebimento para aplicativos de email POP3 e IMAP4

Aplicativos de email POP3 e IMAP4 permitem que os usuários escolham o momento de se conectar ao servidor para enviar e receber emails. Esta seção apresenta algumas das opções de conectividade mais comuns e também fornece alguns fatores que os usuários devem considerar ao selecionar as opções de conexão disponíveis em seus aplicativos de email POP3 e IMAP4.

## Definições de configuração comuns

Três das configurações de conexão mais comuns que podem ser definidas no aplicativo cliente POP3 e IMAP4 são:

  - Enviar e receber mensagens sempre que o aplicativo de email é iniciado. Ao usar essa opção, as mensagens são enviadas e recebidas somente quando o usuário inicia o aplicativo de email.

  - Enviar e receber mensagens manualmente. Ao usar essa opção, as mensagens são enviadas e recebidas somente quando o usuário clica na opção "enviar e receber" na interface de usuário do cliente.

  - Enviar e receber mensagens a cada intervalo de minutos definido. Quando o usuário define essa opção, o aplicativo cliente se conecta ao servidor a cada intervalo de minutos definido para enviar e baixar novas mensagens.

Para informações sobre como configurar essas definições para seu aplicativo de email, consulte a documentação da Ajuda fornecida juntamente com o respectivo aplicativo.

## Considerações ao configurar opções de envio/recebimento

Se o dispositivo ou o computador que está executando o aplicativo de email POP3 ou IMAP4 estiver sempre conectado à Internet, o usuário poderá configurar o aplicativo de email para enviar e receber mensagens em um intervalo de minutos definido. Conectar-se frequentemente ao servidor permite que o usuário mantenha o aplicativo de email atualizado com as informações mais recentes do servidor. No entanto, se o dispositivo ou o computador que está executando o aplicativo de email POP3 ou IMAP4 estiver sempre conectado à Internet, o usuário poderá configurar o aplicativo de email para enviar e receber mensagens manualmente.


> [!TIP]
> Se estiver usando um aplicativo de email compatível com IMAP4 e com suporte ao comando IMAP4 IDLE, o usuário poderá enviar e receber emails de sua caixa de correio do Exchange quase em tempo real. Para que esse método de conexão funcione, o aplicativo do servidor de emails e o aplicativo cliente devem oferecer suporte ao comando IMAP4 IDLE. Na maioria dos casos, não é necessário definir as configurações no aplicativo IMAP4 para usar esse método de conexão.



## Aplicativos POP3 e IMAP4

Como o Exchange 2013 oferece suporte a POP3 e IMAP4, os usuários podem usar vários aplicativos cliente POP3 e IMAP4 para se conectarem ao Exchange 2013. Esses aplicativos incluem o Outlook, o Outlook Web App, o Windows Live Mail, o Outlook Express, o Entourage e muitos aplicativos de terceiros, como o Gmail, Mozilla Thunderbird e o Eudora. Os recursos compatíveis com cada aplicativo cliente de email variam. Para mais informações sobre os recursos específicos oferecidos por determinados aplicativos cliente de email POP3 e IMAP4, veja a documentação de cada aplicativo.

## Definições do usuário para configurar o acesso POP3 ou IMAP4 às suas caixas de correio do Exchange 2013

Depois de habilitar o acesso do cliente POP3 e IMAP4, você precisa oferecer aos usuários informações necessárias para que eles conectem seus programas de email à caixa de correio do Exchange 2016.

Para se conectarem a partir da rede corporativa, os usuários precisam das seguintes informações:

  - Nome do servidor POP3 ou IMAP4 interno

  - Número da porta POP3 ou IMAP4 interna

  - Método de criptografia POP3 ou IMAP4 interno

  - Nome do SMTP (servidor de saída) interno

  - Número da porta SMTP (servidor de saída) interna

  - Método de criptografia do SMTP (servidor de saída) interno

Para se conectarem a partir da Internet, eles precisarão das seguintes informações:

  - Nome do servidor POP3 ou IMAP4 externo

  - Número da porta POP3 ou IMAP4 externa

  - Método de criptografia POP3 ou IMAP4 externo

  - Nome do SMTP (servidor de saída) externo

  - Número da porta SMTP (servidor de saída) externa

  - Método de criptografia do SMTP (servidor de saída) externo

Essas configurações podem ser disponibilizadas aos seus usuários por email ou por outros métodos de comunicação manual. Você também pode configurar o Exchange para que seus usuários possam usar o Outlook Web App para procurar suas próprias configurações.

**Configurar o Exchange para que os usuários possam procurar suas respectivas configurações de servidores POP3, IMAP4 e SMTP**

Por padrão, os usuários não podem pesquisar suas configurações de servidor POP3, IMAP4 e SMTP usando o Outlook Web App. Para permitir que seus usuários façam isso, é preciso usar os cmdlets **Set-PopSettings** e **Set-ImapSettings**. Para permitir que seus usuários procurem suas configurações de servidor SMTP (saída), você deve usar o cmdlet **Set-ReceiveConnector**.

Proceda da seguinte forma para permitir que os usuários procurem suas próprias configurações POP3, IMAP4 e SMTP:

  - **Configurações POP3**   Execute o cmdlet **Set-POPSettings** com o parâmetro *ExternalConnectionSettings*. Use o formato `Set-POPSettings -ExternalConnectionSetting {<FQDN>:995:SSL}`. Por exemplo, execute `Set-PopSettings -ExternalConnectionSetting {Dublin01.Contoso.com:995:SSL}` se quiser que os clientes que se conectam por meio do servidor com FQDN Dublin01.Contoso.com possam consultar suas próprias configurações POP.
    
    Você deve reiniciar o IIS depois de aplicar essa configuração.

  - **Configurações IMAP4**   Execute o cmdlet **Set-IMAPSettings** com o parâmetro *ExternalConnectionSettings*. Use o formato `Set-ImapSettings -ExternalConnectionSetting {<FQDN>:993:SSL}`. Por exemplo, execute `Set-IMAPSettings -ExternalConnectionSetting {Dublin01.Contoso.com:993:SSL}` se quiser que os clientes que se conectam por meio do servidor com FQDN Dublin01.Contoso.com possam consultar sua própria configuração IMAP.
    
    Você deve reiniciar o IIS depois de aplicar essa configuração.

  - **Configurações SMTP**   Execute o cmdlet **Set-ReceiveConnector** com o parâmetro *AdvertiseClientSettings*. Use o formato `Set-ReceiveConnector "Client Frontend <Server Name>" -AdvertiseClientSettings $True -FQDN <FQDN>`. Por exemplo, execute `Set-ReceiveConnector "Client Frontend <Server Name>" -AdvertiseClientSettings $True -FQDN Dublin01.Contoso.com` se quiser que os clientes se conectem pelo servidor com FQDN Dublin01.Contoso.com para poder analisar suas próprias configurações SMTP.
    
    Você deve reiniciar o IIS depois de aplicar essa configuração.

Depois de alterar suas configurações padrão executando os cmdlets **Set-POPSettings**, **Set-IMAPSettings** e **Set-ReceiveConnector**, seus usuários poderão procurar suas configurações de servidor POP, IMAP e SMTP no Outlook Web App clicando em **Configurações** \> **Opções** \> **Conta** \> **Minha conta** \> **Configurações para acesso POP ou IMAP**.

**Deixar uma cópia das mensagens no servidor**

A configuração padrão em alguns programas de email é remover as mensagens no servidor depois delas serem recuperadas. Certifique-se de recomendar aos seus usuários que configurem o programa de email para manter uma cópia de todas as mensagens que o cliente recupera no servidor. Manter uma cópia das mensagens no servidor permite que os usuários acessem suas mensagens a partir de programas de email diferentes.

