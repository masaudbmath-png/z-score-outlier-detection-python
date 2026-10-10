# Z-Score Outlier Detection in Python: The Complete Guide

![Python](https://img.shields.io/badge/Python-3.8%2B-blue?logo=python)
![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-orange?logo=jupyter)
![License](https://img.shields.io/badge/License-MIT-green)

Welcome to the ultimate guide on **Z-score outlier detection in Python**. Whether you are performing Exploratory Data Analysis (EDA), cleaning data for machine learning models, or conducting statistical analysis, identifying and handling outliers is a critical step. This repository provides a comprehensive breakdown of the Z-score method, complete with mathematical explanations, Python code, and Jupyter Notebook examples.

---

## 📑 Table of Contents
1. [What is a Z-Score?](#1-what-is-a-z-score)
2. [How Z-Score Identifies Outliers](#2-how-z-score-identifies-outliers)
3. [Pros and Cons of the Z-Score Method](#3-pros-and-cons-of-the-z-score-method)
4. [Python Implementation (Pandas & Scipy)](#4-python-implementation)
5. [Handling Skewed Data: Modified Z-Score](#5-handling-skewed-data-modified-z-score)
6. [How to Run This Project](#6-how-to-run-this-project)

---

## 1. What is a Z-Score?

The **Z-score** (or standard score) is a fundamental statistical measurement that describes a data point's relationship to the mean of a group of values, measured in terms of standard deviations. 

In simple terms, it tells you **how many standard deviations away from the mean a specific data point is.**

### The Z-Score Formula

$$Z = \frac{(X - \mu)}{\sigma}$$

**Where:**
* **$Z$** = The Z-score
* **$X$** = The individual data point
* **$\mu$** = The mean (average) of the dataset
* **$\sigma$** = The standard deviation of the dataset

---

## 2. How Z-Score Identifies Outliers

When performing **outlier detection in Python**, we rely on the **Empirical Rule** (also known as the 68-95-99.7 rule) for normally distributed (Gaussian) data:

* 📊 **~68%** of data falls within **1** standard deviation of the mean ($Z$ between -1 and 1).
* 📊 **~95%** of data falls within **2** standard deviations ($Z$ between -2 and 2).
* 📊 **~99.7%** of data falls within **3** standard deviations ($Z$ between -3 and 3).

### The Outlier Threshold
Because 99.7% of data in a normal distribution falls within 3 standard deviations, any data point with a Z-score **greater than 3 or less than -3** (i.e., $|Z| > 3$) is highly unusual. Therefore, it is flagged as an **outlier**.

> 💡 **Pro Tip:** Depending on the strictness of your data cleaning pipeline, some data scientists use a threshold of 2.5 or 2.0, but **$|Z| = 3$** is the industry standard for statistical anomaly detection.

---

## 3. Pros and Cons of the Z-Score Method

Before applying the Z-score for data preprocessing, it's important to understand its limitations.

### ✅ Pros
* **Easy to Implement:** Extremely fast to calculate using `pandas` and `scipy`.
* **Highly Effective:** Works exceptionally well for large datasets that follow a normal (Gaussian) distribution.
* **Standardized:** Allows for easy comparison across different features and scales.

### ❌ Cons
* **Assumes Normality:** It assumes the underlying data is normally distributed.
* **The Masking Effect:** Because the mean ($\mu$) and standard deviation ($\sigma$) are heavily influenced by extreme values, the outliers themselves can skew the Z-score calculation, making them harder to detect.
* **Alternative Needed for Skewed Data:** If your data is highly skewed (e.g., income, house prices), the **IQR (Interquartile Range)** method or **Modified Z-score** (using the median and MAD) is highly preferred.

---

## 4. Python Implementation

Here is how you can implement Z-score outlier detection using **Python**, **Pandas**, and **Scipy**.

### Method A: Using `scipy.stats` (Recommended)
