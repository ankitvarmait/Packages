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
[NuGet package](https://img.shields.io/nuget/v/CacheInMemory.svg)](https://www.nuget.org/packages/CacheInMemory) 

## Create a key:

```cs
 public class TestKey : RequestKey
    {
        public override string Name()
        {
            return "TestKey1";
        }
    }
`

# Contribute
Always welcome. Feel free to raise a request from GitHub.

![Twitter Follow](https://img.shields.io/twitter/follow/AnkitVarmait.svg?label=Follow%20@AnkitVarmait)

 <a href="https://www.linkedin.com/in/ankitvarma">
    <img src="https://img.shields.io/badge/linkedin-%230077B5.svg?&style=for-the-badge&logo=linkedin&logoColor=white" />
 </a>
