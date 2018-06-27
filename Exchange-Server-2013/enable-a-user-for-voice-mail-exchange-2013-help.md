---
title: 'Habilitar um usuário para caixa postal: Exchange 2013 Help'
TOCTitle: Habilitar um usuário para caixa postal
ms:assetid: ad027767-5e14-4cb1-9f8a-0791d9188db5
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Bb124147(v=EXCHG.150)
ms:contentKeyID: 50486385
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
f1_keywords:
- Microsoft.Exchange.Management.SnapIn.Esm.Recipients.EnableUnifiedMessagingWizardForm.EnableUnifiedMessagingWizardPage
ms.translationtype: MT
---

# Habilitar um usuário para caixa postal

 

_**Aplica-se a:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Tópico modificado em:**2013-02-22_

Quando você habilita um usuário para Unificação de mensagens (UM), um conjunto padrão das propriedades são aplicadas ao usuário e o usuário será capaz de usar os recursos de caixa postal incluídos com a Unificação de mensagens. Após habilitar um usuário para caixa postal, você tem a opção de adicionar um endereço de protocolo de iniciação de sessão (SIP) para o usuário se eles estão atribuídos a uma política de caixa de correio de Unificação de mensagens que está vinculada a um plano de discagem URI do SIP. Ou então, você pode adicionar um número e. 164 para o usuário se eles estão atribuídos a uma política de caixa de correio de Unificação de mensagens que está vinculada a um plano de discagem e. 164. Em ambos os casos, o usuário ainda deve ter um número de ramal configurado.

Um número de ramal é necessário para cada usuário que está associado a um ramal de telefone, SIP URI Uniform Resource Identifier () ou plano de discagem e. 164. O número de extensão deve ser o número correto de dígitos, conforme especificado no plano de discagem de Unificação de mensagens para a política de caixa de correio de Unificação de mensagens.


> [!TIP]
> Você deve adicionar, remover ou modificar os números de ramal para todos os usuários habilitados para UM usando o EAC ou o Shell, mesmo que estejam vinculados a um URI do SIP ou o plano de discagem e. 164. Para adicionar, remover ou modificar o endereço SIP ou números e. 164 para usuários, você precisará usar o Shell, pois essas opções não estarão disponíveis no EAC.



Para conhecer tarefas de gerenciamento adicionais relacionadas a usuários habilitados para caixa postal, consulte [Procedimentos do usuário habilitado para email de voz](voice-mail-enabled-user-procedures-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: 5 minutos.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Caixas de correio da UM" no tópico [Permissões de mensagens unificadas](unified-messaging-permissions-exchange-2013-help.md).

  - Antes de executar esses procedimentos, confirme se um plano de discagem da UM foi criado. Para obter etapas detalhadas, consulte [Criar um plano de discagem de UM](create-a-um-dial-plan-exchange-2013-help.md).

  - Antes de executar esses procedimentos, verifique se uma política de caixa de correio de UM foi criada. Para obter etapas detalhadas, consulte [Criar uma política de caixa de correio da UM](create-a-um-mailbox-policy-exchange-2013-help.md).

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>..



## O que você deseja fazer?

## Usar o EAC para habilitar um usuário para caixa postal

1.  No EAC, clique em **Destinatários**.

2.  Na exibição de lista, selecione o usuário cuja caixa de correio que você deseja habilitar para a Unificação de mensagens.

3.  No painel Detalhes, em **Telefone e Recursos de Voz**, clique em **Habilitar**.

4.  Na página **Habilitar caixa de correio de UM**, clique no botão **Procurar** ao lado de **Política de caixa de correio de UM**, localize a política de caixa de correio de UM, para atribuir o usuário a partir da lista, e clique em **OK**.

5.  Na página **Habilitar caixa de correio de UM**, preencha as seguintes caixas:
    
      - **Endereço SIP** ou o **número e. 164**, na caixa de texto **endereço SIP** ou o **número e. 164**, digite o endereço SIP ou o número e. 164 para o usuário. Essas opções estarão disponíveis se o usuário que você habilitou para Unificação de mensagens é atribuído a uma política de caixa de correio de Unificação de mensagens que está vinculada a um URI do SIP ou um plano de discagem e. 164. Você não pode adicionar um endereço SIP ou o número e. 164 para um usuário se o usuário estiver associado um plano de discagem de ramal de telefone.
        
        Quando você atribuir um usuário a uma política de caixa de correio de Unificação de mensagens que esteja vinculada a um URI do SIP ou o plano de discagem e. 164, você deve inserir um número de ramal para o usuário. O usuário usará esse número de extensão ao acessar suas caixas de correio via Outlook Voice Access. O número de dígitos que você definir nesta caixa deve corresponder ao número de dígitos configurado no URI do SIP ou o plano de discagem e. 164.
    
      - **Número de ramal**    Use esta caixa de texto para digitar manualmente o número do ramal para o usuário que você está habilitando para Unificação de mensagens.
        
        Você deve fornecer um número de ramal válido para o usuário e deve corresponder ao número de dígitos especificado no plano de discagem. Você só pode inserir dígitos de 1 a 20. O número do ramal típico é 3 para 7 dígitos. O número de dígitos no ramal é definido no plano de discagem que está vinculado para a política de caixa de correio de Unificação de mensagens que é atribuída ao usuário.
    
      - Em **Configurações de PIN**, preencha o seguinte:
        
          - **Gerar automaticamente PIN**    Clique nesse botão para gerar automaticamente um PIN para o usuário habilitado para Unificação de mensagens a ser usada para acesso de email de voz por meio do Outlook Voice Access. Esta é a configuração padrão. O PIN é gerado automaticamente com base nas diretivas PIN configuradas na diretiva de caixa de correio de Unificação de mensagens atribuída ao usuário. O uso dessa configuração ajudará a proteger o PIN do usuário. O PIN é enviado ao usuário na mensagem de boas-vindas que receberem depois que elas são habilitadas para UM. Por padrão, eles terá que alterar esse PIN quando eles entrar pela primeira vez suas caixas de correio para obter suas mensagens de voz.
        
          - **Tipo de um PIN**    Clique nesse botão para inserir um PIN que o usuário irá usar para acessar o sistema de caixa postal. O PIN deve estar em conformidade com as configurações de diretiva PIN configuradas na diretiva de caixa de correio UM associado a esse usuário habilitado para UM. Por exemplo, se a diretiva de caixa de correio de Unificação de mensagens estiver configurada para aceitar apenas os PINs que contêm sete ou mais dígitos, o PIN digitado nesta caixa deve ser pelo menos sete dígitos.
        
          - **Exigir que o usuário redefina seu PIN na primeira vez que entrar**   Marque esta caixa de seleção para forçar o usuário a redefinir seu PIN de caixa postal quando acessar o sistema de caixa postal a partir de um telefone usando o Outlook Voice Access pela primeira vez. Será solicitado que o usuário insira um PIN mais familiar a ele. É uma prática recomendada de segurança forçar usuários habilitados para UM a alterar seus PINs quando entram pela primeira vez para proteção contra acesso não autorizado a dados e Caixa de Entrada. Esta caixa de seleção é marcada por padrão.

6.  Na página **Habilitar UM caixa de correio**, revise suas configurações. Clique em **Concluir** para permitir que o usuário para caixa postal. Clique em **Voltar** para fazer alterações de configuração.

## Use o Shell para habilitar um usuário para caixa postal

Este exemplo habilita a Unificação de mensagens na caixa de correio de tonysmith@contoso.com, define o número do ramal como 51234, define o PIN para o usuário 5643892 e atribui o usuário a uma diretiva de caixa de correio de UM chamado `MyUMMailboxPolicy`.

    Enable-UMMailbox -Identity tonysmith@contoso.com -UMMailboxPolicy MyUMMailboxPolicy -Extensions 51234 -PIN 5643892 -PINExpired $true

Este exemplo habilita a Unificação de mensagens na caixa de correio de tonysmith@contoso.com, atribui o usuário a uma diretiva de caixa de correio de UM chamado `MyUMMailboxPolicy`e define o número de ramal, o endereço SIP e o PIN do usuário.

    Enable-UMMailbox -Identity tonysmith@contoso.com -UMMailboxPolicy MyUMMailboxPolicy -Extensions 51234 -PIN 5643892 -SIPResourceIdentifier "tonysmith@contoso.com" -PINExpired $true

