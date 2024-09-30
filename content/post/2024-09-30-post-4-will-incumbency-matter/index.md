---
title: 'Post #4: Will Incumbency Matter?'
author: Avi Agarwal
date: '2024-09-30'
slug: post-4-will-incumbency-matter
categories: []
tags: []
---



































# Introduction

# Model Excluding Incumbency


```
## 
## Excluding Incumbent Regression Results
## ===================================================
##                            Dependent variable:     
##                       -----------------------------
##                       Democrat Two Party Vote Share
## ---------------------------------------------------
## Weighted Avg. Poll              0.603***           
##                                  (0.102)           
##                                                    
## RDPI Growth Quarterly             0.242            
##                                  (0.242)           
##                                                    
## Constant                        22.060***          
##                                  (4.643)           
##                                                    
## ---------------------------------------------------
## Observations                       13              
## R2                                0.777            
## Adjusted R2                       0.732            
## Residual Std. Error          2.609 (df = 10)       
## F Statistic              17.408*** (df = 2; 10)    
## ===================================================
## Note:                   *p<0.1; **p<0.05; ***p<0.01
```



Table: <span id="tab:unnamed-chunk-12"></span>Table 1: 2024 Democrat Two Party Vote Share via Model Excluding Incumbent Party

| Prediction| Lower Bound| Upper Bound|
|----------:|-----------:|-----------:|
|      50.96|        44.7|       57.22|

# Model Including Incumbency


```
## 
## Including Incumbent Regression Results
## ===================================================
##                            Dependent variable:     
##                       -----------------------------
##                       Democrat Two Party Vote Share
## ---------------------------------------------------
## Weighted Avg. Poll              0.593***           
##                                  (0.080)           
##                                                    
## RDPI Growth Quarterly            0.485**           
##                                  (0.209)           
##                                                    
## Incumbent Party                  3.422**           
##                                  (1.262)           
##                                                    
## Constant                        20.017***          
##                                  (3.708)           
##                                                    
## ---------------------------------------------------
## Observations                       13              
## R2                                0.877            
## Adjusted R2                       0.836            
## Residual Std. Error          2.040 (df = 9)        
## F Statistic               21.432*** (df = 3; 9)    
## ===================================================
## Note:                   *p<0.1; **p<0.05; ***p<0.01
```


Table: <span id="tab:unnamed-chunk-9"></span>Table 2: 2024 Democrat Two Party Vote Share via Model Including Incumbent Party

| Prediction| Lower Bound| Upper Bound|
|----------:|-----------:|-----------:|
|       52.1|       47.04|       57.17|

# Time For Change Model


```
## 
## Time For Change Regression Results
## =========================================================
##                              Dependent variable:         
##                      ------------------------------------
##                      Incumbent Party Two Party Vote Share
## ---------------------------------------------------------
## June Approval                      0.166**               
##                                    (0.065)               
##                                                          
## GDP Growth Quarterly                0.328                
##                                    (0.268)               
##                                                          
## Incumbent                           1.655                
##                                    (1.787)               
##                                                          
## Constant                          49.338***              
##                                    (1.952)               
##                                                          
## ---------------------------------------------------------
## Observations                          13                 
## R2                                  0.734                
## Adjusted R2                         0.646                
## Residual Std. Error             2.931 (df = 9)           
## F Statistic                  8.292*** (df = 3; 9)        
## =========================================================
## Note:                         *p<0.1; **p<0.05; ***p<0.01
```


Table: <span id="tab:unnamed-chunk-16"></span>Table 3: 2024 Democrat Two Party Vote Share via Time for Change Model

| Prediction| Lower Bound| Upper Bound|
|----------:|-----------:|-----------:|
|      46.67|       39.12|       54.23|

