# ant-design-vue-scoffald
ant-design-vue模板相关
## 主题方案
 ### 暗黑主体（theme-mode='datk' | 'light'）
  1、使用直接引入less文件，然后动态将引入的数据放入style标签中
  ![image](https://user-images.githubusercontent.com/68949293/198181919-5f656660-e65f-425d-b91d-adb82d66cf09.png)  
  这个引入的顺序需要注意，后引入的变量会覆盖前面的。不会自定义的会不生效
![image](https://user-images.githubusercontent.com/68949293/198181973-4ec615c2-5cb4-4831-a8fc-dc3da3152e77.png)  
  全局的样式定义(方便后续具体主题色切换颜色值)
  ```less
  /** 
  *variables.less
  **/
  
  @namespace: appeon;
  
  //响应式断点
  @screen-sm: 768px;
  ...
  ```
   ```less
  // variables.less
  :root,
  :root[theme-mode='light'] {
    --primary-color: green;
    --page-bg-color: #ffffff;
    // ... 
  }
  
   :root[theme-mode='dark'] {
    --primary-color: green;
    --page-bg-color: #00000;
    // ... 
  }
  ```
  2、
  ```ts  
  // utils/theme/dark.ts
  import light from './style/theme/index.less' 
  import dark from './style/theme/index.dark.less'
  
  // 暗黑主题切换
  export function updateDarkMode(darkMode： DarkModeEnum) {
    if(darkmode === DarkModeEnum.DARK) setDarkModeStyles(dark)
    else setDarkModeStyles(light)
  }
  
  function setDarkModeStyles(content: stirng) {
    const head = document.head
    document.getElemetnById("theme-mode")?.remove()
    const styleDom = document.createElement("style")
    styleDom.id = "theme-mode"
    styleDome.innerHTML = content
    head.appendChild(styleDom)
  }
  
  ```
 ### 主题颜色(theme-color='green' | 'pink')
