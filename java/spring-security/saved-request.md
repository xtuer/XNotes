```java
Object savedRequestObject = request.getSession().getAttribute("SPRING_SECURITY_SAVED_REQUEST");  

if(savedRequestObject != null) {  
    redirectUrl = ((SavedRequest)savedRequestObject).getRedirectUrl();  
    request.getSession().removeAttribute("SPRING_SECURITY_SAVED_REQUEST");  
}  

或者 

SavedRequest savedRequest = new HttpSessionRequestCache().getRequest(request, response);
```



