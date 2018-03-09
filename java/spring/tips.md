## RequestMappingHandlerMapping and RequestMappingHandlerAdapter

Since introduction of **RequestMappingHandlerMapping** and **RequestMappingHandlerAdapter** in Spring 3.1 the distinction is even simpler:

* RequestMappingHandlerMapping **finds** the appropriate handler method for the given request. 
* RequestMappingHandlerAdapter **executes** this method, providing it with all the arguments.



