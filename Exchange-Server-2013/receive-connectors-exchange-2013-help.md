---
title: 'Conectores de recebimento: Exchange 2013 Help'
TOCTitle: Conectores de recebimento
ms:assetid: 17751a60-39fe-433f-84d2-bfc14ff4ba51
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Aa996395(v=EXCHG.150)
ms:contentKeyID: 50485019
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Conectores de recebimento

 

_**Aplica-se a:**Exchange Server 2013_

_**Tópico modificado em:**2015-04-07_

O fluxo de mensagens de entrada para sua organização do Exchange de controle de conectores de recebimento. Eles são configurados em computadores executando o Microsoft Exchange Server 2013 com o serviço de transporte ou no serviço Front-End em um servidor de acesso para cliente. Eles podem ser criados no Centro de administração do Exchange (EAC) ou no Shell de gerenciamento do Exchange.

Por padrão, conectores de recebimento que são necessários para o fluxo de emails internos são criados automaticamente quando um servidor de acesso para cliente ou servidor de caixa de correio está instalado.

os servidores de Exchange 2013 executando o serviço de transporte exigem conectores de recebimento para receber mensagens da Internet, de clientes de email e de outros servidores de email. Conexões para a organização Exchange de entrada de controles de conector de recebimento.

Cada conector de recebimento escuta as conexões de entrada que coincidem com as configurações do conector de recebimento. Um conector de recebimento escuta conexões que são recebidos por meio de um determinado endereço IP local e a porta e de um intervalo de endereço IP especificado. Quando você deseja controlar quais servidores recebem mensagens de um determinado endereço IP ou intervalo de endereços IP e quando você deseja configurar as propriedades do conector especial para mensagens que são recebidas de um endereço IP específico, como permitir que mensagens maiores ou mais destinatários por mensagem, você pode criar um conector de recebimento. Você também pode abranger o conector de recebimento usando o parâmetro *TlsCertificateName* do cmdlet **Set-ReceiveConnector** , que permite que você especifique o certificado a ser usado para o conector.

Receber conectores têm o escopo para um único servidor e determine como esse servidor específico escuta as conexões. Quando você cria um conector de recebimento em um servidor de caixa de correio executando o serviço de transporte, o conector de recebimento é armazenado em Active Directory como um objeto filho do servidor no qual ele é criado.

Se você precisar conectores de recebimento adicionais para cenários específicos, você pode criá-los usando o Centro de administração do Exchange (EAC) ou o Shell de gerenciamento do Exchange. Cada conector de recebimento deve usar uma combinação exclusiva de vinculações de endereço IP, atribuições de número de porta e intervalos de endereços IP remotos do qual o email é aceito.

Para obter mais informações sobre como criar um conector de recebimento, consulte [Procedimentos do conector de recebimento](receive-connector-procedures-exchange-2013-help.md).

**Sumário**

Conectores de recebimento padrão criados durante a instalação

Conectores de recebimento padrão criados em um servidor de caixa de correio executando o serviço de transporte

Conectores de recebimento padrão criados em um servidor de Front End Transport

Tipos de conector de recebimento

Grupos de permissões de conector de recebimento

Especificações de tipo de conector de recebimento

Permissões de conector de recebimento

Configurações de autenticação do conector de recebimento

Novos recursos de conector de recebimento do Exchange 2013

## Conectores de recebimento padrão criados durante a instalação

Determinadas conectores de recebimento são criados por padrão quando você instala a função de servidor de caixa de correio.

## Conectores de recebimento padrão criados em um servidor de caixa de correio executando o serviço de transporte

Quando você instala um servidor de caixa de correio executando o serviço de transporte, dois conectores de recebimento são criados. Nenhum conector de recebimento adicionais é necessários para a operação típica e na maioria dos casos, os conectores de recebimento padrão não exigem uma alteração de configuração. Esses conectores são as seguintes:

  - **\< Nome do servidor \> padrão**   Aceita conexões de servidores de caixa de correio executando o serviço de transporte e de servidores de borda.

  - **Proxy do cliente \< nome do servidor \>**   Aceita conexões dos servidores front-end. Normalmente, as mensagens são enviadas para um servidor front-end via SMTP.

Um valor de *TransportRole* é atribuído a cada conector. Você pode usá-lo para determinar a função que está em execução no conector. Isso pode ser útil em casos onde você está executando a várias funções em um único servidor. No caso de cada conector de recebimento mencionado anteriormente, o valor de seus *TransportRole* é **HubTransport**.

Para exibir os conectores de recebimento padrão e seus valores de parâmetro, você pode usar o cmdlet [Get-ReceiveConnector](https://technet.microsoft.com/pt-br/library/aa998618\(v=exchg.150\)) .

## Conectores de recebimento padrão criados em um servidor de Front End Transport

Durante a instalação, três conectores de recebimento são criados no transporte de Front-End ou servidor de acesso para cliente. O conector de recebimento de Front End padrão está configurado para aceitar as comunicações de SMTP de todos os intervalos de endereços IP. Além disso, há um conector de recebimento que possa atuar como um proxy de saída para mensagens enviadas para o servidor front-end dos servidores de caixa de correio. Finalmente, há um seguro conector de recebimento configurado para aceitar mensagens criptografadas com a segurança de camada de transporte (TLS). Esses conectores são as seguintes:

  - **FrontEnd padrão \< nome do servidor \>**   Aceita conexões dos remetentes SMTP através da porta 25. Este é o ponto de entrada de mensagens comuns em sua organização.

  - **Frontend de Proxy de saída \< nome do servidor \>**    Aceita as mensagens de um conector de envio de mensagens em um servidor de back-end, com proxy front-end habilitado.

  - **Cliente Frontend \< nome do servidor \>**    Aceita conexões seguras, com Transport Layer Security (TLS) aplicado.

Em uma instalação típica, não há conectores de recebimento adicionais são necessários.

## Tipos de conector de recebimento

O tipo determina as configurações de segurança padrão para cada conector de recebimento.

As configurações de segurança para um conector de recebimento especificarem as permissões que são concedidas aos sessões que se conectam ao conector de recebimento e os mecanismos de autenticação com suporte.

Quando você usar o EAC para configurar um conector de recebimento, o novo conector de recebimento página solicita que você selecione o tipo de conector. Com base na sua seleção, os parâmetros são definidos para se adequar à configuração que você escolheu. Procedimentos específicos contêm mais informações sobre as configurações de tipo de conector de recebimento. Exemplos dos procedimentos a seguir são [Criar um conector de recebimento para receber email da Internet](create-a-receive-connector-to-receive-email-from-the-internet-exchange-2013-help.md) e [Criar um conector de recebimento seguro para receber email de um parceiro](create-a-secure-receive-connector-to-receive-email-from-a-partner-exchange-2013-help.md).

## Grupos de permissões de conector de recebimento

Um grupo de permissão é um conjunto predefinido de permissões de entidades de segurança foram concedidos a conhecido e atribuído a um conector de recebimento. Entidades de segurança incluem usuários, computadores e grupos de segurança. O uso de grupos de permissão simplifica a configuração das permissões nos conectores de recebimento. A propriedade **PermissionGroups** define os grupos ou funções que podem enviar mensagens para o conector de recebimento e as permissões que são atribuídas a esses grupos.

Grupos de permissões incluem *Anonymous*, *ExchangeUsers*, *ExchangeServers*, *ExchangeLegacyServers*e *Partner*.

## Especificações de tipo de conector de recebimento

O tipo determina os grupos de permissão padrão que estão atribuídos ao conector de recebimento e os mecanismos de autenticação padrão que estão disponíveis para autenticação de sessão. A lista a seguir descreve os tipos disponíveis:

1.  **Cliente**   Geralmente usado para conectar aos clientes que não usam o Microsoft Office Outlook. Ele pode usar a autenticação TLS.

2.  **Sinalizador**   Geralmente usado em um cenário entre florestas ou em um cenário em que a sua organização recebe mensagens de um agente de transferência de mensagem SMTP.

3.  **Interno**   Usado para comunicação entre servidores que executam o serviço de transporte ou entre os servidores de caixa de correio executando o serviço de transporte e os agentes de transferência de terceiros.

4.  **Internet**   Usado para receber email SMTP da Internet.

5.  **Parceiro**   Use este tipo quando você deseja configurar a comunicação segura com um parceiro.

Cada tipo é apropriado para um cenário de conexão específica. Selecione o tipo que tenha as configurações padrão mais aplicáveis à configuração que você deseja. Você pode modificar permissões usando os cmdlets **Add-ADPermission** e **Remove-ADPermission** . Para obter mais informações, consulte os tópicos a seguir:

  - [Add-ADPermission](https://technet.microsoft.com/pt-br/library/bb124403\(v=exchg.150\))

  - [Remove-ADPermission](https://technet.microsoft.com/pt-br/library/aa996048\(v=exchg.150\))

## Permissões de conector de recebimento

Conector permissões são atribuídas a entidades de segurança quando você especifica os grupos de permissão para o conector de recebimento. Quando uma entidade de segurança estabelece uma sessão com um conector de recebimento, as permissões de conector de recebimento determinam se a sessão será aceita e como as mensagens recebidas são processadas. Você pode definir permissões de conector de recebimento usando o EAC ou usando o parâmetro *PermissionGroups* com o cmdlet **Set-ReceiveConnector** no Shell. Para modificar as permissões padrão para um conector de recebimento, você também pode usar o cmdlet **Add-ADPermission** .

[Permissões de conector de recebimento](receive-connector-permissions-exchange-2013-help.md) contém uma tabela que lista os tipos de entidades de segurança e permissões de segurança em detalhes.

## Configurações de autenticação do conector de recebimento

No EAC, você pode usar as configurações de autenticação de um conector de recebimento para especificar os mecanismos de autenticação suportados pelo servidor de transporte de Exchange 2013. No Shell, você pode usar o parâmetro *AuthMechanisms* para especificar os mecanismos de autenticação com suporte. Você pode configurar mais de um mecanismo de autenticação para um conector de recebimento. Para obter mais informações, consulte [Mecanismos de autenticação do conector de recebimento](receive-connector-authentication-mechanisms-exchange-2013-help.md).

## Novos recursos de conector de recebimento no Exchange 2013

Os seguintes recursos foram adicionados no Exchange 2013:

  - Com o *TlsCertificateName* o parâmetro, você pode especificar a autoridade de certificação (CA) local emitiu o certificado a ser usado para email seguro. Isso ajuda a reduzir o risco de certificados fraudulentos.

  - O parâmetro *TransportRole* designa a função de servidor associada a esse conector. Normalmente, ele é usado para especificar a função de servidor ao hospedar diversas funções de servidor em um único computador.

Consulte [New-ReceiveConnector](https://technet.microsoft.com/pt-br/library/bb125139\(v=exchg.150\)) para obter mais informações sobre esses parâmetros e outros parâmetros para conectores de recebimento.

