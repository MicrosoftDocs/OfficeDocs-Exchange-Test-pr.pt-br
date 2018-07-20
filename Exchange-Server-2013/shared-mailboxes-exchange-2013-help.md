---
title: 'Caixas de correio compartilhadas: Exchange 2013 Help'
TOCTitle: Caixas de correio compartilhadas
ms:assetid: 1d71c01b-e261-408e-a633-1d1c9d00032a
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/JJ150498(v=EXCHG.150)
ms:contentKeyID: 50485142
ms.date: 01/10/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Caixas de correio compartilhadas

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2015-06-04_

Saiba mais sobre a caixa de correio comp compartilhada Exchange no Microsoft Exchange Server 2013, os motivos para usá-la e como converter uma caixa de correio delegada em uma da caixa de correio compartilhada no Exchange.

Uma caixa de correio compartilhada é uma caixa de correio que pode ser usada por vários usuários para leitura e envio de mensagens de email. As caixas de correio compartilhadas também podem ser usadas para fornecer um calendário comum, permitindo que diversos usuários planejem e exibam o período de férias ou turnos de trabalho.

Dispositivos móveis não dão suporte a caixas de correio compartilhadas.

**Por que configurar uma caixa de correio compartilhada?**

  - Fornece um endereço de email genérico (por exemplo, info@contoso.com ou sales@contoso.com), que pode ser usado pelos clientes para saber mais sobre a sua empresa.

  - Permite que os departamentos que fornecem serviços centralizados aos funcionários (por exemplo, suporte técnico, recursos humanos ou serviços de impressão) respondam às perguntas dos funcionários.

  - Permite que vários usuários monitorem e respondam a um email enviado para um endereço de email (por exemplo, um endereço usado especificamente pelo suporte técnico).

## O que são caixas de correio compartilhadas?

Uma caixa de correio compartilhada é um tipo de caixa de correio de usuário que não possui nome de usuário nem senha próprios. Como resultado, os usuários não podem entrar nelas diretamente. Para acessar uma caixa de correio compartilhada, os usuários devem primeiro receber permissões Enviar Como e de Acesso Total para a caixa de correio. Uma vez que receberem, eles poderão entrar em suas próprias caixas de correio e depois acessar a caixa de correio compartilhada adicionando-a ao seu perfil do Outlook. No Exchange 2003 e anteriores, as caixas de correio compartilhadas eram apenas uma caixa de correio regular para a qual um administrador podia conceder acesso de representante. A partir do Exchange 2007, as caixas de correio compartilhadas se tornaram seu próprio tipo de destinatário:

  - **RecipientType:**  UserMailbox

  - **RecipientTypeDetails:**  SharedMailbox

Na versão anterior do Exchange, criar uma caixa de correio compartilhada era um processo em várias etapas em que você tinha que usar o Shell de Gerenciamento do Exchange para concluir algumas das tarefas. No Exchange 2013, você pode usar o Centro de administração do Exchange (EAC) para criar uma caixa de correio compartilhada em uma etapa. Para detalhes, consulte [Criar uma caixa de correio compartilhada](create-a-shared-mailbox-exchange-2013-help.md). De fato, o EAC tem uma área de recursos dedicada inteiramente a caixas de correio compartilhadas. Apenas vá para **Destinatários** \> **Caixas de correio compartilhadas** para exibir todas as tarefas de gerenciamento para as caixas de correio compartilhadas.

Você pode usar as seguintes permissões com uma caixa de correio compartilhada.

  - **Acesso Total**   A permissão Acesso Total permite que um usuário abra a caixa de correio compartilhada e atue como o proprietário dessa caixa de correio. Após acessar a caixa de correio compartilhada, o usuário pode criar itens de calendário; ler, exibir, excluir e alterar mensagens de email; criar tarefas e contatos de calendário. No entanto, um usuário com a permissão Acesso Total não pode enviar email da caixa de correio compartilhada, a menos que também tenha a permissão Enviar Como ou Enviar em Nome de.

  - **Enviar Como**   A permissão Enviar Como permite que um usuário represente a caixa de correio compartilhada ao enviar um email. Por exemplo, se Kweku efetuar login na caixa de correio compartilhada Departamento de Marketing e enviar um email, ele será exibido como se o Departamento de Marketing tivesse enviado o email.

  - **Enviar em Nome de**   A permissão Enviar em Nome de permite que um usuário envie um email em nome da caixa de correio compartilhada. Por exemplo, se John efetuar login na caixa de correio compartilhada Edifício de Recepção 32 e enviar um email, ele será exibido como sendo enviado por "John, em nome do Edifício de Recepção 32". Não é possível usar o EAC para conceder permissões Enviar em nome de, você deve usar o cmdlet [Set-Mailbox](https://technet.microsoft.com/pt-br/library/bb123981\(v=exchg.150\)) com o parâmetro *GrantSendonBehalf*.

## Convertendo caixas de correio compartilhadas

Nas versões anteriores do Exchange, você podia usar uma caixa de correio regular como uma caixa de correio delegada. Se você tiver caixas de correio delegadas, poderá usar o Shell para converter essas caixas de correio delegadas em caixas de correio compartilhadas. Para detalhes, consulte [Converter uma caixa de correio](convert-a-mailbox-exchange-2013-help.md).

