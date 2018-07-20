---
title: 'Configurar o endereço do postmaster externo: Exchange 2013 Help'
TOCTitle: Configurar o endereço do postmaster externo
ms:assetid: 6b0c8675-3238-462d-8973-b52305fb90d2
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Bb430765(v=EXCHG.150)
ms:contentKeyID: 52058825
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configurar o endereço do postmaster externo

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2016-12-09_

O endereço postmaster externo é usado como o remetente para notificações e mensagens geradas pelo sistema enviadas para remetentes de mensagem existentes fora da sua organização Exchange Server 2013 da Microsoft. Um remetente externo é qualquer remetente que possui um endereço de email em um domínio que não está configurado como um domínio aceito na sua organização.

Por padrão, o valor do endereço postmaster externo é definido como vazio. Este valor padrão resulta no seguinte comportamento na sua organização do Exchange:

  - O endereço postmaster externo é postmaster@\<*Domínio aceito por padrão*\> para todos os servidores de Caixa de Correio e servidores de Transporte de Borda inscritos.

  - O endereço postmaster externo é postmaster@\<*Edge Transport server FQDN*\> para todos os servidores de Transporte de Borda não inscritos.

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: 15 minutos

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada de "Configuração de transporte" no tópico [Permissões de fluxo de email](mail-flow-permissions-exchange-2013-help.md) .

  - Quando você configura um endereço postmaster externo, este valor é aplicado a todos os servidores de Caixa de Correiro Exchange 2013 e servidores de Transporte de Concentrador Exchange 2010 na sua organização do Exchange. Entretanto, este valor não é replicado para os servidores de Transporte de Borda. Se você especificar um valor personalizado para o endereço postmaster externo, você precisa configurar manualmente o valor do endereço postmaster externo em qualquer servidor de Transporte de Borda.

  - Se você tiver quaisquer servidores de transporte de Hub Exchange 2007 ou servidores de transporte de borda em sua organização, você precisará configurar o endereço do postmaster externo personalizadas em cada um desses servidores usando o cmdlet **Set-TransportServer** . Para obter mais informações, consulte [Gerenciando o endereço de Postmaster externo](https://go.microsoft.com/fwlink/?linkid=279922).

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

## O que você deseja fazer?

## Use o EAC para configurar o endereço postmaster externo

1.  No EAC, vá em **Fluxo de email** \> **Receber conectores** \> **Mais opções**![Ícone Mais opções](images/JJ150550.5381819e-3b21-4873-8714-e9b956290b28(EXCHG.150).gif "Ícone Mais opções") \> **Configurações de transporte da organização** \> guia **Entrega** .

2.  No campo **Endereço postmaster externo** , insira o endereço de email SMTP, por exemplo, `postmaster@contoso.com`. Se você deseja retornar o endereço postmaster externo para o valor padrão, exclua qualquer valor existente para que o campo fique vazio.

3.  Ao finalizar, clique em **Salvar**.

## Use o Shell para configurar o endereço postmaster externo

Para configurar o endereço postmaster externo, use a seguinte sintaxe.

    Set-TransportConfig -ExternalPostmasterAddress <postmaster address>

Por exemplo, para definir o valor do endereço postmaster externo para `postmaster@contoso.com`, execute o seguinte comando

    Set-TransportConfig -ExternalPostmasterAddress postmaster@contoso.com

Para retornar o endereço postmaster externo para o valor original, execute o seguinte comando:

    Set-TransportConfig -ExternalPostmasterAddress $null

## Como saber se funcionou?

Para verificar se você configurou com sucesso o endereço postmaster externo, faça o seguinte:

1.  Execute o seguinte comando no servidor da Caixa de Correio para verificar o valor do endereço postmaster externo:
    
        Get-TransportConfig | Format-List ExternalPostmasterAddress

2.  A partir de uma conta de endereço externo, envie uma mensagem para sua organização do Exchange que irá gerar uma notificação de status de entrega (DSN). Por exemplo, você pode configurar uma regra de transporte para enviar uma notificação de não entrega (NDR) para uma mensagem daquele remetente que contenha palavras-chave específicas. Verifique se o endereço de email do remetente no DSN corresponde ao valor que você especificou.

Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), ou [Proteção do Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=285351).

