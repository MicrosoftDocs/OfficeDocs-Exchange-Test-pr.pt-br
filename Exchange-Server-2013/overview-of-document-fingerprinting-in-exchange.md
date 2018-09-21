---
title: 'Impressão Digital de Documento: Exchange 2013 Help'
TOCTitle: Impressão Digital de Documento
ms:assetid: 1e0c579c-26e0-462a-a1b0-d7506dfe05fa
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Dn635176(v=EXCHG.150)
ms:contentKeyID: 61203501
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Impressão Digital de Documento

 

_**Aplica-se a:** Exchange Online, Exchange Server 2013_

_**Tópico modificado em:** 2014-09-11_

Os funcionários de TI em sua organização lidam com vários tipos de informações confidenciais em um dia comum. A *Impressão Digital de Documento* facilita a proteção dessas informações identificando formas padrão usadas em sua organização. Este tópico descreve os conceitos por trás da Impressão Digital de Documento. Se quiser saber como criar uma impressão digital de documento, consulte [Proteger os dados de formulário com a impressão digital de documento](https://docs.microsoft.com/pt-br/exchange/security-and-compliance/data-loss-prevention/protect-data-with-fingerprinting).

## Cenário básico da Impressão Digital de Documento

A Impressão Digital de Documento é um recurso de Prevenção Contra Perda de Dados (DLP) que converte um formulário padrão em um tipo de informação confidencial, que você pode usar para definir regras de transporte e políticas DLP. Por exemplo, você pode criar uma impressão digital de documento com base em um modelo de patente em branco e, então, criar uma política DLP que detecta e bloqueia todos os modelos de patente de saída com conteúdo confidencial. Opcionalmente, você pode configurar as [Dicas de política](https://docs.microsoft.com/pt-br/exchange/security-and-compliance/data-loss-prevention/policy-tips) para notificar os remetentes de que eles podem estar enviando informações confidenciais, e o remetente deve verificar se os remetentes estão qualificados para receber as patentes. Esse processo funciona com qualquer formulário baseado em texto usado em sua organização. Exemplos adicionais de formulários que você pode carregar incluem:

  - Formulários governamentais

  - Formulários compatíveis com a Lei americana HIPAA (Health Insurance Portability Accountability Act, Lei de responsabilidade sobre portabilidade de seguro saúde)

  - Formulários de informação sobre funcionários para departamentos de Recursos Humanos

  - Formulários personalizados criados especificamente para sua organização

Idealmente, sua organização já tem uma prática comercial estabelecida sobre o uso de determinados formulários para transmitir informações confidenciais. Depois de carregar um formulário vazio a ser convertido em uma impressão digital de documento e de configurar uma política correspondente, o agente DLP detectará todos os documentos no email de saída que correspondam a essa impressão digital.

## Funcionamento da Impressão Digital de Documento

Provavelmente você já sabe que os documentos não têm impressões digitais reais, mas o nome ajuda a explicar o recurso. Da mesma maneira que as impressões digitais de uma pessoa têm padrões exclusivos, os documentos têm padrões de palavra exclusivos. Quando você carrega um arquivo, o agente DLP identifica o padrão de palavra exclusivo no documento, cria uma impressão digital de documento com base nesse padrão e usa essa impressão digital de documento para detectar documentos de saída com o mesmo padrão. É por isso que o carregamento de um formulário ou de um modelo cria o tipo mais eficaz de impressão digital de documento. Todos que preenchem um formulário usam o mesmo conjunto de palavras do original e, então, adicionam suas próprias palavras ao documento. Desde que o documento de saída não seja protegido por senha e que contenha todo o texto do formulário original, o agente DLP poderá determinar se o documento corresponde à impressão digital de documento.

O exemplo a seguir mostra o que acontecerá se você criar uma impressão digital de documento com base em um modelo de patente, mas você pode usar qualquer formulário como base para a criação de uma impressão digital de documento.

**Exemplo de um documento de patente correspondente a uma impressão digital de documento de um modelo de patente**

![Um documento de patente combinando uma impressão digital de documentos.](images/Dn635176.9c952770-2cd4-4f62-9735-6d073344be7f(EXCHG.150).png "Um documento de patente combinando uma impressão digital de documentos.")

O modelo de patente contém os campos em branco "Título da patente", "Inventores" e "Descrição" e descrições de todos os campos; esse é o padrão de palavra. Quando você carrega o modelo de patente original, ele está em um dos tipos de arquivo compatíveis e com texto sem formatação. O agente DLP usa um algoritmo para converter esse padrão de palavra em uma impressão digital de documento, que é um pequeno arquivo XML Unicode com um valor de hash exclusivo, que representa o texto original, e a impressão digital é salva como uma classificação de dados no Active Directory. (Como medida de segurança, o próprio documento original não é armazenado no serviço, somente o valor de hash é armazenado e o documento original não pode ser reconstruído a partir do valor de hash.) A impressão digital de patente então se torna um tipo de informação confidencial que pode ser associada a uma política DLP. Depois de associar a impressão digital a uma política DLP, o agente DLP detecta todos os emails de saída com documentos que correspondam à impressão digital de patente e lida com eles de acordo com a política da sua organização. Por exemplo, talvez você queira configurar uma política de DLP que impeça funcionários comuns de enviar mensagens de saída com patentes. O agente DLP usará a impressão digital de patente para detectar patentes e bloqueará esses emails. Como alternativa, talvez você queira permitir que seu departamento jurídico possa enviar patentes para outras organizações porque há uma necessidade comercial de fazer isso. Você pode permitir que departamentos específicos enviem informações confidenciais criando exceções para esses departamentos em sua política DLP ou pode permitir que eles substituam uma dica de política por uma justificativa comercial. Para obter informações mais detalhadas sobre a criação de regras e exceções de política DLP, consulte [Procedimentos DLP](https://technet.microsoft.com/pt-br/library/jj938003\(v=exchg.150\)). Para saber mais sobre a configuração de dicas de política que os usuários podem substituir, consulte [Gerenciar dicas de política](https://docs.microsoft.com/pt-br/exchange/security-and-compliance/data-loss-prevention/manage-policy-tips).

## Tipos de arquivo com suporte

Impressão digital de documento suporta os mesmos tipos de arquivo suportados no regras de transporte. Para obter uma lista dos tipos de arquivo com suporte, consulte [Usar regras de fluxo de email para inspecionar anexos de mensagens no Office 365](https://technet.microsoft.com/pt-br/library/jj919236\(v=exchg.150\)). Uma observação rápida sobre tipos de arquivo: nem regras de transporte nem a impressão digital de documento suporta o tipo de arquivo. dotx, que pode ser confuso, pois é um arquivo de modelo no Word. Quando você vir a palavra "modelo" neste e em outros tópicos de impressão digital de documentos, se refere a um documento que você tenha estabelecido como um formulário padrão, não é o tipo de arquivo do modelo.

## Limitações da impressão digital de documento

O agente de DLP da Impressão Digital de Documento não detectará informações confidenciais nos seguintes casos:

  - Arquivos protegidos por senha

  - Arquivos que contenham somente imagens

  - Documentos que não contenham todo o texto do formulário original usado para criar a impressão digital de documento

## Para saber mais

[Proteger os dados de formulário com a impressão digital de documento](https://docs.microsoft.com/pt-br/exchange/security-and-compliance/data-loss-prevention/protect-data-with-fingerprinting)

[Integrando regras de informações confidenciais com regras de transporte](https://docs.microsoft.com/pt-br/exchange/security-and-compliance/data-loss-prevention/integrate-sensitive-information-rules)

[Procedimentos DLP](https://technet.microsoft.com/pt-br/library/jj938003\(v=exchg.150\))

