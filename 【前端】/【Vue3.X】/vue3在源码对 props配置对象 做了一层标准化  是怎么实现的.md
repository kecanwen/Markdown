在 Vue 3 中，对于组件的 `props` 配置对象进行了一层标准化处理。这个标准化过程是通过 `normalizePropsOptions` 函数来实现的。

具体来说，在 Vue 3 的源码中，`normalizePropsOptions` 函数位于 `runtime-core/src/componentProps.ts` 文件中。它接收一个 `props` 配置对象作为参数，并返回一个标准化后的结果。

下面是 `normalizePropsOptions` 函数的简化版本：

```typescript
import { camelize } from '@vue/shared';

function normalizePropsOptions(props: Record<string, any>): NormalizedPropsOptions {
  const normalized = {};

  for (const key in props) {
    const prop = props[key];
    const propName = camelize(key);

    normalized[propName] = {
      type: prop.type,
      default: prop.default,
      required: prop.required,
      validator: prop.validator,
    };
  }

  return normalized;
}
```

在上述代码中，我们首先创建了一个空对象 `normalized`，用于存储标准化后的 `props` 配置信息。

然后，使用 `for...in` 循环遍历传入的 `props` 对象，获取每个 `prop` 的配置信息。在循环中，我们使用 `camelize` 函数将属性名转换为驼峰命名风格（例如，将 `my-prop` 转换为 `myProp`）。

接着，将每个 `prop` 的类型、默认值、必需性和验证器等信息存储到 `normalized` 对象中，键名为经过驼峰命名的属性名。

最后，返回标准化后的 `normalized` 对象。

通过这个标准化过程，Vue 3 可以统一处理组件的 `props` 配置对象，并将其转换为内部使用的标准格式。这样可以简化后续对 `props` 的处理逻辑，并提供更好的性能和可扩展性。

需要注意的是，上述代码只是一个简化版本，实际的源码中还包含了更多的细节和错误处理。如果你对 Vue 3 的源码感兴趣，可以查看 Vue.js 的 GitHub 仓库，其中包含了完整的源代码以及相关文档。

希望以上解答能够帮助到你！如果还有其他问题，请随时提问。