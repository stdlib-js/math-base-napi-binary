<!--

@license Apache-2.0

Copyright (c) 2020 The Stdlib Authors.

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

   http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.

-->


<details>
  <summary>
    About stdlib...
  </summary>
  <p>We believe in a future in which the web is a preferred environment for numerical computation. To help realize this future, we've built stdlib. stdlib is a standard library, with an emphasis on numerical and scientific computation, written in JavaScript (and C) for execution in browsers and in Node.js.</p>
  <p>The library is fully decomposable, being architected in such a way that you can swap out and mix and match APIs and functionality to cater to your exact preferences and use cases.</p>
  <p>When you use stdlib, you can be absolutely certain that you are using the most thorough, rigorous, well-written, studied, documented, tested, measured, and high-quality code out there.</p>
  <p>To join us in bringing numerical computing to the web, get started by checking us out on <a href="https://github.com/stdlib-js/stdlib">GitHub</a>, and please consider <a href="https://opencollective.com/stdlib">financially supporting stdlib</a>. We greatly appreciate your continued support!</p>
</details>

# binary

[![NPM version][npm-image]][npm-url] [![Build Status][test-image]][test-url] [![Coverage Status][coverage-image]][coverage-url] <!-- [![dependencies][dependencies-image]][dependencies-url] -->

> C APIs for registering a Node-API module exporting interfaces for invoking binary numerical functions.

<!-- Section to include introductory text. Make sure to keep an empty line after the intro `section` element and another before the `/section` close. -->

<section class="intro">

</section>

<!-- /.intro -->

<!-- Package usage documentation. -->

<section class="installation">

## Installation

```bash
npm install @stdlib/math-base-napi-binary
```

</section>

<section class="usage">

## Usage

```javascript
var headerDir = require( '@stdlib/math-base-napi-binary' );
```

#### headerDir

Absolute file path for the directory containing header files for C APIs.

```javascript
var dir = headerDir;
// returns <string>
```

</section>

<!-- /.usage -->

<!-- Package usage notes. Make sure to keep an empty line after the `section` element and another before the `/section` close. -->

<section class="notes">

</section>

<!-- /.notes -->

<!-- Package usage examples. -->

<section class="examples">

## Examples

```javascript
var headerDir = require( '@stdlib/math-base-napi-binary' );

console.log( headerDir );
// => <string>
```

</section>

<!-- /.examples -->

<!-- C interface documentation. -->

* * *

<section class="c">

## C APIs

<!-- Section to include introductory text. Make sure to keep an empty line after the intro `section` element and another before the `/section` close. -->

<section class="intro">

</section>

<!-- /.intro -->

<!-- C usage documentation. -->

<section class="usage">

### Usage

```c
#include "stdlib/math/base/napi/binary.h"
```

#### stdlib_math_base_napi_dd_d( env, info, fcn )

Invokes a binary function accepting and returning double-precision floating-point numbers.

```c
#include <node_api.h>

// ...

static double add( const double x, const double y ) {
    return x + y;
}

// ...

/**
* Receives JavaScript callback invocation data.
*
* @param env    environment under which the function is invoked
* @param info   callback data
* @return       Node-API value
*/
napi_value addon( napi_env env, napi_callback_info info ) {
    return stdlib_math_base_napi_dd_d( env, info, add );
}

// ...
```

The function accepts the following arguments:

-   **env**: `[in] napi_env` environment under which the function is invoked.
-   **info**: `[in] napi_callback_info` callback data.
-   **fcn**: `[in] double (*fcn)( double, double )` binary function.

```c
void stdlib_math_base_napi_dd_d( napi_env env, napi_callback_info info, double (*fcn)( double, double ) );
```

#### stdlib_math_base_napi_ff_f( env, info, fcn )

Invokes a binary function accepting and returning single-precision floating-point numbers.

```c
#include <node_api.h>

// ...

static float addf( const float x, const float y ) {
    return x + y;
}

// ...

/**
* Receives JavaScript callback invocation data.
*
* @param env    environment under which the function is invoked
* @param info   callback data
* @return       Node-API value
*/
napi_value addon( napi_env env, napi_callback_info info ) {
    return stdlib_math_base_napi_ff_f( env, info, addf );
}

// ...
```

The function accepts the following arguments:

-   **env**: `[in] napi_env` environment under which the function is invoked.
-   **info**: `[in] napi_callback_info` callback data.
-   **fcn**: `[in] float (*fcn)( float, float )` binary function.

````c
void stdlib_math_base_napi_ff_f( napi_env env, napi_callback_info info, float (*fcn)( float, float ) );
```de "stdlib/math/base/napi/binary.h"
````

#### stdlib_math_base_napi_zz_z( env, info, fcn )

Invokes a binary function accepting and returning double-precision complex floating-point numbers.

```c
#include "stdlib/complex/float64.h"
#include "stdlib/complex/reim.h"
#include <node_api.h>

// ...

static stdlib_complex128_t add( const stdlib_complex128_t x, const stdlib_complex128_t y ) {
    double xre;
    double xim;
    double yre;
    double yim;
    double re;
    double im;

    stdlib_reim( x, &xre, &xim );
    stdlib_reim( y, &yre, &yim );

    re = xre + yre;
    im = xim + yim;

    return stdlib_complex128( re, im );
}

// ...

/**
* Receives JavaScript callback invocation data.
*
* @param env    environment under which the function is invoked
* @param info   callback data
* @return       Node-API value
*/
napi_value addon( napi_env env, napi_callback_info info ) {
    return stdlib_math_base_napi_zz_z( env, info, add );
}

// ...
```

The function accepts the following arguments:

-   **env**: `[in] napi_env` environment under which the function is invoked.
-   **info**: `[in] napi_callback_info` callback data.
-   **fcn**: `[in] stdlib_complex128_t (*fcn)( stdlib_complex128_t, stdlib_complex128_t )` binary function.

```c
void stdlib_math_base_napi_zz_z( napi_env env, napi_callback_info info, stdlib_complex128_t (*fcn)( stdlib_complex128_t, stdlib_complex128_t ) );
```

#### stdlib_math_base_napi_cc_c( env, info, fcn )

Invokes a binary function accepting and returning single-precision complex floating-point numbers.

```c
#include "stdlib/complex/float64.h"
#include "stdlib/complex/reim.h"
#include <node_api.h>

// ...

static stdlib_complex64_t add( const stdlib_complex64_t x, const stdlib_complex64_t y ) {
    float xre;
    float xim;
    float yre;
    float yim;
    float re;
    float im;

    stdlib_reimf( x, &xre, &xim );
    stdlib_reimf( y, &yre, &yim );

    re = xre + yre;
    im = xim + yim;

    return stdlib_complex64( re, im );
}

// ...

/**
* Receives JavaScript callback invocation data.
*
* @param env    environment under which the function is invoked
* @param info   callback data
* @return       Node-API value
*/
napi_value addon( napi_env env, napi_callback_info info ) {
    return stdlib_math_base_napi_cc_c( env, info, add );
}

// ...
```

The function accepts the following arguments:

-   **env**: `[in] napi_env` environment under which the function is invoked.
-   **info**: `[in] napi_callback_info` callback data.
-   **fcn**: `[in] stdlib_complex64_t (*fcn)( stdlib_complex64_t, stdlib_complex64_t )` binary function.

```c
void stdlib_math_base_napi_cc_c( napi_env env, napi_callback_info info, stdlib_complex64_t (*fcn)( stdlib_complex64_t, stdlib_complex64_t ) );
```

#### stdlib_math_base_napi_di_d( env, info, fcn )

Invokes a binary function accepting a double-precision floating-point number and a signed 32-bit integer and returning a double-precision floating-point number.

```c
#include <node_api.h>
#include <stdint.h>

// ...

static double mul( const double x, const int32_t y ) {
    return x * y;
}

// ...

/**
* Receives JavaScript callback invocation data.
*
* @param env    environment under which the function is invoked
* @param info   callback data
* @return       Node-API value
*/
napi_value addon( napi_env env, napi_callback_info info ) {
    return stdlib_math_base_napi_di_d( env, info, mul );
}

// ...
```

The function accepts the following arguments:

-   **env**: `[in] napi_env` environment under which the function is invoked.
-   **info**: `[in] napi_callback_info` callback data.
-   **fcn**: `[in] double (*fcn)( double, int32_t )` binary function.

```c
void stdlib_math_base_napi_di_d( napi_env env, napi_callback_info info, double (*fcn)( double, int32_t ) );
```

#### stdlib_math_base_napi_fi_f( env, info, fcn )

Invokes a binary function accepting a single-precision floating-point number and a signed 32-bit integer and returning a single-precision floating-point number.

```c
#include <node_api.h>
#include <stdint.h>

// ...

static float mulf( const float x, const int32_t y ) {
    return x * y;
}

// ...

/**
* Receives JavaScript callback invocation data.
*
* @param env    environment under which the function is invoked
* @param info   callback data
* @return       Node-API value
*/
napi_value addon( napi_env env, napi_callback_info info ) {
    return stdlib_math_base_napi_fi_f( env, info, mulf );
}

// ...
```

The function accepts the following arguments:

-   **env**: `[in] napi_env` environment under which the function is invoked.
-   **info**: `[in] napi_callback_info` callback data.
-   **fcn**: `[in] float (*fcn)( float, int32_t )` binary function.

```c
void stdlib_math_base_napi_fi_f( napi_env env, napi_callback_info info, float (*fcn)( float, int32_t ) );
```

#### stdlib_math_base_napi_zi_z( env, info, fcn )

Invokes a binary function accepting a double-precision complex floating-point number and a signed 32-bit integer and returning a double-precision complex floating-point number.

```c
#include "stdlib/complex/float64.h"
#include "stdlib/complex/reim.h"
#include <node_api.h>
#include <stdint.h>

// ...

static stdlib_complex128_t mul( const stdlib_complex128_t x, const int32_t y ) {
    double xre;
    double xim;
    double re;
    double im;

    stdlib_reim( x, &xre, &xim );

    re = xre * y;
    im = xim * y;

    return stdlib_complex128( re, im );
}

// ...

/**
* Receives JavaScript callback invocation data.
*
* @param env    environment under which the function is invoked
* @param info   callback data
* @return       Node-API value
*/
napi_value addon( napi_env env, napi_callback_info info ) {
    return stdlib_math_base_napi_zi_z( env, info, mul );
}

// ...
```

The function accepts the following arguments:

-   **env**: `[in] napi_env` environment under which the function is invoked.
-   **info**: `[in] napi_callback_info` callback data.
-   **fcn**: `[in] stdlib_complex128_t (*fcn)( stdlib_complex128_t, int32_t )` binary function.

```c
void stdlib_math_base_napi_zi_z( napi_env env, napi_callback_info info, stdlib_complex128_t (*fcn)( stdlib_complex128_t, int32_t ) );
```

#### stdlib_math_base_napi_ci_c( env, info, fcn )

Invokes a binary function accepting a single-precision complex floating-point number and a signed 32-bit integer and returning a single-precision complex floating-point number.

```c
#include "stdlib/complex/float64.h"
#include "stdlib/complex/reimf.h"
#include <node_api.h>
#include <stdint.h>

// ...

static stdlib_complex64_t mul( const stdlib_complex64_t x, const int32_t y ) {
    float xre;
    float xim;
    float re;
    float im;

    stdlib_reimf( x, &xre, &xim );

    re = xre * y;
    im = xim * y;

    return stdlib_complex64( re, im );
}

// ...

/**
* Receives JavaScript callback invocation data.
*
* @param env    environment under which the function is invoked
* @param info   callback data
* @return       Node-API value
*/
napi_value addon( napi_env env, napi_callback_info info ) {
    return stdlib_math_base_napi_ci_c( env, info, mul );
}

// ...
```

The function accepts the following arguments:

-   **env**: `[in] napi_env` environment under which the function is invoked.
-   **info**: `[in] napi_callback_info` callback data.
-   **fcn**: `[in] stdlib_complex64_t (*fcn)( stdlib_complex64_t, int32_t )` binary function.

```c
void stdlib_math_base_napi_ci_c( napi_env env, napi_callback_info info, stdlib_complex64_t (*fcn)( stdlib_complex64_t, int32_t ) );
```

#### STDLIB_MATH_BASE_NAPI_MODULE_DD_D( fcn )

Macro for registering a Node-API module exporting an interface for invoking a binary function accepting and returning double-precision floating-point numbers.

```c
static double add( const double x, const double y ) {
    return x + y;
}

// ...

// Register a Node-API module:
STDLIB_MATH_BASE_NAPI_MODULE_DD_D( add );
```

The macro expects the following arguments:

-   **fcn**: `double (*fcn)( double, double )` binary function.

When used, this macro should be used **instead of** `NAPI_MODULE`. The macro includes `NAPI_MODULE`, thus ensuring Node-API module registration.

#### STDLIB_MATH_BASE_NAPI_MODULE_FF_F( fcn )

Macro for registering a Node-API module exporting an interface for invoking a binary function accepting and returning single-precision floating-point numbers.

```c
static float addf( const float x, const float y ) {
    return x + y;
}

// ...

// Register a Node-API module:
STDLIB_MATH_BASE_NAPI_MODULE_FF_F( addf );
```

The macro expects the following arguments:

-   **fcn**: `float (*fcn)( float, float )` binary function.

When used, this macro should be used **instead of** `NAPI_MODULE`. The macro includes `NAPI_MODULE`, thus ensuring Node-API module registration.

#### STDLIB_MATH_BASE_NAPI_MODULE_ZZ_Z( fcn )

Macro for registering a Node-API module exporting an interface for invoking a binary function accepting and returning double-precision complex floating-point numbers.

```c
#include "stdlib/complex/float64.h"
#include "stdlib/complex/reim.h"

static stdlib_complex128_t add( const stdlib_complex128_t x, const stdlib_complex128_t y ) {
    double xre;
    double xim;
    double yre;
    double yim;
    double re;
    double im;

    stdlib_reim( x, &xre, &xim );
    stdlib_reim( y, &yre, &yim );

    re = xre + yre;
    im = xim + yim;

    return stdlib_complex128( re, im );
}

// ...

// Register a Node-API module:
STDLIB_MATH_BASE_NAPI_MODULE_ZZ_Z( add );
```

The macro expects the following arguments:

-   **fcn**: `stdlib_complex128_t (*fcn)( stdlib_complex128_t, stdlib_complex128_t )` binary function.

When used, this macro should be used **instead of** `NAPI_MODULE`. The macro includes `NAPI_MODULE`, thus ensuring Node-API module registration.

#### STDLIB_MATH_BASE_NAPI_MODULE_CC_C( fcn )

Macro for registering a Node-API module exporting an interface for invoking a binary function accepting and returning single-precision complex floating-point numbers.

```c
#include "stdlib/complex/float32.h"
#include "stdlib/complex/reimf.h"

static stdlib_complex64_t add( const stdlib_complex64_t x, const stdlib_complex64_t y ) {
    float xre;
    float xim;
    float yre;
    float yim;
    float re;
    float im;

    stdlib_reimf( x, &xre, &xim );
    stdlib_reimf( y, &yre, &yim );

    re = xre + yre;
    im = xim + yim;

    return stdlib_complex64( re, im );
}

// ...

// Register a Node-API module:
STDLIB_MATH_BASE_NAPI_MODULE_CC_C( add );
```

The macro expects the following arguments:

-   **fcn**: `stdlib_complex64_t (*fcn)( stdlib_complex64_t, stdlib_complex64_t )` binary function.

When used, this macro should be used **instead of** `NAPI_MODULE`. The macro includes `NAPI_MODULE`, thus ensuring Node-API module registration.

#### STDLIB_MATH_BASE_NAPI_MODULE_DI_D( fcn )

Macro for registering a Node-API module exporting an interface invoking a binary function accepting a double-precision floating-point number and a signed 32-bit integer and returning a double-precision floating-point number.

```c
#include <stdint.h>

static double mul( const double x, const int32_t y ) {
    return x * y;
}

// ...

// Register a Node-API module:
STDLIB_MATH_BASE_NAPI_MODULE_DI_D( mul );
```

The macro expects the following arguments:

-   **fcn**: `double (*fcn)( double, int32_t )` binary function.

When used, this macro should be used **instead of** `NAPI_MODULE`. The macro includes `NAPI_MODULE`, thus ensuring Node-API module registration.

#### STDLIB_MATH_BASE_NAPI_MODULE_FI_F( fcn )

Macro for registering a Node-API module exporting an interface invoking a binary function accepting a single-precision floating-point number and a signed 32-bit integer and returning a single-precision floating-point number.

```c
#include <stdint.h>

static float mulf( const float x, const int32_t y ) {
    return x * y;
}

// ...

// Register a Node-API module:
STDLIB_MATH_BASE_NAPI_MODULE_FI_F( mulf );
```

The macro expects the following arguments:

-   **fcn**: `float (*fcn)( float, int32_t )` binary function.

When used, this macro should be used **instead of** `NAPI_MODULE`. The macro includes `NAPI_MODULE`, thus ensuring Node-API module registration.

#### STDLIB_MATH_BASE_NAPI_MODULE_ZI_Z( fcn )

Macro for registering a Node-API module exporting an interface invoking a binary function accepting a double-precision complex floating-point number and a signed 32-bit and returning a double-precision complex floating-point number.

```c
#include "stdlib/complex/float64.h"
#include "stdlib/complex/reim.h"
#include <stdint.h>

static stdlib_complex128_t mul( const stdlib_complex128_t x, const int32_t y ) {
    double xre;
    double xim;
    double re;
    double im;

    stdlib_reim( x, &xre, &xim );

    re = xre * y;
    im = xim * y;

    return stdlib_complex128( re, im );
}

// ...

// Register a Node-API module:
STDLIB_MATH_BASE_NAPI_MODULE_ZI_Z( mul );
```

The macro expects the following arguments:

-   **fcn**: `stdlib_complex128_t (*fcn)( stdlib_complex128_t, int32_t )` binary function.

When used, this macro should be used **instead of** `NAPI_MODULE`. The macro includes `NAPI_MODULE`, thus ensuring Node-API module registration.

#### STDLIB_MATH_BASE_NAPI_MODULE_CI_C( fcn )

Macro for registering a Node-API module exporting an interface invoking a binary function accepting a single-precision complex floating-point number and a signed 32-bit integer and returning a single-precision complex floating-point number.

```c
#include "stdlib/complex/float32.h"
#include "stdlib/complex/reimf.h"
#include <stdint.h>

static stdlib_complex64_t add( const stdlib_complex64_t x, const int32_t y ) {
    float xre;
    float xim;
    float re;
    float im;

    stdlib_reimf( x, &xre, &xim );

    re = xre * y;
    im = xim * y;

    return stdlib_complex64( re, im );
}

// ...

// Register a Node-API module:
STDLIB_MATH_BASE_NAPI_MODULE_CI_C( add );
```

The macro expects the following arguments:

-   **fcn**: `stdlib_complex64_t (*fcn)( stdlib_complex64_t, int32_t )` binary function.

When used, this macro should be used **instead of** `NAPI_MODULE`. The macro includes `NAPI_MODULE`, thus ensuring Node-API module registration.

#### STDLIB_MATH_BASE_NAPI_MODULE_ZD_Z( fcn )

Macro for registering a Node-API module exporting an interface invoking a binary function accepting a double-precision complex floating-point number and a double-precision floating-point number and returning a double-precision complex floating-point number.

```c
#include "stdlib/complex/float64.h"
#include "stdlib/complex/reim.h"

static stdlib_complex128_t mul( const stdlib_complex128_t x, const double y ) {
    double xre;
    double xim;
    double re;
    double im;

    stdlib_reim( x, &xre, &xim );

    re = xre * y;
    im = xim * y;

    return stdlib_complex128( re, im );
}

// ...

// Register a Node-API module:
STDLIB_MATH_BASE_NAPI_MODULE_ZD_Z( mul );
```

The macro expects the following arguments:

-   **fcn**: `stdlib_complex128_t (*fcn)( stdlib_complex128_t, double )` binary function.

When used, this macro should be used **instead of** `NAPI_MODULE`. The macro includes `NAPI_MODULE`, thus ensuring Node-API module registration.

#### STDLIB_MATH_BASE_NAPI_MODULE_CF_C( fcn )

Macro for registering a Node-API module exporting an interface invoking a binary function accepting a single-precision complex floating-point number and a single-precision floating-point number and returning a single-precision complex floating-point number.

```c
#include "stdlib/complex/float32.h"
#include "stdlib/complex/reimf.h"

static stdlib_complex64_t add( const stdlib_complex64_t x, const float y ) {
    float xre;
    float xim;
    float re;
    float im;

    stdlib_reimf( x, &xre, &xim );

    re = xre * y;
    im = xim * y;

    return stdlib_complex64( re, im );
}

// ...

// Register a Node-API module:
STDLIB_MATH_BASE_NAPI_MODULE_CF_C( add );
```

The macro expects the following arguments:

-   **fcn**: `stdlib_complex64_t (*fcn)( stdlib_complex64_t, float )` binary function.

When used, this macro should be used **instead of** `NAPI_MODULE`. The macro includes `NAPI_MODULE`, thus ensuring Node-API module registration.

</section>

<!-- /.usage -->

<!-- C API usage notes. Make sure to keep an empty line after the `section` element and another before the `/section` close. -->

<section class="notes">

### Notes

-   The C-API functions expect that the callback `info` argument provides access to the following JavaScript arguments:

    -   `x`: input value.
    -   `y`: input value.

</section>

<!-- /.notes -->

<!-- C API usage examples. -->

<section class="examples">

</section>

<!-- /.examples -->

</section>

<!-- /.c -->

<!-- Section to include cited references. If references are included, add a horizontal rule *before* the section. Make sure to keep an empty line after the `section` element and another before the `/section` close. -->

<section class="references">

</section>

<!-- /.references -->

<!-- Section for related `stdlib` packages. Do not manually edit this section, as it is automatically populated. -->

<section class="related">

</section>

<!-- /.related -->

<!-- Section for all links. Make sure to keep an empty line after the `section` element and another before the `/section` close. -->


<section class="main-repo" >

* * *

## Notice

This package is part of [stdlib][stdlib], a standard library for JavaScript and Node.js, with an emphasis on numerical and scientific computing. The library provides a collection of robust, high performance libraries for mathematics, statistics, streams, utilities, and more.

For more information on the project, filing bug reports and feature requests, and guidance on how to develop [stdlib][stdlib], see the main project [repository][stdlib].

#### Community

[![Chat][chat-image]][chat-url]

---

## License

See [LICENSE][stdlib-license].


## Copyright

Copyright &copy; 2016-2024. The Stdlib [Authors][stdlib-authors].

</section>

<!-- /.stdlib -->

<!-- Section for all links. Make sure to keep an empty line after the `section` element and another before the `/section` close. -->

<section class="links">

[npm-image]: http://img.shields.io/npm/v/@stdlib/math-base-napi-binary.svg
[npm-url]: https://npmjs.org/package/@stdlib/math-base-napi-binary

[test-image]: https://github.com/stdlib-js/math-base-napi-binary/actions/workflows/test.yml/badge.svg?branch=v0.2.1
[test-url]: https://github.com/stdlib-js/math-base-napi-binary/actions/workflows/test.yml?query=branch:v0.2.1

[coverage-image]: https://img.shields.io/codecov/c/github/stdlib-js/math-base-napi-binary/main.svg
[coverage-url]: https://codecov.io/github/stdlib-js/math-base-napi-binary?branch=main

<!--

[dependencies-image]: https://img.shields.io/david/stdlib-js/math-base-napi-binary.svg
[dependencies-url]: https://david-dm.org/stdlib-js/math-base-napi-binary/main

-->

[chat-image]: https://img.shields.io/gitter/room/stdlib-js/stdlib.svg
[chat-url]: https://app.gitter.im/#/room/#stdlib-js_stdlib:gitter.im

[stdlib]: https://github.com/stdlib-js/stdlib

[stdlib-authors]: https://github.com/stdlib-js/stdlib/graphs/contributors

[stdlib-license]: https://raw.githubusercontent.com/stdlib-js/math-base-napi-binary/main/LICENSE

</section>

<!-- /.links -->
