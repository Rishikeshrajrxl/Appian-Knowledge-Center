**Append()**
	append(array, value)
	 example: `append( {1,2,3}, "Akash")`  => {1, 2, 3, null()}
	 Cannot convert Text in Numbers but vise-versa is true.
**Len()**
	 Returns the length in characters of the **==text==**.
	 Example: `len("abcd") ` => 4
	 but `len({"abcd", "ef"})`  => 4, 2 (here len() received a list of input parameters, so it evaluates all )

**Concat()**
	 Concatenates the specified strings into one string. If arrays are passed as parameters, the function will concatenate the elements of the arrays into one string. This function replaces the concatenate function.
	 example: `concat({1, 2, 3}, "aakash")` => "123aakash"`
	 
**length()**
	Returns the number of elements in an array **==excluding nulls==**. To include nulls, use count.

**Count()**
	Returns the number of elements **==including null==** values. For example, `count(1, 2, {"3", "", "5"}, 6)` returns 6 and `count({"a", "b", "", "d"})` returns 4. To get the number of items in an array excluding nulls, use length.

**a!queryRecordType()**
- Executes a query on a given record type and returns the resulting data.
- **fetchTotalCount** : Retrieves the total number of rows of the resulting datasubset. (Not applicable for process-backed or unsynced expression-backed record types).
- **relatedRecordData**: When selecting one-to-many related record data. This parameter is not supported when performing an aggregation.

**ASCII Code**
 - A - Z -> (65 - 90)
 - a - z -> (97 - 122)
 - 
