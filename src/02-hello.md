# Hello, world!

In this chapter we will create a simple HTML "hello world" program and use the Haskell toolchain
to compile and run it.

> If you haven't installed a Haskell toolchain yet, visit
> [haskell.org/downloads](https://haskell.org/downloads) for instructions on how to download
> and install a Haskell toolchain.

COMMENT: It is unclear if we should install cabal or stack? On haskell.org/downloads they keep mentioning both. As former user of stack and now cabal user, I would probably vote for cabal, since it seems to be close to stack these days + it is more actively developed.

COMMENT: What about the editor? Maybe mention VSCode as ok option to get started quickly and easily?

COMMENT: I wonder if you should have them set up cabal project now, or relatively soon. Since this is a practical book, ideally buy the end of it I would be ready to create a proper Haskell project -> and if I never used cabal but just runghc, I won't be ready. But probably better to do it later in the book?

## A Haskell source file

A Haskell source file is composed of definitions.

The most common type of definitions have the following form:

```hs
<name> = <expression>
```

Note that:

1. We cannot write expressions without binding them to a name
2. Names must start with a lowercase letter
3. We cannot use the same name more than once in a file

A source file containing a definition of the name `main` can be treated as an executable,
and the expression that name `main` is bound to is the entry point to the program.

Let's create a new Haskell source file called `hello.hs`, and write the following line there:

```hs
main = putStrLn "<html><body>Hello, world!</body></html>"
```

We've defined a new name, `main`, and bound it to the expression `putStrLn "<html><body>Hello, world!</body></html>"`.

The body of `main` is calling the function `putStrLn` with the string `"<html><body>Hello, world!</body></html>"`
as input. `putStrLn` takes a single string as input and prints that string to the standard output.

__Note__: In Haskell, we don't need parenthesis after the function name to pass arguments to function.

Running this program will result in the following text printed on the screen:

```
<html><body>Hello, world!</body></html>
```

## Compiling programs

To run this little program, we can compile it using the command line program `ghc`:

```sh
> ghc hello.hs
[1 of 1] Compiling Main             ( hello.hs, hello.o )
Linking hello ...
```

Invoking `ghc` with `hello.hs` will create the following artifact files:

1. `hello.o` - Object file
2. `hello.hi` - Haskell interface file
3. `hello` - A native executable file

And after the compilation, we can run the `hello` executable:

```sh
> ./hello
<html><body>Hello, world!</body></html>
```

## Interpreting programs

Alternatively, we can skip the compilation and creation of artifact files phase, and run the source file directly
using the command line program `runghc`:

```sh
> runghc hello.hs
<html><body>Hello, world!</body></html>
```

We can also redirect the output of the program to a file and then open it in Firefox.

```sh
> runghc hello.hs > hello.html
> firefox hello.html
```

This command should open Firefox and display a web page with `Hello, world!` written in it.

I recommend using `runghc` with this tutorial. While compiling produces significantly faster programs,
intepreting programs provides us with faster feedback while we are developing and making frequent changes.

> If you want to learn more about the core Haskell tools, you can read
> [this article](https://gilmi.me/blog/post/2021/08/14/hs-core-tools),
> but what's described above is enough for our usage at the moment.
## More bindings

We can define the HTML string passed to `putStrLn` in a new name instead of passing
it directly to `putStrLn`. Change the content of file `hello.hs` we defined above to:

```hs
main = putStrLn myhtml

myhtml = "<html><body>Hello, world!</body></html>"
```

__Note__: the order in which we declare the bindings does not matter.

