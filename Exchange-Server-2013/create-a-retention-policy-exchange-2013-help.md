---
title: 'Criar uma política de retenção: Exchange 2013 Help'
TOCTitle: Criar uma política de retenção
ms:assetid: d8806c98-fea5-492f-906d-f514e25361b2
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/JJ150573(v=EXCHG.150)
ms:contentKeyID: 50486760
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Criar uma política de retenção

 

_**Aplica-se a:** Exchange Online, Exchange Server 2013_

_**Tópico modificado em:** 2016-12-09_

Em Exchange Online e Exchange Server 2013, você pode usar as políticas de retenção para gerenciar o ciclo de vida de email. Políticas de retenção são aplicadas por criar marcas de retenção, adicioná-las a uma política de retenção e aplicar a política aos usuários de caixa de correio.

Aqui está um [vídeo](https://go.microsoft.com/fwlink/?linkid=825854) que mostra como criar uma política de retenção e aplicá-la a uma caixa de correio Exchange Online.

Para tarefas de gerenciamento adicionais relacionadas a políticas de retenção, consulte [Procedimentos de gerenciamento de registros de mensagens](messaging-records-management-procedures-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para a conclusão da tarefa: 30 minutos.

  - Os procedimentos neste tópico exigem permissões específicas. Consulte cada procedimento para ver informações sobre permissões.

  - Caixas de correio para o qual você aplicar políticas de retenção devem residir em Exchange Server 2010 servidores ou posteriores.

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

## Como fazer isso?

## Etapa 1: Criar uma marca de retenção

Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Gerenciamento de mensagens registros" no tópico [Permissões de política e conformidade de mensagens](messaging-policy-and-compliance-permissions-exchange-2013-help.md) .

**Usar o EAC para criar uma marca de retenção**

1.  Navegue até **gerenciamento de conformidade** \> **marcas de retenção** e clique em **Adicionar**![Ícone Adicionar](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Ícone Adicionar")

2.  Selecione uma das seguintes opções:
    
      - **Aplicado automaticamente a caixa de correio inteira (padrão)**    Selecione essa opção para criar uma marca de diretiva padrão (DPT). Você pode usar DPTs para criar uma política de exclusão padrão e uma política de arquivo morto padrão, que se aplica a todos os itens da caixa de correio.
        

        > [!TIP]
        > Você não pode usar o EAC para criar um DPT para excluir itens da caixa postal. Para obter detalhes sobre como criar um DPT para excluir itens da caixa postal, consulte o exemplo de Shell a seguir.

    
      - **Aplicado automaticamente a uma pasta específica**    Selecione esta opção para criar uma marca de política de retenção (RPT) para uma pasta padrão, como **caixa de entrada** ou **Itens excluídos**.
        

        > [!TIP]
        > Você só pode criar RPTs com as ações <STRONG>Excluir e permitir recuperação</STRONG> ou <STRONG>Excluir permanentemente</STRONG>.

    
      - **Aplicado pelos usuários para itens e pastas (pessoais)**    Selecione essa opção para criar marcas pessoais. Essas marcas permitem que usuários Outlook e Outlook Web App aplicar as configurações de arquivamento ou exclusão a uma mensagem ou pastas que são diferentes das configurações aplicadas a pasta pai ou a caixa de correio inteira.

3.  O título da página **nova marca de retenção** e opções irá variar dependendo do tipo de marca selecionada. Preencha os seguintes campos:
    
      - **Nome**    Insira um nome para a marca de retenção. O nome da marca para fins de exibição e não tem nenhum impacto na pasta ou item que uma marca é aplicada. Considere a possibilidade de que as marcas pessoais que provisionar usuários estão disponíveis no Outlook e Outlook Web App.
    
      - **Aplicar nesta marca para a seguinte pasta padrão**    Essa opção está disponível apenas se você selecionou **aplicado automaticamente a uma pasta específica**.
    
      - **Ação de retenção**    Selecione uma das seguintes ações a serem tomadas após o item atinge seu período de retenção:
        
          - **Excluir e permitir recuperação**    Selecionar essa ação Excluir itens, mas permitir que os usuários para recuperá-los usando a opção de **Recuperar itens excluídos** no Outlook ou itens do Outlook Web App. são mantidas até que o período de retenção de item excluído configurado para o banco de dados de caixa de correio ou de correio do usuário for atingido.
        
          - **Excluir permanentemente**    Selecione essa opção para excluir permanentemente o item do banco de dados de caixa de correio.
            

            > [!IMPORTANT]
            > Caixas de correio ou itens sujeitos a espera de bloqueio In-loco ou retenção de litígio serão retidos e retornados em pesquisas de descoberta eletrônica In-loco. Para obter mais informações, consulte <A href="in-place-hold-and-litigation-hold-exchange-2013-help.md">Retenção local e Retenção de litígio</A>.

        
          - **Mover para arquivo morto**    Essa ação só estará disponível se você estiver criando um DPT ou uma marca pessoal. Selecione essa ação para mover itens para o arquivo de In-loco do usuário.
    
      - **Período de retenção**    Selecione uma das seguintes opções:
        
          - **Nunca**    Selecione essa opção para especificar que itens nunca devem ser excluídos ou movidos para o arquivo morto.
        
          - **Quando o item atinge a seguinte idade (em dias)**    Selecione essa opção e especifique o número de dias para reter itens antes que eles estiver movidos ou excluídos. A idade de retenção para todos os itens com suporte, com exceção de calendário e tarefas é calculada a partir da data de um item é recebido ou criado. Idade de retenção para itens de calendário e tarefas é calculada da data de término.
    
      - **Comentário**    Usuário esse campo opcional para inserir quaisquer comentários ou anotações administrativas. O campo não será exibido aos usuários.

**Use o Shell para criar uma marca de retenção**

Use o cmdlet **New-RetentionPolicyTag** para criar uma marca de retenção. Diferentes opções disponíveis no cmdlet permitem que você criar diferentes tipos de marcas de retenção. Use o parâmetro *Type* para criar um DPT (`All`), RPT (especificar um tipo de pasta padrão, como `Inbox`) ou uma marca pessoal (`Personal`).

Este exemplo cria um DPT para excluir todas as mensagens na caixa de correio após sete anos (2,556 dias).

    New-RetentionPolicyTag -Name "DPT-Corp-Delete" -Type All -AgeLimitForRetention 2556 -RetentionAction DeleteAndAllowRecovery

Este exemplo cria um DPT para mover todas as mensagens para o arquivamento In-loco em 2 anos (730 dias).

    New-RetentionPolicyTag -Name "DPT-Corp-Move" -Type All -AgeLimitForRetention 730 -RetentionAction MoveToArchive

Este exemplo cria um DPT para excluir mensagens da caixa postal após 20 dias.

    New-RetentionPolicyTag -Name "DPT-Corp-Voicemail" -Type All -MessageClass Voicemail -AgeLimitForRetention 20 -RetentionAction DeleteAndAllowRecovery

Este exemplo cria um RPT para excluir permanentemente mensagens na pasta Lixo eletrônico após 30 dias.

    New-RetentionPolicyTag -Name "RPT-Corp-JunkMail" -Type JunkEmail -AgeLimitForRetention 30 -RetentionAction PermanentlyDelete

Este exemplo cria uma marca pessoal para nunca excluir uma mensagem.

    New-RetentionPolicyTag -Name "Never Delete" -Type Personal -RetentionAction DeleteAndAllowRecovery -RetentionEnabled $false

## Etapa 2: Criar uma diretiva de retenção

Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Gerenciamento de mensagens registros" no tópico [Permissões de política e conformidade de mensagens](messaging-policy-and-compliance-permissions-exchange-2013-help.md) .

**Usar o EAC para criar uma política de retenção**

1.  Navegue até **gerenciamento de conformidade** \> **políticas de retenção** e clique em **Adicionar**![Ícone Adicionar](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Ícone Adicionar")

2.  Na **Nova política de retenção**, preencha os seguintes campos:
    
      - **Nome**    Insira um nome para a política de retenção.
    
      - **Marcas de retenção**    Clique em **Adicionar**![Ícone Adicionar](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Ícone Adicionar") para selecionar as marcas que você deseja adicionar a esta política de retenção.
        
        Uma política de retenção pode conter as seguintes marcas:
        
          - Uma DPT com a ação **Mover para Arquivo Morto**
        
          - Uma DPT com a ação **Excluir e Permitir Recuperação** ou **Excluir Permanentemente**
        
          - Uma DPT para mensagens de caixa postal com as ações **Excluir e Permitir Recuperação** ou **Excluir Permanentemente**
        
          - Um RPT por pasta padrão, como **caixa de entrada** para excluir itens
        
          - Qualquer número de marcas pessoais
            

            > [!TIP]
            > Embora seja possível adicionar qualquer número de marcas pessoais a uma política de retenção, ter muitas marcas pessoais com as configurações de retenção diferente pode confundir os usuários. É recomendável vinculando não ultrapassa dez marcas pessoais a uma política de retenção.

        
        É possível criar uma política de retenção sem adicionando quaisquer marcas de retenção a ele, mas os itens na caixa de correio à qual a política será aplicada não ser movidos ou excluídos. Você também pode adicionar e remover as marcas de retenção de uma política de retenção, após sua criação.

**Usar o Shell para criar uma política de retenção**

Este exemplo cria a política de retenção RetentionPolicy-Corp e usa o parâmetro *RetentionPolicyTagLinks* para associar cinco marcas para a política.

    New-RetentionPolicy "RetentionPolicy-Corp"  -RetentionPolicyTagLinks "DPT-Corp-Delete","DPT-Corp-Move","DPT-Corp-Voicemail","RPT-Corp-JunkMail","Never Delete"

Para obter informações detalhadas de sintaxes e parâmetros, consulte [New-RetentionPolicy](https://technet.microsoft.com/pt-br/library/dd297970\(v=exchg.150\)).

## Etapa 3: Aplicar uma política de retenção para usuários de caixa de correio

Depois de criar uma política de retenção, você deverá aplicá-la aos usuários de caixa de correio. Você pode aplicar diferentes políticas de retenção a conjunto diferente de usuários. Para obter instruções detalhadas, consulte [Aplicar uma política de retenção a caixas de correio](apply-a-retention-policy-to-mailboxes-exchange-2013-help.md).

## Como saber se essa tarefa funcionou?

Depois que você cria marcas de retenção, adicioná-los a uma política de retenção e aplica a política a um usuário de caixa de correio, na próxima vez em que o Assistente de caixa de correio MRM processa a caixa de correio, mensagens são movidas ou excluídas com base nas configurações definidas nas marcas de retenção.

Para verificar se você aplicou a política de retenção, faça o seguinte:

1.  Execute o seguinte comando Shell para executar o assistente MRM manualmente em relação a uma única caixa de correio.
    
        Start-ManagedFolderAssistant -Identity <mailbox identity>

2.  Faça logon na caixa de correio usando Outlook ou Outlook Web App e verificar se as mensagens são excluídas ou movidas para um arquivo morto de acordo com a configuração de diretiva.


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>.


