Say you have an array for which the ith element is the price of a given stock on day i.

If you were only permitted to complete at most one transaction (i.e., buy one and sell one share of the stock), design an algorithm to find the maximum profit.

Note that you cannot sell a stock before you buy one.

* 1. Brute force
```java
public static int maxProfit(int[] prices) {
	int profit=0;
        for(int i=0;i<prices.length;i++){
        	for(int j=i+1;j<prices.length;j++){
        		if(prices[j]-prices[i]>profit){
        			profit=prices[j]-prices[i];
        		}
        	}
        }
        if(profit<=0)
        	return 0;
        else
        	return profit;
	        }
```

* 2. One pass 
![peak](https://leetcode.com/media/original_images/121_profit_graph.png)
We need to find the largest peak following the smallest valley.
```java
//My solution(pass)
public static int maxProfit(int[] prices) {
	int max=prices[0],min=prices[0];
	int maxindex=0,minindex=0;
        for(int i=1;i<prices.length;i++){
        	if(prices[i]>=max){
        		max=prices[i];
        		maxindex=i;
        	}
        	if(prices[i]<min){
        		min=prices[i];
        		minindex=i;
        	}
        	if(maxindex<=minindex){
        		max=0;
        		maxindex=i;
        	}
	        }
        if(maxindex>minindex)
        	return max-min;
        else
        	return 0;     
}
//evaluated
public static int maxProfit(int[] prices) {
	int maxprofit=0;
	int minprice=Integer.MAX_VALUE;
        for(int i=1;i<prices.length;i++){
        	if(prices[i]<minprice){
        		minprice=prices[i];
	        }
        	if(prices[i]-minprice>maxprofit){
        		maxprofit=prices[i]-minprice;
        	}
        }
        return maxprofit;
}
```
