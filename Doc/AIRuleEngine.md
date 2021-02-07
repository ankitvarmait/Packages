
# AI.RuleEngine

[![NuGet package](https://img.shields.io/nuget/v/AI.RuleEngin.svg)](https://www.nuget.org/packages/AI.RuleEngin/)

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
    [![NuGet package](https://img.shields.io/nuget/v/AI.RuleEngine.svg)](https://www.nuget.org/packages/AI.RuleEngine)
    
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

 
