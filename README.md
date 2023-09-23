# Product KERNEL-API

## Product type schema


| Field                       | Description                                                                                                                                                                      | Values                                                                                                                                                                                                                                                                                                                                                                                          |
| :-------------------------- | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `id`                        | product schema id                                                                                                                                                                |                                                                                                                                                                                                                                                                                                                                                                                                 |
| `productType`               | product type for which the schema exists. This product type is provided by categories BC                                                                                         | Clothes type, Fabrics type...                                                                                                                                                                                                                                                                                                                                                                   |
| `categories`                | Set of Categories node types provided by categories BC which we can associate to a certain product   that implements this schema                                                 | Section, buyer, family, first commercial attribute, second commercial attribute...                                                                                                                                                                                                                                                                                                              |
| `attributes`                | List of attributes that we can associate to a products roots or to their variants                                                                                                | Model, quality, color...                                                                                                                                                                                                                                                                                                                                                                        |
| `attributes`.`id`           | Id of attribute value (only in AttributeTypes with key)                                                                                                                          |                                                                                                                                                                                                                                                                                                                                                                                                 |
| `attributes`.`name`         | Attributte name (We can´t add more than one attribute with same name in a certain schema)                                                                                        |                                                                                                                                                                                                                                                                                                                                                                                                 |
| `attribute`.`type`          | Type of attribute                                                                                                                                                                | **Label** (Enumerate string selected from a predefined set of values), **ValueLabel** (Enumerate string with key-value selected from a predefined set of values), **EbomResourceReference**  (references a resource in this case is a ebom resource), **DateUTC**, **String**, **Integer**, **Decimal**, **Boolean**, **i18nCurrency** (Decimal that represents currency ammount in his i18n representation)... |
| `attribute`.`variant`       | Defines if current attribute is a variant attribute and its restriction                                                                                                          | **NOT_VARIABLE** (Doesn´t define variant). **UNIQUE** (Unique in all its variants), **UNIQUE_GROUP**(Combination of all unique_group must be unique), **NO_RESTRICTION** (Conforms variant without restriction). *Only **NOT_VARIABLE** AND **WITHOUT_RESTRICTION** can be `mandatory: false`.                                                                                                  |
| `attribute`.`multivaluated` | `Boolean` Defines if current attribute can be multivaluated. Multivaluated fields can´t be `reference: true` and can´t be `variable: UNIQUE` or `variable: UNIQUE_GROUP` neither |                                                                                                                                                                                                                                                                                                                                                                                                 |
| `attribute`.`mandatory`     | `Boolean` Defines if attribute definition is mandatory                                                                                                                           |                                                                                                                                                                                                                                                                                                                                                                                                 |
| `states`                    | Object in which can define custom states of product root or variants with it´s allowed flow configuration                                                                        |                                                                                                                                                                                                                                                                                                                                                                                                 |
| `states`.`id`               | Custom state id                                                                                                                                                                  |                                                                                                                                                                                                                                                                                                                                                                                                 |
| `states`.`name`             | Custom state name                                                                                                                                                                |                                                                                                                                                                                                                                                                                                                                                                                                 |
| `state`.`in`                | where state can be present                                                                                                                                                       | PRODUCT_ROOT, VARIANT, BOTH                                                                                                                                                                                                                                                                                                                                                                     |
| `state`.`values`            | Set of values ​​that the state can have                                                                                                                                          |                                                                                                                                                                                                                                                                                                                                                                                                 |
| `state`.`initial`           | Initial value of state                                                                                                                                                           |                                                                                                                                                                                                                                                                                                                                                                                                 |
| `state`.`transitions`       | `Object` that configure the allowed transitions that the state can present                                                                                                       |                                                                                                                                                                                                                                                                                                                                                                                                 |
| `state`.`transitions.id`    | Id of transition                                                                                                                                                                 |                                                                                                                                                                                                                                                                                                                                                                                                 |
| `state`.`transitions.from`  | Custom state where transition starts                                                                                                                                             |                                                                                                                                                                                                                                                                                                                                                                                                 |
| `state`.`transitions.to`    | Custom state where transition ends                                                                                                                                               |                                                                                                                                                                                                                                                                                                                                                                                                 |
| `references`                | `Object` that define a set of attributes that can be used to generate product references                                                                                         |                                                                                                                                                                                                                                                                                                                                                                                                 |
| `references`.`inherited`    | define if the reference tooks the product/variant attribute if it´s defined                                                                                                      | **ALWAYS**(The value of the attribute is inherited from product/variant and can´t be changed), **NEVER**(The attribute value never can be the same that its product/variant), **DEFAULT** (the value of attribute is the same that the product/variant if exists but it can be edited). **ALWAYS** only may exists if is defined in the product or variant                                      |
| `references`.`restriction`| Defines reference attributes restriction| **UNIQUE** (Unique in all product references), **UNIQUE_GROUP**(Combination of all unique_group must be unique in all product references ), **NO_RESTRICTION** ()|
|`references`.`visible`| Define if attribute reference is visible ||

```json
{
    "id" : "urn:brand:<brand-zara-id>:product-type:<product-type-clothes-id>:product-schema:<product-schema-clothes-id>",
    "name" : "Clothes Zara Schema",
    "productType" : {
        "id" : "urn:brand:<brand-zara-id>:product-type:<product-type-clothes-id>",
        "name" : "Clothes Zara"
    },
    "categories" : ["section","buyer","family","subfamily"],
    "attributes" : [
        {
            "id" : "urn:zara:ropa:attribute:<model-type-id>",
            "name" : "model",
            "type" : "Label",
            "variant" : "NOT_VARIABLE",
            "multivaluated" : false,
            "mandatory" : true


        },
        {
            "id" : "urn:zara:ropa:attribute:<model-type-id>",
            "name" : "quality",
            "type" : "Label",
            "variant" : "NOT_VARIABLE",
            "multivaluated" : false,
            "mandatory" : true


        },
        {
            "id" : "urn:zara:ropa:attribute:<color-type-id>",
            "name" : "color",
            "type" : "LabelValue",
            "multivaluated" : false,
            "mandatory" : true


        },
        {
            "id" : "urn:zara:ropa:attribute:<size-type-id>",
            "name" : "size",
            "type" : "Label",
            "variant" : "UNIQUE_GROUP",
            "multivaluated" : false,
            "mandatory" : true


        },
        {
            "id" : "urn:zara:ropa:attribute:<ebom-reference-type-id>",
            "name" : "ebom",
            "type" : "EbomResourceReference",
            "variant" : "UNIQUE_GROUP",
            "multivaluated" : false,
            "mandatory" : true


        },
        {
            "id" : "urn:zara:ropa:attribute:<base-price-type-id>",
            "name" : "basePrice",
            "type" : "Label",
            "variant" : "NOT_VARIABLE",
            "multivaluated" : false,
            "mandatory" : false


        },
        {
            "id" : "urn:zara:ropa:attribute:<size-system-type-id>",
            "name" : "sizeSystem",
            "type" : "Label",
            "variant" : "NOT_VARIABLE",
            "multivaluated" : false,
            "mandatory" : true


        }


    ],
    "states" : [
        {
            "id" : "urn:brand:<zara-id>:product-state-types:<clothes-state-type-id>",
            "name" : "ClothesState",
            "in" : "BOTH",
            "values" : ["DEVELOPMENT","OK"],
            "initial": "DEVELOPMENT",
            "transitions" : [
                {
                    "id" : "<comercial-state-transition-1>",
                    "from" : "DEVELOPMENT",
                    "to" : "OK"
                }
            ]
        },
        {
            "id" : "urn:brand:<zara-id>:product-state-types:<commercial-state-type-id>",
            "name" : "CommercialState",
            "in" : "VARIANT",
            "values" : ["DRAFT","PENDING COMMERCIAL","PENDING DEVELOPMENT","OK"],
            "transitions" : [
                {
                    "id" : "<comercial-state-transition-1>",
                    "from" : "DRAFT",
                    "to" : "PENDING COMMERCIAL"
                },
                {
                    "id" : "<comercial-state-transition-1>",
                    "from" : "DRAFT",
                    "to" : "PENDING DEVELOPMENT"
                },
                {
                    "id" : "<comercial-state-transition-3>",
                    "from" : "PENDING DEVELOPMENT",
                    "to" : "OK"
                },
                {
                    "id" : "<comercial-state-transition-3>",
                    "from" : "PENDING COMMERCIAL",
                    "to" : "OK"
                }
            ]
        }
    ],
    "references" : [
        {
            "id" : "urn:zara:ropa:attribute:<model-type-id>",
            "name" : "model",
            "inherited" : "DEFAULT",
            "restriction": "UNIQUE_GROUP",
            "visible": true
        },
        {
            "id" : "urn:zara:ropa:attribute:<model-type-id>",
            "name" : "quality",
            "inherited" : "DEFAULT",
            "restriction": "UNIQUE_GROUP",
            "visible": true
        },
        {
            "id" : "urn:zara:ropa:attribute:<color-type-id>",
            "name" : "color",
            "inherited" : "ALWAYS",
            "restriction": "UNIQUE_GROUP",
            "visible": true

        },
        {
            "id" : "urn:zara:ropa:attribute:<size-type-id>",
            "name" : "size",
            "inherited" : "ALWAYS",
            "restriction": "UNIQUE_GROUP",
            "visible": true

        },
        {
            "id" : "urn:zara:ropa:attribute:<ebom-reference-type-id>",
            "name" : "ebom",
            "type" : "EbomResourceReference",
            "inherited": "NEVER",
            "restriction": "NONE",
            "visible": false
        }
    ]
}
```

## Product
The product object has the general information of the product, the list of attributes that define it and its variants and the posible states 

|Field|Description|Values|
|:---|:---|:---|
|`id`|Product id||
|`brandId`|Organization if of brand that owns the product development  ||
|`productTypeId` | Id of product type (served by Organization BC)|Clothes, Shoes, Fabrics|
|`productTypeSchema.id`| Id of schema of product||
|`productTypeSchema.name`| name of schema of product||
|`states`| Implmentation of States of product root defined in product schema  ||
|`states.name`| Name of state||
|`states.state`| Current state||
|`categories`| Defined Category ids  according schema declaration||
|`productAttributes`| `Array` Defined product root attributes according the schema.||
|`productAttributes.name`| Attribute name unique by schema. With the definition of the schema you can resolve the attribute by its name ||
|`productAttributes.valueType`| Value type of current attribute. | **Label** (Enumerate string selected from a predefined set of values), **ValueLabel** (Enumerate string with key-value selected from a predefined set of values), **EbomResourceReference**  (references a resource in this case is a ebom resource), **DateUTC**, **String**, **Integer**, **Decimal**, **Boolean**, **i18nCurrency** (Decimal that represents currency ammount in his i18n representation)... |
|`productAttributes.value`| `Object` with the data of a certain valueType ||
|`variants`| `Array` List of product variants ||
|`variants.id`| Variant id ||
|`variants.attributes`| `Array` List of the attributes of a variant (same valueType logic that exists in product root attributes) ||
|`variants.states`| `Array` List of custom states defined in product schema implemented for a variant | | 






```json
{
    "id": "urn:product-type:<zara-ropa-id>:product:<product-id>",
    "name" : "Denim trouser",
    "description" : "Simple cotton denim men trouser",
    "brandId" : "urn:brand:<zara-id>",
    "productTypeId" : "urn:brand:<zara-id>:product-type:<product-type-ropa-id>",
    "productTypeSchema" : {
        "id" : "urn:brand:<brand-zara-id>:product-type:<product-type-clothes-id>:product-schema:<product-schema-clothes-id>",
        "name" : "Zara clo"
    },
    "states" : [{
        "name" : "ClothesState",
        "state" : "DEVELOPMENT"
    }],
    "categories" : [
        "urn:brand:<zara-id>:section:<section-men-id>:buyer:<buyer-man-collection-a-id>",
        "urn:brand:<zara-id>:section:<section-men-id>:family:<family-pantalon-id>",
        "urn:brand:<zara-id>:section:<section-men-id>:subfamily:<subfamily-wtrouser-id>",
        "urn:brand:<zara-id>:section:<section-men-id>:first-commercial-attribute:<first-comercial-attribute-cotton-trouser-id>"
    ],
    "attributes" : [
        {
            "name" : "model",
            "valueType" : "Label",
            "value" : "4004"  
        },
        {
            "name" : "quality",
            "valueType" : "Label",
            "value" :  "765"  
        },
        {
            "name" : "basePrice",
            "valueType" : "i18nCurrency",
            "value" : {
                "currency" : "€",
                "value" : 10.99
            }
        },
        {
            "name" : "denim",
            "valueType" : "Boolean",
            "value" : true
        },
        {
            "name" : "sizeSystem",
            "valueType" : "Label",
            "value" :  "Letters"
            
        }  
        
    ],
    "variants" : [
        {
            "id": "urn:product-type:<zara-ropa-id>:product:<product-id>:variant:<variant-1-id>",
            "attributes" : [
                {
                    "name" : "color",
                    "valueType" : "LabelValue",
                    "value" : {
                        "value" : 906,
                        "label" : "Black"
                    }
                },
                {
                    "name" : "size",
                    "valueType" : "Label",
                    "value" : "L"
                    
                },
                {
                    "name" : "size",
                    "valueType" : "Resource",
                    "value" : {
                        "resourceType" : "ebom",
                        "resourceId" : "urn:brand:<brand-zara-id>:ebom:<ebom-pantalon-algodon-basico>",
                        "name" : "EBOM de pantalón de algodon"
                    }
                    
                }
            ],
            "states":[
                {
                    "name" : "ClothesState",
                    "state" : "DEVELOPMENT"
                },
                {
                    "name" : "CommercialState",
                    "state" : "PENDING_COMMERCIAL"
                }

            ]
        },
        {
            "id": "urn:product-type:<zara-ropa-id>:product:<product-id>:variant:<variant-2-id>",
            "attributes" : [
                {
                    "name" : "color",
                    "valueType" : "LabelValue",
                    "value" : {
                        "value" : 901,
                        "label" : "Blue"
                    }
                },
                {
                    "name" : "size",
                    "valueType" : "Label",
                    "value" : "L"
                    
                },
                {
                    "name" : "ebom",
                    "valueType" : "EbomResourceReference",
                    "value" : {
                        "resourceId" : "urn:brand:<brand-zara-id>:ebom:<ebom-pantalon-algodon-basico>",
                        "name" : "EBOM de pantalón de algodon"
                    }
                    
                }
            ],
            "states":[
                {
                    "name" : "ClothesState",
                    "state" : "DRAFT"
                },
                {
                    "name" : "CommercialState",
                    "state" : "DEVELOPMENT"
                }

            ]
        }
    ]

}
```

## Product reference
The product reference identifies and categorizes a certain production channel

|Field| Description | Values|
|:---|:---| :---|
|`id`| domain identification||
|`gtin`| Global Trade Identification Number||
|`productTypeId`| Product type ||
|`productTypeSchema`| Product type schema ||
|`productTypeSchema.id`| Product type schema id ||
|`productTypeSchema.name`| Product type schema name ||
|`productId`| Id of product which the reference belongs||
|`variantId`| Id of variant which the reference belongs||
|`attributes`| `Array` list of attributes that define the reference| Posible attribute types and resctrictions are defined in product schema|
|`attributes.name`| name of the attribute||
|`attribute.valueType`| Value type of current attribute. | **Label** (Enumerate string selected from a predefined set of values), **ValueLabel** (Enumerate string with key-value selected from a predefined set of values), **EbomResourceReference**  (references a resource in this case is a ebom resource), **DateUTC**, **String**, **Integer**, **Decimal**, **Boolean**, **i18nCurrency** (Decimal that represents currency ammount in his i18n representation)...
|`attribute.value`| `Object` with the data of a certain valueType ||
|`attribute.visible`| Flag to define which attributes belongs to a visual representation of a certain reference.  **Ex:** 4004/765/901/L in the sample case, with the configured restrictions, the only attributes that are of interest to see to identify the reference are model,quality, color and size ||


```json
[
    {
        "id" : "<urn:brand:<brand-zara-id>:product-type:<clothes-type-id>:reference:<reference-1-id>",
        "gtin" : 134239483209234,
        "productTypeId" : "urn:product-type:<zara-ropa-id>",
        "productTypeSchema" : {
            "id" : "urn:brand:<brand-zara-id>:product-type:<product-type-clothes-id>:product-schema:<product-schema-clothes-id>",
            "name" : "Clothes Zara schema"
        },
        "productId" : "urn:product-type:<zara-ropa-id>:product:<product-id>",
        "variantId" : "urn:product-type:<zara-ropa-id>:product:<product-id>:variant:<variant-1-id>",
        "attributes" : [
            {
                "name" : "model",
                "valueType" : "Label",
                "value" : "4004",  
                "visible" : true
            },
            {
                "name" : "quality",
                "valueType" : "Label",
                "value" :  "765",
                "visible" : true  
            },
            {
                "name" : "color",
                "valueType" : "ValueLabel",
                "value" : {
                    "value" : 901,
                    "label" : "Azul"
                }, 
                "visible" : true
            },
            {
                "name" : "size",
                "valueType" : "Label",
                "value" : "L", 
                "visible" : true
                
            },
            {
                "name" : "ebom",
                "valueType" : "EbomResourceReference",
                "value" : {
                    "resourceId" : "urn:brand:<brand-zara-id>:ebom:<ebom-pantalon-algodon-basico>",
                    "name" : "EBOM de pantalón de algodon"
                },
                "visible": false
                
            }
        ]
    },
    {
        "id" : "<urn:brand:<brand-zara-id>:product-type:<clothes-type-id>:reference:<reference-1-id>",
        "gtin" : 134239483209234,
        "productTypeSchema" : {
            "id" : "urn:brand:<brand-zara-id>:product-type:<product-type-clothes-id>:product-schema:<product-schema-clothes-id>",
            "name" : "Clothes Zara schema"
        },
        "productId" : "urn:product-type:<zara-ropa-id>:product:<product-id>",
        "variantId" : "urn:product-type:<zara-ropa-id>:product:<product-id>:variant:<variant-1-id>",
        "attributes" : [
            {
                "name" : "model",
                "valueType" : "Label",
                "value" : "4004" , 
                "visible" : true 
            },
            {
                "name" : "quality",
                "valueType" : "Label",
                "value" :  "765" , 
                "visible" : true 
            },
            {
                "name" : "color",
                "valueType" : "ValueLabel",
                "value" : {
                    "value" : 901,
                    "label" : "Azul"
                }, 
                "visible" : true
            },
            {
                "name" : "size",
                "valueType" : "Label",
                "value" : "L", 
                "visible" : true
                
            },
            {
                "name" : "ebom",
                "valueType" : "EbomResourceReference",
                "value" : {
                    "resourceId" : "urn:brand:<brand-zara-id>:ebom:<ebom-pantalon-algodon-basico>",
                    "name" : "EBOM de pantalón de algodon"
                },
                "visible": false
                
            }
        ]
    }
]
```