---
title: 'Criar um gateway IP de UM: Exchange 2013 Help'
TOCTitle: Criar um gateway IP de UM
ms:assetid: 542d6b50-147b-4cec-b54d-61c7b8fc0fc7
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Aa998045(v=EXCHG.150)
ms:contentKeyID: 50485611
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
f1_keywords:
- Microsoft.Exchange.Management.SnapIn.Esm.Servers.UnifiedMessaging.CreateUMIPGatewayWizardForm.CreateUMIPGatewayWizardPage
ms.translationtype: MT
---

# Criar um gateway IP de UM

 

_**Aplica-se a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Tópico modificado em:** 2013-04-16_

Ao criar um gateway IP de UM (Unificação de Mensagens), você permite que servidores do Exchange se conectem a um novo gateway VoIP, a um PBX habilitado para o protocolo SIP e a um PBX IP ou a um SBC (Controlador de Borda de Sessão). Imediatamente após criar um gateway IP do UM, você deve criar um novo grupo de busca do UM e depois associar o grupo de busca do UM com o gateway IP do UM. Você pode associar o gateway IP do UM a um ou mais planos de discagem do UM criando um ou mais grupos de busca do UM.

Para tarefas de gerenciamento adicionais relacionadas a gateways IP da UM, consulte [Procedimentos de gateway IP de Unificação de mensagens](um-ip-gateway-procedures-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: 3 minutos.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Gateways IP da UM" no tópico [Permissões de mensagens unificadas](unified-messaging-permissions-exchange-2013-help.md).

  - Antes de executar esses procedimentos, confirme se um plano de discagem da UM foi criado. Para obter etapas detalhadas, consulte [Criar um plano de discagem de UM](create-a-um-dial-plan-exchange-2013-help.md).

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>..



## O que você deseja fazer?

## Usar o EAC para criar um gateway IP da UM

1.  
    
    No EAC, navegue até **Unificação de Mensagens** \> **Gateways IP da UM** e clique em **Novo**![Ícone Adicionar](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Ícone Adicionar").

2.  Na página do **Novo gateway IP da UM**, insira as seguintes informações:
    
      - **Nome**   Use essa caixa para especificar um nome exclusivo para o gateway IP de UM. Esse é um nome de exibição que aparece no EAC. Se você precisar alterar o nome de exibição do gateway IP da UM depois de sua criação, primeiro exclua o gateway IP da UM existente e depois crie outro com o nome desejado. O nome do gateway IP de UM é necessário, mas é usado apenas para fins de exibição. Como sua organização pode usar vários gateways IP de UM, recomendamos que você use nomes significativos para eles. O comprimento máximo de um nome de gateway IP de UM é 64 caracteres e pode incluir espaços. Entretanto, não pode incluir nenhum dos seguintes caracteres: " / \\ \[ \] : ; | = , + \* ? \< \>.
    
      - **Endereço**   Você pode configurar um gateway IP da UM com um endereço IP ou um nome de domínio totalmente qualificado (FQDN). Use essa caixa para especificar o endereço IP configurado no gateway VoIP, PBX habilitado para SIP, PBX IP, SBC ou FQDN. Essa caixa aceita somente FQDNs válidos e formatados corretamente.
        
        Você pode inserir caracteres alfabéticos e numéricos nessa caixa. Há suporte para FQDNs, endereços IPv6 e endereços IPv4. Se você quiser usar Segurança de Camada de Transporte mútua (TLS mútua) entre um gateway de IP da UM e um plano de discagem funcionando no modo SIP seguro ou Seguro, você deverá configurar o gateway IP da UM com um FQDN. Você também deve configurá-lo para escutar na porta 5061 e verificar se gateways VoIP ou PBXs IP também foram configurados para escutar solicitações de TLS mútuas na porta 5061. Para configurar um gateway IP de UM, execute o seguinte comando: `Set-UMIPGateway -identity MyUMIPGateway -Port 5061`.
        
        Se você usar um FQDN, você também deve se certificar que configurou corretamente um registro de host DNS para o gateway VoIP, de modo que o nome de host seja resolvido corretamente para um endereço IP. Se você utilizar um FQDN em vez de um endereço IP, e a configuração DNS para o gateway IP de UM for alterada, será necessário desabilitar e, em seguida, habilitar o gateway IP de UM para garantir que as informações de configuração do gateway IP de UM sejam atualizadas corretamente.
    
      - **Plano de discagem da UM**   Clique no botão **Procurar** para selecionar o plano de discagem da UM que deseja associar ao gateway IP da UM. Quando você seleciona um plano de discagem de UM para associar a um gateway IP de UM, um número coletivo padrão de UM é também criado e associado ao plano de discagem de UM selecionado. Se você não selecionar um plano de discagem de UM, deverá criar manualmente um grupo de busca de UM e depois associar esse grupo de busca de UM ao gateway IP de UM a ser criado.

3.  
    
    Clique em **Salvar**.

## Usar o Shell para criar um gateway IP de UM

Este exemplo cria um gateway IP da UM chamado `MyUMIPGateway` que permite que os servidores do Exchange comecem a aceitar chamadas de um gateway VoIP, um PBX habilitado para protocolo SIP, um PBX IP ou um SBC que tenha um endereço IP de 10.10.10.1.

    New-UMIPGateway -Name MyUMIPGateway -Address 10.10.10.1

Este exemplo cria um gateway IP da UM chamado `MyUMIPGateway` que permite que os servidores do Exchange comecem a aceitar chamadas de um gateway VoIP, um PBX habilitado para protocolo SIP, um PBX IP ou um SBC que tenha um FQDN de MyUMIPGateway.contoso.com e que escute na porta 5061.

    New-UMIPGateway -Name MyUMIPGateway -Address "MyUMIPGateway.contoso.com" -Port 5061

Este exemplo cria um gateway IP da UM chamado `MyUMIPGateway` e impede que o gateway IP da UM aceite ou faça chamadas, define um endereço IPv6 e permite que o gateway IP da UM use endereços IPv4 e IPv6.

    New-UMIPGateway -Identity MyUMIPGateway -Address fe80::39bd:88f7:6969:d223%11 -IPAddressFamily Any -Status Disabled -OutcallsAllowed $false

