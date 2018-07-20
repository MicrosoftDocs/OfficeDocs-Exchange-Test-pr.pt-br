---
title: 'Configurar o fluxo de emails da Internet através de um servidor de transporte de borda sem usar o EdgeSync: Exchange 2013 Help'
TOCTitle: Configurar o fluxo de emails da Internet através de um servidor de transporte de borda sem usar o EdgeSync
ms:assetid: 6bb98d10-6f12-4b08-a58e-36375f605d65
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Bb232082(v=EXCHG.150)
ms:contentKeyID: 61183352
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configurar o fluxo de emails da Internet através de um servidor de transporte de borda sem usar o EdgeSync

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2017-01-23_

Recomendamos que você use o processo de Inscrição de Borda para estabelecer o fluxo de email entre a organização do Exchange e um servidor de Transporte de Borda. Entretanto, determinadas situações podem impedir que você inscreva o servidor de Transporte de Borda em sua organização do Exchange usando o processo de Inscrição de Borda. Para estabelecer manualmente o fluxo de mensagens entre a organização do Exchange e um servidor de Transporte de Borda, crie e configure os Conectores de envio e de recebimento no servidor de Transporte de Borda e nos servidores de Caixa de Correio na organização do Exchange.

## Antes de você começar

  - Tempo estimado para a conclusão da tarefa: 30 minutos.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Conectores de envio", a entrada "Conectores de envio - Transporte de Borda" e a entrada "Conectores de recebimento - Transporte de Borda" no tópico [Permissões de fluxo de email](mail-flow-permissions-exchange-2013-help.md).

  - Esse procedimento usa autenticação Básica por TLS (Transport Layer Security) para fornecer criptografia e autenticação. Quando você usa autenticação Básica por TLS, o servidor de recebimento deve ter um certificado de servidor SSL (Secure Sockets Layer) X.509 instalado. O valor do FQDN (nome de domínio totalmente qualificado) configurado no Conector de Recebimento deve corresponder ao FQDN no certificado de servidor SSL. Por padrão, o valor do FQDN no Conector de Recebimento é o FQDN do servidor que contém o Conector de Recebimento.

  - Também é possível usar o método de autenticação Protegido Externamente. No entanto, se você fizer isso, a comunicação entre o servidor de Transporte de Borda e o servidor de Caixa de Correio não será autenticada nem criptografada pelo Exchange. Recomendamos que você use o método de autenticação Protegido Externamente somente quando um método de criptografia adicional também for usado. O método de criptografia pode ser uma associação IPsec (Internet Protocol Security) ou uma VPN (rede virtual privada).

  - Um servidor de Transporte de Borda normalmente é *multihomed*. Isso significa que o servidor de Transporte de Borda tem adaptadores de rede que estão conectados a vários segmentos de rede. Cada um desses adaptadores de rede tem uma configuração de IP exclusiva. O adaptador de rede conectado ao segmento de rede externo, ou público, deve ser configurado para usar um servidor DNS público para resolução de nomes. Isso permite ao servidor resolver nomes de domínio SMTP para registros de recurso MX e rotear o email para a Internet. O adaptador de rede conectado ao segmento de rede interno, ou privado, deve ser configurado para usar um servidor DNS na rede de perímetro ou deve ter um arquivo Hosts disponível.

  - Você deve criar uma conta de usuário no Active Directory e adicionar a conta ao grupo de segurança universal no computador do Exchange Server. Essa conta é usada pelo Conector de envio no servidor de Transporte de Borda para autenticar o servidor de Caixa de Correio de destino na organização do Exchange.
    

    > [!IMPORTANT]
    > Essa conta obtém as permissões associadas aos computadores que executam o Exchange Server. Lembre-se de proteger as credenciais da conta para impedir o uso incorreto. Você pode configurar a conta para permitir logon somente a computadores específicos.



## Procedimentos do servidor de Transporte de Borda

Os seguintes conectores são necessários em um servidor de Transporte de Borda:

  - Um conector de Envio configurado para enviar mensagens para a Internet

  - Um conector de Envio configurado para enviar mensagens a servidores de Caixa de Correio na organização do Exchange

  - Um conector de Recebimento configurado para receber mensagens apenas dos servidores de Caixa de Correio na organização do Exchange

  - Um conector de Recebimento configurado para aceitar mensagens apenas da Internet

Por padrão, um único Conector de Recebimento é criado durante a instalação da função de servidor Transporte de Borda. Esse conector pode ser usado tanto para mensagens de entrada da Internet quanto para mensagens de entrada dos servidores de Caixa de Correio. Geralmente, o processo de Inscrição de Borda configura automaticamente as permissões e a autenticação corretas no Conector de Recebimento padrão. Quando você não usar o processo de Inscrição de Borda, recomendamos modificar o conector de Recebimento padrão no servidor de Transporte de Borda para aceitar apenas mensagens da Internet. Assim, você deve criar um conector de Recebimento no servidor de Transporte de Borda configurado apenas para aceitar mensagens dos servidores de Caixa de Correio internos.

As seções a seguir orientam você em meio a todas as etapas de configuração obrigatórias para preparar o servidor de Transporte de Borda para se comunicar com a organização do Exchange.


> [!TIP]
> Você só pode usar o Shell para executar estes procedimentos em servidores de Transporte de Borda.



## Etapa 1: Criar um conector de Envio configurado para enviar mensagens para a Internet

Esse conector de Envio exige as seguintes configurações:

  - **Nome**   Para a Internet (ou qualquer nome descritivo)

  - **Tipo de uso**   Internet.

  - **Espaços de endereçamento**   "\*" (todos os domínios).

  - **Configurações de rede**   Use registros MX do DNS para rotear o email automaticamente. Dependendo da configuração da rede, você também pode rotear mensagens por meio de um host inteligente. O host inteligente, então, direciona a mensagem para a Internet.

Para criar um conector de Envio que esteja configurado para enviar mensagens para a Internet, execute o comando a seguir.

    New-SendConnector -Name "To Internet" -AddressSpaces * -Usage Internet -DNSRoutingEnabled $true

Para informações detalhadas de sintaxes e de parâmetros, consulte [New-SendConnector](https://technet.microsoft.com/pt-br/library/aa998936\(v=exchg.150\)).

## Etapa 2: Criar um conector de Envio configurado para enviar mensagens para a organização do Exchange

Use o cmdlet **New-SendConnector** para criar um novo conector de Envio.


> [!TIP]
> Antes de criar o conector de Envio, você deve primeiro executar o comando <STRONG>Get-Credential</STRONG> para salvar o nome e a senha do usuário que usará em uma variável temporária. Você precisa fazer isso porque o cmdlet <STRONG>New-SendConnector</STRONG> não aceita as credenciais de usuário em texto sem formatação.



Esse conector de Envio exige as seguintes configurações:

  - **Nome**   Para a organização interna (ou qualquer nome descritivo)

  - **Tipo de uso**   Interno

  - **Espaços de endereçamento**   Todos os domínios aceitos para a organização do Exchange Por exemplo, \*.contoso.com.

  - Roteamento DNS desabilitado (roteamento de host inteligente habilitado)

  - **Hosts inteligentes**   FQDN de um ou mais servidores de Caixa de Correio como hosts inteligentes. Por exemplo, mbxserver01.contoso.com e mbxserver02.contoso.com.

  - **Métodos de autenticação de host inteligente**   Autenticação básica sobre TLS

  - **Credenciais de autenticação de host inteligente**   Credenciais para a conta de usuário no domínio interno. Primeiro você precisa salvar o nome de usuário e a senha em uma variável temporária, porque o cmdlet **New-SendConnector** não aceitará credenciais do usuário em texto sem formatação.

Para criar um conector de Envio que esteja configurado para enviar mensagens para a organização do Exchange, execute os comandos a seguir.

    $MailboxCredentials = Get-Credential
    New-SendConnector -Name "To Internal Org" -Usage Internal -AddressSpaces *.contoso.com -DNSRoutingEnabled $false -SmartHosts mbxserver01.contoso.com,mbxserver02.contoso.com -SmartHostAuthMechanism BasicAuthRequireTLS -AuthenticationCredential $MailboxCredentials

Para obter informações detalhadas sobre sintaxe e parâmetros, consulte [New-SendConnector](https://technet.microsoft.com/pt-br/library/aa998936\(v=exchg.150\)).

## Etapa 3: Modificar o conector de Recebimento padrão para aceitar apenas mensagens da Internet

Você deve fazer as seguintes alterações na configuração do conector de Recebimento padrão:

  - Modifique o nome para refletir que o conector será usado exclusivamente para receber email da Internet. O nome do conector de Recebimento padrão é "Conector de Recebimento interno padrão \<Nome do servidor de Transporte de Borda\>".

  - Altere as associações de rede para aceitar mensagens apenas do adaptador de rede acessível na Internet. Por exemplo, 10.1.1.1 e o valor de porta TCP SMTP padrão, 25.

Para modificar o conector de Recebimento padrão para aceitar apenas mensagens da Internet, execute o comando a seguir.

    Set-ReceiveConnector "Default internal Receive connector Edge01" -Name "From Internet" -Bindings 10.1.1.1:25

Para informações detalhadas de sintaxes e de parâmetros, consulte [Set-ReceiveConnector](https://technet.microsoft.com/pt-br/library/bb125140\(v=exchg.150\)).

## Etapa 4: Criar um conector de Recebimento configurado para aceitar exclusivamente mensagens da organização do Exchange

Esse Conector de Recebimento exige as seguintes configurações:

  - **Nome**   Da organização interna (ou qualquer nome descritivo)

  - **Tipo de uso**   Interno

  - **Associações de rede local**   Adaptador de rede voltado para a rede interna. Por exemplo, 10.1.1.2 e o valor de porta TCP SMTP padrão, 25.

  - **Configurações de rede remota**   Endereço IP de um ou mais servidores de Caixa de Correio na organização do Exchange Por exemplo, 192.168.5.10 e 192.168.5.20.

  - **Métodos de autenticação**   TLS, autenticação básica, autenticação básica sobre TLS e autenticação do Exchange Server.

Para criar um conector de Envio que esteja configurado para aceitar mensagens apenas da organização do Exchange, execute o comando a seguir.

    New-ReceiveConnector -Name "From Internal Org" -Usage Internal -AuthMechanism TLS,BasicAuth,BasicAuthRequireTLS,ExchangeServer -Bindings 10.1.1.2:25 -RemoteIPRanges 192.168.5.10,192.168.5.20

Para obter informações detalhadas sobre sintaxe e parâmetros, consulte [New-ReceiveConnector](https://technet.microsoft.com/pt-br/library/bb125139\(v=exchg.150\)).

## Como saber se estas etapas funcionaram?

Para verificar se você configurou com êxito os conectores de Envio e de Recebimento necessários, execute os comandos a seguir no servidor de Transporte de Borda e verifique se os valores exibidos são os valores que você configurou.

    Get-SendConnector | Format-List Name,Usage,AddressSpaces,SourceTransportServers,DSNRoutingEnabled,SmartHosts,SmartHostAuthMechanism
    Get-ReceiveConnector | Format-List Name,Usage,AuthMechanism,Bindings,RemoteIPRanges

## Procedimentos para servidores de Caixa de Correio

Os servidores de Caixa de Correio em sua organização exigem um conector de Envio configurado para enviar mensagens do servidor de Transporte de Borda para retransmissão para a Internet.

Por padrão, dois conectores de Recebimento são criados durante a instalação da função de servidor de Caixa de Correio. O conector chamado Cliente *Nomedoservidor* é configurado para aceitar mensagens de todos os clientes do sistema de mensagens POP3 e IMAP. O conector chamado *Nomedoservidor* Padrão é configurado para aceitar mensagens de um servidor de Transporte de Borda. Nenhuma modificação é necessária nesses conectores.

## Etapa 5: Criar um conector de Envio configurado para enviar mensagens de saída para o servidor de Transporte de Borda

Esse conector de Envio exige as seguintes configurações:

  - **Nome**   Para a borda (ou qualquer nome descritivo)

  - **Tipo de uso**   Interno

  - **Espaços de endereçamento**   "\*" (todos os domínios).

  - Roteamento DNS desabilitado (roteamento de host inteligente habilitado)

  - **Hosts inteligentes**   Endereço IP ou FQDN do servidor de Transporte de Borda. Por exemplo, edge01.contoso.net.

  - **Servidores de Caixa de Correio de origem**   FQDN de um ou mais servidores de Caixa de Correio. Por exemplo, mbxserver01.contoso.com e mbxserver02.contoso.com.

  - **Método de autenticação de host inteligente**   Autenticação básica sobre TLS.

  - **Credenciais de autenticação de host inteligente**   Credenciais para a conta de usuário no servidor de Transporte de Borda. Primeiro você precisa salvar o nome de usuário e a senha em uma variável temporária, porque o cmdlet **New-SendConnector** não aceitará credenciais do usuário em texto sem formatação.

Para criar um conector de Envio que esteja configurado para enviar mensagens para o servidor de Transporte de Borda, execute os comandos a seguir.

    $EdgeCredentials = Get-Credential
    New-SendConnector -Name "To Edge" -Usage Internal -AddressSpaces * -DNSRoutingEnabled $false -SmartHosts edge01.contoso.com -SourceTransportServers mbxserver01.contoso.com,mbxserver02.contoso.com -SmartHostAuthMechanism BasicAuthRequireTLS -AuthenticationCredential $EdgeCredentials

Para obter informações detalhadas sobre sintaxe e parâmetros, consulte [New-SendConnector](https://technet.microsoft.com/pt-br/library/aa998936\(v=exchg.150\)).

## Como saber se essa etapa funcionou?

Para verificar se você criou com êxito um conector de Envio configurado para enviar mensagens de saída para o servidor de Transporte de Borda, execute o comando a seguir no servidor de Caixa de Correio e verifique se os valores exibidos são os valores que você configurou.

    Get-SendConnector | Format-List Name,Usage,AddressSpaces,DSNRoutingEnabled,SmartHosts,SourceTransportServers,SmartHostAuthMechanism

