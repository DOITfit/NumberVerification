# NumberVerification
让用户给你发一条短信来验证手机号

## API

### 新建验证  
`https://api.xianyu.it/v1/sms_receive/create`  
#### 请求
方式：`GET`  

|  Key   | 描述                                                  |
|  :---  | :---                                                 |
| number | 手机号（全数字，例：+86-13800138000 应填 8613800138000） |
|  type  | 两位大写字母，表示接收用户发送的短信的手机号的归属地（可选：BE:比利时，US:美国）      |

返回值

| Key   | 描述 |
| :---  | :--- |
| code  | 状态（值为 10001 时为新建成功） |
| msg   | 对 code 的描述 |
| text  | 应由用户发送的短信内容 |
| sendto | 应接收用户发送的短信的手机号 |
| token | 用于查询验证状态 |

### 查询验证
`https://api.xianyu.it/v1/sms_receive/verify`  
#### 请求  
方式：`GET`  

|  Key   | 描述                                                  |
|  :---  | :---                                                 |
| number | 手机号（全数字，例：+86-13800138000 应填 8613800138000） |
|  token  | 新建请求时服务器返回的token |

返回值

| Key   | 描述 |
| :---  | :--- |
| code  | 状态（值为 10001 时为成功验证，为 10002 时为正在等待短信，为 10003 时为验证超时） |
| msg   | 对 code 的描述 |

### 查询手机号信息（基础版）
`https://api.xianyu.it/v1/number_info/basic`  
#### 请求  
方式：`GET`  

|  Key   | 描述                                                  |
|  :---  | :---                                                 |
| number | 手机号（全数字，例：+86-13800138000 应填 8613800138000） |

返回值

| Key   | 描述 |
| :---  | :--- |
| code  | 状态（值为 10001 时为成功查询，为 30002 时为号码错误，为 30001/30003 时为服务器错误） |
| msg   | 对 code 的描述 |
| international_format_number | 号码国际格式（例：8613800138000） |
| national_format_number | 号码所在国格式（例：138 0013 8000） |
| country_code | 国家代码（例：CN） |
| country_code_iso3 | 国家代码（ISO3）（例：CHN） |
| country_name | 国家名（例：China (PRC)） |
| country_prefix | 国家号码前缀（例：86） |

## 说明
* 本服务测试中，因咕咕咕导致的服务不可用，作者不承担责任，但大概会尽快修复
* 短信验证时间为 10 分钟，即用户须在 10 分钟内，使用新建验证时填写的手机号，发送指定短信内容到指定号码以完成验证
* token 有效期为 6 小时，即您需要在 6 小时内使用 token 查询验证状态
