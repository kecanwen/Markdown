**在 Vue 中，`props` 是用于接收父组件传递的数据的**。Vue 2.x 和 Vue 3.x 在处理 `props` 的初始化和变更方面有一些不同之处。

在 Vue 2.x 中，当组件接收到新的 `props` 值时，会触发更新过程。在更新过程中，Vue 会比较新旧 `props` 的值，并执行相应的更新操作。具体流程如下：

1. 初始化阶段：在组件创建时，会将父组件传递的 `props` 值保存到组件实例的 `_props` 属性中。
2. 更新阶段：当父组件传递的 `props` 发生变化时，Vue 会触发组件的更新。在更新过程中，Vue 会比较新旧 `props` 的值，如果发现有变化，就会执行组件的重新渲染。

**在 Vue 3.x 中，引入了 Composition API，`props` 的初始化和变更也有所改变。具体流程如下：**

1. 初始化阶段：在组件创建时，通过调用 `setup()` 函数来设置组件的初始状态。在 `setup()` 函数中，可以使用 `props` 参数来访问和初始化 `props` 值。

   ```javascript
   import { defineComponent, ref } from 'vue';
   
   export default defineComponent({
     props: {
       message: String,
     },
     setup(props) {
       // 初始化 props 值
       const initialMessage = ref(props.message);
   
       // 访问和修改 props 值
       console.log('props.message:', props.message);
       initialMessage.value = 'New Message';
   
       return {
         initialMessage,
       };
     },
   });
   
   ```

   
2. 变更阶段：当父组件传递的 `props` 发生变化时，Vue 3.x 使用响应式系统进行追踪和处理。在 `setup()` 函数中，可以使用 `watch` 或 `watchEffect` API 来监听 `props` 的变化，并执行相应的逻辑。

   ```javascript
   import { defineComponent, ref, watch } from 'vue';
   
   export default defineComponent({
     props: {
       message: String,
     },
     setup(props) {
       const message = ref(props.message);
   
       // 使用 watch 监听 props 变化
       watch(
         () => props.message, // 监听的表达式
         (newValue, oldValue) => {
           console.log('props.message 变化了:', newValue);
           message.value = newValue; // 更新本地响应式数据
         }
       );
   
       return {
         message,
       };
     },
   });
   ```

   

在源码层面，Vue 2.x 和 Vue 3.x 在处理 `props` 的初始化和变更时有一些不同。Vue 2.x 使用了 defineReactive() 函数来将 `props` 转换为响应式数据，而 Vue 3.x 则使用了 Proxy 对象来实现响应式。这些细节在源码中有所差异，但整体的目标是相同的：将 `props` 初始化为响应式数据，并在变更时触发更新。

需要注意的是，以上是对 Vue 2.x 和 Vue 3.x 处理 `props` 的基本流程进行了简要说明。在实际源码中，还涉及到更多的细节和优化，以确保 `props` 的正确初始化和变更处理。

如果你对 Vue 源码感兴趣，可以查看 Vue.js 的 GitHub 仓库，其中包含了完整的源代码以及相关文档。