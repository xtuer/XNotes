区别: escape, encodeuri, encodeURIComponent

* ~~**escape**~~**: **deprecated, you shouldn't use.
* **encodeURI: **encodes characters that are not allowed \(raw\) in URLs \(use it to fix up broken URIs if you can't fix them beforehand\), replaces all characters except:

  ```
    ; , / ? : @ & = + $ - _ . ! ~ * ' ( ) # a-z 0-9
  ```

* **encodeURIComponent: **as encodeURI plus characters with special meaning in URIs \(use it to encode data for inserting into a URI\), , replaces all characters except:

  ```
    - _ . ! ~ * ' ( ) a-z 0-9
  ```

For the visually minded, here's a table showing the effects of encodeURI, encodeURIComponent and escape on the commonly-used symbolic ASCII characters:

    char  encURI  encURIComp  escape
    *     *       *           *
    .     .       .           .
    _     _       _           _
    -     -       -           -
    ~     ~       ~           %7E
    '     '       '           %27
    !     !       !           %21
    (     (       (           %28
    )     )       )           %29
    /     /       %2F         /
    +     +       %2B         +
    @     @       %40         @
    ?     ?       %3F         %3F
    =     =       %3D         %3D
    :     :       %3A         %3A
    #     #       %23         %23
    ;     ;       %3B         %3B
    ,     ,       %2C         %2C
    $     $       %24         %24
    &     &       %26         %26
          %20     %20         %20
    %     %25     %25         %25
    ^     %5E     %5E         %5E
    [     %5B     %5B         %5B
    ]     %5D     %5D         %5D
    {     %7B     %7B         %7B
    }     %7D     %7D         %7D
    <     %3C     %3C         %3C
    >     %3E     %3E         %3E
    "     %22     %22         %22
    \     %5C     %5C         %5C
    |     %7C     %7C         %7C
    `     %60     %60         %60

和 Base64 比较: Base64 包含了 `a-z`, `A-Z`, `0-9`, `/`, `+` 等 64 个字符 \(最后有可能包含 `=`，只是填充字符\)

