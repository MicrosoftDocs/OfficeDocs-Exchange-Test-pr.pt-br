---
title: 'Agregação de Lista Segura: Exchange 2013 Help'
TOCTitle: Agregação de Lista Segura
ms:assetid: f05430a0-0405-4b65-a18d-18c9e86a13c4
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Bb125168(v=EXCHG.150)
ms:contentKeyID: 50486970
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Agregação de Lista Segura

 

_**Aplica-se a:**Exchange Server 2013_

_**Tópico modificado em:**2013-09-30_

No Microsoft Exchange Server 2013, a *agregação de lista segura* se refere à funcionalidade antispam compartilhada no Microsoft Outlook e no Exchange. Essa funcionalidade coleta dados das Listas de Destinatários Confiáveis, Listas de Remetentes Confiáveis, Listas de Remetentes Bloqueados e os dados de contatos configurados pelos usuários do Outlook, e disponibiliza esses dados para os agentes antispam do Exchange.

Quando você habilita e configura corretamente a agregação de lista segura, o agente Filtro de Conteúdo passa as mensagens de email confiáveis para a caixa de correio corporativa, sem processamento adicional. As mensagens de email que os usuários do Outlook recebem de contatos adicionados por esses usuários à Lista de Destinatários Confiáveis ou à Lista de Remetentes Confiáveis, do Outlook, são identificadas como seguras pelo agente Filtro de Conteúdo. Um *contato* do Outlook é uma pessoa interna ou externa à organização do usuário, sobre quem o usuário pode salvar vários tipos de informação; por exemplo, endereços de email e físicos, números de telefone e fax e URLs de páginas da Web.

No Exchange 2013, o processo de agregação de lista segura também permite que o agente Filtragem de Remetente bloqueie mensagens de entrada provenientes da Lista de Remetentes Bloqueados, por destinatário.

A agregação de lista segura pode ajudar a reduzir as ocorrências de falsos positivos na filtragem antispam executada pelo Exchange. No contexto da filtragem antispam, um *falso positivo* ocorre quando um filtro de spam identifica incorretamente uma mensagem legítima como spam.

Para as organizações que filtram centenas de milhares de mensagens provenientes da Internet, todos os dias, mesmo uma pequena porcentagem de falsos positivos significa que os usuários podem não receber muitas mensagens identificadas indevidamente como spam, caso essas mensagens sejam colocadas em quarentena ou excluídas.

A agregação de lista segura é, provavelmente, a maneira mais eficaz de reduzir falsos positivos. No Outlook 2010 ou em versões mais recentes, os usuários podem criar *Listas de Remetentes Confiáveis*. As Listas de Remetentes Confiáveis especificam uma lista de nomes de domínio e endereços de email, dos quais os usuários do Outlook querem receber mensagens. Por padrão, os endereços de email dos contatos do Outlook e a lista global de endereços do Exchange são incluídas nessa lista. Por padrão, o Outlook adiciona todos os contatos externos, para os quais o usuário envia emails, à Lista de Remetentes Confiáveis.

**Sumário**

Information stored in the Outlook user's safelist collection

How Exchange uses the safelist collection

Hashing of safelist collection entries

Enabling safelist aggregation

## Informações armazenadas no conjunto de listas seguras do usuário do Outlook

Um *conjunto de listas seguras* é a combinação de dados da Lista de Remetentes Confiáveis, da Lista de Destinatários Confiáveis, da Lista de Remetentes Bloqueados e de contatos externos do usuário. Esses dados são armazenados na caixa de correio do Outlook e do Exchange.

Os seguintes tipos de informações são armazenados no conjunto de listas seguras do usuário do Outlook:

  - **Remetentes e destinatários confiáveis**   O cabeçalho de mensagem De indica um remetente. O campo Para da mensagem de email indica um destinatário. Remetentes e destinatários seguros são representados por endereços SMTP completos; por exemplo, masato@contoso.com. Os usuários do Outlook podem adicionar remetentes e destinatários às suas listas seguras.

  - **Remetentes bloqueados**   Assim como os remetentes confiáveis, os usuários podem bloquear remetentes indesejados adicionando-os às Listas de Remetentes Bloqueados.

  - **Domínio seguro**   O domínio é a parte de um endereço SMTP que se segue ao símbolo @. Por exemplo, contoso.com é o domínio no endereço masato@contoso.com. Os usuários do Outlook podem adicionar domínios de envio às suas listas seguras.
    

    > [!IMPORTANT]
    > Por padrão, o Exchange não inclui domínios durante a agregação de lista segura. Entretanto, você pode configurar a agregação de lista segura para incluir dados de domínios seguros para os agentes antispam. Para saber mais, veja <A href="configure-content-filtering-to-use-safe-domain-data-exchange-2013-help.md">Configurar a filtragem para usar os dados de domínio seguro de conteúdo</A>.



  - **Contatos externos** Dois tipos de contatos externos podem ser incluídos na agregação de lista segura. O primeiro tipo de contato externo inclui contatos para os quais os usuários do Outlook enviaram emails. Essa classe de contato será adicionada à Lista de Remetentes Confiáveis apenas se o usuário do Outlook selecionar a opção correspondente, nas configurações de Lixo Eletrônico do Outlook 2007.
    
    O segundo tipo de contato externo inclui os contatos do Outlook. Os usuários podem adicionar ou importar esses contatos no Outlook. Essa classe de contato será adicionada à Lista de Remetentes Confiáveis apenas se o usuário do Outlook selecionar a opção correspondente, nas configurações de Filtro de Lixo Eletrônico do Outlook 2010 ou do Outlook 2007.

Voltar ao início

## Como o Exchange usa o conjunto de listas seguras

O conjunto de listas seguras é armazenado no servidor de caixas de correio do usuário. Um usuário pode ter até 1.024 entradas exclusivas em um conjunto de listas seguras. O Exchange 2013 tem um assistente de caixa de correio, chamado Opções de Lixo Eletrônico, que monitora as alterações feitas nos conjuntos de listas seguras das suas caixas de correio. Essas alterações são então replicadas para o Active Directory, onde o conjunto de listas seguras é armazenada em cada objeto de usuário. Quando o conjunto de listas seguras é armazenado no objeto de usuário, no Active Directory, o conjunto de listas seguras é agregado à funcionalidade antispam do Exchange 2013 e é otimizado para armazenamento e replicação minimizados. O Exchange usa os dados do conjunto de listas seguras durante a filtragem de conteúdo. Se tiver um servidor Transporte de Borda assinado na sua rede de perímetro, o serviço Microsoft Exchange EdgeSync replicará o conjunto de listas seguras para a instância do AD LDS (Active Directory Lightweight Directory Services), no servidor Transporte de Borda.


> [!IMPORTANT]
> Embora os dados de destinatários confiáveis sejam armazenados no Outlook e possam ser agregados ao conjunto de listas seguras, a funcionalidade de filtragem de conteúdo não age sobre os dados de destinatários confiáveis.



Voltar ao início

## Usando hash de entradas do conjunto de listas seguras

As entradas do conjunto de listas seguras são submetidas a hash (SHA-256) uma vez antes de serem armazenadas como conjuntos de matrizes nos três atributos de objeto de usuário, **msExchSafeSenderHash**, **msExchSafeRecipientHash** e **msExchBlockedSendersHash**, como um objeto binário grande. Quando os dados são submetidos a hash, uma saída de tamanho fixo é produzida, e a saída provavelmente será exclusiva. Para hash de entradas de conjunto de listas seguras, um hash de 4 bytes é produzido. Quando uma mensagem é recebida da Internet, o Exchange usa o hash no endereço do remetente e o compara aos hashes armazenados em nome do usuário do Outlook, para quem a mensagem foi enviada. Se o remetente corresponder ao hash de remetentes confiáveis, a mensagem será ignorada pela filtragem de conteúdo. Se o remetente corresponder ao hash de remetentes bloqueados, a mensagem será bloqueada.

O uso de hash unidirecional das entradas do conjunto de listas seguras executa estas funções importantes:

  - **Minimiza o espaço de armazenamento e replicação**   Na maior parte do tempo, o hash reduz o tamanho dos dados com hash. Portanto, salvar e transmitir uma versão com hash de uma entrada do conjunto de listas seguras preserva espaço de armazenamento e tempo de replicação. Por exemplo, um usuário que tenha 200 entradas no conjunto de listas seguras criará aproximadamente 800 bytes de dados com hash, armazenados e replicados no Active Directory.

  - **Renderiza conjuntos de listas seguras do usuário não utilizáveis por usuários mal-intencionados**   Na medida que é impossível aplicar engenharia reversa aos valores com hash unidirecional, no endereço ou domínio SMTP original, os conjuntos de listas seguras não produzem endereços de email que possam ser usados por usuários mal-intencionados, os quais poderiam comprometer um servidor Exchange.

Voltar ao início

## Habilitando a agregação de lista segura

A agregação de lista segura está habilitada, por padrão, no Exchange 2013. Diferentemente do Exchange Server 2007, não é preciso executar manualmente o cmdlet **Update-SafeList** para suar hash e gravar os dados do conjunto de listas seguras no Active Directory. No Exchange 2013, os dados do conjunto de listas seguras são gravados no Active Directory pelo assistente de caixa de correio Opções de Lixo Eletrônico.

Para disponibilizar os dados de agregação de lista segura, no Active Directory, para os servidores de Transporte de Borda na rede de perímetro, você precisa instalar e configurar o serviço Microsoft Exchange EdgeSync, para que os dados da agregação de lista segura sejam replicados para o AD LDS.

Você também pode executar manualmente a agregação de lista segura usando o cmdlet **UpdateSafelist**. Entretanto, é preciso ter em mente o tráfego de rede e replicação que pode ser gerado durante a execução desse comando. A execução de **Update-Safelist** em várias caixas de correio, nas quais as listas seguras são intensamente usadas, pode gerar uma quantidade significativa de tráfego. Recomendamos que, se você executar o comando em vários caixas de correio, você o execute durante os horários não comerciais, fora do pico.

O cmdlet **Update-SafeList** lê o conjunto de listas seguras na caixa de correio do usuário, aplica hash em cada entrada, classifica as entradas para facilitar a pesquisa e então converte o hash em um atributo binário. Por fim, o cmdlet **Update-SafeList** compara o atributo binário que foi criado para qualquer valor armazenado no atributo. Se os dois valores forem idênticos, o cmdlet **Update-SafeList** não atualizará o valor de atributo de usuário com os dados da agregação de lista segura. Se os dois valores de atributo forem diferentes, o cmdlet **Update-SafeList** atualizará o valor da agregação de lista segura.

Voltar ao início

