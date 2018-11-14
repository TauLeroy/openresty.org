<!---
    @title         ChangeLog 1.15.6
    @creator       Thibault Charbonnier
    @created       2018-11-14 01:32 GMT
--->

# Version 1.15.6.2 - dd MMMM YYYY

* upgraded the [nginx](nginx.html) core to 1.15.6.
    * see the changes here: http://nginx.org/en/CHANGES
* feature: ./configure: added new options `--without-stream_ssl_module` and `--without-stream`.
* feature: ./configure: support @rpath placeholder in OS X. Thanks Datong Sun for the patch.
* bugfix: [nginx](nginx.html) did not destroy the cycle memory pool before the daemon process exits. Thanks Yuansheng Wang for the patch.
* resty-doc indexes: skipped nginx's njs docs due to the use of special xml tags.
* upgraded [ngx_lua](https://github.com/openresty/lua-nginx-module#readme) to 0.10.14rc3.
    * change: we no longer support the standard Lua 5.1 interpreter (PUC-Rio Lua). It is now strongly recommended to use the OpenResty LuaJIT releases, bundled with the official OpenResty releases.
    * change: we now print an alert when a non openresty-specific version of LuaJIT is detected since many optimizations would be missing. Thanks Thibault Charbonnier for the patch.
    * change: we now print a warning when writing to the Lua global variable `_G`.
    * feature: added support for ARM64 (Aarch64). Thanks Cloudflare for sponsoring this work. Thanks Dejiang Zhu and Zexuan Luo for the development work of this patch.
    * feature: implemented the [tcpsock:receiveany](https://github.com/openresty/lua-nginx-module#tcpsockreceiveany) upstream cosocket API. Thanks spacewander for the patch.
    * feature: implemented a new [lua_sa_restart](https://github.com/openresty/lua-nginx-module#lua_sa_restart) directive, which sets the `SA_RESTART` flag on [nginx](nginx.html) workers signal dispositions. Thanks Thibault Charbonnier for the patch.
    * bugfix: fixed segfault in [NGINX](nginx.html) core >= 1.15.0 when [init_worker_by_lua*](https://github.com/openresty/lua-nginx-module#init_worker_by_lua) is used. Thanks Datong Sun for the patch.
    * bugfix: [ngx.process](https://github.com/openresty/lua-resty-core/blob/master/lib/ngx/process.md#readme): [type()](https://github.com/openresty/lua-resty-core/blob/master/lib/ngx/process.md#type) didn't return 'master' in master process. Thanks spacewander for the patch.
    * bugfix: [tcpsock:setkeepalive](https://github.com/openresty/lua-nginx-module#tcpsocksetkeepalive): worker processes might take too long to gracefully shut down when the keep alive connections take a long max idle time. Thanks Dejiang Zhu for the patch.
    * bugfix: when variable is cacheable and indexed, setting the request "Host" header should clear any existing cached $host variable value so that subsequent reads return the expected result.
    * bugfix: silenced `-Wcast-function-type` warnings, allowing for compilation with gcc8. Thanks Alessandro Ghedini for the patch.
    * bugfix: the `dd` calls in ngx_http_lua_util.h are now guarded by `#ifdef DDEBUG`. Thanks spacewander for the patch.
    * misc: updated `_G` write guard message to be more accurate. Thanks Thibault Charbonnier for the patch.
    * misc: rename a test file to be properly ordered. Thanks Thibault Charbonnier for the patch.
    * doc: updated the docs to reflect the change that we now no longer support the standard Lua 5.1 interpreter in this module. also recommended OpenResty's LuaJIT branch version instead of the stock LuaJIT.
    * doc: mention that [ngx.req](https://github.com/openresty/lua-resty-core/blob/master/lib/ngx/req.md#readme).set_body_data() and [ngx.req](https://github.com/openresty/lua-resty-core/blob/master/lib/ngx/req.md#readme).set_body_file() must read the request body. Thanks Thibault Charbonnier for the patch.
    * doc: fixed the links to [ssl_session_store_by_lua_block](https://github.com/openresty/lua-nginx-module#ssl_session_store_by_lua_block). Thanks chronolow for the patch.
    * typo: fixed a debug log in access and rewrite handlers. Thanks sbhr for the patch.
* upgraded [ngx_stream_lua](https://github.com/openresty/stream-lua-nginx-module#readme) to 0.0.6rc3.
    * change: we now print an alert when a non openresty-specific version of LuaJIT is detected since many optimizations would be missing. Thanks Thibault Charbonnier for the patch.
    * feature: added support for ARM64. Thanks Cloudflare for sponsoring this work. Thanks Dejiang Zhu and Zexuan Luo for the development work of this patch.
    * feature: [ssl_certificate_by_lua*](https://github.com/openresty/lua-nginx-module#ssl_certificate_by_lua_block) support. Thanks Kong Inc. for sponsoring the development of this feature, and thanks James Callahan and Datong Sun for the development work of this patch.
    * feature: shdict: enabled [FFI](http://luajit.org/ext_ffi.html) support. Thanks Datong Sun for the patch.
    * feature: [ngx.semaphore](https://github.com/openresty/lua-resty-core/blob/master/lib/ngx/semaphore.md#readme) support. Thanks Datong Sun for the patch.
    * feature: enabled [ngx.errlog](https://github.com/openresty/lua-resty-core/blob/master/lib/ngx/errlog.md#readme) support. Thanks Thibault Charbonnier for the patch.
    * feature: implemented a new [lua_sa_restart](https://github.com/openresty/lua-nginx-module#lua_sa_restart) directive, which sets the `SA_RESTART` flag on [nginx](nginx.html) workers signal dispositions. Thanks Thibault Charbonnier for the patch.
    * misc: renamed a test file to be aligned with its [ngx_lua](https://github.com/openresty/lua-nginx-module#readme) counterpart. Thanks Thibault Charbonnier for the patch.
    * misc: updated `_G` write guard message to be more accurate. Thanks Thibault Charbonnier for the patch.
    * misc: re-rendered all files to include newly added template header. Thanks Datong Sun for the patch.
    * doc: added missing links for [ssl_certificate_by_lua*](https://github.com/openresty/lua-nginx-module#ssl_certificate_by_lua_block) directives. Thanks chronolaw for the patch.
* upgraded [lua-resty-core](https://github.com/openresty/lua-resty-core#readme) to 0.1.16rc3.
    * change: now we require OpenResty's LuaJIT branch to work properly on ARM64 since we make use of the thread.exdata Lua API.
    * feature: added support for ARM64 (AArch64). Thanks Cloudflare for sponsoring this work. Thanks Dejiang Zhu and Zexuan Luo for the development work of this patch.
    * feature: [ssl_certificate_by_lua*](https://github.com/openresty/lua-nginx-module#ssl_certificate_by_lua_block) support for the stream subsystem. Thanks Kong Inc. for sponsoring the development of this feature, and thanks James Callahan and Datong Sun for the development work of this patch.
    * feature: shdict: enabled the FFI-based API for the stream subsystem. Thanks Datong Sun for the patch.
    * feature: [ngx.semaphore](https://github.com/openresty/lua-resty-core/blob/master/lib/ngx/semaphore.md#readme): enabled the FFI-based API for the stream subsystem. Thanks Datong Sun for the patch.
    * feature: errlog: enabled the FFI-based API for the stream subsystem. Thanks Thibault Charbonnier for the patch.
    * feature: also implemented the ndk.* API with [FFI](http://luajit.org/ext_ffi.html).
    * bugfix: [ngx.process](https://github.com/openresty/lua-resty-core/blob/master/lib/ngx/process.md#readme): [type()](https://github.com/openresty/lua-resty-core/blob/master/lib/ngx/process.md#type) didn't return 'master' in master process. Thanks spacewander for the patch.
    * bugfix: now we only allow a single version of [ngx_lua](https://github.com/openresty/lua-nginx-module#readme) and [ngx_stream_lua](https://github.com/openresty/stream-lua-nginx-module#readme). Thanks spacewander for the patch.
    * optimize: fixed misuses of Lua global variables in our Lua code (caught by the new version of the lj-releng tool).
    * doc: [ngx.process](https://github.com/openresty/lua-resty-core/blob/master/lib/ngx/process.md#readme): fixed a typo in the spelling of 'privileged agent'. Thanks spacewander for the patch.
    * doc: [ngx.process](https://github.com/openresty/lua-resty-core/blob/master/lib/ngx/process.md#readme): updated the process type list. Thanks spacewander for the patch.
    * doc: [ngx.balancer](https://github.com/openresty/lua-resty-core/blob/master/lib/ngx/balancer.md#readme): fixed a typo in the sample code. Thanks chronolaw for the patch.
    * doc: [ngx.ssl](https://github.com/openresty/lua-resty-core/blob/master/lib/ngx/ssl.md#readme): documented the get
    * doc: [ngx.semaphore](https://github.com/openresty/lua-resty-core/blob/master/lib/ngx/semaphore.md#readme): switch status to production ready.
* upgraded LuaJIT to 2.1-20181029: https://github.com/openresty/luajit2/tags
    * feature: implemented the new Lua and C API functions for thread exdata. This API is used internally by the OpenResty and we advise not to use it yourself in the context of OpenResty. Thanks Zexuan Luo for preparing the final version of the patch.
    * feature: luajit.h: defined the macro `OPENRESTY_LUAJIT` for our branch of LuaJIT.
    * imported Mike Pall's latest changes:
        * Actually implement maxirconst trace limit.
        * MIPS/MIPS64: Fix TSETR barrier (again).
        * Fix memory probing allocator to check for valid end address, too.
        * DynASM/x86: Fix vroundps/vroundpd encoding.
        * DynASM: Fix warning.
        * ARM64: Fix exit stub patching.
        * ARM64: Fix write barrier in BC_USETS.
        * Windows: Add UWP support, part 1.
        * From Lua 5.3: assert() accepts any type of error object.
        * x86: Disassemble FMA3 instructions.
        * DynASM/x86: Add FMA3 instructions.
        * PPC/NetBSD: Fix endianess check.
        * x86/x64: Check for jcc when using xor r,r in emit_loadi().
        * [FFI](http://luajit.org/ext_ffi.html): Make FP to U64 conversions match JIT backend behavior.
        * Bump copyright date to 2018.
        * [FFI](http://luajit.org/ext_ffi.html): Add tonumber() specialization for failed conversions.
        * Give expected results for negative non-base-10 numbers in tonumber().
* upgraded [lua-resty-lrucache](https://github.com/openresty/lua-resty-lrucache#readme) to 0.09rc1.
    * optimize: fixed misuses of Lua global variables in our Lua code (caught by the new version of the lj-releng tool).
* upgraded [lua-resty-lock](https://github.com/openresty/lua-resty-lock#readme) to 0.08rc1.
    * bugfix: we now enforce the use of lua-resty-core's [resty.core.shdict](https://github.com/openresty/lua-resty-core/blob/master/lib/resty/core/shdict.md#readme) module to avoid dead locking with the CFunction-based shdict API in [ngx_lua](https://github.com/openresty/lua-nginx-module#readme).
    * doc: made it clearer that we depend on [lua-resty-core](https://github.com/openresty/lua-resty-core#readme).
    * doc: documented the limitations of certain [ngx_lua](https://github.com/openresty/lua-nginx-module#readme) execution contexts which prohibit yielding.
* upgraded [lua-resty-limit-traffic](https://github.com/openresty/lua-resty-limit-traffic#readme) to 0.06rc1.
    * bugfix: set_conn() method did not work at all due to a copy&paste error. Thanks pearzl for the patch.
    * doc: added the [resty.limit.count](https://github.com/openresty/lua-resty-limit-traffic/blob/master/lib/resty/limit/count.md#readme) module to the library's README. Thanks Thibault Charbonnier for the patch.
* upgraded [resty-cli](https://github.com/openresty/resty-cli#readme) to 0.22rc4.
    * feature: implemented new `--stap` and `--stap-opts` command-line options to trace the underlying [nginx](nginx.html) C process directly (without going through the perl wrapper layer.
    * feature: implemented a new `--main-conf` command-line option for specifying nginx's main {} context directives directly from the command line. Thanks Datong Sun for the patch.
    * feature: implemented a new `--gdb-opts` command-line option, which also implies `--gdb`. Also made the `--valgrind-opts=OPTS` option implies `--valgrind`.
    * bugfix: we did not allow leading and trailing spaces in `--gdb-opts` and `--valgrind-opts` options value strings.
    * bugfix: `-I` DIR option failed to include *.ljbc files in the Lua module search paths. Thanks Dejiang Zhu for the report.
* upgraded [lua-cjson](https://github.com/openresty/lua-cjson#readme) to 2.1.0.7rc1.
    * feature: ported to the ARM64 platform by masking off the bits higher than 47-bit in the lightud. Thanks spacewander for the patch.
* upgraded [lua-resty-mysql](https://github.com/openresty/lua-resty-mysql#readme) to 0.21.
    * bugfix: we did not result sets whose field (column) count is more than 250. Thanks libo.huang for the patch.
    * bugfix: we did not strip the trailing null char from C strings when parsing mysql packets. Thanks libo.huang for the patch.
    * doc: fixed the return value spec for the db:connect() method. Thanks chronolaw for the patch.
    * doc: fixed broken links. Thanks Jesse Skinner for the patch.
    * doc: updated docs to reflect recent changes.
* upgraded [lua-resty-websocket](https://github.com/openresty/lua-resty-websocket#readme) to v0.07rc1.
    * doc: fixed the server example to log the right status code. Thanks bumi001 for the patch.
    * doc: fixed a typo. Thanks Edward Betts for the patch.
    * doc: fixed the reading timeout handling in the sample code.
* upgraded [lua-resty-redis](https://github.com/openresty/lua-resty-redis#readme) to 0.27rc1.
    * optimize: fixed misuses of Lua global variables in our Lua code (caught by the new version of the lj-releng tool).
    * bugfix: error message: typo fix: Unkown => Unknown. Thanks vacuum-car for the patch.
* upgraded [ngx_devel_kit](https://github.com/simpl/ngx_devel_kit#readme) to 0.3.1rc1.
* upgraded [ngx_coolkit](https://github.com/FRiCKLE/ngx_coolkit) to 0.2 (no code changes).

See [ChangeLog 1.13.6](changelog-1013006.html) for the changes of [OpenResty](openresty.html) 1.13.6.x.
