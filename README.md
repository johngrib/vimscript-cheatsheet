# vimscript-cheatsheet
vimscript cheatsheet

`:help script` - If you want to know more about vimscript

## Hello, World!

```viml
echo 'Hello, World!'
```

* `echomsg` is same with `echo`. but `echomsg` saves message history.
* You can see the message history with `:message`.

```viml
echomsg 'Hello, Vimscript!'
```

## variables: Number, Float, String

```viml
" Number is integer
let number = 42     " Defines Number
let number += 1     " 43

echomsg number      " print 43

unlet number        " Undefines number

echo number         " error
```

```viml
let pi = 3.141592

" parseInt
let pi_int = float2nr(pi)   " 3

" toString
let pi_str = string(pi)     " '3.141592'
```

```viml
let name = 'John'               " 'John'
let size = strchars(name)       " 4

" concat string
let full_name = name . ' Grib'  " 'John Grib'

" substring
echo strcharpart(full_name, 5, 1)   " 'G'
```

## namespaces

* `g:` - Global.

* `l:` - Local to a function.
* `s:` - Local to a script file.
* `a:` - Function argument (only inside a function).

* `v:` - Global, predefined by Vim.

* `b:` - Local to the current buffer.
* `w:` - Local to the current window.
* `t:` - Local to the current tab page.

```viml
let g:number = 42       " global
let s:number = 67       " script scope

function s:foo(number)  " function : script scope

    echo g:number . ' is global.'
    echo a:number . ' is argument.'

    let l:number = 23

    echo l:number . ' is local.'

endfunction

call s:foo(s:number)
    " 42 is global.
    " 67 is argument.
    " 23 is local.
```
