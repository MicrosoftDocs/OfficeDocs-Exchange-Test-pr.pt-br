---
title: 'Modelos de política DLP fornecidos no Exchange: Exchange 2013 Help'
TOCTitle: Modelos de política DLP fornecidos no Exchange
ms:assetid: 7e1917ab-1920-4a52-97d1-7dfe2add6198
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/JJ150530(v=EXCHG.150)
ms:contentKeyID: 50484740
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Modelos de política DLP fornecidos no Exchange

 

_**Aplica-se a:**Exchange Online, Exchange Server 2013_

_**Tópico modificado em:**2015-03-09_

No Microsoft Exchange Server 2013 e Exchange Online, você pode usar dados modelos de política perda prevention (DLP) como ponto de partida para a criação de políticas de DLP que ajudarão-lo a atender às suas necessidades de políticas específicas de normativos e de negócios. Você pode modificar os modelos para atender às necessidades específicas da sua organização.


> [!WARNING]
> Você deve habilitar as políticas de DLP no modo de teste antes de executá-las no seu ambiente de produção. Durante esses testes, recomenda-se que você configure caixas de correio de usuários de amostra e envie mensagens de teste que invoquem as políticas de teste para confirmar os resultados.<BR>O uso dessas políticas não garanta a conformidade com qualquer regulamentação. Depois que o teste for concluído, faça as alterações de configuração necessárias no Exchange para a transmissão de informações cumpre diretivas da sua organização. Por exemplo, talvez você precisará configurar o TLS com parceiros comerciais conhecidos ou adicionar mais restritivas ações de regra de transporte, como a adição de proteção de direitos às mensagens que contêm um determinado tipo de dados.



## Modelos disponíveis para DLP

A tabela a seguir lista os modelos de política DLP no Exchange. Para saber mais sobre como personalizar esses modelos para criar políticas de DLP, consulte [Gerenciar políticas de DLP](manage-dlp-policies-exchange-2013-help.md).


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Modelo</th>
<th>Descrição</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Dados Financeiros da Austrália</p></td>
<td><p>Ajuda a detectar a presença de informações comumente consideradas como dados financeiros na Austrália, incluindo cartões de crédito e códigos SWIFT.</p></td>
</tr>
<tr class="even">
<td><p>Ato de Registros de Integridade da Austrália (Ato HRIP)</p></td>
<td><p>Ajuda a detectar a presença de informações comumente consideradas sujeitas ao Ato de Privacidade de Registros e Informações de Saúde (HRIP Act) da Austrália, como número da conta médica e registro no imposto de renda.</p></td>
</tr>
<tr class="odd">
<td><p>Dados de Informações Identificáveis Pessoalmente (PII) da Austrália</p></td>
<td><p>Ajuda a detectar a presença de informações comumente consideradas como informações identificáveis pessoalmente (PII) na Austrália, como registro no imposto de renda e carteira de motorista.</p></td>
</tr>
<tr class="even">
<td><p>Ato de Privacidade da Austrália</p></td>
<td><p>Ajuda a detectar a presença de informações comumente consideradas sujeitas ao Ato de Privacidade da Austrália, como carteira de motorista e número de passaporte.</p></td>
</tr>
<tr class="odd">
<td><p>Dados Financeiros do Canadá</p></td>
<td><p>Ajuda a detectar a presença de informações comumente consideradas como dados financeiros no Canadá, incluindo números de conta bancária e cartões de crédito.</p></td>
</tr>
<tr class="even">
<td><p>Ato de Informações de Saúde do Canadá (HIA)</p></td>
<td><p>Ajuda a detectar a presença de informações sujeitas ao Ato de Informações de Saúde (HIA) do Canadá para Alberta, incluindo dados como números de passaporte e informações de saúde.</p></td>
</tr>
<tr class="odd">
<td><p>Ato de Saúde Pessoal do Canadá (PHIPA) - Ontário</p></td>
<td><p>Ajuda a detectar a presença de informações sujeitas ao Ato de Proteção a Informações de Saúde Pessoais (PHIPA) do Canadá para Ontário, incluindo dados como números de passaporte e informações de saúde.</p></td>
</tr>
<tr class="even">
<td><p>Ato de Informações de Saúde Pessoais do Canadá (PHIA) - Manitoba</p></td>
<td><p>Ajuda a detectar a presença de informações sujeitas ao Ato de Informações de Saúde Pessoais (PHIA) do Canadá para Manitoba, incluindo dados como informações de saúde.</p></td>
</tr>
<tr class="odd">
<td><p>Ato de Proteção a Informações Pessoais do Canadá (PIPA)</p></td>
<td><p>Ajuda a detectar a presença de informações sujeitas ao Ato de Proteção a Informações Pessoais (PIPA) do Canadá para Colúmbia Britânica, incluindo dados como números de passaporte e informações de saúde.</p></td>
</tr>
<tr class="even">
<td><p>Ato de Proteção a Informações Pessoais do Canadá (PIPEDA)</p></td>
<td><p>Ajuda a detectar a presença de informações sujeitas ao Ato de Proteção a Informações Pessoais e Documentos Eletrônicos (PIPEDA) do Canadá, incluindo dados como números de passaporte e informações de saúde.</p></td>
</tr>
<tr class="odd">
<td><p>Dados de Informações Identificáveis Pessoalmente (PII) do Canadá</p></td>
<td><p>Ajuda a detectar a presença de informações comumente consideradas como informações identificáveis pessoalmente (PII) no Canadá, como número de identificação de saúde e número da previdência social.</p></td>
</tr>
<tr class="even">
<td><p>Ato de Proteção de Dados da França</p></td>
<td><p>Ajuda a detectar a presença de informações comumente consideradas sujeitas ao Ato de Proteção de Dados na França, como o número da carteira do seguro saúde.</p></td>
</tr>
<tr class="odd">
<td><p>Dados Financeiros da França</p></td>
<td><p>Ajuda a detectar a presença de informações comumente consideradas como informações financeiras na França, incluindo informações como cartões de crédito, informações de conta e números de cartão de débito.</p></td>
</tr>
<tr class="even">
<td><p>Dados de Informações Identificáveis Pessoalmente (PII) da França</p></td>
<td><p>Ajuda a detectar a presença de informações comumente consideradas como PII na França, como números de passaporte.</p></td>
</tr>
<tr class="odd">
<td><p>Dados Financeiros da Alemanha</p></td>
<td><p>Ajuda a detectar a presença de informações comumente consideradas como dados financeiros na Alemanha, incluindo números de cartões de débito da UE.</p></td>
</tr>
<tr class="even">
<td><p>Dados de Informações Identificáveis Pessoalmente (PII) da Alemanha</p></td>
<td><p>Ajuda a detectar a presença de informações comumente consideradas como PII na Alemanha, como carteira de motorista e números de passaporte.</p></td>
</tr>
<tr class="odd">
<td><p>Dados Financeiros de Israel</p></td>
<td><p>Ajuda a detectar a presença de informações comumente consideradas como dados financeiros em Israel, incluindo números de contas bancárias e códigos SWIFT.</p></td>
</tr>
<tr class="even">
<td><p>Dados de Informações Identificáveis Pessoalmente (PII) de Israel</p></td>
<td><p>Ajuda a detectar a presença de informações comumente consideradas como informações identificáveis pessoalmente (PII) em Israel, como número de identificação nacional/regional.</p></td>
</tr>
<tr class="odd">
<td><p>Proteção de Privacidade de Israel</p></td>
<td><p>Ajuda a detectar a presença de informações comumente consideradas sujeitas à Proteção de Privacidade em Israel, incluindo informações como números de conta bancária ou ID nacional.</p></td>
</tr>
<tr class="even">
<td><p>Dados Financeiros do Japão</p></td>
<td><p>Ajuda a detectar a presença de informações comumente consideradas como informações financeiras no Japão, incluindo informações como cartões de crédito, informações de conta e números de cartão de débito.</p></td>
</tr>
<tr class="odd">
<td><p>Dados de Informações Identificáveis Pessoalmente (PII) do Japão</p></td>
<td><p>Ajuda a detectar a presença de informações comumente consideradas como PII no Japão, como carteira de motorista e números de passaporte.</p></td>
</tr>
<tr class="even">
<td><p>Proteção de Informações Pessoais do Japão</p></td>
<td><p>Ajuda a detectar a presença de informações sujeitas à Proteção de Informações Pessoais do Japão, incluindo dados como números de registro de residentes.</p></td>
</tr>
<tr class="odd">
<td><p>Padrão de Segurança de Dados PCI (PCI DSS)</p></td>
<td><p>Ajuda a detectar a presença de informações sujeitas ao Padrão de Segurança de Dados PCI (PCI DSS), incluindo informações como números de cartões de crédito ou de débito.</p></td>
</tr>
<tr class="even">
<td><p>Arábia Saudita - Lei Contra Crimes Cibernéticos</p></td>
<td><p>Ajuda a detectar a presença de informações comumente consideradas sujeitas à Lei Contra Crimes Cibernéticos na Arábia Saudita, incluindo números de contas bancárias internacionais e códigos SWIFT.</p></td>
</tr>
<tr class="odd">
<td><p>Dados Financeiros da Arábia Saudita</p></td>
<td><p>Ajuda a detectar a presença de informações comumente consideradas como dados financeiros na Arábia Saudita, incluindo números de contas bancárias internacionais e códigos SWIFT.</p></td>
</tr>
<tr class="even">
<td><p>Dados de Informações Identificáveis Pessoalmente (PII) da Arábia Saudita</p></td>
<td><p>Ajuda a detectar a presença de informações comumente consideradas como informações identificáveis pessoalmente (PII) na Arábia Saudita, como número de identificação nacional.</p></td>
</tr>
<tr class="odd">
<td><p>Ato de Acesso a Prontuários Médicos do Reino Unido</p></td>
<td><p>Ajuda a detectar a presença de informações sujeitas ao Ato de Acesso a Prontuários Médicos do Reino Unido, incluindo dados como números do Serviço de Saúde Nacional.</p></td>
</tr>
<tr class="even">
<td><p>Ato de Proteção de Dados do Reino Unido</p></td>
<td><p>Ajuda a detectar a presença de informações sujeitas ao Ato de Proteção de Informações do Reino Unido, incluindo dados como números do seguro nacional.</p></td>
</tr>
<tr class="odd">
<td><p>Dados Financeiros do Reino Unido</p></td>
<td><p>Ajuda a detectar a presença de informações comumente consideradas como informações financeiras no Reino Unido, incluindo informações como cartões de crédito, informações de conta e números de cartão de débito.</p></td>
</tr>
<tr class="even">
<td><p>Código de Prática Online de Informações Pessoais (PIOCP) do Reino Unido</p></td>
<td><p>Ajuda a detectar a presença de informações sujeitas ao Código de Prática Online de Informações Pessoais do Reino Unido, incluindo dados como informações de saúde.</p></td>
</tr>
<tr class="odd">
<td><p>Dados de Informações Identificáveis Pessoalmente (PII) do Reino Unido</p></td>
<td><p>Ajuda a detectar a presença de informações comumente consideradas como PII no Reino Unido, como carteira de motorista e números de passaporte.</p></td>
</tr>
<tr class="even">
<td><p>Regulamentações de Comunicações Eletrônicas e Privacidade do Reino Unido</p></td>
<td><p>Ajuda a detectar a presença de informações sujeitas às Regulamentações de Comunicações Eletrônicas e Privacidade do Reino Unido, incluindo dados como informações financeiras.</p></td>
</tr>
<tr class="odd">
<td><p>Regras para Consumidores da Comissão Comercial Federal (FTC) dos EUA</p></td>
<td><p>Ajuda a detectar a presença de informações sujeitas às Regras para Consumidores da Comissão Comercial Federal (FTC) dos EUA, incluindo dados como números de cartão de crédito.</p></td>
</tr>
<tr class="even">
<td><p>Finanças dos Estados Unidos</p></td>
<td><p>Ajuda a detectar a presença de informações comumente consideradas como informações financeiras nos Estados Unidos, incluindo informações como cartões de crédito, informações de conta e números de cartão de débito.</p></td>
</tr>
<tr class="odd">
<td><p>Ato Gramm-Leach-Bliley (GLBA) dos EUA</p></td>
<td><p>Ajuda a detectar a presença de informações sujeitas ao Ato Gramm-Leach-Bliley (GLBA), incluindo informações como números do seguro social ou de cartão de crédito.</p></td>
</tr>
<tr class="even">
<td><p>Ato do Seguro de Saúde (HIPAA) dos EUA</p></td>
<td><p>Ajuda a detectar a presença de informações sujeitas ao Ato de Portabilidade e Contabilidade do Seguro Saúde (HIPAA) dos Estados Unidos, incluindo dados como números de segurança social e informações de saúde.</p></td>
</tr>
<tr class="odd">
<td><p>Patriot Act dos EUA</p></td>
<td><p>Ajuda a detectar a presença de informações comumente sujeitas ao Patriot Act dos EUA, incluindo informações como números de cartão de crédito ou registros no imposto de renda.</p></td>
</tr>
<tr class="even">
<td><p>Dados de Informações Identificáveis Pessoalmente (PII) dos EUA</p></td>
<td><p>Ajuda a detectar a presença de informações comumente consideradas como PII nos Estados Unidos, como carteira de motorista e números de seguro social.</p></td>
</tr>
<tr class="odd">
<td><p>Leis de Notificação de Ruptura de Estado dos EUA</p></td>
<td><p>Ajuda a detectar a presença de informações sujeitas às Leis de Notificação de Ruptura de Estado dos EUA, incluindo dados como números de seguro social e cartão de crédito.</p></td>
</tr>
<tr class="even">
<td><p>Leis de Confidencialidade de Número de Seguro Social de Estado dos EUA</p></td>
<td><p>Ajuda a detectar a presença de informações sujeitas às Leis de Confidencialidade de Número de Seguro Social de Estado dos EUA, incluindo dados como números de seguro social.</p></td>
</tr>
</tbody>
</table>


## Para obter mais informações

[Prevenção de perda de dados](technical-overview-of-dlp-data-loss-prevention-in-exchange.md)

[Criar uma política de DLP a partir de um modelo](how-to-new-dlp-data-loss-prevention-policy-template.md)

[O que os tipos de informações confidenciais no Exchange procurar](what-the-sensitive-information-types-in-exchange-look-for-exchange-online-help.md)

