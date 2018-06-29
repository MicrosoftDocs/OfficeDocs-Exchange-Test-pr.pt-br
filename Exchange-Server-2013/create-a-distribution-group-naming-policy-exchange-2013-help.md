---
title: 'Criar um diretiva de nomeação de grupo de distribuição: Exchange 2013 Help'
TOCTitle: Criar um diretiva de nomeação de grupo de distribuição
ms:assetid: b2ffb654-345d-4be1-be8e-83d28901373e
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/JJ218693(v=EXCHG.150)
ms:contentKeyID: 50484812
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Criar um diretiva de nomeação de grupo de distribuição

 

_**Aplica-se a:**Exchange Online, Exchange Server 2013_

_**Tópico modificado em:**2012-11-01_

*Diretiva de nomenclatura de grupo* permite padronizar e gerenciar os nomes dos grupos de distribuição criados por usuários em sua organização. Você pode exigir um prefixo específico e o sufixo de ser adicionado ao nome do grupo de distribuição quando ele é criado e você pode bloquear palavras específicas de serem usadas. Isso ajuda a minimizar o uso de palavras inadequados em nomes de grupo.

Uma diretiva de nomeação de grupo:

  - Impõe uma estratégia de nomeação consistente para grupos criados por usuários.

  - Identifica a grupos de distribuição no catálogo de endereços compartilhado.

  - Sugere a função ou a associação do grupo.

  - Identifica o tipo de usuários que são provavelmente membros do grupo.

  - Identifica a região geográfica, que o grupo é usado.

  - Palavras inadequadas de blocos em nomes de grupo.

Como funciona a uma diretiva de nomeação de grupo? Quando um usuário cria um grupo, eles especificam um nome no campo nome de exibição. Depois que o grupo é criado, o Microsoft Exchange se aplica o diretiva de nomenclatura adicionando nenhum prefixo ou sufixo que você tenha definido no grupo de diretiva de nomenclatura de grupo. O nome completo é exibido na lista de grupos de distribuição no Centro de administração do Exchange (EAC), o catálogo de endereços compartilhado e para:, Cc: e a partir: campos em mensagens de email. Se um usuário tenta usar uma palavra que você bloqueou, eles obtém uma mensagem de erro quando tentar salvar o novo grupo e serão solicitados para remover a palavra bloqueada e salve o grupo novamente.

Aqui estão alguns exemplos de um diretiva de nomenclatura de grupo. Em cada um, **\< nome do grupo \>** é um nome descritivo fornecido pela pessoa que cria o grupo. Exchange adiciona os prefixos e sufixos definidos pela política com o nome de exibição quando o grupo é criado.

  - Cadeias de caracteres de texto, com caracteres de sublinhado, usados para um único prefixo (**DG**) e o sufixo (**usuários**):
    
    **\_Users DG\_ \< nome do grupo \>**

  - Vários prefixos (**DG** e **Contoso**) e um sufixo (**usuários**), usando cadeias de caracteres de texto:
    
    **\_Users DG\_Contoso\_ \< nome do grupo \>**

  - Um atributo (**departamento**) usado para o prefixo:
    
    **Department\_ \< nome do grupo \>**
    
    Por exemplo, dizer que sua escola preenche o atributo do departamento para que membros de Corpo Docente. Aqui está um exemplo de nome de um grupo criado por um membro de Corpo Docente do departamento psicologia:
    
    **Psychology\_Cognitive201**
    
    Neste exemplo, o caractere de sublinhado (\_) é fornecido como a cadeia de caracteres de texto apenas em um segundo prefixo para separar o nome do departamento do nome do grupo.

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: 5 minutos.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Grupos de distribuição" no tópico [Permissões de destinatários](recipients-permissions-exchange-2013-help.md) .

  - O comprimento máximo do nome de um grupo é de 64 caracteres. Isso inclui o número combinado de caracteres no prefixo, o nome do grupo fornecidos pelo usuário e o sufixo.

  - O diretiva de nomenclatura de grupo é aplicado somente aos grupos criados por usuários. Quando você ou outros administradores de usarem o EAC para criar grupos de distribuição, o diretiva de nomenclatura de grupo é ignorado e não é aplicado ao nome do grupo.

  - Nomes de grupo são criados sem espaçamento. Recomendamos que você use um caractere de sublinhado (\_) ou algum outro espaço reservado entre cadeias de caracteres de texto, atributos e o nome do grupo.

  - Você pode usar o Windows PowerShell para substituir o grupo de diretiva de nomenclatura quando você cria e edita um grupo de distribuição. Para obter mais informações, consulte [Substituir o diretiva de nomenclatura de grupo de distribuição](override-the-distribution-group-naming-policy-exchange-2013-help.md).

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>..



## Usar o EAC para criar um diretiva de nomenclatura de grupo

1.  No EAC, selecione **grupos** \> **mais**![Ícone Mais opções](images/JJ150550.5381819e-3b21-4873-8714-e9b956290b28(EXCHG.150).gif "Ícone Mais opções") \> **grupo Configurar diretiva de nomenclatura**.

2.  Em **Diretiva de nomenclatura de grupo**, configure o prefixo selecionando **texto** ou **atributo** no menu suspenso.
    
      - **Atributo**   Selecione o atributo e clique em **OK**.
    
      - **Texto**   Digite a cadeia de caracteres de texto e clique em **OK**.
    
    Observe que a cadeia de caracteres de texto que você digitou ou o atributo selecionado é exibido como um hiperlink. Clique no hiperlink para alterar a cadeia de caracteres de texto ou atributo.

3.  Clique em **Adicionar** para adicionar prefixos adicionais.

4.  Para o sufixo, no menu suspenso, selecione o **atributo** ou **texto** e configurar o sufixo.

5.  Clique em **Adicionar** para adicionar sufixos adicionais.
    
    Depois de adicionar um prefixo ou sufixo, observe que uma visualização do grupo de diretiva de nomenclatura é exibida.

6.  Para excluir um prefixo ou sufixo da política, clique em **Remover**![ícone Remover](images/JJ657492.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "ícone Remover").

7.  Clique em **Bloqueado palavras** para adicionar ou remover palavras bloqueadas.
    
      - Para adicionar uma palavra à lista, digite a palavra para bloquear e clique em **Adicionar**![Ícone Adicionar](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Ícone Adicionar").
    
      - Para remover uma palavra da lista, selecione-o e clique em **Remover**.
    
      - Para editar uma palavra bloqueada existente, selecione-o e clique em **Editar**.

8.  Quando você tiver concluído, clique em **Salvar**.

## Como saber se funcionou?

Para verificar se você criou com êxito um diretiva de nomenclatura de grupo, faça o seguinte:

  - No EAC, selecione **grupos** \> **mais** \> **grupo Configurar diretiva de nomenclatura**.
    
    Na página **diretiva de nomenclatura de grupo**, o política que você definiu de nomenclatura de grupo é exibido em **visualização da política**.

  - No Windows PowerShell, execute o seguinte comando para exibir o diretiva de nomenclatura de grupo.
    
        Get-OrganizationConfig | FL DistributionGroupNamingPolicy

