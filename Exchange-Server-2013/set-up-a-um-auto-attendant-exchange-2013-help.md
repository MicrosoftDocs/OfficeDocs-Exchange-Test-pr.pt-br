---
title: 'Configurar um atendedor automático: Exchange 2013 Help'
TOCTitle: Configurar um atendedor automático
ms:assetid: 0a3492f8-8aba-4904-96fd-6e023175012a
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/JJ673508(v=EXCHG.150)
ms:contentKeyID: 50484982
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configurar um atendedor automático

 

_**Aplica-se a:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Tópico modificado em:**2015-03-09_

Além de permitir que os usuários acessem a caixa postal, a Unificação de Mensagens (UM) permite que você crie um ou mais atendedores automáticos de UM, dependendo das necessidades da sua organização. Os atendedores automáticos de UM podem ser usados para criar um sistema de menus de voz para um organização que permita, aos chamadores externos e internos, localizar, fazer ou transferir chamadas para usuários da companhia ou departamentos em uma organização.

Para conhecer tarefas de gerenciamento adicionais relacionadas a atendedores automáticos de UM, consulte [Procedimentos atendedor automático a Unificação de mensagens](um-auto-attendant-procedures-exchange-2013-help.md).

## Atendedores automáticos

Em ambientes de telefonia ou de Unificação de Mensagens, um atendedor automático ou um sistema de menus de atendedor automático transfere os chamadores para o ramal de um usuário ou de um departamento sem a intervenção de uma recepcionista ou um operador. Em muitos sistemas de atendedor automático, é possível entrar em contato com uma recepcionista ou um operador pressionando ou dizendo zero. Em alguns sistemas de atendedor automático, existem menus de informações somente para mensagens e menus de voz que são usados para que uma organização possa comunicar o horário de atendimento, instruções sobre as instalações, informações sobre oportunidades de emprego e respostas a outras perguntas freqüentes. Depois que a mensagem é reproduzida, o chamador é encaminhado à recepcionista ou ao operador ou retorna ao menu principal.

Embora possam ser muito úteis, se os atendedores automáticos não forem projetados e configurados corretamente, eles poderão confundir e frustrar os chamadores. Por exemplo, principalmente em grandes organizações, quando os atendedores automáticos não são projetados corretamente, os chamadores podem passar por uma série interminável de perguntas e prompts de menus antes de serem finalmente transferidos a uma pessoa que responda à sua pergunta.

## Como eu configuro um atendedor automático?

No Centro de Administração do Exchange (ECA), você pode configurar e gerenciar atendedores automáticos de UM para atender automaticamente chamadas para sua organização e permitir que os chamadores selecionem diferentes opções com as teclas do telefone. Você pode ter apenas um atendedor automático do UM que ofereça navegação de menu básica aos chamadores da sua organização ou vários atendedores automáticos aninhados e ramificados que ofereçam uma experiência mais rica aos seus chamadores. Entretanto, em ambos os casos, você deve planejar e configurar seus atendedores automáticos cuidadosamente.

Para planejar e criar uma nova estrutura de atendedor automático de UM, você precisa fazer o seguinte:

1.  Decida se você deseja permitir que os usuários interajam com o atendedor automático, usando entradas de fala.

2.  Decida que idioma você deseja usar para seu atendedor automático principal e se você precisa criar outros atendedores automáticos, para suportar mais idiomas.

3.  Decida o horário comercial e o não comercial para o atendedor automático e defina o horário comercial usando **Horário comercial**. Apesar de isso não ser obrigatório, você também pode escolher os horários de feriado para esse atendedor automático.
    

    > [!TIP]
    > Você também deve definir o fuso horário no atendedor.



4.  Decida se você deseja saudações padrão geradas pelo sistema ou criar gravações personalizadas para os horários comercial e não comercial.
    
    Se você quiser usar saudações personalizadas, planeje e grave saudações para os horários comercial e não comercial, para serem reproduzidas para os chamadores nos respectivos horários. Se você precisar, também poderá criar uma saudação de anúncio informacional. Por exemplo, na saudação de horário comercial, você pode usar "Bem-vindo à Contoso. Para português, pressione ou diga 1; para espanhol, pressione ou diga 2." Para a saudação de horário não comercial, você poderia gravar este script: "Bem-vindo à Contoso. Nosso escritório está fechado no momento. Nós abriremos na segunda-feira às 08:00."

5.  Planeje sua estrutura de atendedor automático baseada em suas necessidades de negócios. Por exemplo, uma organização pode ser uma empresa multinacional, com escritórios tanto na Alemanha quanto no Reino Unido e, assim, precisar de uma estrutura de atendedor automático com base em vários idiomas. Outra organização pode ter seu escritório corporativo em um local, as Vendas em outro e o Atendimento ao Cliente em outro ainda, precisando de um atendedor automático que se relacione diretamente à estrutura da organização.

6.  Decida se você precisa de atendedores automáticos de fallback de DTMF ou outros atendedores automáticos para usar quando os comandos de voz do atendedor não funcionarem.

7.  Planeje a navegação de menu para horário comercial e horário não comercial. Para cada atendedor automático, incluindo os do DTMF, você precisará planejar e configurar os prompts de menu e as entradas de navegação do menu. Você precisará fazer isso tanto para o horário comercial quanto para o não comercial.

8.  Veja a seguir o exemplo de uma planilha que poderia ser usada para planejar a navegação de menu em horários não comerciais.
    
    
    <table>
    <colgroup>
    <col style="width: 33%" />
    <col style="width: 33%" />
    <col style="width: 33%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th><strong>Tecla</strong></th>
    <th><strong>Nome de entrada de menu de navegação/prompt</strong></th>
    <th><strong>Resposta a ser gravada</strong></th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td><p>1</p></td>
    <td><p>Seleção de idioma para usar português.</p></td>
    <td><p>&quot;Pressione ou diga 1 para usar português.&quot;</p></td>
    </tr>
    <tr class="even">
    <td><p>2</p></td>
    <td><p>Saldo da conta</p></td>
    <td><p>&quot;Pressione ou diga 2 para saber o saldo da sua conta.&quot;</p></td>
    </tr>
    <tr class="odd">
    <td><p>3</p></td>
    <td><p>Transferir para Vendas</p></td>
    <td><p>&quot;Pressione ou diga 3 para ser transferido para o nosso departamento de vendas.&quot;</p></td>
    </tr>
    <tr class="even">
    <td><p>4</p></td>
    <td><p>Transferir para o atendimento ao cliente</p></td>
    <td><p>&quot;Pressione ou dia 4 para ser transferido para um representante do atendimento ao cliente.&quot;</p></td>
    </tr>
    <tr class="odd">
    <td><p>5</p></td>
    <td><p>Horário comercial</p></td>
    <td><p>Nenhuma resposta necessária.</p></td>
    </tr>
    <tr class="even">
    <td><p>6</p></td>
    <td><p>Local da empresa</p></td>
    <td><p>Nenhuma resposta necessária.</p></td>
    </tr>
    </tbody>
    </table>


9.  Com seu plano de navegação de menu, grave prompts que informem os chamadores sobre o que eles podem fazer. Por exemplo, dependendo da estrutura do atendedor automático da navegação de menu para horários não comerciais mostrada na tabela, você poderia gravar o script a seguir: Por exemplo, para a navegação de menu em horário não comercial, mostrada na tabela, você poderia gravar este script: "Para deixar uma mensagem para Vendas, pressione 1. Para obter nosso horário comercial, pressione 2. Para obter nosso endereço, pressione 3."

10. Determine como os chamadores terão acesso à sua organização. Considere como eles irão procurar e fazer contato com os usuários em sua organização. Também pense em como transferir chamadores, incluindo como eles irão fazer contato com uma pessoa ativa ou representante da organização, e se os chamadores irão acessar um operador, durante os horários comercial e não comercial.

11. Determine que chamadas você permitirá que os chamadores façam, quando estiverem usando um atendedor automático específico. Por exemplo, se você deseja permitir que os chamadores liguem para usuários em um só plano de discagem, para qualquer ramal, ou se você irá permitir que eles façam ligações fora da sua organização.

12. Depois de planejar suas configurações de atendedor automático, saudações e navegação de menu e de criar arquivos de áudio que contenham suas saudações, prompts de navegação de menu e respostas de navegação de menu gravadas, você estará pronto para criar e configurar seu atendedor automático. Veja como:
    
      - [Criar um Atendedor Automático da UM](create-a-um-auto-attendant-exchange-2013-help.md)
    
      - [Gerenciar um atendedor automático](manage-a-um-auto-attendant-exchange-2013-help.md)

13. Se você tiver criado a estrutura e as configurações do atendedor automático, habilite o atendedor automático de UM, para que ele comece a aceitar ligações.

