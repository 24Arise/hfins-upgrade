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
