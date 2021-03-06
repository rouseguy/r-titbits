---
layout:     post
title:      "using apply with a custom function"
subtitle:   "Find number of times price went up in a week."
date:       2016-01-19 12:00:00
author:     "Bargava"
header-img: "img/post-bg-2016-1.jpg"
tags:
- R
- Data Science
---

Consider the following problem: *Prices of the product at the end of the day are given for one week. Find the number of times price went up compared to the previous day?*

We can use the `apply` function to find this. To use that, we will need to make use of a custom function. 

**Step 1**: Let's generate the data

	# Set seed for reproducibility
    set.seed(123)
    # Generate a matrix that has prices for 5 products for each day of the week
    product_prices <- matrix(runif(35,0,1), 5)
   

**Step 2**: Use `apply` function

The solution using `apply` function should be something like this

    product_prices$num_upmoves <- apply(product_prices, 1, find_num_upmoves)
    
Let's now write the `find_num_upmoves` function before executing Step 2.

**Step 3** The `find_num_upmoves` function

	find_num_upmoves <- function(x){
	  #Need to initialize two variables
	  #Counter - to loop through all the values in the row
	  #Variable to store the number of times price increased
	  i = 1   #counter variable
	  num_of_elem_greater = 0  #variable to store no. of times price increased
	  while(i < length(x)){
	    if(x[i]<x[i+1]) {
	      num_of_elem_greater = num_of_elem_greater + 1
	    }
	    i = i + 1
	  }
	  return(num_of_elem_greater)
	}
	
**Step 4** Run the `apply` function - as typed in Step 2

After that, type this to check

	product_prices$num_upmoves
	
This should return

	[1] 3 2 4 3 2
