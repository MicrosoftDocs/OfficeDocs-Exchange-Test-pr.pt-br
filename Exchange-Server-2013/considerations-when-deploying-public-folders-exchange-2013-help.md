---
title: 'Considerações ao implantar a pastas públicas: Exchange 2013 Help'
TOCTitle: Considerações ao implantar a pastas públicas
ms:assetid: 2e416eed-b88f-45db-a482-1232fd2610fa
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Dn957481(v=EXCHG.150)
ms:contentKeyID: 65010732
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Considerações ao implantar a pastas públicas

 

_**Aplica-se a:**Exchange Server 2013_

_**Tópico modificado em:**2016-07-12_

Embora existam muitas vantagens em usar pastas públicas do Exchange 2013, há algumas coisas a considerar antes de implementá-las em sua organização.

## Considerações de implantação para pastas públicas

Este artigo contém os fatores a serem considerados antes de implantar as pastas públicas em sua organização, especialmente se você planeja tiver um grande número de pastas públicas. Agora, o Exchange 2013 oferece suporte a até um milhão de pastas públicas.

  - Atividade em uma pasta pública diretamente afeta a carga que é colocada na caixa de correio de pasta pública em que a pasta está localizada. Para evitar problemas de conectividade de cliente, como alta latência ou a incapacidade de acessar uma pasta pública, recomendamos que você faça o seguinte:
    
      - Não deixe as caixas de correio de pasta pública exceder o limite de tamanho de caixa de correio 50%. Se isso acontecer, considere usar o script `Split-PublicFolderMailbox.ps1` localizado na pasta C:\\Program Files\\Microsoft\\Exchange Server\\V15\\Scripts no servidor Exchange 2013 para mover algumas pastas públicas para uma nova caixa de correio de pasta pública.
    
      - Considere a possibilidade de movimentação das pastas públicas usado intensamente uma caixa de correio de pasta pública dedicado.
    
      - Exclua pastas públicas usado intensamente de atendendo a hierarquia de pastas públicas. Você pode fazer isso, definindo a propriedade *IsExcludedFromServingHierarchy* na caixa de correio de pasta pública usando o cmdlet **Set-Mailbox** .
    
      - Para grandes organizações com muitas pastas públicas, considere a adição de caixas de correio de pasta pública adicionais para distribuir a carga de atender às solicitações da hierarquia de pasta pública.

  - Coloque a caixa de correio de pasta pública principal em um DAG para aumentar a disponibilidade da caixa de correio. A caixa de correio de pasta pública principal é a cópia autoritativa da hierarquia de pasta pública.

  - Coloque caixas de correio de pasta pública secundária em um DAG ou backup as caixas de correio frequentemente.

  - Coloque caixas de correio de pasta pública no local geográfico que está mais próximo dos usuários que acessarão o conteúdo de pasta pública neles.

  - Melhorar o tempo de acesso de hierarquia de pastas públicas, usando a propriedade DefaultPublicFolderMailbox em caixas de correio dos usuários para especificar uma caixa de correio de pastas públicas e está perto-los. Isso impedirá que os usuários Recuperando a hierarquia de pasta pública de uma caixa de correio de pasta pública em outras localidades geográficas.

  - Nas implantações com mais de 50 caixas de correio de pastas públicas secundário, recomendamos que você não armazene o conteúdo da pasta pública na caixa de correio de pasta pública principal. Isso dedica a caixa de correio de pasta pública principal para sincronizar a hierarquia com as caixas de correio de pasta pública secundária.

  - Exchange 2013 não oferece suporte para bancos de dados de pasta pública. Portanto, os usuários do Outlook Web App com caixas de correio do Exchange 2013 não poderão acessar pastas públicas do Exchange 2010 ou Exchange 2007. Usuários do Exchange 2013 podem acessar pastas públicas do Exchange 2010 ou Exchange 2007 com o Outlook ou o Outlook para Mac.

  - Há suporte para o Outlook Web App, mas com limitações. Você pode adicionar e remover pastas públicas favoritas e realizar operações em nível de item, como criar, editar, excluir postagens e responder a postagens. No entanto, você não pode criar nem excluir pastas públicas do Outlook Web App. Além disso, apenas as pastas públicas Email, Postagem, Calendário e Contatos podem ser adicionadas à lista de favoritos no Outlook Web App.

  - Embora uma pesquisa de texto completo de conteúdo de pastas públicas esteja disponível, o conteúdo de pasta pública não é pesquisável em pastas públicas, e o conteúdo não é indexado pela Pesquisa do Exchange.

  - É necessário usar o Outlook 2007 ou posterior para acessar pastas públicas em servidores Exchange 2013.

  - Não há suporte a políticas de retenção para caixas de correio de pastas públicas.

