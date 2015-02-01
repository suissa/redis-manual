{<2>}![](http://upload.wikimedia.org/wikipedia/en/thumb/6/6b/Redis_Logo.svg/467px-Redis_Logo.svg.png)

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

##Instalação

###MacOs

```
brew install redis
```

Para rodar o servidor basta executar:

```
redis-server
[3279] 01 Feb 20:14:29.426 # Warning: no config file specified, using the default config. In order to specify a config file use redis-server /path/to/redis.conf
[3279] 01 Feb 20:14:29.428 * Increased maximum number of open files to 10032 (it was originally set to 2560).
                _._                                                  
           _.-``__ ''-._                                             
      _.-``    `.  `_.  ''-._           Redis 2.8.17 (00000000/0) 64 bit
  .-`` .-```.  ```\/    _.,_ ''-._                                   
 (    '      ,       .-`  | `,    )     Running in stand alone mode
 |`-._`-...-` __...-.``-._|'` _.-'|     Port: 6379
 |    `-._   `._    /     _.-'    |     PID: 3279
  `-._    `-._  `-./  _.-'    _.-'                                   
 |`-._`-._    `-.__.-'    _.-'_.-'|                                  
 |    `-._`-._        _.-'_.-'    |           http://redis.io        
  `-._    `-._`-.__.-'_.-'    _.-'                                   
 |`-._`-._    `-.__.-'    _.-'_.-'|                                  
 |    `-._`-._        _.-'_.-'    |                                  
  `-._    `-._`-.__.-'_.-'    _.-'                                   
      `-._    `-.__.-'    _.-'                                       
          `-._        _.-'                                           
              `-.__.-'                                               

[3279] 01 Feb 20:14:29.429 # Server started, Redis version 2.8.17
[3279] 01 Feb 20:14:29.429 * The server is now ready to accept connections on port 6379
```
E para usar o cliente do Redis usamos o `redis-cli`:

```
redis-cli
127.0.0.1:6379> 
```

###Linux

```
$ wget http://download.redis.io/releases/redis-2.8.19.tar.gz
$ tar xzf redis-2.8.19.tar.gz
$ cd redis-2.8.19
$ make
```

Os binários compilados estão na pasta `src`:

```
$ src/redis-server
```

Para rodar o cliente basta:

```
$ src/redis-cli
redis> set foo bar
OK
redis> get foo
"bar"
```

##Chaves

As chaves no Redis são [binary safe](http://en.wikipedia.org/wiki/Binary-safe), isso significa que você pode usar qualquer sequência de binários como uma chave, desde uma String como "nomadev" até o conteúdo de um arquivo JPEG, uma String vazia também é uma chave válida.

Algumas regras sobre as chaves:

- Chaves muito longas não são uma boa ideia, por exemplo uma chave com 1024 bytes é uma péssima ideia não apenas pensando na memória, mas também porque a pesquisa da chave no conjunto de dados pode necessitar de várias comparações de chave que são dispendiosas.
- Muito chaves curtas, muitas vezes não são uma boa idéia. Não vale a pena por escrito "u1000flw" como uma chave se você pode, em vez escrever "usuario:1000:seguidores". Este último é mais legível e o espaço adicional é menor em comparação com o espaço usado pelo próprio objeto de chave e o objeto de valor. Enquanto chaves curtas, obviamente, consumirão um pouco menos memória, o seu trabalho é encontrar o equilíbrio certo.
- Tente ficar com um esquema. Por exemplo "tipo de objeto: id" é uma boa idéia, como em "user:1000". Pontos ou traços são muitas vezes utilizados para campos com várias palavras, como em "comentario:1234:reply.to" ou "comentario: 1234:reply-to".
- O máximo permitido tamanho da chave é 512 MB.





