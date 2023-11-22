**Web Components** 是一组 Web 原生 API 的总称

默认情况下，Vue 会优先尝试将一个非原生的 HTML 标签解析为一个注册的 Vue 组件，如果失败则会将其渲染为自定义元素

这种行为会导致在开发模式下的 Vue 发出`“failed to resolve component”`的警告

