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

## List

* List basic

```viml
let list = []
let list = ['one', 'two', 'three', 'four']

echo list[0]             " 'one'
echo list[-1]            " 'four'
echo list[9]             " error

echo get(list, 0)        " 'one'
echo get(list, -1)       " 'four'
echo get(list, 9, 'ten') " 'ten'

let size = len(s:list)   " size is 4

echo list[:1]       " ['one', 'two']
echo list[:2]       " ['one', 'two', 'three']

echo list[1:]       " ['two', 'three', 'four']
echo list[2:]       " ['three', 'four']

echo list[0:1]      " ['one', 'two']
echo list[1:2]      " ['two', 'three']
echo list[1:-1]     " ['two', 'three', 'four']
echo list[1:-2]     " ['two', 'three']

let list += ['five', 'six']                 " ['one', 'two', 'three', 'four', 'five', 'six']
let long_list = list + ['seven', 'eight']

call add(long_list, 'nine')

let copied_list = copy(list)
let recursively_copied_list = deepcopy(list)

let list[3:4] = [4, 5]      " ['one', 'two', 'three', 4, 5, 'six']
```

* List unpack

```viml
let list = [1, 2, 3]

let [var1, var2, var3] = list

echo var1   " 1
echo var2   " 2
echo var3   " 3
```

```viml
let list = [1, 2, 3, 4]

let [var1, var2; var3] = list   " use semicolon

echo var1   " 1
echo var2   " 2
echo var3   " [3, 4]
```

* List functions

```viml

" length
echo len([1, 2, 3])     " 3

" check empty
echo empty([1, 2, 3])   " 0
echo empty([])          " 1

" remove
let list = [1, 2, 3]
call remove(list, 1)                " [1, 3]
let removed_item = remove(list, 0)  " removed_item is 1, list is [3]

" filter
let list = [1, 2, 3]
call filter(list, {idx, val -> val > 1})    " use lambda
echo list   " [2, 3]

" map
let list = [1, 2, 3]
call map(list, {idx, val -> val * 10})
echo list   " [10, 20, 30]

" sort, reverse, uniq, max, min
call sort(list)
call reverse(list)
call uniq(list)
let max = max(list)
let min = min(list)

" count, index
let list = [1, 2, 3, 4, 5, 5]
echo count(list, 5)             " 2
echo index(list, 2)             " 1

" split, join
let list = split('1 2 3', '\s') " ['1', '2', '3']
let str = join(list, '-')       " '1-2-3'
```

