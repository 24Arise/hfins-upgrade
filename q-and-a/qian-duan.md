# 前端

## _hzerojs_

_`hfins-front`  `@hzerojs/preset-hzero` 升级 `~0.13.261` 报错_

> Unhandled Rejection (ReferenceError): \_\_hzero\_umi is not defined

* `app.tsx`

{% code lineNumbers="true" %}
```tsx
// import CompanyChoose from '@common/layout/CompanyChoose';
// import EmptyRender from '@common/components/EmptyRender';

const EmptyRender = require('@common/components/EmptyRender').default;
const CompanyChoose = require('@common/layout/CompanyChoose').default;
```
{% endcode %}



## _transpile_

编译子模块时出现 _`typescript`_ 的异常

> 可通过设置 _`noUnusedLocals`_ 和 _`noUnusedParameters`_ 不显示&#x20;

{% hint style="info" %}
_`noUnusedLocals：`**Report errors on unused locals.**_

_`noUnusedParameters：`**Report errors on unused parameters.**_
{% endhint %}

{% code overflow="wrap" lineNumbers="true" %}
```yaml
$ umi hzero-transpile hfins-front-common
正在 transpile hfins-front-common 模块...
Successfully compiled 241 files with Babel (11906ms).
正在 typescript 编译 hfins-front-common 模块...
../../node_modules/@hzerojs/plugin-layout/browsers/HzeroLayout/eventEmitter.ts(4,3): error TS6133: 'init' is declared but its value is never read.
../../node_modules/hzero-front/src/utils/utils/file.ts(23,3): error TS6133: 'tenantId' is declared but its value is never read.

Error: Command failed: node "/Users/Arise/Developer/worker/07-research/hfins-front/node_modules/typescript/lib/tsc.js"

    at ChildProcess.exithandler (node:child_process:398:12)
    at ChildProcess.emit (node:events:527:28)
    at maybeClose (node:internal/child_process:1090:16)
    at Socket.<anonymous> (node:internal/child_process:449:11)
    at Socket.emit (node:events:527:28)
    at Pipe.<anonymous> (node:net:709:12) {
  code: 1,
  killed: false,
  signal: null,
  cmd: 'node "/Users/Arise/Developer/worker/07-research/hfins-front/node_modules/typescript/lib/tsc.js"'
}
✨  Done in 26.30s.

```
{% endcode %}

* `tsconfig.json`

{% hint style="info" %}
_hfins-front_  根目录的 _tsconfig.json_ 文件
{% endhint %}

{% code overflow="wrap" lineNumbers="true" %}
```json
"noUnusedParameters": false,
"noUnusedLocals": false,
```
{% endcode %}



