# visu_roassal

## Installation
In order to install this project, execute the following script in the Playground of your Moose Image

```Smalltalk
Metacello new
  baseline: 'LabelContractor';
  repository: 'github://reda-idtaleb/label_contractor:main';
  load.
```  

## LabelContractor description:
The LabelContractor is an API will allow reducing labels on visualizations using different strategies.
In what follows, we will present the different strategies implemented and their applications on demonstration examples.

**Note: at the moment we cannot combine the strategies (that's the next job).**

### The original images of the examples on which the different strategies are applied:

The first image represents an example of visualization which contains boxes with labels above and the second image is a list of all the classes of the system built by spec2.
<p float="left">
  <img src="images/roassalExamples/original_visualization.png" width="1300" />
  <img src="images/specListExamples/originalList.png" width="450" /> 
</p>

### Strategies description:

*For each strategy, we show two examples, the top image represents the application of a strategy to a visualization and the one at the bottom is the application of a strategy to a list of all classes in the system generated by spec2.*

There are 9 ways to reduce labels:

1- LbCAbbreviateNamesStrategy: it allows to keep only the initial letter of each name except the last one('ExampleSomething' -> 'ESomething'). By default it takes the 1st letter of the first 3 names.
<p float="left">
  <img src="images/roassalExamples/abbreviateNamesStrategy.png" width="800" />
  <img src="images/specListExamples/abbreviateNamesStrategy.png" width="320" /> 
</p>

2- LbCBaseNameStrategy: for strings representing an absolute file paths, only the name of the file is kept by removing the path and its extension. ('A: path/example.txt' or 'example.txt' -> 'example').

*The left image represents an example of visualization before the application of the strategy and the image to the right represents the result of applying this strategy.*
<p float="left">
  <img src="images/roassalExamples/baseNameOriginal.png" width="300" />
  <img src="images/roassalExamples/baseNameStrategy.png" width="300" /> 
</p>


3- LbCEllipsisStrategy: consists in keeping a certain first and last letter of the string separated by 2 dots ('..'). By default we reduce up to 8 characters (without counting '..'). ('anExample' -> 'anEx..mple').
<p float="left">
  <img src="images/roassalExamples/ellipsisStrategy.png" width="800" />
  <img src="images/specListExamples/ellipsisStrategy.png" width="320" /> 
</p>

4- LbCPickFirstLettersStrategy: allows to keep some first letters of the string. By default, we keep the 8 first letters.
<p float="left">
  <img src="images/roassalExamples/pickFirstLettersStrategy.png" width="800" />
  <img src="images/specListExamples/pickFirstLettersStrategy.png" width="300" /> 
</p>

5- LbCRemoveFrequentLettersStrategy: allows you to remove frequent letters from a string until having the choosen size. By default we reduce until having a string of length 8.
<p float="left">
  <img src="images/roassalExamples/removeFrequentLettersStrategy.png" width="800" />
  <img src="images/specListExamples/removeFrequentLettersStrategy.png" width="300" /> 
</p>

6- LbCRemoveAnySubstringStrategy: allows you to remove all the occurrences of each substring from the string you want to reduce.

-> on the following visualization(left picture) we have removed { 'Hashed'. 'Moose'. 'value'. 'Identity' } from labels.

-> on the spec list(right picture) we removed the following substrings { 'ast'. 'Test'. 'Abstract' }.
<p float="left">
  <img src="images/roassalExamples/removeAnySubstringStrategy.png" width="900" />
  <img src="images/specListExamples/removeAnySubstringStrategy.png" width="320" /> 
</p>

7- LbCRemovePrefixStrategy: allows you to remove a substring(s) which is the prefix of the string you want to reduce.

-> on the following visualization(left picture) we have removed { 'Hashed'. 'Moose'. 'Wide'. 'small'. 'Identity' } from labels.

-> on the spec list(right picture) we removed the following substrings { 'abstract'. 'ast' }.
<p float="left">
  <img src="images/roassalExamples/removePrefixStrategy.png" width="900" />
  <img src="images/specListExamples/removePrefixStrategy.png" width="300" /> 
</p>

8- LbCRemoveSuffixStrategy: allows you to remove a substring(s) which is the suffix of the string that you want to reduce.

-> on the following visualization we removed { 'Storage'. 'Moose'. 'Bag'. 'Array'. 'set' } from labels

-> on the spec list(right picture) we removed { 'Test' }

<p float="left">
  <img src="images/roassalExamples/removeSuffixStrategy.png" width="900" />
  <img src="images/specListExamples/removeSuffixStrategy.png" width="300" /> 
</p>

9- LbCRemoveVowelsStrategy: consists in removing all the vowels (the letter 'y' is an exception in English, it's removed only when it represents a vowel) from the string.
<p float="left">
  <img src="images/roassalExamples/removeVowelsStrategy.png" width="850" />
  <img src="images/specListExamples/removeVowelsStrategy.png" width="320" /> 
</p>

## How to reduce a string using contractor: 
The API is based on the design strategy, so for example to use a "remove vowels strategy" you can type on the playground:

```Smalltalk
| removeVowelsStrategy |
removeVowelsStrategy := LbCRemoveVowelsStrategy new .
LbCContractor new
    strategy: removeVowelsStrategy;
    reduce: 'HashedCollection'. 
```    
