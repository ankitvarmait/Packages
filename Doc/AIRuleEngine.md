
# AI.RuleEngine

[![NuGet package](https://img.shields.io/nuget/v/AI.RulesEngine.svg)](https://www.nuget.org/packages/AI.RulesEngine/)

Configure simple json based rules configurations.

# Introduction 
* Simple JSON based configuration. 
* Check configurations and rules by
  * User Role.
  * System or Group.
  * Any custom conditions. 
  * With Equal or Contains support.
  
* Schema

	  ``` josn
    
        {
          "RulesConfigurations": [
            {
              "Group": "*",
              "Configurations": [
                {
                  "ConfigurationType": "ColumnHeaders-A",
                  "ConfigurationValues": [
                    {
                      "PropertyName": "Test-ID-A",
                      "PropertyValue": "Test-Value-A",
                      "PropertyRemark": ""
                    }
                  ],
                  "ConfigurationConditions": [
                    {
                      "ConditionOn": "Role",
                      "Values": [
                        "Admin",
                        "Contributor",
                        "Guest"
                      ],
                      "ConditionOperators": "Equal"
                    }
                  ]
                }
              ]
            }
          ]}

	 ```
   
# Getting Started
   
## Install package: 

[![NuGet package](https://img.shields.io/nuget/v/AI.RulesEngine.svg)](https://www.nuget.org/packages/AI.RulesEngine/)
    
## Define configurations:
    
## Create the instance:
   
   
```cs    
    IRuleEngine engine = await RuleEngineFactory.CreateRuleEngineAsync();
```

## Setup Rules:
   
   
```cs    
      await engine.SetupJsonRulesStringAsync(data);
      Or
      await engine.SetupRulesAsync(data);
```

 ## Get all supported configurations for group = 'Group2' from RuleId = 'TestRules',  for Role 'Admin2'
   
   
```cs    
     await engine.GetConfigurationValuesAsync("TestRules", "Group2", ("Role", "Admin2", "*"));
```

 ## Get 'config1' configuration for group = 'Group2' from RuleId = 'TestRules',  for Role 'Admin2'
   
   
```cs    
     await engine.GetConfigurationValuesAsync("TestRules", "Group2", ("Role", "Admin2", "config1"));
```

 ## Get 'config1' configuration from RuleId = 'TestRules',  for Role 'Admin2'
   
   
```cs    
     await engine.GetConfigurationValuesAsync("TestRules", "*", ("Role", "Admin2", "config1"));
```


