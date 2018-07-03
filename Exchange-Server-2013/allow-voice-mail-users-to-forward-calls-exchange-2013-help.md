---
title: 'Permitir usuários de email encaminhar chamadas de voz: Exchange 2013 Help'
TOCTitle: Permitir usuários de email encaminhar chamadas de voz
ms:assetid: 1f8e0a53-3d9d-4f8c-9be3-9f1e2a4347a3
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Dd335138(v=EXCHG.150)
ms:contentKeyID: 50556156
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Permitir usuários de email encaminhar chamadas de voz

 

_**Aplica-se a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Tópico modificado em:** 2013-02-22_

O recurso de Regras de Atendimento de Chamadas foi apresentado pela primeira vez no Exchange 2010. Ao usar esse recurso, os usuários que estão habilitados para caixa postal podem controlar como suas chamadas de entrada devem ser tratadas. As regras de atendimento de chamadas são aplicadas a chamadas de entrada de modo semelhante àquele com o qual as regras da Caixa de Entrada são aplicadas a mensagens de email de entrada.

As regras de atendimento de chamadas são criadas e configuradas por um usuário habilitado para caixa postal usando Outlook ou Outlook Web App. As regras são armazenadas junto com outras configurações de voz na caixa de correio do usuário. Um total de nove regras de atendimento de chamadas podem ser configuradas para cada caixa de correio habilitada para UM. Essas regras são independentes das regras de Caixa de Correio configuradas pelos usuários e não consomem uma parte da cota das regras de Caixa de Correio do usuário.

Por padrão, quando um usuário é habilitado para Unificação de Mensagens (UM) e caixa postal, nenhuma regra de atendimento de mensagens é configurada. Se uma chamada de entrada for atendida por um sistema de caixa postal, o chamador será solicitado a deixar uma mensagem de voz ou, se o chamador não receber uma solicitação, ele também conseguirá deixar uma mensagem de voz para a o usuário.

Se seus usuários quiserem que o sistema de caixa postal atenda suas chamadas de entrada e grave uma mensagem de voz, não será preciso criar nenhuma regra de atendimento de chamadas. Entretanto, se decidir configurar condições ou ações, você poderá fazê-lo usando a seção **Regras de Atendimento de Chamadas** da página **Caixa Postal** do Outlook Web App. Use a seção **Regras de Atendimento de Chamadas** para criar, editar e excluir regras de atendimento de chamadas.

## Anatomia das regras de atendimento de chamadas

Uma regra de atendimento de chamada tem duas partes: condições e ações. Você pode associar uma ou mais condições a uma única regra de atendimento de chamada. A regra de atendimento de chamada será processada somente se todas as condições dela forem cumpridas. Você pode associar uma ou mais ações a uma única regra de atendimento de chamada. Essas ações determinam que opções serão oferecidas ao chamador, quando a regra de atendimento de chamada for processada.

Regras de Atendimento de Chamada suportam as seguintes condições:

  - De quem é a chamada de entrada?

  - A hora do dia

  - Status de disponibilidade no calendário

  - Se respostas automáticas estão ativadas para email

Estas ações são suportadas:

  - Encontrar-me

  - Transferir o chamador para outra pessoa

  - Deixar uma mensagem de voz

Se um usuário gravar uma saudação personalizada para uma regra de atendimento de chamada, ele deve incluir a opção do menu como parte da saudação personalizada, quando configurar a regra de atendimento de chamada. Se ele não fizer isso, a Unificação de Mensagens não gerará um prompt de menu que deixa o chamador saber quais são suas escolhas. Após a reprodução da saudação personalizada, o servidor aguardará a mensagem do chamador. Se não for incluída uma opção de menu na saudação, o chamador não dirá nada e o servidor perguntará "Você ainda está aí?"

## Condições

As condições são regras que você pode aplicar às regras de atendimento de chamadas. Ao usar uma combinação de condições, você pode criar várias regras de atendimento de chamadas que serão disparadas quando as condições forem atendidas. Para criar uma regra-padrão que será aplicada a todas as chamadas, crie uma regra que não contenha nenhuma condição.

Há três condições que podem ser usadas quando você criar regras de atendimento de chamadas, incluindo:

  - ID do chamador

  - Hora do dia

  - Status de disponibilidade

## Ações

As ações são usadas para definir o que você quer que aconteça quando uma condição for atendida. Os dois tipos de ações são:

  - Encontrar-me

  - Transferência de chamadas

**Adição de uma ação de Localize-me**

Quando um chamador seleciona Localize-me, o sistema de caixa postal tentará localizar você em dois números de telefone diferentes e, depois, conectá-lo ao chamador, caso você esteja disponível em um desses números.

  - Você pode especificar o texto que será lido para o chamador. Por exemplo, se digitar \&quot;Assuntos Urgentes\&quot; para informar aos seus chamadores que eles só devem selecionar essa ação se tiverem algo importante a tratar com você, o sistema de caixa postal dirá "Para Assuntos Urgentes, pressione a tecla 1".

  - É preciso associar a ação Localize-me ao número do teclado numérico do telefone que o chamador deverá pressionar para selecionar a ação. No exemplo acima, a tecla **1** do telefone será o número que os chamadores irão pressionar para encontrá-lo em um dos números de telefone que você especificar.

  - Em seguida, você precisa especificar um ou dois números de telefone que o sistema de caixa postal discará. Se você especificar dois números de telefone, o segundo será discado caso você não esteja disponível no primeiro. Cada número de telefone que você especificar terá uma duração associada. A duração é o período em que o sistema de caixa postal tentará discar para o número do telefone antes de tentar o próximo número. Ou, se não for possível contatá-lo, o sistema de caixa postal voltará ao menu de opções.

  - Depois que tiver inserido essas informações, clique em **Aplicar** para salvar as configurações do Localize-me.

**Adicionando ações de Transferência de Chamadas**

Ao configurar uma ação de Transferência de Chamadas, você oferece aos chamadores a opção de serem transferidos para o número de telefone de outra pessoa. Há muitas opções disponíveis para a transferência de chamadas de entrada para outro telefone ou contato.

  - Você pode especificar o texto que será lido para o chamador. Por exemplo, você pode digitar \&quot;Assuntos Importantes\&quot; para informar aos seus chamadores que eles devem escolher essa opção se tiverem algo importante a tratar e se precisarem conversar com alguém.

  - É preciso associar a ação **Transferência de Chamadas** ao número do teclado numérico do telefone que o chamador deverá pressionar para selecionar a ação.

  - Ao escolher a ação Transferência de Chamadas, você terá que especificar uma pessoa ou número de telefone para o qual o chamador será transferido. Você pode escolher um número de telefone ou selecionar um contato a ser chamado quando o chamador pressionar a tecla correta no teclado numérico do telefone. Se você especificar um contato que esteja no diretório da sua empresa, o sistema de caixa postal tentará transferir a chamada para o número de ramal do contato.

  - Além de especificar uma pessoa ou número para transferir o chamador, também é preciso especificar o número do teclado numérico do telefone que o chamador deverá pressionar para selecionar a ação de Transferência de Chamadas.

  - Depois que tiver inserido essas informações, clique em **Aplicar** para salvar as configurações de Transferência de Chamadas.

## Selecionando uma regra de atendimento de chamada para cada chamada de entrada

Depois de criar e configurar as regras de Atendimento de Chamadas, a Unificação de Mensagens irá:

1.  Determinar se o usuário criou quaisquer regras de atendimento de chamada. Caso contrário, a UM irá oferece ao chamador a opção de deixar uma mensagem de voz.

2.  Se uma ou mais regras de atendimento de chamada tiverem sido configuradas, a UM irá avaliar cada uma dessas regras. A primeira regra cujas condições forem cumpridas será processada.

3.  Após avaliar todas as regras, se a um UM não localizar uma regra cujas condições sejam cumpridas, a UM irá pedir ao chamador para deixar uma mensagem de voz.

## Regras de discagem

Dependendo de como uma regra de atendimento de chamada for configurada, uma chamada de entrada pode resultar em uma transferência de chamada. Quando isso acontece, o número de telefone de destino estará sujeito às regras de discagem e às restrições na diretiva da caixa de correio da UM à qual quem recebeu a ligação está associado. Para obter mais informações sobre chamadas externas e regras e restrições de discagem, consulte [Permitir que os usuários façam chamadas](allow-users-to-make-calls-exchange-2013-help.md).

## Habilitando/desabilitando Regras de Atendimento de Chamada

Por padrão, as Regras de Atendimento de Chamada são automaticamente habilitadas para usuários habilitados para UM. Entretanto, você pode desabilitar as regras de atendimento de chamadas para usuários desabilitando o recurso em uma política de caixa de correio da UM ou da caixa de correio do usuário. Para detalhes sobre como habilitar ou desabilitar as Regras de Atendimento de Chamadas, consulte estes tópicos:

  - [Permitir ou impedir que os usuários na mesma política de caixa de correio de Unificação de mensagens criando regras de atendimento de chamada](allow-or-prevent-users-in-the-same-um-mailbox-policy-from-creating-call-answering-rules-exchange-2013-help.md)

  - [Permitir ou impedir que um usuário crie regras de atendimento de chamada](allow-or-prevent-a-user-from-creating-call-answering-rules-exchange-2013-help.md)

