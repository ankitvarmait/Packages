# CacheInMemory
[![NuGet package](https://img.shields.io/nuget/v/CacheInMemory.svg)](https://www.nuget.org/packages/CacheInMemory) 
[![Open Source? No!](https://badgen.net/badge/Open%20Source%20%3F/No%21/blue?icon=github)](https://github.com/ankitvarmait/ServerRoleAuth)

# Introduction 
This client library provides capabilities to add data in memory cache.
- Thread safe. 
- Auto Refresh all data when configured.
- Easy to configure each data with different source e.g get some data by making call to database.
- Get timestamp when the data was last updated in the cache.
- Easy to integrate.

# Getting Started
## Install package: 
[![NuGet package](https://img.shields.io/nuget/v/CacheInMemory.svg)](https://www.nuget.org/packages/CacheInMemory) 

## Create a cache key:

```cs
 public class TestKey : RequestKey
    {
        // Not necessary to be unique for each key, it is just an identifier.
        public override string Name { get; set; } = "TestKey1";	
    }
```
## Create a value for the key and configure datasource:

```cs
public class TestValue : ResponseValues
    {
        public override async Task<Func<ResponseValues>> GetDataSourceAsync(CancellationToken cancellationToken)
        {
	   // Get data
            var response = new Dictionary<string, string>() { {"Test", "Value"} } ; 
	   // or even from /external/ databaseApi/ layer to get data.
           var response = await databaseApi.GetData(); 
	   
          
           // return the same response value for your data
           return () => new TestValue(this.helper)
            {
                Data = response
            };
        }
        
        // Holding any data that we want to cache agaist the key: TestKey.
        public Dictionary<string, string> Data { get; set; }
        
        // Also possible to hold multiple value against one key: TestKey
	// Add many as properties that you want to return with the same key
        public string DomainData { get; set;}  
	
	// Other properties etc..
    }    
    
```
## Save Key and Value

```cs
var key1 = new TestKey();
var value1 = new TestValue();

InMemoryCache.AddOrUpdateAsync(key1, value1);
//or
InMemoryCache.AddOrUpdateAsync>("TestKey1", value1);
```
## How to get Value based on the key

```cs
var currentValue = InMemoryCache.GetValue<TestValue>(key1);
//or 
var currentValue = InMemoryCache.GetValue<TestValue>("TestKey1");
```

## How to refresh or update the value for the key
 This calls underline data source configured and saved value for the key.
 
```cs
InMemoryCache.RefreshValueAsync(key1);
//or
InMemoryCache.RefreshValueAsync("TestKey1");
```

## How to refresh/ update all values
 This calls underline data source configured and save value for each key.
 
```cs
var token = new CancellationTokenSource();
token.CancelAfter(5000);
await InMemoryCache.RefreshAllValuesAsync(token.Token);
```
## How to remove key from cache
 
```cs
InMemoryCache.RemoveKeyAsync(key1);
//or
InMemoryCache.RemoveKeyAsync("TestKey1");
```

## How to remove all keys from cache | Or clear compelete cache
 
```cs
InMemoryCache.ClearCacheAsync();
```

### Advanced scenarios: 
## Inject dependency for the underline data source
 
```cs

    public class TestValue : ResponseValues
    {
	private readonly DataBaseHelper helper;
        public TestValue(DataBaseHelper helper)
        {
            this.helper = helper;
        }       
        
	public override async Task<Func<ResponseValues>> GetDataSourceAsync(CancellationToken cancellationToken)
         {
           // databaseApi/ layer to get data.
           var response = await databaseApi.GetData();           
          
           // return the same response value for your data
           return () => new TestValue(this.helper)
            {
                Data = response
            };
        }
        public Dictionary<string, string> Data { get; set; }
        
    }

```
## Set Expiry policy for the cache value

```cs
RequestKey.Policy = Policy.EnableCleanup
RequestKey.ExpiredBy = <timeSpan>
```

# Contribute
Always welcome. Feel free to raise a request from GitHub.

![Twitter Follow](https://img.shields.io/twitter/follow/AnkitVarmait.svg?label=Follow%20@AnkitVarmait)

 <a href="https://www.linkedin.com/in/ankitvarma">
    <img src="https://img.shields.io/badge/linkedin-%230077B5.svg?&style=for-the-badge&logo=linkedin&logoColor=white" />
 </a>
