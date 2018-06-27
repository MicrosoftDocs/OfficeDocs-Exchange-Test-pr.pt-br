---
title: 'Caixa postal para usuários: Exchange 2013 Help'
TOCTitle: Caixa postal para usuários
ms:assetid: 48e1f43b-fb7e-4a52-a2cb-0fb5da6ca65f
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Aa997885(v=EXCHG.150)
ms:contentKeyID: 50485487
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Caixa postal para usuários

 

_**Aplica-se a:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Tópico modificado em:**2013-02-19_

Com a UM (Unificação de Mensagens), os usuários em uma organização do Exchange podem receber todas as suas mensagens de email e voz em uma única caixa de correio. A funcionalidade de Unificação de Mensagens e os recursos de caixa postal aumentam a produtividade dos usuários e permite uma troca de mensagens mais flexível em toda uma organização.

Ao adicionar um usuário à sua organização, você tem a opção de criar uma caixa de correio ou conectar o usuário a uma caixa de correio existente. Depois de uma caixa de correio ser criada para o usuário ou o usuário ser conectado a uma caixa de correio existente, você poderá habilitar a caixa de correio para Unificação de Mensagens, de modo que o usuário possa usar o sistema de caixa postal e os recursos incluídos com a caixa postal. Depois que o usuário estiver habilitado para a Unificação de Mensagens, todas as mensagens de email, de caixa postal e de fax serão entregues à caixa de correio dele. Usando o Microsoft Office Outlook 2007 ou posteriores, o Outlook Web App, um celular habilitado para o Microsoft ExchangeActiveSync ou um telefone comum ou celular, os usuários podem acessar suas mensagens de email e de voz, além das informações de calendário e contatos.

**Sumário**

Propriedades de usuário de caixa postal

A relação entre um usuário de caixa postal e outros componentes de UM

Extension numbers and SIP addresses

Using the EAC to enable a user for UM and voice mail

Using the Shell to enable a user for UM and voice mail

Disabling UM for a user

## Propriedades de usuário de caixa postal

Um usuário deve ter uma caixa de correio antes de poder ser habilitado para Unificação de Mensagens. Mas, por padrão, um usuário que tenha uma caixa de correio não está habilitado para a Unificação de Mensagens. Depois que o usuário for habilitado para UM, você poderá gerenciar, modificar e configurar as propriedades de UM e de caixa postal do usuário. Você pode habilitar um usuário para Unificação de Mensagens usando o EAC ou o Shell. Para detalhes, consulte [Habilitar um usuário para caixa postal](enable-a-user-for-voice-mail-exchange-2013-help.md). Para habilitar vários usuários de UM, use o EAC ou o cmdlet **Enable-UMMailbox** do Shell de Gerenciamento do Exchange.

## A relação entre um usuário de caixa postal e outros componentes de UM

Quando você habilita um usuário para Unificação de Mensagens, ele deve estar associado ou vinculado a uma política de caixa de correio de UM existente e você deve fornecer um número de ramal para o usuário. Você pode associar um usuário a uma política de caixa de correio de UM, com o cmdlet **Enable-UMMailbox** no Shell ou selecionando a política de caixa de correio quando habilitar o usuário para Unificação de Mensagens. Por padrão, quando você cria um plano de discagem de UM, uma nova política de caixa de correio de UM é criada. Essa política pode ser modificada, ou uma outra política pode ser criada e vinculada ao plano de discagem, para determinar que recursos ou configurações serão aplicadas a um usuário ou grupo de usuários.

Uma diretiva de caixa de correio UM contém configurações como restrições de discagem e diretivas de PIN de um usuário. Quando uma diretiva de caixa de correio UM é criada, ele deve ser associado a apenas um plano de discagem de UM. Qualquer servidor do Exchange pode atendimento de chamadas de entrada e fornecer serviços de email para usuários habilitados para Unificação de mensagens que estão vinculados de voz com UM plano de discagem. Depois que o usuário está habilitado para Unificação de mensagens, as configurações de uma política de caixa de correio de Unificação de mensagens são aplicadas ao usuário habilitado para UM.

## Números de ramal e endereços SIP

Quando habilita um usuário para Unificação de Mensagens, você deve definir pelo menos um número de ramal que será usado pela Unificação de Mensagens quando a caixa postal for enviada para a caixa de correio do usuário. Depois de habilitar o usuário para Unificação de Mensagens, você poderá adicionar números de ramal secundários à caixa de correio do usuário, bem como modificá-los ou removê-los, configurando o endereço de proxy da Unificação de Mensagens (endereço proxy EUM) do Exchange na caixa de correio do usuário, ou adicionar ou remover os ramais adicionais ou secundários do usuário no EAC. Você pode remover o número de ramal principal no EAC, removendo o endereço proxy de EUM, mas é recomendável não o remover. Remover o número de ramal principal não permitirá que as chamadas sejam encaminhadas corretamente para a caixa de correio do usuário.


> [!TIP]
> Não há limites para o número de ramais secundários que você pode adicionar para um usuário habilitado para UM, mas pode haver somente um número de ramal principal por usuário.



A caixa de correio de um usuário habilitado para UM pode ser associada a apenas um plano de discagem do UM. Ao usuário habilitado para UM, pode ser atribuído o seguinte:

  - Um único número de ramal principal, endereço SIP ou endereço E.164 em um único plano de discagem.

  - Vários números de ramal secundários, endereços SIP ou E.164, em um único plano de discagem.

  - Vários números de ramal principais, endereços SIP ou endereços E.164 em dois planos de discagem separados.


> [!TIP]
> Cada número de ramal, endereço SIP e número de E.164 deve ser exclusivo dentro de um plano de discagem, e o número de dígitos no plano de discagem será usado para todos os usuários que são vinculados ao plano de discagem.



Por exemplo, um usuário habilitado para UM viaja freqüentemente de Nova York a Tóquio. A caixa de correio do usuário é associada ao plano de discagem de Nova York e um número de ramal único é configurado na caixa de correio do usuário. Um segundo número de ramal é configurado na caixa de correio do usuário para o plano de discagem de Tóquio. Quando os chamadores ligam para qualquer um dos números de ramal e deixam uma mensagem de voz para o usuário, a mensagem de voz será entregue para a mesma caixa de correio habilitada para UM.

Voltar ao início

## Usar o EAC para habilitar um usuário para UM e caixa postal

Depois de criar uma caixa de correio do Exchange para o usuário, você poderá configurar a caixa de correio de UM, usando **Exibir Detalhes**, em **Unificação de Mensagens**, no EAC. Quando você habilitar um usuário, haverá várias configurações que você precisará configurar:

1.  **Endereço SIP** Esse é o endereço SIP do usuário. Você verá essa configuração se o usuário que você estiver habilitando para UM receber uma política de caixa de correio de UM que esteja vinculada a um plano de discagem URI SIP. Os planos de discagem URI SIP são usados quando você integra o Office Communications Server 2007 R2 ou o Microsoft Lync Server. Quando você atribui o usuário a uma política de caixa de correio da UM vinculada a um plano de discagem E.164 ou SIP URI, você deve ainda inserir também um número de ramal para o usuário. O número de ramal principal é usado pelo usuário para acessar o Outlook Voice Access.

2.  **Número do ramal**   Você deve inserir manualmente o número do ramal do usuário que você está habilitando para UM.
    
    Você deve fornecer um número de ramal válido para o usuário e corresponder ao número de dígitos especificado no plano de discagem. Você pode inserir somente caracteres numéricos ou dígitos de 1 a 20. Um número de ramal típico tem de 3 a 7 dígitos e é configurado no plano de discagem ao qual a política de caixa de correio de UM é vinculada e atribuída ao usuário.

3.  **Configurações de PIN para o usuário:**
    
      - **Gerar PIN automaticamente**   Essa configuração gera automaticamente um PIN para o usuário habilitado para UM usar para acessar a caixa postal, através do Outlook Voice Access. Essa é a configuração padrão. Quando você clicar nesse botão, um PIN será gerado automaticamente com base nas políticas de PIN configuradas na política de caixa de correio da UM atribuída ao usuário. É recomendável o uso dessa configuração para ajudar a proteger o PIN do usuário. O PIN é enviado ao usuário na mensagem de boas-vindas que ele recebe após ter habilitado a UM. Por padrão, ele terá que alterar esse PIN quando entrar pela primeira vez em sua caixa de correio para verificar seu correio de voz.
    
      - **Digitar um PIN**   Essa configuração habilita você a especificar manualmente um PIN que o usuário irá usar para acessar o sistema de caixa postal.
        
        O PIN deve estar de acordo com as configurações de política de PIN definidas na política de caixa de correio de UM associada a esse usuário habilitado para UM. Por exemplo, se a política de caixa de correio da UM estiver configurada para aceitar somente PINs que contenham sete ou mais dígitos, o PIN digitado nessa caixa deverá ter pelo menos sete dígitos.
    
      - **Exigir que o usuário redefina seu PIN na primeira vez que entrar**   Essa configuração força o usuário a redefinir o PIN da sua caixa postal quando acessar o sistema de caixa postal com um telefone usando o Outlook Voice Access pela primeira vez. Será solicitado que o usuário insira um PIN mais familiar a ele. É uma prática recomendada de segurança forçar usuários habilitados para UM a alterar seus PINs quando entram pela primeira vez para proteção contra acesso não autorizado a dados e Caixa de Entrada. Esta caixa de seleção é marcada por padrão.

## Usar o Shell para habilitar um usuário para UM e caixa postal

Este exemplo habilita a Unificação de Mensagens e a caixa postal na caixa de correio de tonysmith@contoso.com, define o ramal e define manualmente o PIN do usuário e atribui, ao usuário, uma política de caixa de correio de UM chamada `MyUMMailboxPolicy`.

    Enable-UMMailbox -Identity tonysmith@contoso.com -UMMailboxPolicy MyUMMailboxPolicy -Extensions 51234 -PIN 5643892 -PINExpired $true

Este exemplo habilita a Unificação de Mensagens e a caixa postal na caixa de correio de tonysmith@contoso.com, atribui, ao usuário, uma política de caixa de correio de UM chamada `MyUMMailboxPolicy` e definir número de ramal, endereço SIP e define manualmente o PIN do usuário.

    Enable-UMMailbox -Identity tonysmith@contoso.com -UMMailboxPolicy MyUMMailboxPolicy -Extensions 51234 -PIN 5643892 -SIPResourceIdentifier "tonysmith@contoso.com" -PINExpired $true

## Desabilitar a UM para um usuário

Ao desabilitar a Unificação de Mensagens para um usuário, a conta desse usuário pode ainda estar na lista quando um chamador fizer uma busca de diretório usando um menu do atendedor automático da UM ou o Outlook Voice Access. Os chamadores podem conseguir localizar um usuário no diretório, mas ao tentar entrar em contato com o usuário, retornarão ao menu principal na Unificação de Mensagens. Isso pode fazer com que os chamadores fiquem frustrados com o sistema. Você pode evitar que os chamadores usem a pesquisa de diretório para entrar em contato com um usuário que tenha sido desabilitado para Unificação de Mensagens, conectando o usuário a outro sistema de caixa postal, removendo o usuário da pesquisa de diretório do atendedor automático de UM ou removendo a conta do usuário.

Depois que uma conta de usuário habilitado para UM for desabilitada para Unificação de Mensagens, o usuário ainda poderá ter acesso à sua caixa de correio individual habilitada para UM usando do Outlook Voice Access ou o Microsoft Outlook. Isso pode ocorrer quando todas as alterações não são consistentes no diretório. Para diminuir o risco de um usuário obter acesso à caixa de correio mesmo que sua conta tenha sido desabilitada para Unificação de Mensagens, você pode forçar manualmente a replicação ou pode remover todas as informações da Unificação de Mensagens da caixa de correio do usuário quando ele for desabilitado para a Unificação de Mensagens.

