# Functions
## To do
- Update functions
- Uploading pictures
- Uploading configs
- Functions - retrieving client print settings
- Functions - orders
- Set default settings
- Set lead time

Add to docs:
- getSupportedLanguages
- getVisualSettings
- updateGeneralInfo
- getCurrencyByCode
- getLanguageByCode
- getCountryByCode

## Notes

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
    "name": "",
    "symbol": "",
    "code": ""
  }
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
### Get countries (managed data)
```
getCountries()
```
#### Response example
Country name is in English
```json
{
  "SB": "Solomon Islands",
  "BR": "Brazil",
  "GR": "Greece","
  ...
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
       }
     }
    }
```
### Remove supported country for shipping
```
removeSupportedCountry(organizationId, code)
```
#### code
Represents country code
```json json_schema
{
  "type": "string",
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
  "type": "string"
}
```
### Remove supported language
```
removeSupportedLanguages(organizationId, code)
```
#### code
Value represents language code.
```json json_schema
{
    "type": "string"
}
```
### Set default language
```
setDefaultLanguage(organizationId, code)
```
#### code
Represents language code
```json json_schema
{
  "type": "string"
}
```
## Print settings
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
Flow: prvo da ide screen sa podesavanjem ovih vrijednosti, nakon cega se kreira proces u bazi. Nakon toga se dodaju qualities, materials, colors i postproductions. 
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
Ovdje se sve salje sa frontenda, jer klijent moze kreirati svoj materijal i svakako ce se slati podaci kao sto su name, description itd. Dakle ako odabere materijal iz managed data, kopirace se i slati u funkciju. Ako kreira svoj, podaci ce se uzeti iz forme i slati u funkciju.
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