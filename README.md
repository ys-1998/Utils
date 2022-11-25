# Utils
常用工具类封装-自用

1.时间格式转换 String <==>Date String <=> LocalDateTime

2.自定义JsonData 用于返回json数据给前端。

区分状态码和业务状态码：（对于前端来说都是200的请求，这里的成功失败根据业务状态码来定）成功无操作|成功返回数据|失败返回错误信息|失败返回自定义状态码+错误信息|

3.数据库逆向工程（通过数据库表信息自动创建|实体类model|mapper|service|controller）
 
 流程：1.添加依赖 2.创建测试类MyBatisPlusGenerator（运行生成代码）运行前记得创建目录用于保存文件 3.将代码复制到项目工程中
