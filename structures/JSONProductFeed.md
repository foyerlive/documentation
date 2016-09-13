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
| media | array | References to various media assets. |
|  |  |  |  |

```
{
  id: "NIKAJORDFORT",
  upc: "886549136925",
  url: "http://store.nike.com/au/en_gb/pd/air-jordan-spike-forty-shoe/pid-10873124/pgid-11115776",
  brand: "Nike",
  name: "AIR JORDAN SPIKE FORTY",
  description: "<h2> A LEGEND, REIMAGINED.</h2><p>The Air Jordan Spike Forty Men's Shoe is a player-exclusive sequel to the beloved Jordan Spizike. Iconic elements from the AJ V all get a fresh look thanks to modern materials and technology.</p>",
  price: 260.00,
  salePrice: 199.00,
  media: [
    {
      url:"http://images.nike.com/is/image/DotCom/PDP_HERO_S/AIR-JORDAN-SPIKE-FORTY-819952_029_A_PREM.jpg"
    }
  ]
}
```
