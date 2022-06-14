1.	Create a variable that specifies the field ordering:
orderedFieldList = ['COLUMN1', 'COLUMN2']

2.	Use the following logic
%dw 2.0
output application/json
fun orderFields(json, fieldList) =
  fieldList reduce (field, acc={}) -> acc ++ {(field):json[(field)]}
--- 
{GetRclaDataBSOutput: payload map(item, idx) -> orderFields(item mapObject (v,k,i) -> 
		{
			(k): v
		}, vars.orderedFieldList)
}
