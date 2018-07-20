---
title: 'Gerenciar agregação de lista segura: Exchange 2013 Help'
TOCTitle: Gerenciar agregação de lista segura
ms:assetid: 5ac17168-f411-4cb7-ae98-ebefb865b210
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Aa998280(v=EXCHG.150)
ms:contentKeyID: 50485655
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Gerenciar agregação de lista segura

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2015-04-08_

*Agregação de lista segura* refere-se à funcionalidade antispam que é compartilhada do Microsoft Outlook para o Microsoft Exchange Server 2013. Essa funcionalidade coleta dados de Listas de Destinatários Confiáveis, Listas de Remetentes Confiáveis, Listas de Remetentes Bloqueados e dados de contatos que usuários do Outlook configuram; depois esses dados são disponibilizados para os agentes antispam do Exchange. A agregação de lista segura pode ajudar a reduzir as instâncias de falsos positivos na filtragem antispam executada pelos servidores do Exchange em que os agentes antispam estão sendo executados.

## O que você precisa saber antes de começar?

  - Tempo estimado para concluir cada procedimento: 10 minutos

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Seção "Permissões de provisionamento do destinatário" no tópico [Permissões de destinatários](recipients-permissions-exchange-2013-help.md) e "Recursos antispam" no tópico [Permissões antispam e antimalware](anti-spam-and-anti-malware-permissions-exchange-2013-help.md).

  - Você só pode usar o Shell para executar esse procedimento.

  - Por padrão, os recursos antispam não estão habilitados no serviço de Transporte em um servidor de Caixa de Correio. Normalmente, você apenas habilita os recursos antispam em um servidor de Caixa de Correio se sua organização do Exchange não realiza nenhuma ação antes da filtragem antispam antes de aceitar mensagens de entrada. Para saber mais, confira [Habilitar a funcionalidade anti-spam em servidores de caixa de correio](enable-anti-spam-functionality-on-mailbox-servers-exchange-2013-help.md).

  - Preste atenção ao tráfego que pode ser gerado na rede e durante a replicação ao executar o cmdlet **Update-SafeList**. Executar o comando em várias caixas de correio em que listas seguras sejam muito usadas poderá gerar um volume de tráfego significativo. Recomendamos que, se você executar o comando em várias caixas de correio, faça-o em horários que não sejam de pico nem no horário comercial.

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>.



## O que você deseja fazer?

## Usar o Shell para configurar os limites de coleção de lista segura de caixa de correio

É possível configurar a quantidade máxima de remetentes confiáveis e remetentes bloqueados que um usuário pode definir. Por padrão, os usuários podem configurar até 5.000 remetentes confiáveis e 500 remetentes bloqueados.

Para configurar a quantidade máxima de remetentes confiáveis e remetentes bloqueados, execute este comando:

    Set-Mailbox <MailboxIdentity> -MaxSafeSenders <Integer> -MaxBlockedSenders <Integer>

Este exemplo configura a caixa de correio john@contoso.com para ter no máximo 2.000 remetentes confiáveis e 200 remetentes bloqueados.

    Set-Mailbox john@contoso.com -MaxSafeSenders 2000 -MaxBlockedSenders 200

## Como saber se funcionou?

Para verificar se os limites de coleção de lista segura de caixa de correio foram configurados com êxito, faça o seguinte:

1.  Execute o comando a seguir:
    
        Get-Mailbox <Identity> | Format-List Name,Max*Senders

2.  Verifique se os valores exibidos correspondem aos valores que você configurou.

## Usar o Shell para executar o comando Update-Safelist

No Exchange 2013, a agregação de lista segura é feita automaticamente; logo, você não precisa mais agendar ou executar manualmente o cmdlet **Update-Safelist**. Entretanto, você pode querer, ocasionalmente, executar esse cmdlet, para testar a agregação de lista segura.

Este exemplo grava a lista de remetentes confiáveis da caixa de correio john@contoso.com no Active Directory.

    Update-Safelist john@contoso.com -Type SafeSenders

Para informações detalhadas sobre sintaxes e parâmetros, consulte [Update-SafeList](https://technet.microsoft.com/pt-br/library/bb125034\(v=exchg.150\)).

## Como saber se funcionou?

Para verificar se você configurou com êxito a agregação de lista segura, execute estas etapas:

## Etapa 1: Usar o Shell para verificar se o agente Filtro de Conteúdo está habilitado no servidor do Exchange

1.  Execute o comando a seguir:
    
        Get-ContentFilterConfig | Format-List Enabled

2.  Se a saída mostra o parâmetro *Enabled* como `True`, a filtragem de conteúdo está habilitada. Se não for isso, execute o seguinte comando para habilitar a filtragem de conteúdo e o agente Filtro de Conteúdo no servidor do Exchange:
    
        Set-ContentFilterConfig -Enabled $true

## Etapa 2: (Opcional) Usar o Editor ADSI para verificar a replicação dos dados de agregação da lista segura para servidores de Transporte de Borda

Essa etapa será necessária somente se você executar o agente Filtro de Conteúdo em um servidor de Transporte de Borda na rede de perímetro.

Você pode exibir os objetos de usuário na instância do Active Directory Lightweight Directory Services (AD LDS) no servidor de Transporte de Borda para verificar se os dados do conjunto de lista segura estão atualizados para os objetos de usuário e se o serviço do Microsoft Exchange EdgeSync replicou os dados para a instância do AD LDS.

Há três atributos da coleção de lista segura para cada objeto de usuário:

  - **msExchSafeRecipientsHash**   Esse atributo armazena o hash da coleção de Lista de Destinatários Seguros para o usuário.

  - **msExchSafeSendersHash**   Esse atributo armazena o hash da coleção de Lista de Remetentes Seguros para o usuário.

  - **msExchBlockedSendersHash**   Este atributo armazena o hash da coleção da Lista de Remetentes Bloqueados para o usuário.

Se uma cadeia de caracteres hexadecimais, como `0xac 0xbd 0x03 0xca`, estiver presente no atributo, o objeto do usuário terá sido atualizado. Se o atributo tiver um valor `<Not Set>`, o atributo não foi atualizado.

É possível pesquisar e exibir os atributos usando o snap-in Editar do Active Directory Service Interfaces (ADSI) do AD LDS.

## Etapa 3: Enviar uma mensagem de teste para verificar se a agregação de lista segura está funcionando

Para testar se a agregação de lista segura está funcionando, é preciso enviar uma mensagem para si mesmo a partir de um remetente confiável que seria, de outra forma, bloqueado pela filtragem de conteúdo. Se a agregação de lista segura estiver funcionando, a mensagem chegará à Caixa de Entrada.

1.  Localize uma conta de email externa existente para usar, ou crie uma conta de email em um provedor de email gratuito da Web, como o Microsoft Hotmail.

2.  Adicione essa conta à sua lista de Remetentes Confiáveis no Microsoft Outlook.

3.  Use o cmdlet **Update-SafeList** para que a coleção de lista segura dessa caixa de correio seja copiada para o Active Directory.

4.  Opcional: se você estiver executando o agente Filtro de Conteúdo em um servidor de Transporte de Borda na rede de perímetro, execute o cmdlet **Start-EdgeSynchronization** para forçar a replicação do EdgeSync.

5.  Adicione uma palavra específica, como uma frase bloqueada, à configuração da filtragem de conteúdo. Para etapas detalhadas, consulte [Gerenciar filtragem de conteúdo](manage-content-filtering-exchange-2013-help.md).

6.  Na conta externa que você criou na etapa 1, envie uma mensagem que inclui a frase bloqueada configurada na etapa 5 para a caixa de correio do Exchange.
    
    Se a mensagem for entregue com êxito à sua Caixa de Entrada, a agregação de lista segura está funcionando corretamente.

