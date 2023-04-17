---
title: A lolcat clone
published: true
---

***

## [](#header-1)SETUP

***
lolcat is a commandline tool that takes input and outputs in as colored text.

i am  using the go programming language for this project.

***

## [](#header-2)Prequisitives

***
> You need to have go installed in your system and if you don't here is a tutorial on how to do [that](link to installation page).
>

I'm using GNU/linux  but the commands are similar to windows except where you will replace the touch command with type

``` bash
# create a project directory
mkdir go-lolcat
# move into that directory
cd go-lolcat

# create a main.go file
touch main.go # for *nix and

type main.go # for windows
```
The basic structure for go programs is :
```go
package main //this is very important it helps the go compiler 

import (
  // add your imports here eg,
    "fmt"
)

func main(){
  // code goes here
  fmt.Print("Hello World")
}

```

### [](#header-4)modules we are going to use

*   bufio - it is a package that offers buffered I/O operations.It wraps an io.Reader or io.Writer object, creating another object (Reader or Writer) that also implements the same interface, but provides buffering and some help for textual I/O.
  
*   math - for calculations.
*   fmt - to output to the console.
*   os - it provides a platform independent interface to operating system

***

#### [](#header-5) now lets wrte the program

***
1. import the modules.
  ``` go
  import (
      "bufio"
      "fmt"
      "io"
      "math"
      "os"
  )
  ```
2.  in the main function we are going to do a few things.
   - Check if the input is coming from a pipe
      ```go
            // in the main funtion
             info, _ := os.Stdin.Stat()
        if info.Mode()&os.ModeCharDevice != 0 {
        fmt.Println("The command is intended to work with pipes.")
        fmt.Println("Usage: fortune | go-lolcat")
        }
      ```

    - Read input from the pipe.
      ``` go
      reader := bufio.NewReader(os.Stdin)
      j := 0
      for {
        input, _, err := reader.ReadRune()
        if err != nil && err == io.EOF {
        break
        }
      }
      ```
      
      
3. Now we colorize our input.We will use  a rgb() func that takes an  integer and returns the RGB values of a color.The rainbow color is generated using the rgb() function, as implemented in the original Ruby source code in [https://github.com/busyloop/lolcat/blob/master/lib/lolcat/lol.rb](https://github.com/busyloop/lolcat/blob/master/lib/lolcat/lol.rb).
   ```go
   func rgb(i int) (int, int, int) {
  var f = 0.1
  return int(math.Sin(f*float64(i)+0)*127 + 128),
  int(math.Sin(f*float64(i)+2*math.Pi/3)*127 + 128),
  int(math.Sin(f*float64(i)+4*math.Pi/3)*127 + 128)
  }
```
what this function does is that it generates color using  a sine wave function with a frequency of 0.1.

***

### [](#header-6)The full program should look like this
```go
    package main

    import (
     "bufio"
     "fmt"
     "io"
     "math"
     "os"
    )

    // rgb function takes an integer i and returns three integers representing the RGB values of a color.
    // The color is generated using a sine wave function with a frequency of 0.1.
    func rgb(i int) (int, int, int) {
     var f = 0.1
     return int(math.Sin(f*float64(i)+0)*127 + 128),
      int(math.Sin(f*float64(i)+2*math.Pi/3)*127 + 128),
      int(math.Sin(f*float64(i)+4*math.Pi/3)*127 + 128)
    }

    func main() {
     // Check if the input is coming from a pipe
     info, _ := os.Stdin.Stat()

     if info.Mode()&os.ModeCharDevice != 0 {
      fmt.Println("The command is intended to work with pipes.")
      fmt.Println("Usage: fortune | gorainbow")
     }

     // Read input from the pipe
     reader := bufio.NewReader(os.Stdin)
     j := 0
     for {
      input, _, err := reader.ReadRune()
      if err != nil && err == io.EOF {
       break
      }
      // Generate a color based on the current index j and print the input character in that color
      r, g, b := rgb(j)
      fmt.Printf("\033[38;2;%d;%d;%dm%c\033[0m", r, g, b, input)
      j++
     }
    }
```


* * *

#### Build and Run:

```
  go run .

```
to build
```
  go build -o go-lolcat
```

### to build for other platforms check the go installation [blog](add link).


