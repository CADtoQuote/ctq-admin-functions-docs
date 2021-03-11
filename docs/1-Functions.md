# Functions
## To do
- Update functions
- Functions - retrieving client print settings
- Functions - orders

### Notes
Implement transactions for supported languages and translations. If new language is added, translations for every setting has to be added.
If new settings are being added at the same time, supported_languages are being read to get all required translations. That function has to be transaction as well.

## Create organization
### Get currencies (managed data)
```
getCurrencies()
```
#### Response example
Each element has following format with three letter code as object name.
```json
{
  "EUR": {
    "name": "string",
    "symbol": "string",
    "code": "string"
  }
}
```
### Get currency by code (managed data)
```
getCurrencyByCode(code)
```
#### Response example
```json
{
    "name": "string",
    "symbol": "string",
    "code": "string"  
}
```
### Get languages (managed data)
```
getLanguages()
```
#### Response example
```json
{
  "pt": { 
    "name": "Portuguese", 
    "native_name": "português" 
  }
}
```
### Get language by code (managed data)
```
getLanguageByCode(code)
```
#### Response example
```json
{
    "name": "Portuguese", 
    "native_name": "português" 
}
```
### Get countries (managed data)
```
getCountries()
```
#### Response example
Country names are in English
```json
{
  "SB": "Solomon Islands",
  "BR": "Brazil",
  "GR": "Greece","
  ...
}
```
### Get country by code (managed data)
```
getCountryByCode(code)
```
#### Response example
Country name in every language that exists in managed data.
```json
{
  "de":"Bosnien und Herzegowina",
  "pt":"Bósnia e Herzegovina",
  "en":"Bosnia & Herzegovina",
  "it":"Bosnia ed Erzegovina",
  "sv":"Bosnien och Hercegovina",
  "es":"Bosnia y Herzegovina",
  "bs":"Bosna i Hercegovina"
}
```
### Create new organization
```
createOrganization(data)
```
#### data
```json json_schema
{
  "type": "object",
  "properties": {
    "company_name": {
      "type": "string"
    },
    "contact": {
      "type": "object",
      "properties": {
        "street_address": {
          "type": "string"
        },
        "phone": {
          "type": "string"
        },
        "mail": {
          "type": "string"
        },
        "country": {
          "type": "string"
        },
        "postal_code": {
          "type": "string"
        },
        "city": {
          "type": "string"
        }
      }
    },
    "currency_code": {
      "type": "string"
    }
  }
}
```
#### Response
```json
{
  "organization_id": "string",
}
```
## General settings
### Get organization's general info
Response depends on data that's been added to organization.
```
getGeneralInfo(organizationId)
```
#### Response
```json json_schema
{
  "type": "object",
  "properties": {
    "company_name": {
      "type": "string"
    },
    "contact": {
      "type": "object",
      "properties": {
        "street_address": {
          "type": "string"
        },
        "phone": {
          "type": "string"
        },
        "mail": {
          "type": "string"
        },
        "country": {
          "type": "string"
        },
        "postal_code": {
          "type": "string"
        },
        "city": {
          "type": "string"
        }
      }
    },
    "currency": {
      "type": "object",
        "properties": {
          "code": {
            "type": "string"
          },
          "name": {
            "type": "string"
          },
          "symbol": {
            "type": "string"
          }
        }
    },
    "visual_settings": {
      "type": "object",
      "properties": {
        "button_color": {
          "type": "string",
        },
        "corner_roundness": {
          "type": "string",
        }
      }
    },
    "default_language": {
      "type": "object",
      "properties": {
        "en": {
          "type": "object",
          "description": "Language code",
          "properties": {
            "name": {
              "type": "string"
            },
            "native_name": {
              "type": "string"
            }
          }
          }
        }
      },
      "vat": {
          "type": "number"
      },
      "min_order_value": {
          "type": "number"
      },
    "supported_languages": {
    "type": "object",
    "properties": {
      "en": {
        "type": "object",
        "properties": {
          "name": {
            "type": "string"
          },
          "native_name": {
            "type": "string"
          }
        },
        "description": "Language code"
    }}
    },
    "orders_count": {
      "type": "object",
      "properties": {
        "new": {
          "type": "number"
        },
        "in_process": {
          "type": "number"
        },
        "pending": {
          "type": "number"
        },
        "total": {
          "type": "number"
        },
        "completed": {
          "type": "number"
        }
      }
    }
  }
}
```
### Update organization's general info
```
updateGeneralInfo(organizationId, data)
```
#### data
```json json_schema
{
  "type": "object",
  "properties": {
    "company_name": {
      "type": "string"
    },
    "contact": {
      "type": "object",
      "properties": {
        "street_address": {
          "type": "string"
        },
        "phone": {
          "type": "string"
        },
        "mail": {
          "type": "string"
        },
        "country": {
          "type": "string"
        },
        "postal_code": {
          "type": "string"
        },
        "city": {
          "type": "string"
        }
      }
    }
  }
}
```
### Set default currency
```
setDefaultCurrency(organizationId, code)
```
#### code
```json json_schema
{
  "type": "string",
  "description": "Currency code"
}
```
### Get visual settings
```
getVisualSettings(organizationId)
```
#### Response
```json json_schema
{
      "type": "object",
      "properties": {
        "button_color": {
          "type": "string",
        },
        "corner_roundness": {
          "type": "string",
        }
      }
    }
```
### Get supported countries for shipping
```
getSupportedCountries(organizationId)
```
#### Response
```json json_schema
{
  "type": "array",
  "items": {
    "type": "object",
     "properties": {
       "code": {
         "type": "string"
       },
       "name": {
         "type": "string"
       },
       "shipping_zone": {
         "type": "string"
       },
       "vat": {
         "type": "number"
       },
       "translations": {
          "type": "object",
          "properties": {
            "es": {
              "type": "object",
              "properties": {
                "name": {
                  "type": "string"
                }
              },
              "description": "Language code"
            }
          }
          }
     }
    }
  }
}
```
### Add supported country for shipping
```
addSupportedCountry(organizationId, data)
```
#### data
```json json_schema
{
    "type": "object",
     "properties": {
       "code": {
         "type": "string"
       },
       "shipping_zone": {
         "type": "string"
       },
       "vat": {
         "type": "number"
       }
     }
    }
```
### Remove supported country for shipping
```
removeSupportedCountry(organizationId, code)
```
#### code
```json json_schema
{
  "type": "string",
  "description": "Country code"
}
```
### Add shipping option
```
addShippingOption(organizationId, data)
```
#### data
```json json_schema
{
        "type": "object",
        "properties": {
          "name": {
            "type": "string"
          },
          "description": {
            "type": "string"
          },
          "units": {
            "type": "string",
            "example": "Business Days"
          },
          "min": {
            "type": "number"
          },
          "max": {
            "type": "number"
          },
          "price": {
            "type": "number"
          },
          "shipping_zone": {
            "type": "string"
          },
          "translations": {
            "type": "object",
            "properties": {
              "es": {
                "type": "object",
                "properties": {
                  "name": {
                    "type": "string"
                  },
                  "description": {
                    "type": "string"
                  },
                  "units": {
                    "type": "string"
                  }
                },
                "description": "Language code"
              }
            }
            }
            }
}
```
### Get shipping options
```
getShippingOptions(organizationId)
```
#### Response
```json json_schema
{
      "type": "array",
      "items": {
        "type": "object",
        "properties": {
          "id": {
            "type": "string"
          },
          "name": {
            "type": "string"
          },
          "description": {
            "type": "string"
          },
          "units": {
            "type": "string",
            "example": "Business Days"
          },
          "min": {
            "type": "number"
          },
          "max": {
            "type": "number"
          },
          "price": {
            "type": "number"
          },
          "shipping_zone": {
            "type": "string"
          },
          "translations": {
            "type": "object",
            "properties": {
              "es": {
                "type": "object",
                "properties": {
                  "name": {
                    "type": "string"
                  },
                  "description": {
                    "type": "string"
                  },
                  "units": {
                    "type": "string"
                  }
                },
                "description": "Language code"
              }
            }
          }
        }
      }
}
```
### Set min order value
```
setMinOrderValue(organizationId, value)
```
#### value
```json json_schema
{
  "type": "number",
}
```
### Set home vat value
```
setVat(organizationId, value)
```
#### value
```json json_schema
{
  "type": "number",
}
```
### Set visual settings
```
setVisualSettings(organizationId, data)
```
#### data
```json json_schema
{
      "type": "object",
      "properties": {
        "button_color": {
          "type": "string",
        },
        "corner_roundness": {
          "type": "string",
        }
      }
    }
```
### Add supported language
```
addSupportedLanguage(organizationId, code)
```
#### code
```json json_schema
{
  "type": "string",
  "description": "Language code"
}
```
### Get supported languages
```
getSupportedLanguages(organizationId)
```
#### Response example
```json
{
  "en": {
    "name": "English",
    "native_name": "English"
  },
  "de": {
    "name": "German",
    "native_name": "Deutsch"
  }
}
```
### Remove supported language
```
removeSupportedLanguages(organizationId, code)
```
#### code
```json json_schema
{
    "type": "string",
    "description": "Language code"
}
```
### Set default language
```
setDefaultLanguage(organizationId, code)
```
#### code
```json json_schema
{
  "type": "string",
  "description": "Language code"
}
```
## Print settings
### Upload picture
```
uploadPicture(organizationId, file)
```
#### Response
```json json_schema
{
  "type": "string",
  "description": "Picture URL"
}
```

### Get processes (managed data)
```
getProcesses()
```
#### Response
```json json_schema
{
  "type": "array",
  "items": {
    "type": "object",
    "properties": {
      "id": {
        "type": "string"
      },
      "name": {
        "type": "string"
      },
      "description": {
        "type": "string"
      },
      "type": {
        "type": "string"
      },
      "pic_url": {
        "type": "string"
      },
      "translations": {
        "type": "object",
        "properties": {
          "es": {
            "type": "object",
            "properties": {
              "name": {
                "type": "string"
              },
              "description": {
                "type": "string"
              }
            },
            "description": "Language code"
          }
        }
        }
    }
  }
}
```
### Add process
```
addProcess(organizationId, data)
``` 
#### data
```json json_schema
{
  "type": "object",
  "properties": {
    "name": {
      "type": "string"
    },
    "description": {
      "type": "string"
    },
    "pic_url": {
      "type": "string"
    },
    "type": {
      "type": "string"
    },
    "starting_cost": {
      "type": "number"
    },
    "cost_per_hour": {
      "type": "number"
    },
    "slicer": {
      "type": "string"
    },
          "translations": {
        "type": "object",
        "properties": {
          "es": {
            "type": "object",
            "properties": {
              "name": {
                "type": "string"
              },
              "description": {
                "type": "string"
              }
            },
            "description": "Language code"
          }
        }
        }
  }
}
```
### Get materials (managed data)
```
getMaterials()
```
#### Response
```json json_schema
{
  "type": "array",
  "items": {
    "type": "object",
    "properties": {
      "id": {
        "type": "string"
      },
      "name": {
        "type": "string"
      },
      "description": {
        "type": "string"
      },
      "process_type": {
        "type": "string"
      },
      "pic_url": {
        "type": "string"
      },
      "translations": {
        "type": "object",
        "properties": {
          "es": {
            "type": "object",
            "properties": {
              "name": {
                "type": "string"
              },
              "description": {
                "type": "string"
              }
            },
            "description": "Language code"
          }
        }
        }
    }
  }
}
```
### Get colors (managed data)
```
getColors()
```
#### Response
```json json_schema
{
  "type": "array",
  "items": {
    "type": "object",
    "properties": {
      "id": {
        "type": "string"
      },
      "name": {
        "type": "string"
      },
      "hex_value": {
        "type": "string"
      },
      "translations": {
        "type": "object",
        "properties": {
          "es": {
            "type": "object",
            "properties": {
              "name": {
                "type": "string"
              }
            },
            "description": "Language code"
          }
        }
        }
    }
  }
}
```
### Add material
```
addMaterial(organizationId, processId, data)
```
#### data
```json json_schema
{
  "type": "object",
  "properties": {
    "name": {
      "type": "string"
    },
    "description": {
      "type": "string"
    },
    "pic_url": {
      "type": "string"
    },
    "process_type": {
      "type": "string"
    },
    "status": {
      "type": "string"
    },
    "cost_per_kg": {
      "type": "number"
    },
    "translations": {
      "type": "object",
        "properties": {
          "es": {
            "type": "object",
            "properties": {
              "name": {
                "type": "string"
              },
              "description": {
                "type": "string"
              }
            },
            "description": "Language code"
          }
        }
      }
  }
}
```
### Get qualities (managed data)
```
getQualities()
```
#### Response
```json json_schema
{
  "type": "array",
  "items": {
    "type": "object",
    "properties": {
      "id": {
        "type": "string"
      },
      "name": {
        "type": "string"
      },
      "description": {
        "type": "string"
      },
      "translations": {
        "type": "object",
        "properties": {
          "es": {
            "type": "object",
            "properties": {
              "name": {
                "type": "string"
              },
              "description": {
                "type": "string"
              }
            },
            "description": "Language code"
          }
        }
        }
    }
  }
}
```
### Add color
```
addColor(organizationId, processId, materialId, data)
```
#### data
```json json_schema
{
  "type": "object",
  "properties": {
    "name": {
      "type": "string"
    },
    "hex_value": {
      "type": "string"
    },
      "translations": {
        "type": "object",
        "properties": {
          "es": {
            "type": "object",
            "properties": {
              "name": {
                "type": "string"
              }
            },
            "description": "Language code"
          }
        }
        }
  }
}
```
### Upload config 
```
uploadConfig(organizationId, file)
```
#### Response
```json json_schema
{
  "type": "string",
  "description": "Storage location",
  "example": "gs://example.appspot.com/path/config.ini"
}
```
### Add quality
```
addQuality(organizationId, processId, data)
```
#### data
```json json_schema
{
  "type": "object",
  "properties": {
    "name": {
      "type": "string"
    },
    "description": {
      "type": "string"
    },
    "config_url": {
      "type": "string"
    },
      "translations": {
        "type": "object",
        "properties": {
          "es": {
            "type": "object",
            "properties": {
              "name": {
                "type": "string"
              },
              "description": {
                "type": "string"
              }
            },
            "description": "Language code"
          }
        }
        }
  }
}
```
### Get postproductions (managed data)
```
getPostproductions()
```
#### Response
```json json_schema
{
  "type": "array",
  "items": {
    "type": "object",
    "properties": {
      "id": {
        "type": "string"
      },
      "name": {
        "type": "string"
      },
      "description": {
        "type": "string"
      },
      "pic_url": {
        "type": "string"
      },
      "process_type": {
        "type": "string"
      },
      "translations": {
        "type": "object",
        "properties": {
          "es": {
            "type": "object",
            "properties": {
              "name": {
                "type": "string"
              },
              "description": {
                "type": "string"
              }
            },
            "description": "Language code"
          }
        }
        }
    }
  }
}
```
### Add postproduction
```
addPostproduction(organizationId, processId, data)
```
#### data
```json json_schema
{
  "type": "object",
  "properties": {
    "name": {
      "type": "string"
    },
    "description": {
      "type": "string"
    },
    "pic_url": {
      "type": "string"
    },
    "process_type": {
      "type": "string"
    },
    "cost": {
      "type": "number"
    },
    "translations": {
        "type": "object",
        "properties": {
          "es": {
            "type": "object",
            "properties": {
              "name": {
                "type": "string"
              },
              "description": {
                "type": "string"
              }
            },
            "description": "Language code"
          }
        }
        }
  }
}
```