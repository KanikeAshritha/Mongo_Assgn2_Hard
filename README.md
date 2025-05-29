# Mongo_Assgn2_Hard
<pre>
-----------------Hard1----------------------

db.products.aggregate([
  {
		$group : {
			_id : "$category",
			value : {$sum : { $multiply: ["$price", "$quantity"] }}
		}
	},
  {
		$project : {
			_id:0,
			categoryName : "$_id",
			totalInventoryValue : "$value",
			valueClassification : {
			$cond : {
				if: { $gt : ["$value",10000]},then : "High Value",
				else : {
					$cond : {
						if : {$gt : ["$value",5000]},then : "Medium Value",
						else : "Standard Value"
					}
				}
			}
		}}
	}
])

O/p:
{
  categoryName: 'Apparel',
  totalInventoryValue: 8800,
  valueClassification: 'Medium Value'
}
{
  categoryName: 'Electronics',
  totalInventoryValue: 28025,
  valueClassification: 'High Value'
}
{
  categoryName: 'Accessories',
  totalInventoryValue: 5400,
  valueClassification: 'Medium Value'
}
{
  categoryName: 'Sports',
  totalInventoryValue: 2700,
  valueClassification: 'Standard Value'
}
{
  categoryName: 'Home Goods',
  totalInventoryValue: 7500,
  valueClassification: 'Medium Value'
}

-----------------Hard2----------------------
	
db.products.aggregate([
{
	$sort : {price : -1}
},
{
	$group : {
		_id : "$supplier.name",
		maxPrice : {$first : "$price"},
		mostExpensiveProductName : {$first : "$name"}		
	}
},
{
	$project : {
		_id:0,
		supplierName : "$_id",
		mostExpensiveProductName : 1,
		maxPrice : 1
	}
},
{
	$sort : {maxPrice : -1}
}
])

o/p:	
{
  maxPrice: 1200,
  mostExpensiveProductName: 'Laptop Pro',
  supplierName: 'TechGlobe'
}
{
  maxPrice: 250,
  mostExpensiveProductName: 'Espresso Machine',
  supplierName: 'HomeBest'
}
{
  maxPrice: 199,
  mostExpensiveProductName: 'Smartwatch',
  supplierName: 'GadgetPro'
}
{
  maxPrice: 80,
  mostExpensiveProductName: 'Bluetooth Speaker',
  supplierName: 'SoundWave'
}
{
  maxPrice: 60,
  mostExpensiveProductName: 'Denim Jeans',
  supplierName: 'FashionHub'
}
{
  maxPrice: 45,
  mostExpensiveProductName: 'Leather Wallet',
  supplierName: 'StyleCraft'
}
{
  maxPrice: 30,
  mostExpensiveProductName: 'Yoga Mat',
  supplierName: 'ActiveLife'
}

	
-----------------Hard3----------------------
db.products.aggregate([
  {
    $match : {
      tags : {$all : ["portable"], $nin : ["computer"]}
    }
  },
  {
    $project : {
      _id : 0,
      name : 1,
      tags : 1
    }
  }
])

o/p:	
{
  name: 'Smartwatch',
  tags: [
    'wearable',
    'gadget',
    'portable'
  ]
}
{
  name: 'Bluetooth Speaker',
  tags: [
    'audio',
    'portable',
    'wireless'
  ]
}


	
</pre>
