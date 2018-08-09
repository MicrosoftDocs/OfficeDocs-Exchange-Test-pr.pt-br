---
title: 'Cenário: configurar o Exchange para suporte a controladores de otimização WAN'
TOCTitle: 'Cenário: Configurar o Exchange para oferecer suporte a controladores de otimização de WAN'
ms:assetid: 1f407698-0b71-45a3-867a-640ccf7351da
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Ee633456(v=EXCHG.150)
ms:contentKeyID: 52058802
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Cenário: Configurar o Exchange para oferecer suporte a controladores de otimização de WAN

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2012-09-28_

No Microsoft Exchange Server 2013, a criptografia TLS (Transport Layer Security) é obrigatória para toda comunicação SMTP no serviço Transporte entre os servidores de Caixa de Correio. Isso aumenta a segurança geral da comunicação do serviço Transporte entre os servidores de Caixa de Correio. No entanto, em determinadas topologias nas quais os dispositivos WOC (WAN Optimization Controller) são usados, a criptografia TLS do tráfego SMTP pode ser indesejada. É possível desabilitar o TLS para a comunicação do serviço Transporte entre servidores de Caixa de Correio para esses cenários específicos.

Considere a topologia mostrada na figura a seguir. Presume-se nesta topologia de quatro sites que os dois sites do escritório central e do Branch Office 2 estejam bem conectados, enquanto a conexão entre o Central Office Site 1 e o Branch Office 1 se dá por um link WAN. A empresa instalou dispositivos WOC nesse link para compactar e otimizar o tráfego pela WAN.

**Topologia de rede de exemplo com dispositivos WOC**

![Topologia de exemplo com otimizadores WAN](images/Ee633456.52876869-52f1-4c0f-85b2-7a850643e8a1(EXCHG.150).gif "Topologia de exemplo com otimizadores WAN")

Nessa topologia, como o Exchange 2013 usa a criptografia TLS para a comunicação entre os servidores de Caixa de Correio, o tráfego SMTP que passa pelo link WAN não pode ser compactado. O ideal é que todo tráfego SMTP que passa pelo link WAN deve ser SMTP sem criptografia, retendo a segurança do TLS dentro de sites bem conectados. O Exchange 2013 proporciona a opção de desabilitar a criptografia TLS para o tráfego entre sites por meio da configuração dos Conectores de recebimento. Com esse recurso no Exchange 2013, é possível configurar uma exceção para o tráfego SMTP entre o Central Office Site 1 e o Branch Office 1, como mostra a figura a seguir.

**Fluxo de mensagens lógicas preferenciais**

![Fluxo de mensagens lógicas preferenciais](images/Ee633456.e0fe62fa-1bad-4d43-9eaf-205a9b8d07e1(EXCHG.150).gif "Fluxo de mensagens lógicas preferenciais")

A configuração recomendada é limitar o tráfego SMTP sem criptografia apenas às mensagens que passam pelo link WAN. Portanto, a comunicação intra-site do serviço Transporte entre os servidores de Caixa de Correio em todos os sites e a comunicação intersite do serviço Transporte entre os servidores de Caixa de Correio que não envolve o Branch Office 1 devem ser TLS criptografadas.

Para conseguir esse resultado final, você precisa executar as seguintes ações, na ordem especificada, em todo servidor de Caixa de Correio nos sites que contêm os dispositivos WOC (Central Office Site 1 e Branch Office 1 no exemplo de topologia):

1.  Habilite a autenticação rebaixada do Exchange Server.

2.  Crie um Conector de recebimento dedicado para lidar com o tráfego na conexão com dispositivos WOC.
    
    1.  Configure a propriedade do intervalo de endereços IP remoto do Conector de recebimento dedicado para os intervalos de endereço IP dos servidores de Caixa de Correio no site remoto do Active Directory.
    
    2.  Desabilite o TLS no Conector de recebimento dedicado.

Além disso, você precisa executar as seguintes ações para garantir que todo tráfego SMTP pela WAN seja manipulado pelos Conectores de recebimento dedicados que você criou:

  - Configure os sites do Active Directory que participarão na comunicação não TLS como sites de hub a fim de forçar todo fluxo de mensagens pelos Conectores de recebimento dedicados (Central Office Site 1 e Branch Office Site 1 no exemplo de topologia).

  - Verifique se os custos de link de site IP do Active Directory estão configurados de uma maneira que garanta que o caminho de roteamento de menor custo até seu site remoto (Branch Office 1 no exemplo de topologia) passe pelo link de rede com os dispositivos WOC. Atribua um custo específico ao Exchange para os links de site do Active Directory, conforme o necessário.

As seções a seguir fornecem uma visão geral dessas etapas. Para obter instruções detalhadas sobre como configurar sua organização para esse cenário, consulte [Desabilitar o TLS entre sites do Active Directory](disable-tls-between-active-directory-sites-exchange-2013-help.md).

**Sumário**

Downgrade authentication over TLS-disabled connections

Create and configure dedicated Receive connectors

Configure Hub sites

Configure Exchange-specific Active Directory site link costs

## Autenticação rebaixada sobre conexões com TLS desabilitado

A autenticação Kerberos é usada com a criptografia TLS no Exchange. Quando você desabilita o TLS na comunicação do serviço Transporte entre os servidores de Caixa de Correio, é necessário executar outra forma de autenticação. Quando o Exchange 2013 se comunica com outros servidores que estão executando o Exchange e que não suportam **X-ANONYMOUSTLS**, ele volta a usar a autenticação GSSAPI (Generic Security Services Application Programming Interface). Todas as comunicações do serviço Transporte entre os servidores de Caixa de Correio do Exchange 2013 usam **X-ANONYMOUSTLS**. Quando você configura o serviço Transporte em seu servidor de Caixa de Correio para usar a autenticação rebaixada do Exchange Server, na verdade você está habilitando a autenticação GSSAPI para a comunicação do serviço Transporte com outros servidores de Caixa de Correio do Exchange 2013.

Voltar ao início

## Criar e configurar Conectores de recebimento dedicados

É preciso criar Conectores de recebimento que sejam responsáveis única e exclusivamente por lidar com o tráfego sem criptografia TLS. O uso de Conectores de recebimento separados para esse propósito garante que todo o tráfego que não passe pelo link de WAN continue protegido pela criptografia TLS.

Para restringir os Conectores de recebimento dedicados apenas ao tráfego pela WAN, é necessário configurar a propriedade do intervalo de endereços IP remoto. O Exchange sempre usa o conector com o intervalo de endereços IP remoto mais específico. Sendo assim, esses novos conectores têm a preferência sobre o Conector de recebimento padrão configurado para receber mensagens de qualquer lugar.

Voltando à topologia de exemplo, suponha que a sub-rede de classe C 10.0.1.0/24 seja usada para o Central Office Site 1 e que 10.0.2.0/24 seja usada para o Branch Office 1. Para se preparar para desabilitar o TLS entre esses dois sites, é preciso:

1.  Crie um Conector de recebimento chamado WAN em cada servidor de Caixa de Correio no Central Office Site 1 e no Branch Office 1.

2.  Configure o intervalo de endereços IP remoto de 10.0.2.0/24 em cada Conector de recebimento dedicado no Central Office Site 1.

3.  Configure o intervalo de endereços IP remoto de 10.0.1.0/24 em cada Conector de recebimento dedicado no Branch Office 1.

4.  Desabilite o TLS em todos os Conectores de recebimento dedicados.

O resultado final é exibido na figura a seguir (com a propriedade do intervalo de endereços IP remoto dos Conectores de recebimento chamados de WAN exibidos entre parênteses). Apenas um servidor de Caixa de Correio é exibido no Branch Office 1, e o Branch Office 2 é omitido para manter a clareza.

**Configuração do conector de recebimento**

![Configuração do conector de recebimento](images/Ee633456.1821b3db-1f7a-4ae7-afbc-5c99e117f976(EXCHG.150).gif "Configuração do conector de recebimento")

Voltar ao início

## Configurar sites de Hub

Por padrão, um servidor de Caixa de Correio do Exchange 2013 tentará uma conexão direta com o servidor de Caixa de Correio mais próximo ao destino final de uma mensagem específica. No exemplo de topologia, se um usuário no Branch Office 2 enviar uma mensagem para um usuário no Branch Office 1, o servidor de Caixa de Correio no Branch Office 2 se conectará diretamente ao servidor de Caixa de Correio no Branch Office 1 a fim de entregar essa mensagem. Essa conexão será criptografada e, por consequência, indesejável na topologia específica. Para que essas mensagens passem pelos servidores de Caixa de Correio no Central Office Site 1, garantindo assim que não sejam criptografadas enquanto estiverem em trânsito até o link WAN link, o Central Office Site 1 e o Branch Office 1 precisam ser configurados como sites de hub. Resumindo, qualquer site que tenha um servidor de Caixa de Correio com um Conector de recebimento com TLS desabilitado precisa ser configurado como um site de hub, para que você possa forçar os servidores em outros sites a encaminhar o tráfego por esse site. Para obter mais informações, consulte [Configurar definições de roteamento de email do Exchange no Active Directory](configure-exchange-mail-routing-settings-in-active-directory-exchange-2013-help.md).

Voltar ao início

## Configurar custos de link de site do Active Directory específicos ao Exchange

Apenas configurar sites de hub não basta para garantir que todo o tráfego pelo link de WAN não seja criptografado. Isso ocorre porque o Exchange encaminhará mensagens pelos sites de hub somente se o site de hub estiver dentro do caminho de roteamento de menor custo. Por exemplo, vamos supor que os custos do link de site IP para nosso exemplo de topologia sejam configurados no Active Directory conforme mostra a figura a seguir (Central Office Site 2 é omitido para manter a clareza).

**Custos do link de site IP para a topologia de exemplo**

![Custos do link do site IP para topologia de exemplo](images/Ee633456.099deb15-795a-417a-b6aa-925b3bedf8b4(EXCHG.150).gif "Custos do link do site IP para topologia de exemplo")

Nesse caso, o caminho do Branch Office 2 para o Branch Office 1 que passa pelo site de hub tem custo total de 12 (6+6), enquanto o custo do caminho direto é 10. Sendo assim, nenhuma das mensagens do Branch Office 2 para o Branch Office 1 passará pelo Central Office Site 1, e todo o tráfego continuará sendo criptografado com TLS.

Para evitar esse problema, você precisa designar um custo específico do Exchange superior a 12 para o link de site IP entre o Branch Office 2 e o Branch Office 1, conforme mostra a figura a seguir. Isso irá garantir que todas as mensagens passem pelo canal não criptografado entre o Central Office Site 1 e o Branch Office 1.

**Topologia de exemplo configurada com custos de link de site IP específicos do Exchange**

![Topologia de exemplo com custos do Exchange](images/Ee633456.cd036fe0-c37d-479e-a4c1-235e17e90ca7(EXCHG.150).gif "Topologia de exemplo com custos do Exchange")

Para obter mais informações, consulte [Configurar definições de roteamento de email do Exchange no Active Directory](configure-exchange-mail-routing-settings-in-active-directory-exchange-2013-help.md).

Voltar ao início

