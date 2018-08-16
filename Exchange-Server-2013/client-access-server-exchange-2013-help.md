---
title: 'Servidor de Acesso para Cliente: Exchange 2013 Help'
TOCTitle: Servidor de Acesso para Cliente
ms:assetid: 87e206ab-7a7b-4b4f-be1a-5035713c74d2
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Dd298114(v=EXCHG.150)
ms:contentKeyID: 50486086
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Servidor de Acesso para Cliente

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2014-07-02_

O Microsoft Exchange 2013 trouxe mudanças importantes na arquitetura das funções de servidor do Exchange. Em vez das cinco funções de servidor presentes no Exchange 2010 e no Exchange 2007, a quantidade de funções de servidor no Exchange 2013 foi reduzida a três: servidor de Acesso para Cliente e servidor de Caixa de Correio e, com o Service Pack 1, a função de servidor de Transporte de Borda.


> [!NOTE]
> O Exchange 2013 também pode funcionar com a função de servidor de Transporte de Borda do Exchange 2010.



O servidor de Caixa de Correio do Exchange 2013 inclui muitos dos componentes de servidor encontrados no Exchange 2010: protocolos de acesso para cliente, serviços de transporte, bancos de dados de caixa de correio e serviços de Unificação de Mensagens (o servidor de Acesso para Cliente redireciona o tráfego SIP gerado por chamadas recebidas para o servidor de Caixa de Correio). Para obter mais informações sobre o servidor de Caixa de Correio do Exchange 2013, consulte [Servidor de Caixa de Correio](mailbox-server-exchange-2013-help.md).

O servidor de Acesso para Cliente oferece serviços de autenticação, redirecionamento limitado e de proxy, além de todos os protocolos habituais de acesso para cliente: HTTP, POP, IMAP e SMTP. O servidor de Acesso para Cliente é um servidor leve e sem monitoramento de estado, que não processa dados. Nunca há nada armazenado ou na fila do servidor de Acesso para Cliente. Para obter mais informações sobre a nova arquitetura do Exchange 2013, consulte [Novidades do Exchange 2013](what-s-new-in-exchange-2013-exchange-2013-help.md).


> [!WARNING]
> Os servidores de Acesso para Cliente não são compatíveis com redes de perímetro e devem ser implantados dentro de seu ambiente interno do Active Directory. Todo site do Active Directory que contenha um servidor de Caixa de Correio também deve conter um servidor de Acesso para Cliente.



Como resultado dessas alterações na arquitetura, houve algumas alterações na conectividade do cliente. Em primeiro lugar, RPC/TCP não é mais um protocolo de acesso direto compatível. Isso significa que toda a conectividade do Outlook deve ocorrer utilizando RPC sobre HTTPS (também conhecido como Outlook em Qualquer Lugar) ou com Exchange 2013 SP1 e Outlook 2013 SP1, MAPI sobre HTTP. O resultado dessas alterações é que não é necessário ter o serviço de Acesso para Cliente RPC no servidor de Acesso para Cliente. Além disso, uma solução com resiliência de site exige menos namespaces do que no Exchange 2010, e não é mais necessário oferecer afinidade para o serviço Acesso para Cliente RPC. Além disso, os clientes do Outlook não se conectam mais ao nome de domínio totalmente qualificado (FQDN) de um servidor como faziam em todas as versões anteriores do Exchange. Usando a Descoberta Automática, o Outlook encontra um novo ponto de conexão formado pela GUID da caixa de correio do usuário + @ + a parte de domínio do endereço SMTP principal do usuário. Com essa mudança, é muito menos provável que os usuários vejam a infame mensagem "Seu administrador fez uma alteração em sua caixa de correio". Somente o Outlook 2007 e versões posteriores são compatíveis com o Exchange 2013.

## Funcionalidade de servidor de Acesso para Cliente

O servidor de Acesso para Cliente no Exchange 2013 age como uma porta de entrada, aceitando todas as solicitações de clientes e roteando-as para o banco de dados de Caixa de Correio ativo correto. O servidor de Acesso para cliente fornece funcionalidade de segurança de rede, como protocolo SSL e autenticação de cliente, e gerencia conexões de cliente por meio das funcionalidades de redirecionamento e proxy. O servidor de Acesso para Cliente autentica conexões de cliente e, na maioria dos casos, encaminha por proxy uma solicitação ao servidor de Caixa de Correio que armazena a cópia ativa no momento do banco de dados que contém a caixa de correio do usuário. Em alguns casos, o servidor de Acesso para Cliente pode redirecionar a solicitação para um servidor de Acesso para Cliente mais adequado, em um local diferente ou executando uma versão mais recente do Exchange Server.

O servidor de acesso para cliente tem as seguintes características:

  - **Servidor sem monitoração de estado** Em versões anteriores do Exchange, muitos dos protocolos de Acesso para Cliente exigiam afinidade de sessão. Por exemplo, o Outlook Web App exigia que todas as solicitações de um cliente específico fossem tratadas por um servidor de Acesso para Cliente específico em uma matriz de carga balanceada de servidores de Acesso para Cliente. No Exchange 2013, o servidor de Acesso para Cliente não tem monitoração de estado. Em outras palavras, como todo o processamento de caixa de correio ocorre no servidor de Caixa de Correio, não importa qual servidor de Acesso para Cliente em uma matriz de servidores de Acesso para Cliente recebe cada solicitação individual de cliente. Essa mudança de funcionalidade significa que a afinidade de sessão não é mais exigida no nível do balanceador de carga. Isso permite que conexões de entrada nos servidores de Acesso para Cliente sejam balanceadas através de técnicas simples fornecidas por tecnologia de balanceamento de carga, como DNS round-robin. Ela também permite que dispositivos de balanceamento de carga de hardware ofereçam suporte a uma quantidade expressivamente maior de conexões simultâneas.

  - **Pool de conexões** Os servidores de Acesso para Cliente tratam da autenticação do cliente e enviam os dados AuthN ao servidor de Caixa de Correio. A conta usada pelos servidores de Acesso para Cliente para a conexão aos servidores de Caixa de Correio é uma conta com privilégios, membro do grupos Servidores do Exchange. Com isso, os servidores de Acesso para Cliente podem fazer um pool de conexões aos servidores de Caixa de Correio de forma eficaz. Uma gama de servidores de Acesso para Cliente pode tratar de milhões de conexões de clientes da Internet, mas uma quantidade muito menor de conexões é usada para encaminhar por proxy as solicitações aos servidores de Caixa de Correio do que em versões anteriores do Exchange. Isso melhora a eficiência do processamento e a latência de fim a fim.

## Tarefas de gerenciamento no servidor de Acesso para Cliente

No Exchange 2013, há várias tarefas importantes que podem ser realizadas no servidor de Acesso para Cliente. O gerenciamento de certificados digitais é realizado principalmente no servidor de Acesso para Cliente, e parte do gerenciamento de protocolos de clientes para Exchange ActiveSync, POP3 e IMAP4 também fica por conta do servidor de Acesso para Cliente.

