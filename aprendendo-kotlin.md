# Aprendendo Kotlin e Sua Documentação Oficial

## Introdução ao Kotlin

- Linguagem recente mas madura;
- Interoperável com Java e outras linguagens;
- Virou linguagem oficial para desenvolvimento mobile pela Google;
- Não está mais atrelada apenas com o desenvolvimento de aplicativos mobile;
- Oferece muitas opções para reutilizar código entre várias plataformas;
- Está ampliando seus "horizontes";
- O Kotlin está incluso no **IntelliJ IDEA** e **Android Studio** mas pode ser utilizado através do [Kotlin Playground](https://play.kotlinlang.org/).

**Documentação**

- [Documentação Oficial - kotlinlang.org](https://kotlinlang.org/)
- [Introdução ao Kotlin](https://kotlinlang.org/docs/getting-started.html)

## Introdução Prática à Linguagem de Programação Kotlin

[Learn Kotlin by Example](https://play.kotlinlang.org/byExample/overview)

**Hello World**

```
// Definindo o pacote (muito comum para organização do código)
// site ao contrário e depois o nome desse pacote
package me.dio.helloworld 

// Ponto de entrada de um código Kotlin, definido pela função [main]
fun main() {
    // Imprime na saída padrão um texto, pulando linha por causa do ln
    // se fosse apenas print ele não pularia a linha
    println("Hello, World!")
    print("Exemplo de que")
    print("Não pulou a linha")
}
```

**Funções**
**- Valores de Parâmetro Padrão e Argumentos Nomeados:**

```
// função que recebe como parâmetro um texto, alfanumérico, para realizar as operações dentro dela
// um pouco redundante esse função pois é possível chamar um println de forma mais simples
// mas serve como exemplo de como criar um parâmetro
fun printMessage(message: String): Unit {                               
    println(message)
}

// função que imprime uma mensagem com um prefixo
// Info é um prefixo padrão para caso não seja especificado 
fun printMessageWithPrefix(message: String, prefix: String = "Info") {  
    // interpolação de strings
    // método mais simples de concatenar 
    println("[$prefix] $message")
}

// função de soma
// existe um retorno explicíto, como int (inteiro)
fun sum(x: Int, y: Int): Int {                                          
    return x + y
}

// inline function: está sendo definida em apenas uma linha
// função de multiplicação
// retorno declarado implicitamente
fun multiply(x: Int, y: Int) = x * y                                    

// função principal que irá executar as funções anteriores passando os valores para que elas funcionem 
fun main() {
    printMessage("Hello")  

    // sem definir o prefixo
    printMessageWithPrefix("World")

    // com prefixo definido na ordem que foi criado na função
    // message e depois prefix
    printMessageWithPrefix("World", "Hello") 

    // com prefixo definido em outra ordem pois conseguimos definir quem é quem
    printMessageWithPrefix(prefix = "Hello", message = "World") 

    // chamando as outras duas funções de conta          
    println(sum(1, 2))                                                  
    println(multiply(2, 4))                                            
}
```

**- Parâmetros vararg**
Varargs permitem que você passe qualquer número de argumentos, desde que respeitem o tipo especificado (string, int, etc) separando-os com vírgulas.
```
// função principal
// note que as funções podem ser criadas dentro dela 
// sendo assim possível criar um tipo de hierarquia de funções
fun main() {

    // função que pega todas as mensagens e printa elas 
    // chama messages de m para simplificar
    fun printAll(vararg messages: String) {                            // 1
        for (m in messages) println(m)
    }
    // inserindo strings 
    printAll("Hello", "Hallo", "Salut", "Hola", "你好", "Olá")                 // 2
    
    // mesma coisa mas definindo um prefixo 
    fun printAllWithPrefix(vararg messages: String, prefix: String) {  // 3
        for (m in messages) println(prefix + m)
    }
    printAllWithPrefix(
            "Hello", "Hallo", "Salut", "Hola", "你好",
            prefix = "Greeting: "                                          // 4
    )

    // função que chama outra que também é um vararg
    fun log(vararg entries: String) {
        // necessário o * para identificar esses dados como vararg e não como array
        // nos outros casos estava como array
        printAll(*entries)                                             // 5
    }
    log("Hello", "Hallo", "Salut", "Hola", "你好")

}
```

**Variáveis var e val**