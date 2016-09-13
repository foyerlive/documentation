#FoyerLive - JSON Product Feed

##Product Object Properties
  
| Field | Type | Overview |
| ----- | ---- | -------- |
| sku | string | A unique identifier for the product. |
| upc | string | The barcode, UPC or ISBN number for the product. |
| url | string | A URL to purchase the product. |
| inventory | number | The number of products available for ordering. |
| name | string | The product name. |
| description | string | The product description. Can contain basic HTML. |
| price | double | The default product price. |
| salePrice | double | The product sale price, leave empty to use the default price. |
| media | array | References to various Media assets. |
| attributes | array | References to various product Attributes. |
| categories | array | References to various product Categories. |
| similarProducts | array | References to similar product SKUs. |
| relatedProducts | array | References to related product SKUs. |
| options | array | List of attributes that require configuration. |
| variations | array | List of product Variations, based on attributes like size or color. |

### Simple Product Example
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
### Configurable Product Example
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

##Media Object Properties
Each product has an array of Media objects. Each Product Variation can also have an distinct set of Media Objects.

Providing a pure string property represents `{ type: 'image', url: STRINGVALUE }`

| Field | Type | Overview |
| ----- | ---- | -------- |
| type | string | Defaults to 'image', also supported: 'video', 'youtube' |
| url | string | A URL reference for the asset |
| label (optional) | string | A description of the asset |
| position (optional) | integer | Used for sorting assets (assending) |
