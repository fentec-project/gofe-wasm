## Call GoFE functions from JavaScript

Main.go contains function **risk** which uses GoFE to encrypt the vector **x** (more below).

The following command grabs main.go and builds lib.wasm - a file that contains functions registered in Main.go and can be used by JavaScript:

```
GOOS=js GOARCH=wasm go build -o lib.wasm
```

Make sure you are using wasm_exec.js from the same version of Golang as was used to compile the binary.
That means get GOROOT/misc/wasm/wasm_exec.js on your computer and put it in this folder (replace the existing wasm_exec.js).

Then run:

```
goexec 'http.ListenAndServe(":8081", http.FileServer(http.Dir(".")))'
```

Open http://localhost:8081 in the browser.

Two functions are registered in main.go to be used from JavaScript: **risk** and **add**.

The function **risk** reads the parameters on the website (age, systolic blood pressure, ...) and encrypts them using GoFE. The ciphertext is written out in the debugging console.
See privacy-friendly-analyses repository for more about the privacy-friendly computation of the risk of developing the cardiovascular diseases. 

The function **add** reads the Number 1 and Number 2, computes the sum (in Go), and writes out the result in the last text field on the website.

