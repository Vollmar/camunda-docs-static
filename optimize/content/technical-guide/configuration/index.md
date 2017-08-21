---

title: "Configuration"
weight: 60

menu:
  main:
    identifier: "configuration"
    parent: "technical-guide"

---

All distributions of Camunda Optimize come with a predefined set of configuration options that can be overwritten by the user, based on current environment requirements. To do that, have a look into the folder named environment. There is one file called environment-config.json with values that override the defaults optimize properties.

In the following, all adjustable properties are listed with their default value and a short explanation of their purpose.

# Available configuration

```json
{
  "auth": {
    "defaultAuthentication": {
      /*
      Default password that is automatically added the first time
      optimize is started.
      */
      "password": "admin",
      /*
      Default user name that is automatically added the first time
      optimize is started.
      */
      "user": "admin",
      /*
      Enables the creation of the default Optimize user. If you're using
      Optimize in production, you should disable this property,
      so you just use the users from the engine.
      */
      "creationEnabled": true
    },
    "token": {
      /*
      Optimize uses token-based authentication to keep track of which users are
      logged in. Define when a token is supposed to expire.
      */
      "lifeMin": 15,
      /*
      Define a secret (password), which is used to hash the token.
      */
      "secret": "obfuscate"
    }
  },
  "container": {
    /*
    A host name or IP address, to identify a specific network interface on
    which to listen.
    */
    "host": "localhost",
    "ports": {
      /*
      A port number that will be used by the embedded jetty server to process
      HTTP connections.
      */
      "http": 8090,
      /*
      A port number that will be used by the embedded jetty server to process
      secure HTTPS connections.
      */
      "https": 8091
    },
    /*
    HTTPS requires an SSL Certificate. When you generate an SSL Certificate,
    you are creating a keystore file and a keystore password for use when the
    browser interface connects
    */
    "keystore": {
      "location": "keystore.jks",
      "password": "optimize"
    }
  },
  "engine": {
    "auth": {
      /*
      With the specified group id, only engine users that are part of the
      group can access optimize.
      */
      "accessGroup": "",
      /*
      Toggles basic authentication on or off. When enabling basic
      authentication, please be aware that you also need to adjust the values
      of the user and password
      */
      "enabled": false,
      /*
      When basic authentication is enabled, this password is used to
      authenticate against the engine.
      */
      "password": "",
      /*
      When basic authentication is enabled, this user is used to authenticate
      against the engine.
      */
      "user": ""
    },
    /*
    The name of the engine that will be used to import data.
    */
    "name": "/engine/default",
    /*
    A base URL that will be used for connections to the Camunda Engine REST API.
    */
    "rest": "http://localhost:8080/engine-rest",
    "connection": {
      /*
      Maximum time without connection to the engine, Optimize should wait until a time out is triggered.
      */
      "timeout": 10000
    },
    /*
    Check if engine should be considered connected. Disable only for testing!
    */
    "enabled": true,
    "groups": {
      /*
      The engine endpoint to verify group memberships of users.
      */
      "resource": "/identity/groups"
    },
    "hai": {
      /*      
      The engine endpoint to the historic activity instance count.
      */
      "count": "/history/activity-instance/count",
      /*
      The engine endpoint to the historic activity instances.
      */
      "resource": "/history/activity-instance"
    },
    "history": {
      "procinst": {
        /*
        The engine endpoint to the historic process instance count.
        */
        "count": "/history/process-instance/count",
        /*
        The engine endpoint to the historic process instances.
        */
        "resource": "/history/process-instance"
      },
      "variable": {
        /*
        The engine endpoint to the historic variable instance count.
        */
        "count": "/history/variable-instance/count",
        /*
        The engine endpoint to the historic variable instances.
        */
        "resource": "/history/variable-instance"
      }
    },
    "import": {
      "activity-instance": {
        "pageSize": {
          /*
          Overwrites the maximum page size for historic activity instance
          fetching.
          */
          "max": 10000,
          /*
          Overwrites the maximum page size for historic activity instance
          fetching.
          */
          "min": 50
        }
      },
      /*
      Number of threads being used to process the import jobs in the import
      job queue
      */
      "executorThreadCount": 2,
      /*
      Adjust the queue size of the import jobs created.
      A too large value might cause memory problems.
      */
      "jobQueueMaxSize": 100,
      /*
      The data is fetched from the engine in pages. Define a default minimum
      and maximum size or, to be precise, a range for the number of entities
      that should be fetched at once for each import type.
      */
      "pageMaxSize": 1000,
      "process-definition": {
        "pageSize": {
          "max": 1000,
          /*
          Overwrites the minimum page size for process definitions fetching.
          */
          "min": 10
        }
      },
      /*
      Restrict the import only for the given process definition ids.
      If empty, all the data is imported.
      The value should be a comma seperated list of process definition ids
      */
      "process-definition-list": "",      
      "process-definition-xml": {
        "pageSize": {
          /*
          Overwrites the maximum page size for process definition xml model
          fetching. Should be a low value, as large models will lead to
          memory or timeout problems.
          */
          "max": 4,
          /*
          Overwrites the minimum page size for process definition xml
          model fetching. Should be a low value, as large models will lead
          to memory or timeout problems.
          */
          "min": 1
        }
      },
      "process-instance": {
        "pageSize": {
          /*
          Overwrites the maximum page size for historic process instance
          fetching.
          */
          "max": 1000
        }
      },
      "variable": {
        "pageSize": {
          /*
          Overwrites the maximum page size for historic variable instance
          fetching.
          */
          "max": 1000
        }
      },
      "writer": {
        /*
        Number of retries when there is a version conflict in Elasticsearch
        during the import.
        */
        "numberOfRetries": 5
      }
    },
    "procdef": {
      /*
      The engine endpoint to the process definition count.
      */
      "count": "/process-definition/count",
      /*
      The engine endpoint to the process definition.
      */
      "resource": "/process-definition",
      /*
      The engine endpoint to the process definition xml.
      */
      "xml": "/xml"
    },
    "read": {
      /*
      Maximum time a request to the engine should last,
      before a timeout triggers.
      */      
      "timeout": 15000
    },
    "user": {
      "validation": {
        /*
        The engine endpoint for the user validation.
        */
        "resource": "/identity/verify"
      }
    }
  },
  "es": {
    "analyzer": {
      /*
      camunda.optimize.es.analyzer.name=case_sensitive
      */
      "name": "case_sensitive",
      /*
      Tokenfilter applied to every token.
      */
      "tokenfilter": "standard",
      /*
      Tokenizer used to process tokens within a query.
      */
      "tokenizer": "whitespace"
    },
    "connection": {
      /*
      Maximum time without connection to Elasticsearch, Optimize should
      wait until a time out triggers.
      */
      "timeout": 10000
    },
    "event": {
      /*
      The name of the event type.
      */
      "type": "event"
    },
    "heatmap": {
      "duration": {
        /*
        The name of the duration target value type.
        */
        "targetValueType": "duration-target-value"
      }
    },
    /*
    A hostname on which the Elasticsearch TCP listener is available.
    */
    "host": "localhost",
    /*
    A port number used by Elasticsearch to accept TCP connections.
    */
    "port": 9300,
    "import": {
      "handler": {
        "backoff": {
          /*
          Interval which is used for the backoff time calculation.
          */
          "interval": 1000,
          /*
          If all jobs are backing off at the moment, this interval is used
          to trigger general backoff
          */
          "value": 6000,
          /*
          Once all pages are consumed, the import scheduler component will
          start scheduling fetching tasks in increasing periods of time,
          controlled by "backoff" counter.
          */
          "max": 5
        },
        "pages": {
          "resetInterval": {
            /*
            Chronological unit used to calculate index reset due date.
            Possible values are:

            Seconds, Minutes, Hours, HalfDays, Days, Weeks, Months

            in case not supported value is provided 'Minutes' will be used
            for interval calculation.
            */
            "unit": "Minutes",
            /*
            Interval the import is started all over again, meaning only missing
            entities are fetched during the import restart. The data already
            imported is kept.
            */
            "value": 30
          }
        }
      },
      /*
      The name of the import index type.
      */
      "indexType": "import-index"
    },
    /*
    An index name used to create all Camunda Optimize types, shards, etc.
    */
    "index": "optimize",
    "licenseType": "license",
    "procdef": {
      /*
      The name of the import index type when a list of process definitions
      to import is defined.
      */
      "indexType": "process-definition-import-index",
      /*
      The name of the process definition type.
      */
      "type": "process-definition",
      /*
      The name of the process definition xml type.
      */
      "xmlType": "process-definition-xml"
    },
    "processInstance": {
      /*
      The name of the process instance (pi) tracking type that is used
      to find pi’s that were already imported.
      */
      "idTrackingType": "process-instance-id-tracking",
      /*
      The name of the process instance type.
      */
      "type": "process-instance"
    },
    "sampler": {
      /*
      Connection sampler interval set to the client
      */
      "interval": 5000
    },
    /*
    Maximum time a request to elasticsearch should last, before a timeout
    triggers.
    */
    "scrollTimeout": 60000,
    "settings": {
      "index": {
        /*
        How often should the data replicated in case of node failure.
        Note, the more replicas you define, the slower Elasticsearch becomes.
        */
        "number_of_replicas": 0,
        /*
        How many shards should be used in the cluster.
        */
        "number_of_shards": 1,
        /*
        How long Elasticsearch waits until the documents are available
        for search. A positive value defines the duration in seconds.
        A value of -1 means that a refresh needs to be done manually.
        */
        "refresh_interval": "2s"
      }
    },
    "users": {
      /*
      The name of the user type.
      */
      "type": "users"
    },
    "variable": {
      /*
      The name of the variable type.
      */
      "type": "variable"
    }
  },
  "plugin": {
    "variableImport": {
      /*
      Look in the given base package list for variable import adaption plugins.
      If empty, the import is not influenced. The value can be single value or
      a comma seperated list of base packages, e.g., org.mycompany.myproject1,
      org.mycompany.myproject2
      */
      "basePackages": ""
    }
  },
  "serialization": {
    /*
    Define a custom date format that should be used
    (should be the same as in the engine)
    */
    "dateFormat": "yyyy-MM-dd'T'HH:mm:ss"
  },
  "variable": {
    /*
    States the maximum number of values that are shown for the user in the
    variable filter selection.
    */
    "maxValueListSize": 15
  }
}
```
