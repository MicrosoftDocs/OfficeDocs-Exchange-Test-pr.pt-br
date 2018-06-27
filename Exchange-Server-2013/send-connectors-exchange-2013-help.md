---
title: 'Conectores de envio: Exchange 2013 Help'
TOCTitle: Conectores de envio
ms:assetid: 6aa19a12-c7b2-4eac-a8dc-9a4d26919ac5
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Aa998662(v=EXCHG.150)
ms:contentKeyID: 50485880
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Conectores de envio

 

_**Aplica-se a:**Exchange Server 2013_

_**Tópico modificado em:**2012-10-15_

No Microsoft Exchange Server 2013, um conector de Envio controla o fluxo de mensagens de saída para o servidor destinatário. Eles são configurados em servidores de Caixa de Correio com o serviço de Transporte. Mais comumente, você configura um conector de Envio para enviar emails de saída para um host inteligente ou diretamente para o destinatário, usando DNS.

Os servidores de Caixa de Correio do Exchange 2013 com o serviço de Transporte exigem que os conectores de Envio entreguem as mensagens no próximo salto do caminho para seus destinos. Os conectores de envio criados nos servidores de Caixa de Correio são armazenados no Active Directory e estão disponíveis a todos os servidores de Caixa de Correio com o serviço de Transporte na organização.


> [!IMPORTANT]
> Quando você implanta o Exchange 2013, o fluxo de email de saída não pode acontecer até que você configure um conector de Envio para rotear emails de saída para a Internet. Para mais informações, consulte <A href="create-a-send-connector-for-email-sent-to-the-internet-exchange-2013-help.md">Criar um conector de envio de email enviado para a Internet</A>.



## Selecionar o Tipo de um conector de Envio

Normalmente, você cria um conector de Envio na seção **Fluxo de emails** do Centro de Administração do Exchange (EAC). Quando você cria um novo conector de Envio, você escolher um **Tipo** apropriado para o seu cenário de conexão. O tipo determina os conjuntos padrão de permissões que são atribuídos no conector e concede essas permissões às entidades de segurança confiáveis. Entidades de segurança incluem usuários, computadores e grupos de segurança.

Procedimentos que explicam seleções de **Tipo** específicas incluem [Criar um conector de envio para rotear emails de saída por meio de um host inteligente](create-a-send-connector-to-route-outbound-email-through-a-smart-host-exchange-2013-help.md) e [Criar um conector de envio para enviar email para um parceiro, com Transport Layer Security (TLS) aplicada](create-a-send-connector-to-send-email-to-a-partner-with-transport-layer-security-tls-applied-exchange-2013-help.md).

Se você preferir usar o Shell de Gerenciamento do Exchange ao EAC, você poderá criar um conector de Envio e especificar um tipo, usando o cmdlet [New-SendConnector](https://technet.microsoft.com/pt-br/library/aa998936\(v=exchg.150\)).

## Novos recursos do conector de Envio no Exchange 2013

Com o relacionamento entre o serviço de Transporte de Front End nos servidores de Acesso para Cliente e o serviço de Transporte em servidores de Caixa de Correio no Exchange 2013, vem um novo comportamento para conectores de Envio. Primeiramente, você pode enviar um conector de Envio, no serviço de Transporte de um servidor de Caixa de correio, para rotear um email de saída através de um servidor de transporte de Front End no site do Active Directory local, através do parâmetro *FrontEndProxyEnabled* do cmdlet [Set-SendConnector](https://technet.microsoft.com/pt-br/library/aa998294\(v=exchg.150\)), consolidando, assim, como os emails são roteados do serviço de Transporte. [Roteamento de mensagens](mail-routing-exchange-2013-help.md) contém mais informações sobre serviços de transporte, comportamento de roteamento e destinos no Exchange 2013. [Fluxo de mensagens](mail-flow-exchange-2013-help.md) oferece uma visão geral do pipeline de transporte e descrições de cada serviço de transporte.

O parâmetro *IsCoexistenceConnector* está sendo preterido. Na maioria dos casos, quando você quiser configurar um ambiente híbrido, em que uma parte das suas caixas de correio estão hospedadas local e uma parte está hospedada na nuvem, recomendamos que você use o Assistente de Configuração Híbrida.

*LinkedReceiveConnector* foi preterido. Esse parâmetro foi usado para criar conectores que poderiam rotear mensagens para um serviço antispam de terceiros, por exemplo. Agora, na maioria dos casos, você roteia emails do seu serviço antispam, através do seu registro MX e o comportamento de conector vinculado não é necessário.

O tamanho de mensagem máximo padrão, especificado pelo parâmetro *MaxMessageSize*, foi aumentado de 10 MB para 25 MB. [Set-SendConnector](https://technet.microsoft.com/pt-br/library/aa998294\(v=exchg.150\)) contém mais informações sobre como definir parâmetros em um conector de Envio.

*TlsCertificateName* foi adicionado. Ele é usado para autenticar o certificado local, para ser usado para conexões de saída e minimizar o risco de certificados fraudulentos.

