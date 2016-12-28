# Spring 使用记录
##HttpMessageConverter usage
when an HTTP request comes in that specifies an Accept header,Spring MVC loops through
the configured HttpMessageConverter until if finds one that can vonvert from the POJO domain model types into the content-type specified in the Accept header,if so configured.

Spring Boot automatically wires up an HttpMessageConverter that can convert generic objects to JSON,absent any more specific converter.

HttpMessageConverters work in both directions:incoming requests bodies are converted to java objects, and java objects are vonverted into HTTP response bodies
    
    
    