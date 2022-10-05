In oder to get some response from the service we need controller. An example controller is shown below:
```
@Controller("/")
class HelloController {
    @Get("/hello/{name}")
    fun hello(name: String) : String {
        return "Hello $name"
    }
}
```
In Micronaut there is no need to add @PathVariable annotation and the default reponse data format is JSON. Parameter produces can be used to change return data format.
```
@Get("/hello/{name}", produces = [MediaType.TEXT_PLAIN])
```
http://localhost:8080/hello/Ramzes will produce Hello Ramzes response
