---
title: 'Certificados digitais e SSL: Exchange 2013 Help'
TOCTitle: Certificados digitais e SSL
ms:assetid: a9e2e08c-d46a-4135-a387-eb653212b676
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Dd351044(v=EXCHG.150)
ms:contentKeyID: 51407893
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Certificados digitais e SSL

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2013-08-26_

O protocolo SSL é um método utilizado para proteger a comunicação entre um cliente e um servidor. Para o Exchange Server 2013, o SSL é utilizado para ajudar a proteger as comunicações entre o servidor e clientes. Entre os clientes estão incluídos celulares, computadores dentro da rede da organização e computadores fora da rede da organização.

Por padrão, ao instalar o Exchange 2013, as comunicações de clientes são criptografadas com SSL quando você utiliza o Outlook Web App, o Exchange ActiveSync, e o Outlook Anywhere.

O SSL exige que você utilize certificados digitais. Este tópico resume os vários tipos de certificados digitais e as informações sobre como configurar o Exchange 2013 para utilizar esses tipos de certificados digitais.

**Sumário**

Overview of digital certificates

Digital certificates and proxying

Digital certificates best practices

## Visão geral dos certificados digitais

Certificados digitais são arquivos eletrônicos que funcionam como uma senha online para verificar a identidade de um usuário ou computador. Eles são usados para criar o canal criptografado SSL, usado para a comunicações de clientes. Um certificado é uma declaração digital emitida por uma autoridade de certificação (CA), que valida a identidade do portador do certificado e permite que as partes se comuniquem de forma segura, usando criptografia.

Os certificados digitais:

  - Autenticam que seus portadores - pessoas, sites e até mesmo recursos de rede, como roteadores - são realmente quem ou o que dizem ser.

  - Protegem dados trocados online contra roubo ou violação.

Os certificados digitais podem ser emitidos por uma CA de terceiros confiável ou uma infra-estrutura de chave pública (PKI) do Windows utilizando Serviços de Certificado, ou podem ser autoassinados. Cada tipo de certificado tem vantagens e desvantagens. Cada tipo de certificado digital é inviolável e não pode ser falsificado.

Os certificados podem ser emitidos para vários usos. Entre eles, autenticação de usuário da Web, autenticação de servidor da Web, S/MIME (Secure/Multipurpose Internet Mail Extensions), protocolo IPsec (IPsec), protocolo TLS (TSL) e assinatura de código.

Um certificado contém uma chave pública e a vincula à identidade de uma pessoa, computador ou serviço que contém a chave privada correspondente. As chaves pública e privada são usadas pelo cliente e pelo servidor para criptografar dados antes que sejam transmitidos. Para usuários, computadores e serviços baseados no Windows, a confiança em uma CA é estabelecida quando há uma cópia do certificado raiz no armazenamento de certificados raiz confiável e o certificado contém um caminho de certificação válido. Para que o certificado seja válido, ele não pode ter sido revogado, nem ter expirado.

## Tipos de certificados

Há três tipos principais de certificados digitais: certificados autoassinados, certificados gerados pela infraestrutura de chave pública (PKI) do Windows e certificados de terceiros.

## certificados autoassinados

Ao instalar o Exchange 2013, um certificado autoassinado é configurado automaticamente nos servidores de caixa de correio. Um certificado autoassinado é assinado pelo aplicativo que o criou. O assunto e o nome do certificado são correspondentes. O emissor e o assunto são definidos no certificado. Este certificado autoassinado é utilizado para criptografar as comunicações entre o servidor de Acesso para Cliente e o servidor de Caixa de Correio. O servidor de acesso para cliente confia o certificado autoassinado no servidor de caixa de correio automaticamente, portanto, nenhum certificado de terceiros é necessário no servidor de caixa de correio. Ao instalar o Exchange 2013, um certificado autoassinado também é criado no servidor de Acesso para Cliente.. Este certificado autoassinado permitirá que alguns protocolos de clientes usem SSL em suas comunicações. e o Outlook Web App pode estabelecer uma conexão SSL utilizando um certificado autoassinado. Anywhere não funcionará com um certificado autoassinado no servidor de Acesso para Cliente. Certificados autoassinados devem ser copiados manualmente para o armazenamento de certificados raiz confiável no computador ou dispositivo móvel cliente. Quando um cliente se conecta a um servidor por SSL e o servidor apresenta um certificado autoassinado, o cliente deve verificar se o certificado foi emitido por uma autoridade confiável. O cliente deve confiar explicitamente na autoridade emissora. Se o cliente confirmar a relação de confiança, as comunicações SSL poderão continuar.


> [!TIP]
> Por padrão, o certificado digital instalado no servidor de caixa de correio ou servidores é um certificado autoassinado. Não é necessário substituir o certificado autoassinado nos servidores de caixa de correio em sua organização por um certificado confiável de terceiros. O servidor de Acesso para Cliente confia automaticamente, o certificado autoassinado no servidor de caixa de correio e nenhuma outra configuração é necessária para certificados neste servidor.



Pequenas organizações com frequência decidem não usar um certificado de terceiros ou não instalar sua própria PKI para emitir seus próprios certificados. Talvez tomem essa decisão porque essas soluções são muito caras, porque os administradores não têm experiência e conhecimento para criar sua própria hierarquia de certificados, ou por ambas as razões. O custo é mínimo e a instalação é simples quando certificados autoassinados são usados. No entanto, é muito mais difícil estabelecer uma infraestrutura para o gerenciamento do ciclo de vida, renovação, gerenciamento de confiança e revogação do certificado quando certificados autoassinados são usados.

## Certificados de infraestrutura de chave pública do Windows

O segundo tipo de certificado é um certificado gerado pela infraestrutura de chave pública (PKI) do Windows. Uma PKI é um sistema de certificados digitais, autoridades de certificação e autoridades de registro (RAs) que verifica e autentica a validade de cada parte envolvida em uma transação eletrônica, usando criptografia de chave pública. Ao implementar uma PKI em uma organização que usa o Active Directory, forneça uma infraestrutura para o gerenciamento do ciclo de vida, renovação, gerenciamento de confiança e revogação do certificado. No entanto, há um custo adicional envolvido na implantação de servidores e infraestrutura para criar e gerenciar certificados gerados pela PKI do Windows.

Os Serviços de Certificados são necessários para implantar uma PKI do Windows, e podem ser instalados em **Adicionar ou Remover Programas**, no Painel de Controle. Você pode instalar os Serviços de Certificados em qualquer servidor no domínio.

Se você obtiver certificados de uma CA com domínio vinculado ao Windows, poderá usá-la para solicitar ou assinar certificados para emitir para seus próprios servidores ou computadores na rede. Isso permite que você use uma PKI semelhante a um fornecedor terceirizado de certificados, mas é mais barato. Esses certificados PKI não podem ser implantados publicamente, ao contrário de outros tipos de certificado. No entanto, quando um CA de PKI assina o certificado do solicitante usando a chave privada, o solicitante é verificado. A chave pública dessa CA é parte do certificado. Um servidor que possui este certificado no armazenamento de certificado raiz confiável pode usar esta chave pública para descriptografar o certificado do solicitante e autenticar o solicitante.

As etapas para implantar um certificado gerado por PKI são parecidas com as etapas necessárias para implantar um certificado autoassinado. Ainda é preciso instalar uma cópia do certificado raiz confiável da PKI no armazenamento de certificado raiz confiável dos computadores ou dispositivos móveis que devem estabelecer uma conexão SSL com o Microsoft Exchange.

Uma PKI do Windows permite que organizações publiquem seus próprios certificados. Clientes podem solicitar e receber certificados de uma PKI do Windows na rede interna. A PKI do Windows pode renovar ou revogar certificados.

## Certificados Confiáveis de Terceiros

Certificados comerciais ou de terceiros são aqueles gerados por uma CA comercial ou de terceiros, posteriormente adquiridos para seu uso em servidores de rede. Um problema dos certificados baseados em PKI e autoassinados é que, por não serem automaticamente confiáveis para o computador cliente ou dispositivo móvel, você deve importar o certificado para o armazenamento de certificado raiz confiável em computadores cliente e outros dispositivos. Certificados comerciais ou de terceiros não têm esse problema. A maioria dos certificados de CA comerciais já é confiável, porque o certificado já reside no armazenamento de certificado raiz confiável. Como o emissor é confiável, o certificado também o é. Usar certificados de terceiros simplifica muito a implantação.

Para organizações grandes ou que precisem implantar certificados publicamente, usar um certificado comercial ou de terceiros é a melhor solução, mesmo incidindo um custo associado ao certificado. Certificados comerciais podem não ser a melhor solução para organizações pequenas e médias e talvez você decida usar uma das outras opções de certificado disponíveis.

Voltar ao início

## Escolhendo um Tipo de Certificado

Ao escolher que tipo de certificado instalar, vários fatores devem ser levados em consideração. Para ser válido, um certificado deve ser assinado. Ele pode ser autoassinado ou assinado por uma CA. Um certificado autoassinado tem limitações. Por exemplo, nem todos os dispositivos móveis permitem que um usuário instale um certificado digital no armazenamento de certificado raiz confiável. A capacidade de instalar certificados em um dispositivo móvel depende do fabricante e da operadora do serviço do dispositivo. Alguns fabricantes e operadoras de serviços móveis desabilitam o acesso ao armazenamento de certificado raiz confiável. Neste caso, nem um certificado autoassinado, nem um certificado de uma CA de PKI do Windows podem ser instalados no dispositivo móvel.

## Certificados do Exchange padrão

Por padrão, o Exchange instala um certificado autoassinado tanto no servidor de Acesso para Cliente quanto no servidor de Caixa de Correio para que toda a comunicação de rede sejam criptografadas. Criptografar toda a comunicação da rede requer que todos os servidores do Exchange tenham um certificado X.509 que possam utilizar. Você deve substituir o certificado autoassinado no servidor de Acesso para Cliente por um que seja automaticamente confiável para seus clientes.

"autoassinado" significa que um certificado foi criado e assinado apenas pelo próprio servidor do Exchange. Como não foi criado e assinado por uma CA confiável, o certificado padrão autoassinado não será confiável a qualquer software, exceto a outros servidores do Exchange na mesma organização. O certificado padrão está habilitado para todos os serviços do Exchange. Ele tem um nome alternativo de entidade (SAN) que corresponde ao nome do servidor Exchange que é instalado no servidor. Também tem uma lista de SANs que inclui o nome do servidor e o nome de domínio totalmente qualificado (FQDN) do servidor.

Embora outros servidores Exchange em sua organização do Exchange confie automaticamente este certificado, clientes como navegadores da web, clientes do Outlook , celulares e outros clientes de email além dos servidores de email externos, não irão confiá-lo automaticamente. Portanto, considere substituir este certificado por um certificado confiável de terceiros em seus servidores de Acesso para Cliente dor Exchange . Se você tem sua própria PKI interna e todos os seus clientes confiam nessa entidade, também pode usar certificados emitidos por você mesmo.

## Requisitos de certificado por serviço

Certificados são usados por várias razões no Exchange. A maioria dos clientes também usa certificados em mais de um servidor do Exchange. Em geral, quanto menos certificados você tem, mais fácil se torna o gerenciamento de certificados.

## IIS

Todos os serviços a seguir do Exchange utilizam o mesmo certificado em um determinado servidor de Acesso para Cliente do Exchange :

  - Outlook Web App

  - Centro de Administração (EAC)

  - Serviços Web do Exchange

  - Exchange ActiveSync

  - Outlook Anywhere

  - Descoberta Automática

  - Distribuição do Catálogo de Endereços do Outlook

Pelo fato de apenas um único certificado poder ser associado a um site, e porque todos esses serviços são oferecidos em um único site por padrão, todos os nomes que os clientes desses serviços utilizam devem estar no certificado (ou se enquadrarem como um nome curinga no certificado).

## POP/IMAP

Certificados usados para POP ou IMAP podem ser especificados separadamente do certificado usado para o IIS. No entanto, para simplificar a administração, é recomendável que você inclua o nome do serviço POP ou IMAP em seu certificado IIS e use um único certificado para todos esses serviços.

## SMTP

Um certificado separado pode ser utilizado para cada conector de recebimento que você configurar. O certificado deve incluir o nome que os clientes SMTP (ou outros servidores SMTP) usam para alcançar o conector. Para simplificar o gerenciamento de certificados, considere incluir todos os nomes cujo tráfego TLS deve ser suportado em um único certificado.

## Certificados Digitais e Proxy

Proxy é o método pelo qual um servidor envia conexões de clientes para outro servidor. No caso do Exchange 2013, isto ocorre quando o servidor de Acesso para Cliente representa uma solicitação de cliente recebida ao servidor de Caixa de Correio que contém a cópia ativa da caixa de correio do cliente.

Quando servidores de Acesso para Cliente utilizam o proxy para solicitações, o SSL é usado para criptografia, mas não para autenticação. O certificado autoassinado no servidor de Caixa de Correio criptografa o tráfego entre o servidor de Acesso para Cliente e o servidor de Caixa de Correio.

## Proxies e certificados reversos

Muitas implantações do Exchange utilizam proxies reversos para publicar serviços do Exchange na Internet. Proxies reversos podem ser configurados para encerrar a criptografia SSL, examinar o tráfego em limpeza no servidor e, em seguida, abrir um novo canal de criptografia SSL dos servidores de proxy reverso para os servidores Exchange por detrás deles. Esse processo é conhecido como ponte SSL. Outra forma de configurar os servidores de proxy reverso é deixar que as conexões SSL passem direto para os servidores do Exchange, atrás dos servidores de proxy reverso. Com qualquer um dos modelos de implantação, os clientes na Internet conectam-se ao servidores de proxy reverso usando um nome de host para o acesso ao Exchange, como mail.contoso.com. Então, o servidor de proxy reverso conecta-se ao Exchange usando um nome de host diferente, como o nome de máquina no servidor de Acesso para Cliente do Exchange. Não é preciso incluir o nome de máquina do servidor de Acesso para Cliente do Exchange em seu certificado, porque os servidores de proxy reverso mais comuns conseguem comparar o nome de host original usado pelo cliente com o nome de host interno do servidor de Acesso para Cliente do Exchange.

## SSlL e DNS dividido

DNS Dividido é uma tecnologia que permite que você configure diferentes endereços IP para o mesmo nome de host, dependendo de onde a solicitação DNS se originou. Isso também é conhecido como DNS de omissão de rotas, DNS no modo divisão ou DNS de redes separadas. DNS Dividido pode ajudá-lo a reduzir a quantidade de nomes de host que você precisa gerenciar para o Exchange permitindo a sus clientes conectarem-se ao Exchange através do mesmo nome de host se estiverem conectando da internet ou da Intranet. DNS dividido permite solicitações originadas de intranet para receber um endereço IP diferente do que solicitações originadas da Internet.

DNS Dividido geralmente é desnecessário em uma implantação do Exchange pequena porque os usuários podem acessar o mesmo ponto de extremidade DNS, se eles estiverem vindo da intranet ou da Internet No entanto, em implantações maiores, essa configuração resultará em uma carga muito alta no servidor de proxy de saída da Internet e em seu servidor de proxy reverso. Para implantações maiores, configure o DNS dividido para que, por exemplo, usuários externos acessem mail.contoso.com e usuários internos acessem internal.contoso.com. Usar o DNS dividido para essa configuração garante que seus usuários não precisarão lembrar de usar nomes de host diferentes, dependendo de onde estiverem localizados.

## Windows PowerShell Remoto

Autenticação Kerberos e criptografia Kerberos são utilizados para acesso remoto do Windows PowerShell, a partir do Centro de Administração do Exchange (EAC) e do Shell de Gerenciamento do Exchange . Portanto, não será necessário configurar seus certificados SSL para uso com o Windows PowerShell remoto.

Voltar ao início

## Práticas recomendadas de certificados digitais

Embora a configuração dos certificados digitais da sua organização variem com base em suas necessidades específicas, informações sobre práticas recomendadas foram incluídas para ajudá-lo a escolher a configuração de certificado digital certa para você.

## Práticas recomendadas: Utilizar um certificado confiável de terceiros.

Para evitar que clientes recebem erros relacionados a certificados não confiáveis, o certificado usado pelo seu servidor do Exchange deve ser emitido por alguém em quem o cliente confie. Embora a maioria dos clientes possa ser configurada para confiar em qualquer certificado ou emissor de certificado, é mais simples usar um certificado de terceiros confiável em seu servidor do Exchange. Isso acontece porque a maioria dos clientes já confia em seus certificados raiz. Há vários emissores de certificados de terceiros que oferecem certificados configurados especificamente para o Exchange. É possível utilizar o EAC para gerar solicitações de certificado que funcionam com a maioria dos emissores de certificado.

## Como selecionar uma autoridade de certificação

Uma autoridade de certificação (CA) é uma empresa que emite e garante a validade dos certificados. Softwares cliente (por exemplo, navegadores como o Microsoft Internet Explorer, ou sistemas operacionais como o Windows ou Mac OS) têm uma lista interna de CAs em que confiam. A lista geralmente pode ser configurada para adicionar ou remover CAs, mas essa configuração é geralmente cansativa. Use os seguintes critérios ao selecionar uma CA para adquirir seus certificados:

  - Garanta que o software cliente (sistemas operacionais, navegadores e telefones celulares) que se conectará aos seus servidores do Exchange confia na CA.

  - Escolha uma CA que declare o suporte oferecido a "certificados de Comunicações Unificadas" para uso com o servidor do Exchange.

  - Certifique-se de que a CA ofereça suporte aos tipos de certificados que você usará. Considere o uso de certificados de nome alternativo da entidade (SAN). Nem todas as CAs oferecem suporte a certificados SAN, e outras CAs não oferecem suporte a tantos nomes de host quantos você possa precisar.

  - Certifique-se de que a licença adquirida para os certificados permite que você coloque o certificado no número de servidores que pretende usar. Algumas CAs só permitem que você coloque um certificado em um servidor.

  - Compare os preços dos certificados entre as CAs.

## Práticas recomendadas: Utilizar certificados SAN

Dependendo de como os nomes de serviço em sua implantação do Exchange estão configurados, seu servidor do Exchange pode exigir um certificado que represente vários nomes de domínio. Embora um certificado curinga, para um \*. contoso.com, possa resolver este problema, muitos clientes estão desconfortáveis com as implicações de segurança da manutenção de um certificado que pode ser utilizado para qualquer subdomínio. Uma alternativa mais segura é listar cada um dos domínios necessários como SANs no certificado. Por padrão, esta abordagem é usada quando as solicitações de certificado são geradas pelo Exchange.

## Práticas recomendadas: Utilizar o assistente de certificado do Exchange para solicitar certificados

Há muitos serviços em Exchange que usam certificados. Um erro comum ao solicitar certificados é fazer a solicitação sem incluir o conjunto correto de nomes de serviço. O assistente de certificado no Centro de Administração do Exchange lhe ajudará a incluir a lista de nomes correta na solicitação de certificado. O assistente permite que você especifique com quais serviços o certificado tem que trabalhar e, com base nos serviços selecionados, inclui os nomes que você deve ter no certificado, para que ele possa ser usado com esses serviços. Execute o assistente de certificado quando tiver implantado o conjunto inicial de servidores Exchange 2013 e determinado os nomes de host a serem utilizados para os diferentes serviços para sua implantação. Em condições ideais, você só precisará executar o assistente de certificado uma vez para cada site do Active Directory em que o Exchange estiver implantado.

Ao invés de se preocupar em esquecer um nome de host na lista SAN do certificado que você adquiriu, você pode usar uma autoridade de certificado que ofereça, sem custos, um período de cortesia durante o qual você pode devolver um certificado e solicitar o mesmo certificado novo, com alguns nomes de host adicionais.

## Práticas recomendadas: Utilizar o mínimo de nomes de host possível,

Além de usar o mínimo de certificados possível, você também deve usar o mínimo de nomes de host possível. Essa prática pode economizar dinheiro. Muitos provedores de certificados cobram uma taxa com base no número de nomes de host adicionados ao certificado.

A etapa mais importante para reduzir o número de nomes de host que você deve ter e, portanto, a complexidade do gerenciamento do seu certificado, é não incluir nomes de host de servidor individuais nos nomes alternativos para requerente do certificado.

Os nomes de host que devem ser incluídos em seus certificados do Exchange são os nomes de host usados pelos aplicativos cliente para se conectarem ao Exchange. A seguir, uma lista de nomes de host típicos que seriam exigidos para uma empresa chamada Contoso:

  - **Mail.contoso.com**   Este nome de host abrange a maioria das conexões ao Exchange, incluindo o MicrosoftOutlook, o Outlook Web App, o Outlook Anywhere, o catálogo de endereços offline, Exchange serviços Web, POP3, IMAP4, SMTP, Exchange Painel de Controle, e ActiveSync.

  - **Autodiscover.contoso.com**   Este nome de host é usado por clientes que suportam a Descoberta Automática, incluindo clientes do Microsoft Office Outlook 2007 e versões posteriores, do Exchange ActiveSync, e dos Serviços Web do Exchange.

  - **Legacy.contoso.com**   Este nome de host é exigido em um cenário de coexistência com o Exchange 2007 e o Exchange 2013. Se você tiver clientes com caixas de correio no Exchange 2007 e no Exchange 2013, configurar um nome de host herdado evita que os usuários tenham de aprender uma segunda URL durante o processo de atualização.

## Noções básicas sobre certificados curinga

Um certificado curinga é criado para dar suporte a um domínio e vários sub-domínios. Por exemplo, a configuração de um certificado curinga para \*.contoso.com resulta em um certificado que funcionará para mail.contoso.com, web.contoso.com e autodiscover.contoso.com.

Voltar ao início

