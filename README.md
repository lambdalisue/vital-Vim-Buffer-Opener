vital-Vim-Buffer-Opener
==============================================================================
[![Codecov](https://img.shields.io/codecov/c/github/lambdalisue/vital-Vim-Buffer-Opener/master.svg?style=flat-square)](https://codecov.io/gh/lambdalisue/vital-Vim-Buffer-Opener)
[![Travis CI](https://img.shields.io/travis/lambdalisue/vital-Vim-Buffer-Opener/master.svg?style=flat-square&label=Travis%20CI)](https://travis-ci.org/lambdalisue/vital-Vim-Buffer-Opener)
[![AppVeyor](https://img.shields.io/appveyor/ci/lambdalisue/vital-Vim-Buffer-Opener/master.svg?style=flat-square&label=AppVeyor)](https://ci.appveyor.com/project/lambdalisue/vital-Vim-Buffer-Opener/branch/master)
![Version 1.0.0](https://img.shields.io/badge/version-1.0.0-yellow.svg?style=flat-square)
![Support Vim 8.0.0000 or above](https://img.shields.io/badge/support-Vim%208.0.0000%20or%20above-yellowgreen.svg?style=flat-square)
![Support Neovim 0.2.0 or above](https://img.shields.io/badge/support-Neovim%200.2.0%20or%20above-yellowgreen.svg?style=flat-square)
[![MIT License](https://img.shields.io/badge/license-MIT-blue.svg?style=flat-square)](LICENSE)
[![Doc](https://img.shields.io/badge/doc-%3Ah%20Vital.Vim.Buffer.Opener-orange.svg?style=flat-square)](doc/Vital/Vim/Buffer/Opener.txt)

*Vital.Vim.Buffer.Opener* is a simple library to open a buffer.

Following example directly use `append()` function just after opening a buffer.

```vim
let s:Opener = vital#vital#import('Vim.Buffer.Opener')

function! s:open_pseudo_file(opener) abort
  let config = { 'opener': a:opener }
  let context = s:Opener.open('a pseudo file', config)

  " The focus is on a target buffer even an opener for preview window
  " such as 'pedit' has specified so using append() directly is safe.
  call append(line('$'), ['This is a pseudo content'])

  " Focus back if necessary
  call context.end()
endfunction

command! -nargs=* OpenPseudoFile call s:open_pseudo_file(<q-args>)
```

Basically when `{opener}` is an opener for preview window (e.g `pedit`), `append()` will be pefromed on a wrong buffer because `pedit` does not move the focus to a opened buffer.
Using `Vital.Vim.Buffer.Opener` solve this issue by focusing a specified buffer even the buffer is a `previewwindow`.
