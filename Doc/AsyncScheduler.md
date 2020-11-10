
# AsyncScheduler

# Introduction 
- Thread safe. 
- Easy to integrate.
- This client library provides capabilities to configure activities that is Task and run in memory either in asynchronously or synchronously.  
- Create as many as activity (jobs that you want to run). 
- Configure to run all activities or one activity. 
- Container support to easily register dependencies.

# Getting Started
## Install package: 
[![NuGet package](https://img.shields.io/nuget/v/AsyncScheduler.svg)](https://www.nuget.org/packages/AsyncScheduler)

## Create a activity(s):

```cs
    public class Activity1 : IActivity
    {
        public async Task ExecuteAsync(TraceSource ts, CancellationToken cancellationtoken)
        {
            Task task1 = Task.Factory.StartNew(() =>
            {
                int i = 0;
                while (i < 100)
                {
                    ts.TraceInformation($"Activit1 {i}");
                    Thread.Sleep(TimeSpan.FromMilliseconds(500));
                    i++;
                };
            }, cancellationtoken);

            await task1;
        }

        public string Name()
        {
            return nameof(Activity1);
        }
    }
    
    public class Activity2 : IActivity
    {
        public async Task ExecuteAsync(TraceSource ts, CancellationToken cancellationtoken)
        {
            Task task1 = Task.Factory.StartNew(() =>
            {
                int i = 0;
                while (i < 100)
                {
                    ts.TraceInformation($"Activit2 {i}");
                    Thread.Sleep(TimeSpan.FromMilliseconds(1000));

                    if (i == 14)
                    {
                        throw new Exception("Activity2 Failed.");
                    }
                    i++;
                };
            }, cancellationtoken);

            await task1;
        }

        public string Name()
        {
            return nameof(Activity2);
        }
    }
```
## Create configurations for runner:
- ### Run all activities 
```cs
      var option = new Options()
            {
                ActivityToRun = "*", 
                TraceSource = ts
            };
    
```
- ### Run a specific activity 
```cs
      var option = new Options()
            {
                ActivityToRun = "Activity2", 
                TraceSource = ts
            };
    
```
## Register activities 
```cs
            Registration.RegisterActivity(new Activity1());
            Registration.RegisterActivity(new Activity2());
```

## Run it

```cs
 await ActivityRunner.RunAsync(option, default(CancellationToken));
```


# Contribute
Always welcome. Feel free to raise a request from GitHub.

![Twitter Follow](https://img.shields.io/twitter/follow/AnkitVarmait.svg?label=Follow%20@AnkitVarmait)

 <a href="https://www.linkedin.com/in/ankitvarma">
    <img src="https://img.shields.io/badge/linkedin-%230077B5.svg?&style=for-the-badge&logo=linkedin&logoColor=white" />
 </a>
