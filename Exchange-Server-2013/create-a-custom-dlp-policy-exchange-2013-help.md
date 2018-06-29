---
title: 'Criar uma política DLP personalizada: Exchange 2013 Help'
TOCTitle: Criar uma política DLP personalizada
ms:assetid: b3299a39-9663-41e4-b76e-9d2f7879d486
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/JJ150550(v=EXCHG.150)
ms:contentKeyID: 50484793
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Criar uma política DLP personalizada

 

_**Aplica-se a:**Exchange Online, Exchange Server 2013_

_**Tópico modificado em:**2016-03-18_

Uma política de prevenção (DLP) de perda de dados personalizados permite estabelecer condições, regras e ações que pode ajudar a atender às necessidades específicas da sua organização e que não podem ser cobertos em um dos modelos de DLP pré-existente.

As condições de regra que estão disponíveis para você em uma única política incluem todas as regras de transporte tradicional, além dos tipos de informações confidenciais apresentados no [O que os tipos de informações confidenciais no Exchange procurar](what-the-sensitive-information-types-in-exchange-look-for-exchange-online-help.md). Para obter mais informações sobre regras de transporte, consulte [Regras de fluxo de emails ou de transporte](mail-flow-rules-transport-rules-in-exchange-2013-exchange-2013-help.md) (Exchange 2013 ) ou [Regras de fluxo de emails (regras de transporte) no Exchange Online](https://technet.microsoft.com/pt-br/library/jj919238\(v=exchg.150\)) (Exchange Online ).


> [!WARNING]
> Você deve habilitar as suas políticas de DLP no modo de teste antes de executá-los em seu ambiente de produção. Durante esses testes, é recomendável que você configurar caixas de correio de usuário de amostra e envia mensagens de teste que acionem suas políticas de teste para ter a certeza os resultados. Para obter mais informações sobre como testar, consulte <A href="test-a-mail-flow-rule-exchange-2013-help.md">Testar uma regra de fluxo de email</A>.



Para tarefas de gerenciamento adicionais relacionadas à criação de uma política DLP personalizada, consulte [Procedimentos DLP](dlp-procedures-exchange-2013-help.md)(Exchange 2013 ) ou [Procedimentos DLP](https://technet.microsoft.com/pt-br/library/jj938003\(v=exchg.150\)) (Exchange Online ).

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: 60 minutos

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada \&quot;Prevenção de perda de dados (DLP)\&quot; no tópico [Permissões de política e conformidade de mensagens](messaging-policy-and-compliance-permissions-exchange-2013-help.md).

  - Para criar uma nova política DLP personalizada, você deve seguir as instruções de instalação para Exchange 2013. Para obter mais informações sobre a implantação, consulte [Planejamento e implantação](planning-and-deployment-for-exchange-2013-installation-instructions.md).

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Devido às variações nos ambientes do cliente, serviços de suporte a cliente Microsoft (CSS) não podem participar de desenvolvimento ou teste de scripts personalizados de expressão Regular ("RegEx scripts"). Para o desenvolvimento de script personalizado RegEX, testar e depurar, os clientes do Office 365 precisará contar com os recursos de TI internos. Como alternativa, os clientes do Office 365 podem optar por usar um recurso de consultoria externo, como serviços de consultoria Microsoft (MCS). Independentemente do recurso de desenvolvimento de script, os engenheiros de suporte de CSS EXO e o EOP não estão disponíveis para ajudar os clientes com as consultas de script personalizados RegEx.




> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>.



## Usar o EAC para criar uma política DLP personalizada sem todas as regras existentes

1.  No EAC, navegue até **gerenciamento de conformidade** \> **prevenção de perda de dados**. Quaisquer políticas existentes que você configurou são mostradas em uma lista.

2.  Clique na seta ao lado do ícone de![Ícone Adicionar](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Ícone Adicionar")**Adicionar** e selecione **nova política personalizada**.
    

    > [!IMPORTANT]
    > Se você clicar em um ícone de<IMG title="Ícone Adicionar" alt="Ícone Adicionar" src="images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif"><STRONG>Adicionar</STRONG> em vez de seta para baixo, você criará uma nova política baseada em um modelo. Para obter mais informações sobre como usar modelos, consulte <A href="how-to-new-dlp-data-loss-prevention-policy-template.md">Criar uma política de DLP a partir de um modelo</A>.



3.  Na página **nova política personalizada**, preencha os seguintes campos:
    
    1.  **Nome**   Adicionar um nome que irá distinguir essa política das outras.
    
    2.  **Descrição**   Adicionar uma descrição opcional que resuma esta política.
    
    3.  **Escolher um estado**    Selecione o modo ou estado para esta diretiva. A nova diretiva não está habilitada totalmente até que você especifique o que deve ser. O modo de padrão para uma diretiva é teste sem notificações.

4.  Clique em **Salvar** para concluir a criação de novas informações de referência de política. A política é adicionada à lista de todas as diretivas que você configurou, embora não haja ainda quaisquer regras ou as ações associadas a essa nova política personalizada.

5.  Clique duas vezes na política que você acabou de criar ou selecioná-la e clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").

6.  Na página **política de DLP Editar**, clique em **regras**.
    
    Clique em **Adicionar**![Ícone Adicionar](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Ícone Adicionar") para adicionar uma nova regra em branco. Você pode estabelecer condições usando todas as regras de transporte tradicional, além dos tipos de informações confidenciais.
    
    Para evitar a confusão, forneça um nome exclusivo para cada parte da sua política ou regra quando você tem a opção para fornecer sua própria cadeia de caracteres. Há várias opções adicionais de opções disponíveis para você:
    
    1.  Clique na seta ao lado do ícone de![Ícone Adicionar](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Ícone Adicionar")**Add** para adicionar uma regra sobre notificação do remetente ou permitindo substituições.
    
    2.  Para remover uma regra, realce a regra e clique em **Excluir**![Excluir ícone](images/JJ673559.14f639f6-61e8-4418-bbfb-0db14de9d2f5(EXCHG.150).gif "Excluir ícone").
    
    3.  Clique em **mais opções**![Ícone Mais opções](images/JJ150550.5381819e-3b21-4873-8714-e9b956290b28(EXCHG.150).gif "Ícone Mais opções") para adicionar outras condições e ações para essa regra, incluindo os limites de ligação de tempo da imposição ou efeitos sobre outras regras nessa política.

7.  Clique em **Salvar** para concluir a modificação a política e salvar suas alterações.

Modelos de política DLP são um tipo de recurso de design do Microsoft Exchange que podem ajudá-lo e aplicam um sistema de política e conformidade robusto para seu ambiente de mensagens. Para obter mais informações sobre recursos de conformidade, consulte [Conformidade e política de sistema de mensagens](messaging-policy-and-compliance-exchange-2013-help.md) (Exchange 2013 ) ou [Segurança e conformidade para Exchange Online](https://technet.microsoft.com/pt-br/library/jj200706\(v=exchg.150\)).

## Para obter mais informações

[Prevenção de perda de dados](technical-overview-of-dlp-data-loss-prevention-in-exchange.md)

[Regras de fluxo de emails ou de transporte](mail-flow-rules-transport-rules-in-exchange-2013-exchange-2013-help.md) Exchange 2013

[Regras de fluxo de emails (regras de transporte) no Exchange Online](https://technet.microsoft.com/pt-br/library/jj919238\(v=exchg.150\)) Exchange Online

[Integrando regras de informações confidenciais com regras de transporte](integrating-sensitive-information-rules-with-transport-rules-exchange-2013-help.md)

