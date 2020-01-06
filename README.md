# evan-steps
uniapp步骤组件，支持自定义icon   
测试过微信小程序、app（包括nvue模式）、h5

### 用法
参考[github demo](https://github.com/EvanMaFYH/evan-steps)中的用法

### 注意点

#### 1.水平模式下不要超过三个步骤
#### 2.nvue模式下目前不支持slot完全自定义icon，只支持通过icon参数的uni-icons的图标

### 还存在的问题（坐等大佬出现( ^_^ )）   

#### 1.在nvue模式下description过长step无法自动撑开（理论上高度应该自动撑开，没找到什么原因），因此是通过高度计算直接给height赋值实现，不是很理想


### evan-steps props
| 参数           | 说明            | 类型    | 可选值     | 默认值  |    
| :------------- | :------------------------------ | :------ | :----- | :--- |  
| direction | 步骤方向 | string | vertical/horizontal | vertical |
| active | 当前步骤，从0开始，可以通过status覆盖状态 | number | - | 0 |
| status | 指定当前步骤的状态 | string | wait/process/finish/error | process |
| primaryColor | 主题色 | string | - | #108ee9 |
| errorColor | error状态的颜色 | string | - | #F43347 |

### evan-step props   
| 参数           | 说明            | 类型    | 可选值     | 默认值  |    
| :------------- | :------------------------------ | :------ | :----- | :--- |  
| title | 标题 | string | - | - |
| description | 步骤的详情描述，可选 | string | - | - |
| status | 当前步骤的状态，如果不指定该状态，则会按照steps的active来指定状态 | string | wait/process/finish/error | - |
| icon | 步骤图标，可选，如果有值将覆盖默认的图标 | string | - | - |

### evan-step slot
| name | 说明 |
| :--- | :---------------- |
| icon | evan-step自定义icon，如果是用的其他icon组件，设置size为22，如果是用的图片等，请设置宽高为22，并且将图片的默认display设为block |
