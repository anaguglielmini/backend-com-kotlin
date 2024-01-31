# Estruturas de Controle de Fluxo e Coleções em Kotlin

## Controle de Fluxo

- **When**

Pode ser usado no lugar da repetição de Switch case mas com uma estrutura muito mais flexível e limpa.

Há duas formas de utilizar o When:

**1 - When Statement**

Estrutura para fazer verificações.

```
fun main() {
    cases("Hello")
    cases(1)
    cases(0L)
    cases(MyClass())
    cases("hello")
}

// função que interpreta o que será realizado dependendo do caso
// tem um objeto sendo passado e tipado como any para receber "qualquer coisa" como parâmetro
fun cases(obj: Any) {                                
    when (obj) { 
        // se obj for 1                                    
        1 -> println("One")                          

        // se obj for Hello
        "Hello" -> println("Greeting")     

        // se for do tipo Long          
        is Long -> println("Long")                   

        // se não for do tipo string
        // ! significa não ou contrário
        !is String -> println("Not a string")        

        else -> println("Unknown")                   
    }   
}

class MyClass
```

**2 - When Expression**

Expressão para atribuir um valor.

```
fun main() {
    println(whenAssign("Hello"))
    println(whenAssign(3.4))
    println(whenAssign(1))
    println(whenAssign(MyClass()))
}

// recebe e devolve "qualquer coisa", any
fun whenAssign(obj: Any): Any {
    val result = when (obj) {                   
        1 -> "one"                              
        "Hello" -> 1                            
        is Long -> false                        
        else -> 42                              
    }
    return result
}

class MyClass
```

## Estrutura de Repetição - Loops

- **For**

```
fun main() {

// criando uma lista de strings com nomes de bolos
    val cakes = listOf("carrot", "cheese", "chocolate")
    
    // for que chama cada item da lista cakes de flavor
    // e realiza a mesma ação com cada item
    for (flavor in cakes) {  
        // interpolação de strings para concatenar texto e valor                            
        println("Yummy, it's a $flavor cake!")
    }

}
```

- **While e Do While**

```
// simulação de bolos sendo comidos e assados
fun eatACake() = println("Eat a Cake")
fun bakeACake() = println("Bake a Cake")

fun main() {
    var cakesEaten = 0
    var cakesBaked = 0
    
    // enquanto cakesEaten (bolos comidos) for menor que 5
    // irá realizar enquanto for verdadeira a afirmação
    // não sairá desse laço de repetição enquanto cakesEaten for menor que 5
    while (cakesEaten < 5) {                    
        // irá comer um bolo
        eatACake()
        // e adicionar um na contagem de bolos comidos
        cakesEaten ++
    }
    
    // faça um bolo, asse um bolo 
    do {                                        
        bakeACake()
        // e adiciona um na contagem de bolos assados
        cakesBaked++
        // enquanto bolos assados for menor que bolos comidos
    } while (cakesBaked < cakesEaten)

}
```

- **Iterators**

Permite percorrer uma lista.

```
class Animal(val name: String)

class Zoo(val animals: List<Animals>) {

    operator fun iterator(): Iterator<Animal> {             
        return animals.iterator()                           
    }
}

fun main() {

    val animals = listOf(Animal("Zebra"), Animal("Lion"));
    val zoo = Zoo(animals)

    for (animal in zoo) {                                   
        println("Watch out, it's a ${animal.name}")
    }

}
```

- **Ranges**
## Coleções