### @Service与@Transactional同时使用

@Service（dubbo的@service）与@Transactional同时使用，dubbo无法发布。
原因：

事务控制的底层原理是为服务提供者类创建代理对象，而默认情况下Spring是基于JDK动态代理方式创建代理对象，而此代理对象的完整类名为com.sun.proxy.$Proxy42（最后两位数字不是固定的），我们在配置中进行包扫描不是com.sun.proxy，导致Dubbo在发布服务前进行包匹配时无法完成匹配，进而没有进行服务的发布。
解决方案：

（1）修改applicationContext-service.xml配置文件，开启事务控制注解支持时指定proxy-target-class属性，值为true。其作用是使用cglib代理方式为Service类创建代理对象。cglib创建的代理对象，包名与我们的包名一致。

```java
<!--开启事务控制的注解支持-->
<tx:annotation-driven transaction-manager="transactionManager" proxy-target-class="true"/>
```

（2）在Service注解中加入interfaceClass属性，值为**要指定的的服务接口.class**，作用是指定服务的接口类型。否则会导致发布的服务接口为SpringProxy，而不是需要的接口。

```java
@Service(interfaceClass = TravelGroupService.class)
@Transactional
public class TravelGroupServiceImpl implements TravelGroupService {
    @Autowired
    TravelGroupDao travelGroupDao;
}
```



