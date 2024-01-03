`compiler.hooks` 是Webpack编译器提供的钩子函数集合，它包含了一系列的钩子函数，用于在Webpack构建过程中的不同时机执行自定义逻辑。下面是一些常用的钩子函数及其对应的时机：

1. `beforeRun`: 在Webpack开始编译之前调用，即在执行 `webpack` 命令之前。

2. `run`: 在Webpack开始编译时调用。

3. `watchRun`: 在Webpack开始监听模式下的编译之前调用，即在执行 `webpack --watch` 命令之前。

4. `compile`: 在每次新的编译(compilation)创建时调用。

5. `compilation`: 在每次新的编译(compilation)创建完成后调用。

6. `emit`: 在生成资源到输出目录之前调用。

7. `afterEmit`: 在生成资源到输出目录之后调用。

8. `done`: 在Webpack编译完成后调用，无论成功与否。

9. `failed`: 在Webpack编译失败时调用。

10. `invalid`: 在Webpack监听模式下，当编译无效（文件发生变化）时调用。

11. `watchClose`: 在Webpack监听模式下，当监听被关闭时调用，即执行 `Ctrl + C` 终止监听时。

这些钩子函数提供了在Webpack构建过程中不同阶段执行自定义逻辑的能力。你可以通过使用这些钩子函数，注册相应的回调函数，并在特定的时机执行你的自定义逻辑。例如，你可以在 `beforeRun` 钩子函数中执行一些准备工作，或者在 `done` 钩子函数中输出编译结果等。

请注意，以上列出的钩子函数只是一部分常用的钩子函数，Webpack提供了更多的钩子函数，你可以根据需要查阅Webpack官方文档以获取完整的钩子函数列表和详细说明。