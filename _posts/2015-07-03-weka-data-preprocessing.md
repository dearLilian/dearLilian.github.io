---
layout: post
title: 通过weka.jar包来进行数据预处理
date: 2015-07-03
tag: 数据挖掘
---


## 目录

* TOC 
{:toc}



本文转自<a href="http://blog.csdn.net/lilianforever/article/details/46740331">我的CSDN博客</a>。


前言：注意首先要将weka.jar包加载到相应的路径中去。程序中的数据也是用的weka自带的数据。
扩展：eclipse添加jar包的操作方法：
打开eclipse ,在对应的工程下右击，选择Build Path ->选择Configure Build Path  ->选择Libraries  ->点击Add External JARs  ->然后到你的jar包所在路径选择它。即可。


## 一、特征选择

```java
package learning;

import weka.attributeSelection.ASEvaluation;
import weka.attributeSelection.InfoGainAttributeEval;
import weka.attributeSelection.Ranker;
import weka.core.Instances;
import weka.core.converters.ConverterUtils.DataSink;
import weka.core.converters.ConverterUtils.DataSource;
import weka.filters.Filter;
import weka.filters.supervised.attribute.AttributeSelection;


/**feature selection via weka
 * 
 * @author wenbaoli
 *
 */
public class featureSelect {

	/**
	 * 
	 * @param arg
	 */
	public static void main(String[] arg){
		
		try {

			System.out.println("++++++++++++Example3:Feature Selection Via Weka.+++++++++");
			
			System.out.println("Step1:load data...");
			String fn = "E:/weka/data/iris.arff";
			DataSource source = new DataSource(fn);
			Instances instances = source.getDataSet();
			
			System.out.println("Step2:feature selction...");
			featureSelect fs = new featureSelect();
			
			int k = 2;
			AttributeSelection as = new AttributeSelection();
			
			Ranker rank = new Ranker();
			rank.setThreshold(0.0);
			rank.setNumToSelect(k);
			
			ASEvaluation ae = new InfoGainAttributeEval();
		
			as.setEvaluator(ae);
			as.setSearch(rank);
			as.setInputFormat(instances);
			Instances reductData = Filter.useFilter(instances, as);
			
			System.out.println("Step3:保存规约后的数据到新文件...");
			DataSink.write("E:/weka/data/iris_reducted.arff", reductData);
			System.out.println("Finished...");
			
			
		} catch (Exception e) {
			e.printStackTrace();
		}	
	}
	
}
```

## 二、缺失值处理

```java
package learning;

import weka.core.Instances;
import weka.core.converters.ConverterUtils.DataSink;
import weka.core.converters.ConverterUtils.DataSource;


/**Missing value Handling via weka
 * 
 * @author wenbaoli
 *
 */
public class missingHandle {

	/**
	 * 
	 * @param arg
	 */
	public static void main(String[] arg) {
		
		try {
			System.out.println("+++++++++++++Example 2 :Missing Value Handling.++++++++++++++");
			
			System.out.println("Step1:load data...");
			
			String fn = "E:weka/data/labor.arff";
			
			DataSource source = new DataSource(fn);
			
			Instances instances = source.getDataSet();
			int dim = instances.numAttributes();
			int num = instances.numInstances();
			
			System.out.println("Step2:缺失值处理...");
			double[] meanV = new double[dim];
			for (int i = 0; i < meanV.length; i++) {
				meanV[i] = 0;
				int count = 0;
				for (int j = 0; j < num; j++) {
					if(!instances.instance(j).isMissing(i)){
						meanV[i] += instances.instance(j).value(i);
						count++;
					}
				}
				meanV[i] = meanV[i]/count;
				System.out.println(meanV[i]);
			}
			
			
			for (int i = 0; i < meanV.length; i++) {
				meanV[i] = 0;
				int count = 0;
				for (int j = 0; j < num; j++) {
					if(instances.instance(j).isMissing(i)){
						instances.instance(j).setValue(i, meanV[i]);
					}
				}
				
				
			}
			
			System.out.println("Step3:保存数据到新文件...");
			
			DataSink.write("E:weka/data/labor_missingValueHandled.arff", instances);
			System.out.println("Finished.");
		} catch (Exception e) {
			e.printStackTrace();
		}
		
		
	}
}
```

## 三、归一化处理



```java
package learning;



import weka.core.Attribute;
import weka.core.Instance;
import weka.core.Instances;
import weka.core.converters.ConverterUtils.DataSink;
import weka.core.converters.ConverterUtils.DataSource;
import weka.filters.Filter;
import weka.filters.unsupervised.attribute.Normalize;


/**normalize data via weka
 * 
 * @author wenbaoli
 *
 */
public class normalizeTest {

	/**
	 * 
	 * @param arg
	 */
	public static void main(String[] arg) {
		
		
		String file = "cpu.arff";
		String file_norm = "norm_" + file;
		//对数据进行归一化
		try {
		System.out.println("+++++++++++++Example 1 : Normalize Data via weka.+++++++++");
		
		System.out.println("Step1:读取数据...");
		DataSource source = new DataSource("E:/Weka/data/" + file);
		Instances instances = source.getDataSet();
		
		System.out.println("Step2:原数据打印...");
		System.out.println("---------------------------------");
		int attributeNo = instances.numAttributes();
		for (int i = 0; i < attributeNo; i++) {
			Attribute attr = instances.attribute(i);
			System.out.print(attr.name() + "\t");
			
		}
		System.out.println();
		
		int instanceNo = instances.numInstances();
		for (int i = 0; i < instanceNo; i++) {
			Instance ins = instances.instance(i);
			System.out.print(ins.toString() + "\t");
			System.out.println();
		}
		
		System.out.println("Step3:归一化...");
		Normalize norm = new Normalize();
		norm.setInputFormat(instances);
		
		//归一化关键步骤：
		Instances newInstances = Filter.useFilter(instances, norm);
		
		System.out.println("Step4:归一化之后的数据(打印)...");
		System.out.println("---------------------------------");
		
		//打印属性名
		int numOfAttributes = newInstances.numAttributes();
		for (int i = 0; i < numOfAttributes; i++) {
			Attribute attribute = newInstances.attribute(i);
			System.out.print(attribute.name() + "\t");
			
		}
		System.out.println();
		
		//打印实例
		int numOfInstance = newInstances.numInstances();
		for (int i = 0; i < numOfInstance ; i++) {
			Instance instance = newInstances.instance(i);
			System.out.print(instance.toString() + "\t");
			System.out.println();
		}
		//发现一个问题：这把标签label也给归一化了。。。。。。。。。。这样可以吗？？？？？？？
		
		System.out.println("Step5:保存归一化的新数据到新文件...");
		System.out.println("-----------------------");
		DataSink.write("E:/Weka/data/" +file_norm, newInstances);
		System.out.println("Congratulations.");
		} catch (Exception e) {
			e.printStackTrace();
		}
		
		
	}
}
```

