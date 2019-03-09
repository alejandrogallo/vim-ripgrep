Just add these lines into your `.vimrc`


```vim
function! Rg(...)
  let l:output = system("rg --vimgrep ".join(a:000, " "))
  let l:list = split(l:output, "\n")
  let l:ql = []
  for l:item in l:list
    let sit = split(l:item, ":")
    call add(l:ql,
        \ {"filename": sit[0], "lnum": sit[1], "col": sit[2], "text": sit[3]})
  endfor
  call setqflist(l:ql, 'r')
  echo 'Rg results: '.len(l:ql)
endfunction
command! -nargs=* Rg call Rg(<q-args>)
```

and use it like

```
:Rg something
```

and browse the results with `:cn` and `:cp`.

