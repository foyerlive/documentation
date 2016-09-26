#FoyerLive - JSON Product Feed

##Product Object properties
  
| Field | Type | Overview |
| ----- | ---- | -------- |
| sku | String | A unique identifier for the product. |
| upc *(optional)*| String | The barcode, UPC or ISBN number for the product. |
| inventory *(optional)*| Number | The number of products available for ordering. |
| url | String | A URL to purchase the product. |
| name | String | The product name. |
| description | String | The product description. Can contain basic HTML. |
| price | Double | The default product price. |
| salePrice | Double | The product sale price, leave empty to use the default price. |
| media | Array | References to one or more [Media Assets](#media-object-properties). |
| attributes | Array | References to one or more [Product Attributes](#attribute-object-properties). |
| categories | Array | References to one or more [Product Categories](#category-object-properties). |
| similarProducts | Array | References to similar product SKUs. |
| relatedProducts | Array | References to related product SKUs. |
| options *(optional)*| Array | List of attribute keys that are available to configure a product down to one unique [Product Variation](#product-variation-object-properties) |
| variations *(optional)*| Array | List of [Product Variations](#product-variation-object-properties), based on attributes like size or color. |

### Simple Product example
```
{
  sku: "619360-067",
  url: "http://store.nike.com/au/en_gb/pd/jordan-jumpman-fitted-hat/pid-10997158/pgid-11100969",
  name: "JORDAN JUMPMAN",
  description: "<h2>BOLD CONTRAST, LASTING COMFORT</h2><p>The Jordan Jumpman Adjustable Hat features vivid colour-blocking and a world-famous symbol on wool fabric for iconic style and a durable, comfortable fit.</p>",
  price: 40.00,
  media: [
    {
      url: "http://images.nike.com/is/image/DotCom/PDP_HERO_S/Jordan-Jumpman-Adjustable-Hat-619360_067_A.jpg",
    }
  ],
  attributes: {
    // Example of basic attributes...
    type: "Hat",
    color: "Cool Grey/White",
    colorFamily: "Grey",
    care: "Do not wash",
    weight: 100,
    brand: "Nike",
    material: "Fabric: Body/face of front: 100% wool. Back of front panel: 80% polyester/20% cotton. Underbill: 100% cotton.",
    size: "Adjustable"
  },
  categories: [
    {
      name: "Clothing",
      path: "clothing/"
    },
    {
      name: "Hats",
      path: "clothing/hats/"
    }
  ],
  similarProducts: [
    "729497-010"
  ],
  relatedProducts: [
    "619360-689"
  ],
  updatedAt: "2016-01-05T10:00:00-04:00",
  createdAt: "2015-12-09T10:00:00-04:00",
  
  // Include inventory and UPC if available...
  inventory: 43,
  upc: "886549136925"
}
```
### Advanced Product example with Variations
```
{
  sku: "819952-029",
  url: "http://store.nike.com/au/en_gb/pd/air-jordan-spike-forty-shoe/pid-10873124/pgid-11115776",
  name: "AIR JORDAN SPIKE FORTY",
  description: "<h2>A LEGEND, REIMAGINED.</h2><p>The Air Jordan Spike Forty Men's Shoe is a player-exclusive sequel to the beloved Jordan Spizike. Iconic elements from the AJ V all get a fresh look thanks to modern materials and technology.</p>",
  price: 260.00,
  salePrice: 199.00,
  media: [
    {
      url: "http://images.nike.com/is/image/DotCom/PDP_HERO_S/AIR-JORDAN-SPIKE-FORTY-819952_029_A_PREM.jpg",
      {
        type: "video",
        url: "https://youtu.be/NPYJKb0MbXU"
      }
    }
  ],
  attributes: {
    // Example of basic attributes...
    type: "Shoe",
    color: "Black/Photo Blue/Atomic Orange/Fire Pink",
    colorFamily: "Multicolored",
    care: "Machine washable",
    weight: 240,
    brand: "Nike",
    sport: "Basketball",
    gender: "Mens"
    
    // Example of an array attribute...
    material: ["rubber", "fabric"],
    colors: ["Blue", "Black"],
    
    // Example of a detailed attribute..
    {
      name: "Shoe Height",
      code: "shoeHeight",
      value: "High Top"
    }
  },
  categories: [
    {
      name: "Men's",
      path: "mens/"
    },
    {
      name: "Men's Shoes",
      path: "mens/shoes/"
    },
    {
      name: "Men's Basketball Shoes",
      path: "mens/shoes/basketball"
    }
    {
      name: "Basketball Shoes",
      path: "basketball/shoes"
    }
  ],
  similarProducts: [
    "819952-706",
    "819952-605"
  ],
  relatedProducts: [
    "SX4846-901",
    "SX2554-901"
  ],
  updatedAt: "2016-01-05T10:00:00-04:00",
  createdAt: "2015-12-09T10:00:00-04:00",
  options: [
    "color",
    "size"
  ]
  variations: [
    {
      sku: "819952-029-BLU-9",
      upc: "886549136925",
      inventory: 43,
      attributes: [
        color: "Blue",
        size: "9"
      ],
      media: [
        url: "http://images.nike.com/is/image/DotCom/PDP_HERO_S/AIR-JORDAN-SPIKE-FORTY-819952_029_A_PREM_BLUE.jpg",
      ]
    },
    {
      sku: "819952-029-BLU-10",
      upc: "886549136927",
      inventory: 85,
      attributes: [
        color: "Blue",
        size: "10"
      ],
      media: [
        url: "http://images.nike.com/is/image/DotCom/PDP_HERO_S/AIR-JORDAN-SPIKE-FORTY-819952_029_A_PREM_BLUE.jpg",
      ]
    },
    {
      sku: "819952-029-BLA-9",
      upc: "886549136928",
      inventory: 143,
      attributes: [
        color: "Black",
        size: "9"
      ],
      media: [
        url: "http://images.nike.com/is/image/DotCom/PDP_HERO_S/AIR-JORDAN-SPIKE-FORTY-819952_029_A_PREM_BLACK.jpg",
      ]
    },
    {
      sku: "819952-029-BLA-10",
      upc: "886549136929",
      inventory: 235,
      attributes: [
        color: "Black",
        size: "10"
      ],
      media: [
        url: "http://images.nike.com/is/image/DotCom/PDP_HERO_S/AIR-JORDAN-SPIKE-FORTY-819952_029_A_PREM_BLACK.jpg",
      ]
    }
  ]
}
```
##Product Variation Object properties
When a Product has several variations, based on, for example, size and color, a product variation is required for each
possible combination. The variations are dynamically added to the interface as options of a single Product SKU to be selected when configuring that Product for order/purchase.

| Field | Type | Overview |
| ----- | ---- | -------- |
| sku | String | A unique identifier for this product variation. |
| upc *(optional)*| String | The barcode, UPC or ISBN number for the product. |
| inventory *(optional)*| Number | The number of products available for ordering. |
| media | Array | References to one or more [Media Assets](#media-object-properties), specifically for this variation |
| attributes | Array | References to one or more [Product Attributes](#attribute-object-properties). <br><br>**Note:** There must be an attribute for each of the attribute keys in the `options` Product property.

##Media Object properties
Each product has an array of Media Asset objects. Each Product Variation can also have a distinct set of Media Asset Objects.

Providing a pure string property represents `{ type: 'image', url: STRINGVALUE }`

| Field | Type | Overview |
| ----- | ---- | -------- |
| type *(optional)* | String | Defaults to 'image', also supported: 'video', 'youtube' |
| url | String | A URL reference for the asset |
| label *(optional)* | String | A description of the asset |
| position *(optional)* | Integer | Used for sorting assets (assending) |

##Attribute Object properties
Each product has an array of Attribute objects. Each Product Variation can also have a distinct set of Attribute Objects.

There are a couple of ways to provide product attributes, Detailed Attribute Object properties or Simple Attribute Object properties.

###Detailed Attribute Object properties

| Field | Type | Overview |
| ----- | ---- | -------- |
| name | String | A visible representation for the name of the attribute, i.e. Shoe Width |
| code | String | A code-level representation for the name of the attribute, i.e. shoeWidth or shoe_width |
| value | String | The actual value of the attribute |
| type *(optional)* | String | Defaults to 'string', also supported: 'Array', 'Object', 'HTML' |
| position *(optional)* | Integer | Used for sorting displayed attributes (ascending) |

###Simple Attribute Object properties
As an alternative to providing a detailed object property, a simple key: value Object can also be used.
Where value can be either an Array, String, Number or Float.

####Simple Attributes example
```
{
  
  ...Product Properties...,

  attributes: {
    key: value,
    
    // Array
    colors: ['Red', 'Green', 'Blue'],
    
    // String
    shoeWidth: 'Wide',
    
    // Number
    size: 5,
    
    // Float
    weight: 10.5,

  }
}
```

##Category Object properties
Each product has an array of Category objects, typically used as the display structure for FoyerLive Interact.

**Note: It is not necessary to include a ROOT category**

| Field | Type | Overview |
| ----- | ---- | -------- |
| name | String | The visible name of the category, excluding parent category references. |
| path | String | The full path for the category |

### Invalid Category Object examples

#### Providing a ROOT category
```
{
    name: "All Products",
    path: "/"
}
```

#### Path starting with a slash (/)
```
{
    name: "Shoes",
    path: "/shoes"
}
```

#### Name contains a breadcrumb format
In this case a more appropriate value for the `name` property would be `"Men's Shoes"`

```
{
    name: "Shoes - Mens",
    path: "shoes/mens"
}
```

#### Path contains an unnecessary slash (/)
```
{
    name: "Running Shoes",
    path: "shoes/running/"
}
```

### Valid Category Object examples

#### First-level category
```
{
    name: "Shoes",
    path: "shoes/"
}
```

#### Second-level category
```
{
    name: "Men's Shoes",
    path: "shoes/mens"
}
```

#### Third-level category
```
{
    name: "Running Shoes",
    path: "shoes/mens/running"
}
```

#### Third-level category alternative
```
{
    name: "Men's Running Shoes",
    path: "shoes/mens/running"
}
```

