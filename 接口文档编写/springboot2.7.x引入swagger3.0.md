# springboot2.7.x引入swagger3.0

## 1.添加依赖

```
 <!--swagger文档-->
        <dependency>
            <groupId>io.springfox</groupId>
            <artifactId>springfox-boot-starter</artifactId>
            <version>3.0.0</version>
        </dependency>
```

## 2.添加配置文件（非必须可以直接写在配置文件中）

```
spring:
  application:
    name: 应用名称
  mvc:
    pathmatch:
      matching-strategy: ant_path_matcher
swagger:
  enable: true(是否开启)
  application-name: ${spring.application.name}
  application-version: 版本
  application-description: 描述
  
  
  提示：该配置为设置路径匹配方案，2.7x版本后路径匹配方式发生改变，需要手动设置回下面的版本
   mvc:
    pathmatch:
      matching-strategy: ant_path_matcher
      
```



## 3.添加配置文件swagger.config

```
@Component
@Data
@ConfigurationProperties("swagger") //读取配置文件信息
@EnableOpenApi //开启文档规范
public class SwaggerConfig {

    /**
     * 是否开启swagger，生产环境一般关闭，所以这里定义一个变量
     */
    private Boolean enable;

    /**
     * 项目应用名
     */
    private String applicationName;

    /**
     * 项目版本信息
     */
    private String applicationVersion;

    /**
     * 项目描述信息
     */
    private String applicationDescription;



    @Bean
    public Docket docket() {
        return new Docket(DocumentationType.OAS_30)
                .pathMapping("/")

                // 定义是否开启swagger，false为关闭，可以通过变量控制，线上关闭
                .enable(enable)

                //配置api文档元信息
                .apiInfo(apiInfo())

                // 选择哪些接口作为swagger的doc发布
                .select()
                //TODO 选择你需要的指定生成接口文档方式
                //apis() 控制哪些接口暴露给swagger，
                // RequestHandlerSelectors.any() 所有都暴露
                // RequestHandlerSelectors.basePackage("net.xdclass.*")  指定包位置
                // withMethodAnnotation(ApiOperation.class)标记有这个注解 ApiOperation
                .apis(RequestHandlerSelectors.withMethodAnnotation(ApiOperation.class))

                .paths(PathSelectors.any())

                .build();
    }

    private ApiInfo apiInfo() {
        return new ApiInfoBuilder()
                .title(applicationName)
                .description(applicationDescription)
                //TODO 设置你的联系方式
                .contact(new Contact("名字", "网站", "邮箱"))
                .version(applicationVersion)
                .build();
    }
}
```



## 4.使用

controller类上添加

```
@Api(tags = "描述类的功能")
```



方法上

```
@ApiOperation(value = "描述方法功能")

//自定义错误返回码含义（根据业务需求，看是否添加）
@ApiResponses({
          @ApiResponse(responseCode = "200", description = "保存成功"),
          @ApiResponse(responseCode = "205", description = "保存失败")
})
```

例子：

![image-20221228110934263](https://img-blog.csdnimg.cn/img_convert/242f4bf5bacefb753d4e48cc6ce2159e.png)





参数上

```
@ApiParam(name = "",value = "",example = "")

例子：
 public JsonData login(
          @ApiParam(name = "phone", value = "手机号",example = "13888888888")
          @RequestParam("phone") String phone,

          @ApiParam(name = "pwd", value = "密码",example = "123456")
          @RequestParam("pwd")String pwd){

      return JsonData.buildSuccess();
  }
```

