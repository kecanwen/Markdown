使用Axios调用XMLHttpRequest的`onprogress`事件需要在Axios的配置对象中添加一个`onUploadProgress`或`onDownloadProgress`属性来指定相应的事件处理函数。这两个属性分别用于上传进度和下载进度的监听。

下面是一个示例，展示如何通过Axios调用XMLHttpRequest的`onprogress`事件：

```javascript
axios({
  method: 'POST',
  url: '/upload',
  data: formData,
  onUploadProgress: (progressEvent) => {
    const percent = Math.round((progressEvent.loaded * 100) / progressEvent.total);
    console.log(`Upload progress: ${percent}%`);
  },
})
  .then((response) => {
    console.log('Response:', response);
  })
  .catch((error) => {
    console.error('Error:', error);
  });
```

在上述示例中，我们使用Axios发送一个POST请求，并传递一个`formData`对象作为请求数据。同时，我们在配置对象中添加了一个`onUploadProgress`属性，并指定了一个事件处理函数。这个事件处理函数会在上传过程中触发，并提供一个`progressEvent`参数，其中包含了上传进度的相关信息。

在事件处理函数中，我们可以根据`progressEvent`的`loaded`和`total`属性计算上传进度的百分比，并进行相应的处理。在示例中，我们简单地将上传进度打印到控制台。

需要注意的是，Axios还提供了`onDownloadProgress`属性，用于监听下载进度。使用方式与上述示例类似，只需要将事件处理函数添加到`onDownloadProgress`属性中即可。

通过使用Axios的`onUploadProgress`和`onDownloadProgress`属性，你可以方便地获取XMLHttpRequest的`onprogress`事件并处理上传或下载的进度信息。