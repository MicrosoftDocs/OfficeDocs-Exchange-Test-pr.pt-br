---
title: 'Gerenciar um gateway IP de UM: Exchange 2013 Help'
TOCTitle: Gerenciar um gateway IP de UM
ms:assetid: 387e540f-8c59-42d2-a423-99fcf97e00aa
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Aa997283(v=EXCHG.150)
ms:contentKeyID: 50485342
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
f1_keywords:
- Microsoft.Exchange.Management.SnapIn.Esm.Servers.UnifiedMessaging.UMIPGatewayGeneralPropertyPageControl
ms.translationtype: MT
---

# Gerenciar um gateway IP de UM

 

_**Aplica-se a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Tópico modificado em:** 2013-02-21_

Depois de criar um gateway IP da Unificação de Mensagens (UM), é possível visualizar ou definir diversas configurações. Por exemplo, é possível configurar o endereço IP ou um nome de domínio totalmente qualificado (FQDN), definir as configurações das chamadas de saída e habilitar ou desabilitar o Indicador de Mensagens em Espera.

Para tarefas de gerenciamento adicionais relacionadas a gateways IP da UM, consulte [Procedimentos de gateway IP de Unificação de mensagens](um-ip-gateway-procedures-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: 5 minutos.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Gateways IP da UM" no tópico [Permissões de mensagens unificadas](unified-messaging-permissions-exchange-2013-help.md).

  - Antes de executar esses procedimentos, confirme se um plano de discagem de UM foi criado. Para obter etapas detalhadas, consulte [Criar um plano de discagem de UM](create-a-um-dial-plan-exchange-2013-help.md).

  - Antes de executar esses procedimentos, verifique se um gateway IP da UM foi criado. Para obter etapas detalhadas, consulte [Criar um gateway IP de UM](create-a-um-ip-gateway-exchange-2013-help.md).

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>..



## O que você deseja fazer?

## Usar o EAC para visualizar ou configurar as propriedades do gateway IP da UM

1.  No EAC, navegue até **Unificação de Mensagens** \> **Gateways IP da UM**. No modo de exibição de lista, selecione o gateway IP da UM que você deseja gerenciar e clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").

2.  
    
    Use a página **Gateway IP da UM** para visualizar e definir as configurações do gateway IP da UM. Também é possível visualizar ou definir as seguintes configurações:
    
      - **Status**   Esse campo apenas para exibição mostra o status do gateway IP da UM.
    
      - **Nome**   Use essa caixa para especificar um nome exclusivo para o gateway IP de UM. Esse é um nome de exibição que aparece no EAC. Se você precisar alterar o nome de exibição do gateway IP de UM depois da sua criação, primeiro exclua o gateway IP de UM existente e depois crie outro com o nome apropriado. O nome do gateway IP de UM é necessário, mas é usado apenas para fins de exibição. Como sua organização pode usar vários gateways IP de UM, recomendamos que você use nomes significativos para eles. O comprimento máximo de um nome de gateway IP de UM é 64 caracteres e pode incluir espaços.
    
      - **Endereço**   Você pode configurar um gateway IP de UM com um endereço IP ou um FQDN (nome de domínio totalmente qualificado). Use essa caixa para especificar o endereço IP ou FQDN configurado no gateway VoIP, PBX habilitado para SIP, PBX IP ou SBC.
        
        Você pode inserir caracteres alfabéticos e numéricos nessa caixa. Há suporte para FQDNs, endereços IPv6 e endereços IPv4. Se você usar um FQDN, você também deve se certificar que você configurou corretamente um registro de host DNS para o gateway VoIP, de modo que o nome de host seja resolvido corretamente para um endereço IP. Se você utilizar um FQDN em vez de um endereço IP, e a configuração DNS para o gateway IP da UM for alterada, você deverá desabilitar e, em seguida, habilitar o gateway IP de UM para certificar-se de que as informações de configuração do gateway IP da UM estejam atualizadas corretamente.
        
        Se você quiser usar Segurança de Camada de Transporte mútua (TLS mútua) entre um gateway de IP da UM e um plano de discagem funcionando no modo SIP seguro ou Seguro, você deverá configurar o gateway IP da UM com um FQDN. Você também deve configurá-lo para escutar na porta 5061 e verificar se gateways IP ou IP PBXs também foram configurados para escutar solicitações de TLS mútuo na porta 5061. Para configurar um gateway IP da UM, execute o seguinte comando: `Set-UMIPGateway -identity MyUMIPGateway -Port 5061`.
    
      - **Permitir chamadas de saída através deste gateway IP da UM**   Marque essa caixa de seleção para permitir que o gateway IP da UM aceite e processe chamadas de saída. Essa configuração não afeta transferências de chamadas ou chamadas de entrada de um gateway VoIP.
        
        Por padrão, quando o gateway IP da UM é criado, essa configuração é habilitada. Se você desabilitar essa configuração, usuários associados ao plano de discagem não poderão fazer chamadas de saída pelo gateway VoIP, PBX IP ou SBC definidos no campo **Endereço**.
    
      - **Permitir indicador de mensagens em espera**   Marque essa caixa de seleção para permitir que as notificações de caixa postal sejam enviadas aos usuários das chamadas executadas pelo gateway IP da UM. Essa configuração permite que o gateway IP da UM receba e envie mensagens SIP NOTIFY para os usuários. Essa configuração está habilitada por padrão e permite que notificações de mensagens em espera sejam enviadas aos usuários.
        
        O Indicador de Mensagens em Espera pode se referir a qualquer mecanismo que indique a existência de uma mensagem ou não ouvida. A indicação da chegada de uma nova mensagem de voz pode ser encontrada na Caixa de Entrada de clientes como o Outlook e o Outlook Web App. Ela pode ser entregue na forma de SMS (Short Messaging Service) ou mensagem de texto enviada a um telefone celular registrado, na forma de chamada de saída feita a partir de um servidor de Unificação de Mensagens do para um número pré-configurado a fim de reproduzir um novo item ou na forma de uma luz acesa no telefone de mesa de um usuário.

## Usar o Shell para configurar as propriedades do gateway IP da UM

Este exemplo modifica o endereço IP de um gateway IP da UM chamado `MyUMIPGateway`.

    Set-UMIPGateway -Identity MyUMIPGateway -Address 10.10.10.1

Este exemplo impede que o gateway IP da UM chamado `MyUMIPGateway` aceite chamadas de entrada e impede chamadas de saída.

    Set-UMIPGateway -Identity MyUMIPGateway -Address voipgateway.contoso.com -Status 2 -OutcallsAllowed $false

Este exemplo habilita o gateway IP da UM para funcionar como um simulador de gateway VoIP e pode ser usado com o cmdlet **Test-UMConnectivity**.

    Set-UMIPGateway -Identity MyUMIPGateway -Simulator $true


> [!IMPORTANT]
> Há um período de latência até que todas as alterações nas configurações de um gateway IP da UM sejam replicadas a todos os servidores de Unificação de Mensagens que estejam no mesmo plano de discagem de UM como o gateway IP da UM.



Este exemplo impede que o gateway IP da UM com o nome `MyUMIPGateway` aceite chamadas de entrada e impeça chamadas de saída, define um endereço IPv6 e permite que o gateway IP da UM use endereços IPv4 e IPv6.

    Set-UMIPGateway -Identity MyUMIPGateway -Address fe80::39bd:88f7:6969:d223%11 -IPAddressFamily Any -Status Disabled -OutcallsAllowed $false

## Usar o Shell para visualizar as propriedades do gateway IP da UM

Este exemplo exibe uma lista formatada de todos os gateways IP da UM na floresta do Active Directory.

    Get-UMIPGateway |Format-List

Este exemplo exibe as propriedades de um gateway IP da UM chamado `MyUMIPGateway`.

    Get-UMIPGateway -Identity MyUMIPGateway

Este exemplo exibe todos os gateways IP da UM, inclusive os simuladores de gateway VoIP da floresta do Active Directory.

    Get-UMIPGateway -IncludeSimulator $true

