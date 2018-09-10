---
title: 'Configurar códigos de discagem: Exchange 2013 Help'
TOCTitle: Configurar códigos de discagem
ms:assetid: e5b5efee-b734-4f70-8357-11be07b23bd0
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Bb124992(v=EXCHG.150)
ms:contentKeyID: 51407928
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configurar códigos de discagem

 

_**Aplica-se a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Tópico modificado em:** 2013-02-22_

Você pode configurar códigos de discagem, prefixos de número e formatos de número que são usados pela Unificação de mensagens para fazer chamadas de entrada e saídas para os usuários habilitados para Unificação de mensagens. Na maioria dos casos, você vai configurar um plano de discagem com os códigos de discagem, prefixos e formatos de número atualmente configurados em sua rede de telefonia.

Códigos de discagem e prefixos de número são usados para determinar o número correto para discar para uma chamada de saída que for feita por um usuário habilitado para UM. *Outdialing* é o termo usado para descrever o processo pelo qual um usuário em um plano de discagem de UM inicia uma chamada de saída. Formatos de número são usados para chamadas de entrada dentro de um país ou região, chamadas internacionais ou chamadas que são colocadas dentro de um plano de discagem. Você pode configurar um plano de discagem para corresponder ao formato de número de chamada de entrada para números de país/região e internacionais. Quando você configura os formatos de número do país/região e internacionais, você pode restringir as chamadas de entrada para os usuários vinculadas com um plano de discagem.

Para conhecer tarefas de gerenciamento adicionais relacionadas à discagem externa, consulte [Permitindo que usuários façam chamadas de procedimentos](https://docs.microsoft.com/pt-br/exchange/voice-mail-unified-messaging/set-up-client-voice-mail-features/allow-users-to-make-calls-procedures).

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: Menos de 1 minuto.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Planos de discagem de UM" no tópico [Permissões de mensagens unificadas](unified-messaging-permissions-exchange-2013-help.md).

  - Antes de executar esses procedimentos, confirme se um plano de discagem da UM foi criado. Para obter etapas detalhadas, consulte [Criar um plano de discagem de UM](create-a-um-dial-plan-exchange-2013-help.md).

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>..



## O que você deseja fazer?

## Usar o EAC para configurar códigos de discagem, prefixos e formatos numéricos

1.  No EAC, navegue até **Unificação de Mensagens** \> **Planos de discagem de UM**.

2.  Selecione o plano de discagem da UM que deseja gerenciar e, depois, clique em **Editar**![Ícone de edição](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Ícone de edição").

3.  Na página **Plano de discagem de UM**, clique em **Configurar**.

4.  Na página **plano de discagem da UM** \> **Códigos de discagem**, configure as seguintes opções:
    
      - **Código de acesso de linha externa**
    
      - **Código de acesso internacional**
    
      - **Prefixo de número nacional/regional**
    
      - **Código do País/Região**

5.  Em **Formatos de número para discagem entre planos de discagem**, configure o seguinte:
    
      - **Formato numérico do país/região**
    
      - **Formato de número internacional**
    
      - **Formatos de número para chamadas de entrada dentro do mesmo plano de discagem**   Para adicionar um formato numérico, clique em **Adicionar**![Ícone Adicionar](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Ícone Adicionar").

6.  Clique em **Salvar** para salvar suas alterações.

## Usar o Shell para configurar códigos de discagem, prefixos e formatos numéricos

Este exemplo configura um plano de discagem de UM chamado `MyUMDialPlan` com um formato numérico de país ou região, um formato numérico internacional e os seguintes códigos de discagem:

  - 9 para o código de acesso à linha externo

  - 011 para o código de acesso internacional

  - 1 para o prefixo de número nacional

  - 1 para o código de país ou região

<!-- end list -->

    Set-UMDialPlan -Identity MyUMDialPlan -OutsideLineAccessCode 9 -InternationalAccessCode 011 -NationalNumberPrefix 1 CountryorRegionCode 1 -InCountryOrRegionNumberFormat 1425xxxxxxx -InternationalNumberFormat 441425xxxxxxx

