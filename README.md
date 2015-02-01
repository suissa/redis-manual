![](http://upload.wikimedia.org/wikipedia/en/thumb/6/6b/Redis_Logo.svg/467px-Redis_Logo.svg.png)

O [Redis](http://redis.io/)(**RE**mote **DI**ctionary **S**erver) é um banco NoSQL de chave-valor muito utilizado para cache, um banco do tipo chave-valor trabalha simplesmente com uma estrutura:

```js
chave: valor
1: "Suissa"
2: ["Suissa", "Nomadev"]
3: {name: "Nomadev", type: "Blog"}
```

Como percebido acima no valor nós podemos ter qualquer forma de objeto, porém ele irá virar String quando salvo no Redis e a chave sempre será uma só, então você só consegue buscar o valor a partir da chave.

Porém nós não precisamos trabalhar diretamente com Strings pois o Redis que fará essa conversão, para isso possuímos alguns tipos de dados:

- [strings](http://redis.io/topics/data-types-intro#strings)
- [hashes](http://redis.io/topics/data-types-intro#hashes)
- [lists](http://redis.io/topics/data-types-intro#lists)
- [sets](http://redis.io/topics/data-types-intro#sets)
- [sorted sets](http://redis.io/topics/data-types-intro#sorted-sets)
- [bitmaps](http://redis.io/topics/data-types-intro#bitmaps)
- [hyperloglogs](http://redis.io/topics/data-types-intro#hyperloglogs)

Nós veremos todos os tipos mais para frente, antes iremos aprender como usar o Redis via terminal.

Redis keys
Redis keys are binary safe, this means that you can use any binary sequence as a key, from a string like "foo" to the content of a JPEG file. The empty string is also a valid key.
