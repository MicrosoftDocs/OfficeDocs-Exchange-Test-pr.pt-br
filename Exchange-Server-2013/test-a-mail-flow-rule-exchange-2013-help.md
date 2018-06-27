---
title: 'Testar uma regra de fluxo de email: Exchange Online Protection Help'
TOCTitle: Testar uma regra de fluxo de email
ms:assetid: 3d949e2a-8ba4-4261-8cfb-736fd2446ea1
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Dn831862(v=EXCHG.150)
ms:contentKeyID: 63144002
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Testar uma regra de fluxo de email

 

_**Aplica-se a:**Exchange Online, Exchange Online Protection, Exchange Server 2013_

_**Tópico modificado em:**2016-12-09_

Cada vez que você cria uma regra de fluxo de email do Exchange, também conhecida como uma regra de transporte, você deve testá-lo antes de ativá-la. Dessa forma, se você criar acidentalmente uma condição que não faz exatamente o que deseja ou interage com outras regras de maneiras inesperadas, não terão qualquer consequências indesejadas.


> [!IMPORTANT]
> Aguarde 30 minutos após a criação de uma regra antes de você testá-lo. Se você testar imediatamente após a criação da regra, você pode obter comportamento inconsistente. Se você estiver usando o Exchange Server e tiver vários servidores Exchange, ele pode demorar até mesmo mais para todos os servidores receber a regra.



## Etapa 1: Criar uma regra no modo de teste

Você pode avaliar as condições de uma regra sem tomar as medidas que têm impacto sobre o fluxo de emails, escolhendo um modo de teste. Você pode configurar uma regra de modo que você receber uma notificação de e-mail sempre que a regra é correspondida, ou você pode examinar o rastreamento da mensagem para mensagens que correspondam a regra. Há dois modos de teste:

  - **Teste sem dicas de política**    Use este modo junto com uma ação de relatório de incidente e você poderá receber uma mensagem de email, um email de cada vez que corresponda à regra.

  - **Testar com dicas de política**    Esse modo só estará disponível se você estiver usando o [Prevenção de perda de dados](technical-overview-of-dlp-data-loss-prevention-in-exchange.md) (DLP), que está disponível com algumas Exchange Online e Proteção do Exchange Online (EOP) planos de assinatura. Com esse modo, uma mensagem é definida para o remetente quando uma mensagem que estão enviando corresponde a uma política, mas nenhum ações de fluxo de email são colocadas.

Aqui está o que você verá quando uma regra é correspondida se você incluir a ação de relatório de incidente:

![Mensagem enviada quando a regra é detectada](images/Dn831862.c1a2db60-3fb9-4ddc-86d5-1757e2250f59(EXCHG.150).png "Mensagem enviada quando a regra é detectada")

Use um modo de teste com uma ação de relatório de incidente

1.  No Centro de administração do Exchange (EAC), vá para **fluxo de emails** \> **regras**.

2.  Criar uma nova regra, ou selecione uma regra existente e selecione **Editar**.

3.  Role até a seção **Escolher um modo para essa regra** e selecione **teste sem dicas de política** ou **testar com dicas de política**.

4.  Adicione uma ação de relatório de incidente:
    
    1.  Selecione a **ação Add** ou, se não estiver visível, selecione **mais opções** e selecione **Adicionar ação**.
    
    2.  Selecione **Generate incidente relatar e enviá-lo para**.
    
    3.  Clique em **Selecionar uma …** e selecione sozinho ou outra pessoa.
    
    4.  Selecione **incluir propriedades de mensagem** e selecione Propriedades qualquer mensagem que deseja incluir no email que receber. Se você não selecionar nenhum, você ainda receberá um email quando a regra é correspondida.

5.  Selecione **Salvar**.

## Etapa 2: Avalie se sua regra faz o que você pretende

Para testar uma regra, você pode enviá suficiente mensagens de teste para confirmar se o que você espera que acontece ou olhar sobre a mensagem de rastreamento de mensagens que as pessoas na sua organização de envio. Certifique-se de avaliar os seguintes tipos de mensagens:

  - Mensagens que você espera que correspondem à regra

  - Mensagens que você não espera que correspondem à regra

  - Mensagens enviadas de e para pessoas da sua organização

  - Mensagens enviadas de e para pessoas fora da sua organização

  - Respostas às mensagens que correspondem à regra

  - Mensagens que podem causar a interações entre várias regras

## Dicas para enviar mensagens de teste

Uma maneira de teste deve entrar como o remetente e o destinatário de uma mensagem de teste.

  - Se você não tem acesso a várias contas em sua organização, você pode testar em uma [conta de avaliação do Office 365](https://go.microsoft.com/fwlink/p/?linkid=402791) ou criar alguns usuários falsos temporários em sua organização.

  - Porque um navegador da web geralmente não permitirá que você tiver simultâneo de sessões abertas no mesmo computador conectado ao várias contas, você pode usar o [Internet Explorer Navegação InPrivate](https://go.microsoft.com/fwlink/p/?linkid=402784), ou um computador diferente, dispositivo ou navegador da web para cada usuário.

## Examine o rastreamento de mensagens

O rastreamento de mensagem inclui uma entrada para cada regra correspondente para a mensagem e o leva uma entrada para cada ação de regra. Isso é útil para controlar o que acontece às mensagens de teste e também para controlar o que acontece às mensagens reais precisar passar por sua organização.

![Rastreamento de mensagens mostrando ações da regra de transporte](images/Dn831862.64179f28-5c8c-421b-b630-cc1f7de9a34f(EXCHG.150).png "Rastreamento de mensagens mostrando ações da regra de transporte")

1.  No EAC, vá para **fluxo de email** \> **rastreamento de mensagens**.

2.  Encontre as mensagens que você deseja rastrear usando critérios como o remetente e a data de envio. Para obter ajuda sobre como especificar critérios, consulte [Executar um rastreamento de mensagem e exibir os resultados](https://technet.microsoft.com/pt-br/library/jj200712\(v=exchg.150\)).

3.  Após localizar a mensagem que você deseja rastrear, clique duas vezes nele para exibir detalhes sobre a mensagem.

4.  Procure na coluna **eventoregra de transporte**. A coluna **ação** mostra a ação específica tomada.

## Etapa 3: Quando terminar o teste, definido para impor a regra

1.  No EAC, vá para **Fluxo de emails** \> **Regras**.

2.  Selecione uma regra e selecione **Editar**.

3.  Selecione **impor**.

4.  Se você tiver usado uma ação para gerar um relatório de incidente, selecione a ação e selecione **Remover**.

5.  Selecione **Salvar**.


> [!TIP]
> Para evitar surpresas, informe seus usuários sobre as novas regras.



## Sugestões de solução de problemas

Aqui estão alguns problemas comuns e as resoluções:

  - **Tudo parece certo, mas a regra não está funcionando.**
    
    Ocasionalmente, levará mais de 15 minutos para um novo fluxo de email esteja disponível. Aguarde algumas horas e teste novamente. Também verificar se outra regra pode ser interferência. Tente alterar esta regra para prioridade 0, movendo-o para o topo da lista.

  - **Isenção de responsabilidade é adicionada à mensagem original e todas as respostas, em vez de apenas a mensagem original.**
    
    Para evitar isso, você pode adicionar uma exceção à sua regra de isenção de responsabilidade para procurar uma frase exclusiva na isenção de responsabilidade.

  - **Minha regra tem duas condições e eu quero que a ação a ser acontecer quando alguma das condições for atendida, mas ele só é correspondido quando ambas as condições forem atendidas.**
    
    Você precisa criar duas regras, uma para cada condição. Você pode copiar facilmente a regra selecionando **cópia** e, em seguida, remover uma condição do original e a outra condição da cópia.

  - **Estou trabalhando com grupos de distribuição e** **O remetente é** (**SentTo** ) **não parece estar funcionando.**
    
    **SentTo** corresponde a mensagens em que um dos destinatários é uma caixa de correio, usuário habilitado para email, ou contato, mas você não pode especificar um grupo de distribuição com essa condição. Em vez disso, use o **para a caixa contém um membro desse grupo** (**SentToMemberOf** ).

## Outras opções de teste

Se você estiver usando Exchange Online ou Proteção do Exchange Online, você pode verificar o número de vezes que cada regra é correspondida usando um relatório de regras. Para ser incluído nos relatórios, uma regra deve ter a caixa de seleção **Auditar esta regra com nível de severidade** selecionada. Esses relatórios ajudam você a identificar tendências no uso da regra e identificar as regras que não são correspondentes.

Para exibir um relatório de regras no Centro de administração do Office 365, selecione **relatórios**.


> [!TIP]
> Embora a maioria dos dados esteja no relatório dentro de 24 horas, alguns dados podem demorar até 5 dias para aparecer.



![Relatório mostrando o uso da regra](images/Dn831862.df5bf202-741d-432a-b71d-b37143f0ec0a(EXCHG.150).png "Relatório mostrando o uso da regra")

Para saber mais, consulte [Exibir relatórios de proteção de email](https://go.microsoft.com/fwlink/p/?linkid=402958).

## Precisa de mais ajuda?

[Gerenciar regras de fluxo de emails](manage-mail-flow-rules-exchange-2013-help.md)

[Regras de fluxo de emails (regras de transporte) no Exchange Online](https://technet.microsoft.com/pt-br/library/jj919238\(v=exchg.150\)) (Exchange Online)

[Regras de fluxo de emails (regras de transporte) no Exchange Online Protection](https://technet.microsoft.com/pt-br/library/dn271424\(v=exchg.150\)) (Proteção do Exchange Online)

[Regras de fluxo de emails ou de transporte](mail-flow-rules-transport-rules-in-exchange-2013-exchange-2013-help.md) (Exchange Server)

