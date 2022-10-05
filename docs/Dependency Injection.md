# This chapter will focus on dependency injection mechanism in micronaut and its slight differences when comparing to Spring
### Defining beans

Unlike other frameworks which rely on runtime reflection and proxies, Micronaut uses compile time data to implement dependency injection.
The object called beans are managed by IoC Container. In order to start the application context and get the bean we use:
```
ApplicationContext context = ApplicationContext.run()
MyBean myBean = context.getBean(MyBean.class)
```

```
interface Engine {
    val cylinders : Int
    fun start() : String
}

@Singleton
class V8Engine : Engine {

    override val cylinders = 8
    override fun start(): String {
        return "Starting V8"
    }
}

@Singleton
class Vehicle(private val engine: Engine) {
    fun start(): String {
        return engine.start()
    }
}
```
```
fun main(args: Array<String>) {
	run(*args)
	val context = BeanContext.run();
	val vehicle = context.getBean(Vehicle::class.java)
	println(vehicle.start());
}

```
The BeanContext is a container object for all your bean definitions (it also implements BeanDefinitionRegistry).
### Bean qualifiers
If the given interface has multiple implementations, we need to use quelifier when injecting.
The simplest way to do this is by adding named parameter when injecting the constructor:
```
@Singleton
class Vehicle @Inject constructor(@param:Named("V8") private val engine: Engine) {
    fun start(): String {
        return engine.start()
    }
}

```
