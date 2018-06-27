---
title: 'ID de remetente: Exchange 2013 Help'
TOCTitle: ID de remetente
ms:assetid: 0f628f83-df8c-43fb-bf49-7aaa9ec69ab1
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Aa996295(v=EXCHG.150)
ms:contentKeyID: 50485029
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# ID de remetente

 

_**Aplica-se a:**Exchange Server 2013_

_**Tópico modificado em:**2016-12-09_

O agente de ID de Remetente é um agente antispam disponível no Microsoft Exchange Server 2013. O agente de ID do Remetente se baseia no cabeçalho SMTP (Simple Mail Transfer Protocol) RECEIVED e em uma consulta ao serviço DNS (Sistema de Nome de Domínio) do sistema de envio para determinar qual ação, se houver alguma, executar em uma mensagem de entrada.

A ID do Remetente é usado para combater a representação de um remetente ou domínio, uma prática normalmente chamada de *falsificação*. Um *email falsificado* é email que possui um endereço de envio que foi modificado para parecer ter sido enviado por outro remetente que não o remetente real do email.

Mensagens falsificadas normalmente contêm um endereço De: que simula ser de uma determinada organização. Anteriormente, era relativamente fácil falsificar o endereço De:, na sessão SMTP, como cabeçalho MAIL FROM:, e nos dados de mensagem RFC 2822, como From: "Masato Kawai" masato@contoso.com, pois os cabeçalhos não eram validados.

**Sumário**

Using Sender ID to combat spoofing

Updating your organization's Internet-facing DNS to support Sender ID

Specifying recipients and sender domains to exclude from Sender ID filtering

## Usar a ID de Remetente para combater a falsificação

A ID de Remetente dificulta a falsificação. Quando você habilita a ID de Remetente, cada mensagem contém um status da ID do Remetente nos metadados da mensagem. Quando um email é recebido, o servidor do Exchange consulta o servidor DNS do remetente para verificar se o endereço IP que enviou a mensagem está autorizado a enviar mensagens para o domínio especificado nos cabeçalhos da mensagem. O endereço IP do servidor de envio autorizado é conhecido como PRA (Purported Responsible Address, Endereço Responsável por Expressão).

Os administradores de domínio publicam registros de estrutura (SPF) de política do remetente em seus servidores DNS. Registros SPF identificam os servidores de email de saída autorizado. Se um registro SPF estiver configurado nesse servidor DNS do remetente, o Exchange server analisa o registro SPF e determina se o endereço IP do qual a mensagem foi recebida está autorizado a enviar emails em nome de domínio que é especificado na mensagem. Para obter mais informações sobre o que contém um registro SPF e como criar um registro SPF, consulte o [ID de remetente](https://go.microsoft.com/fwlink/p/?linkid=50977).

O servidor Exchange atualiza os metadados da mensagem com o status da ID de Remetente baseado no registro da SPF. Depois de o servidor do Exchange atualiza os metadados do email, a entrega da mensagem continua normalmente.

## Valores de status da ID do Remetente

O processo de avaliação da ID do Remetente cria um status da ID do Remetente para a mensagem. O status da ID do Remetente é usado para avaliar a classificação de nível de confiança de spam (SCL) da mensagem. Esse status pode ser definido como um dos seguintes valores:

  - **Aprovado**    Tanto o Endereço IP quanto o PRA (Endereço Responsável pela Expressão) passaram pela verificação da ID do Remetente.

  - **Neutro**   Os dados publicados da ID do Remetente são explicitamente inconclusos.

  - **Soft fail**   O endereço IP do PRA pode fazer parte do conjunto de não-permitidos.

  - **Reprovado**   O endereço IP não é permitido; nenhum PRA foi encontrado no email de entrada ou o domínio de envio não existe.

  - **None**   Não existem dados de SPF publicados no DNS do remetente.

  - **TempError**   Ocorreu uma falha de DNS temporária, como um servidor DNS indisponível.

  - **PermError** A gravação de DNS é inválida, como um erro no formato de gravação.

O status da ID do Remetente é adicionado aos metadados da mensagem e convertido posteriormente em uma propriedade MAPI. O filtro de lixo eletrônico no Microsoft Outlook usa a propriedade MAPI durante a geração do valor de SCL.

O Outlook não mostra o status da ID do Remetente nem sinaliza, necessariamente, uma mensagem como lixo eletrônico por causa de determinados valores de ID de Remetente. O Outlook usa o status da ID de Remetente somente durante o cálculo do valor SCL.

Além das sete situações que geram status da ID do Remetente, o processo de avaliação da ID do Remetente pode revelar instâncias em que o endereço From: IP esteja faltando. Se o endereço From: IP estiver faltando, o status da ID do Remetente não poderá ser definido. Se o status da ID de Remetente não puder ser definido, o Exchange continuará a processar a mensagem sem incluir um status da ID do Remetente na mensagem. A mensagem não é descartada ou rejeitada. Neste cenário, o status da ID do Remetente não será definido e um evento de aplicativo será registrado.

Para mais informações sobre como o status da ID do Remetente é exibido nas mensagens, consulte [Carimbos anti-spam](anti-spam-stamps-exchange-2013-help.md).

## Opções da ID do Remetente para manipular mensagens falsificadas e servidores DNS inacessíveis

Você também pode definir como o servidor do Exchange manipula mensagens identificadas como falsificadas e como o servidor do Exchange manipula mensagens quando um servidor DNS não pode ser acessado. As opções para como o servidor do Exchange manipula mensagens falsificadas e servidores DNS inacessíveis incluem as seguintes ações:

  - **Carimbar status**   Esta opção é a ação padrão. O status da ID de Remetente é incluído nos metadados de todas as mensagens de entrada da sua organização.

  - **Rejeitar**   Esta opção rejeita a mensagem e envia uma resposta de erro SMTP para o servidor remetente. A resposta de erro SMTP é uma resposta de protocolo de nível 5*xx* com texto que corresponde ao status da ID de Remetente.

  - **Excluir**   Essa opção exclui a mensagem sem informar o sistema remetente sobre a exclusão. Na verdade, o servidor do Exchange envia um comando SMTP OK falso para o servidor de envio e exclui a mensagem. Por achar que a mensagem já foi enviada, o servidor de envio não tenta enviar a mensagem novamente na mesma sessão.

Para mais informações sobre como configurar o agente da ID do Remetente, consulte [Gerenciar o ID de remetente](manage-sender-id-exchange-2013-help.md).

Voltar ao início

## Atualizar o DNS voltado para a Internet da sua organização, para oferecer suporte à ID do Remetente

A eficácia da ID do Remetente depende de dados de DNS específicos. Quanto mais organizações atualizarem seus servidores DNS voltados para a Internet usando um registro SPF, mais eficaz será a identificação de emails falsificados realizada pela ID do Remetente.

Para oferecer suporte a infraestrutura de ID do remetente, você deve atualizar seus dados DNS voltado à Internet criando um registro SPF e hospedando o registro SPF em seus servidores DNS públicos. Para obter mais informações sobre como criar e implantar os registros SPF, consulte o [ID de remetente](https://go.microsoft.com/fwlink/p/?linkid=50977).

Voltar ao início

## Especificar domínios de destinatários e remetentes a serem excluídos da filtragem da ID do Remetente

Talvez você queira excluir domínios de remetentes e destinatários específicos da filtragem da ID do Remetente. Para fazer isso, você deve especificar os domínios de remetentes e destinatários no Shell de Gerenciamento do Exchange, usando o cmdlet **Set-SenderIdConfig**. Para mais informações, consulte [Set-SenderIdConfig](https://technet.microsoft.com/pt-br/library/aa998859\(v=exchg.150\)).

Voltar ao início

