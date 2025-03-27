---
title: 'Background Services in .NET Core: What, Why, and How'
tags: []
published: true
date: '2025-03-27'
---
![https://raw.githubusercontent.com/rodrigoffinger/rodrigoffinger.github.io/master/images/background-services-netcore.png](https://raw.githubusercontent.com/rodrigoffinger/rodrigoffinger.github.io/master/images/background-services-netcore.png)

In modern applications, especially web services, it's common to need tasks running in the background—whether it's polling an API, processing a queue, or running scheduled jobs. In .NET Core, this is made easy with **Background Services**.

#### 🧠 What is a Background Service?

A Background Service is a long-running task that runs alongside your main application. In .NET Core, the most common way to implement this is by using the `BackgroundService` base class from `Microsoft.Extensions.Hosting`.

#### 🔧 Why Use It?

Background services are great for:

*   Scheduled or repeated tasks
    
*   Queue processing
    
*   Background monitoring
    
*   Cleanup or maintenance tasks
    

They allow you to keep your app responsive while offloading work to run independently of the request/response cycle.

#### 🛠 How to Implement One

1.  **Create a class that inherits from** `BackgroundService`**:**
    
    ![https://raw.githubusercontent.com/rodrigoffinger/rodrigoffinger.github.io/master/images/background-services-csharp-1.png](https://raw.githubusercontent.com/rodrigoffinger/rodrigoffinger.github.io/master/images/background-services-csharp-1.png)
    
2.  **Register it in your** `Startup.cs` **or Program.cs:**
    
    ![https://raw.githubusercontent.com/rodrigoffinger/rodrigoffinger.github.io/master/images/background-services-csharp-2.png](https://raw.githubusercontent.com/rodrigoffinger/rodrigoffinger.github.io/master/images/background-services-csharp-2.png)
    

#### 🧵 Things to Keep in Mind

*   Always honor the `CancellationToken` to allow graceful shutdown.
    
*   Use `Scoped` services by creating a scope via `IServiceScopeFactory` inside the background service.
    
*   Avoid blocking calls—stick to `async/await` to keep things efficient.
    

#### ✅ Common Use Case Example: Queue Processor

Many apps use a `Channel<T>` or a `ConcurrentQueue<T>` that the background service consumes while the web app enqueues tasks. This keeps the API fast and the processing isolated.

#### 🧩 Conclusion

Background services in .NET Core are powerful tools that help you move work off the main thread and keep your application responsive. They’re easy to set up and incredibly flexible.
