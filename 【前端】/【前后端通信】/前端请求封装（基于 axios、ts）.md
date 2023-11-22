## 为什么要对请求进行二次封装

#### 处理统一逻辑，包括：异常捕获、数据上报、状态码处理、请求缓存、csrf 处理、跨域处理、token 生命周期管理等

抽象这一层后，可以做到随意更换请求库（axios、fetch 甚至 xhr），但是对外用法不变

#### 封装思路

1. 提供缓存能力，当传参不变时，可选择缓存结果，用 mem 实现，config.cacheable 控制
2. 异常或错误，统一弹 Notice。提供强制不 Notice 的能力，config.preventNotice 控制
3. 扩展 axios.config 参数，如上述提到的能力，可通过 config 参数实现控制
4. 统一返回 axios 的 response.data，方便日常编码

为适应上述改变，ts 声明也需要相应变化

```tsx
代码
import axios, { AxiosRequestConfig } from 'axios';
import mem from 'mem';

// config 扩展，控制全局弹窗、缓存等开关
export interface RequestConfig extends AxiosRequestConfig {
    preventNotice?: boolean;
    cacheable?: boolean;
}

export const axiosBase = axios.create({
    timeout: 0,
    headers: {
		xsrfCookieName: 'XSRF-TOKEN',
		xsrfHeaderName: 'X-XSRF-TOKEN'
	},
});

axiosBase.interceptors.response.use(
    (response) => {
        // 统一处理返回
        return response.data;
    },
    (error) => {
        // 统一处理异常
        const errorRes = error.response;
        switch (errorRes.code) {
            case 500:
                if (!errorRes.config.preventNotice) {
                    // 统一弹窗
                }
            default:
        }
        return Promise.reject(error);
    }
);

const cachedGet = mem(axiosBase.post, {
    cacheKey: (args) => `${args[0]}${JSON.stringify(args[1])}`,
});
export function get<T = any>(url: string, config?: RequestConfig): Promise<T> {
    if (config?.cacheable) {
        // 缓存请求
        return cachedGet(url, config);
    }
    return axiosBase.get(url, config);
}

const cachedPost = mem(axiosBase.post, {
    cacheKey: (args) =>
        `${args[0]}${JSON.stringify(args[1])}${JSON.stringify(args[2])}`,
});
export function post<T = any>(
    url: string,
    data?: any,
    config?: RequestConfig
): Promise<T> {
    if (config?.cacheable) {
        // 缓存请求
        return cachedPost(url, data, config);
    }
    return axiosBase.post(url, data, config);
}
```


