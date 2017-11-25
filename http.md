##PROTOCOLO HTTP

###O que é HTTP?

HTTP da sigla inglesa Hypertext Transfer Protocol traduz-se para Protocolo de Transferência de Hipertexto, é um protocolo de comunicação para sustentar a World Wide Web.

É um protocolo stateless ou seja não mantem estado (sessão), todo o dado segue de um ponto ao outro (cliente/servidor) em um body (corpo) e caso algum dado precise ser comum em todas as requisições, o mesmo deve ser repetido no cabeçalho de todas as requisições.

Vamos facilitar e entender o que compõe o corpo de uma requisição HTTP e seu fluxo, nesse cenário imagine o cliente solicitando algum recurso do servidor. Um cliente pode ser um celular, tablet, browser ou seja qualquer dispositivo que consiga operar nesse protocolo.

![enter image description here](http://blog.leandrocurioso.com/wp-content/uploads/2017/05/HTTP1.png)

 1. O cliente solicita um recurso ao servidor; 
 2. O servidor recebe a requisição e a processa; 
 3. O servidor devolve uma resposta ao cliente;

### O que seria um Recurso? 

Um recurso a ser solicitado pode ser um conteúdo HTML, um arquivo,  um json ou xml e etc..

### Certo! E o que seria uma resposta? 

A resposta do servidor é exatamente aquilo que foi requisitado pelo cliente.

Então nem o servidor nem o cliente não mantem estado sobre o que é requisitado ou respondido, por exemplo:

- Quantas vezes foram requisitados esses dados ou arquivos? Não sei!
- Qual é a sessão do cliente? Não sei!
- Qual era o IP do usuário há duas horas atras? Não sei!

Então o processo fica nesse ciclo onde o cliente solicita e o servidor responde. (***Request/Response***)

Tá mas e o exemplo do corpo de uma requisição cadê? Segue  o corpo de uma requisição utilizando o verbo POST:

    POST /salvar-usuario HTTP/1.1 
    Host: meudominio.com.br
    User-Agent: Google Chrome
    Content-Type: application/x-www-form-urlencoded 
    Meu-Header: Coloque alguma coisa aqui
    Content-Length: 38
     
    nome=jackson&amp;amp;idade=36&amp;amp;genero=masculino

Vamos entender esse corpo de requisição básica que no exemplo chama a rota /salvar-usuario

###Esses são chamados cabeçalhos (headers).

**POST:** Verbo HTTP utilizado.
**Host:** Domínio de origem da requisição.
**User-Agent:** Agente do usuário, no caso pode ser um browser, celular, servidor etc…
**Content-Type:** Tipo do conteúdo utilizado para transmitir dados no corpo da requisição.
**Content-Length:** Tamanho da string do corpo da requisição.
**Meu-Header:** Esse header é uma demonstração para que você possa ver que é livre para criar qualquer cabeçalho que quiser.

Logo abaixo perceba onde tem nome=leandro esse é o corpo da requisição, provavelmente esses dados vieram de uma página HTML com um formulário de cadastro, veja que os dados  são separados pelo simbolo &.

##Verbos HTTP o que seria isso?

Para explicar isso vou copiar um trecho da documentação do Mozilla pois achei muito bem explicado. Link

    “O protocolo HTTP define uma série de Métodos de Requisição responsáveis por indicar a ação a ser executada na representação de um determinado recurso. Embora esses métodos possam ser descritos como substantivos, eles também são comumente referenciados como verbos, os chamados “HTTP Verbs”. Cada um deles implementa uma diferente função sendo que alguns recursos são comuns entre todos os verbos, por exemplo, qualquer método de requisição pode ser do tipo safe, idempotent, ou cacheable.”

**GET**
O Método GET é utilizado para solicitar uma representação de um recurso específico, Requisições utilizando o Método GET devem retornar apenas dados. Exemplo: Me traga um arquivo ou os dados em json ou xml da lista de usuário ativos.

Já percebeu que algumas URLS tem esse simbolo de interrogação ?

Exemplo: meudominio.com.br?codigo=20

Essa interrogação na URL é chamada de ***Query String***, ela é uma das formas que temos para passar parâmetros para o servidor além dos cabeçalhos.

Importante ressaltar que  ao inserir ou alterar dados no servidor, utilizar esse verbo GET não é uma boa escolha pois os dados estariam visíveis na URL o qual queremos sigilo certo?

O verbo recomendado para fazer isso nessa situação é o **POST**, o qual iremos falar mais logo abaixo.

**HEAD**
O Método HEAD solicita uma resposta de forma idêntica ao processo que ocorre no tipo GET, porém sem um corpo body contendo o recurso.

**POST**
O Método POST é utilizado para submeter uma entidade a um recurso específico, As vezes causando uma mudança no estado do recurso ou solicitando alterações do lado do servidor. Exemplo: Criar ou salvar um usuário existente.

**PUT**
O Método PUT substitui as representações de seu recurso alvo através de uma requisição com uma carga de dados.

**DELETE**
O Método DELETE remove um recurso específico.

**CONNECT**
O Método CONNECT estabelece um túnel para conexão com o servidor a partir do recurso alvo;

**OPTIONS**
O Método OPTIONS é usado para descrever as opções de comunicação com o recurso alvo.

**TRACE**
O Método TRACE executa uma chamada de loopback como teste durante o caminho de conexão com o recurso alvo;

**PATCH**
O Método PATCH é utilizado para aplicar modificações parciais em um recurso.

Atualmente é bastante incomum ver pessoas utilizando todos esses verbos em suas aplicações posso afirmar para vocês que os 4 mais utilizados são GET, POST, PUT e DELETE em especial o GET e o POST que resolvem o problema de 99% dos casos.

Quero deixar claro que não é necessário utilizar todos os verbos listados aqui, você pode decidir como fazer o uso de acordo a arquitetura e necessidade da sua aplicação.

##Códigos de resposta HTTP

Existem 5 categorias de códigos de retorno das respostas do servidor para o cliente:

**Categoria 500**

Indica erro no servidor. A requisição é valida partida do cliente porém o servidor não conseguiu processar.

**Categoria 400**

Simboliza erro no cliente. A requisição foi feita porém a página perdeu sua validação.

**Categoria 300**

Indica a recepção da requisição mas a necessidade de executar outro passo para que a requisição seja completada.

**Categoria 200**

Indica a recepção da requisição e seu sucesso no processamento.

**Categoria 100**

Informativa. Indica que a requisição foi recebida e o processo continua.

Segue a lista completa de códigos de resposta HTTP da documentação do Mozilla  [Link](https://developer.mozilla.org/en-US/docs/Web/HTTP/Status)

Os códigos mais conhecidos são:

**200 OK**
A requisição foi bem sucedida.

**301 Moved Permanently**
O recurso foi movido permanentemente para outra URI.

**302 Found**
O recurso foi movido temporariamente para outra URI.

**304 Not Modified**
O recurso não foi alterado.

**401 Unauthorized**
A URI especificada exige autenticação do cliente. O cliente pode tentar fazer novas requisições.

**403 Forbidden**
O servidor entende a requisição, mas se recusa em atendê-la. O cliente não deve tentar fazer uma nova requisição.

**404 Not Found**
O servidor não encontrou nenhuma URI correspondente.

**405 Method Not Allowed**
O método especificado na requisição não é válido na URI. A resposta deve incluir um cabeçalho Allow com uma lista dos métodos aceitos.

**410 Gone**
O recurso solicitado está indisponível mas seu endereço atual não é conhecido.

**500 Internal Server Error**
O servidor não foi capaz de concluir a requisição devido a um erro inesperado.

**502 Bad Gateway**
O servidor, enquanto agindo como proxy ou gateway, recebeu uma resposta inválida do servidor upstream a que fez uma requisição.

**503 Service Unavailable**
O servidor não é capaz de processar a requisição pois está temporariamente indisponível.

É muito importante seguir os códigos ao programar o servidor pois além de estar mais próximo do padrão facilita o cliente qual o devido tratamento que ele deve dar para cada código de resposta.

###Cookies

Um cookie HTTP (web cookie, browser cookie) é um pequena peça de dado que o servidor envia ao cliente ou o cliente envia ao servidor, o qual pode ser armazenado e enviado junto com a próxima requisição para o mesmo servidor. Tipicamente é utilizado para saber se a requisição veio do mesmo cliente permitindo manter o cliente logado. É lembrado o estado da informação para o protocolo HTTP que naturalmente não possui estado.

Usos típicos do cookie:

 - Gerenciamento de sessão (Login de usuário, carrinho de compra e etc..)
 - Personalização (Preferências do usuário)
 - Rastreio (Analisar o comportamento do usuário)

O cookie vai como um cabeçalho no corpo da requisição contendo

    key=value /expire; /path; /domain=mydomain.com

Importante ressaltar que o cookie de um domínio, pode ser acessado pelos seus subdomínios e visa e versa, então caso você queira aproveitar o cookie para manter o usuário logado em ouras aplicações você pode.