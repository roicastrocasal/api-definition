# Product KERNEL-API

### 1. [Product type schema](#product-type-schema)

- #### 1.1 [Fields description](#fields-description-of-product-schema)
- #### 1.2 [Sample JSON](#example-of-product-type-schema)

### 2. [Product](#product)

- #### 2.1 [Fields description](#fields-description-of-product)
- #### 2.2 [Sample JSON](#example-of-product)

### 3. [Product reference](#product-reference)

- #### 3.1 [Fields description](#fields-description-of-product-reference)
- #### 3.2 [Sample JSON](#example-of-reference)

### 4. [Attributes](#attributes)

- #### 3.1 [KeyLabel attributes](#keylabel-attribute)
- #### 3.2 [Label attributes](#label-attribute)

## Product type schema

The product schema defines:

- The categories that the product may define
- The attributes that the product may define
- The attributes that the variant may define
- The attributes that the reference may define
- The management groups of a product. Define variant attributes that can aggregate certain attributes. That attributes can be inherited by a variant
- The marks. it can define custom marks to denotate the in which point is the product in a certain flow
- The restrictions of the attributes in product, variant and references

### Fields description of product schema

| Field                       | Description                                                                                                                                                                      | Values                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| :-------------------------- | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `id`                        | product schema id                                                                                                                                                                |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| `version`                   | Version to manage concurrence                                                                                                                                                    |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| `name`| Name of schema ||
| `productType`               | product type for which the schema exists. This product type is provided by categories BC                                                                                         | Clothes type, Fabrics type...                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
| `productType.id`| Id of product type ||
| `productType.name`| Name of product type ||
| `categories`                | Set of Categories node types provided by categories BC which we can associate to a certain product that implements this schema                                                   | Section, buyer, family, first commercial attribute, second commercial attribute...                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
| `attributes`                | List of attributes that we can associate to a products roots or to their variants                                                                                                | Model, quality, color...                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
| `attributes`.`id`           | Id of attribute value (only in AttributeTypes with key)                                                                                                                          |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| `attributes`.`name`         | Attributte name (We can´t add more than one attribute with same name in a certain schema)                                                                                        |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| `attribute`.`type`          | Type of attribute                                                                                                                                                                | [**Label**](./sample-jsons/attributes/types/LabelType.json) (Enumerate string selected from a predefined set of values), [**KeyLabel**](./sample-jsons/attributes/types/KeyLabelType.json) (Enumerate string with key-value selected from a predefined set of values), [**EbomResourceReference**](./sample-jsons/attributes/types/ebomReferenceType.json) (references a resource in this case is a ebom resource), **DateUTC**, **String**, **Integer**, **Decimal**, **Boolean**, [**i18nCurrency**](./sample-jsons/attributes/types/i18nCurrencyType.json) (Decimal that represents currency ammount in his i18n representation)... |
| `attribute`.`variant`       | Defines if current attribute is a variant attribute and its restriction                                                                                                          | **NOT_VARIABLE** (Doesn´t define variant). **UNIQUE** (Unique in all its variants), **UNIQUE_GROUP**(Combination of all unique_group must be unique), **NO_RESTRICTION** (Conforms variant without restriction), **OVERWRITE** (The variant can overwrite the default value for product). \*Only **NOT_VARIABLE** AND **NO_RESTRICTION** can be `mandatory: false`.                                                                                                                                                                                                                                                                    |
| `attribute`.`multivaluated` | `Boolean` Defines if current attribute can be multivaluated. Multivaluated fields can´t be `reference: true` and can´t be `variable: UNIQUE` or `variable: UNIQUE_GROUP` neither |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| `attribute`.`mandatory`     | `Boolean` Defines if attribute definition is mandatory                                                                                                                           |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| `managementGroups`|   Define variant attributes that can aggregate certain attributes. That attributes can be inherited by a variant ||    
|`managementGroups.id`| Id of the type of management groups ||
| `managementGroups.name`| It must be a variant attribute key name ||
| `managementGroups.data`| *Arrray* Type of data that we can attach to a management group ||
| `managementGroup.data.id`| Id of the type of the attribute that it can attach ||
| `managementGroup.data.name`|  key name of the type of the attribute | color, size...|  
| `managementGroup.data.type`| type of data of the attributte type |[**Label**](./sample-jsons/attributes/types/LabelType.json) (Enumerate string selected from a predefined set of values), [**KeyLabel**](./sample-jsons/attributes/types/KeyLabelType.json) (Enumerate string with key-value selected from a predefined set of values), [**EbomResourceReference**](./sample-jsons/attributes/types/ebomReferenceType.json) (references a resource in this case is a ebom resource), **DateUTC**, **String**, **Integer**, **Decimal**, **Boolean**, [**i18nCurrency**](./sample-jsons/attributes/types/i18nCurrencyType.json) (Decimal that represents currency ammount in his i18n representation)...|                                                                                                                               |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| `managementGroup.data.multivaluated`| define if the value can be multivaluated  ||
| `managementGroup.data.mandatory`| define if the definition is mandatory at management group level || 
| `marks`| *Array* Custom marks to denotate the in which point is the product in a certain flow ||
| `marks.id`| id to identify the custom mark ||
| `marks.name`| Custom name for the mark ||
| `marks.in`| Define where can appear the mark | PRODUCT, VARIANT, BOTH|
| `marks,values`| List of values that mark can have ||
| `marks.default`| Default value of the mark on product creation ||
| `references.delimiter`| Custom delimiter used to autogenerate the refKeys of product, variants and references
| `references.attributes`             | `Object` that define a set of attributes that can be used to generate product references                                                                                         |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| `references`.`attributes`.`inherited`    | define if the reference tooks the product/variant attribute if it´s defined                                                                                                      | **ALWAYS**(The value of the attribute is inherited from product/variant and can´t be changed), **NEVER**(The attribute value never can be the same that its product/variant), **DEFAULT** (the value of attribute is the same that the product/variant if exists but it can be edited). **ALWAYS** only may exists if is defined in the product or variant                                                                                                                                                                                                                                                                             |
| `references`.`attributes`.`restriction`  | Defines reference attributes restriction                                                                                                                                         | **UNIQUE** (Unique in all product references), **UNIQUE_GROUP**(Combination of all unique_group must be unique in all product references ), **NO_RESTRICTION** ()                                                                                                                                                                                                                                                                                                                                                                                                                                                                      |
| `references`.`attributes`.`visible`      | Define if attribute reference is visible. The visible attributes  need to be mandatories in product. This visible attributes are used to generete the visibles references |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |


### Example of product type schema

```json
{
  "id": "urn:brand:<brand-zara-id>:product-type:<product-type-clothes-id>:product-schema:<product-schema-clothes-id>",
  "version": 1,
  "name": "Clothes Zara Schema",
  "productType": {
    "id": "urn:brand:<brand-zara-id>:product-type:<product-type-clothes-id>",
    "name": "Clothes Zara"
  },
  // No tener en cuenta para ejercicio de grupos
  "categories": [ "buyer-code", "family", "subfamily"],
  "attributes": [
    {
      "id": "urn:zara:ropa:attribute:<model-type-id>",
      "name": "model",
      "type": "Label",
      "variant": "NOT_VARIABLE",
      "multivaluated": false,
      "mandatory": true
    },
    {
      "id": "urn:zara:ropa:attribute:<quality-type-id>",
      "name": "quality",
      "type": "Label",
      "variant": "NOT_VARIABLE",
      "multivaluated": false,
      "mandatory": true
    },
    {
      "id": "urn:zara:ropa:attribute:<base-price-type-id>",
      "name": "basePrice",
      "type": "i18nCurrency",
      "variant": "OVERWRITABLE",
      "multivaluated": false,
      "mandatory": false
    },
    {
      "id": "urn:zara:ropa:attribute:<color-type-id>",
      "name": "color",
      "type": "KeyLabel",
      "variant": "UNIQUE_GROUP",
      "multivaluated": false,
      "mandatory": true
    
    },
    {
      "id": "urn:zara:ropa:attribute:<size-type-id>",
      "name": "size",
      "type": "Label",
      "variant": "UNIQUE_GROUP",
      "multivaluated": false,
      "mandatory": true
    },
    {
      "id": "urn:zara:ropa:attribute:<image-reference-type-id>",
      "name": "image",
      "type": "ImageResourceReference",
      "variant" : "NO_RESTRICTION",
      "multivaluated": false,
      "mandatory": false
    },
    {
      "id": "urn:<measurements-reference-type-id>",
      "name": "measurement",
      "type": "MeasurementsResourceReference",
      "variant" : "NO_RESTRICTION",
      "multivaluated": false,
      "mandatory": false
    }
  ],
  "managementGroups" : [
    {
      "id" : "<management-unit-type-color-id>",
      "name": "color",
      "data" :   [
        {
          "id": "urn:zara:ropa:attribute:<image-reference-type-id>",
          "name": "image",
          "type": "ImageResourceReference",
          "multivaluated": false,
          "mandatory": true
        },
        {
          "id": "urn:zara:ropa:attribute:<price-reference-type-id>",
          "name": "basePrice",
          "type": "PriceResourceReference",
          "multivaluated": false,
          "mandatory": true
        }
      ]
    },
    {
      "id" : "<management-unit-type-size-id>",
      "name": "Size group",
      "field": "size",
      "linkedTypes" :   [
        {
          "id": "urn:<measurements-reference-type-id>",
          "name": "measure",
          "type": "MeasurementsResourceReference",
          "multivaluated": false,
          "mandatory": true
        }
      ]
    }
  ],
  "marks": [
    {
      "id": "urn:brand:<zara-id>:product-state-types:<clothes-mark-type-id>",
      "name": "QualityMark",
      "in": "BOTH",
      "values": ["IN DEVELOPMENT", "QUALITY OK"],
      "default": "DEVELOPMENT"
    },
    {
      "id": "urn:brand:<zara-id>:product-state-types:<clothes-mark-type-id>",
      "name": "LegalMark",
      "in": "BOTH",
      "values": ["PENDING", "NOT OK", "OK"],
      "default": "PENDING"
    }
  ],
  "references": {
    "attributes": [
      {
        "id": "urn:zara:ropa:attribute:<model-type-id>",
        "name": "model",
        "type": "Label",
        "inherited": "DEFAULT",
        "restriction": "UNIQUE_GROUP",
        "visible": true
      },
      {
        "id": "urn:zara:ropa:attribute:<model-type-id>",
        "name": "quality",
        "type": "Label",
        "inherited": "DEFAULT",
        "restriction": "UNIQUE_GROUP",
        "visible": true
      },
      {
        "id": "urn:zara:ropa:attribute:<color-type-id>",
        "name": "color",
        "type": "KeyLabel",
        "inherited": "ALWAYS",
        "restriction": "UNIQUE_GROUP",
        "visible": true
      },
      {
        "id": "urn:zara:ropa:attribute:<size-type-id>",
        "name": "size",
        "type": "Label",
        "inherited": "ALWAYS",
        "restriction": "UNIQUE_GROUP",
        "visible": true
      },
      {
        "id": "urn:zara:ropa:attribute:<ebom-reference-type-id>",
        "name": "ebom",
        "type": "EbomResourceReference",
        "restriction": "NOT_RESTRICTION",
        "visible": false
      }
    ],
    "visibleDelimiter" : "/"
  }
}

```

## Product

The product object has the general information of the product, the list of attributes that define it and its variants and the posible states

### Fields description of product

| Field                         | Description                                                                                                  | Values                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| :---------------------------- | :----------------------------------------------------------------------------------------------------------- | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `id`                          | Product id                                                                                                   |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| `refKey`| `String` readable unique reference for a tenant URN||
| `ref`|  configurable readable reference for root product. No need to be unique in tenant. It can be autogenerated with schema references info||
| `name`| Name of the product ||
| `description`| Description of the product ||
| `version`                     | Version to manage concurrence                                                                                |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| `brandId`                     | Organization that owns the product development                                                   |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| `productTypeId`               | Id of product type (served by Organization BC)                                                               | Clothes, Shoes, Fabrics                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| `productTypeSchema.id`        | Id of schema of product                                                                                      |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| `productTypeSchema.name`      | name of schema of product                                                                                    |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| `categories`                  | Defined category ids according schema declaration                                                            |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| `state`                      | State of product root. *Has it a predefined common state machine for all products?*                                     |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| `state.id`| Id of state ||
| `state.name`| Name of state ||
| `marks`| Custom marks that we can assign to a product. ||
| `marks.name`                 | Name of mark type                                                                                                |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| `marks.mark`                | Current mark                                                                                                |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| `attributes`           | `Array` Defined product root attributes according the schema. All the info that it´s not present may be infered by the product schema                                              |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| `attributes.name`      | Attribute name unique by schema. With the definition of the schema you can resolve the attribute by its name |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| `attributes.valueType` | Value type of current attribute. Gives the format of the value field                                                                           | [**Label**](./sample-jsons/attributes/types/LabelType.json) (Enumerate string selected from a predefined set of values), [**KeyLabel**](./sample-jsons/attributes/types/KeyLabelType.json) (Enumerate string with key-value selected from a predefined set of values), [**EbomResourceReference**](./sample-jsons/attributes/types/ebomReferenceType.json) (references a resource in this case is a ebom resource), **DateUTC**, **String**, **Integer**, **Decimal**, **Boolean**, [**i18nCurrency**](./sample-jsons/attributes/types/i18nCurrencyType.json) (Decimal that represents currency ammount in his i18n representation)... |
| `attributes.value`     | `Object` or `DataType`(String, int...) with the data of a certain valueType                                                                |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| `variants`                    | `Array` List of posible values for the product variant instances                                                                         |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| `variants.name`                 | name of one of variant attributes                                                                                                |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| `variants.valueType`|  Value type of current attribute. Gives the format of the value field     | Label, KeyLabel, Resource...|
| `variants.values`| *Array* List of posible values for this `variant.name` attribute ||
| `variants.values.value` |`Object` or `DataType`(String, int...) with the data of a certain valueType   | |
| `variants.data`         | `Array` List of the attribute values linked to this group of variants they have the same structucture of the rest the attributes: *name-valueType-value*    |   |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |                         |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |

### Example of product

```json
{
    "id" : "<product-id>",
    "refKey": "urn:product-type:<zara-ropa-id>:product:<product-id>",
    "ref" :  "4004/765",
    "version": 1,
    "name": "Denim trouser",
    "description": "Simple cotton denim men trouser",
    "brandId": "urn:brand:<zara-id>",
    "productTypeId": "urn:brand:<zara-id>:product-type:<product-type-ropa-id>",
    "productTypeSchema": {
      "id": "urn:brand:<brand-zara-id>:product-type:<product-type-clothes-id>:product-schema:<product-schema-clothes-id>",
      "name": "Clothes Zara schema"
    },
    "categories": [
      "urn:brand:<zara-id>:section:<section-men-id>:section:<man-section>",
      "urn:brand:<zara-id>:section:<section-men-id>:buyer:<buyer-man-collection-a-id>",
      "urn:brand:<zara-id>:section:<section-men-id>:family:<family-pantalon-id>",
      "urn:brand:<zara-id>:section:<section-men-id>:subfamily:<subfamily-wtrouser-id>"
    ],
    "state" : {
      "id" : "<state-id>",
      "name": "Draft"
    },
    "marks": [
      {
        "name": "QualityMark",
        "mark": "IN DEVELOPMENT"
      },
      {
        "name": "LegalMark",
        "mark": "PENDING"
      }
    ],
    
    "attributes": [
      {
        "name": "model",
        "valueType": "Label",
        "value": "4004"
      },
      {
        "name": "quality",
        "valueType": "Label",
        "value": "765"
      },
      {
        "name": "basePrice",
        "valueType": "i18nCurrency",
        "value": {
          "currency": "€",
          "amount": 10.99,
          "locale": "es-ES"
        }
      }
      
    ],
    "variants" : [
        {
            "name" : "color",
            "valueType" : "LabelKey",
            "values" : [
              {
                "value" : {
                  "key": 701,
                  "label": "Blue"
                },
                "data" : []
              },
              {
                "value" : {
                  "key": 800,
                  "label": "Red"
                },
                "data" : [
                  {
                    "name": "image",
                    "valueType": "ImageResourceReference",
                    "value": "urn:image-color-800"
                  },
                  {
                    "name": "basePrice",
                    "valueType": "I18nCurrency",
                    "value": {
                      "currency": "€",
                      "amount": 19.99,
                      "locale": "es-ES"
                    }
                  } 
                ]
              }
                
            ]
        },
        {
            "name" : "size",
            "values" : [
              {
                "value" : "XL",
                "data" : [
                  {
                    "name": "measurements",
                    "valueType": "measurementResourceReference",
                    "value": "urn:product:measurements:<xl-measurement-id>"
                  }
                ]
              },
              {
                "value" : "L",
                "data" : [
                  {
                    "name": "measurements",
                    "valueType": "measurementResourceReference",
                    "value": "urn:product:measurements:<xl-measurement-id>"
                  }
                ]
              }
            ]
        }
    ]
}
```

## Variants 
Instances of the combination of de variable values of a product

|Field| Description| Values|
|:---| :---| :---|
|`id`| Identifier of a variant ||
| `refkey`| Unique readable reference ||
| `productRefKey`| Reference of the product which is its parent ||
| `rekKey`| Human readable key. It may be autogenerated by the schema references definition||
| `state`                      | State of variant root. *Has it a predefined common state machine for all variants?*                                     |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| `state.id`| Id of state ||
| `state.name`| Name of state ||
| `attribute`| *Array* List of the attributes that define the variant ||
| `attributes.name`      | Attribute name unique by schema. With the definition of the schema you can resolve the attribute by its name |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| `attributes.valueType` | Value type of current attribute. Gives the format of the value field                                                                           | [**Label**](./sample-jsons/attributes/types/LabelType.json) (Enumerate string selected from a predefined set of values), [**KeyLabel**](./sample-jsons/attributes/types/KeyLabelType.json) (Enumerate string with key-value selected from a predefined set of values), [**EbomResourceReference**](./sample-jsons/attributes/types/ebomReferenceType.json) (references a resource in this case is a ebom resource), **DateUTC**, **String**, **Integer**, **Decimal**, **Boolean**, [**i18nCurrency**](./sample-jsons/attributes/types/i18nCurrencyType.json) (Decimal that represents currency ammount in his i18n representation)... |
| `attributes.value`     | `Object` or `DataType`(String, int...) with the data of a certain valueType
| `variants.data`         | `Array` List of the attribute values linked to this variant that overrides what management group defines in product    |   |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |                         |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |

### Example of product

```json
{
    "id" : "<variant-1-id>",
    "refKey": "urn:product-type:<zara-ropa-id>:product:<product-id>:variant:<variant-1-id>",
    "productRefKey" : "urn:product-type:<zara-ropa-id>:product:<product-id>",
    "ref" : "800/XL",
    "state" : {
      "id" : "<state-id-1>",
      "state": "DEVELOPMENT"
    }, 
    "attributes": [
      {
        "name": "color",
        "valueType": "KeyLabel",
        "value": {
          "key": 800,
          "label": "Red"
        },
        "data":[
          {
            "name": "image",
            "valueType": "ImageResourceReference",
            "value": "urn:image-color-800-EXCEPTION"
          },
          {
            //EXCEPTION
            "name": "basePrice",
            "valueType": "I18nCurrency",
            "value": {
              "currency": "€",
              "amount": 29.99,
              "locale": "es-ES"
            }
          }

        ]
      },
      {
        "name": "size",
        "valueType": "Label",
        "value": "XL"
      }
    ],
    "marks": [
      {
        "name": "QualityMark",
        "mark": "IN DEVELOPMENT"
      },
      {
        "name": "LegalMark",
        "mark": "PENDING"
      }
    ]
  }
```
## Product reference

The product reference identifies and categorizes a certain production channel

### Fields description of product reference

| Field                    | Description                                                                                                                                                                                                                                                                         | Values                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| :----------------------- | :---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `id`                     | Identify the reference                                                                                                                                                                                                                                                              |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| `refKey`| Unique readable reference ||
| `ref`| Human readable key. It may be autogenerated by the schema references definition ||  
| `version`                | Version to manage concurrence                                                                                                                                                                                                                                                       |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| `gtin`                   | Global Trade Identification Number                                                                                                                                                                                                                                                  |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| `productTypeId`          | Product type                                                                                                                                                                                                                                                                        |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| `productTypeSchema`      | Product type schema                                                                                                                                                                                                                                                                 |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| `productTypeSchema.id`   | Product type schema id                                                                                                                                                                                                                                                              |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| `productTypeSchema.name` | Product type schema name                                                                                                                                                                                                                                                            |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| `productRef`              | Ref of product which the reference belongs                                                                                                                                                                                                                                           |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| `variantRef`              | Ref of variant which the reference belongs                                                                                                                                                                                                                                           |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| `attributes`             | `Array` list of attributes that define the reference                                                                                                                                                                                                                                | Posible attribute types and resctrictions are defined in product schema                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| `attributes.name`        | name of the attribute                                                                                                                                                                                                                                                               |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| `attribute.valueType`    | Value type of current attribute.                                                                                                                                                                                                                                                    | [**Label**](./sample-jsons/attributes/types/LabelType.json) (Enumerate string selected from a predefined set of values), [**KeyLabel**](./sample-jsons/attributes/types/KeyLabelType.json) (Enumerate string with key-value selected from a predefined set of values), [**EbomResourceReference**](./sample-jsons/attributes/types/ebomReferenceType.json) (references a resource in this case is a ebom resource), **DateUTC**, **String**, **Integer**, **Decimal**, **Boolean**, [**i18nCurrency**](./sample-jsons/attributes/types/i18nCurrencyType.json) (Decimal that represents currency ammount in his i18n representation)... |
| `attribute.value`        | `Object` with the data of a certain valueType                                                                                                                                                                                                                                       |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |

### Example of reference

```json
{
  "id": "<reference-1-id>",
  "refKey": "<urn:brand:<brand-zara-id>:product-type:<clothes-type-id>:reference:<reference-1-id>",
  "ref" : "4004/765/901/L",
  "version": 1,
  "gtin": 134239483209234,
  "productTypeId": "urn:product-type:<zara-ropa-id>",
  "productTypeSchema": {
    "id": "urn:brand:<brand-zara-id>:product-type:<product-type-clothes-id>:product-schema:<product-schema-clothes-id>",
    "name": "Clothes Zara schema"
  },
  "productRef": "urn:product-type:<zara-ropa-id>:product:<product-id>",
  "variantRef": "urn:product-type:<zara-ropa-id>:product:<product-id>:variant:<variant-1-id>",
  "attributes": [
    {
      "name": "model",
      "valueType": "Label",
      "value": "4004"
    },
    {
      "name": "quality",
      "valueType": "Label",
      "value": "765"
    },
    {
      "name": "color",
      "valueType": "ValueLabel",
      "value": {
        "value": 901,
        "label": "Azul"
      }
    },
    {
      "name": "size",
      "valueType": "Label",
      "value": "L"
    },
    {
      "name": "ebom",
      "valueType": "EbomResourceReference",
      "value": {
        "resourceId": "urn:brand:<brand-zara-id>:ebom:<ebom-pantalon-algodon-basico>",
        "name": "EBOM de pantalón de algodon"
      }
    }
  ]
}
```

## Attributes

### KeyLabel attribute

Attributes in which may define a key (Integer, string, decimal, boolean) and a label

#### Fields

| Field              | Description                                                                                 | Values |
| :----------------- | :------------------------------------------------------------------------------------------ | :----- |
| `id`               | domain identification                                                                       |        |
| `name`             | name of the attibute type                                                                   |        |
| `keyName`          | name used to create json key                                                                |        |
| `productTypeIds`   | list of product types that can use current attribute                                        |        |
| `keyDataType`      | Data type of certain attribute                                                              |        |
| `items`            | `Array` Set of values for the current attribute                                             |        |
| `items.id`         | id of a attribute item                                                                      |        |
| `items.categories` | categories for which can use current attribute item                                         |        |
| `items.label`      | label for a certain key of one item                                                         |        |
| `items.key`        | key for a certain attribute item. This key is unique in a certain attribute type (color...) |        |

#### Example of keyLabel attributes

```json
{
  "id": "urn:brand:<zara-id>:label-value-attribute:<color-key-label-attribute>",
  "name": "Color",
  "keyName": "color",
  "productTypeIds": [
    "urn:brand:<zara-id>:product-type:<product-type-clothes-id>",
    "urn:brand:<zara-id>:product-type:<product-type-fabrics-id>"
  ],
  "keyDataType": "Integer",
  "items": [
    {
      "id": "<id-color-900>",
      "categories": ["urn:brand:<zara-id>:section:<section-men-id>"],
      "label": "Black",
      "key": 900
    },
    {
      "id": "<id-color-701>",
      "categories": ["urn:brand:<zara-id>:section:<section-men-id>"],
      "label": "Blue",
      "key": 701
    },
    {
      "id": "<id-color-705>",
      "categories": ["urn:brand:<zara-id>:section:<section-woman-id>"],
      "label": "Blue W",
      "key": 705
    }
  ]
}
```

### Label attribute

Attributes in which may define a enumerated list of strings

#### Fields

| Field              | Description                                                                                             | Values |
| :----------------- | :------------------------------------------------------------------------------------------------------ | :----- |
| `id`               | domain identification                                                                                   |        |
| `name`             | name of the attibute type                                                                               |        |
| `keyName`          | name used to create json key                                                                            |        |
| `productTypeIds`   | list of product types that can use current attribute                                                    |        |
| `items`            | `Array` Set of values for the current attribute                                                         |        |
| `items.id`         | id of a attribute item                                                                                  |        |
| `items.categories` | categories for which can use current attribute item                                                     |        |
| `items.label`      | label for a certain key of one item. This key is unique in a certain attribute type (model, quality...) |        |

#### Example of label attributes

```json
{
  "id": "urn:brand:<zara-id>:label-value-attribute:<model-label-attribute>",
  "name": "model",
  "keyName": "Model",
  "productTypeIds": [
    "urn:brand:<zara-id>:product-type:<product-type-clothes-id>",
    "urn:brand:<zara-id>:product-type:<product-type-fabrics-id>"
  ],
  "items": [
    {
      "id": "<id-model-4004>",
      "categories": ["urn:brand:<zara-id>:section:<section-men-id>"],
      "label": "4004"
    },
    {
      "id": "<id-model-4005>",
      "categories": ["urn:brand:<zara-id>:section:<section-men-id>"],
      "label": "4005"
    },
    {
      "id": "<id-model-3002>",
      "categories": ["urn:brand:<zara-id>:section:<section-men-id>"],
      "label": "3002"
    }
  ]
}
```
