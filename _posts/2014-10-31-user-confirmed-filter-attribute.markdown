---
layout: post
title:  "ASP.NET User confirmed email filter attribute"
date:   2014-10-31 21:48:45
description: Read how to create an action filter attribute to verify that a user has confirmed his email.
categories:
- blog
comments: true
---

[Action filters][af] is a very powerful mechanism in an ASP.NET MVC application that gives us the capability of injecting functionality in our application in a centralized and structure way. 
In this post I am showing how we can create an action filter attribute in order to decorate our controllers in order to check if the current user has verified his email address 
after registered in our system through new ASP.NET [Identity system][identity]. I am going to create two filters as we want to have this functionality in regular MVC controllers and in Web Api controllers as well.

First lets see the code for the regular MVC controllers. What we have to do is just derive from ActionFilterAttribute class that lives in System.Web.Mvc namespace and override the OnActionExecuting method.
```csharp
[AttributeUsage(AttributeTargets.Class | AttributeTargets.Method, AllowMultiple = true, Inherited = true)]
    public class UserConfirmedFilterAttribute : ActionFilterAttribute
    {
        public override void OnActionExecuting(ActionExecutingContext filterContext)
        {
            var userId = filterContext.HttpContext.User.Identity.GetUserId();
            // User is not logged in so redirect him to log in controller action
            if (string.IsNullOrEmpty(userId))
            {
                filterContext.Result = new RedirectToRouteResult(new RouteValueDictionary(
                            new
                            {
                                controller = "Account",
                                action = "Login",
                                returnUrl = filterContext.HttpContext.Request.RawUrl
                            }));
                return;
            }

            var userManager = filterContext.HttpContext.GetOwinContext().GetUserManager<ApplicationUserManager>();
            if (!userManager.IsEmailConfirmed(userId))
            {
                filterContext.Result =
                    new RedirectToRouteResult(
                        new RouteValueDictionary(new { controller = "ConstrollerNameToRedirect", action = "ActionMethodToRedirect" }));
                return;
            }

            base.OnActionExecuting(filterContext);
        }
    }
```

[af]: https://www.asp.net/mvc/overview/older-versions-1/controllers-and-routing/understanding-action-filters-cs/
[identity]: http://www.asp.net/identity