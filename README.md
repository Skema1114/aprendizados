# Javascript | Typescript

```Throttle``` Padrão que limita a quantidade de requisições realizadas, fazendo com que a cada vez que o usuário pressionar o botão, essa requisição demore meio segundo (ou outro tempo determinado) para ser enviada e caso o usuário pressione 2 vezes seguidas, a requisição reseta a contagem e começa a valer a partir da última vez que foi pressionada, assim faz com que o usuário não fique metralhando requisições;


# Programação Defensiva

- ## Javascript | Typescript

  - ```new Date()``` Precisa ter um cuidado com o Date pois se passado da forma errada para o usuário, tanto mostrando quanto requisitando, o usuário conseguirá    modificá-lo caso seja passado para ele uma referência do Date em questão, para criar uma programação defensiva para esse objeto, é necessário passar uma cópia do objeto, assim caso o usuário consiga editar essa Data, ele não estará alterando a data principal e sim a cópia, em javascript | typescript é feita assim:
    - Quando requisitar uma data, envolvê la em um:
    ````js
      new Date(data recebida)
    ````
    - No construtor quando recebe uma data, é necessário envolver essa data para garantir que o objeto ```Date``` recebido não venha já alterado;
    ````js
      new Date(data recebida pelo construtor)
    ````

  - ```.length()``` = Essa propriedade de um array pode abrir uma brecha para a exclusão desse array, caso o usuário passe
     - Retorna o tamanho do array:
    ````js
      array.length
    ````
    - Zera todo o array, colocando o tamanho do mesmo para 0:
    ````js
      array.length = 0
    ````
    Uma possivel forma de contornar isso é retornando:
    ````js
      [ ].concat(array)
    ````
    Isso faz com que o array mostrado seja uma copia do verdadeiro e que assim o mesmo nao possa ser editado;


