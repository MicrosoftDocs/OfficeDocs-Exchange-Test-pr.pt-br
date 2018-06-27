---
title: 'Criar um plano de discagem de UM: Exchange 2013 Help'
TOCTitle: Criar um plano de discagem de UM
ms:assetid: 963ff2e1-515d-439a-953a-664174e5e283
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Bb123819(v=EXCHG.150)
ms:contentKeyID: 50486161
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
f1_keywords:
- Microsoft.Exchange.Management.SnapIn.Esm.Servers.UnifiedMessaging.CreateUMDialPlanWizardForm.CreateUMDialPlanWizardPage
ms.translationtype: MT
---

# Criar um plano de discagem de UM

 

_**Aplica-se a:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Tópico modificado em:**2013-04-16_

Um plano de discagem de Unificação de mensagens (UM) contém informações de configuração relacionadas à sua rede de telefonia. Um plano de discagem UM estabelece um vínculo do número de ramal de um usuário habilitado para caixa postal para suas caixas de correio. Quando você cria um plano de discagem de UM, você pode configurar o número de dígitos nos ramais, o tipo de identificador de recurso uniforme (URI) e a voz sobre configuração de segurança IP (VoIP) para o plano de discagem.

Cada vez que você criar um plano de discagem de Unificação de mensagens, uma política de caixa de correio de Unificação de mensagens também é criada. A diretiva de caixa de correio de Unificação de mensagens é nomeada \<*DialPlanName*\> política padrão.

Para mais tarefas de gerenciamento relacionadas a planos de discagem de UM, consulte [Procedimentos de plano de discagem de UM](um-dial-plan-procedures-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: 3 minutos.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Planos de discagem de UM" no tópico [Permissões de mensagens unificadas](unified-messaging-permissions-exchange-2013-help.md).

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>..



## O que você deseja fazer?

## Usar o EAC para criar um plano de discagem de UM

1.  
    
    No EAC, navegue para **Unificação de Mensagens** \> **Planos de discagem de UM** e, em seguida, clique em **Novo**![Ícone Adicionar](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Ícone Adicionar").

2.  Na página de **plano de discagem de UM novo**, preencha as seguintes caixas:
    
      - **Nome**    Digite o nome do plano de discagem. Um nome de plano de discagem de Unificação de mensagens é obrigatório e deve ser exclusivo. No entanto, ele é usado somente para exibição no EAC e o Shell. Se você precisar alterar o nome de exibição do plano de discagem após ele ter sido criado, você deve primeiro excluir o plano de discagem UM existente e, em seguida, criar outro plano de discagem que tenha o nome apropriado. Se sua organização usa vários planos de discagem de Unificação de mensagens, recomendamos que você use nomes significativos para seus planos de discagem de Unificação de mensagens. O comprimento máximo de um nome de plano de discagem de Unificação de mensagens é de 64 caracteres e pode incluir espaços. No entanto, ele não pode incluir qualquer um dos seguintes caracteres: "/ \\ \[\]:; | = , + \* ? \< \>.
        
        Embora você possa incluir espaços em um nome de plano de discagem de Unificação de mensagens, se você integrar a Unificação de mensagens com o Office Communications Server 2007 R2 ou Microsoft Lync Server, o nome do plano de discagem não pode incluir espaços. Portanto, se você criou um plano de discagem com espaços no nome de exibição e você estiver integrando com o Office Communications Server 2007 R2 ou o Lync Server, você deve primeiro exclua que plano de discagem e, em seguida, criar outro plano de discagem que não incluem espaços no nome de exibição.
        

        > [!IMPORTANT]
        > Embora a caixa para o nome do plano de discagem pode aceitar 64 caracteres, o nome do plano de discagem não pode ter mais de 49 caracteres. Se você tentar criar um nome de plano de discagem que contém mais de 49 caracteres, você receberá uma mensagem de erro. A mensagem será dizer que a diretiva de caixa de correio de Unificação de mensagens não pôde ser gerada porque o nome de plano de discagem de Unificação de mensagens é muito longo. Isso acontece porque, como mencionado anteriormente, quando você cria um plano de discagem uma diretiva de caixa de correio de Unificação de mensagens padrão denominada <EM>&lt;DialPlanName&gt;</EM> política padrão também será criada. Quando os 15 caracteres na política padrão são adicionados ao nome do plano de discagem, o total de caracteres exceder o limite. Planejar ao parâmetro <EM>name</EM> para ambas as situações de discagem de UM e política de caixa de correio de Unificação de mensagens pode ser 64 caracteres. No entanto, se o nome do plano de discagem for maior que 49 caracteres, o nome da diretiva de caixa de correio de Unificação de mensagens padrão será mais de 64 caracteres, e isso não é permitido pelo sistema.

    
      - **Comprimento da extensão (dígitos)**    Insira o número de dígitos para o plano de discagem. O número de dígitos para números de ramal baseia-se no plano de discagem de telefonia criado em uma Private Branch eXchange (PBX) ou IP PBX. Por exemplo, se um usuário associado com um plano de discagem de telefonia disca para uma extensão de quatro dígitos para chamar o outro usuário no mesmo plano de discagem de telefonia, selecione 4 como o número de dígitos no ramal.
        
        Essa é uma caixa necessária que tem um intervalo de valores de 1 a 20. O comprimento da extensão típico é de 3 a 7. Se o ambiente de telefonia existente incluir números de ramal, você deve especificar um número de dígitos que corresponde ao número de dígitos nestas extensões.
        
        Quando você cria um protocolo de iniciação de sessão (SIP) ou um plano de discagem e. 164 e associa um usuário habilitado para UM plano de discagem, você ainda deve digitar um número de ramal a ser usado pelo usuário. Esse número é usado pelos usuários do Voice Access Outlook quando acessarem suas caixas de correio.
    
      - UNRESOLVED\_TOKENBLOCK\_VAL(Tipo UI\_URI)
    
      - UNRESOLVED\_TOKENBLOCK\_VAL(Segurança UI\_VoIP)
    
      - **Idioma de áudio**    Use essa lista para especificar o idioma padrão a ser utilizado pelos usuários do Outlook Voice Access. Essa configuração não se aplica a configuração do idioma em um atendedor automático. Você pode definir o idioma do Outlook Voice Access a ser igual ou diferente do idioma usado em um atendedor automático. Quando um usuário faz uma chamada para um usuário que está vinculada com um plano de discagem, o idioma de áudio é o idioma padrão que usa o operador registradas de voz. Os prompts de sistema que os chamadores ouvem são executados no mesmo idioma. O idioma escolhido em UM plano de discagem é usado para ler email, caixa postal e itens de calendário; o nome do usuário que informa se um pessoal saudação não foi registrada; transcrever uma mensagem de voz usando o recurso de visualização da caixa postal; e habilitar o reconhecimento de fala automático (ASR) funcione corretamente.
    
      - **Código de país/região**    Use esta caixa para digitar o número de código de país/região a ser usado para chamadas de saída. Esse número terão precedência sobre o número de telefone discado. Essa caixa aceita de 1 a 4 dígitos. Por exemplo, nos Estados Unidos, o código de país/região é 1. No Reino Unido, ele 's 44.

3.  Clique em **Salvar**.

## Usar o Shell para criar um plano de discagem de UM

Este exemplo cria um novo plano de discagem de UM chamado `MyUMDialPlan` que usa números de ramal de quatro dígitos.

    New-UMDialplan -Name MyUMDialPlan -NumberofDigits 4

Este exemplo cria um novo plano de discagem UM chamado `MyUMDialPlan` que usa números de ramal de cinco dígitos e suporta URIs do SIP.

    New-UMDialplan -Name MyUMDialPlan -UriType SIPName -NumberofDigits 5

