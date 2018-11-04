Developing Data Product Week4 - Interest Calculator
========================================================
author: Ankit Singhal
date: 11-Nov-2018
autosize: true

Overview
========================================================

This is an RStudio shiny application developed as a part of final project in the Developing Data Products course in Coursera Data Science Specialization track. The application is an interest calculator
The project includes:
A number input to input the principal amount
Slider inputs to select the interest rate and the time period
A dropdown box to select the rate of caluclation (Yearly or Quarterly)

This app is hosted at: 

Application widgets used
========================================================
This application uses four widgets listed below:

numericInput: A field to enter numbers, in this case - the principal amount (in $)

sliderInput: A slider bar 1. First slider is to choose the yearly interest rate (in %) 2. Second slider 
is to choose the number of time periods

selectInput: A box with choices to select from, in this case - the type of time period: years, quarters

actionButton: An Action Button, in this case to provide non-reactive reactivity to refresh and calculate

Code- Ui.R
========================================================

```r
library(shiny)

# Define UI for application that draws a histogram
shinyUI(fluidPage(
  
  # Application title
  titlePanel("Simple Interest Calculator"),
  
  # Sidebar with a slider input for number of bins 
  sidebarLayout(
    sidebarPanel(
      helpText("This app calculates simple interest based on your inputs."),            
      numericInput("num_principal", label = h6("Enter the principal amount (in $)"), value = 100),
      sliderInput("slider_intrate", label = h6("Choose the yearly interest rate (in %)"), min = 0, max = 30, value = 2),
      sliderInput("slider_num", label = h6("Choose the number of time periods"), min = 0, max = 20, value = 5),
      selectInput("select_time", label = h6(""), choices = list("Years" = 1, "Quarters" = 2), selected = 1),
      actionButton("action_Calc", label = "Refresh & Calculate")        
    ),
    
    # Show a plot of the generated distribution
    mainPanel(
      tabsetPanel(
        tabPanel("Output",
                 p(h5("Your entered values:")), textOutput("text_principal"),
                 textOutput("text_intrate"), textOutput("text_num"),
                 textOutput("text_time"), p(h5("Calculated values:")),
                 textOutput("text_int"), textOutput("text_amt")
        ),
        tabPanel("Documentation",
                 p(h4("Simple Interest Calculator:")),
                 helpText("This application calculates simple interest and total amount, i.e. principal + interest."),
                 HTML("<u><b>Method for calculation: </b></u>
                      <br> <br>
                      <b> Amt = Prpl + Int = Prpl(1 + rate * time) ; R = rate * 100 </b>
                      <br>
                      where: <br>
                      Amt = Total amount (Principal + Interest) <br>
                      Prpl = Principal amount <br>
                      Int = Interest amount <br>
                      rate = Rate of interest per year, in decimal; r=R/100 <br>
                      time = Time period invested in years/quarters")                
        )
      )
    )
  )
))
```

<!--html_preserve--><div class="container-fluid">
<h2>Simple Interest Calculator</h2>
<div class="row">
<div class="col-sm-4">
<form class="well">
<span class="help-block">This app calculates simple interest based on your inputs.</span>
<div class="form-group shiny-input-container">
<label for="num_principal">
<h6>Enter the principal amount (in $)</h6>
</label>
<input id="num_principal" type="number" class="form-control" value="100"/>
</div>
<div class="form-group shiny-input-container">
<label class="control-label" for="slider_intrate">
<h6>Choose the yearly interest rate (in %)</h6>
</label>
<input class="js-range-slider" id="slider_intrate" data-min="0" data-max="30" data-from="2" data-step="1" data-grid="true" data-grid-num="10" data-grid-snap="false" data-prettify-separator="," data-prettify-enabled="true" data-keyboard="true" data-data-type="number"/>
</div>
<div class="form-group shiny-input-container">
<label class="control-label" for="slider_num">
<h6>Choose the number of time periods</h6>
</label>
<input class="js-range-slider" id="slider_num" data-min="0" data-max="20" data-from="5" data-step="1" data-grid="true" data-grid-num="10" data-grid-snap="false" data-prettify-separator="," data-prettify-enabled="true" data-keyboard="true" data-data-type="number"/>
</div>
<div class="form-group shiny-input-container">
<label class="control-label" for="select_time">
<h6></h6>
</label>
<div>
<select id="select_time"><option value="1" selected>Years</option>
<option value="2">Quarters</option></select>
<script type="application/json" data-for="select_time" data-nonempty="">{}</script>
</div>
</div>
<button id="action_Calc" type="button" class="btn btn-default action-button">Refresh &amp; Calculate</button>
</form>
</div>
<div class="col-sm-8">
<div class="tabbable">
<ul class="nav nav-tabs" data-tabsetid="3824">
<li class="active">
<a href="#tab-3824-1" data-toggle="tab" data-value="Output">Output</a>
</li>
<li>
<a href="#tab-3824-2" data-toggle="tab" data-value="Documentation">Documentation</a>
</li>
</ul>
<div class="tab-content" data-tabsetid="3824">
<div class="tab-pane active" data-value="Output" id="tab-3824-1">
<p>
<h5>Your entered values:</h5>
</p>
<div id="text_principal" class="shiny-text-output"></div>
<div id="text_intrate" class="shiny-text-output"></div>
<div id="text_num" class="shiny-text-output"></div>
<div id="text_time" class="shiny-text-output"></div>
<p>
<h5>Calculated values:</h5>
</p>
<div id="text_int" class="shiny-text-output"></div>
<div id="text_amt" class="shiny-text-output"></div>
</div>
<div class="tab-pane" data-value="Documentation" id="tab-3824-2">
<p>
<h4>Simple Interest Calculator:</h4>
</p>
<span class="help-block">This application calculates simple interest and total amount, i.e. principal + interest.</span>
<u><b>Method for calculation: </b></u>
                      <br> <br>
                      <b> Amt = Prpl + Int = Prpl(1 + rate * time) ; R = rate * 100 </b>
                      <br>
                      where: <br>
                      Amt = Total amount (Principal + Interest) <br>
                      Prpl = Principal amount <br>
                      Int = Interest amount <br>
                      rate = Rate of interest per year, in decimal; r=R/100 <br>
                      time = Time period invested in years/quarters
</div>
</div>
</div>
</div>
</div>
</div><!--/html_preserve-->

Code - Server.R
========================================================


```r
library(shiny)
library(dplyr)
library(stats)
library(base)
# Define server logic required to draw a histogram
# Define server logic required to draw a histogram
shinyServer(function(input, output) {
  values <- reactiveValues()
  
  # Calculate the interest and amount    
  observe({
    input$action_Calc
    values$int <- isolate({
      input$num_principal * input$slider_intrate *
        recode(input$select_time, '1' = 1, '2' = 0.25)/100 * input$slider_num  
    })
    values$amt <- isolate(input$num_principal) + values$int
  })
  
  # Display values entered
  output$text_principal <- renderText({
    input$action_Calc
    paste("Principal Amount: [$]", isolate(input$num_principal))
  })
  
  output$text_intrate <- renderText({
    input$action_Calc
    paste("Interest Rate: ", isolate(input$slider_intrate), 
          " % per year")
  })
  
  output$text_num <- renderText({
    input$action_Calc
    paste("Time Period ", isolate(input$slider_num),
          recode(isolate(input$select_time),
                 '1' = 'Years', '2' = 'Quarters')
    )
  })
  
  output$text_int <- renderText({
    if(input$action_Calc == 0) ""
    else
      paste("Simple Interest [$]:", values$int)
  })
  
  output$text_amt <- renderText({
    if(input$action_Calc == 0) ""
    else 
      paste("Total Amount, i.e. Principal + Interest [$]:", values$amt)
  })
  
})
```
