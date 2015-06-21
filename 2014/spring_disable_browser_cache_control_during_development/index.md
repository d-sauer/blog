#Spring disable browser cache control during development

During development of web page/application there is one annoying web browser feature, cache. Cache is useful thing in production, but in development when some resource is frequently changed like javascript, css, templates or some other resource. When we hit refresh some resources are refreshed, and some of them are not, depending on browser internal caching mechanism. Annoying thing is repeatedly clearing cache when we made some changes on resources and sometimes browser load new resources and sometime don’t. Some modern browsers also have option for disabling the cache.


To avoid this frustration in development phase, easiest way to always refresh resources is to set HTTP headers for all resources:
- Cache-Control = no-cache, no-store, must-revalidate
- Pragma = no-cache
- Expires = 0

If your work with Spring framework, easiest way to do this is with Interceptor. Create custom interceptor: ```RequestDevelopmentInterceptor.java```


```prettyprint
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
 
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;
import org.springframework.web.servlet.HandlerInterceptor;
import org.springframework.web.servlet.ModelAndView;
 
public class RequestDevelopmentInterceptor implements HandlerInterceptor {
 
    @Override
    public void postHandle(HttpServletRequest request, HttpServletResponse response, Object handler, ModelAndView modelAndView) throws Exception {
        response.setHeader("Cache-Control", "no-cache, no-store, must-revalidate");
        response.setHeader("Pragma", "no-cache");
        response.setHeader("Expires", "0");
    }
}
```
    
    
And in case of java configuration, we need to register interceptor:
```prettyprint
@Configuration
@ComponentScan("com.davorsauer.controller")
@EnableWebMvc
public class Config extends WebMvcConfigurerAdapter {
 
    @Override
    public void addInterceptors(InterceptorRegistry registry) {
        registry.addInterceptor(new RequestDevelopmentInterceptor());
    }
}
```
