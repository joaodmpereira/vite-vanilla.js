# Tutorial maneiro de Java Script

## Nullish Coalescing Operator

```js
const idade = null;
document.body.innerText = "Sua idade é: " + (idade || "Não definido");
```

Caso eu coloque neste caso o idade = 0. O JS ainda vai continuar apresentando o "Não definido" pois o 0 apesar de ser um valor numérico, será interpretado igual a um null, undefined, false, etc...

Pra corrigir isso a gente usa o **nullish coalescing operador = ??**

```js
const idade = 0;
document.body.innerText = "Sua idade é: " + (idade ?? "Não definido");
```

Aqui ele printa 0

## Objetos

A principio vamos trabalhar com o seguinte objeto

```js
const user = {
    name: "João"
    age: 24
    adress: {
        street: "Rua top",
        number: 666
    }
}
```

um `("name" in user)` retorna `true` pois existe atributo. Porem um `("nickname" in user)` retorna `falso`

No caso de um `Object.keys(user)` o retorno será as chaves do meu objeto `name,age,adress`

No caso de um `Object.values(user)` o retorno será os valores do meu objeto `João,24,[object Object]`

Uma excelente dica pra printar estruturas de dados mais complexas é usar o `JSON.stringfy`.

```js
document.body.innerText = JSON.stringify(Object.values(user));
```

```sh
[
    "João",
    24,
    {
        "street": "Rua top",
        "number": 666
    }
]
```

Outro método interessante é usar o `Object.entries(user)`. Ele pareia a chave e o valor do objeto

```js
document.body.innerText = JSON.stringify(Object.entries(user));
```

```sh
[
    [
        "name",
        "João"
    ],
    [
        "age",
        24
    ]
    [
        "adress",
        {
            "street": "Rua top",
            "number": 666
        }
    ]
]
```

### Desestruturação de dados

Jeito padrão:

```js
const address = user.address;

document.body.innerText = JSON.stringify(address);
```

Uma forma mais eficiente:

```js
const { address } = user;

document.body.innerText = JSON.stringify(address);
```

Esta forma é interessante pois eu posso pegar **varias variáveis ao mesmo tempo**. Outra coisa muito maneira é que consigo facilmente **renomear variáveis** assim:

```js
const { address, age: idade } = user;

document.body.innerText = JSON.stringify({ address, idade });
```

Posso tambem colocar **valores padrões** para variáveis:

```js
const { address, age: idade, nickname = "Pereira" } = user;

document.body.innerText = JSON.stringify({ address, idade, nickname });
```

Neste caso como nickname **não** está compreendido no meu objetivo, vai funcionar tranquilo, porem se eu **defino nickname com outro valor no objeto**, dai o que **será printado será o valor do objeto**, não o valor padrão.

Posso também usar com funções:

```js
funtion MostraIdade({ age }){
    return age
}

document.body.innerText = mostraIdade(user);
```

#### Algo muuuito importante: **Rest Operator**

```js
const { name, ...rest } = user;

document.body.innerText = JSON.stringyfy(rest);
```

Aqui eu consigo printar **tudo do meu objeto, menos o name!** (O **Rest Operator** também funciona com **arrays**).

```js
const array = [1, 2, 3, 4, 5, 6, 7, 8, 9];
const [first, second, ...rest] = array;

document.body.innerText = JSON.stringyfy(rest);
```

### Short Syntax

Quando se trata de criar objetos com variaveis possuidoras de mesmo nome, eu não preciso colocar um `name: name` e um `age:age`, basta colocar uma vez só as chaves vão possuir o nome da variável automaticamente.

```js
const name = "João";
const age = 24;

const user = {
	name,
	age,
};

document.body.innerText = JSON.stringyfy(rest);
```

### Optional Chaining

Sempre que a gente acessar uma variável de um objeto é importante verificar se a variável existe usando o operador "**?**" junto das variáveis, ex:

```js
const user = {
    name: "João"
    age: 24
    adress: {
        street: "Rua top",
        number: 666,
        zip: {
            code: "35540000",
            city: "chuchu_beleza"
        }
    }
}

document.body.innerText = user.address?.zip?.code ?? "Não informado"
```

A ideia é:

-   verifica se tem **address**, caso não tenha printa "Não informado".
-   Logo após, verifica sem tem **zip**, caso não tenha printa "Não informado"

O maneiro é que também ela funciona pra funções:

```js
const user = {
    name: "João"
    age: 24
    adress: {
        street: "Rua top",
        number: 666,
        zip: {
            code: "35540000",
            city: "chuchu_beleza"
        },
        showFullAddress() {
            return "ok"
        }
    }
}

document.body.innerText = user.address?.showFullAdress?.() ?? "Não informado"
```

### Metodos de array

Array elementar que usaremos para essa etapa:

```js
const array = [1, 2, 3, 4, 5];
```

#### ForEach()

Aqui eu acrescento cada elemento de forma concatenada ao print da função

```js
array.forEach((item) => {
	document.body.innerText += item;
});
```

#### map()

A função map me permite criar uma instância com base no meu array original.

```js
const newArray = array.map((item) => {
	if (item % 2 == 0) {
		return item * 10;
	}
	return item;
});

document.body.innerText = JSON.stringify(newArray);
```

#### filter()

Me retorna uma parte do array se a condição for verdadeira

```js
const newArray = array.filter((item) => item % 2 != 0);

document.body.innerText = JSON.stringify(newArray);
```

#### every()

Percerro todo o meu vetor e me devolve um boolean se a condição foi verdadeira para **todos** os itens

```js
const todosOsItensSaoNumeros = array.every((item) => {
	return typeof item === "number";
});

document.body.innerText = JSON.stringify(todosOsItensSaoNumeros);
```

#### some()

Percerro todo o meu vetor e me devolve um boolean se a condição foi verdadeira para **pelo menos um** dos itens

```js
const peloMenosUmItensEVerdairo = array.some((item) => {
	return typeof item === "number";
});

document.body.innerText = JSON.stringify(peloMenosUmItensEVerdairo);
```

#### find()

Percerro todo o meu vetor e me devolve o primeiro item no qual a condição é atingida

```js
const primeiroItem = array.find((item) => (item) => item % 2 == 0);

document.body.innerText = JSON.stringify(primeiroItem);
```

#### findIndex()

Percerro todo o meu vetor e me devolve o indice do primeiro item no qual a condição é atingida

```js
const primeiroIndex = array.findIndex((item) => (item) => item % 2 == 0);

document.body.innerText = JSON.stringify(primeiroIndex);
```

#### reduce()

Faço muitas coisas, pra esse exemplo irei somar todos os elementos do meu array. **CONTUDO**, pra usar o `reduce()` é necessário colocar um valor inicial para a minha operação reduce( () => {} , valor_inicial)

```js
const soma = array.reduce((acc, item) => {
	document.body.innerText += acc + "," + item + "---";
	return acc + item;
}, 0);

document.body.innerText = JSON.stringify(soma);
```

### Template Literals

A melhor forma de combinar variáveis dentro de strings

```js
const name = "João";
const message = `Bem vindo, ${name ? name : "visitante"}`;
```

### Promises

Uma promise é uma promessa no qual uma função vai me retornar um valor no futuro, para isso temos que passar dois possíveis resultados: caso a promessa se cumpra (**resolve**) ou caso ela não se cumpra (**reject**).

Neste caso a função `.then()` executa se a promessa for bem resolvida e o `.catch()` executa caso ela não for resolvida, e sempre depois de uma promise, caso eu tenha um `.finally()` esta seção sempre será executada.

```js
const somaDoisNumeros = (a, b) => {
	return new Promise((resolve, reject) => {
		setTimeout(() => {
			resolve(a + b);
		}, 2000);
	});
};

somaDoisNumeros(5, 10)
	.then((soma) => {
		document.body.innerText = soma;
	})
	.catch((err) => {
		console.log(err);
	});
```

Exemplo um pouco mais real:

```js
fetch("https://api.github.com/users/joaodmpereira")
	.then((response) => {
		response.json().then((body) => {
			console.log(body);
		});
	})
	.catch((err) => {
		console.log(err);
	});
```

porem eu tenho um `.then()` dentro de outro `.then()`. Isto não é o ideal pois pode complicar a legibilidade, o que fica legal é fazer o primeiro `.then()` retornar um resposta, dai então eu chamo outro `.then()`.

```js
fetch("https://api.github.com/users/joaodmpereira")
	.then((response) => {
		return response.json();
	})
	.then((body) => {
		console.log(body);
	})
	.catch((err) => {
		console.log(err);
	})
	.finally(() => {
		console.log("deu");
	});
```

Outra forma de fazer promises:

```js
async function buscaDadosNoGitub() {
	const response = await fetch("https://api.github.com/users/joaodmpereira");
	const body = await response.json();

	console.log(body);
}

buscaDadosNoGitub();
```

Dai posso combinar com o `try() catch() finally()` por fora da requisição

```js
async function buscaDadosNoGitub() {
	try {
		const response = await fetch(
			"https://api.github.com/users/joaodmpereira",
		);
		const body = await response.json();

		console.log(body);
	} catch (err) {
		console.log(err);
	} finally {
		console.log("acabou");
	}
}

buscaDadosNoGitub();

buscaDadosNoGitub();
```

No caso se eu quiser retornar alguma coisa da minha função assíncrona e salvar esse retorno em alguma variável, ela vai virar uma promise, então terei que usar o `.then()`.

```js
async function buscaDadosNoGitub() {
	try {
		const response = await fetch(
			"https://api.github.com/users/joaodmpereira",
		);
		const body = await response.json();

		console.log(body);
		return body;
	} catch (err) {
		console.log(err);
	} finally {
		console.log("acabou");
	}
}

buscaDadosNoGitub().then((body) => {
	console.log(body);
});
```
