---
title: 'Regras de proteção de transporte: Exchange 2013 Help'
TOCTitle: Regras de proteção de transporte
ms:assetid: 9bd6d049-165e-4e51-a79f-3b8ff409da55
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Dd298166(v=EXCHG.150)
ms:contentKeyID: 50486218
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Regras de proteção de transporte

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2016-12-09_

Mensagens de email e anexos cada vez mais contenham informações essenciais aos negócios como dados financeiros, documentos de estratégia de negócios e as especificações do produto ou informações de identificação pessoal (PII) como registros de funcionários, números de cartão de crédito, números do seguro social e detalhes do contato. Há um número de normas específicas do setor e o locais em várias partes do mundo que governam o conjunto, armazenamento e a divulgação de informações de identificação Pessoal.

Para ajudar a proteger informações confidenciais, as organizações criar políticas de mensagens que fornecem diretrizes sobre como lidar com essas informações. Em MicrosoftExchange Server 2013, você pode usar as regras de proteção de transporte para implementar essas políticas a mensagens inspecionando o conteúdo da mensagem, criptografar conteúdo de email confidenciais e usando o gerenciamento de direitos para controlar o acesso ao conteúdo.

Para tarefas de gerenciamento relacionadas ao gerenciamento de IRM, consulte [Procedimentos de gerenciamento de direitos de informação](information-rights-management-procedures-exchange-2013-help.md).

## AD RMS e regras de proteção de transporte

Regras de proteção de transporte permitem que você use as regras de transporte para proteger o IRM mensagens aplicando um modelo de diretiva de direitos do [Active Directory Rights Management Services](https://go.microsoft.com/fwlink/p/?linkid=129823) (AD RMS).


> [!TIP]
> AD RMS é uma tecnologia de proteção de informações que funciona com aplicativos habilitados por RMS Rights Management Service e clientes de proteger informações confidenciais online e offline. Para usar a proteção de IRM em uma implantação no local Exchange, Exchange 2013 requer uma implantação local do AD RMS em execução no Windows Server 2008 ou posterior.



AD RMS usa os modelos de política baseado em XML para permitir que aplicativos compatíveis com IRM habilitado aplicar as políticas de proteção consistentes. No Windows Server 2008 e posterior, o servidor AD RMS expõe um serviço Web que pode ser usado para enumerar e adquirir modelos. Exchange 2013 é fornecido com o modelo não encaminhar.

Quando o modelo não encaminhar é aplicado a uma mensagem, somente os destinatários abordados na mensagem podem descriptografar a mensagem. Os destinatários não podem encaminhar a mensagem para qualquer pessoa, copiar o conteúdo da mensagem ou imprimir a mensagem.

Modelos de RMS adicionais podem ser criados no local a implantação do AD RMS para atender aos requisitos de proteção de direitos em sua organização.


> [!IMPORTANT]
> Se um modelo de diretiva de direitos é removido do servidor AD RMS, você deve modificar quaisquer regras de proteção de transporte que usam o modelo removido. Se uma regra de proteção de transporte continuar a usar um modelo de diretiva de direitos é foram removido, o servidor AD RMS falhará licenciar o conteúdo para qualquer um dos destinatários e um relatório de falha na entrega (NDR) serão entregues ao remetente.<BR>No Windows Server 2008 e posterior, direitos modelos de política podem ser arquivados, em vez de excluído. Os modelos arquivados ainda podem ser usados para licenciar conteúdo, mas quando você cria ou modificar uma regra de proteção de transporte, os modelos arquivados não estão incluídos na lista de modelos.



Para obter mais informações sobre a criação de modelos do AD RMS, consulte o [Guia de passo a passo do AD RMS direitos política modelos de implantação](https://go.microsoft.com/fwlink/p/?linkid=136593).

## Proteção automática usando regras de proteção de transporte

Mensagens contendo informações essenciais aos negócios ou PII podem ser identificadas por meio de uma combinação de condições de regra de transporte, incluindo as expressões regulares para identificar padrões de texto, como números de seguridade social. Organizações exigem diferentes níveis de proteção de informações confidenciais. Algumas informações podem ser restritas aos funcionários, prestadores de serviços ou parceiros. enquanto outras informações podem ser restritas aos funcionários em tempo integral. O nível desejado de proteção pode ser aplicado às mensagens aplicando um modelo de política de direitos apropriados. Por exemplo, os usuários podem marcar mensagens ou anexos de email como confidencial da empresa. Conforme ilustrado na figura a seguir, você pode criar uma regra de proteção de transporte para inspecionar o conteúdo da mensagem para as palavras "Confidencial da empresa" e automaticamente IRM Proteja a mensagem.

Para obter mais informações sobre a criação de regras de transporte para impor a proteção de direitos, consulte [Criar uma regra de proteção de transporte](create-a-transport-protection-rule-exchange-2013-help.md).

## Proteção persistente de anexos de email

Os usuários enviar informações essenciais aos negócios e PII nos anexos de email usando os formatos de arquivo comuns do Microsoft Office como Microsoft OfficeWord, Excel e PowerPoint. Todos esses formatos suporte persistente proteção de arquivo do via IRM e você podem assegurar-se de que as informações essenciais aos negócios e PII esses documentos estão protegidos adequadamente. Regras de proteção de transporte aplicam a mesma proteção para mensagens e anexos em formatos de arquivo com suporte.

## Agente de regras de transporte e o agente de criptografia

Quando você usa regras de proteção de transporte para mensagens de proteger o IRM com base nas condições de regra, o agente de regras de transporte do serviço de transporte inspeciona mensagens. Se eles atendem a todas as condições e nenhuma das exceções, ela sinalizadores a mensagem a ser protegida com IRM. O agente de criptografia, um agente de transporte internas que é acionado no evento **OnRoutedMessage** , realmente aplica proteção de IRM na mensagem. Agente de criptografia atua em mensagens somente se o IRM é habilitado para mensagens internas. Para obter mais informações sobre como habilitar o IRM, consulte [Habilitar ou desabilitar o IRM para mensagens internas](enable-or-disable-irm-for-internal-messages-exchange-2013-help.md).

Quando o serviço transporte é reiniciado e processa a primeira mensagem que requer criptografia de IRM, o agente de criptografia deve ser capaz de acessar um servidor AD RMS na organização. Para mensagens subsequentes, o agente não precisará contatar o servidor do AD RMS. Após a falha ao criptografar uma mensagem devido a condições transitórias, Exchange repete a mensagem três vezes em intervalos de 10 minutos. Após três tentativas, se a mensagem não puder ser criptografada, ele não é entregue aos destinatários. Um NDR é enviado ao remetente. É recomendável que você planeje sua implantação do AD RMS para alta disponibilidade certificar-se de que o fluxo de mensagens não é afetado.

Ao planejar usar regras de proteção de transporte, você deve considerar o tipo de informação que você deseja proteger e planejar a criação de regras de acordo. Em Exchange 2013, regras de transporte tem um grande número de predicados que permitem que você inspecione o conteúdo da mensagem, incluindo anexos suportados, os cabeçalhos de mensagem, endereços do remetente e destinatário, seus atributos Active Directory como departamento, a associação de grupo de distribuição e relacionamentos de gerenciamento do remetente com destinatários. Para obter mais detalhes sobre predicados de regra de transporte disponíveis no Exchange 2013, consulte [Condições de regra de transporte (predicados)](mail-flow-rule-conditions-and-exceptions-predicates-in-exchange-2013-exchange-2013-help.md).

Você também deve considerar o tráfego de mensagens em sua organização e o número de mensagens será protegida usando regras de proteção de transporte. Aplicar proteção IRM a um grande número de mensagens requer mais recursos no servidor de caixa de correio. Além disso, protegendo um grande número de mensagens ou todas as mensagens também afeta a experiência do cliente, principalmente para usuários do Microsoft Outlook.

