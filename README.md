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

  
</pre>
