#FoyerLive - JSON Product Feed

##Product Properties
  
| Field | Type | Overview |
| ----- | ---- | -------- |
| sku | integer,string | A unique identifier for the product. |
| upc | string | The barcode, UPC or ISBN number for the product. |
| url | string | A URL to purchase the product. |
| brand | string | The brand name or vendor of the product. |
| name | string | The product name. |
| description | string | The product description. Can contain basic HTML. |
| price | double | The default product price. |
| salePrice | double | The product sale price, leave empty to use the default price. |
| media | array | References to various Media assets. |
| attributes | array | References to various product Attributes. |
| categories | array | References to various product Categories. |
| similarProducts | array | References to similar product SKUs. |
| relatedProducts | array | References to related product SKUs. |

```
{
  id: "819952-029",
  upc: "886549136925",
  url: "http://store.nike.com/au/en_gb/pd/air-jordan-spike-forty-shoe/pid-10873124/pgid-11115776",
  brand: "Nike",
  name: "AIR JORDAN SPIKE FORTY",
  description: "<h2> A LEGEND, REIMAGINED.</h2><p>The Air Jordan Spike Forty Men's Shoe is a player-exclusive sequel to the beloved Jordan Spizike. Iconic elements from the AJ V all get a fresh look thanks to modern materials and technology.</p>",
  price: 260.00,
  salePrice: 199.00,
  media: [
    {
      url:"http://images.nike.com/is/image/DotCom/PDP_HERO_S/AIR-JORDAN-SPIKE-FORTY-819952_029_A_PREM.jpg",
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
    weight: 170,
    sport: "Basketball",
    gender: "Mens"
    
    // Example of an array attribute...
    material: ["rubber", "fabric"],
    
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
  createdAt: "2015-12-09T10:00:00-04:00"
}
```
