The following command will grab main.go and build lib.wasm - a file that can be used by JavaScript:

```
GOOS=js GOARCH=wasm go build -o lib.wasm
```

Make sure you are using wasm_exec.js support script from the same version of Golang as was used to compile binary.
That means grab GOROOT/misc/wasm/wasm_exec.js script on your computer and put it in this folder (replace the existing wasm_exec.js).

Then run:

```
goexec 'http.ListenAndServe(":8081", http.FileServer(http.Dir(".")))'
```

Open http://localhost:8081 in the browser.

Two functions are registered in main.go to be used from JavaScript: risk and add.

The function risk reads the parameters on the site (age, systolic blood pressure, ...) and encrypts them using GoFE. The ciphertext is written out in the debugging console.
See privacy-friendly-analyses repository for more about the privacy-friendly computation of the risk of developing the cardiovascular diseases. 

The function add reads the Number 1 and Number 2, computes the sum (in Go), and writes out the result in the last text field on the site.

