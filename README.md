# NswagAxiosTypeScriptTemplates
简易的 Nswag 代码模板，用于 Axios 请求代码生成

原版的模板太复杂，删删改改给简化了下，有空再研究研究。

`AxiosClient.liquid` 文件更改变量 `unlessName` 以过滤全局 token 等 headers:  参数。

使用 [NSwagStudio](https://github.com/RicoSuter/NSwag) 打开

效果如下：

```ts
import AxiosRequest from "@/plugins/axios";

export class APP_APIServiceProxy {

    /**
     * app版本的状态
     * @param version 当前的版本号
     * @return OK
     */
    getAppVersionInfoUsingGET(version: string, cancelToken?: CancelToken | undefined): Promise<AxiosResponse<Response_app版本信息模型>> {
        let url_ = "/app/versionInfo?";
        if (version === undefined || version === null)
            throw new Error("参数 'version' 必须定义且不能 null。");
        else
            url_ += "version=" + encodeURIComponent("" + version) + "&";
        url_ = url_.replace(/[?&]$/, "");

        let options_ = <AxiosRequestConfig>{
            method: "GET",
            url: url_,
            headers: {
                "Accept": "*/*"
            },
            cancelToken
        };

        return AxiosRequest(options_)
    }
}

export interface Response_app版本信息模型 {
    errCode: string | null;
    errMsg: string | null;
    resp: App版本信息模型 | null;
    success: boolean | null;
}

export interface App版本信息模型 {
    /** 最低可用的版本号 */
    lowestVersion: string | null;
    /** 最低可用的版本更新日志 */
    lowestVersionLog: string | null;
    /** 最新可选的版本号 */
    newestVersion: string | null;
    /** 最新可选的版本号更新日志 */
    newestVersionLog: string | null;
    /** 商店跳转的地址 */
    url: string | null;
}
```