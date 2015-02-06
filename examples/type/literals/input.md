Numeric literals can be type annotated by adding the type as a suffix, with the
exception of `usize` that uses the `us` suffix and `isize` that uses the `is`
suffix.

The type of unsuffixed literals will depend on how they are used. If no
constraint exists, the compiler will raise an error.

{literals.play}

There are some concepts used in the previous code that haven't been explained
yet, here's a brief explanation for the impatient readers:

* `fun(&foo)` is used to pass an argument to a function *by reference*, rather
  than by value (`fun(foo)`). For more details see [borrowing][borrow].
* `std::mem::size_of_val` is a function, but called with its *full path*. Code
  can be split in logical units called *modules*. In this case, the
  `size_of_val` function is defined in the `mem` module, and the `mem` module
  is defined in the `std` *crate*. For more details, see
  [modules][mod] and [crates][crate].

[borrow]: /borrow.html
[mod]: /mod.html
[crate]: /crates.html
