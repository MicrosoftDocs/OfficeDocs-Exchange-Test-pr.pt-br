---
title: 'Implantar certificados para Unificação de mensagens: Exchange 2013 Help'
TOCTitle: Implantar certificados para Unificação de mensagens
ms:assetid: 95658f6f-eac2-4674-90e7-f2d3f25c5242
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Ee681661(v=EXCHG.150)
ms:contentKeyID: 52058858
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Implantar certificados para Unificação de mensagens

 

_**Aplica-se a:** Exchange Server 2013, Exchange Server 2016_

_**Tópico modificado em:** 2013-04-29_

Você pode usar mutual Transport Layer Security (TLS mútuo) para habilitar a Unificação de mensagens (UM) para criptografar dados enviados entre seus servidores do Microsoft Exchange 2013 e gateways VoIP, IP PBXs, controladores de borda de sessão (SBCs) e o Microsoft Lync Server. Certificados vinculam a identidade do proprietário do certificado a um par de chaves eletrônicas (públicos e particulares) que são usados para criptografar e assinar digitalmente o informações.

Se você estiver usando o SIP protegido ou planos de discagem protegido em sua organização do Exchange 2010, você precisará importar os certificados que foram usadas para seus servidores de acesso para cliente do Exchange 2013 executando o serviço do Microsoft Exchange roteador de chamada UM e os servidores de caixa de correio executando o serviço UM do Microsoft Exchange. Você pode usar um dos seguintes certificados para os serviços de Unificação de mensagens e o roteador de chamada UM:

  - Um certificado autoassinado (do Exchange)

  - Um certificado interno de infraestrutura de chave pública (PKI)

  - Um certificado comercial de terceiros

Por padrão, quando você instala a Unificação de mensagens, um certificado autoassinado é criado e usado. Este certificado auto-assinado pode ser usado com gateways VoIP, PBXs IP e SBCs, mas não quando você estiver integrando a Unificação de mensagens com o Lync Server. Se você estiver implantando certificados a ser usado com o Lync Server, você precisará usar o Assistente de certificado do Exchange ou o cmdlet **New-ExchangeCertificate** para obter um certificado emitido por uma interno ou PKI autoridade de certificação (CA) ou um terceiro ou comercial de compra do certificado que é mutuamente confiável Unified Messaging e Lync Server.

## Implantar certificados para gateways VoIP, PBXs IP e SBCs

Para habilitar a Unificação de mensagens criptografar dados enviados entre gateways VoIP, PBXs IP e SBCs, você precisa fazer o seguinte:

  - Usar o certificado autoassinado de Unificação de mensagens, crie uma nova solicitação de certificado do Exchange e obter um certificado PKI interno ou adquirir um certificado comercial de terceiros que você pode usar para TLS mútuo entre UM e gateways VoIP, PBXs IP e SBCs.

  - Importe o certificado que será usado na caixa de correio e acesso para cliente de todos os servidores em sua organização.

  - Habilite o certificado a ser usado pelos serviços de Unificação de mensagens.

  - Importe o certificado nos seus gateways VoIP, PBXs IP e SBCs.

  - Configure o plano de discagem de UM como SIP protegido ou protegido.

  - Configure o modo de inicialização de Unificação de mensagens nos servidores de acesso para cliente e caixa de correio em sua organização.

  - Crie gateways IP de UM necessários com um nome de domínio totalmente qualificado (FQDN).

  - Configure a porta de escuta nos gateways IP de UM para usar a porta 5061 para TLS.

  - Reinicie o serviço de roteador de Unificação de chamada em todos os servidores de acesso para cliente e reinicie o serviço de Unificação de mensagens do Microsoft Exchange em todos os servidores de caixa de correio.

## Implantar certificados para o Lync Server

Para criptografar dados enviados entre UM e o Lync Server, você precisará fazer o seguinte:

  - Criar uma nova solicitação de certificado do Exchange e obter um certificado PKI interno ou adquirir um certificado comercial de terceiros. O certificado deve ser confiável mutuamente pela Unificação de mensagens e o Lync Server.

  - Importe o certificado que será usado na caixa de correio e acesso para cliente de todos os servidores em sua organização.

  - Habilite o certificado a ser usado pelos serviços de Unificação de mensagens.

  - Importe o certificado nos computadores executando o Lync Server.

  - Configure o plano de discagem UM de URI SIP como SIP protegido ou protegido.

  - Configure o modo de inicialização de Unificação de mensagens nos servidores de acesso para cliente e caixa de correio em sua organização.

  - Execute OcsUmUtil.exe de um computador do Lync Server.

  - Reinicie o serviço de roteador de Unificação de chamada em todos os servidores de acesso para cliente e reinicie o serviço de Unificação de mensagens do Microsoft Exchange em todos os servidores de caixa de correio em sua organização. Para obter detalhes, consulte [Procedimentos de serviços de Unificação de mensagens](um-services-procedures-exchange-2013-help.md).

  - Reinicie o serviço de front-end do Lync Server em todos os servidores do Lync que fazem parte de um pool de Front End do Enterprise Edition ou Standard Edition servidores Front-End de reiniciar. Você pode usar o cmdlet **Stop-CsWindowsService** para interromper os serviços do Lync Server e o cmdlet **Start-CsWindowsService** para iniciar os serviços do Lync Server.
    
    Os cmdlets **Start-CsWindowsService** e **Stop-CsWindowsService** são semelhantes aos de cmdlets do Windows PowerShell genérico **Start-Service** e **Stop-Service**. Se desejar, você pode usar os cmdlets **Start-Service** ou **Stop-Service** para iniciar e parar um serviço do Lync Server. No entanto, os cmdlets de**Stop-CsWindowsServiceStart-CsWindowsService**incluir um parâmetro *ComputerName* que torna fácil parar e iniciar um serviço do Lync Server em um computador remoto. Para fazer isso, você deve incluir o parâmetro *ComputerName* seguido do nome de domínio totalmente qualificado (FQDN) do computador remoto. Os cmdlets **Start-Service** e **Stop-Service** não tem um parâmetro comparável.
    

    > [!NOTE]
    > Para integrar completamente a Unificação de mensagens e o Lync Server, você também deve executar o script ExchUCUtil. Ps1 em qualquer acesso para cliente ou o servidor de caixa de correio em sua organização


