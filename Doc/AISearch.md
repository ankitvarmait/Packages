
# AI.Search

# Introduction 
- This client library provides capabilities to perform search on Azure search service without sdk dependencies.
- Search with simple parameters.
- No hard dependencies.
- No sdk, packages required. 
- Light weight asyn.
- Easy to integrate and configure.

# Getting Started
## Install package: 
[![NuGet package](https://img.shields.io/nuget/v/AI.RuleEngine.svg)](https://www.nuget.org/packages/AI.RuleEngine)

## Define configurations:

```cs
     var config = new AIConfiguration("Azure Search Key.", "Azure Search URL e.g. https://xxxx.xxxx.xxx.xxx</param>");
```

## Create the instance:
- Tip: You can reuse the instance, try singleton registration for the instance.

```cs    
    IAISearch aISearch = AISearch.CreateInstance(config);
```

## Perform search:

```cs    
     var respons = await aISearch.SearchAsync<TResponseType>("Test", /*Optional Filter if any*/ filterBy, /*PageSize*/ 10, /*Skip*/ 0, "YourIndexName");
```
- TResponseType : Is the type of the obejct stored on the azure search index.
- Use FilterByBuilder.Equal() to create an filterBy parameter.
   - E.g. Search all data where City = Redmond.
   ```cs
    var filterBy = FilterByBuilder.Equal("City", "Redmond");
    ```
 - It returns records and total number of records found for the matching criteria.   
  
## Advanced scenarios: 
### Register multiple indexes and use it without name 

```cs 
     var indexId1 = config.AddIndex("YourIndexName1");
     var indexId2 = config.AddIndex("YourIndexName2");
     
     var responseFromIndex1 = await aISearch.SearchAsync<TResponseType>("Test", /*Optional Filter if any*/ filterBy, /*PageSize*/ 10, /*Skip*/ 0, indexId1);
     var responseFromIndex2 = await aISearch.SearchAsync<TResponseType>("Test", /*Optional Filter if any*/ filterBy, /*PageSize*/ 10, /*Skip*/ 0, indexId2);
     
     //OR
     
     var responseFromIndex1 = await aISearch.SearchAsync<TResponseType>("Test", /*Optional Filter if any*/ filterBy, /*PageSize*/ 10, /*Skip*/ 0, "YourIndexName1");
     var responseFromIndex2 = await aISearch.SearchAsync<TResponseType>("Test", /*Optional Filter if any*/ filterBy, /*PageSize*/ 10, /*Skip*/ 0, "YourIndexName2");
```
### Pagination

```cs     
    // Take first 10 records     
     var responseFromIndex1 = await aISearch.SearchAsync<TResponseType>("Test", /*Optional Filter if any*/ filterBy, /*PageSize*/ 10, /*Skip*/ 0, "YourIndexName1");\
     
    // Take next 10 records     
    var responseFromIndex1 = await aISearch.SearchAsync<TResponseType>("Test", /*Optional Filter if any*/ filterBy, /*PageSize*/ 10, /*Skip*/ 10, "YourIndexName1");
```

# Contribute
Always welcome. Feel free to raise a request from GitHub.

![Twitter Follow](https://img.shields.io/twitter/follow/AnkitVarmait.svg?label=Follow%20@AnkitVarmait)

 <a href="https://www.linkedin.com/in/ankitvarma">
    <img src="https://img.shields.io/badge/linkedin-%230077B5.svg?&style=for-the-badge&logo=linkedin&logoColor=white" />
 </a>
