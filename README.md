# Javascript | Typescript

## Decorator
Um Decorator é um tipo especial de declaração que pode ser anexado a uma declaração de classe, método, acessador, propriedade ou parâmetro para os mais diversos fins:

#### Deorator | Throttle
Padrão de projeto que limita a quantidade de requisições realizadas, fazendo com que a cada vez que o usuário pressionar o botão, essa requisição demore meio segundo (ou outro tempo determinado) para ser enviada e caso o usuário pressione 2 vezes seguidas, a requisição reseta a contagem e começa a valer a partir da última vez que foi pressionada, assim faz com que o usuário não fique metralhando requisições;

Exemplo de ````decorator```` no padrão ````throttle```` que é feito para uma requisição de cadastro que não tem retorno, e nessa é mandado um ````event```` que faz com que a página não se recarregue (para aplicações padrão ````single page````);

````ts
  export function throttle(milissegundos = 500) {
      return function(target: any, propertyKey: string, descriptor: PropertyDescriptor) {
          const metodoOriginal = descriptor.value;

          let timer = 0;
              descriptor.value function(...args, any[]) {
                  if (event) {
                      event.preventDefault();
                  }

                  clearInterval(timer);

                  timer = setTimeout(() => metodoOriginal.apply(this, args), milissegudos);
              }

          return descriptor;
      }
  }
````

<br>
<br>

#### Decorator de método
Um decorator que executa algo antes e depois da chamada de um método:

Ele é chamado:
  
````ts
  @tempoExecucao();
  minhaFuncao() {
      //função
  }
````
 
 Exemplo de um ```decorator``` que retorna o tempo demorado para executar uma função:
    
````ts
  export function tempoExecucao() {
      return function(target: any, propertyKey: string, descriptor: PropertyDescriptor) {
          const metodoOriginal = descriptor.value;
          descriptor.value function(...args, any[]) {
              console.log("----------------------------------");
              console.log(`Parâmetros passados para o método ${propertyKey}: ${JSON.stringify(args)}`);

              const t1 = performance.now();
              const retorno = metodoOriginal.apply(this, args);
              const t2 = performance.now();

              console.log(`O retorno do método ${propertyKey} é ${JSON.stringify(retorno)}`);
              console.log(`O método ${propertyKey} demorou ${t2 - t1} ms  `);

              return retorno;
          }

          return descriptor;
      }
  }
````

<br>
<br>

#### Decorator | Doom Inject
Um decorator que verifica se o elemento ja foi buscado, se não foi ele busca e faz isso apenas uma vez quando o elemento é requisitado, conhecido como ```LazyLoad```:

Ele é chamado:
  
````ts
    @doomInject("#data");
    private _inputData: JQuery;
````
Exemplo:
   
````ts
    export function doomInject(seletor: string) {
        return function(target: any, key: string) {
            let elemento: JQuery;

            const getter = function() {
                if (!elemento) {
                    console.log(`Buscando ${seletor} para injetar em ${key}`);
                    elemento = $(seletor);
                }

                return elemento;
            }

            Object.defineProperty(target, key, {
                get: getter
            });
        }
    }
````
<br>
<br>

## Barrels
É possivel facilitar as importações no Javascript | Typescrypt com o padrão Barrel, onde neste você criará um arquivo index dentro de uma determinada pasta centralizando os arquivos contidos nela, ou seja, se na pasta ```models``` tem os modelos do ```usuario```, ```produto``` e ```regiao```.

Normalmete é importado assim:

```ts
    import { Usuario } from './models/usuario';
    import { Produto } from './models/produto';
    import { Regiao } from './models/regiao';
```

Pode ser adicionado um arquivo chamado ```index``` (extensão da linguagem, ou seja, .js ou .ts) na raiz da pasta ```models``` e exportar esses arquivos ali. Exemplo:

```ts
    export * from './usuario';
    export * from './produto';
    export * from './regiao';
```

Isso facilitará na hora de importar esses arquivos, pois será assim:

```ts
    import { Usuario, Produto, Regiao } from './models/index';
```

# Programação Defensiva

## Javascript | Typescript

#### new Date()
Precisa ter um cuidado com o Date pois se passado da forma errada para o usuário, tanto mostrando quanto requisitando, o usuário conseguirá    modificá-lo caso seja passado para ele uma referência do Date em questão, para criar uma programação defensiva para esse objeto, é necessário passar uma cópia do objeto, assim caso o usuário consiga editar essa Data, ele não estará alterando a data principal e sim a cópia, em javascript | typescript é feita assim:

Quando requisitar uma data, envolvê la em um:

````js
    new Date(data recebida)
````
No construtor quando recebe uma data, é necessário envolver essa data para garantir que o objeto ```Date``` recebido não venha já alterado;
````js
    new Date(data recebida pelo construtor)
````
<br>
<br>

#### .length()
Essa propriedade de um array pode abrir uma brecha para a exclusão desse array, caso o usuário passe

Retorna o tamanho do array:

````js
    array.length
````
    
Zera todo o array, colocando o tamanho do mesmo para 0:

````js
    array.length = 0
````

Uma possivel forma de contornar isso é retornando:

````js
    [ ].concat(array)
````

Isso faz com que o array mostrado seja uma copia do verdadeiro e que assim o mesmo nao possa ser editado;


