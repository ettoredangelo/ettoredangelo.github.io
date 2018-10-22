---
layout: post
title:  "Selenium guide"
date:   2018-10-15 09:00:00 -0400
featured-img: python
---
## To whom is this guide for?
The target of this guide is a beginner Python user. The guide will take as requirement only a basic understanding of Python, but it will go through every other concept.

In any case I suggest reading the [Selenium official website](https://www.seleniumhq.org/) in order to have the most up-to-date informations.

## What is Selenium?

As the official Selenium webpage says: *"Selenium automates browsers".* Which means that you can use Selenium in order to automatize the actions that is highly repetitive and boring. What you do with this tool is entirely up to you!

For example you can automate a super boring task. Says that you need to download from a webpage a certain number of pdfs, with Selenium **you can do it!**  Says that you need to create a web scraper to download your favourite lyrics, with Selenium **you can do it!**. <br> If you need to automate your coffee machine to prepare your  morning coffee and bring it to your bed, well unfortunately you can't do it with Selenium...

## Installation

The main initial disadvantage of the Selenium library is that it may be quite difficult to install. We will go through the installation process in the two main Operating Systems:
- [iOS](#mac os)

- [Windows](#windows)

  <a id='mac os'>

  #### Mac OS

  The installation consists in two parts: 
  - installing the selenium library
  - installing the WebDriver.

  ##### Installing the Selenium library

  If you have Anaconda installed open the Terminal and try:

  `conda install selenium`

  If this does not work, or you do not have Anaconda installed, you need to use pip:

  `pip install selenium`

  When this process is done if you open Python and run:

  ```python
  import selenium
  ```

  **Should give no error.**

  If this gives an error it means that `pip` is not installed (in this case you need to install it).

  This is the procedure to install any Python library.

  ##### Installing the WebDriver

  Now we need to **download the WebDriver**. The WebDriver is the program that creates the browser window that can be automated by Python.
  There are several different browsers that can be used:
  - Chrome
  - Safari
  - Mozilla
  - Opera
    and many others.

  In my personal opinion the best one is the Chrome driver that can be downloaded from [here](https://sites.google.com/a/chromium.org/chromedriver/).

  In this guide we will see how to install the Chrome driver, but the procedure is identical for any other browser. <br>
  **N.B.** you need to have the browser installed in order to use the driver.

  Once you download the zip file you need to extract the executable and put it in a folder of your choice. You need to copy the directory of the file. It is enough to press the right button on the executable, then click on 'Get Info..' and copy the directory from the window that is now opened.

  Now we neeed to change the Environmental variable named PATH. Do not be scared, because it is not as difficult as it looks like. The best way is the following:
  1. Open your terminal
  2. Run `sudo nano /etc/paths`
  3. It will ask for your password, enter it.
  4. Now a file is opened, do to the bottom and paste the directory that we copyed before
  5. Press CTRL and X simultaneously
  6. Press Y to Save
  7. Press Enter to confirm

  Now your PATH environmental variable is edited. To check that everything is correct, close the Terminal and re-open it. Be aware that restarting the terminal is a fundamental part. Now run `echo $PATH`. <br> 
  You should see at the end of the output the directory that you just pasted.

  Now run the following in Python:
  ```python
  from selenium import webdriver
  
  driver = webdriver.Chrome('paste here the path\chromedriver')
  ```

  After a little bit an empty Chrome window should open

  Congratulations!! The installation is completed! You can now write your [first program with Selenium](#first program)!

  <a id='windows'>

  #### Windows

  The installation consists in two parts:
  - install the selenium library 
  - install the webdriver.

  If you have Anaconda installed open the Anaconda Prompt (you can find it form the Start menu):

  `conda install selenium`

  If this does not work, or you do not have Anaconda installed, you need to use pip, open the command line (Press the button with the Windows icon and R simoultaneously then type 'cmd' and press Enter):

  `pip install selenium`

  When this process is done if you open Python and run:

  ```python
  import selenium
  ```

  **Should give no error.**

  If this gives an error it means that `pip` is not installed (in this case you need to install it).

  This is the standard procedure to install any Python library.

  Now we need to **download the WebDriver**. The WebDriver is the program that creates the browser window that can be automated by Python.
  There are several different browsers that can be used:
  - Chrome
  - Safari
  - Mozilla
  - Opera
    and many others.

  In my personal opinion the best one is the Chrome driver that can be downloaded from [here](https://sites.google.com/a/chromium.org/chromedriver/).

  In this guide we will see how to install the Chrome driver, but the procedure is identical for any other browser. <br>
  **N.B.** you need to have the browser installed in order to use the driver.

  Once you download the zip file you need to extract the executable and put it in the same folder as Chrome. <br>
  The Chrome folder is in: C: > Programs (x86) > Google > Chrome > Application. <br>
  You need to copy the directory of the file. It is enough to press the right button on the executable, then click on 'Properties' and copy the directory from the window that is now opened.


  Now run the following in Python:
  ```python
  from selenium import webdriver
  
  driver = webdriver.Chrome('paste here the path\chromedriver.exe')
  ```

  After a little bit an empty Chrome window should open.

  Congratulations!! The installation is completed! You can now write your [first program with Selenium](#first program)!

  <a id='first program'>

  ## The first program with Selenium!

In this section we will write a simple script and explain each passage step by step. The script is the following:

  ```python
  from selenium import webdriver
  
  driver = webdriver.Chrome('paste here the path\chromedriver.exe')
  
  driver.get("https://www.google.it")
  
  inputElement = driver.find_element_by_name("q")
  inputSentence = "meteo " + "Milano"
  inputElement.send_keys(inputSentence)
  inputElement.submit()
  
  temp = driver.find_element_by_id("wob_tm")
  temp = temp.text
  ```

  This really short script does the following:
  1. It opens the browser at 'www.google.it'
  2. Searches 'meteo Milano'
  3. Takes the temperature in Milan

  I will explain each point in the following subparagraphs

  **How do we open the browser at the URL of our choice?**

  ```python
  driver.get("https://www.google.it")
  ```

  We do it thanks to the 'get' method. 
  This opens the browser at the URL given as a string.

  **How do we type in a text box?**

  ```python
  inputElement = driver.find_element_by_name("q")
  inputSentence = "meteo " + "Milano"
  inputElement.send_keys(inputSentence)
  inputElement.submit()
  ```

  First of all we need to select the text box, we do it by the 'find_element_by_name' method. There are many different find elements method, more or less one for each type of HTML characteristics. <br>
  We insert the string in the textbox with the 'send_keys' method and then we submit with the homonimous method.

  **How do we extract text?**

  ```python
  temp = driver.find_element_by_id("wob_tm")
  temp = temp.text
  ```

  First of all we select the element with another 'find_element_by' method. 
  Then we take it thanks to the 'text' attribute

