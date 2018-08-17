---
title: 'Outlook for iOS and Android: Exchange 2013 Help'
TOCTitle: Outlook for iOS and Android
ms:assetid: 3a66817c-30da-4965-a6db-2955b5365b0f
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Mt465744(v=EXCHG.150)
ms:contentKeyID: 70061448
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Outlook for iOS and Android

 

_**Aplica-se a:** Exchange Server 2010, Exchange Server 2013_

_**Tópico modificado em:** 2018-04-02_

**Resumo:**  Este artigo contém arquiteturais e informações de segurança para administradores sobre o Outlook para iOS e Android em um Exchange 2013 ambiente local.

O aplicativo do Outlook para o iOS e Android é projetado para reunir email, calendário, contatos e outros arquivos, permitindo que os usuários em sua organização fazer mais de seus dispositivos móveis. Este artigo fornece uma visão geral da arquitetura e o design de armazenamento do aplicativo, para que os administradores do Exchange podem implantar e manter o Outlook para iOS e Android em suas organizações do Exchange.


> [!NOTE]
> O <A href="https://support.office.com/en-us/article/outlook-for-ios-and-android-help-center-cd84214e-a5ac-4e95-9ea3-e07f78d0cde6">Outlook para o Centro de Ajuda do Android e iOS</A> está disponível para usuários, incluindo a Ajuda para usando o app em dispositivos específicos e informações de solução de problemas.



## Arquitetura do Outlook para iOS e Android

Outlook para iOS e Android consiste em um aplicativo de front-end que é instalado em dispositivos móveis e um serviço em nuvem segura e escalável no back-end, conhecido como o *serviço do Outlook*. Processamento de informações no serviço do Outlook permite que os recursos que aprimoram a experiência do Outlook, bem como o melhor desempenho e a estabilidade e recursos avançados. Essa arquitetura baseia-se no serviço do Outlook para uso intenso processamento, minimizando os recursos exigidos de dispositivos dos usuários.

Exemplos de como o que o servidor do Outlook fornece aos usuários:

  - Categorização de entrada focada.

  - Um clique Cancelar a assinatura de recurso de listas de distribuição.

  - Melhore a eficiência e rapidez de pesquisa.

  - A capacidade de encaminhar e enviar arquivos grandes sem primeiro baixá-los para um dispositivo móvel.

## Cache de dados

Para obter melhor desempenho, um subconjunto de email, calendário e dados de arquivo da caixa de correio de cada usuário é armazenado em cache no serviço do Outlook. Esse serviço é executado no momento Microsoft Azure. Podemos estiver movendo o serviço do Outlook para o Office 365 e planeje ter essa movimentação concluída em breve.

As informações no serviço do Outlook está atualmente armazenados em cache nos Estados Unidos ou na Europa, dependendo do endereço IP do cliente conectado. À medida que passamos o serviço do Outlook ao Office 365, podemos será alinhar os princípios de centro de confiança do Office 365 com uma estratégia de centro de dados regionalizado. No Office 365 país ou região, que o administrador do cliente durante a configuração inicial dos serviços de entradas, de um cliente determina o local de armazenamento primário para os dados do cliente. Para obter mais informações, consulte [A Central de confiabilidade do Office 365](https://go.microsoft.com/fwlink/p/?linkid=525776).

## Perguntas frequentes sobre o cache de dados

A seguir é perguntas frequentes sobre o armazenamento de dados no Outlook para iOS e Android.

## A quantidade de dados de caixa de correio do usuário é armazenado em cache no serviço do Outlook?

Aproximadamente um mês de email, calendário e dados de contato. O processo de cache é determinado por um algoritmo que contas, entre outros fatores, o tamanho de uma caixa de correio, a importância relativa de uma determinada pasta dentro da caixa de correio (por exemplo, a caixa de entrada pasta padrão em comparação com uma pasta que foi criada pelo usuário), e com que frequência um usuário acessa uma determinada pasta.

O serviço de Outlook armazena dados de anexo da seguinte maneira: quando um usuário solicita para abrir um anexo de email no Outlook, o serviço recupera o anexo do Exchange server e a armazena temporariamente. Nesse momento, o anexo é entregue para o aplicativo no dispositivo móvel do usuário. Dados mais antigos do que um mês é rotineiramente esvaziado fora de serviço, na qual aponte o anexo só estará disponíveis no Exchange server.

## Como remover minhas informações do serviço do Outlook?

Você tem três opções para remover as informações do serviço do Outlook.

  - Opção 1: Inicie um apagamento remoto para cada usuário que usou o aplicativo do Outlook para o iOS e Android para se conectar ao Office 365 ou Exchange.

  - Opção 2: Têm todos os usuários de excluir o aplicativo do Outlook. Todos os dados serão removidos em aproximadamente de 3 a 7 dias.

  - Opção 3: Com que cada usuário remover suas contas do Outlook app e exclua o aplicativo de seus dispositivos móveis. Para remover uma conta, tiver usuários siga estas etapas:
    
    1.  No Outlook app, nas **configurações**, toque em **Configurações de conta**.
    
    2.  **Selecione uma conta** de toque e, com a conta selecionada, toque em **Conta remover**.
    
    3.  Toque em **dispositivo & dados remotos**.

## Como os dados de caixa de correio armazenado em cache temporariamente são protegidos enquanto armazenadas no serviço do Outlook?

Você pode ler sobre como os nossos dados são protegidos no momento na [Central de confiabilidade do Azure](https://azure.microsoft.com/support/trust-center/). Conforme observado anteriormente, estamos passando do Windows Azure para o Office 365. A segurança desses serviços é abordada no [Centro de confiança do Office 365](https://go.microsoft.com/fwlink/p/?linkid=525776).

