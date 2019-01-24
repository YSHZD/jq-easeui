# jq-easeui
jq easeui
数组相邻合并
var datas = [
		{'name':'a','age':26}, // 0
		{'name':'a','age':26},// 1

		{'name':'b','age':26},// 2
		{'name':'b','age':26},// 3
		{'name':'b','age':26},// 4

		{'name':'a','age':26},// 5

		{'name':'c','age':26},// 6
		{'name':'c','age':26},// 7

		{'name':'a','age':26},// 8
		{'name':'a','age':26},// 9

		{'name':'d','age':26},// 10
		{'name':'d','age':26},// 11
		{'name':'d','age':26},// 12
		{'name':'d','age':26},// 13

		{'name':'a','age':26},// 14
		/*{'name':'a','age':26}// 15
		{'name':'a','age':26}// 16*/
	];
	function changeDate(Dates){
		var endResult = [];
		var out = [];
		var len = Dates.length;
		for(var i = 0; i < len-1; i++){
			if(Dates[i]['name'] == Dates[i+1]['name']){
				continue;
			}else{
				endResult.push(i)
			}
		}
		console.log(endResult); // [1, 4, 5, 7, 9, 13]
		var lens = endResult.length;
		for(var i = 0; i < lens; i++){
			if(i==0){
				out.push({
					'index':0,
					'count':endResult[i]+1
				})
			}else{
				out.push({
					'index':endResult[i-1]+1,
					'count':endResult[i] - endResult[i-1]
				})
			}
		}
		if(endResult[endResult.length-1]<=len){
			out.push({
					'index':endResult[endResult.length-1]+1,
					'count':len - endResult[endResult.length-1]-1
				})
		}
		/*out = [
			{'index':0,'count':2},
			{'index':2,'count':3},
			{'index':5,'count':1},
			{'index':6,'count':2},
			{'index':8,'count':2},
			{'index':10,'count':4},
			{'index':14,'count':2}
		];*/
		console.log(out);
	}
	changeDate(datas)
	
	
	function group(arr,num){
		var arr = quickSort(arr);
		arr = arr.reverse();
		console.log(arr)
		var endArr = [];
		var arrLen = arr.length;
		for(var i = 0; i < num; i++){
			endArr.push({
				'data':[],
				'sum':0
			})
		}
		for(var i = 0; i < arrLen; i++){
			(function(i){
				var index = minArr(endArr);
				endArr[index].data.push(arr[i]);
				endArr[index].sum = endArr[index].sum + arr[i];
			})(i)
			
		}
		for(var i = 0; i < num; i++){
			endArr[i].data = endArr[i].data.sort(function(a,b){
				return Math.random()>=0.5
			})
		}
		console.log(endArr)
	}
	function minArr(arr){
		var minKey = 0;
		var len = arr.length;
		for(var i = 1; i < len; i++){
			if(arr[minKey].sum > arr[i].sum){
				minKey = i
			}
		}
		return minKey;
	}

function quickSort(arr){
	if(arr.length <= 1){
		return arr
	}
	var basePoint = Math.floor(arr.length/2);
	var point = arr.splice(basePoint,1)[0];
	var left = [];
	var right = [];
	for( var i = 0; i < arr.length; i++){
		if(arr[i] < point){
			left.push(arr[i])
		}else{
			right.push(arr[i])
		}
	}
	return quickSort(left).concat([point],quickSort(right));
}
var arr = [2,3,4,5,6,3,23,4,3,4,2,34,6,23,32,34,54,43,23,43,34,2,3,34,23,2,12,23,43,23,1,14,15,15,16,16,17,18,9,13,15];
group(arr,3);
数组分组 每组相差最小
