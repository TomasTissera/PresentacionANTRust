# Rust

RUST es un lenguaje de programación que su primera versión estable fue publicada el día 15 de Mayo del año 2015, desarrollado por Mozilla, sus objetivos principales son:

  - Un diseño e implementación de un lenguaje de programación que sea práctico
  - Multiparadigma
  - Orientado a objetos
  - Potente
  - Seguro
  - Veloz

### Características de RUST

  - Ejecución dinámica de seguridad (errores y registros).
  - Orientado a Objetos.
  - Interfaz simple.
  - Gestión automática de guardado.
  - Inmutable.
  - Compilación nativa y estática.
  - Multiplataforma.
  - Control de la memoria explícita.
  - Permite cadenas UTF8.
  - Multiparadigmático.
  - Concurrente.

Ventajas de RUST:
  - A nivel global, Rust permite desarrollar grandes programas del lado del cliente y del servidor mejorando la calidad del software, sin necesidad de requerir más poder del hardware que lo ejecuta considerando esta como una de las principales ventajas que ofrece. Adicionalmente, gracias al compilador de este, se cumplen convenientemente las garantías de seguridad del resto de las validaciones que conllevan que este lenguaje sea eficiente y seguro.
### Instalación 

Instalación en Linux o macOS

```sh
$  curl --proto '=https' --tlsv1.2 https://sh.rustup.rs -sSf | sh
```

Instalación en Windows:
Tiene que ser desde la pagina oficial de [Rust](https://www.rust-lang.org/tools/install) 

### Hola Mundo!
```sh
main.rs:
	fn main() {
  	  println!("Hello, world!");
}
```

Revisaremos paso a paso lo que sucedio en nuestro hola mundo


> fn main(){
> }

Estas líneas definen una función en Rust. La función principal es especial: siempre es el primer código que se ejecuta en cada programa ejecutable de Rust. La primera línea declara una función llamada main que no tiene parámetros y no devuelve nada. Si hubiera parámetros, irían entre paréntesis, ()
Además, tenga en cuenta que el cuerpo de la función está entre llaves, {}. Rust los requiere en todos los cuerpos funcionales. Es un buen estilo colocar el corchete de apertura en la misma línea que la declaración de función, agregando un espacio entre ellos.
> println!("Hello, world!");


Esta línea hace todo el trabajo en este pequeño programa: 
- Imprime texto en la pantalla. Hay cuatro detalles importantes a tener en cuenta aquí. 
  - Primero, el estilo Rust es sangrar con cuatro espacios, no una tabulación. En segundo lugar, imprima! llama a una macro Rust. Si en su lugar llamara a una función, se ingresaría como println (¡sin el!). 
  -  Discutiremos las macros de Rust con más detalle en el Capítulo 19. Por ahora, solo necesita saber que usar un! significa que está llamando a una macro en lugar de a una función normal. 
  - En tercer lugar, verá el mensaje "¡Hola, mundo!" cuerda. Pasamos esta cadena como argumento a println !, y la cadena se imprime en la pantalla. Cuarto, terminamos la línea con un punto y coma (;), lo que indica que esta expresión ha terminado y la siguiente está lista para comenzar. La mayoría de las líneas de código de Rust terminan con un punto y coma.
### Compilado
Al compilarlo rust genera un ejecutable binario
- En linux o Mac:
```sh
$ rustc main.rs
$ ./mian
Hello, world!
```
- En Windows:
```sh
$ rustc main.rs
$ ./mian.exe
Hello, world!
```
## Cargo
Cargo es el sistema de construcción y el administrador de paquetes de Rust. La mayoría de los rustáceos usan esta herramienta para administrar sus proyectos de Rust porque Cargo maneja muchas tareas por usted, como construir su código, descargar las bibliotecas de las que depende su código y construir esas bibliotecas. (Llamamos a las bibliotecas su código necesita dependencias).

°Compilar con Cargo:
```sh
$ cargo build
    Compiling hello_cargo v0.1.0 (file:///projects/hello_cargo)
    Finished dev [unoptimized + debuginfo] target(s) in 2.85 secs
```
°Compilar y ejecutar con cargo
```sh
$ cargo run
    Finished dev [unoptimized + debuginfo] target(s) in 0.0 secs
     Running `target/debug/hello_cargo`
Hello, world!
```
Creemos un nuevo proyecto con Cargo y observemos en qué se diferencia de nuestro original "¡Hola, mundo!" . 
En cualquier sistema operativo, ejecute lo siguiente:
```sh
$ cargo new hello_cargo
$ cd hello_cargo
```
Cargo genera a la par del main.rs el archivo Cargo.toml:

```sh
[package]
name = "hello_cargo"
version = "0.1.0"
authors = ["Your Name <you@example.com>"]
edition = "2018"

[dependencies]
```
La primera línea, [package], es un encabezado de sección que indica que las siguientes declaraciones están configurando un paquete. A medida que agreguemos más información a este archivo, agregaremos otras secciones.
Las siguientes cuatro líneas establecen la información de configuración que Cargo necesita para compilar su programa: el nombre, la versión, quién lo escribió y la edición de Rust que debe usar. Cargo obtiene su nombre y la información de correo electrónico de su entorno, por lo que si esa información no es correcta, corrija la información ahora y luego guarde el archivo. Hablaremos sobre la clave de edition  en el Apéndice E.
La última línea, [dependencies], es el comienzo de una sección para que enumeres cualquiera de las dependencias de tu proyecto. En Rust, los paquetes de código se denominan cajas. No necesitaremos otras cajas para este proyecto, pero lo haremos en el primer proyecto del Capítulo 2, por lo que usaremos esta sección de dependencias.

## Programación de un juego de adivinanzas
- Configurar un nuevo proyecto
```sh
$ cargo new guessing_game
$ cd guessing_game
```
La primera parte del programa del juego de adivinanzas solicitará la entrada del usuario, procesará esa entrada y verificará que la entrada esté en la forma esperada. 
```sh
use std::io;

fn main() {
    println!("Guess the number!");

    println!("Please input your guess.");

    let mut guess = String::new();

    io::stdin()
        .read_line(&mut guess)
        .expect("Failed to read line");

    println!("You guessed: {}", guess);
}
```
Para obtener la entrada del usuario y luego imprimir el resultado como salida, necesitamos traer la biblioteca io (entrada / salida) al alcance. La biblioteca io proviene de la biblioteca estándar (que se conoce como std):
> use std::io;

El siguiente código imprime un mensaje que indica qué es el juego y solicita información del usuario.

> println!("Guess the number!");
> println!("Please input your guess.");

A continuación, crearemos un lugar para almacenar la entrada del usuario, como este:
>    let mut guess = String::new();

----------------------------------------------
 let usa para crear una variable 
 > let foo = 5; // immutable
 > let mut bar = 5; // mutable
--------------------------------------------
Ahora llamaremos a la función stdin desde el módulo io:
>    io::stdin()
>        .read_line(&mut guess)

Si no hubiéramos puesto la línea use std :: io al principio del programa, podríamos haber escrito esta llamada de función como std :: io :: stdin. La función stdin devuelve una instancia de std :: io :: Stdin, que es un tipo que representa un identificador para la entrada estándar de su terminal.

La ultima linea nos devolvera una salida de texto con el numero que hemos ingresado
>    println!("You guessed: {}", guess);

Necesariamos que se genere un numero alateoreo para poder adivinarlo:
- Icorporamos la dependencia " rand = "0.5.5" " en el archivo Cargo.toml
>[dependencies]
>rand = "0.5.5"

Luego comprimiremos el proyecto para que se actualizen las dependencias 
```sh
$ cargo build
    Updating crates.io index
  Downloaded rand v0.5.5
  Downloaded libc v0.2.62
  Downloaded rand_core v0.2.2
  Downloaded rand_core v0.3.1
  Downloaded rand_core v0.4.2
   Compiling rand_core v0.4.2
   Compiling libc v0.2.62
   Compiling rand_core v0.3.1
   Compiling rand_core v0.2.2
   Compiling rand v0.5.5
   Compiling guessing_game v0.1.0 (file:///projects/guessing_game)
    Finished dev [unoptimized + debuginfo] target(s) in 2.53s

```

```sh
use std::io;
use rand::Rng;

fn main() {
    println!("Guess the number!");

    let secret_number = rand::thread_rng().gen_range(1, 101);

    println!("The secret number is: {}", secret_number);

    println!("Please input your guess.");

    let mut guess = String::new();

    io::stdin()
        .read_line(&mut guess)
        .expect("Failed to read line");

    println!("You guessed: {}", guess);
}
```
Como primera intancia importaremos en nuestro archivo la dependecia que incorporamos al proyecto
> use rand::Rng;

Luego creamos una variable donde se creara nustro numero secreto "secret_number "
> let secret_number = rand::thread_rng().gen_range(1, 101);

el numero secreto se genara desde 1 al 101

Ahoras aremos que se comparen el valor ingresado y el numero secreto 

> use std::cmp::Ordering;

Llamaremos a  "std :: cmp :: Ordering " al alcance de la biblioteca estándar. Al igual que Result, Ordering es otra enumeración, pero las variantes de Ordering son Less, Greater e Equal. Estos son los tres resultados que son posibles cuando compara dos valores.

```sh
    // --snip--
    let mut guess = String::new();

    io::stdin()
        .read_line(&mut guess)
        .expect("Failed to read line");

    let guess: u32 = guess.trim().parse().expect("Please type a number!");

    println!("You guessed: {}", guess);

    match guess.cmp(&secret_number) {
        Ordering::Less => println!("Too small!"),
        Ordering::Greater => println!("Too big!"),
        Ordering::Equal => println!("You win!"),
    }
}
```
Creamos una variable llamada conjetura. Pero espere, ¿el programa no tiene ya una variable llamada conjetura? Lo hace, pero Rust nos permite sombrear el valor anterior de adivinar con uno nuevo. Esta función se utiliza a menudo en situaciones en las que desea convertir un valor de un tipo a otro. El sombreado nos permite reutilizar el nombre de la variable de conjetura en lugar de obligarnos a crear dos variables únicas, como guess_str y guess, por ejemplo. 
> let guess: u32 = guess.trim().parse().expect("Please type a number!");


```sh
$ cargo run
   Compiling guessing_game v0.1.0 (file:///projects/guessing_game)
    Finished dev [unoptimized + debuginfo] target(s) in 0.43s
     Running `target/debug/guessing_game`
Guess the number!
The secret number is: 58
Please input your guess.
  76
You guessed: 76
Too big!
```
Ahora nustro programa compara el dato ingresado y el numero secreto generado diciendonos si el numero ingresadi es mayor "Too big!" o si es menor "Too small!", pero nos faltaria que el programa termine cuando se alla adivinado el numero secreto, para ello incorporaremos el programa dentro de un "loop":
```sh
use rand::Rng;
use std::cmp::Ordering;
use std::io;

fn main() {
    println!("Guess the number!");

    let secret_number = rand::thread_rng().gen_range(1, 101);

    // --snip--

    println!("The secret number is: {}", secret_number);

    loop {
        println!("Please input your guess.");

        // --snip--


        let mut guess = String::new();

        io::stdin()
            .read_line(&mut guess)
            .expect("Failed to read line");

        let guess: u32 = guess.trim().parse().expect("Please type a number!");

        println!("You guessed: {}", guess);

        match guess.cmp(&secret_number) {
            Ordering::Less => println!("Too small!"),
            Ordering::Greater => println!("Too big!"),
            Ordering::Equal => println!("You win!"),
        }
    }
}
```
Y para que el programa termine cuando se alla adivinado el numero secreto aremos que el "loop" termine :
```sh
match guess.cmp(&secret_number) {
            Ordering::Less => println!("Too small!"),
            Ordering::Greater => println!("Too big!"),
            Ordering::Equal => {
                println!("You win!");
                break;
            }
```
```sh
$ cargo run
   Compiling guessing_game v0.1.0 (file:///projects/guessing_game)
     Running `target/debug/guessing_game`
Guess the number!
The secret number is: 61
Please input your guess.
10
You guessed: 10
Too small!
Please input your guess.
99
You guessed: 99
Too big!
Please input your guess.
foo
Please input your guess.
61
You guessed: 61
You win!
```
