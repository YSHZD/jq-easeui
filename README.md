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
